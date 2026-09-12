---
name: evidence-hourglass-research
description: >
  Structured evidence research that expands, deliberately disconfirms, then contracts
  into a sharper research prompt (Hourglass Expand→Disconfirm→Contract under LRR).
  Pick for contested topics, progress charts, or simple lookup (light path).
  Not dump-and-summarize. Aliases: deep-research, Hourglass-EDC, morph hourglass, structured deep research.
metadata:
  type: workflow
  version: "2.1"
  short-description: "Expand → disconfirm → rewrite research prompt (hourglass)"
  pairs-with: honest-prompt-rewrite, breakthrough-multi-path-thinking, steelman-truth-tournament, llmve-factor-compute, transformer-stage-atlas
  former-name: deep-research
---
# Evidence Hourglass Research — EDC + LRR
Evidence morph under fixed telos. **Expand** harvest → **Disconfirm** → **Contract_LRR** into a sharper research prompt. Not dump-and-summarize.
Parent controller: **`honest-prompt-rewrite`**.
## What this skill does (pick from list)
| You want… | This skill… |
|-----------|-------------|
| Serious multi-source research | Full hourglass EDC rounds |
| Quick factual lookup | Light path (1 expand + short LRR) |
| LLMVE substrate harvest | Stage-aware, NO LLAMA, claim_class |
Research synthesis ≠ / / G1 closed.
## Paths
| Path | When | Loop |
|------|------|------|
| **light** | simple lookup | 1× expand_external → short CONTRACT_LRR → answer |
| **full hourglass** | contested / high-stakes / progress chart | EDC rounds to saturation |
| **after think** | steered by breakthrough thinking first | inherit markers/residue; then EDC |
## Geometry: Hourglass-EDC
```text
each round:
  1. EXPAND — multi-source harvest under current research_prompt
  2. DISCONFIRM — ≥1 search that could kill leading hypothesis (mandatory)
  3. CONTRACT_LRR — rewrite research_prompt (shorter, evidence-conditioned)
     Logic Ration markers Reason warrants only
stop: diagnostic saturation | budget | user stop
```
Disconfirm is load-bearing; expand-only and inductive-only contracts lose.
## Phase map
| Phase | Hourglass role |
|-------|----------------|
| 1 Harvest | EXPAND |
| 2 ACH / consilience | score diagnosticity; DISCONFIRM built-in |
| 3 Synthesis | CONTRACT_LRR → may re-EXPAND |
| 4 Stress | steelman-truth-tournament if contested policy/identity |
## Evidence rules
- Provenance on every atom 
- Prefer primary / systematic reviews 
- ACH across 3–6 hypotheses 
- Consilience hotspots vs single-source fragile 
- **Contract:** only evidence with `necessary_because` + `marker` enters morph prompt 
## Substrate / LLMVE mode
When charge is transformer residual / factor:
- Stage-ID optional via `transformer-stage-atlas` 
- NO LLAMA as product_orch mass proxy 
- claim_class on numeric claims 
- Hand off multiply to `llmve-factor-compute` 
- Identity contest to `steelman-truth-tournament` 
## Reality-testing
```text
Reason ⇔ Logic ∧ Semantic integrity ∧ Pattern-under-lock
```
## Output package
1. Executive synthesis (calibrated) 
2. ACH / evidence map 
3. Pattern markers + warrants 
4. Morph log of research prompts 
5. Uncertainties + what would change conclusions 
6. Open questions 
## Chain
```text
breakthrough-multi-path-thinking → evidence-hourglass-research (this)
this → steelman-truth-tournament
honest-prompt-rewrite mode=shared for combined projection
```
## WHEN NOT TO USE
- Pure introspective morph without evidence need → breakthrough-multi-path-thinking 
## Resources
- Parent: `honest-prompt-rewrite` 
- `references/hourglass-edc.md` — EDC beat, light path 
