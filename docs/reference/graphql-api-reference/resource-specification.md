# Resource Specification

Specification of a kind of resource. Could define a material item, service, digital item, currency account, etc. Used instead of a classification when more information is needed, particularly for recipes.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the resource specification. |
| `revisionId` | `ID!` | The identifier of the last revision of this resource specification. |
| `name` | `String!` | An informal or formal textual identifier for a type of resource. |
| `image` | `URI` | A URI to an image relevant to the entity. |
| `imageList` | `[URI!]` | URI addresses to images relevant to the type of resource. |
| `resourceClassifiedAs` | `[URI!]` | References concepts in a taxonomy for categorization. |
| `note` | `String` | A textual description or comment. |
| `defaultUnitOfResource` | `Unit` | The default unit used for the resource itself. |
| `defaultUnitOfEffort` | `Unit` | The default unit used for use or work. |
| `substitutable` | `Boolean` | Defines if any resource of this type can be freely substituted. |
| `commitments` | `CommitmentConnection` | Commitments for this resource specification. |
| `revision` | `ResourceSpecification` | Retrieves a specific revision of a resource specification. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `intents` | `IntentConnection` | Intents for this resource specification. |
| `conformingResources` | `EconomicResourceConnection` | Resources that conform to this specification. |
| `economicEvents` | `EconomicEventConnection` | Economic events for this resource specification. |

## Queries

### `resourceSpecification(id: ID!)`
Retrieves a single `ResourceSpecification` by its `id`.

### `resourceSpecifications(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `ResourceSpecification`s.

## Mutations

### `createResourceSpecification(resourceSpecification: ResourceSpecificationCreateParams!)`
Creates a new `ResourceSpecification`.

### `updateResourceSpecification(resourceSpecification: ResourceSpecificationUpdateParams!)`
Updates an existing `ResourceSpecification`.

### `deleteResourceSpecification(revisionId: ID!)`
Deletes a `ResourceSpecification`.

---

## Related Types

### Input: `ResourceSpecificationCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | Name of the resource specification. |
| `image` | `URI` | An image for the resource specification. |
| `imageList` | `[URI!]` | A list of images for the resource specification. |
| `resourceClassifiedAs` | `[URI!]` | Concepts for categorization. |
| `note` | `String` | A textual description. |
| `defaultUnitOfResource` | `ID` | The ID of the default unit of resource. |
| `defaultUnitOfEffort` | `ID` | The ID of the default unit of effort. |
| `substitutable` | `Boolean` | Is the resource substitutable? |

### Input: `ResourceSpecificationUpdateParams`
Requires a `revisionId` and allows updating the same fields as `ResourceSpecificationCreateParams`.

### Response: `ResourceSpecificationResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `resourceSpecification` | `ResourceSpecification!` | The resource specification record that was created or updated. |

### Connection: `ResourceSpecificationConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[ResourceSpecificationEdge!]!` | A list of resource specification edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `ResourceSpecificationEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `ResourceSpecification!` | The resource specification record. |
| `cursor` | `String!` | A cursor for use in pagination. |

