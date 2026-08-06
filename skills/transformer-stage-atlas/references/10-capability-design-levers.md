# Capability & design levers — better LLM from substrate

Use after stage audit + pathology scan. Propose **one primary lever** per campaign.

---

## 1. Architecture levers (shape of matmuls)

| Lever | Stage | Trade |
|-------|-------|-------|
| d_model | all | capacity vs bandwidth bottleneck |
| n_layers | depth composition | programs vs collapse risk |
| n_heads / d_k | QK rank | specialization vs compute |
| GQA/MQA | K,V share | long-ctx cost |
| d_ff ratio / SwiGLU | MLP | feature width |
| MoE | sparse MLP matmuls | capacity at fixed FLOPs |
| context window + RoPE scale | S2,S8 | long-range geometry |
| Pre-LN vs Post-LN | S4 | train stability |

---

## 2. Geometry levers (how mass moves)

| Lever | Targets | Success signal |
|-------|---------|----------------|
| Softmax scale / QK-norm | entropy collapse | F in healthy band, not always 1 |
| Attention sinks / window / DiffAttn | dead or sink mass | T_tail meaningful |
| Center / spectral fix | rank collapse width | stable rank of A |
| Vocab quality / glossary | C_d | labeled purity, grade hold |
| LoRA rank placement | ore use | energy_at_r, stable_rank of BA |

---

## 3. Training / data levers

| Lever | Note |
|-------|------|
| Data density (compositional) | pretrain “ore” quality |
| Synthetic loop load | watch free vs forced path drag |
| Preference / safety strength | can raise \(e^{\sigma}\) if enforced Second Reality |
| CE vs other objectives | fight_width on V |

**Never** use Ω as train reward (Stasi bureaucracy of the meter).

---

## 4. Decision procedure (operator)

```text
1. Pick stage S# with worst residual honesty gap
2. Choose one lever from tables above
3. Instrument: pre dump → intervene → post dump
4. Metrics: F, T_tail, P_L, U_W, stable_rank, grade if labeled
5. claim_class=partial; seals held
6. Accept / revert; do not multiply into unrestricted Ω
```

---

## 5. “Best version” criteria (honest)

A better LLM under this skill:

1. Uses rank budget (ore) without lazy critical maps  
2. Maintains non-collapsed routing (F not stuck at 0 or 1)  
3. Clears claims on V without uncontrolled dilution  
4. Composes depth into circuits (induction etc.) without depth collapse  
5. Keeps path drag (enforcement) instrumented and bounded  
6. Never confuses theater metrics with measured science
