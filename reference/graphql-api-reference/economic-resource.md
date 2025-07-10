# Economic Resource

A resource which is useful to people or the ecosystem.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the economic resource. |
| `revisionId` | `ID!` | The identifier of the last revision of this economic resource. |
| `name` | `String` | An informal or formal textual identifier for an item. |
| `classifiedAs` | `[URI!]` | References concepts in a taxonomy for categorization. |
| `trackingIdentifier` | `String` | A serial number or other unique tracking identifier. |
| `image` | `URI` | A URI to an image for the resource. |
| `imageList` | `[URI!]` | A list of URIs to images for the resource. |
| `accountingQuantity` | `Measure` | The quantity of the resource for which the agent has primary rights. |
| `onhandQuantity` | `Measure` | The quantity of the resource under the agent's direct control. |
| `note` | `String` | A textual description or comment. |
| `unitOfEffort` | `Unit` | The unit used for use or work actions for this resource. |
| `state` | `Action` | The state of the resource (e.g., after a test or review process). |
| `containedIn` | `EconomicResource` | The resource that this resource is contained within. |
| `contains` | `[EconomicResource!]` | Resources that this resource contains. |
| `economicEventsInOutFrom` | `EconomicEventConnection` | All events affecting this resource (provider, transfers, etc.). |
| `economicEventsTo` | `EconomicEventConnection` | All events where this resource is the receiver. |
| `primaryAccountable` | `Agent` | The agent with primary rights and responsibilities for the resource. |
| `commitments` | `CommitmentConnection` | Commitments involving this resource. |
| `revision` | `EconomicResource` | Retrieves a specific revision of an economic resource. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `intents` | `IntentConnection` | Intents involving this resource. |
| `stage` | `ProcessSpecification` | The last process specification this resource went through. |
| `conformsTo` | `ResourceSpecification!` | The specification that this resource conforms to. |
| `previous` | `[EconomicEvent!]` | The previous event(s) in a production flow. |
| `next` | `[EconomicEvent!]` | The next event(s) in a production flow. |
| `track` | `[TrackTraceItem!]` | The item(s) to track from this resource. |
| `trace` | `[TrackTraceItem!]` | The item(s) to trace from this resource. |

## Queries

### `economicResource(id: ID!)`
Retrieves a single `EconomicResource` by its `id`.

### `economicResources(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `EconomicResource`s.

## Mutations

Mutations for `EconomicResource` are handled via `createEconomicEvent` and `updateEconomicResource`. See the [Economic Event](./economic-event.md) page for details.

---

## Related Types

### Input: `EconomicResourceCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String` | An informal or formal textual identifier for an item. |
| `trackingIdentifier`| `String` | A serial number or other unique tracking identifier. |
| `image` | `URI` | A URI to an image for the resource. |
| `imageList` | `[URI!]` | A list of URIs to images for the resource. |
| `containedIn` | `ID` | The ID of the container resource. |
| `note` | `String` | A textual description or comment. |

### Input: `EconomicResourceUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the resource to update. |
| `classifiedAs` | `[URI!]` | Concepts for categorization. |
| `image` | `URI` | An image for the resource. |
| `imageList` | `[URI!]` | A list of images for the resource. |
| `containedIn` | `ID` | The ID of the container resource. |
| `unitOfEffort` | `ID` | The ID of the unit of effort. |
| `note` | `String` | A textual description. |

### Response: `EconomicResourceResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `economicResource` | `EconomicResource!` | The resource record that was created or updated. |

### Connection: `EconomicResourceConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[EconomicResourceEdge!]!` | A list of economic resource edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `EconomicResourceEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `EconomicResource!` | The economic resource record. |
| `cursor` | `String!` | A cursor for use in pagination. | 