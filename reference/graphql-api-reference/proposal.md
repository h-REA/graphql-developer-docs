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
List all proposals that are being listed as requests.
> Status: Unimplemented

### `offers`
List all proposals that are being listed as offers.
> Status: Unimplemented

## Mutations

### `createProposal`

> Status: Implemented

### `updateProposal`

> Status: Implemented

### `deleteProposal`

> Status: Implemented

### `proposeIntent`
Include an existing intent as part of a proposal.
@param publishedIn the (`Proposal`) to include the intent in
@param publishes the (`Intent`) to include as part of the proposal
> Status: Implemented

### `deleteProposedIntent`

> Status: Implemented

### `proposeTo`
Send a proposal to another agent.
@param proposed the (`Proposal`) to send to an involved agent
@param proposedTo the (`Agent`) to include in the proposal
> Status: Implemented

### `deleteProposedTo`

> Status: Implemented

