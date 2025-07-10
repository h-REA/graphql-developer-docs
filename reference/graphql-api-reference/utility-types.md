# Utility Types

These are common types used throughout the schema to provide standardized structures for things like pagination and metadata.

## Scalar Types

### `URI`
The `URI` type simply declares a reference to an external web URL, Holochain entry or other resource.

### `DateTime`
The `DateTime` scalar type represents a DateTime value as specified by [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601).

### `Decimal`
The `Decimal` scalar type represents arbitrary-precision floating-point numbers as specified by [IEEE 854-1987](https://en.wikipedia.org/wiki/IEEE_854-1987). They are represented as strings.

---

## Pagination

### `PageInfo`
Information about pagination in a connection.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `hasNextPage` | `Boolean!` | Indicates if there are more pages of data. |
| `hasPreviousPage` | `Boolean!` | Indicates if there are previous pages of data. |
| `startCursor` | `String` | The cursor of the first edge in the connection. |
| `endCursor` | `String` | The cursor of the last edge in the connection. |
| `totalCount` | `Int` | The total result count, if it can be determined. |
| `pageLimit` | `Int` | The number of items requested per page. |

---

## Record History

### `RecordMeta`
Generic metadata fields attached to all primary record types.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `previousRevision` | `Revision` | Metadata about the previous revision of this record. |
| `previousRevisionsCount`| `Int` | Number of older revisions, if known. |
| `futureRevisionsCount` | `Int` | Number of newer revisions, if known. |
| `latestRevision` | `Revision` | Metadata regarding the most recent revision of this record. |
| `retrievedRevision`| `Revision!`| Metadata regarding the requested revision of this record. |

### `Revision`
Represents a single revision of a record.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the revision. |
| `time` | `DateTime` | The timestamp of when the revision was created. |

---

## Ordering

### `Sort` (enum)
Defines the sort order for a connection.

| Value | Description |
| ----- | ----------- |
| `asc` | Ascending |
| `desc` | Descending |

---

## Other Utility Types

### `Measure`
A quantity of something, including the value and the unit.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `hasNumericalValue` | `Decimal!` | The numeric value of the measure. |
| `hasUnit` | `Unit!` | The unit of the measure. |

### `Duration`
The length of time something lasts.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `hasNumericalValue` | `Decimal!` | The numeric value of the duration. |
| `hasUnit` | `Unit!` | The unit of time for the duration. |

### `AccountingScope`
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