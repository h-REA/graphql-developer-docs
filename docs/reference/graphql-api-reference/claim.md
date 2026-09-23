# Claim

A claim for a future economic event, triggered by an economic event that already happened. ValueFlows 1.0, and implemented for the first time in `happ-0.5.0-beta.1`.

!!! warning "This page changed in `happ-0.5.0-beta.1`"

    Earlier versions of this reference described a `Settlement` type with its own queries and mutations. There is no `Settlement` type in the schema this release builds. Settlement is expressed on the two records that participate in it: `EconomicEvent.settles` points at the claim being settled, and `Claim.settledBy` is the reverse.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the claim. |
| `revisionId` | `ID!` | The identifier of the last revision of this record. |
| `action` | `Action!` | Relates the claim to the verb of the expected event, such as `transfer`. |
| `resourceClassifiedAs` | `[URI!]` | References a concept in a common taxonomy for categorisation. |
| `resourceQuantity` | `Measure` | The amount and unit of the expected resource. |
| `effortQuantity` | `Measure` | The amount and unit of the expected work or use. |
| `triggeredBy` | `EconomicEvent!` | The economic event that gave rise to this claim. Required. |
| `due` | `DateTime` | The date the claim is expected to be settled. |
| `created` | `DateTime` | The date and time the claim was created. |
| `finished` | `Boolean` | Whether the claim is considered complete. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | Reference to an agreement, on chain or off. |
| `settledBy` | `[EconomicEvent!]` | The economic events that settle this claim. The reverse of `EconomicEvent.settles`. VF 1.0. |

## Queries

### `claim(id: ID!)`
Retrieves a single `Claim`.

### `claims(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of claims.

## Mutations

### `createClaim(claim: ClaimCreateParams!)`
### `updateClaim(claim: ClaimUpdateParams!)`
### `deleteClaim(revisionId: ID!)`

---

## Related types

### Input: `ClaimCreateParams`

| Field | Type | Description |
| ----- | ---- | ----------- |
| `action` | `ID!` | The action identifier, for example `transfer`. Required. |
| `triggeredBy` | `ID!` | The economic event that triggered the claim. Required. |
| `resourceClassifiedAs` | `[URI!]` | |
| `resourceQuantity` | `IMeasure` | |
| `effortQuantity` | `IMeasure` | |
| `due` | `DateTime` | |
| `created` | `DateTime` | |
| `finished` | `Boolean` | |
| `note` | `String` | |
| `agreedIn` | `URI` | |

### Input: `ClaimUpdateParams`
Takes a `revisionId` plus the same fields as the create params.

### Response: `ClaimResponse`
Wraps the record under `claim`.

## Settling a claim

Settlement is recorded on the economic event, not on a separate record:

```graphql
mutation {
  createEconomicEvent(event: {
    action: "transfer"
    provider: "..."
    receiver: "..."
    settles: "<claim id>"
  }) {
    economicEvent { id settles { id } }
  }
}
```

Reading it back from the claim uses `settledBy`.
