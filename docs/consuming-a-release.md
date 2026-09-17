# Consuming a release

What a published hREA release contains, which artifact you want, and what to pin.

The full reference lives with the code, in the hREA repository: **[docs/consuming-a-release.md](https://github.com/h-REA/hREA/blob/sprout/docs/consuming-a-release.md)**. It is versioned alongside the thing it describes, so it is the authority when this page and that one disagree. What follows is the orientation.

## The two artifacts

A release attaches two files, and they are not interchangeable:

| Artifact | What it is | Use it when |
|---|---|---|
| `hrea.dna` | the hREA DNA on its own | you are composing hREA into your own hApp, alongside your own DNAs |
| `hrea.happ` | a packaged hApp containing that DNA | you want to run hREA by itself, as a separately installed app |

Both names have been stable since `happ-0.4.0-beta`, so a script that fetches by name keeps working across releases.

**The npm adapter is not published by the release workflow.** Getting that pair wrong is the most common way an integration fails, which is why the next section exists.

## What to pin

| Component | For `happ-0.5.0-beta.1` |
|---|---|
| Holochain conductor | **0.7.x** |
| `@holochain/client` | **^0.21.0** |
| `@valueflows/vf-graphql-holochain` | **0.700.x** |
| `@valueflows/vf-graphql` | `^0.9.1-alpha.5`, the ValueFlows 1.0 schema |

The client and the conductor move together: 0.20 speaks to a 0.6 conductor, 0.21 to a 0.7 one, and mixing them does not fail with a message that says so.

The adapter's version line tracks the DNA line: `0.700.x` pairs with the Holochain 0.7 releases, `0.600.x` with the 0.6 ones. That correspondence starts at `0.700.0-rc.0`; for older releases, read the release notes rather than assuming it holds.

## Upgrading from `happ-0.4.0-beta`

Two things will reach your own code, and neither is optional.

**Holochain 0.6 to 0.7 breaks your integrity zomes.** Every `validate_*` signature moves from `EntryCreationAction` to `TypedAction<EntryCreationData>` and its siblings, and the action wire format splits. The exact before and after, in copyable form, is in the hREA repository's [consuming-a-release](https://github.com/h-REA/hREA/blob/sprout/docs/consuming-a-release.md#what-changed-under-you-holochain-06-to-07) document.

**Your own integrity zomes need the same port.** If you compose `hrea.dna` alongside DNAs of your own, every `validate_*` callback you wrote has to move to the 0.8 HDI signatures too. hREA's own integrity zome is the worked example.

**The validation rules themselves did not change.** `happ-0.4.0-beta` already enforced required strings, temporal ordering, quantity bounds, the 21-identifier action vocabulary, collection bounds and immutable-on-update fields; the entity validators in the two tags are byte for byte identical, and the only difference in the integrity zome is the signature port above. A write a 0.4.0 conductor accepted is still accepted. What those rules are, with the message each one returns, is on [Validation rules](validation-rules.md).

## ValueFlows 1.0 additions

All additive to the schema, all new in this release:

- `Proposal.purpose`, with the `ProposalPurpose` enum (`offer`, `request`) and the `offers` and `requests` queries that partition on it
- `Claim` with `settledBy`, and `EconomicEvent.settles`
- `SpatialThing`
- `AgreementBundle`
- `ResourceSpecification.mediumOfExchange`
- `EconomicEvent.reciprocalRealizationOf` and `Commitment.reciprocalClauseOf`

Each has a page in the **[GraphQL API Reference](reference/graphql-api-reference/README.md)**.
