---
name: breakthrough-multi-path-thinking
description: >
  Multi-path breakthrough reasoning under a fixed goal (Diamond-MCTS).
  Runs parallel lenses, scores define/redefine/explore/adapt moves, reroots every 2 rounds,
  contracts with Logic Ration Reason. Pick when standard chain-of-thought is too thin
  and you need structured breakthrough thinking with direction knobs.
  Aliases: deep-think, Diamond-MCTS-R2, think deeply, morph diamond, breakthrough reasoner.
metadata:
  type: workflow
  version: "2.1"
  short-description: "Multi-path breakthrough reasoning (Diamond-MCTS + LRR)"
  pairs-with: honest-prompt-rewrite, evidence-hourglass-research, steelman-truth-tournament, llmve-factor-compute
  former-name: deep-think
---
# Breakthrough Multi-Path Thinking — Diamond-MCTS + LRR
Introspective morph under **fixed telos**. Expand with scored branching; **contract under LRR**; **reroot every 2 rounds** so the working prompt stays the user charge, upgraded.
Parent controller: **`honest-prompt-rewrite`** (load for full state schema + CONTRACT_LRR).
## What this skill does (pick from list)
| You want… | This skill… |
|-----------|-------------|
| Breakthrough / hard strategy | Parallel traces + scored morph ops |
| Adjustable lenses / depth | Direction knobs |
## When to use
- Breakthrough / high-stakes reasoning, strategy, philosophy, creative-technical synthesis
- User wants **direction knobs** (which lenses, depth, constraints)
- Before an evidence-hourglass research chart (steer first)
## Direction knobs (user-adjustable)
| Knob | Values | Effect |
|------|--------|--------|
| lenses | first-principles, analogical, counterfactual, systems, probabilistic, narrative, genius-council | expand streams |
| depth | rounds 2–8 (default 5) | diamond iterations |
| creativity | low/med/high | explore vs define weight |
| reroot | every 2 (default) \| every 1 (strict anchor) | telos tightness |
| residual_honest | on (default) | claim_class discipline on empirical legs |
## Geometry: Diamond-MCTS-R2
```text
each round:
  select ≤4 ops via UCB over {define, redefine, explore, adapt}
  simulate short parallel traces (lenses)
  retain residue cards (quality × telos_fit − invent_green_risk)
  every 2 rounds: REROOT
    root_prompt := original_telos ⊕ markers ⊕ retained distinctions
  CONTRACT_LRR (logic ration reason)
emit: synthesis on final root + morph_log + falsify table
```
Ops:
- **define** — lock terms, success criteria
- **redefine** — stress alternative framings (risk: drift → reroot fixes)
- **explore** — divergent streams (see Phase 1)
- **adapt** — fold residue into structure
## Phase map
| Phase | Diamond role |
|-------|----------------|
| 1 Parallel traces | explore under lenses |
| 2 Critique / mutate | adapt + redefine |
| 3 Ground / pre-mortem | optional light external; disconfirm leading candidate |
| 4 Refine | contract_LRR + reroot cadence |
| 5 Synthesize | emit on final root_prompt |
## Reason bind
```text
Reason ⇔ Logic ∧ Semantic integrity ∧ Pattern-under-lock
```
CONTRACT_LRR enforces Logic + Ration (markers) + Reason (warrants). See `honest-prompt-rewrite` / `references/contract-lrr.md`.
## Residual-honest design mode
When charge is LLMVE / design lever:
- One lever + stage ID if matmul-relevant (`transformer-stage-atlas`)
- claim_class on empirical claims
- Hand off compute to `llmve-factor-compute`; identity contest to `steelman-truth-tournament`
## Chain
```text
breakthrough-multi-path-thinking (this)
  → honest-prompt-rewrite state
  → evidence-hourglass-research
this → steelman-truth-tournament (contested)
```
## Output package
1. Core insight(s) on final root_prompt 
2. Pattern markers minted 
3. Morph log highlights 
4. Falsification / what would change mind 
5. Open frontiers for research 
## WHEN NOT TO USE
- Simple lookup → `evidence-hourglass-research` light 
- Evidence tournament without introspection need → research or steelman 
- Closing G1 / from polish 
## Resources
- Parent: skill `honest-prompt-rewrite` 
- `references/diamond-mcts.md` — op scores, reroot rules 
