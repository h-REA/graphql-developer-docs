# Unit

A unit of measure.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the unit. |
| `revisionId` | `ID!` | The identifier of the last revision of this unit. |
| `label` | `String!` | A textual label for the unit. |
| `symbol` | `String` | A symbol for the unit. |

## Queries

### `unit(id: ID!)`

Retrieves a single `Unit` by its `id`.

### `units(first: Int, after: String, last: Int, before: String)`

Retrieves a paginated list of all `Unit`s.

## Mutations

_No mutations are available for this type._ 