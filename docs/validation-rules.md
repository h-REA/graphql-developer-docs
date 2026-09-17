# Validation rules

What the hREA DNA rejects. These rules run in the integrity zome, so they apply to every write on every conductor, whatever client made it. A rejected write comes back as an error whose message names the rule it broke, and a caller that only validates in its own UI will meet them anyway.

Everything on this page is read from `dnas/hrea/zomes/integrity/hrea/` in the hREA repository. The shared checks live in `src/lib.rs`; each entity's `src/rea_*.rs` decides which of them apply to it.

## The rule classes

| Class | Rejection message | Applies to |
|---|---|---|
| Required string | `<Entity> <field> must not be empty` (a value of only whitespace counts as empty) | `Agent.name`, `Agent.agentType`, `Process.name`, `ProcessSpecification.name`, `ResourceSpecification.name`, `SpatialThing.name`, `Unit.label`, `Unit.symbol`, `Unit.om_unit_identifier`, `Intent.action` |
| Non-negative quantity | `<Entity> <field> must not be negative` | every `QuantityValue` on `Claim`, `Commitment`, `EconomicEvent`, `EconomicResource`, `Intent`, including `accountingQuantity`, `onhandQuantity`, `resourceQuantity`, `effortQuantity`, `availableQuantity`, `minimumQuantity` |
| Action vocabulary | `<Entity> action '<id>' is not a valid ValueFlows action` | `Claim`, `Commitment`, `EconomicEvent`, `Intent` |
| Temporal coherence | `<Entity> has_beginning must not be after has_end`, and `<Entity> has_point_in_time cannot be combined with has_beginning/has_end` | `Commitment`, `EconomicEvent`, `Intent`, `Process`, `Proposal` |
| Immutable on update | `<Entity> <field> cannot be changed after creation` | `provider`, `receiver` and `action` on `Commitment`, `EconomicEvent` and `Intent`; `purpose` on `Proposal` |
| Collection bound | `<Entity> <field> exceeds the maximum of 1024 entries` | list fields on `Agent`, `AgreementBundle`, `Claim`, `Commitment`, `EconomicEvent`, `Intent`, `Process`, `Proposal`, `Unit` |
| Transfer needs two agents | `EconomicEvent action '<id>' is a transfer and requires both provider and receiver` | `EconomicEvent` only, for `transfer`, `transfer-all-rights` and `transfer-custody` |

Two rules belong to one entity each rather than to a class:

- **`SpatialThing` coordinates are WGS84.** `lat` must be between -90 and 90, `long` between -180 and 180. The messages are `SpatialThing lat must be between -90 and 90` and its longitude counterpart.
- **`Intent.minimumQuantity` must not exceed `Intent.availableQuantity`.** Checked only when both are present.

Transfer actions are an `EconomicEvent` rule on purpose. An `Intent` is legitimately one-sided, and a `Commitment` may be open, so neither is required to name both agents.

## The action vocabulary

`action` must be one of 21 identifiers. Anything else is rejected at write time, not silently stored:

```
dropoff        pickup         consume        use            work
cite           produce        accept         modify         pass
fail           combine        separate       copy           deliver-service
transfer-all-rights           transfer-custody              transfer
move           raise          lower
```

`pass` and `fail` are pre-1.0 legacy actions and are not in the ValueFlows 1.0 vocabulary. They are kept because removing them would break existing consumers; do not build new work on them.

## What this means when you upgrade from `happ-0.4.0-beta`

These rules are **not** new in `happ-0.5.0-beta.1`. They shipped in `happ-0.4.0-beta` and the two releases enforce them identically: the entity validators are byte for byte the same, and the only change to the integrity zome between the two tags is the Holochain 0.6 to 0.7 signature port, `EntryCreationAction` becoming `TypedAction<EntryCreationData>` and its siblings.

So a write that a `happ-0.4.0-beta` conductor accepted will still be accepted. What actually breaks on the way to `happ-0.5.0-beta.1` is the platform, not the rules: the conductor, `@holochain/client`, the adapter signature, and your own integrity zomes if you compose hREA alongside them. [Consuming a release](consuming-a-release.md) covers that side.

## Testing against them

The rules are asserted on their actual messages in the hREA repository, not just on the fact that a write failed:

- `tests/sweettest/tests/integrity_gate.rs` covers the `SpatialThing` bounds, the action vocabulary, the required action, and the immutable-action-on-update rule.
- `tests/sweettest/tests/proposal.rs` covers `Proposal.purpose`, its enum, and its immutability.

Both run with `yarn run test:sweettest` inside the Nix shell. If you are adding a rule, add it there: the integrity zome is the only place that can enforce one, and a message is part of the contract once an integrator reads it.
