# Agent Relationship

A record of a relationship between two agents.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the agent relationship. |
| `revisionId` | `ID!` | The identifier of the last revision of this agent relationship. |
| `relationship` | `AgentRelationshipRole!` | The role of the relationship. |
| `object` | `Agent!` | The agent that is the object of the relationship. |
| `subject` | `Agent!` | The agent that is the subject of the relationship. |

## Queries

### `agentRelationship(id: ID!)`

Retrieves a single `AgentRelationship` by its `id`.

### `agentRelationships(first: Int, after: String, last: Int, before: String)`

Retrieves a paginated list of all `AgentRelationship`s.

## Mutations

_No mutations are available for this type._ 