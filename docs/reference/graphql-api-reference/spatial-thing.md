# SpatialThing

A physical, mappable location. Added in ValueFlows 1.0 and new in `happ-0.5.0-beta.1`.

`SpatialThing` replaces the `Geolocation` type that earlier versions of this reference described. Geolocation is not in the schema this release builds.

## Fields

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the spatial thing. |
| `revisionId` | `ID!` | The identifier of the last revision of this record. |
| `name` | `String!` | An informal or formal textual identifier for the location. Required. |
| `mappableAddress` | `String` | An address that will be recognised by mapping software. |
| `lat` | `Decimal` | Latitude. |
| `long` | `Decimal` | Longitude. |
| `alt` | `Decimal` | Altitude. |
| `note` | `String` | A textual description or comment. |

## Queries

### `spatialThing(id: ID!)`
Retrieves a single `SpatialThing`.

### `spatialThings(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of spatial things.

## Mutations

### `createSpatialThing(spatialThing: SpatialThingCreateParams!)`
### `updateSpatialThing(spatialThing: SpatialThingUpdateParams!)`
### `deleteSpatialThing(revisionId: ID!)`

---

## Related types

### Input: `SpatialThingCreateParams`

| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | Required. |
| `mappableAddress` | `String` | |
| `lat` | `Decimal` | |
| `long` | `Decimal` | |
| `alt` | `Decimal` | |
| `note` | `String` | |

### Input: `SpatialThingUpdateParams`
Takes a `revisionId` plus the same fields as the create params.

### Response: `SpatialThingResponse`
Wraps the record under `spatialThing`.
