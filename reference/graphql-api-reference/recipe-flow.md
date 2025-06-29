# Recipe Flow

The specification of a resource inflow to, or outflow from, a recipe process.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the recipe flow. |
| `revisionId` | `ID!` | The identifier of the last revision of this recipe flow. |
| `resourceQuantity` | `Measure` | The amount and unit of the economic resource. |
| `effortQuantity` | `Measure` | The amount and unit of the work or use action. |
| `action` | `Action!` | Relates a process input or output to a verb. |
| `recipeInputOf` | `RecipeProcess` | Relates an input flow to its process in a recipe. |
| `recipeOutputOf` | `RecipeProcess` | Relates an output flow to its process in a recipe. |
| `recipeClauseOf` | `RecipeExchange` | Relates a flow to its exchange agreement in a recipe. |
| `providerRole` | `ID` | The role of the provider in the exchange agreement. |
| `receiverRole` | `ID` | The role of the receiver in the exchange agreement. |
| `recipeReciprocalClauseOf` | `RecipeExchange` | Relates a flow to its reciprocal exchange agreement. |
| `stage` | `ProcessSpecification` | Relates to a process specification in a recipe. |
| `instructions` | `String` | The instructions for planning. |
| `note` | `String` | A textual description or comment. |
| `revision` | `RecipeFlow` | Retrieves a specific revision of a recipe flow. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `resourceConformsTo` | `ResourceSpecification!` | The resource definition referenced by this flow. |

## Queries

### `recipeFlow(id: ID!)`
Retrieves a single `RecipeFlow` by its `id`.

### `recipeFlows(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `RecipeFlow`s.

## Mutations

### `createRecipeFlow(recipeFlow: RecipeFlowCreateParams!)`
Creates a new `RecipeFlow`.

### `updateRecipeFlow(recipeFlow: RecipeFlowUpdateParams!)`
Updates an existing `RecipeFlow`.

### `deleteRecipeFlow(revisionId: ID!)`
Deletes a `RecipeFlow`.

---

## Related Types

### Input: `RecipeFlowCreateParams`
See the full schema for the extensive list of fields for this input type.

### Input: `RecipeFlowUpdateParams`
Requires a `revisionId` and allows updating the same fields as `RecipeFlowCreateParams`.

### Response: `RecipeFlowResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `recipeFlow` | `RecipeFlow!` | The recipe flow record that was created or updated. |

### Connection: `RecipeFlowConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[RecipeFlowEdge!]!` | A list of recipe flow edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `RecipeFlowEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `RecipeFlow!` | The recipe flow record. |
| `cursor` | `String!` | A cursor for use in pagination. | 