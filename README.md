# Grok Build Morph Skills Pack

**Stamp:** 2026-08-06  
**Seals:** `train_ok=false` · `measured_omega=false` · `G1=OPEN` · `endpointAssumed=false`

Prompt-morph controller pack for Grok Build / CLI:

| Skill | Role |
|-------|------|
| **morph-shared** | Shared spine — state machine, geometries, **CONTRACT_LRR** |
| **deep-think** v2 | Diamond-MCTS-R2 introspective morph + direction knobs |
| **deep-research** v2 | Hourglass-EDC evidence morph + light lookup path |
| **argueforge** v2.1 | Truth crucible + LLMVE factor-identity mode |

No plugin binary required. Copy `skills/*` into your Grok skills directory (e.g. workspace `.grok/skills/` or host skill root) so the CLI can load `SKILL.md` by name.

## Install (CLI / host)

```bash
# clone
git clone https://github.com/Jadon-Fox/grok-morph-skills.git
# copy skills into your skills root
cp -R grok-morph-skills/skills/* /path/to/.grok/skills/
```

Or sparse-add into `training_orchestrator` docs if you keep agent skills mirrored there.

## Pipelines

```text
deep-think (steer) → morph-shared state → deep-research (chart)
morph-shared mode=shared   # full projection
deep-research light        # simple lookup
argueforge                 # contested identity / tournament
```

## CONTRACT_LRR (contract gate)

- **Logic** — three laws, fallacies, semantic integrity  
- **Ration** — pattern markers for next expand  
- **Reason** — evidence only with necessity warrant + marker attach  

## Non-claims

Skill text ≠ residual science on GPU. Tournament / morph winners ≠ measured Ω.

## Layout

```text
skills/
  morph-shared/
  deep-think/
  deep-research/
  argueforge/
```
