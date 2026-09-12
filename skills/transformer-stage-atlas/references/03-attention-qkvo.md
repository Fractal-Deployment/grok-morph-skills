# Attention — QK / OV circuits (S5–S11)
**Authority framing:** Anthropic *A Mathematical Framework for Transformer Circuits* (2021) + LLMVE substrate.
---
## 1. Reparameterization that matters
Keys/queries/values are intermediates. End-to-end, each head is:
\[
W_{QK} = W_Q^\top W_K \quad\text{(low-rank score map)}
\]
\[
W_{OV} = W_O W_V \quad\text{(low-rank write map)}
\]
\[
A = \mathrm{softmax}(x^\top W_{QK} x / \sqrt{d_k})\quad\text{(per head, schematic)}
\]
\[
h(x) = (A \otimes W_{OV})\, x
\]
- **QK circuit:** *where* to move information (token→token pattern). 
- **OV circuit:** *what* to write when attended.
Heads are **independent additive** residual writers. Concat-then-multiply is only an efficiency form.
---
## 2. Stage-by-stage matmul
| Step | Op | Shape notes |
|------|-----|-------------|
| Project | \(Q=XW_Q\), \(K=XW_K\), \(V=XW_V\) | often fused; multi-head split of last dim |
| Score | \(S=QK^\top/\sqrt{d_k}\) | \(T\times T\) per head; causal mask −∞ |
| Softmax | \(A=\mathrm{softmax}_{\mathrm{row}}(S)\) | rows on simplex |
| Mix | \(Y=AV\) | soft selection of values |
| Out | \(h = \mathrm{concat}(Y)\,W_O\) | write into residual |
**Scaling \(\sqrt{d_k}\):** keeps score variance ~O(1) under idealized i.i.d. assumptions. Trained norms can still drift → entropy collapse or logit blow-up.
---
## 3. Composition across layers (virtual weights)
Residual linearity ⇒ virtual weights = products of writes and later reads:
| Composition | Meaning | Example |
|-------------|---------|---------|
| **Q-composition** | later \(W_Q\) reads prior head write | pattern depends on earlier content |
| **K-composition** | later \(W_K\) reads prior write | **induction heads** |
| **V-composition** | later \(W_V\) chains movement | virtual head \(A_2 A_1\), \(W_{OV2}W_{OV1}\) |
Design implication: depth buys **programs** (composition), not just deeper lookup tables.
---
## 4. Geometry sensors (structure only)
On each attention row \(a\):
\[
F = 1 - H(a)/\log T = \mathrm{KL}(a\|u)/\log T
\]
\[
T_{\mathrm{tail}} = \frac{\sum_{r\le\lfloor\sqrt{T}\rfloor} a_{(r)}}{\sum a},\quad
\hat{P}_L = T_{\mathrm{tail}} F
\]
| Pattern | F | T_tail | Reading |
|---------|---|--------|---------|
| Uniform | ~0 | ~k/T | dead routing |
| Mild peak | mid | mid | soft k-NN |
| One-hot | ~1 | ~1 | brittle / collapsed |
**Jurisdiction:** these are **capacity/structure**. They are not “answer correct.”
---
## 5. Odd behaviors (attention-specific)
1. **Entropy collapse** — large score variance → near-one-hot rows; gradients vanish off the peak. 
2. **Rank collapse (width)** — softmax Markov structure: spectral gap \(s_1=1\) vs \(s_2\sim T^{-1/2}\) drives tokens toward shared representation (Mind the Gap, 2024). 
3. **Skip-trigram bugs** — factored OV/QK tables predict unintended combinations. 
4. **Copying vs positive eigenvalues** — positive eig of OV suggests copy but non-orthonormal bases break naive interpretation. 
5. **Lazy Attention-Output** — \(W_O\) often shows few MP outliers / weak activation-covariance overlap (small singular values analysis, 2024–25). 
6. **Dead heads** — near-uniform A or near-zero OV contribution.
---
## 6. Design levers
| Lever | Effect |
|-------|--------|
| \(d_k\), #heads | rank of QK/OV; head specialization |
| Softmax temperature / scale | peakiness of A |
| GQA / MQA | share K/V across heads — bandwidth vs cost |
| DiffAttn / sinks / window | pathology mitigations |
| Ablate free vs forced residual | path-drag observation (not invent σ) |
---
## 7. Implementation check (when instrumenting)
- Emit **topk scores + logsumexp** (mass basis), not topk-renorm as \(T_{\mathrm{tail}}=1\). 
- Separate head-wise \(F\) from mean \(F\). 
- Do not call high \(F\) “exergy” without usable-for-\(W\) residual.
