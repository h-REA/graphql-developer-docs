# Measurement

This document outlines the schema for defining and representing measurements, units, and durations.

## Enums

### `TimeUnit`
Defines the unit of time for a temporal `Duration`.

| Value | Description |
| ----- | ----------- |
| `year` | |
| `month` | |
| `week` | |
| `day` | |
| `hour` | |
| `minute` | |
| `second` | |

---

## Types

### `Duration`
Represents an interval between two `DateTime` values.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `numericDuration`| `Decimal!`| A number representing the duration, paired with a unit. |
| `unitType` | `TimeUnit!` | A unit of measure. |

### `Unit`
Defines a unit of measurement, along with its display symbol, based on the OM2 vocabulary.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the unit. |
| `revisionId` | `ID!` | The identifier of the last revision of this unit. |
| `label` | `String!` | A human-readable label for the unit, potentially language-specific. |
| `symbol`| `String!` | A standard display symbol for the unit. |
| `omUnitIdentifier`| `String!` | The OM2 identifier for the unit. |
| `classifiedAs`| `String` | Arbitrary classification for the unit. |

### `Measure`
Binds a quantity to its measurement unit, providing semantic meaning.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `hasNumericalValue` | `Decimal!`| A number representing the quantity, paired with a unit. |
| `hasUnit`| `Unit` | A unit of measure. |

---

## Queries

### `unit(id: ID!)`
Retrieves a `Unit` by its unique identifier.

### `units(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `Unit` records.

---

## Mutations

### `createUnit(unit: UnitCreateParams!)`
Creates a new `Unit`.

### `updateUnit(unit: UnitUpdateParams!)`
Updates an existing `Unit`.

### `deleteUnit(revisionId: ID!)`
Deletes a `Unit`.

---

## Related Types

### Input: `IDuration`
Input structure for defining time durations.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `numericDuration`| `Decimal!`| A number representing the duration, paired with a unit. |
| `unitType` | `TimeUnit!` | A unit of measure. |

### Input: `IMeasure`
Input structure for defining measurements.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `hasNumericalValue` | `Decimal!`| A number representing the quantity, paired with a unit. |
| `hasUnit`| `ID` | The ID of a `Unit`. |

### Input: `UnitCreateParams`
Input structure for creating a `Unit`.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `label` | `String!` | A human-readable label for the unit. |
| `symbol`| `String!` | A standard display symbol for the unit. |
| `omUnitIdentifier`| `String!` | The OM2 identifier for the unit. |
| `classifiedAs`| `[URI!]` | References to a taxonomy for categorization. |

### Input: `UnitUpdateParams`
Input structure for updating a `Unit`.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the unit to update. |
| `label` | `String` | A human-readable label for the unit. |
| `symbol`| `String` | A standard display symbol for the unit. |
| `omUnitIdentifier`| `String` | The OM2 identifier for the unit. |
| `classifiedAs`| `[URI!]` | References to a taxonomy for categorization. |

### Response: `UnitResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `unit` | `Unit!` | The `Unit` that was created or updated. |

### Connection: `UnitConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[UnitEdge!]!` | A list of unit edges. |
| `pageInfo`| `PageInfo!` | Information to aid in pagination. |

### Edge: `UnitEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Unit!` | The `Unit` record. |
| `cursor` | `String!` | A cursor for use in pagination. | 