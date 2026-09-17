# Recipe

A recipe is a shareable blueprint for a workflow, which can be used to create plans for carrying out work. It consists of processes, flows, and exchanges.

---

## Types

### `RecipeFlow`
Specifies the inflow or outflow of a resource for a recipe process.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the recipe flow. |
| `revisionId` | `ID!` | The identifier of the last revision of this recipe flow. |
| `resourceQuantity`| `Measure` | The amount and unit of the economic resource. |
| `effortQuantity` | `Measure` | The amount and unit of the work or use action. |
| `action` | `Action!` | The action associated with the flow (e.g., consume, produce). |
| `recipeInputOf` | `RecipeProcess` | The process this flow is an input to. |
| `recipeOutputOf`| `RecipeProcess` | The process this flow is an output of. |
| `recipeClauseOf` | `RecipeExchange` | The exchange agreement this flow is a clause of. |
| `recipeReciprocalClauseOf` | `RecipeExchange` | The reciprocal exchange agreement for this flow. |
| `stage` | `ProcessSpecification` | The process specification for this flow. |
| `instructions` | `String` | Instructions for planning. |
| `note` | `String` | A textual description or comment. |

### `RecipeProcess`
Specifies a process within a recipe.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the recipe process. |
| `revisionId` | `ID!` | The identifier of the last revision of this recipe process. |
| `name` | `String!` | A name for the recipe process. |
| `hasDuration` | `Duration`| The planned duration of the process. |
| `processClassifiedAs`| `[URI!]`| References to a taxonomy for categorization. |
| `note` | `String` | A textual description or comment. |
| `image` | `URI` | An image representing the process. |
| `recipeInputs` | `[RecipeFlow!]` | The non-reciprocal flows that are part of this process. |
| `recipeOutputs`| `[RecipeFlow!]` | The reciprocal flows that are part of this process. |

### `RecipeExchange`
Specifies an exchange agreement within a recipe.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the recipe exchange. |
| `revisionId` | `ID!` | The identifier of the last revision of this recipe exchange. |
| `name` | `String!` | A name for the recipe exchange. |
| `note` | `String` | A textual description or comment. |
| `recipeClauses` | `[RecipeFlow!]` | The non-reciprocal flows that are part of this exchange. |
| `recipeReciprocalClauses`| `[RecipeFlow!]` | The reciprocal flows that are part of this exchange. |

---

## Queries

### `recipeFlow(id: ID!)`
Retrieves a single `RecipeFlow` by its `id`.

### `recipeFlows(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `RecipeFlow`s.

### `recipeProcess(id: ID!)`
Retrieves a single `RecipeProcess` by its `id`.

### `recipeProcesses(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `RecipeProcess`es.

### `recipeExchange(id: ID!)`
Retrieves a single `RecipeExchange` by its `id`.

### `recipeExchanges(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `RecipeExchange`s.

---

## Mutations

### `createRecipeFlow(flow: RecipeFlowCreateParams!)`
Creates a new `RecipeFlow`.

### `updateRecipeFlow(flow: RecipeFlowUpdateParams!)`
Updates an existing `RecipeFlow`.

### `deleteRecipeFlow(revisionId: ID!)`
Deletes a `RecipeFlow`.

### `createRecipeProcess(process: RecipeProcessCreateParams!)`
Creates a new `RecipeProcess`.

### `updateRecipeProcess(process: RecipeProcessUpdateParams!)`
Updates an existing `RecipeProcess`.

### `deleteRecipeProcess(revisionId: ID!)`
Deletes a `RecipeProcess`.

### `createRecipeExchange(exchange: RecipeExchangeCreateParams!)`
Creates a new `RecipeExchange`.

### `updateRecipeExchange(exchange: RecipeExchangeUpdateParams!)`
Updates an existing `RecipeExchange`.

### `deleteRecipeExchange(revisionId: ID!)`
Deletes a `RecipeExchange`.

---

## Related Types

### Input: `RecipeFlowCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `action` | `ID!` | The ID of the `Action` for the flow. |
| `resourceQuantity`| `IMeasure` | The amount and unit of the economic resource. |
| `effortQuantity` | `IMeasure` | The amount and unit of the work or use action. |
| `recipeInputOf` | `ID` | The ID of the `RecipeProcess` this flow is an input to. |
| `recipeOutputOf` | `ID` | The ID of the `RecipeProcess` this flow is an output of. |
| `recipeClauseOf` | `ID` | The ID of the `RecipeExchange` this flow is a clause of. |
| `recipeReciprocalClauseOf` | `ID` | The ID of the reciprocal `RecipeExchange`. |
| `stage` | `ID` | The ID of the `ProcessSpecification` for this flow. |
| `state` | `String` | The state of the desired economic resource. |
| `instructions` | `String` | Instructions for planning. |
| `note` | `String` | A textual description or comment. |

### Input: `RecipeFlowUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the flow to update. |
| `action` | `ID` | The ID of the `Action` for the flow. |
| `resourceQuantity`| `IMeasure` | The amount and unit of the economic resource. |
| `effortQuantity` | `IMeasure` | The amount and unit of the work or use action. |
| `recipeInputOf` | `ID` | The ID of the `RecipeProcess` this flow is an input to. |
| `recipeOutputOf` | `ID` | The ID of the `RecipeProcess` this flow is an output of. |
| `recipeClauseOf` | `ID` | The ID of the `RecipeExchange` this flow is a clause of. |
| `recipeReciprocalClauseOf` | `ID` | The ID of the reciprocal `RecipeExchange`. |
| `stage` | `ID` | The ID of the `ProcessSpecification` for this flow. |
| `state` | `String` | The state of the desired economic resource. |
| `instructions` | `String` | Instructions for planning. |
| `note` | `String` | A textual description or comment. |

### Response: `RecipeFlowResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `recipeFlow` | `RecipeFlow!` | The `RecipeFlow` that was created or updated. |

### Input: `RecipeProcessCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | A name for the recipe process. |
| `hasDuration` | `IDuration`| The planned duration of the process. |
| `processClassifiedAs`| `[URI!]`| References to a taxonomy for categorization. |
| `note` | `String` | A textual description or comment. |

### Input: `RecipeProcessUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the process to update. |
| `name` | `String` | A name for the recipe process. |
| `hasDuration` | `IDuration`| The planned duration of the process. |
| `processClassifiedAs`| `[URI!]`| References to a taxonomy for categorization. |
| `note` | `String` | A textual description or comment. |

### Response: `RecipeProcessResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `recipeProcess` | `RecipeProcess!` | The `RecipeProcess` that was created or updated. |

### Input: `RecipeExchangeCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | A name for the recipe exchange. |
| `note` | `String` | A textual description or comment. |

### Input: `RecipeExchangeUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the exchange to update. |
| `name` | `String` | A name for the recipe exchange. |
| `note` | `String` | A textual description or comment. |

### Response: `RecipeExchangeResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `recipeExchange` | `RecipeExchange!` | The `RecipeExchange` that was created or updated. |

### Connection: `RecipeFlowConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[RecipeFlowEdge!]!` | A list of recipe flow edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `RecipeFlowEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `RecipeFlow!` | The `RecipeFlow` record. |
| `cursor` | `String!` | A cursor for use in pagination. |

### Connection: `RecipeProcessConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[RecipeProcessEdge!]!` | A list of recipe process edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `RecipeProcessEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `RecipeProcess!` | The `RecipeProcess` record. |
| `cursor` | `String!` | A cursor for use in pagination. |

### Connection: `RecipeExchangeConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[RecipeExchangeEdge!]!` | A list of recipe exchange edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `RecipeExchangeEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `RecipeExchange!` | The `RecipeExchange` record. |
| `cursor` | `String!` | A cursor for use in pagination. | 