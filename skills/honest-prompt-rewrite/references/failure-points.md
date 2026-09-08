# Failure points — this charged action only

A **failure point** is a kill condition for **one** charged action.
It is not a seal. It is not inventory. It does not ride into the next charge.

## Rules

1. Name the action in one sentence (`THIS_ACTION`).
2. List only what would make **that** action fail (`fail_if`).
3. Each point needs an observable trip (`trip`).
4. When the action ends, discard the list. Next charge starts empty.
5. Do not copy last charge's points forward.
6. Do not print a standing status block.
7. Do not restore deleted inventory names as live fields.

## Shape

```text
THIS_ACTION: <one sentence>
FAILURE_POINTS:
  - fail_if: <condition that kills THIS action>
    trip: <what we would observe>
```

Maximum six points. If you need more, the action is too big. Split the charge.

## Not failure points

- A banner that must stay false forever
- A health score for the model or the repo
- A field that multiplies into Ω
- Forward-looking "so we do not forget"
- Eloquence, length, or humility as proof the action succeeded

## Contract

If a listed trip fires, **this action fails**. Stop. Do not narrate through.
If no trip fires, that is not success-of-product. It is only "this action did not hit its own kill conditions."
