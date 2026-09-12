# Stage matrix — every tiny stage (load first for navigation)
**Skill:** transformer-matmul-geometry 
**Use:** Locate the stage, open the matching deep ref, act.
---
## Full stage table
| ID | Stage | Inputs | Matmuls / ops | Outputs | Sensors / observables | Failure modes | Deep ref |
|----|-------|--------|---------------|---------|----------------------|---------------|----------|
| S0 | Tokenization | text | BPE/Unigram | token ids | vocab hit rate, split length | over-fragment, OOV | 01 |
| S1 | Token embed | ids | gather \(W_E\) | \(x_0\in\mathbb{R}^{T\times d}\) | embed norms, cluster structure | superposition overload | 01 |
| S2 | Position | \(x_0\) | RoPE on Q/K, ALiBi bias, or \(W_P\) add | positioned states | long-ctx score decay | length extrapolation break | 01 |
| S3 | Residual stream | all writes | add | \(x_\ell\) | energy \(\|x\|_2\), cosine drift | overwrite, deletion channels | 02 |
| S4 | Pre/Post LN | \(x\) | RMSNorm / LayerNorm | scaled \(x\) | gain, path scale | LN path non-linearity hides virtual weights | 06 |
| S5 | Q proj | \(x\) | \(Q=xW_Q\) | \(Q\in\mathbb{R}^{T\times h d_k}\) | \(\|Q\|\), singular spectrum | low-rank bottleneck | 03 |
| S6 | K proj | \(x\) | \(K=xW_K\) | \(K\) | same | same | 03 |
| S7 | V proj | \(x\) | \(V=xW_V\) | \(V\) | same | lazy V | 03 |
| S8 | Scores | Q,K | \(S=QK^\top/\sqrt{d_k}\) | logits \(T\times T\) | var(S), max logit | entropy collapse, overflow | 04 |
| S9 | Softmax attn | S | row-softmax (+mask/causal) | \(A\in\Delta^{T-1}\) | \(F\), \(T_{\mathrm{tail}}\), entropy | one-hot brittle, uniform dead | 04 |
| S10 | Value mix | A,V | \(Y=AV\) | head values | effective rank of Y | soft k-NN failure | 03 |
| S11 | Out proj | Y | \(h=YW_O\) (or concat×\(W_O\)) | residual write | OV spectrum | lazy O (few MP outliers) | 03 |
| S12 | Attn residual | x,h | \(x\leftarrow x+h\) | updated stream | Δ energy | destructive interference | 02 |
| S13 | MLP up | x | \(u=xW_{\mathrm{up}}\) | wide | spectrum small/large σ | unused rank | 05 |
| S14 | MLP gate (SwiGLU) | x | \(g=xW_{\mathrm{gate}}\), act | gated | gate sparsity | dead gates | 05 |
| S15 | MLP down | u⊙g | \(xW_{\mathrm{down}}\) | write | **small singular values matter** | ablation kills quality | 05,09 |
| S16 | MLP residual | x,m | \(x\leftarrow x+m\) | stream | — | — | 02 |
| S17 | Layer stack | — | S4–S16 × L | \(x_L\) | layer-wise F, T_tail series | depth rank collapse | 08 |
| S18 | Composition | heads×layers | virtual \(W_{OV}^j W_{OV}^i\), Q/K-comp | circuits | induction scores | skip-trigram bugs | 03,08 |
| S19 | Final LN | \(x_L\) | norm | clean | — | — | 06 |
| S20 | lm_head | x | \(z=xW_U\) (+ tied \(W_E^\top\)) | logits over V | support_width, margin | C_d pressure | 07 |
| S21 | Softmax_V | z | softmax over vocab | \(p\in\Delta^{V-1}\) | F_vocab, T_tail_vocab | uniform / peaky | 07 |
| S22 | Decode / CE | p, target | sample or CE | token / loss | fight_width, grad topk | train theater | 07 |
| S23 | Ore spectrum | weights | RSVD + MP null | bulk vs outliers | stable_rank, energy_at_r | treat spectrum as Φ_E | 09 |
---
## Front-to-back vs back-to-front
| Direction | Question | Start | End |
|-----------|----------|-------|-----|
| **Front→back** | How does a token become a next-token distribution? | S0 | S22 |
| **Back→front** | Where does gradient / credit land? Which matmul absorbs pressure? | S22 loss | S1 embed |
See `12-front-to-back.md` and `13-back-to-front.md`.
---
## Two theaters (hard split)
```text
Attention theater: softmax over positions → context routing
Vocab theater: softmax over V → claim spend
```
Never sell attn FLOPs as claim quality. Never sell top-k accuracy as \(P_L\) without \(F\).
---
## Sensor priority when instrumenting a new model
1. S9: true \(F\) from attn rows (not F_proxy from act_l2) 
2. S21: F_vocab + T_tail_vocab with **logsumexp mass basis** (not topk-renorm) 
3. S11/S15: stable_rank + MP outliers (ore inventory) 
4. S12 free vs forced residual (path drag candidate) 
5. Only then: join product under fixed hypothesis (H-OMEGA-*)
---
## Claim classes
| claim_class | Meaning |
|-------------|---------|
| fixture | synthetic / unit geometry |
| partial | real dumps, incomplete dual / scope |
| measured_under_fixed_hypothesis | product under named H-OMEGA-* only |
| theory_narrative | useful story, not multiply leaf |
