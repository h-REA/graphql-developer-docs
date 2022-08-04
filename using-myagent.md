---
description: How to conceptualize and utilize agency and identity with Holochain and hREA
---

# Using "myAgent"

## Background

There are some basic assumptions about Holochain that we need to establish in order to understand hREA and how it works.&#x20;

Rather than utilizing an email address and password combination, Holochain utilizes a set of cryptographic "private keys" stored on the end users local file system to represent your personal "account". There is no centralized database of accounts, nor are there 'forgot password' by email reset mechanisms. All of that is gone.

Depending on how the end user is accessing Holochain, their keys may have been generated at different points in their registration process. Suffice to say, at some point the user needs to generate a private key / public key pair with Holochain in order to run hREA, and that hREA will be installed under the agency of one (1) specific private/public key pair. The public key half of this combination may appear within the API labeled as an `agentPubKey` value.

Conceptually, every request to hREA occurs within the context of a specific `AgentPubKey`, or identity. It is known implicitly within the internal hApp context, and that is why it DOES NOT need to passed over API requests, as one might with an API token in more typical web architectures.

**In short, user identity is known implicitly during every API request, and doesn't need to be provided in the request as a value.**&#x20;

There are a set of special GraphQL API endpoints provided for this common use case of providing the "current user" with information about themselves. Let's explore this.

## R-E-Agent

in the Resource-Event-Agent model, their is a primitive known as "Agent". In `hREA` there are multiple sub-types of "Agent", but they are all "Agents". Two such examples are "Person" and "Organization". All Resources and Events likely contain references to an "Agent".&#x20;

"Agent"s are explicitly recorded in the system, and are different than the notion of devices which hREA running and have joined the network of peers. Any given device **may OR may not** be associated with one such "Agent" record.&#x20;

Therefore there is a need for three specific GraphQL endpoints related to this:&#x20;

1. If the current user/device is associated with an Agent, return it. This is `myAgent`
2. Allow for the creation of new Agent records. This is `createPerson` or `createOrganization`
3. Allow an Agent record to become associated with a user/device, represented by an AgentPubKey. This is `associateMyAgent`

### myAgent

In a typical application flow, we would see `myAgent` called to check if the active user has associated their device with an Agent. It will return an error if none has been.&#x20;

An example query

```graphql
query MyQuery {
  myAgent {
    id
  }
}
```

An example error, which just tells the developer no Agent has been associated to this identity

```graphql
{
  "errors": [
    {
      "message": "Unexpected error value: { type: \"error\", data: { type: \"ribosome_error\", data: \"Wasm error while working with Ribosome: Guest(\\\"No Agent data is associated with the currently authenticated user\\\")\" } }",
      "locations": [
        {
          "line": 2,
          "column": 3
        }
      ],
      "path": [
        "myAgent"
      ]
    }
  ],
  "data": {
    "myAgent": null
  }
}
```

### createPerson

From a given device, `createPerson` may be called as many times as desired, and does not imply that the created Person will be associated with the currrent device, other than in its metadata history.&#x20;

Here is example GraphQL:

```graphql
mutation CreatePerson {
  createPerson(person: { name: "Luke Skywalker" }) {
    agent {
      id
      name
    }
  }
}
```

Here is an example response to that:

```graphql
{
  "data": {
    "createPerson": {
      "agent": {
        "id": "uhCEkhEPmOsgnVv1HCno3T5XbNPl3g8xOf3HxWUGhykVwjGyHDRGH:uhC0kyzFVhHjoqf2ZvsH6FmNQ16DC4EtjD1OIsFbNwJGMBZyVGV3w",
        "name": "Luke Skywalker"
      }
    }
  }
}
```

The value to pay close attention to there is `data.createPerson.agent.id`. That value is the "Agent ID" and we need to reference it in the following example.

### associateMyAgent

So that `myAgent` will return a real Agent next time, we need to call `associateMyAgent`. Here is an example:

```graphql
mutation AssociateMyAgent {
  associateMyAgent(agentId: "uhCEkhEPmOsgnVv1HCno3T5XbNPl3g8xOf3HxWUGhykVwjGyHDRGH:uhC0kyzFVhHjoqf2ZvsH6FmNQ16DC4EtjD1OIsFbNwJGMBZyVGV3w")
}
```

The value can be any valid Agent ID, such as the value `data.createPerson.agent.id` from the example `createPerson` response.&#x20;

This simply returns `true` if the request was successful. Now, `myAgent` can be called again, and will return data for that Agent, instead of an error!
