# Plan

A logical collection of processes that constitute a body of planned work with defined deliverable(s).

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the plan. |
| `revisionId` | `ID!` | The identifier of the last revision of this plan. |
| `name` | `String!` | An informal or formal textual identifier for a plan. |
| `created` | `DateTime` | The time the plan was made. |
| `due` | `DateTime` | The time the plan is expected to be complete. |
| `note` | `String` | A textual description or comment. |
| `deletable` | `Boolean` | Indicates if the plan can be safely deleted. |
| `inScopeOf` | `[AccountingScope!]` | The accounting scope this plan falls within. |
| `involvedAgents` | `AgentConnection` | Agents involved in the plan. |
| `independentDemands` | `[Commitment!]` | Desired deliverables expected from this plan. |
| `nonProcessCommitments` | `[Commitment!]` | Commitments in the plan that are not tied to a process. |
| `revision` | `Plan` | Retrieves a specific revision of a plan. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `processes` | `[Process!]` | Processes that are part of this plan. |
| `refinementOf` | `Scenario` | This plan refines a scenario, making it operational. |

## Queries

### `plan(id: ID!)`
Retrieves a single `Plan` by its `id`.

### `plans(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Plan`s.

## Mutations

### `createPlan(plan: PlanCreateParams!)`
Creates a new `Plan`.

### `updatePlan(plan: PlanUpdateParams!)`
Updates an existing `Plan`.

### `deletePlan(revisionId: ID!)`
Deletes a `Plan`.

---

## Related Types

### Input: `PlanCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | An informal or formal textual identifier for the plan. |
| `inScopeOf` | `[ID!]` | The accounting scope of the plan. |
| `refinementOf` | `ID` | The scenario this plan refines, making it operational. |
| `created` | `DateTime` | The time the plan was made. |
| `due` | `DateTime` | The time the plan is expected to be complete. |
| `note` | `String` | A textual description or comment. |

### Input: `PlanUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the plan to update. |
| `name` | `String` | An informal or formal textual identifier for the plan. |
| `inScopeOf` | `[ID!]` | The accounting scope of the plan. |
| `refinementOf` | `ID` | The scenario this plan refines, making it operational. |
| `created` | `DateTime` | The time the plan was made. |
| `due` | `DateTime` | The time the plan is expected to be complete. |
| `note` | `String` | A textual description or comment. |

### Response: `PlanResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `plan` | `Plan!` | The plan record that was created or updated. |

### Connection: `PlanConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[PlanEdge!]!` | A list of plan edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `PlanEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Plan!` | The plan record. |
| `cursor` | `String!` | A cursor for use in pagination. |

