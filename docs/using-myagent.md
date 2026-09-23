# Identifying the current agent

!!! warning "`myAgent` is declared but not implemented in `happ-0.5.0-beta.1`"

    The base ValueFlows schema declares a `myAgent` query, and `createHolochainSchema` therefore includes it: an operation using it will parse and validate. It has **no resolver** in this release, and neither does `associateMyAgent`, which is not in the schema at all.

    This page used to describe that association flow. It is kept at its old address because the address is linked from elsewhere, but the flow it described does not exist today.

## What the pattern was meant to be

ValueFlows separates the cryptographic identity of a device from the economic identity of an agent. A person may hold several keys; an organization is an agent that no single key is. The intended shape was three operations: ask which agent this key is associated with (`myAgent`), create agent records (`createPerson`, `createOrganization`), and bind a key to an agent record (`associateMyAgent`).

The first and third are unimplemented. The second works.

## What to do instead today

Create the agent record, then keep its `id` yourself. The `id` is stable for the life of the record, so storing it locally, or deriving it from your own application's user record, is enough for a single-user client:

```typescript
const { data } = await client.mutate({
  mutation: gql`
    mutation ($person: AgentCreateParams!) {
      createPerson(person: $person) {
        agent { id revisionId name }
      }
    }
  `,
  variables: { person: { name: 'Ada Lovelace' } },
})

const myAgentId = data.createPerson.agent.id
// persist myAgentId in your own storage
```

From then on, pass `myAgentId` anywhere an operation takes a `provider`, `receiver`, `proposedTo` or similar agent reference.

`agents`, `people` and `organizations` list what exists on the DHT, so an application that needs to find an agent again can query and match on `name`. That is weaker than a real association, since names are not unique, which is exactly why the association operations are worth having.

## Following the work

Agent association is tracked in the [hREA repository](https://github.com/h-REA/hREA/issues). If your application needs it, saying so on an issue is the most useful thing you can do.
