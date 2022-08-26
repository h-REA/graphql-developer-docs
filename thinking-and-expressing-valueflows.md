---
description: >-
  This is a walk-through to help you learn to think about the world in terms of
  ValueFlows, and to practice expressing real world occurrences through the
  vocabulary.
---

# Thinking & Expressing ValueFlows

If you have gone through the [Quick Start - API Explorer](quick-start.md) setup, you will be seeing something like the following screen.

![a web browser with 3 panels lined up horizontally, the left has code in it, the middle is empty, and right has some developer documentation](https://i.imgur.com/14flkez.png)

It is a user interface, but isn't an "end user application". It is a "graphiql" explorer, built for mostly for engaging as a developer with a ["graphql"](https://graphql.org/) application programming interface (API). However, anyone can use it, and you're encouraged you to stick with this, and see what you can do. [https://github.com/graphql/graphiql](https://github.com/graphql/graphiql). The "i" stands for "interactive".

This interface is super handy for testing and getting to know the ValueFlows data structures and functions.

We can imagine a different "end user interface" making the same underlying graphql queries and mutations as we will make using this more developer-centric user interface.

So of course we want to know what we can do with it, so let's find out!

### Making Any Sense of ValueFlows

`hREA` is an implementation of a specification, [ValueFlows](https://www.valueflo.ws). It implements the ValueFlows ["vocabulary"](https://www.w3.org/standards/semanticweb/ontology) with [holochain](https://holochain.org) as the database and networking service.

At first while exploring them, the ValueFlows vocabulary (terms and data types) can feel very foreign and dense. Following is a selection from some of the more concise references, the ones that are the easiest to understand and get started with.

What is intimidating about ValueFlows is its seeming expansiveness, the huge scope of everything it covers, everything it is. For this reason, when starting to learn about it, it can be easiest to focus on the level of the "REA", Resources - Events - Agents, these original and central aspects, before allowing ourselves to explore to the other corners of the vocabulary. If you agree, just keep in mind, there is so much more to it than this, and this is only the beginning! ;)

"In ValueFlows you (and everyone) are an **Economic Agent**". [_source_](https://speakerdeck.com/mikorizal/everything-in-valueflows-is-connected?slide=3)

"You are connected to all of the **Economic Events** you have participated in. They may be many types of Events: Work, Production, Consumption, etc." [_source_](https://speakerdeck.com/mikorizal/everything-in-valueflows-is-connected?slide=5)

"**Economic Events** change **Economic Resources**. They may (for example) create, consume, use, cite, provide, or transfer Resources." [_source_](https://speakerdeck.com/mikorizal/everything-in-valueflows-is-connected?slide=6)

**Economic Events** fall under a category that ValueFlows calls "Observations". Observations are "a record of what actually happened". [_source_](https://lab.allmende.io/valueflows/vf-schemas/vf-graphql/-/blob/sprout/lib/schemas/observation.gql)

A **Process** is an activity that transforms input Economic Resources (sent in by Economic Events) into output Economic Resources. A Process can and often does have many inputs and outputs. The Process itself has a beginning and end time. [_more info_](https://www.valueflo.ws/concepts/processes/)

![ source](https://i.imgur.com/IPK5qV2.png)

In this example "Cook Salsa Today" is a **Process**, "consumed 6 lb Diced Tomato lot 234" is an **Economic Event** that refers to the pre-existing "Diced Tomato lot 234" **Economic Resource** and "produced 6 lb Salsa Bulk lot 456" is an **Economic Event** that results in the new **Economic Resource** "Salsa Bulk lot 456".

Below is a more abstract version, which connects many Events, Resources, and Processes.&#x20;

![ source](https://i.imgur.com/7jP14nr.png)

If you are wondering where the "Agents" are in this situation, they are most likely the ones "doing the work", and would be referenced in particular by **Economic Events**.

### Expressing in ValueFlows

Now we want to try to express an **Economic Event** of some kind.

We might start by thinking about the day to day economics of our own life, to start grounding it.

Things like:

* I buy groceries, make and eat food, and dispose of food and other waste, as well as place things in recycling.
* I consume water, both into my body as well as during showering and washing.
* I use my computer a great deal, primarily for the economic activities of running my business, doing consulting work, and writing software

How might we express these activities using ValueFlows?

The docs on the right hand side can be helpful if we explore them

![](https://i.imgur.com/HJGxPhF.png)

In Graphql, a **Query** is anything that ONLY reads data, and does not change (mutate) that data in any way. Oppositely, a **Mutation** is meant to be used to alter a database or persisted data of some kind. It could potentially be used to create new things, update existing things, or delete them (in the case of holochain, just "tombstone" them, they aren't gone gone).

We are interested in mutations first of all, because we want to make stuff happen!

Clicking on `mutation: Mutation` we get a long list!

This gives us a sense of all the things that could be done here. However, here are a subset of the functions, simplified to just their names, that seem to relate to the most basic areas we are interested in:

```
createEconomicEvent

createProcess
```

### Creating an Economic Event

Finally, let's focus on the function: `createEconomicEvent`. Let's try to make an "Observation".

We click on the `createEconomicEvent` function to take a closer look at the "function signature", which is what type of data does the function expect as an input, and what type of data can it be expected to return as a result, if successful (it could also return an error)

![](https://i.imgur.com/DVTcFdv.png)

It will return a `EconomicEventResponse`, and expects at least one input, but possibly two inputs, `EconomicEventCreateParams` and `EconomicResourceCreateParams`. The `!` indicates a required portion of the input, the `EconomicEventCreateParams`.

It does not have a description, which could have been useful. A few of the other functions did have a description.

We look at `EconomicEventCreateParams`, by clicking on it. It has lots of potential fields on it.

| ![](https://i.imgur.com/dEcWYPK.png) | ![](https://i.imgur.com/NHlwJnz.png) | ![](https://i.imgur.com/t1bKKeN.png) | ![](https://i.imgur.com/beOyt1D.png) |
| ------------------------------------ | ------------------------------------ | ------------------------------------ | ------------------------------------ |

Out of all of them, only 3 are marked as required (`!`), we may find that deceptively simple though.

The 3 marked as required are: `action`, `provider`, and `receiver`

`provider` and `receiver` say that they expect the `ID` of an `Agent`. This should be something like the `id` field of the response to our original `myAgent` query, but ideally has two separate agents given as provider and receiver: ourselves, and one other.

`action` says it expects the `ID` of an `Action`. We don't know what an `Action` is. We will have to find out.

Let's get to trying this out.

Closing the Docs on the right panel, we switch over to using the other "Explorer" which actually helps with query building.

![](https://i.imgur.com/ezUlmtH.png)

We select 'Mutation' at the bottom, and click the '+'.

![](https://i.imgur.com/6udosZe.png)

Under the "Explorer", we click on `createEconomicEvent` in the list, to fill it in in the query panel.

We see that the required fields are already added in as empty values.

![](https://i.imgur.com/D3EZE9W.png)

Because we're going to need valid agent `ID`s for `provider` and `receiver` we can plug in our own agent ID to both. In the future we may want to have another agent's `ID` to add as one or the other, to represent a transfer.

Use the following query in order to retrieve your own agent ID.&#x20;

{% hint style="warning" %}
This will ONLY work if you have gone through the first two steps of the [Quick Start - API Explorer](quick-start.md) tutorial, or otherwise called `associateMyAgent`
{% endhint %}

```graphql
{
  myAgent {
    id
    name
  }
}
```

Running it we get something like this:

![](https://i.imgur.com/NbkK737.png)

We just asked the API the question: "Who am I?"

We find out we are the agent identified by this very long string value : `uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO`

The system represents an ID as one whole string value containing two parts, with that colon separator in the middle. This is important. Throughout all that comes next, we need to reference agent IDs, like this one.

```graphql
mutation FirstEconomicEvent {
  createEconomicEvent(event: {
    action: "",
    provider: "uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO",
    receiver: "uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO"
  })
}
```

Firstly, we need to fix our query so that we also return some portion of the response. We can select what we want off it, let's just pick `id` off of `economicEvent` on the response for now.

```graphql
mutation FirstEconomicEvent {
  createEconomicEvent(event: {action: "", provider: "uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO", receiver: "uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO"}) {
    economicEvent {
      id
    }
  }
}
```

`action` is still empty. So what do we put there?

Well, we can get the full list of options with this query:

```graphql
query ListAllActions {
  actions {
    id
  }
}
```

When we 'Play' it, we get something like the following (with adjusted formatting):

```json
{"data":{"actions":[
  {"id":"dropoff"},
  {"id":"pickup"},
  {"id":"consume"},
  {"id":"use"},
  {"id":"work"},
  {"id":"cite"},
  {"id":"produce"},
  {"id":"accept"},
  {"id":"modify"},
  {"id":"pass"},
  {"id":"fail"},
  {"id":"deliver-service"},
  {"id":"transfer-all-rights"},
  {"id":"transfer-custody"},
  {"id":"transfer"},
  {"id":"move"},
  {"id":"raise"},
  {"id":"lower"}
]}}
```

So that looks good. We can use one of these verbs as the `Action` `ID`.

A minimal explanation of these various **Action**'s is available here: [https://www.valueflo.ws/concepts/actions/](https://www.valueflo.ws/concepts/actions/).

Building an understanding of these different verbs will be a critical layer to understanding `hREA` well.

We find from the list one that seems useful and simple: `raise`: "adjusts a quantity up based on a beginning balance or inventory count".

```graphql
mutation FirstEconomicEvent {
  createEconomicEvent(event: {
    action: "raise",
    provider: "uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO",
    receiver: "uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO"
  }) {
    economicEvent {
      id
    }
  }
}
```

We've got all the "required" fields filled out. This could work. We hit play to find out.

We get back an error:

```
EconomicEvent must reference an inventoried resource,
resource specification or resource classification
```

Ok! That's progress. We don't mind an error message if it's instructive.

Now, (skipping over a couple of steps of back and forth with the system, of getting the right fields in place to make a functional `createEconomicEvent),` we have a working query that looks like this:

```graphql
mutation FirstEconomicEvent {
  createEconomicEvent(
    event: {action: "raise", provider: "uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO", receiver: "uhCAkMrhQvJznARbU6HGnDrdMk-eMbEDE7B8GnBDA66wCv0R4UX6f:uhC0k646zXkQKNvC0vhEkQxW-iGgoILG4-QtrdUyDNdzoCbRkOMXO", resourceClassifiedAs: "https://some-schema.com/lettuce", resourceQuantity: {hasNumericalValue: 3}, hasPointInTime: "2022-02-20T01:30:15.01-08:00"}
  ) {
    economicEvent {
      id
      action {
        id
      }
      resourceClassifiedAs
      resourceQuantity {
        hasNumericalValue
      }
      hasPointInTime
    }
  }
}
```

This works! We get as a response:

```json
{
  "data": {
    "createEconomicEvent": {
      "economicEvent": {
        "id": "uhCEkIwCORIp1w6e6n71ncHOMRMG3Bn188_UKLJLcW7WAsu5TPO-w:uhC0koJqjCLtl6BlWqHmg_1J8jqH6DNbsPdjfG2E-0XqEgVM9ApjB",
        "action": {
          "id": "raise"
        },
        "resourceClassifiedAs": [
          "https://some-schema.com/lettuce"
        ],
        "resourceQuantity": {
          "hasNumericalValue": 3
        },
        "hasPointInTime": "2022-02-20T09:30:15.010Z"
      }
    }
  }
}
```

That is the `id` of our new Economic Event! Give it a try.

The `resourceClassifiedAs` field satisfies the original error message. It seems to be replaceable with `resourceConformsTo` or `resourceInventoriedAs`.

`resourceQuantity` being set satisfies an error message that said: "EconomicEvent must include either a resource quantity or an effort quantity"

`hasPointInTime` being set satisfies an error message that said: "EconomicEvent must have a beginning, end or exact time" and seems to be replaceable by setting `hasBeginning` and (or?) `hasEnd`.

By setting these 6 fields, for example, we seem to have one version of a minimum viable **Economic Event**:

* action
* provider
* receiver
* resourceClassifiedAs
* resourceQuantity
* hasPointInTime

Makes pretty good sense!

We said: "I have 3 heads of lettuce in my inventory".

Now, we can begin imagining different types of resources, and different agents being involved.

That's something we can expand upon and explore, in another walk-through.
