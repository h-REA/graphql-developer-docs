# Recipe Process

Specifies a process in a recipe for use in planning from recipe.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the recipe process. |
| `revisionId` | `ID!` | The identifier of the last revision of this recipe process. |
| `name` | `String!` | An informal or formal textual identifier for a recipe process. |
| `hasDuration` | `Duration` | The planned calendar duration of the process. |
| `processClassifiedAs` | `[URI!]` | References concepts in a taxonomy for categorization. |
| `note` | `String` | A textual description or comment. |
| `image` | `URI` | An image that represents the recipe process. |
| `recipeInputs` | `[RecipeFlow!]` | The non-reciprocal recipe flows that are part of this process. |
| `recipeOutputs` | `[RecipeFlow!]` | The reciprocal recipe flows that are part of this process. |
| `revision` | `RecipeProcess` | Retrieves a specific revision of a recipe process. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `processConformsTo`| `ProcessSpecification` | The standard specification or definition of a process. |

## Queries

### `recipeProcess(id: ID!)`
Retrieves a single `RecipeProcess` by its `id`.

### `recipeProcesses(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `RecipeProcess`es.

## Mutations

### `createRecipeProcess(recipeProcess: RecipeProcessCreateParams!)`
Creates a new `RecipeProcess`.

### `updateRecipeProcess(recipeProcess: RecipeProcessUpdateParams!)`
Updates an existing `RecipeProcess`.

### `deleteRecipeProcess(revisionId: ID!)`
Deletes a `RecipeProcess`.

---

## Related Types

### Input: `RecipeProcessCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | Name of the recipe process. |
| `hasDuration` | `IDuration` | Planned duration of the process. |
| `processClassifiedAs` | `[URI!]` | Concepts for categorization. |
| `note` | `String` | A textual description. |
| `processConformsTo` | `ID` | ID of the process specification. |

### Input: `RecipeProcessUpdateParams`
Requires a `revisionId` and allows updating the same fields as `RecipeProcessCreateParams`.

### Response: `RecipeProcessResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `recipeProcess` | `RecipeProcess!` | The recipe process record that was created or updated. |

### Connection: `RecipeProcessConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[RecipeProcessEdge!]!` | A list of recipe process edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `RecipeProcessEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `RecipeProcess!` | The recipe process record. |
| `cursor` | `String!` | A cursor for use in pagination. | 