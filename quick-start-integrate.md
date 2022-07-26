---
description: >-
  This guide is intended to assist with bringing the library into your project
  which enables making GraphQL calls into the holochain-based hREA 'backend'.
---

# Quick Start - Integrate

First, this guide assumes that you have a nodejs project which uses `npm` to manage dependencies. You can replace `npm` commands with the relevant commands for your package manager of choice. The main library we are dealing the interface of here is this library: `@valueflows/vf-graphql-holochain`.

From your terminal, navigate to the folder where your project source files are located within.

Run the following commands:

`npm install --save @valueflows/vf-graphql-holochain`

`npm install --save graphql@16.2.0`

### Pointing the client to the holochain service

Assuming that you installed and are running an hREA "hApp" within a holochain service, you need to provide two details to your client in order to know how to connect to, and make requests, of the holochain service. An "app id" and a "websocket url". Here's the quickest way to do that:

To your package.json startup command, whatever it is, add this as a prefix to the rest of the command:

```
REACT_APP_HC_APP_ID='hrea_suite' REACT_APP_HC_CONN_URL='ws://localhost:4000'
```

So that it looks something like this:

```json
  "scripts": {
    "start": "REACT_APP_HC_APP_ID='hrea_suite' REACT_APP_HC_CONN_URL='ws://localhost:4000' node index.js"
  },
```

{% hint style="info" %}
As an alternative to this, use the [dotenv](https://www.npmjs.com/package/dotenv) library or set these environment variables however you choose.
{% endhint %}

#### Knowing What The Values Should Be, and What They Mean

When installing a 'hApp' to holochain, each hApp must be given a unique identifier. Whatever the value of the `installed_app_id` value given to holochain for the hREA happ, that value is what should be used instead of 'hrea\_suite'.

`REACT_APP_HC_APP_ID='hrea_suite'`&#x20;

When running a holochain service, it can be instructed to setup a websocket server, over which requests can be made. The URL of this websocket server can be constructed similar to the following, based on whatever port the 'App Websocket' service is declared by holochain to be running, such as `4000`.&#x20;

`REACT_APP_HC_CONN_URL='ws://localhost:4000'`

{% hint style="info" %}
`If you are looking to release to the Holochain Launcher, during your build process, if you have one, make sure to set both of these values to '' empty, as the Launcher will assist your client to negogiate these values automatically through some` [`'magical introspection'`](https://github.com/holochain/holochain-client-js/blob/cc9563ca5db448cd03f7e298e4fd71fc1625cbcd/src/environments/launcher.ts)`.`&#x20;
{% endhint %}

### Imports

In whatever entry point file is most relevant for you, add these lines to your imports:

```javascript
import bindSchema, { autoConnect, VfModule } from '@valueflows/vf-graphql-holochain'
```

### Variables to hold in memory

Elsewhere in your code, somewhere near the entry point and in a high level or global scope, trigger the websocket to be connected, and the Graphql Schema to be set up.

```javascript
    const { dnaConfig, conductorUri } = await autoConnect()
    const schema = await bindSchema({ dnaConfig, conductorUri })
```

From here on out, the implementation details depend on which javascript framework (or not) you're using.

<details>

<summary>Apollo Client (React, or others)</summary>

In addition to the above, follow these additional steps.



Run this command:

`npm install --save @apollo/client@3.5.7`



In whatever entry point file is most relevant for you, add these lines to your imports:

```javascript
import {
  ApolloClient,
  ApolloProvider,
  InMemoryCache,
  NormalizedCacheObject,
  gql,
} from '@apollo/client'
import { SchemaLink } from '@apollo/client/link/schema'
```



Assuming that you have the variable `schema` defined in scope, as outlined in the initial section of this page, add the following line just after it.

```javascript
const link = new SchemaLink({ schema })
const cache = new InMemoryCache()
const client = new ApolloClient({
  cache: cache,
  link: link,
})
```

Everything is configured now, and you're ready to make your first requests!&#x20;

To continue with this, see Step 4 and beyond in this @apollo/client getting started tutorial: [https://www.apollographql.com/docs/react/get-started](https://www.apollographql.com/docs/react/get-started)



</details>
