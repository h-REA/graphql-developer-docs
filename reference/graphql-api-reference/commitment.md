# Commitment

A planned economic flow that has been promised by an agent to another agent.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the commitment. |
| `revisionId` | `ID!` | The identifier of the last revision of this commitment. |
| `action` | `Action!` | Relates a commitment to a verb, such as consume, produce, work, improve, etc. |
| `resourceClassifiedAs` | `[URI!]` | References a concept in a common taxonomy or other classification scheme for purposes of categorization or grouping. |
| `resourceQuantity` | `Measure` | The amount and unit of the economic resource counted or inventoried. |
| `effortQuantity` | `Measure` | The amount and unit of the work or use or citation effort-based action. |
| `hasBeginning` | `DateTime` | The planned beginning of the commitment. |
| `hasEnd` | `DateTime` | The planned end of the commitment. |
| `hasPointInTime` | `DateTime` | The planned date/time for the commitment. Can be used instead of beginning and end. |
| `due` | `DateTime` | The time something is expected to be complete. |
| `created` | `DateTime` | The creation time of the commitment. |
| `finished` | `Boolean` | The commitment is complete or not. This is irrespective of if the original goal has been met, and indicates that no more will be done. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | Reference to an agreement between agents which specifies the rules or policies or calculations which govern this commitment. |
| `deletable` | `Boolean` | The commitment can be safely deleted, has no dependent information. |
| `satisfies` | `Intent` | The intent which this commitment satisfies. |
| `provider` | `Agent!` | The economic agent from whom the commitment is initiated. |
| `receiver` | `Agent!` | The economic agent whom the commitment is for. |
| `inScopeOf` | `[AccountingScope!]` | Grouping around something to create a boundary or context, used for documenting, accounting, planning. |
| `involvedAgents` | `[Agent!]` | The agents involved in this commitment. |
| `clauseOf` | `Agreement` | This commitment is part of the exchange agreement. |
| `resourceInventoriedAs` | `EconomicResource` | Exact economic resource involved in the commitment. |
| `fulfilledBy` | `[EconomicEvent!]` | The economic events that fulfill this commitment. |
| `independentDemandOf` | `Plan` | Represents a desired deliverable expected from this plan. |
| `plannedWithin` | `Plan` | The transfer commitment is part of the plan. |
| `stage` | `ProcessSpecification` | References the ProcessSpecification of the last process the economic resource went through. |
| `resourceConformsTo` | `ResourceSpecification` | The primary resource specification or definition of an existing or potential economic resource. |
| `revision` | `Commitment` | Retrieves a specific revision of a commitment. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `inputOf` | `Process` | Defines the process to which this commitment is an input. |
| `outputOf` | `Process` | Defines the process for which this commitment is an output. |

## Queries

### `commitment(id: ID!)`
Retrieves a single `Commitment` by its `id`.

### `commitments(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Commitment`s.

## Mutations

### `createCommitment(commitment: CommitmentCreateParams!)`
Creates a new `Commitment`.

### `updateCommitment(commitment: CommitmentUpdateParams!)`
Updates an existing `Commitment`.

### `deleteCommitment(revisionId: ID!)`
Deletes a `Commitment`.

---

## Related Types

### Input: `CommitmentCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `action` | `ID!` | The ID of the `Action` for the commitment. |
| `resourceClassifiedAs`| `[URI!]`| References to a taxonomy for categorization. |
| `resourceQuantity`| `IMeasure` | The amount and unit of the economic resource. |
| `effortQuantity` | `IMeasure` | The amount and unit of the work or use action. |
| `hasBeginning` | `DateTime` | The planned beginning of the commitment. |
| `hasEnd` | `DateTime` | The planned end of the commitment. |
| `hasPointInTime` | `DateTime` | The planned date/time for the commitment. |
| `due` | `DateTime` | The time something is expected to be complete. |
| `created` | `DateTime` | The creation time of the commitment. |
| `finished` | `Boolean` | Indicates if the commitment is complete. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | A reference to an agreement governing this commitment. |
| `satisfies` | `ID` | The ID of the `Intent` this commitment satisfies. |
| `provider` | `ID!` | The ID of the provider `Agent`. |
| `receiver` | `ID!` | The ID of the receiver `Agent`. |
| `inScopeOf` | `[ID!]` | The accounting scope of the commitment. |
| `clauseOf` | `ID` | The ID of the `Agreement` this commitment is a clause of. |
| `resourceInventoriedAs` | `ID` | The ID of the `EconomicResource` involved. |
| `stage` | `ID` | The ID of the `ProcessSpecification`. |
| `resourceConformsTo`| `ID` | The ID of the `ResourceSpecification`. |
| `inputOf` | `ID` | The ID of the `Process` this is an input to. |
| `outputOf` | `ID` | The ID of the `Process` this is an output of. |

### Input: `CommitmentUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the commitment to update. |
| `action` | `ID` | The ID of the `Action` for the commitment. |
| `resourceClassifiedAs`| `[URI!]`| References to a taxonomy for categorization. |
| `resourceQuantity`| `IMeasure` | The amount and unit of the economic resource. |
| `effortQuantity` | `IMeasure` | The amount and unit of the work or use action. |
| `hasBeginning` | `DateTime` | The planned beginning of the commitment. |
| `hasEnd` | `DateTime` | The planned end of the commitment. |
| `hasPointInTime` | `DateTime` | The planned date/time for the commitment. |
| `due` | `DateTime` | The time something is expected to be complete. |
| `created` | `DateTime` | The creation time of the commitment. |
| `finished` | `Boolean` | Indicates if the commitment is complete. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | A reference to an agreement governing this commitment. |
| `clauseOf` | `ID` | The ID of the `Agreement` this commitment is a clause of. |
| `stage` | `ID` | The ID of the `ProcessSpecification`. |
| `resourceConformsTo`| `ID` | The ID of the `ResourceSpecification`. |

### Response: `CommitmentResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `commitment` | `Commitment!` | The commitment record that was created or updated. |

### Connection: `CommitmentConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[CommitmentEdge!]!` | A list of commitment edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `CommitmentEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Commitment!` | The commitment record. |
| `cursor` | `String!` | A cursor for use in pagination. |

