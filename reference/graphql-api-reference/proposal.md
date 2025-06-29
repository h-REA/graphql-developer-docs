# Proposal

Published requests or offers, sometimes with what is expected in return.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the proposal. |
| `revisionId` | `ID!` | The identifier of the last revision of this proposal. |
| `name` | `String` | An informal or formal textual identifier for a proposal. |
| `hasBeginning` | `DateTime` | The beginning time of proposal publication. |
| `hasEnd` | `DateTime` | The end time of proposal publication. |
| `unitBased` | `Boolean` | Indicates if this proposal contains unit-based quantities. |
| `created` | `DateTime` | The date and time the proposal was created. |
| `note` | `String` | A textual description or comment. |
| `publishes` | `[Intent!]!` | The intents which are part of this proposal. |
| `reciprocal` | `[Intent!]!` | The reciprocal intents which are part of this proposal. |
| `proposedTo` | `[Agent!]!` | Agents to whom the proposal is proposed. |
| `inScopeOf` | `[AccountingScope!]` | The accounting scope this proposal falls within. |
| `revision` | `Proposal` | Retrieves a specific revision of a proposal. |
| `meta` | `RecordMeta!` | Metadata about the record. |

## Queries

### `proposal(id: ID!)`
Retrieves a single `Proposal` by its `id`.

### `proposals(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Proposal`s.

### `offers(first: Int, after: String, last: Int, before: String)`
List all proposals that are being listed as offers.

### `requests(first: Int, after: String, last: Int, before: String)`
List all proposals that are being listed as requests.

## Mutations

### `createProposal(proposal: ProposalCreateParams!)`
Creates a new `Proposal`.

### `updateProposal(proposal: ProposalUpdateParams!)`
Updates an existing `Proposal`.

### `deleteProposal(revisionId: ID!)`
Deletes a `Proposal`.

---

## Related Types

### Input: `ProposalCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String` | Name of the proposal. |
| `hasBeginning`| `DateTime`| Start time of the proposal. |
| `hasEnd` | `DateTime` | End time of the proposal. |
| `unitBased` | `Boolean` | Is the proposal unit-based? |
| `note` | `String` | A textual description. |
| `created` | `DateTime` | Creation time of the proposal. |
| `publishes` | `[ID!]!` | IDs of the intents to publish. |
| `reciprocal` | `[ID!]` | IDs of the reciprocal intents. |
| `proposedTo` | `[ID!]` | IDs of the agents to propose to. |
| `inScopeOf` | `[ID!]` | IDs of the accounting scopes. |

### Input: `ProposalUpdateParams`
Requires a `revisionId` and allows updating the same fields as `ProposalCreateParams`.

### Response: `ProposalResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `proposal` | `Proposal!` | The proposal record that was created or updated. |

### Connection: `ProposalConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[ProposalEdge!]!` | A list of proposal edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `ProposalEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Proposal!` | The proposal record. |
| `cursor` | `String!` | A cursor for use in pagination. |

