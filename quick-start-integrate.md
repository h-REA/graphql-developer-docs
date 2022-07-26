---
description: >-
  This guide is intended to assist with bringing the library into your project
  which enables making GraphQL calls into the holochain-based hREA 'backend'.
---

# Quick Start - Integrate

First, this guide assumes that you have a nodejs project which uses `npm` to manage dependencies. You can replace `npm` commands with the relevant commands for your package manager of choice.

From your terminal, navigate to the folder where your project source files are located within.

Run the following commands:

`npm install --save @valueflows/vf-graphql-holochain`

`npm install --save graphql@16.2.0`



In whatever entry point file is most relevant for you, add these lines to your imports:

```javascript
import bindSchema, { autoConnect, VfModule } from '@valueflows/vf-graphql-holochain'
```



Elsewhere in your code, to set up the Graphql Schema

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
