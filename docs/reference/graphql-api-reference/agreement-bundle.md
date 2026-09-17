# AgreementBundle

A group of agreements treated as one unit. Added in ValueFlows 1.0 and new in `happ-0.5.0-beta.1`.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the bundle. |
| `revisionId` | `ID!` | The identifier of the last revision of this record. |
| `name` | `String` | An informal or formal textual identifier for the bundle. |
| `note` | `String` | A textual description or comment. |
| `agreements` | `[Agreement!]` | The agreements this bundle groups. |

## Queries

### `agreementBundle(id: ID!)`
Retrieves a single `AgreementBundle`.

### `agreementBundles(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of bundles.

## Mutations

### `createAgreementBundle(agreementBundle: AgreementBundleCreateParams!)`
### `updateAgreementBundle(agreementBundle: AgreementBundleUpdateParams!)`
### `deleteAgreementBundle(revisionId: ID!)`

---

## Related types

### Input: `AgreementBundleCreateParams`

| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String` | |
| `note` | `String` | |
| `agreements` | `[ID!]` | IDs of the agreements to bundle. |

### Input: `AgreementBundleUpdateParams`
Takes a `revisionId` plus the same fields as the create params.

### Response: `AgreementBundleResponse`
Wraps the record under `agreementBundle`.
