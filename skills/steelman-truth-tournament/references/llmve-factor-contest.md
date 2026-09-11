# LLMVE Factor Contest Mode — ArgueForge

Use when the charge is **sensor→factor identity**, jurisdiction, or dual-lane disagreement — not general policy alone.

```text
may_multiply_into_omega=false from debate alone
```

Winners = ranked identity readings. Compute legs only via `llmve-matmul-algebra` on real dumps.

## Hypothesis card (required)

```text
hypothesis_id:
  denotation: <from glossary; no free rename>
  formula_candidate: <explicit>
  sensors: [ ... ]
  required_fields: [ ... ]
  apparatus: product_orch_dumps | primary_citation | fixture | none
  mass_basis: logsumexp_full | topk_renorm | other_labeled
  maps_to: F | T_tail | P_L | Phi_E | M_ph | C_d | sigma_sub | tau | f_dTdR | OPEN
  claim_class: refuse | fixture_only | partial | capacity_v2 | measured_scope
  non_claims: [not_training_cleared, does_not_close_product_omega, not_gate_closed, not_energy_identity, ...]
  falsify_if: <residual observation that kills this map>
```

## Dual-lane sheet

```text
Lane A: <card>
Lane B: <card>
Evidence diagnostic to A vs B: [...]
Outcome: A_wins | B_wins | synthesis | abandon
Synthesis product reading (if any): <one card, not average>
```

Never average two non-null lanes into green. Never dual-proof.

## Three-books check (gate before MCDA)

| If hypothesis uses… | Must keep in book | Reject if… |
|---------------------|-------------------|------------|
| usable-for-W, U_W, exergy | ENERGY / EXERGY / Φ_E | rewritten as C_d or σ |
| claim medium, not-good units as good | C_d | rewritten as energy or path drag |
| path drag, free vs forced friction | e^σ_sub | rewritten as C_d or M_ph |

Φ_E3 ∝ F(1−C_d) = probe only, not energy identity.

## ACH tips for factor contests

- Prefer diagnostic residual evidence (paired free/forced, full-mass vs topk theater, LPT package presence).
- Low diagnosticity: narrative architecture folklore, llama chat logprobs as product_orch proxy, topk renorm without logsumexp.
- Force disconfirming search per lane (Red-team expand).
- Mark consilience: circuits paper + RMT + product dump agree → stronger than any single line.

## MCDA residual-honesty criterion (weight hard in LLMVE mode)

Score 0–10 on:

1. claim_class honesty (no overclaim)
2. three-books integrity
3. dual-lane discipline
4. apparatus match (NO LLAMA when product path claimed)
5. falsify_if specificity

A high eloquence / low honesty score **must not** win tournament.

## Hand-off after winners

| Winner says… | Hand off to |
|--------------|-------------|
| Identity partial; dumps exist | `llmve-matmul-algebra` Phase C compute |
| Substrate facts missing | `deep-research` substrate mode |
| One lever after identity settled | `deep-think` residual-honest design |
| P_L method identity | `pl24-p-l-methods` then algebra |
| Stage pathology unclear | `transformer-matmul-geometry` stage matrix |

## Anti-patterns

- Top-K equals C_d
- multi_step_span equals tau
- high probability equals asset
- usable-work language inside P_L
- dual-proof because both sensors fired
- setting training_cleared or omega_was_measured from whitepaper polish
- llama pin as orchestrator mass basis

## Output minimum (LLMVE mode)

2. ACH with dual-lane outcome if used
3. Top 3 with claim_class + maps_to + apparatus + non_claims
4. Grand synthesis identity product (or abandon)
5. Open residual list (what would move partial → capacity_v2)
6. Explicit hand-offs (not invent compute)

## Non-claims

This reference does not close G1, training_cleared, or omega_was_measured. It does not invent residual tensors or attention weights. It does not rewrite formula_id.
