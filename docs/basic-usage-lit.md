# Basic Usage

A complete example of connecting a user interface to hREA. The connection module is framework agnostic; the component at the end uses [Lit](https://lit.dev/), which is close enough to plain web components that the pattern ports to anything.

This page assumes you followed the **[Integration Guide](integration-guide.md)** and have the `hrea` role in your hApp manifest.

## 1. The connection module

The adapter does one thing: it builds an executable GraphQL schema whose resolvers call into the hREA cell. You bring your own GraphQL client.

```typescript title="src/hrea-client.ts"
import { AppWebsocket } from '@holochain/client'
import { createHolochainSchema } from '@valueflows/vf-graphql-holochain'
import { ApolloClient, InMemoryCache } from '@apollo/client/core'
import { SchemaLink } from '@apollo/client/link/schema'

export async function connectHrea(roleName = 'hrea') {
  // In the Holochain Launcher, or in a dev UI started by `hc spin`, the
  // connection details come from the environment and `connect()` needs no
  // arguments. Outside that, pass { url, token } yourself.
  const appWebSocket = await AppWebsocket.connect()

  // Synchronous: it returns a GraphQLSchema, not a promise. `roleName` must
  // match the role you declared in workdir/happ.yaml.
  const schema = createHolochainSchema({ appWebSocket, roleName })

  return new ApolloClient({
    link: new SchemaLink({ schema }),
    cache: new InMemoryCache(),
    defaultOptions: {
      query: { fetchPolicy: 'no-cache' },
      mutate: { fetchPolicy: 'no-cache' },
    },
  })
}
```

!!! note "Two things that changed in `happ-0.5.0-beta.1`"

    The adapter takes `{ appWebSocket, roleName }`. Earlier documentation showed `{ holochainClient, dnaRoleName }`, which no longer matches the shipped signature.

    `createHolochainSchema` is synchronous. `await` in front of it is harmless but says something untrue about the API.

!!! tip "Caching"

    The example turns Apollo's cache off for clarity, which is what the acceptance suite does so that every assertion hits the DHT. A real application usually wants `cache-first` for queries. Mutations should stay uncached.

## 2. A first query

Agents are the simplest place to start. Collection queries are Relay-style connections, so results arrive under `edges { node { ... } }`.

```typescript
import { gql } from '@apollo/client/core'

const ALL_AGENTS = gql`
  query {
    agents {
      edges {
        node {
          id
          name
          note
        }
      }
    }
  }
`

const client = await connectHrea()
const { data } = await client.query({ query: ALL_AGENTS })
const agents = data.agents.edges.map((e: any) => e.node)
```

## 3. A first mutation

```typescript
const CREATE_PERSON = gql`
  mutation ($person: AgentCreateParams!) {
    createPerson(person: $person) {
      agent {
        id
        revisionId
        name
      }
    }
  }
`

const { data } = await client.mutate({
  mutation: CREATE_PERSON,
  variables: { person: { name: 'Ada Lovelace', note: 'first contributor' } },
})
```

Every mutation response wraps the record in a named field (`agent` here, `proposal` for proposals, and so on), and every record carries both `id` and `revisionId`. Updates and deletes take the `revisionId`, not the `id`: hREA records are append-only, and the revision is what identifies the version you are amending.

## 4. Offers and requests

`Proposal.purpose` is the ValueFlows 1.0 field that distinguishes an offer from a request, and hREA exposes two queries that partition on it:

```typescript
const OFFERS = gql`
  query {
    offers {
      edges {
        node {
          id
          name
          purpose
          publishes { id }
        }
      }
    }
  }
`
```

Create one by setting `purpose` on the proposal:

```typescript
const CREATE_OFFER = gql`
  mutation ($proposal: ProposalCreateParams!) {
    createProposal(proposal: $proposal) {
      proposal { id purpose }
    }
  }
`

await client.mutate({
  mutation: CREATE_OFFER,
  variables: {
    proposal: {
      name: 'Two hours of welding',
      purpose: 'offer',        // or 'request'
      publishes: [intentId],
    },
  },
})
```

## 5. Wiring it into a component

```typescript title="src/hrea-demo.ts"
import { LitElement, html } from 'lit'
import { customElement, state } from 'lit/decorators.js'
import type { ApolloClient } from '@apollo/client/core'
import { connectHrea } from './hrea-client.js'

@customElement('hrea-demo')
export class HreaDemo extends LitElement {
  @state() private client?: ApolloClient<any>
  @state() private agents: any[] = []
  @state() private error?: string

  async connectedCallback() {
    super.connectedCallback()
    try {
      this.client = await connectHrea()
      await this.loadAgents()
    } catch (e: any) {
      this.error = e?.message ?? String(e)
    }
  }

  private async loadAgents() {
    const { data } = await this.client!.query({ query: ALL_AGENTS })
    this.agents = data.agents.edges.map((e: any) => e.node)
  }

  render() {
    if (this.error) return html`<p>Could not connect: ${this.error}</p>`
    if (!this.client) return html`<p>Connecting…</p>`
    return html`
      <ul>
        ${this.agents.map(a => html`<li>${a.name}</li>`)}
      </ul>
    `
  }
}
```

## Where to go next

- The **[GraphQL API Reference](reference/graphql-api-reference/README.md)** lists every type, query and mutation, and says which ones are declared in the schema but not yet backed by the DNA.
- **[Consuming a release](consuming-a-release.md)** covers artifact choice, version pinning, and what changed between releases.
