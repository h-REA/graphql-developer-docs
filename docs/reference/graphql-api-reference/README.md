# GraphQL API Reference

Every type, query and mutation in the schema that `@valueflows/vf-graphql-holochain` builds for `happ-0.5.0-beta.1`.

The schema is assembled from the sixteen ValueFlows modules hREA enables, plus hREA's own ValueFlows 1.0 extensions. See [Enabled modules](../../configuring-enabled-modules.md) for the list and for why it is not configurable.

## What actually works

A type being in the schema does not mean the DNA implements it. Three states, and the pages say which one they are in:

| State | Meaning | Types |
|---|---|---|
| **Implemented** | queries and mutations reach the DNA | Action, Agent (person, organization), Agreement, AgreementBundle, Claim, Commitment, EconomicEvent, EconomicResource, Intent, Plan, Process, ProcessSpecification, Proposal (with offers and requests), Recipe (exchange, flow, process), ResourceSpecification, SpatialThing, Unit |
| **Declared, no resolver** | parses and validates, returns nothing | AgentRelationship, AgentRelationshipRole, `myAgent` |
| **Type only** | in the schema, no operations at all | ProductBatch |

Two more things worth knowing before you plan an integration:

- **The CRUD set is not uniform.** There is no `deleteEconomicEvent`: events are the record of what happened, and you correct one with a compensating event. There is no `createEconomicResource` or `deleteEconomicResource` either, because a resource comes into being through an event, via the `newInventoriedResource` argument on `createEconomicEvent`.
- **Updates and deletes take `revisionId`, not `id`.** Records are append-only; the revision identifies the version you are amending.

## Types

- [Action](./action.md)
- [Agent](./agent.md)
- [Agent Relationship](./agent-relationship.md)
- [Agent Relationship Role](./agent-relationship-role.md)
- [Agreement](./agreement.md)
- [Agreement Bundle](./agreement-bundle.md)
- [Claim](./claim.md)
- [Commitment](./commitment.md)
- [Economic Event](./economic-event.md)
- [Economic Resource](./economic-resource.md)
- [Intent](./intent.md)
- [Measurement](./measurement.md)
- [Plan](./plan.md)
- [Process](./process.md)
- [Process Specification](./process-specification.md)
- [Product Batch](./product-batch.md)
- [Proposal](./proposal.md)
- [Recipe](./recipe.md)
- [Resource Specification](./resource-specification.md)
- [Spatial Thing](./spatial-thing.md)
- [Scalars](./scalars.md)
- [Utility Types](./utility-types.md)

## Removed in `happ-0.5.0-beta.1`

Three pages are gone because their types are not in the schema this release builds. Their ValueFlows modules are not enabled, so an operation naming them fails at validation:

- **Appreciation** and **Scenario**: modules not enabled.
- **Geolocation**: superseded by [SpatialThing](./spatial-thing.md), the ValueFlows 1.0 type for a mappable location.

And **Settlement** is no longer a type of its own. Settlement is expressed as `EconomicEvent.settles` with `Claim.settledBy` as the reverse. See [Claim](./claim.md).
