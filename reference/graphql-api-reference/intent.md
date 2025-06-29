# Intent

A planned economic flow which has not been committed to, which can lead to economic events (sometimes through commitments).

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the intent. |
| `revisionId` | `ID!` | The identifier of the last revision of this intent. |
| `name` | `String` | An informal or formal textual identifier for an intent. |
| `action` | `Action!` | Relates an intent to a verb, such as consume, produce, work, improve, etc. |
| `resourceClassifiedAs` | `[URI!]` | References a concept in a common taxonomy or other classification scheme for categorization. |
| `resourceQuantity` | `Measure` | The amount and unit of the economic resource. |
| `effortQuantity` | `Measure` | The amount and unit of the work or use or citation effort-based action. |
| `availableQuantity` | `Measure` | The total quantity of the offered resource available. |
| `minimumQuantity` | `Measure` | Minimum quantity of the offered resource available. |
| `hasBeginning` | `DateTime` | The planned beginning of the intent. |
| `hasEnd` | `DateTime` | The planned end of the intent. |
| `hasPointInTime` | `DateTime` | The planned date/time for the intent. |
| `due` | `DateTime` | The time something is expected to be complete. |
| `finished` | `Boolean` | Indicates if the intent is complete or not. |
| `image` | `URI` | A URI to an image relevant to the intent. |
| `imageList` | `[URI!]` | URI addresses to images relevant to the intent. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | Reference to an agreement governing this intent. |
| `deletable` | `Boolean` | Indicates if the intent can be safely deleted. |
| `provider` | `Agent` | The agent from whom the intent is initiated (implies an offer). |
| `receiver` | `Agent` | The agent for whom the intent is (implies a request). |
| `inScopeOf` | `[AccountingScope!]` | The accounting scope this intent falls within. |
| `revision` | `Intent` | Retrieves a specific revision of an intent. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `satisfiedBy` | `[Commitment!]` | The commitments that satisfy this intent. |
| `resourceInventoriedAs` | `EconomicResource` | A specific economic resource that can service the intent. |
| `observedBy` | `[EconomicEvent!]` | Economic events that observed this intent. |
| `publishedIn` | `[Proposal!]` | Proposals that this intent is published in. |
| `resourceConformsTo` | `ResourceSpecification` | The primary resource specification of the resource. |
| `inputOf` | `Process` | Defines the process to which this intent is an input. |
| `outputOf` | `Process` | Defines the process to which this intent is an output. |

## Queries

### `intent(id: ID!)`
Retrieves a single `Intent` by its `id`.

### `intents(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Intent`s.

## Mutations

### `createIntent(intent: IntentCreateParams!)`
Creates a new `Intent`.

### `updateIntent(intent: IntentUpdateParams!)`
Updates an existing `Intent`.

### `deleteIntent(revisionId: ID!)`
Deletes an `Intent`.

---

## Related Types

### Input: `IntentCreateParams`
See the full schema for the extensive list of fields for this input type.

### Input: `IntentUpdateParams`
See the full schema for the extensive list of fields for this input type. Requires a `revisionId`.

### Response: `IntentResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `intent` | `Intent!` | The intent record that was created or updated. |

### Connection: `IntentConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[IntentEdge!]!` | A list of intent edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `IntentEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Intent!` | The intent record. |
| `cursor` | `String!` | A cursor for use in pagination. |

