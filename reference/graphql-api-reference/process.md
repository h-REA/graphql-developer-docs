# Process

An activity that changes inputs into outputs. It could transform or transport economic resource(s).

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the process. |
| `revisionId` | `ID!` | The identifier of the last revision of this process. |
| `name` | `String!` | An informal or formal textual identifier for a process. |
| `hasBeginning` | `DateTime` | The planned beginning of the process. |
| `hasEnd` | `DateTime` | The planned end of the process. |
| `finished` | `Boolean` | Indicates if the process is complete or not. |
| `classifiedAs` | `[URI!]` | References concepts in a taxonomy for categorization. |
| `note` | `String` | A textual description or comment. |
| `nextProcesses` | `[Process!]` | The processes that follow this one. |
| `previousProcesses`| `[Process!]` | The processes that precede this one. |
| `deletable` | `Boolean` | Indicates if the process can be safely deleted. |
| `involvedAgents` | `AgentConnection` | Agents involved in the process. |
| `workingAgents` | `AgentConnection` | Agents working on the process. |
| `inScopeOf` | `[AccountingScope!]` | The accounting scope this process falls within. |
| `revision` | `Process` | Retrieves a specific revision of a process. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `observedInputs` | `[EconomicEvent!]` | Observed economic events that are inputs to this process. |
| `observedOutputs`| `[EconomicEvent!]` | Observed economic events that are outputs of this process. |
| `unplannedInputs` | `[EconomicEvent!]` | Unplanned economic events that are inputs to this process. |
| `unplannedOutputs`| `[EconomicEvent!]` | Unplanned economic events that are outputs of this process. |
| `committedInputs` | `[Commitment!]` | Committed inputs for this process. |
| `committedOutputs`| `[Commitment!]` | Committed outputs for this process. |
| `intendedInputs` | `[Intent!]` | Intended inputs for this process. |
| `intendedOutputs` | `[Intent!]` | Intended outputs for this process. |
| `plannedWithin` | `Plan` | The plan that this process is a part of. |
| `basedOn` | `ProcessSpecification` | The definition or specification for a process. |

## Queries

### `process(id: ID!)`
Retrieves a single `Process` by its `id`.

### `processes(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Process`es.

## Mutations

### `createProcess(process: ProcessCreateParams!)`
Creates a new `Process`.

### `updateProcess(process: ProcessUpdateParams!)`
Updates an existing `Process`.

### `deleteProcess(id: ID!)`
Deletes a `Process`.

---

## Related Types

### Input: `ProcessCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | An informal or formal textual identifier for the process. |
| `hasBeginning`| `DateTime` | The planned beginning of the process. |
| `hasEnd` | `DateTime` | The planned end of the process. |
| `finished` | `Boolean` | Indicates if the process is complete. |
| `classifiedAs`| `[URI!]` | References concepts in a taxonomy. |
| `note` | `String` | A textual description or comment. |
| `inScopeOf` | `[ID!]` | The accounting scope IDs this process falls within. |
| `plannedWithin` | `ID` | The ID of the plan this process is part of. |
| `basedOn` | `ID` | The ID of the process specification. |

### Input: `ProcessUpdateParams`
Requires a `revisionId` and allows updating the same fields as `ProcessCreateParams`.

### Response: `ProcessResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `process` | `Process!` | The process record that was created or updated. |

### Connection: `ProcessConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[ProcessEdge!]!` | A list of process edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `ProcessEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Process!` | The process record. |
| `cursor` | `String!` | A cursor for use in pagination. |

