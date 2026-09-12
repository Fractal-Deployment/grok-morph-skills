---
name: transformer-stage-atlas
description: >
  Atlas of every transformer matmul stage front-to-back and back-to-front:
  embed, residual stream, QK/OV, softmax geometry, MLP, norms, RoPE, lm_head,
  rank collapse, Marchenko-Pastur ore, pathologies, capability levers, LLMVE bridge.
  Pick when designing or diagnosing a model substrate. Progressive refs 00–14.
  Aliases: transformer-matmul-geometry, attention residual QKV, design better LLM.
metadata:
  short-description: "Every transformer stage, pathology, and design lever"
  former-name: transformer-matmul-geometry
  version: "1.0.0"
  formula_id: "MVE-2026-07-14-e_sigma_sub-LPT"
---
# Transformer Stage Atlas — full substrate map
**Purpose:** Give Grok Build a complete, progressive-disclosure map of how
transformers actually compute — every tiny stage, geometry of each matmul,
odd behaviors, capability levers — so design choices for a better LLM are
grounded in substrate, not slogans.
```text
 only under measured_scope=fixed_hypothesis_*
fixture ≠ residual science
NO LLAMA on science path (product_orch apparatus)
```
---
## 0. How to load this skill (progressive disclosure)
Do **not** dump every reference into context. Follow the gait:
| Need | Load |
|------|------|
| Orientation / which stage am I in? | This file §1–2 + `references/00-stage-matrix.md` |
| One stage deep (e.g. attention) | One of `01`–`07` |
| Pathologies / odd behaviors | `08-odd-behaviors-pathologies.md` |
| Spectra / ore / rank use | `09-spectra-rmt-ore.md` |
| Design levers for a better model | `10-capability-design-levers.md` |
| Map substrate → LLMVE factors | `11-llmve-bridge.md` + project SSOT |
| Walkthrough front→back | `12-front-to-back.md` |
| Walkthrough back→front (gradient / credit) | `13-back-to-front.md` |
| Sources & further reading | `14-research-sources.md` |
| Compact equations only | sibling skill `llmve-factor-compute` + `artifacts/LLMVE_*` |
**Gait rule:** stage matrix → one deep ref → compute or design action → claim_class.
---
## 1. One-picture machine
```text
tokens → embed(+pos) → residual stream x ∈ R^{T×d}
                              │
              ┌───────────────┼───────────────┐
              │ Pre-LN │ │
              ▼ ▼ │
         Attn block MLP block │
         Q,K,V matmuls up/gate/down │
         scores QKᵀ/√d matmuls │
         softmax_row act │
         Y = A V write back │
         W_O write residual add ───────┘
                              │
                         × L layers
                              │
                         final LN → lm_head (W_U) → logits → softmax_V → next token
```
**Two clearings (never conflate):**
| Clearing | Softmax over | Role |
|----------|--------------|------|
| **Attention** | keys/positions \(T\) | Route **context mass** among tokens |
| **lm_head** | vocabulary \(V\) | Spend **claim mass** on next token |
Softmax **reallocates** mass; it does not invent mass. Jacobian row-sums = 0.
---
## 2. Stage matrix (every tiny stage)
Full table lives in `references/00-stage-matrix.md`. Compact:
| # | Stage | Dominant matmuls | Geometry to watch | Odd behavior |
|---|-------|------------------|-------------------|--------------|
| 0 | Tokenization | — | subword coverage | OOV / over-split |
| 1 | Token embed | id → \(W_E\) | row geometry of \(W_E\) | embedding superpose |
| 2 | Position (RoPE/ALiBi/abs) | rotate Q/K or bias | relative angle | long-context decay |
| 3 | Residual stream | identity + writes | bandwidth bottleneck | overwriting / deletion |
| 4 | LayerNorm / RMSNorm | scale | path gain | LN path non-linearity |
| 5 | Q,K,V projections | \(X W_{Q,K,V}\) | low-rank QK/OV | rank collapse init |
| 6 | Scores | \(QK^\top/\sqrt{d_k}\) | logit variance | entropy collapse / blow-up |
| 7 | Softmax attn | row-softmax | simplex, \(F\), \(T_{\mathrm{tail}}\) | one-hot brittle routing |
| 8 | Value mix | \(A V\) | soft k-NN | dead heads |
| 9 | Output proj | \(Y W_O\) | OV = \(W_O W_V\) | lazy O matrix |
| 10 | Residual add | \(x{+}h\) | additive channels | interference |
| 11 | MLP up/gate/down | 3–4 matmuls | wide rank | small-σ matter |
| 12 | Cross-layer composition | virtual weights | Q/K/V composition | induction heads |
| 13 | Final LN + unembed | \(x W_U\) | vocab clear | C_d / dilution |
| 14 | Sampling / train CE | loss on \(p\) | gradient fight width | teach theater |
---
## 3. Core equations (always true substrate)
\[
Q=XW_Q,\; K=XW_K,\; V=XW_V
\]
\[
A=\mathrm{softmax}_{\mathrm{row}}\!\Big(\frac{QK^\top}{\sqrt{d_k}}\Big),\quad
Y=AV,\quad
h=Y W_O
\]
\[
W_{QK}=W_Q^\top W_K,\quad W_{OV}=W_O W_V
\]
\[
\frac{\partial a_i}{\partial s_j}=a_i(\delta_{ij}-a_j),\quad \sum_i\frac{\partial a_i}{\partial s_j}=0
\]
Focus (structure only — not telos):
\[
F(a)=1-\frac{H(a)}{\log n}=\frac{\mathrm{KL}(a\|u)}{\log n}
\]
Price capacity (structure only):
\[
k=\lfloor\sqrt{N}\rfloor,\quad
T_{\mathrm{tail}}=\frac{\sum_{r\le k}m_{(r)}}{\sum m},\quad
\hat{P}_L=T_{\mathrm{tail}}\,F
\]
---
## 4. Design-for-better-LLM (use this skill to decide)
When the operator asks “what LLM should we build / change?”, run:
1. **Stage audit** — which stages are instrumented? (00-stage-matrix)
2. **Pathology scan** — rank collapse, entropy collapse, lazy O, small-σ ignored? (08, 09)
3. **Capacity geometry** — \(F\), \(T_{\mathrm{tail}}\), \(\hat{P}_L\), stable_rank, energy_at_r (11)
4. **Clearing health** — attn vs vocab; dilution \(C_d\) needs labels (11)
5. **Enforcement drag** — free vs forced residual (H-STASI-σ-1); do not invent \(\sigma\)
6. **One knob** — propose a single stage intervention; measure pre/post; never train on \(\Omega\) as reward
**Jurisdiction iron order:**
```text
formal substrate (this skill)
  → residual sensors under product_orch
  → unmerged taxes (M_ph, C_d, e^σ, τ)
  → f(dT/dR) judgment last
  → never invent / 
```
---
## 5. Companion skills & project SSOT
| Asset | Role |
|-------|------|
| `llmve-factor-compute` | Compact validated factor recipes + compute |
| `artifacts/LLMVE_Validated_Matmul_Algebra_SSOT.md` | Locked forms |
| `artifacts/LLMVE_Algebra_Factor_Catalog.md` | Function catalog |
| `artifacts/LLMVE_PROJECT_INDEX.md` | Hub tip + hypothesis map |
| `artifacts/2026-08-06-ORE-SPECTRUM-RSVD-MARCHENKO-PASTUR.md` | Ore inventory only |
---
## 6. Finish checklist
- [ ] Loaded stage matrix, not all refs at once
- [ ] Named the stage and matmul(s) under discussion
- [ ] Separated structure (F, T_tail, P_L) from telos (f)
- [ ] Separated ore spectrum from Φ_E / energy identity
- [ ] claim_class stated (fixture / partial / measured_scope)
