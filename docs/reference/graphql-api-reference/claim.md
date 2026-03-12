# Claim

A `Claim` is a request for a future economic event in reciprocity for an economic event that has already occurred. For example, a claim for payment for goods that have been delivered.

---

## Types

### `Claim`
Represents a claim for a future economic event.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the claim. |
| `revisionId` | `ID!` | The identifier of the last revision of this claim. |
| `action` | `Action!` | The action associated with the claim (e.g., consume, produce). |
| `resourceClassifiedAs`| `[URI!]`| References to a taxonomy for categorization. |
| `resourceQuantity`| `Measure` | The amount and unit of the economic resource. |
| `effortQuantity` | `Measure` | The amount and unit of the work or use action. |
| `triggeredBy` | `EconomicEvent!` | The economic event that triggered this claim. |
| `due` | `DateTime` | The date the claim is expected to be settled. |
| `created` | `DateTime` | The date the claim was created. |
| `finished` | `Boolean` | Indicates if the claim is complete. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | A reference to an agreement governing this claim. |
| `settledBy` | `SettlementConnection` | The settlements that have been made for this claim. |

### `Settlement`
Represents the settlement of a claim.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the settlement. |
| `revisionId` | `ID!` | The identifier of the last revision of this settlement. |
| `settles` | `Claim!` | The claim that is being settled. |
| `settledBy` | `EconomicEvent!` | The economic event that settles the claim. |
| `resourceQuantity`| `Measure` | The amount and unit of the economic resource. |
| `effortQuantity` | `Measure` | The amount and unit of the work or use action. |
| `note` | `String` | A textual description or comment. |

---

## Queries

### `claim(id: ID!)`
Retrieves a single `Claim` by its `id`.

### `claims(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Claim` records.

### `settlement(id: ID!)`
Retrieves a single `Settlement` by its `id`.

### `settlements(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Settlement` records.

---

## Mutations

### `createClaim(claim: ClaimCreateParams!)`
Creates a new `Claim`.

### `updateClaim(claim: ClaimUpdateParams!)`
Updates an existing `Claim`.

### `deleteClaim(revisionId: ID!)`
Deletes a `Claim`.

### `createSettlement(settlement: SettlementCreateParams!)`
Creates a new `Settlement`.

### `updateSettlement(settlement: SettlementUpdateParams!)`
Updates an existing `Settlement`.

### `deleteSettlement(revisionId: ID!)`
Deletes a `Settlement`.

---

## Related Types

### Input: `ClaimCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `action` | `ID!` | The ID of the `Action` for the claim. |
| `resourceClassifiedAs`| `[URI!]`| References to a taxonomy for categorization. |
| `resourceQuantity`| `IMeasure` | The amount and unit of the economic resource. |
| `effortQuantity` | `IMeasure` | The amount and unit of the work or use action. |
| `due` | `DateTime` | The date the claim is expected to be settled. |
| `triggeredBy` | `ID!` | The ID of the `EconomicEvent` that triggered this claim. |
| `created` | `DateTime` | The date the claim was created. |
| `finished` | `Boolean` | Indicates if the claim is complete. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | A reference to an agreement governing this claim. |

### Input: `ClaimUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the claim to update. |
| `action` | `ID` | The ID of the `Action` for the claim. |
| `resourceClassifiedAs`| `[URI!]`| References to a taxonomy for categorization. |
| `resourceQuantity`| `IMeasure` | The amount and unit of the economic resource. |
| `effortQuantity` | `IMeasure` | The amount and unit of the work or use action. |
| `due` | `DateTime` | The date the claim is expected to be settled. |
| `triggeredBy` | `ID` | The ID of the `EconomicEvent` that triggered this claim. |
| `created` | `DateTime` | The date the claim was created. |
| `finished` | `Boolean` | Indicates if the claim is complete. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | A reference to an agreement governing this claim. |

### Response: `ClaimResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `claim` | `Claim!` | The `Claim` that was created or updated. |

### Input: `SettlementCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `settles` | `ID!` | The ID of the `Claim` being settled. |
| `settledBy` | `ID!` | The ID of the `EconomicEvent` that settles the claim. |
| `resourceQuantity`| `IMeasure` | The amount and unit of the economic resource. |
| `effortQuantity` | `IMeasure` | The amount and unit of the work or use action. |
| `note` | `String` | A textual description or comment. |

### Input: `SettlementUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the settlement to update. |
| `settles` | `ID` | The ID of the `Claim` being settled. |
| `settledBy` | `ID` | The ID of the `EconomicEvent` that settles the claim. |
| `resourceQuantity`| `IMeasure` | The amount and unit of the economic resource. |
| `effortQuantity` | `IMeasure` | The amount and unit of the work or use action. |
| `note` | `String` | A textual description or comment. |

### Response: `SettlementResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `settlement` | `Settlement!` | The `Settlement` that was created or updated. |

### Connection: `ClaimConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[ClaimEdge!]!` | A list of claim edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `ClaimEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Claim!` | The `Claim` record. |
| `cursor` | `String!` | A cursor for use in pagination. |

### Connection: `SettlementConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[SettlementEdge!]!` | A list of settlement edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `SettlementEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Settlement!` | The `Settlement` record. |
| `cursor` | `String!` | A cursor for use in pagination. | 