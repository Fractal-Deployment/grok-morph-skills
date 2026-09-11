# State, geometries, sim-backed defaults

## Geometries

| Name | Shape | Skill |
|------|-------|--------|
| Diamond-MCTS-R2 | expand ops → retain → reroot every 2 → re-expand | deep-think |
| Hourglass-EDC | expand → disconfirm → contract_LRR | deep-research |
| Shared projection | both fuels + LRR + disconfirm + reroot@2 | morph-shared mode shared |

## Sim-backed defaults (structural control sims 2026-08-06)

Not omega_was_measured. Proxies only.

**Research:** Expand → Disconfirm → Contract each round. Disconfirm is load-bearing. Expand-only and inductive-only contracts lose badly.

**Contract:** Full LRR beats any single leg; inductive-only worst. Chain best: think LRR → research LRR+disconfirm.

## Pipeline recipes

### A — Steer then chart
1. deep-think morph-diamond (user direction knobs)
2. pass S (markers, residue, telos) to deep-research hourglass-EDC

### B — Shared projection
1. morph-shared expand_policy=shared for N rounds
2. emit synthesis + morph_log

### C — Simple lookup
1. deep-research light: one harvest + short CONTRACT_LRR
2. stop

## Anti-patterns

- Morph without telos lock
- Contract as naive summary
- Evidence without warrants
- Treating marker bank as residual science
