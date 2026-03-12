# Process Specification

Specifies the kind of process.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the process specification. |
| `revisionId` | `ID!` | The identifier of the last revision of this process specification. |
| `name` | `String!` | An informal or formal textual identifier for the process. |
| `note` | `String` | A textual description or comment. |
| `image` | `String` | An image of the process. |
| `commitmentsRequiringStage` | `CommitmentConnection` | Commitments requiring this process specification as a stage. |
| `revision` | `ProcessSpecification` | Retrieves a specific revision of a process specification. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `resourcesCurrentlyAtStage` | `EconomicResourceConnection` | Resources currently at this stage. |
| `conformingProcesses` | `ProcessConnection` | Processes that conform to this specification. |
| `conformingRecipeProcesses` | `RecipeProcessConnection` | Recipe processes that conform to this specification. |
| `recipeFlowsRequiringStage` | `RecipeFlowConnection` | Recipe flows requiring this process specification as a stage. |

## Queries

### `processSpecification(id: ID!)`
Retrieves a single `ProcessSpecification` by its `id`.

### `processSpecifications(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `ProcessSpecification`s.

## Mutations

### `createProcessSpecification(processSpecification: ProcessSpecificationCreateParams!)`
Creates a new `ProcessSpecification`.

### `updateProcessSpecification(processSpecification: ProcessSpecificationUpdateParams!)`
Updates an existing `ProcessSpecification`.

### `deleteProcessSpecification(revisionId: ID!)`
Deletes a `ProcessSpecification`.

---

## Related Types

### Input: `ProcessSpecificationCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | An informal or formal textual identifier for the process. |
| `note` | `String` | A textual description or comment. |
| `image` | `String` | An image of the process. |

### Input: `ProcessSpecificationUpdateParams`
Requires a `revisionId` and allows updating the same fields as `ProcessSpecificationCreateParams`.

### Response: `ProcessSpecificationResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `processSpecification` | `ProcessSpecification!` | The process specification record that was created or updated. |

### Connection: `ProcessSpecificationConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[ProcessSpecificationEdge!]!` | A list of process specification edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `ProcessSpecificationEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `ProcessSpecification!` | The process specification record. |
| `cursor` | `String!` | A cursor for use in pagination. |

