# Residual stream (S3, S12, S16)

---

## 1. Communication channel

\[
x_{\ell+1} = x_\ell + h_{\mathrm{attn}}(x_\ell) + m_{\mathrm{mlp}}(x_\ell)
\]

(Pre-LN variants apply LN **inside** the branches.)

- Residual stream is the **only** cross-layer highway.  
- Dimension \(d\) is a **bandwidth bottleneck** (MLP often \(4d\) intermediate).  
- Subspaces: different features ride nearly orthogonal directions; heads/MLPs read/write subspaces.

---

## 2. Virtual weights

Because writes are linear (modulo LN/softmax), path products form **virtual weights**:

\[
W_{\mathrm{virt}} = W_{\mathrm{read}}^{\ell_2}\, W_{\mathrm{write}}^{\ell_1}
\]

Enables path expansion: logits ≈ sum of direct bigram path + head paths + composed paths.

---

## 3. Memory management

- Positive cosine / eigenvalues of OV → copy / reinforce.  
- Negative → **deletion** / suppression (memory management).  
- Overwrite: later writes dominate if not residual-protected.

---

## 4. Energy geometry (optional sensors)

\[
E_{\mathrm{tot}} = \sum_\ell \|x_\ell\|_2^2
\]

With focus-based luminous share (LLMVE):

\[
E_{\mathrm{lum}} = \Phi_E E_{\mathrm{tot}},\quad E_{\mathrm{bg}}=(1-\Phi_E)E_{\mathrm{tot}}
\]

**Not** FLOPs-as-exergy.

---

## 5. Free vs forced residual (path drag)

Same weights, vary only enforcement/context load:

- Free residual vs forced preference/consistency  
- Measure recovery / support-restricted usable mass  
- Residual **compounding** cost after \(C_d,M_{\mathrm{ph}}\) separation → candidate \(e^{\sigma}\)  
- See H-STASI-σ-1; dual lanes not dual-proof
