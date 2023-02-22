---
description: >-
  This guide is intended to assist with bringing the library into your project
  which enables making GraphQL calls into the holochain-based hREA 'backend'.
---

# Quick Start - Integrate

First, this guide assumes that you have a nodejs project which uses `npm` to manage dependencies. You can replace `npm` commands with the relevant commands for your package manager of choice. The main library we are dealing with the interface of here is this library: `@vf-ui/graphql-client-holochain`, hosted on `npm`.

From your terminal, navigate to the folder where your project source files are located within.

Run the following commands:

`npm install --save @vf-ui/graphql-client-holochain`

`npm install --save graphql@15.8`

### Pointing the client to the holochain service

Assuming that [you installed and are running an hREA "hApp" within a holochain service](running-hrea-backend.md), you need to provide three details to your client in order to know how to connect to, and make requests, of the holochain service. An "app id", an "app websocket url" and an "admin websocket url". Here's the quickest way to do that:

To your package.json startup command, whatever it is, add this as a prefix to the rest of the command:

```
REACT_APP_HC_APP_ID='hrea_suite' REACT_APP_HC_CONN_URL='ws://localhost:4000' REACT_APP_HC_ADMIN_CONN_URL='ws://localhost:4001'
```

So that it looks something like this:

```json
  "scripts": {
    "start": "REACT_APP_HC_APP_ID='hrea_suite' REACT_APP_HC_CONN_URL='ws://localhost:4000' REACT_APP_HC_ADMIN_CONN_URL='ws://localhost:4001' node index.js"
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

When running a holochain service, it will always need to open an admin level websocket server, over which secure administration requests can be sent to holochain to control it. The URL of this websocket server can be constructed similar to the following, based on whatever port the 'Admin Websocket' service is declared by holochain to be running, such as `4001`.&#x20;

{% hint style="info" %}
If you are looking to release to the [**Holochain Launcher**](https://github.com/holochain/launcher), during your build process, if you have one, make sure to set both of these values to '' empty, as the Launcher will assist your client to negotiate these values automatically through some ['magical introspection'](https://github.com/holochain/holochain-client-js/blob/cc9563ca5db448cd03f7e298e4fd71fc1625cbcd/src/environments/launcher.ts).&#x20;
{% endhint %}

### Imports

In whatever entry point file is most relevant for you, add these lines to your imports:

```javascript
import graphqlClientHolochain from '@vf-ui/graphql-client-holochain'
```

### Variables to hold in memory

Elsewhere in your code, somewhere near the entry point and in a high level or global scope, trigger the websocket to be connected, and the Graphql Schema to be set up.

```javascript
    const client = await graphqlClientHolochain()
```

The `client` is an instance of an `ApolloClient` from the `@apollo/client` npm library.&#x20;

Everything is configured now, and you're ready to make your first requests!&#x20;

To continue with this, see Step 4 and beyond in this @apollo/client getting started tutorial: [https://www.apollographql.com/docs/react/get-started](https://www.apollographql.com/docs/react/get-started/#step-4-connect-your-client-to-react)&#x20;
