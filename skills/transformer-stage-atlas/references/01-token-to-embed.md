# Tokenization → embed → position (S0–S2)

---

## S0 Tokenization

- Maps UTF-8 text → integer ids in vocab \(V\).  
- BPE / Unigram / WordPiece: **subword** geometry affects effective sequence length \(T\).  
- Odd: rare languages over-split → longer T → quadratic attn cost + diluted context.

**Observables:** tokens per char, OOV rate, average T.

---

## S1 Token embedding

\[
x_{0,t} = W_E[\mathrm{id}_t] \in \mathbb{R}^d
\]

- \(W_E \in \mathbb{R}^{|V|\times d}\): each row is a token vector.  
- Superposition: many features packed into d dimensions.  
- Often **tied** with unembedding \(W_U \approx W_E^\top\) (not always).

**Odd:** embedding norms vary by frequency; high-freq tokens dominate early residual energy.

---

## S2 Position

| Scheme | Mechanism | Odd behavior |
|--------|-----------|--------------|
| Absolute learned \(W_P\) | add \(W_P[t]\) | poor length OOD |
| Sinusoidal | fixed sin/cos | classic original TF |
| **RoPE** | rotate Q,K by angle ∝ position | relative; long-ctx needs scale/NTK/YaRN |
| ALiBi | linear bias on scores | simple length bias |

RoPE does **not** write position into residual directly; it warps the **score geometry** of QK.

---

## Design levers

- Vocab size vs compression  
- Tie / untie embed–lm_head  
- RoPE base / scale for context length  
- Never treat embed row as “currency” — currency is the **vocab medium** at lm_head clear
