# lm_head — vocab claim clearing (S20–S22)

---

## 1. Ops

\[
z = x_{\mathrm{final}} W_U \quad (+ \text{optional bias})
\]
\[
p = \mathrm{softmax}(z)\in\Delta^{|V|-1}
\]

Tied weights: \(W_U = W_E^\top\).

---

## 2. Claim medium doctrine

- **Vocabulary V** = only claim medium (currency of the act).  
- Token ids = claim **positions / holders**, not currency themselves.  
- Softmax \(p\) = claim split after competition on the medium.

---

## 3. Sensors

| Field | Meaning |
|-------|---------|
| peak_id, p_ch | spend vs peak |
| T_tail, F_vocab | Price capacity on V |
| support_width | how many tokens fight |
| margin | peak vs second |
| fight_width | grad top-m under CE |

**Dilution \(C_d\):** needs labeled good/bad claim mass under glossary lock.  
Else identity placeholder 1 — do not invent from “wrong answer.”

---

## 4. Pathology

- Peak without usable support (high F, dead U_W on task)  
- Flat high-entropy vocab (no claim authority)  
- CE fight on huge support → noisy updates

---

## 5. Link to S_EXERGY_W

Support-restricted usable mass \(U_W\) on planned answers under fixed weights:

- Aligned context vs distractor vs uniform_V dead  
- Product orch dumps only (NO LLAMA science path)  
- Thin \(\hat\Phi_{E,W}\) partial until dual-lane residual honest
