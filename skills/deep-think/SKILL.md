---
name: deep-think
description: Diamond-MCTS prompt morph for introspective breakthrough reasoning under fixed telos. Parallel traces, UCB morph ops define redefine explore adapt, mandatory reroot every 2, LRR contraction for logic semantic integrity pattern markers and necessity warrants. Trigger with deep-think on [problem], think deeply, morph diamond, breakthrough reasoning, Diamond-MCTS-R2, or when standard CoT is insufficient. Direction knobs supported. Chains to morph-shared and deep-research.
metadata:
  type: workflow
  version: "2.0"
  seals: train_ok-false measured_omega-false G1-OPEN endpointAssumed-false
  pairs-with: morph-shared, deep-research, argueforge, reason-telos-lookup
---

# Deep Think v2 — Diamond-MCTS-R2 + LRR

Introspective morph under **fixed telos**. Expand with scored branching; **contract under LRR**; **reroot every 2 rounds** so the working prompt stays the user charge, upgraded.

Parent controller: **`morph-shared`** (load for full state schema + CONTRACT_LRR).

## Seals / non-claims

```text
train_ok=false · measured_omega=false · G1=OPEN · endpointAssumed=false
```

Amazing insight ≠ measured_omega. No invent-green.

## When to use

- Breakthrough / high-stakes reasoning, strategy, philosophy, creative-technical synthesis
- User wants **direction knobs** (which lenses, depth, constraints)
- Before a deep-research chart (steer first)

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
  CONTRACT_LRR (logic · ration · reason)
emit: synthesis on final root + morph_log + falsify table
```

Ops:
- **define** — lock terms, success criteria
- **redefine** — stress alternative framings (risk: drift → reroot fixes)
- **explore** — divergent streams (see Phase 1)
- **adapt** — fold residue into structure

## Phase map (compatible with v1)

| Phase | Diamond role |
|-------|----------------|
| 0 Framing | define + telos lock + seals |
| 1 Parallel traces | explore under lenses |
| 2 Critique / mutate | adapt + redefine |
| 3 Ground / pre-mortem | optional light external; disconfirm leading candidate |
| 4 Refine | contract_LRR + reroot cadence |
| 5 Synthesize | emit on final root_prompt |

## Reason bind

```text
Reason ⇔ Logic ∧ Semantic integrity ∧ Pattern-under-lock
```

CONTRACT_LRR enforces Logic + Ration (markers) + Reason (warrants). See `morph-shared` / `references/contract-lrr.md`.

## Residual-honest design mode

When charge is LLMVE / design lever:
- One lever + stage ID if matmul-relevant
- claim_class on empirical claims
- Hand off compute to `llmve-matmul-algebra`; identity contest to `argueforge`

## Chain

```text
deep-think (this) → morph-shared state → deep-research
deep-think → argueforge (contested)
```

## Output package

1. Core insight(s) on final root_prompt  
2. Pattern markers minted  
3. Morph log highlights  
4. Falsification / what would change mind  
5. Open frontiers for research  
6. Seals / non-claims  

## WHEN NOT TO USE

- Simple lookup → `deep-research` light  
- Evidence tournament without introspection need → `deep-research` or `argueforge`  
- Closing G1 / train_ok from polish  

## Resources

- Parent: skill `morph-shared`  
- `references/diamond-mcts.md` — op scores, reroot rules  
