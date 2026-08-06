# Softmax geometry (S8–S9, S21)

---

## 1. Definition and simplex

\[
a_i = \frac{e^{s_i}}{\sum_j e^{s_j}},\quad a\in\Delta^{n-1}
\]

- Attention: \(n=T\) (positions).  
- lm_head: \(n=|V|\) (vocab).

Temperature / scale:

\[
a = \mathrm{softmax}(s/\tau)
\]

Smaller \(\tau\) → sharper. Standard attn uses \(\tau=\sqrt{d_k}\).

---

## 2. Jacobian — mass conservation

\[
\frac{\partial a_i}{\partial s_j} = a_i(\delta_{ij}-a_j)
\]

\[
\sum_i \frac{\partial a_i}{\partial s_j} = 0
\]

**Meaning:** changing a logit only **reallocates** probability mass. Softmax never creates mass.  
This is why focus \(F\) is a pure geometry of the distribution, not an energy identity.

---

## 3. Focus \(F\) (validated identity)

\[
H(a)=-\sum_j a_j\log a_j,\quad
F(a)=1-\frac{H(a)}{\log n}=\frac{\mathrm{KL}(a\|u)}{\log n}
\]

| a | F |
|---|---|
| uniform | 0 |
| one-hot | 1 |
| mild peak | (0,1) |

Majorization: more peaked ⇒ higher \(F\).  
\(\sum_j \partial F/\partial s_j = 0\) (reallocation only).

---

## 4. Vital-few share \(T_{\mathrm{tail}}\)

\[
k=\max(1,\lfloor\sqrt{n}\rfloor),\quad
T_{\mathrm{tail}}=\frac{\sum_{r=1}^{k} m_{(r)}}{\sum m}
\]

Use **full mass basis** (logsumexp over V or true row sum).  
**Ban:** topk-renorm that forces \(T_{\mathrm{tail}}=1\) theater.

---

## 5. Pathologies

| Name | Mechanism | Symptom |
|------|-----------|---------|
| Entropy collapse | large \(\mathrm{var}(s)\) | near one-hot A; brittle |
| Rank collapse width | spectral gap of Markov A | tokens align; stable rank →1 |
| Dead uniform | flat scores | F≈0; no routing |
| Topk-renorm theater | incomplete mass | false \(T_{\mathrm{tail}}=1\) |
| High-F dead U_W | peak without usable support | focus ≠ exergy |

---

## 6. Two-theater rule

```text
F_attn     = geometry of context routing
F_vocab    = geometry of claim spend
never average them into one “F” without labeling theater
```

---

## 7. Ops checklist

1. Prefer logsumexp mass_basis stamps.  
2. Report \(n\) (T or V) with every F.  
3. \(F=0\) is a **measured** uniform field, not a missing meter.  
4. Never multiply F alone into Ω as “smart.”
