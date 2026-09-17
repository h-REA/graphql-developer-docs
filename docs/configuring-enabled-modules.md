# Enabled modules

ValueFlows is specified as a set of modules, and a GraphQL schema is assembled from the subset an implementation supports. In `happ-0.5.0-beta.1` that subset is **fixed at build time** and is not configurable by the consuming application.

The adapter enables these sixteen:

`util`, `pagination`, `history`, `agent`, `action`, `plan`, `commitment`, `proposal`, `recipe`, `process`, `measurement`, `observation`, `process_specification`, `resource_specification`, `agreement`, `intent`

They are declared in [`modules/vf-graphql-holochain/index.ts`](https://github.com/h-REA/hREA/blob/sprout/modules/vf-graphql-holochain/index.ts), which is also where hREA's own ValueFlows 1.0 extensions are layered on top of the base schema.

## What this means in practice

**Modules that are not enabled are not in your schema at all.** Querying `appreciation` or `scenario` fails at validation, before any zome call happens, because those types do not exist in the built schema.

**A type being in the schema does not mean it is implemented.** The `agent` module brings in `AgentRelationship` and `AgentRelationshipRole`, and the base ValueFlows schema declares `myAgent`, but none of the three has a resolver in this release. They parse, they validate, and they return nothing useful. The reference marks them.

If you need a module that is not enabled, that is a feature request against [hREA](https://github.com/h-REA/hREA/issues) rather than a configuration flag on your side.
