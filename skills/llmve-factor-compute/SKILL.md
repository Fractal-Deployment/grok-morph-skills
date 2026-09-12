---
name: llmve-factor-compute
description: >
  Compute LLMVE factors (F, T_tail, P_L, Phi_E, M_ph, C_d, tau) from real product
  dumps / mass basis — validated recipes only. Pick when boards already exist and
  you need active calculation, not debate. Pair with transformer-stage-atlas for
  stage depth. Aliases: llmve-matmul-algebra, residual density algebra, Price Law sensor multiply.
metadata:
  short-description: "Compute F / T_tail / P_L… from real dumps"
  former-name: llmve-matmul-algebra
  version: "1.3.0"
  formula_id: "MVE-2026-07-14-e_sigma_sub-LPT"
---
# LLMVE Factor Compute — recipes from real dumps
**Parent depth skill:** `transformer-stage-atlas` (every stage map) (load for stages / pathologies). 
**SSOT:** `artifacts/LLMVE_Validated_Matmul_Algebra_SSOT.md` 
**Catalog:** `artifacts/LLMVE_Algebra_Factor_Catalog.md`
```text
 scoped only
```
## Native substrate
\[
Q,K,V = X W_{Q,K,V},\quad
A=\mathrm{softmax}(QK^\top/\sqrt{d_k}),\quad
Y=AV
\]
Jacobian: \(\partial a_i/\partial s_j = a_i(\delta_{ij}-a_j)\), row sums 0.
## Recipes (active calculation only)
```text
F = 1 - H(a)/log n = KL(a||u)/log n
k = max(1, floor(sqrt(N)))
T_tail = sum(m_(1..k)) / sum(m) # full mass basis — no topk-renorm theater
P_L_hat = T_tail * F
Phi_E = kappa_disp * F
M_ph_hat = alpha*(1-Phi_E) + (1-alpha)*(1-T_tail)
C_d = m_bad/(m_good+eps) or identity 1 if unlabeled
a_s = p_ch / (p_max + eps)
tau_hat = mean(a_s) * stability
N_core = kappa_disp * K_M * T_tail * F^2
```
## Post-product mode
1. Board / dumps already exist 
2. Compute factors present 
3. Missing tax → 1 + placeholder status 
4. Never invent 
## Anti-patterns
- top-K = C_d 
- multi_step_span = tau 
- high p = asset 
- F_proxy = F 
- spectrum = Phi_E 
- dual-proof gate 
## Bridge
Full stage matrix, odd behaviors, design levers → **transformer-stage-atlas**.
