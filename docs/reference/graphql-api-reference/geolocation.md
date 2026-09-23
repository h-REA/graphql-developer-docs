# Location

A location can be a physical address or a virtual place.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the location. |
| `revisionId` | `ID!` | The identifier of the last revision of this location. |
| `label` | `String` | A human-readable name for the location. |
| `lat` | `Float` | The latitude of the location. |
| `lng` | `Float` | The longitude of the location. |
| `alt` | `Float` | The altitude of the location. |
| `note` | `String` | A textual description or comment. |
| `meta` | `RecordMeta!` | Metadata about the record. |

## Queries

### `location(id: ID!)`
Find a location by its ID.

### `locations(first: Int, after: String, last: Int, before: String)`
Loads all locations in this collaboration space.

## Mutations

### `createLocation(location: LocationCreateParams!)`
Creates a new location.

### `updateLocation(location: LocationUpdateParams!)`
Updates an existing location.

### `deleteLocation(revisionId: ID!)`
Deletes a location. 