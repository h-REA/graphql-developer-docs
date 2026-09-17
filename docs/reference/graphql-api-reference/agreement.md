# Agreement

Any type of agreement among economic agents.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the agreement. |
| `revisionId` | `ID!` | The identifier of the last revision of this agreement. |
| `name` | `String` | An informal or formal textual identifier for an agreement. |
| `created` | `DateTime` | The date and time the agreement was created. |
| `note` | `String` | A textual description or comment. |
| `involvedAgents` | `AgentConnection` | Agents involved in the agreement. |
| `commitments` | `[Commitment!]` | Commitments made under this agreement. |
| `revision` | `Agreement` | Retrieves a specific revision of an agreement. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `economicEvents` | `[EconomicEvent!]` | Economic events that are part of this agreement. |
| `unplannedEconomicEvents` | `[EconomicEvent!]` | Unplanned economic events related to this agreement. |

## Queries

### `agreement(id: ID!)`
Retrieves a single `Agreement` by its `id`.

### `agreements(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Agreement`s.

## Mutations

### `createAgreement(agreement: AgreementCreateParams)`
Creates a new `Agreement`.

### `updateAgreement(agreement: AgreementUpdateParams)`
Updates an existing `Agreement`.

### `deleteAgreement(revisionId: ID!)`
Deletes an `Agreement`.

---

## Related Types

### Input: `AgreementCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String` | An informal or formal textual identifier for the agreement. |
| `created` | `DateTime` | The date and time the agreement was created. |
| `note` | `String` | A textual description or comment. |

### Input: `AgreementUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the agreement to update. |
| `name` | `String` | An informal or formal textual identifier for the agreement. |
| `created` | `DateTime` | The date and time the agreement was created. |
| `note` | `String` | A textual description or comment. |

### Response: `AgreementResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `agreement` | `Agreement!` | The agreement record that was created or updated. |

### Connection: `AgreementConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[AgreementEdge!]!` | A list of agreement edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `AgreementEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Agreement!` | The agreement record. |
| `cursor` | `String!` | A cursor for use in pagination. |

