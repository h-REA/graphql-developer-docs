# Recipe Exchange

Specifies an exchange agreement as part of a recipe.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the recipe exchange. |
| `revisionId` | `ID!` | The identifier of the last revision of this recipe exchange. |
| `name` | `String!` | An informal or formal textual identifier for a recipe exchange. |
| `note` | `String` | A textual description or comment. |
| `recipeClauses` | `[RecipeFlow!]` | The non-reciprocal recipe flows that are part of this exchange. |
| `recipeReciprocalClauses` | `[RecipeFlow!]` | The reciprocal recipe flows that are part of this exchange. |
| `revision` | `RecipeExchange` | Retrieves a specific revision of a recipe exchange. |
| `meta` | `RecordMeta!` | Metadata about the record. |

## Queries

### `recipeExchange(id: ID!)`
Retrieves a single `RecipeExchange` by its `id`.

### `recipeExchanges(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `RecipeExchange`s.

## Mutations

### `createRecipeExchange(recipeExchange: RecipeExchangeCreateParams!)`
Creates a new `RecipeExchange`.

### `updateRecipeExchange(recipeExchange: RecipeExchangeUpdateParams!)`
Updates an existing `RecipeExchange`.

### `deleteRecipeExchange(revisionId: ID!)`
Deletes a `RecipeExchange`.

---

## Related Types

### Input: `RecipeExchangeCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | Name of the recipe exchange. |
| `note` | `String` | A textual description. |

### Input: `RecipeExchangeUpdateParams`
Requires a `revisionId` and allows updating the same fields as `RecipeExchangeCreateParams`.

### Response: `RecipeExchangeResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `recipeExchange` | `RecipeExchange!` | The recipe exchange record that was created or updated. |

### Connection: `RecipeExchangeConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[RecipeExchangeEdge!]!` | A list of recipe exchange edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `RecipeExchangeEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `RecipeExchange!` | The recipe exchange record. |
| `cursor` | `String!` | A cursor for use in pagination. | 