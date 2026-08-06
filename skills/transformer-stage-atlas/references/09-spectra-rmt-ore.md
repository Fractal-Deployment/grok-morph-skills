# Spectra, RMT, ore inventory (S23)

**Jurisdiction:** inventory / capacity geometry **only**. Not Φ_E, not C_d, not friction.

---

## 1. Marchenko–Pastur null

For Wishart-like noise with aspect \(c=m/n\), variance \(\sigma^2\):

\[
\lambda_\pm = \sigma^2(1\pm\sqrt{c})^2
\]

Bulk inside edges ≈ random; outliers above (and for non-square, below) ≈ structure.

---

## 2. What transformers actually show

| Matrix | Typical spectrum note |
|--------|----------------------|
| Q, K, V | large outliers; feature learning |
| Attention O | fewer outliers; often **lazy** |
| MLP Up/Down/Gate | large **and small** outliers matter |

Ablating small singular values on Down-Projection can crush quality — small ≠ noise.

---

## 3. Practical engine: RSVD

On 12 GiB: randomized SVD (Halko) with oversampling p≈10, power q∈{1,2,4}.

Emit:

- top-k Σ  
- stable_rank = \(\|W\|_F^2/\|W\|_2^2\)  
- eff_rank (entropy of normalized σ)  
- energy_at_r  
- mp edges, n_outliers_hi/lo, mp_fit_quality  

claim_class=partial · maps_to=ore_inventory · not_Phi_E

---

## 4. Rank collapse vs unused rank

| Concept | Meaning |
|---------|---------|
| Rank collapse (width/depth) | representations become linearly dependent |
| stable_rank ≪ budget | update/weight does not use full LoRA/base rank |

Both are inventory signals; neither is train_ok.

---

## 5. Three-books ban list

```text
spectrum ≠ measured Φ_E
MP bulk ≠ e^σ friction
outlier_energy_frac ≠ P_L
energy_at_r ≠ train_ok
mp_fit=poor ≠ invent structure
```
