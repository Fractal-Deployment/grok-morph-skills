# Front-to-back walk (token → distribution)
Use when explaining or debugging the forward pass end-to-end.
```text
[1] TEXT
      → tokenizer (S0)
[2] ids
      → W_E rows (S1) + position (S2) → x_0
[3] for ℓ = 1..L:
      x → LN (S4)
      → W_Q,W_K,W_V (S5–S7)
      → scores QKᵀ/√d (S8) [+ mask/RoPE effect]
      → softmax_row A (S9) ## context mass clearing
      → AV → W_O (S10–S11)
      → residual add (S12)
      x → LN
      → MLP up/gate/down (S13–S15)
      → residual add (S16)
[4] final LN (S19)
[5] x W_U → logits (S20)
[6] softmax_V → p (S21) ## claim mass clearing
[7] sample / argmax / CE (S22)
```
**Checkpoints to instrument on a new stack:**
1. After S9: F_attn, T_tail_attn per layer 
2. After S15: activation energy + weight stable_rank 
3. After S21: F_vocab, T_tail_vocab, support_width 
4. Free vs forced residual around S12 
**Narrate only what is measured.** Missing dump = wire gap, not “undefined algebra.”
