# Agent Relationship Role

A kind of role that exists between 2 agents.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the agent relationship role. |
| `revisionId` | `ID!` | The identifier of the last revision of this role. |
| `name` | `String!` | An informal or formal textual identifier for the role. |
| `note` | `String` | A textual description or comment. |
| `revision` | `AgentRelationshipRole` | Retrieves a specific revision of a role. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `relationships` | `[AgentRelationship!]` | The relationships that have this role. |

## Queries

### `agentRelationshipRole(id: ID!)`
Retrieves a single `AgentRelationshipRole` by its `id`.

### `agentRelationshipRoles(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `AgentRelationshipRole`s.

## Mutations

### `createAgentRelationshipRole(role: AgentRelationshipRoleCreateParams!)`
Creates a new `AgentRelationshipRole`.

### `updateAgentRelationshipRole(role: AgentRelationshipRoleUpdateParams!)`
Updates an existing `AgentRelationshipRole`.

### `deleteAgentRelationshipRole(revisionId: ID!)`
Deletes an `AgentRelationshipRole`.

---

## Related Types

### Input: `AgentRelationshipRoleCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | Name of the role. |
| `note` | `String` | A textual description. |

### Input: `AgentRelationshipRoleUpdateParams`
Requires a `revisionId` and allows updating the same fields as `AgentRelationshipRoleCreateParams`.

### Response: `AgentRelationshipRoleResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `agentRelationshipRole` | `AgentRelationshipRole!` | The role record that was created or updated. |

### Connection: `AgentRelationshipRoleConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[AgentRelationshipRoleEdge!]!` | A list of role edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `AgentRelationshipRoleEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `AgentRelationshipRole!` | The role record. |
| `cursor` | `String!` | A cursor for use in pagination. | 