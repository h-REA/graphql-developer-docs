# hREA Developer Docs

Documentation for building applications on the hREA GraphQL API.

hREA implements the [ValueFlows](https://valueflo.ws) vocabulary on [Holochain](https://holochain.org). You talk to it in GraphQL, through the `@valueflows/vf-graphql-holochain` adapter, and the adapter turns your operations into calls against the hREA cell running in your hApp.

!!! info "Current release"

    These pages describe **`happ-0.5.0-beta.1`**: Holochain 0.7, `@holochain/client` ^0.21.0, and the ValueFlows 1.0 surface. Earlier releases target earlier Holochain lines; see [Consuming a release](consuming-a-release.md).

## Start here

- **[Quick Start](quick-start.md)**: scaffold a Holochain 0.7 app to build on.
- **[Integration Guide](integration-guide.md)**: add the hREA DNA to your hApp and install the client dependencies.
- **[Basic Usage](basic-usage-lit.md)**: connect, query, mutate.
- **[Consuming a release](consuming-a-release.md)**: which artifact to take, what to pin, what breaks when upgrading.

## Go deeper

- **[GraphQL API Reference](reference/graphql-api-reference/README.md)**: every type, query and mutation, and which of them the DNA actually implements.
- **[Thinking and Expressing ValueFlows](thinking-and-expressing-valueflows.md)**: how to model an economic flow before you write the query.

## Elsewhere

- [hrea.io](https://hrea.io) for what hREA is and who is building it.
- [valueflo.ws](https://www.valueflo.ws) for the ontology itself.
- The [hREA repository](https://github.com/h-REA/hREA), whose [`docs/`](https://github.com/h-REA/hREA/tree/sprout/docs) directory covers architecture, repository layout and contributing, for people working on hREA rather than with it.
