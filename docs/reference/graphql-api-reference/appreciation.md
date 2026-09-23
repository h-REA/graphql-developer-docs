# Appreciation

An `Appreciation` ties an economic event given in loose fulfilment for another economic event, without commitments or expectations. It is a key component for supporting gift economies.

---

## Types

### `Appreciation`
Represents the act of giving one economic event in appreciation for another.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the appreciation. |
| `revisionId` | `ID!` | The identifier of the last revision of this appreciation. |
| `appreciationOf` | `EconomicEvent!` | The economic event being acknowledged. |
| `appreciationWith` | `EconomicEvent!` | The economic event given as a gift. |
| `note` | `String` | A textual description or comment. |

---

## Queries

### `appreciation(id: ID!)`
Retrieves a single `Appreciation` by its `id`.

### `appreciations(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Appreciation` records.

---

## Mutations

### `createAppreciation(appreciation: AppreciationCreateParams!)`
Creates a new `Appreciation`.

### `updateAppreciation(appreciation: AppreciationUpdateParams!)`
Updates an existing `Appreciation`.

### `deleteAppreciation(revisionId: ID!)`
Deletes an `Appreciation`.

---

## Related Types

### Input: `AppreciationCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `appreciationOf` | `ID!` | The ID of the `EconomicEvent` being acknowledged. |
| `appreciationWith`| `ID!` | The ID of the `EconomicEvent` being given as a gift. |
| `note` | `String` | A textual description or comment. |

### Input: `AppreciationUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the appreciation to update. |
| `appreciationOf` | `ID` | The ID of the `EconomicEvent` being acknowledged. |
| `appreciationWith`| `ID` | The ID of the `EconomicEvent` being given as a gift. |
| `note` | `String` | A textual description or comment. |

### Response: `AppreciationResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `appreciation` | `Appreciation!` | The `Appreciation` that was created or updated. |

### Connection: `AppreciationConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[AppreciationEdge!]!` | A list of appreciation edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `AppreciationEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Appreciation!` | The `Appreciation` record. |
| `cursor` | `String!` | A cursor for use in pagination. | 