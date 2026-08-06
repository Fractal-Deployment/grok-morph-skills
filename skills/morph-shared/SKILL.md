---
name: morph-shared
description: Shared prompt-morph controller for Grok with diamond and hourglass geometries and LRR contraction (Logic three-laws semantic integrity, Ration pattern markers, Reason necessity warrants). Use as spine for deep-think and deep-research, full projection pipelines, and iterative telos-locked re-prompting. Trigger with morph-shared, shared morph, LRR contract, prompt morph controller, diamond hourglass morph, think then research pipeline, or morph projection.
metadata:
  type: workflow
  version: "1.0"
  seals: train_ok-false measured_omega-false G1-OPEN endpointAssumed-false
  pairs-with: deep-think, deep-research, argueforge, reason-telos-lookup, llmve-matmul-algebra
---

# morph-shared — Prompt Morph Controller (LRR)

Shared spine for **deep-think** (diamond) and **deep-research** (hourglass). Expand may stretch; **contract is gated by Logic · Ration · Reason**.

## Seals / non-claims

```text
train_ok=false · measured_omega=false · G1=OPEN · endpointAssumed=false
```

Morphology ≠ measured residual. Pattern markers ≠ product dumps. No invent-green.

## When to use

| Need | Mode |
|------|------|
| Full projection (think + research) | `shared` |
| Introspective / directional morph | hand off expand policy to `deep-think` |
| Harvest / lookup / progress chart | hand off expand policy to `deep-research` |
| Contested factor identity | `argueforge` (LLMVE mode), not this skill alone |

## State object (persist across rounds)

```text
S = {
  telos,                 # immutable success criteria + seals
  root_prompt,           # current best re-rooting of user charge
  expand_policy,         # think | research | shared
  residue_cards[],       # insights / partials
  pattern_markers[],     # ration bank
  evidence_atoms[],      # only justified+attached survive contract
  open_frontiers[],
  morph_log[],           # prompt_t → prompt_{t+1} + why
  ACH?,                  # research
  budget                 # rounds / tools
}
```

## Expand policies

| Policy | Fuel | Geometry |
|--------|------|----------|
| `think` | internal redefine / explore / adapt | diamond — reroot every 2 rounds |
| `research` | external harvest | hourglass — expand → disconfirm → contract |
| `shared` | internal + external + pattern-boosted | both + reroot@2 + disconfirm |

**MCTS-shaped control (not full game tree):** select morph op by impact × uncertainty × telos-fit; simulate one bounded pass; retain residue; backprop preference into next selection.

Recommended think ops: `{define, redefine, explore, adapt}` with UCB-like selection, **branch≤4**, **reroot_every=2**.

Recommended research beat: **Expand → Disconfirm → Contract_LRR** each round.

## CONTRACT_LRR (mandatory on every contract)

Detail → `references/contract-lrr.md`

1. **Logic** — identity, non-contradiction, excluded middle; fallacy scrub; semantic integrity (no silent rename).
2. **Ration** — mint/update **pattern markers** from residue + justified evidence (recognition handles for next expand).
3. **Reason** — evidence enters morph prompt only with `necessary_because` (telos link) **and** `marker` attach. Reject bare inductive dump.

### Morph prompt minimum shape

```text
TELOS: <unchanged user charge>
MARKERS: [id: claim / situation pattern]
WARRANTED_EVIDENCE:
  - claim: ...
    necessary_because: <telos link>
    marker: <id>
    source: ...
OPEN: <frontiers>
NON_CLAIMS: seals...
```

## Round loop

```text
for r in 1..budget:
  expand under expand_policy
  if research|shared: disconfirm (≥1 frontier that could kill leading reading)
  CONTRACT_LRR → new root_prompt
  if think|shared and r % 2 == 0: reroot (telos ⊕ markers ⊕ warrants)
  log morph
stop: budget | marginal gain low | diagnostic saturation (research)
emit: synthesis + markers + morph_log + open frontiers + seals
```

## Pipeline (preferred chain)

```text
deep-think (steer)  →  morph-shared state  →  deep-research (chart)
```

Or single `shared` mode for strong overall projection.

## Light path (simple lookup)

1× `expand_external` → short `CONTRACT_LRR` → answer. No long hourglass.

## Hand-offs

| Next need | Skill |
|-----------|--------|
| Identity contest | argueforge llmve-factor-identity |
| Factor compute from dumps | llmve-matmul-algebra |
| Gait / RTH | reason-telos-lookup |
| Stage depth transformers | transformer-matmul-geometry |

## WHEN NOT TO USE

- One-shot factual answer with no iteration needed (just answer).
- Closing train_ok / measured_omega / G1 from eloquence.
- Substituting morph scores for product_orch residual multiply.

## Resources

- `references/contract-lrr.md` — LRR gate checklist
- `references/state-and-pipelines.md` — state schema, pipelines, sim-backed defaults
