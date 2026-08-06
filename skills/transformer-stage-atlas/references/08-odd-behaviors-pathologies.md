# Odd behaviors & pathologies (catalog)

Use this as a **diagnostic checklist**, not a green list.

---

## A. Initialization / depth

| Pathology | Mechanism | Fix levers (research) |
|-----------|-----------|----------------------|
| Rank collapse **depth** | stacked attn + softmax mixes tokens toward same vector | residual scale, better init, spectral fixes |
| Rank collapse **width** | Markov spectral gap \(s_1=1 \gg s_2\) | center A (remove all-ones), scale Q/K carefully (Mind the Gap) |
| Exploding / vanishing grads | product of singular values over L | Pre-LN, residual, careful init variance |
| Logit blow-up | unscaled \(d_k\) or norm drift | \(\sqrt{d_k}\), QK-norm, temperature |

---

## B. Attention runtime

| Pathology | Sign |
|-----------|------|
| Entropy collapse | max(A)→1, F→1, off-peak grad ~0 |
| Attention sink | mass on first/BOS token |
| Dead head | OV≈0 or A nearly uniform always |
| Induction failure | no K-composition with prev-token head |
| Skip-trigram bug | OV×QK factorization predicts wrong combo |

---

## C. Weight spectra (ore)

| Observation | Reading (inventory only) |
|-------------|--------------------------|
| Large σ outliers vs MP bulk | feature learning / spikes |
| **Small** σ outliers (non-square Up/Down) | **also** carry info — ablation hurts |
| Attention-Output few outliers | often **lazy** relative to Q/K/V |
| stable_rank ≪ rank budget | rank not used (geometry of update) |

**Forbidden:** MP bulk = friction; spectrum alone = Φ_E.

---

## D. Training / preference

| Pathology | Sign | Book (if instrumented) |
|-----------|------|------------------------|
| Synthetic consistency tax | free≈forced until load rises | candidate \(e^{\sigma}\) |
| Claim dilution | support_width↑, F_vocab↓, grade↓ | \(C_d\) (needs labels) |
| Phantom spend | recovery with no usable-W map | \(M_{\mathrm{ph}}\) |
| Train theater | open_count=0 + dead F | **not** measured_omega |

---

## E. LLMVE-linked pathology notes (from SSOT)

- \(F\to 1\): brittle routing; background share \(\to 1-\kappa_{\mathrm{disp}}\).  
- Extreme focus under no-go policy → candidate \(\sigma_{\mathrm{sub}}\), not automatic \(M_{\mathrm{ph}}\).  
- High probability ≠ asset. Asset = compositional density in pretrain geometry.  
- Dual-proof gate is **erased**; dual = theory lanes.

---

## F. Quick triage flow

```text
symptom
  → stage matrix (which S#)
  → pathology table (A–D)
  → instrument that stage only
  → claim_class partial
  → one knob intervention
  → remeasure
```
