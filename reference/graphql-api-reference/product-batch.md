# Product Batch

A `ProductBatch` represents a lot or batch, defining a resource produced at the same time and in the same way. This is a standard concept in enterprise resource management and supply chain.

---

## Types

### `ProductBatch`
Represents a lot or batch of a resource.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | Unique identifier for the product batch. |
| `revisionId` | `ID!` | The identifier of the last revision of this product batch. |
| `batchNumber` | `String!` | The standard unique identifier of the batch. |
| `expiryDate` | `DateTime` | The expiration date of the batch, commonly used for food. |
| `productionDate` | `DateTime` | The date the batch was produced. |

---

## Queries

### `productBatch(id: ID!)`
Retrieves a single `ProductBatch` by its `id`.

### `productBatches(first: Int, after: String, last: Int, before: String)`
Retrieves a paginated list of all `ProductBatch` records.

---

## Mutations

### `createProductBatch(productBatch: ProductBatchCreateParams!)`
Creates a new `ProductBatch`.

### `updateProductBatch(productBatch: ProductBatchUpdateParams!)`
Updates an existing `ProductBatch`.

### `deleteProductBatch(id: ID!)`
Deletes a `ProductBatch`.

---

## Related Types

### Input: `ProductBatchCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `batchNumber` | `String!` | The standard unique identifier of the batch. |
| `expiryDate` | `DateTime` | The expiration date of the batch. |
| `productionDate` | `DateTime` | The date the batch was produced. |

### Input: `ProductBatchUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the product batch to update. |
| `batchNumber` | `String` | The standard unique identifier of the batch. |
| `expiryDate` | `DateTime` | The expiration date of the batch. |
| `productionDate` | `DateTime` | The date the batch was produced. |

### Response: `ProductBatchResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `productBatch` | `ProductBatch!` | The `ProductBatch` that was created or updated. |

### Connection: `ProductBatchConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[ProductBatchEdge!]!` | A list of product batch edges. |
| `pageInfo`| `PageInfo!` | Information to aid in pagination. |

### Edge: `ProductBatchEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `ProductBatch!` | The `ProductBatch` record. |
| `cursor` | `String!` | A cursor for use in pagination. 