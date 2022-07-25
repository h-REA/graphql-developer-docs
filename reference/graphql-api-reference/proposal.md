# Proposal

## Classes

### `Proposal`

Published requests or offers, sometimes with what is expected in return.

### `ProposedIntent`

Represents many-to-many relationships between Proposals and Intents, supporting including intents in multiple proposals, as well as a proposal including multiple intents.

### `ProposedTo`

An agent to which the proposal is to be published.  A proposal can be published to many agents.

## Queries

### `proposal`
> Status: Implemented

### `proposals`
> Status: Implemented

### `requests`
> Status: Unimplemented

### `offers`
> Status: Unimplemented

## Mutations

### `createProposal`

> Status: Implemented

### `updateProposal`

> Status: Implemented

### `deleteProposal`

> Status: Implemented

### `proposeIntent`

> Status: Implemented

### `deleteProposedIntent`

> Status: Implemented

### `proposeTo`

> Status: Implemented

### `deleteProposedTo`

> Status: Implemented

