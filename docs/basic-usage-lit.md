# Basic Usage with Lit

This section provides a complete, framework-agnostic example of how to connect to the hREA backend from a user interface. We will use [Lit](https://lit.dev/), a simple library for building fast, lightweight web components. Because Lit is based on native Web Components, these patterns can be easily adapted to any other framework or even vanilla JavaScript.

This guide assumes you have followed the **[Integration Guide](integration-guide.md)** and have your backend configured.

### 1. UI File Structure

In your scaffolded project, navigate to the `ui/` directory. We will create the following file structure:

```
ui/
├── src/
│   ├── holochain-client.ts  # Core logic for connecting to Holochain & hREA
│   ├── client-provider.ts   # A component to provide the client to the app
│   └── hrea-test.ts         # The example component with buttons and results
│   └── index.css            # Styles
├── index.html               # The main HTML file
└── ... (other config files)
```

### 2. Add Lit Dependency

If you didn't choose Lit during the scaffolding, you'll need to add it to your `ui/package.json`:

```bash
cd ui
npm install lit @lit-labs/context
```

### 3. The Code

Here is the full code for each of the files.

#### `src/holochain-client.ts`

This file contains the core, framework-agnostic logic for establishing the connection to Holochain and creating the Apollo GraphQL client for hREA.

```typescript
import { ApolloClient, InMemoryCache, type ApolloClientOptions } from "@apollo/client/core";
import { SchemaLink } from "@apollo/client/link/schema";
import type { AppClient } from "@holochain/client";
import { AppWebsocket } from "@holochain/client";
import { createHolochainSchema } from "@valueflows/vf-graphql-holochain";
import { createContext } from '@lit-labs/context';

// This is the data that will be passed down via context
export interface HreaClientContext {
  holochainClient: AppClient,
  hreaClient: ApolloClient<any>,
}

// Lit context key for the hrea client context
export const hreaClientContext = createContext<HreaClientContext>('hrea-client-context');

/**
 * Main class to manage Holochain and hREA connections.
 */
export class HolochainConnection {
  
  public appWebsocket!: AppWebsocket;
  public holochainClient!: AppClient;
  public hreaClient!: ApolloClient<any>;

  public status: 'initializing' | 'connected' | 'error' = 'initializing';
  public error?: any;

  constructor(private onStatusUpdate: (status: string, error?: any) => void) {}

  public async connect() {
    try {
      this.onStatusUpdate('connecting-holochain');
      this.appWebsocket = await AppWebsocket.connect();
      this.holochainClient = this.appWebsocket.appClient({
        installed_app_id: 'hrea-work-testing',
      });

      this.onStatusUpdate('initializing-hrea');
      const schema = await createHolochainSchema({
        holochainClient: this.holochainClient,
        dnaRoleName: "hrea", 
      });

      const options: ApolloClientOptions<any> = {
        cache: new InMemoryCache(),
        link: new SchemaLink({ schema }),
        defaultOptions: {
          query: { fetchPolicy: "cache-first" },
          mutate: { fetchPolicy: "no-cache" },
        },
      };

      this.hreaClient = new ApolloClient(options);
      
      this.status = 'connected';
      this.onStatusUpdate('connected');

    } catch (e) {
      console.error("Error connecting to Holochain and hREA", e);
      this.status = 'error';
      this.error = e;
      this.onStatusUpdate('error', e);
    }
  }

  public getContext(): HreaClientContext {
    if (this.status !== 'connected') {
      throw new Error("Cannot get context when not connected.");
    }
    return {
      holochainClient: this.holochainClient,
      hreaClient: this.hreaClient,
    }
  }
}
```

#### `src/client-provider.ts`

This is a wrapper component. Its only job is to connect to Holochain and then provide the client instances to all of its child components via Lit's context API.

```typescript
import { LitElement, html, css } from 'lit';
import { customElement, state, property } from 'lit/decorators.js';
import { ContextProvider } from '@lit-labs/context';

import { HolochainConnection, hreaClientContext, type HreaClientContext } from './holochain-client';

@customElement('client-provider')
export class ClientProvider extends LitElement {
  
  // Setup the context provider
  private provider = new ContextProvider(this, {context: hreaClientContext});

  @state()
  private connection: HolochainConnection;

  @state()
  private statusMessage: string = "Initializing...";

  constructor() {
    super();
    // Create a new HolochainConnection instance, passing a callback
    // to update the status message on this component.
    this.connection = new HolochainConnection((status: string, error?: any) => {
      switch(status) {
        case 'connecting-holochain':
          this.statusMessage = "Connecting to Holochain...";
          break;
        case 'initializing-hrea':
          this.statusMessage = "Initializing hREA GraphQL schema...";
          break;
        case 'connected':
          this.statusMessage = "Connected!";
          // When connected, set the value for the context provider
          this.provider.setValue(this.connection.getContext());
          break;
        case 'error':
          this.statusMessage = `Error: ${error?.message || 'Unknown error'}`;
          break;
      }
    });
  }

  firstUpdated() {
    // Start the connection process when the component is first added to the DOM
    this.connection.connect();
  }

  render() {
    if (this.connection.status === 'connected') {
      // If connected, render the child components that were passed in.
      return html`<slot></slot>`;
    } else {
      // Otherwise, show a loading/error message.
      return html`
        <div class="status ${this.connection.status}">
          <div class="spinner"></div>
          <p>${this.statusMessage}</p>
        </div>
      `;
    }
  }

  static styles = css`
    /* Add styles for spinner and status messages here */
    .status {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 200px;
      padding: 40px 20px;
    }
    .error { color: #ff6b6b; }
    /* ... etc ... */
  `;
}
```

#### `src/hrea-test.ts`

This component consumes the context provided by `<client-provider>` and uses the Apollo Client to send queries and mutations to hREA.

```typescript
import { LitElement, html, css } from 'lit';
import { customElement, state } from 'lit/decorators.js';
import { ContextConsumer } from '@lit-labs/context';
import { hreaClientContext, type HreaClientContext } from './holochain-client';
import { gql, type ApolloClient } from '@apollo/client/core';

@customElement('hrea-test')
export class HreaTest extends LitElement {

  // Setup the context consumer
  private consumer = new ContextConsumer(this, {
    context: hreaClientContext,
    subscribe: true // Re-render when the context value changes
  });

  @state()
  private results: string[] = [];

  @state()
  private isLoading: boolean = false;
  
  private get hreaClient(): ApolloClient<any> | undefined {
    return this.consumer.value?.hreaClient;
  }

  private async createPerson() {
    if (!this.hreaClient) return;
    this.isLoading = true;
    this.results = [...this.results, "🔧 Creating a person agent..."];
    try {
      const result = await this.hreaClient.mutate({
        mutation: gql`
          mutation CreatePerson($person: AgentCreateParams!) {
            createPerson(person: $person) {
              agent { id, name }
            }
          }
        `,
        variables: {
          person: {
            name: `Person ${Date.now()}`,
            note: "Created via Lit example",
          },
        },
      });
      const agent = result.data.createPerson.agent;
      this.results = [...this.results, `✅ Person created: ${agent.name}`];
    } catch (e) {
      this.results = [...this.results, `❌ Failed to create person: ${(e as Error).message}`];
    } finally {
      this.isLoading = false;
    }
  }
  
  // Add other methods like createOrganization, queryAgents etc. here
  // ...

  render() {
    if (!this.consumer.value) {
      return html`<p>Waiting for HREA client...</p>`
    }

    return html`
      <div class="hrea-example">
        <h2>hREA Basic Example (Lit)</h2>
        <div class="buttons">
          <button @click=${this.createPerson} .disabled=${this.isLoading}>
            Create Person
          </button>
          <!-- Add other buttons here -->
        </div>
        <div class="results">
          <h3>Results:</h3>
          <div class="results-container">
            ${this.results.map(r => html`<div class="result-line">${r}</div>`)}
          </div>
        </div>
      </div>
    `;
  }

  static styles = css`
    /* Add styles for buttons, results, etc. */
  `;
}
```

#### `index.html`

Finally, your `ui/index.html` ties everything together.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>hREA Lit Example</title>
    <link rel="stylesheet" href="/src/index.css" />
  </head>
  <body>
    <client-provider>
      <h1>hREA Lit Integration</h1>
      
      <hrea-test></hrea-test>

    </client-provider>

    <script type="module">
      import './src/client-provider.ts';
      import './src/hrea-test.ts';
    </script>
  </body>
</html>
```

### 4. How It Works

1.  **`index.html`** loads the `<client-provider>` component.
2.  **`client-provider.ts`** is rendered. Its `firstUpdated` lifecycle method triggers the `connect()` method in our `HolochainConnection` class.
3.  While connecting, it displays a "Connecting..." status message.
4.  Once the connection is successful, `HolochainConnection` creates the Apollo Client for hREA and calls the status update callback.
5.  The `ClientProvider` receives the 'connected' status and sets the `hreaClientContext` value, passing down the client instances. It then renders its `<slot>`, which contains the `<hrea-test>` component.
6.  **`hrea-test.ts`** consumes the context. Now that it has a value, it renders the UI with the buttons.
7.  When you click a button, a method like `createPerson` is called, which uses the `this.hreaClient` instance to send a GraphQL mutation.
8.  The results are added to the component's reactive `results` state, causing the UI to re-render and display the outcome. 