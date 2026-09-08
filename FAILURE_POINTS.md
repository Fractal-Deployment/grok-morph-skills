# Failure points — charged action only

**Pack version:** 2.1.0  
**Meaning pointer:** `Fractal-Deployment/llmve-meaning` 0.6.0 — fail the charged action, not a standing status block.

## What this is

A **failure point** names what would make *this* action, *this* train of thought, or *this* research topic fail.

It is not a health banner. It is not inventory. It is not forward-looking. It does not ride into the next charge.

```text
action:     <one sentence naming THIS charge>
fail_if:    <observable that kills THIS action>
trip_on:    <evidence that would trip it, or “none yet”>
```

After the action ends, discard the list. The next charge mints its own or has none.

## What this is not

- A standing status block copied onto every turn
- A JSON `seals:` object in plugin or skill YAML
- A forever-false flag with no accept path
- Restored deleted inventory names (tombstone lives only in meaning CHANGELOG / Forge)
- A constitution, meter, or product leaf

## Skill-pack job under this rule

Each skill does **one job**. On each use, mint failure points for **that use only**.

| Skill | This-use job | This-use fails if |
|-------|----------------|-------------------|
| honest-prompt-rewrite | Rewrite the working prompt under LRR | Telos drifts; evidence lacks `necessary_because` + marker; this rewrite is sold as product proof |
| breakthrough-multi-path-thinking | Multi-path steer | Simple lookup absorbed; this diamond is sold as a multiply |
| evidence-hourglass-research | Expand → disconfirm → contract | No disconfirm; this harvest is sold as measured product |
| steelman-truth-tournament | Contest identity | This tournament winner is treated as measured Ω |
| llmve-factor-compute | Compute from existing dumps | Missing field written as 0 or 1-as-truth; this compute invents measured Ω |
| transformer-stage-atlas | Map stages | This map is treated as measured product |

Honesty that is **not** a failure point: do not invent green. That is a law of the write, not a banner.

## Example (dies with the action)

Charge: hook residual co-emission on one short prompt.

```text
action:  emit (h_{ℓ-1}, Δ_ℓ, a_ℓ) on one forward pass
fail_if: Δ_ℓ missing, identity gate fails, or board treated as closed product leaf
trip_on: none until the hook runs
```

When that hook run ends, these three lines are dead.
