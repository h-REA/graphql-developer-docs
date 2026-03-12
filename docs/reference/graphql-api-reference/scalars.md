# Scalar Types

Custom scalar types are used in the GraphQL schema to represent specific kinds of data.

## `URI`
A Uniform Resource Identifier, constrained to the formal syntax defined in RFC 3986.

## `DateTime`
An ISO 8601-encoded UTC date and time string, such as `2024-05-09T14:30:00Z`.

## `Decimal`
A field whose value is a number with a decimal component. It is represented as a string.

## `Action`
Relates a process input or output to a verb. Defined in the Valueflows vocabulary, common actions include: `produce`, `use`, `transfer`, `move`, `modify`, `consume`, `cite`, `work`, `pickup`, `dropoff`, `take`, `give`. 