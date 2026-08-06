# MLP / FFN (S13–S16)

---

## 1. Forms

**Classic GELU FFN:**

\[
m = W_{\mathrm{down}}\,\sigma(W_{\mathrm{up}} x)
\]

**SwiGLU (LLaMA-style):**

\[
m = W_{\mathrm{down}}\big(\mathrm{SiLU}(W_{\mathrm{gate}} x)\odot (W_{\mathrm{up}} x)\big)
\]

Shapes: \(d \to d_{\mathrm{ff}}\) (often \(8d/3\) rounded for SwiGLU) \(\to d\).

---

## 2. Role in residual geometry

- MLP expands to a **privileged** (or semi-privileged) basis of features.  
- Often implements key-value style memory, feature detection, cleanup.  
- Wider rank than attention OV — capacity for many sparse features.

---

## 3. Spectra (critical)

Non-square Up/Down/Gate matrices:

- Deviate from Marchenko–Pastur at **both** large **and small** singular values.  
- Small singular values **carry task-relevant information** (ablation raises perplexity).  
- Do **not** truncate small σ casually for “compression theater.”

Sensors: stable_rank, eff_rank, energy_at_r, n_outliers_hi/lo, mp_fit_quality.

---

## 4. Odd behaviors

| Behavior | Note |
|----------|------|
| Dead neurons | gate≈0 always |
| Superposition | more features than dimensions |
| Lazy regime | weights stay near init; few outliers |
| Polysemanticity | one neuron multi-feature |

---

## 5. Design levers

- \(d_{\mathrm{ff}}/d\) ratio  
- SwiGLU vs GELU  
- MoE experts (sparse matmuls)  
- LoRA on up/down vs attn sites — rank use via energy_at_r
