# Economic Event

An observed economic flow, as opposed to a flow planned to happen in the future. This could reflect a change in the quantity of an economic resource.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the economic event. |
| `revisionId` | `ID!` | The identifier of the last revision of this economic event. |
| `action` | `Action!` | Relates an economic event to a verb, such as consume, produce, work, improve, etc. |
| `resourceInventoriedAs` | `EconomicResource` | The specific economic resource involved in the event. |
| `toResourceInventoriedAs`| `EconomicResource`| The resource on the receiving side of a transfer or move. |
| `resourceClassifiedAs` | `[URI!]` | References a concept in a common taxonomy for categorization. |
| `resourceQuantity` | `Measure` | The amount and unit of the economic resource. |
| `effortQuantity` | `Measure` | The amount and unit of the work or use action. |
| `hasBeginning` | `DateTime` | The beginning of the economic event. |
| `hasEnd` | `DateTime` | The end of the economic event. |
| `hasPointInTime` | `DateTime` | The date/time at which the economic event occurred. |
| `note` | `String` | A textual description or comment. |
| `agreedIn` | `URI` | A reference to an agreement governing this event. |
| `triggeredBy` | `EconomicEvent` | References another economic event that implied this one. |
| `satisfies` | `[Intent!]` | The intents this economic event satisfies. |
| `fulfills` | `[Commitment!]` | The commitments this economic event fulfills. |
| `corrects` | `EconomicEvent` | The economic event that this event corrects. |
| `deletable` | `Boolean` | Indicates if the event can be safely deleted. |
| `triggers` | `[EconomicEvent!]` | Other economic events which have been triggered by this one. |
| `provider` | `Agent!` | The economic agent from whom the event is initiated. |
| `receiver` | `Agent!` | The economic agent for whom the event is. |
| `inScopeOf` | `[AccountingScope!]` | The accounting scope this event falls within. |
| `revision` | `EconomicEvent` | Retrieves a specific revision of an economic event. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `realizationOf` | `Agreement` | This event occurs as part of this agreement. |
| `inputOf` | `Process` | Defines the process to which this event is an input. |
| `outputOf` | `Process` | Defines the process for which this event is an output. |
| `resourceConformsTo` | `ResourceSpecification` | The primary resource specification of the resource. |

## Queries

### `economicEvent(id: ID!)`
Retrieves a single `EconomicEvent` by its `id`.

### `economicEvents(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `EconomicEvent`s.

## Mutations

### `createEconomicEvent(event: EconomicEventCreateParams!, newInventoriedResource: EconomicResourceCreateParams)`
Registers a new `EconomicEvent`. Can also be used to register a new `EconomicResource`.

### `updateEconomicEvent(event: EconomicEventUpdateParams!)`
Updates an existing `EconomicEvent`.

### `updateEconomicResource(resource: EconomicResourceUpdateParams!)`
Updates an existing `EconomicResource`.

---

## Related Types

### Input: `EconomicEventCreateParams`
See the full schema for the extensive list of fields for this input type.

### Input: `EconomicEventUpdateParams`
See the full schema for the extensive list of fields for this input type. Requires a `revisionId`.

### Response: `EconomicEventResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `economicEvent` | `EconomicEvent!` | The event record that was created or updated. |
| `economicResource` | `EconomicResource` | Any new resource created by the event. |

### Connection: `EconomicEventConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[EconomicEventEdge!]!` | A list of economic event edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `EconomicEventEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `EconomicEvent!` | The economic event record. |
| `cursor` | `String!` | A cursor for use in pagination. | 