# Norms & path gain (S4, S19)
---
## LayerNorm
\[
\mathrm{LN}(x) = \gamma \odot \frac{x-\mu}{\sqrt{\sigma^2+\varepsilon}} + \beta
\]
## RMSNorm (common modern)
\[
\mathrm{RMSNorm}(x) = \gamma \odot \frac{x}{\mathrm{RMS}(x)}
\]
---
## Why it matters for matmul geometry
- Norms **rescale** residual subspaces before Q/K/V/MLP reads. 
- Break pure linearity of virtual weights (path importance becomes input-dependent). 
- Pre-LN vs Post-LN changes gradient flow and whether residual is “clean.”
**Pre-LN (dominant):** stable deep training; residual is main highway. 
**Post-LN (original):** harder deep train; different path expansion.
---
## Odd
- LN can hide composition strength across layers (harder to compare heads by raw weight products). 
- γ scales can absorb into adjacent matmuls in analysis (careful when attributing).
