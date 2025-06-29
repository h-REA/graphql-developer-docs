# Utility Types

These are common types used throughout the schema to provide standardized structures for things like pagination and metadata.

## `PageInfo`
Information about pagination in a connection.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `hasNextPage` | `Boolean!` | Indicates if there are more pages of data. |
| `hasPreviousPage` | `Boolean!` | Indicates if there are previous pages of data. |
| `startCursor` | `String` | The cursor of the first edge in the connection. |
| `endCursor` | `String` | The cursor of the last edge in the connection. |

## `RecordMeta`
Generic metadata fields attached to all primary record types.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The identifier of the last revision of the record. |
| `revision` | `Revision` | Retrieves a specific revision of the record. |
| `revisions` | `[Revision!]` | A list of all revisions of the record. |
| `deletable` | `Boolean` | Indicates if the record can be safely deleted. |

## `Revision`
Represents a single revision of a record.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the revision. |
| `timestamp` | `DateTime!` | The timestamp of when the revision was created. |
| `author` | `Agent!` | The agent who authored the revision. |
| `note` | `String` | An optional note about the revision. |
| `record` | `JSONObject` | The record data at this revision. |

## `Measure`
A quantity of something, including the value and the unit.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `hasNumericalValue` | `Decimal!` | The numeric value of the measure. |
| `hasUnit` | `Unit!` | The unit of the measure. |

## `Duration`
The length of time something lasts.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `hasNumericalValue` | `Decimal!` | The numeric value of the duration. |
| `hasUnit` | `Unit!` | The unit of time for the duration. |

## `AccountingScope`
Grouping around something to create a boundary or context.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the scope. |
| `revisionId` | `ID!` | The identifier of the last revision of this scope. |
| `name` | `String!` | An informal or formal textual identifier for the scope. |
| `note` | `String` | A textual description or comment. |
| `meta` | `RecordMeta!` | Metadata about the record. |
| `commitments` | `CommitmentConnection` | Commitments in this scope. |
| `economicEvents` | `EconomicEventConnection` | Economic events in this scope. |
| `intents` | `IntentConnection` | Intents in this scope. |
| `processes` | `ProcessConnection` | Processes in this scope. |
| `proposals` | `ProposalConnection` | Proposals in this scope. | 