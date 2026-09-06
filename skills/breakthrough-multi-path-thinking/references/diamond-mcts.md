# Diamond-MCTS-R2

## Selection

Maintain visits/values per op in {define, redefine, explore, adapt}.

```text
score(op) = value(op) + c * sqrt(log(N+1) / visits(op))
c default 1.5; branch top 4 (or all four)
```

After simulation, update value of chosen op from retain score:

```text
retain = telos_fit * residue_quality - invent_green_risk - 0.1 * drift
```

## Reroot (mandatory every 2 by default)

```text
root_prompt must:
  - still be answerable as the original user charge
  - include marker ids and key warrants
  - list OPEN items explicitly
```

## Lenses (explore)

first-principles · analogical · counterfactual/pre-mortem · systems · probabilistic · narrative · genius-council

User knobs may subset lenses.

## Stop

marginal retain gain < ε · budget · user interrupt  
