# Scenario

A `Scenario` is an estimated or analytical logical collection of higher-level processes used for budgeting, analysis, plan refinement, and other purposes.

---

## Types

### `Scenario`
Represents a scenario for planning and analysis.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the scenario. |
| `revisionId` | `ID!` | The identifier of the last revision of this scenario. |
| `name` | `String!` | A name for the scenario. |
| `hasBeginning` | `DateTime` | The beginning date/time of the scenario. |
| `hasEnd` | `DateTime` | The ending date/time of the scenario. |
| `definedAs` | `ScenarioDefinition` | The definition of this scenario (e.g., yearly budget). |
| `refinementOf` | `Scenario` | The scenario that this scenario refines. |
| `note` | `String` | A textual description or comment. |
| `refinements` | `[Scenario!]` | Scenarios that refine this scenario. |

### `ScenarioDefinition`
Represents the type definition of one or more scenarios.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the scenario definition. |
| `revisionId` | `ID!` | The identifier of the last revision of this scenario definition. |
| `name` | `String!` | A name for the scenario definition. |
| `hasDuration` | `Duration` | The duration of the scenario. |
| `note` | `String` | A textual description or comment. |
| `scenarios` | `ScenarioConnection` | Scenarios that use this definition. |

---

## Queries

### `scenario(id: ID!)`
Retrieves a single `Scenario` by its `id`.

### `scenarios(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Scenario` records.

### `scenarioDefinition(id: ID!)`
Retrieves a single `ScenarioDefinition` by its `id`.

### `scenarioDefinitions(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `ScenarioDefinition` records.

---

## Mutations

### `createScenario(plan: ScenarioCreateParams!)`
Creates a new `Scenario`.

### `updateScenario(plan: ScenarioUpdateParams!)`
Updates an existing `Scenario`.

### `deleteScenario(revisionId: ID!)`
Deletes a `Scenario`.

### `createScenarioDefinition(plan: ScenarioDefinitionCreateParams!)`
Creates a new `ScenarioDefinition`.

### `updateScenarioDefinition(plan: ScenarioDefinitionUpdateParams!)`
Updates an existing `ScenarioDefinition`.

### `deleteScenarioDefinition(revisionId: ID!)`
Deletes a `ScenarioDefinition`. 