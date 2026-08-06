# Back-to-front walk (loss → which matmul)

Use for training pressure, credit assignment, and “what absorbs the fight.”

```text
[1] CE / sample grade on p (S22)
      ∇z = p - one_hot(y)     ## fight on V
[2] Through W_U (S20)
      pressure into final residual x_L
[3] Backward through layers L..1:
      MLP down/up/gate receive feature gradients
      Attn: ∂L/∂A and ∂L/∂V; then to Q,K via scores
      Softmax Jacobian reallocates only (row sum 0)
[4] Residual adds distribute credit to all prior writers
[5] Embed W_E (and tied head) absorb token-level pressure
```

**Observables:**

| Signal | Meaning |
|--------|---------|
| fight_width | how many vocab ids CE fights |
| grad top-m mass | concentration of update |
| Head-wise grad norm | which heads absorb |
| LoRA site energy | which BA updates |

**Odd:** softmax Jacobian zeros almost all directions when A is one-hot → brittle credit.  
**Odd:** deep residual can bury early-layer credit (vanishing path products).

Design: if fight_width is huge and F_vocab low, you are training noise on the claim medium — fix data/geometry before more steps.
