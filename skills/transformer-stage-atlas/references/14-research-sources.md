# Research sources (anchors)

Not exhaustive. Prefer primary geometry papers + project SSOT over blogs.

---

## Foundational geometry / circuits

1. Vaswani et al., *Attention Is All You Need* (2017) — scaled dot-product, multi-head.  
2. Elhage et al., *A Mathematical Framework for Transformer Circuits* (Anthropic, 2021) — residual stream, QK/OV, composition.  
3. McCormick, *Patterns and Messages* (2025) — head independence, QK vs OV framing.

## Softmax / rank / signal propagation

4. *Mind the Gap* (arXiv 2410.07799) — rank collapse width/depth, spectral gap of Markov attention.  
5. Softmax Jacobian / mass conservation — standard information geometry; used in LLMVE validation.

## Spectra / RMT / ore

6. *Small Singular Values Matter* (arXiv 2410.17770) — MP deviations large **and small**; lazy O; ablation.  
7. Halko, Martinsson, Tropp — randomized SVD (practical ore engine).  
8. Marchenko & Pastur (1967) — bulk null.

## Position / modern stacks

9. RoPE (Su et al.) — rotary position.  
10. LLaMA / SwiGLU — modern MLP form.  
11. GQA literature — multi-query / grouped query attention.

## Belief / residual geometry

12. NeurIPS 2024 — belief-state geometry linearly represented in residual stream.

## Project-native (LLMVE)

13. `artifacts/LLMVE_Validated_Matmul_Algebra_SSOT.md`  
14. `artifacts/LLMVE_Algebra_Factor_Catalog.md`  
15. `artifacts/2026-08-06-ORE-SPECTRUM-RSVD-MARCHENKO-PASTUR.md`  
16. Hub: H-STASI-σ-1, three-books, NO-LLAMA, dual-lane docs  

---

## How to add new research into the skill

1. Map finding → stage ID (S0–S23).  
2. Add 3–8 lines under the matching reference (or new `15-*.md`).  
3. Update 00-stage-matrix odd-behavior cell if new pathology.  
4. If it changes a locked factor formula → **do not** silently edit; open formula_id change + human lock.  
