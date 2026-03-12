# Action

An action verb defining the kind of event, commitment, or intent. It is recommended that the lowercase action verb should be used as the record ID in order that references to `Action`s elsewhere in the system are easily readable.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the action. |
| `label` | `String!` | A unique verb which defines the action. |
| `resourceEffect` | `String!` | The accounting effect of an economic event on a resource, increment, decrement, no effect, or decrement resource and increment 'to' resource. |
| `onhandEffect` | `String!` | The onhand effect of an economic event on a resource, increment, decrement, no effect, or decrement resource and increment 'to' resource. |
| `inputOutput` | `String` | Denotes if a process input or output, or not related to a process. |
| `pairsWith` | `String` | The action that should be included on the other direction of the process, for example accept with modify. |

## Queries

### `action(id: ID!)`

Retrieves a single `Action` by its `id`.

### `actions`

Retrieves a list of all `Action`s.

## Mutations

_No mutations are available for this type._

