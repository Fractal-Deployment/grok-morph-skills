# Salvage protocol v2

Seals open. No invent-green. train_ok=false · measured_omega=false · G1=OPEN · endpointAssumed=false

Active agent. Not a reporter.

Companion files:
- `DIAGNOSTIC.md` — class → priority → warrant → lose-if-drop → steelman → action
- `WORKTREE.md` — local isolation for agent ops
- `LEDGER.md` — run history

---

## Cadence

Hourly heartbeat 06:00–22:00 America/Detroit.

| Condition | Action |
| --- | --- |
| No dirty AND last salvage < 3h | CLEAN heartbeat only (1 line). Stop. |
| Any dirty OR last salvage ≥ 3h | Full protocol |
| Dirty found before 3h gate | Full protocol anyway |

Prefer 3–4h salvage spacing. Never skip a dirty because the clock is early.

---

## Invariant (non-negotiable)

**Save as much data as possible.**

Never delete, overwrite, or clean a surface until its current bytes are archived.

If any step is blocked: keep the archive, disclose residual, do not invent a clean state.

---

## Phase contracts

Order is locked. Each phase has an entry condition and exit artifact.

### 1. DETECT

**Entry:** heartbeat or manual run  
**Exit artifact:** ordered dirty list `{path, class, evidence, priority, bytes?, unique?}`

Cheap probe first:
- GitHub: repo trees, recent commits, untracked/uncommitted surfaces when local access exists
- Drive: `modified_after` last salvage
- Priority sort: data-at-risk → unversioned → contradiction → orphan → seal-break → invent-green → phantom-mass

Name only what you can warrant. No invented dirties.

### 2. ARCHIVE

**Entry:** ≥1 dirty with evidence  
**Exit artifact:** salvage vault file exists (or full content in run output if push blocked)

Capture current content (or faithful digest + size + sha for huge files) **before any rewrite**.

Preferred store:
```
grok-morph-skills/versioning/salvage/YYYY-MM-DDTHH-MMZ.md
```

Fallback chain: reason-telos-lookup → gist → inline in run output.

**Hard gate:** do not enter DIAGNOSE/CLEAN without an archive artifact.

### 3. DIAGNOSE

**Entry:** archive exists  
**Exit artifact:** per-dirty diagnosis card

One dirty at a time, highest priority first. For each:

| Field | Meaning |
| --- | --- |
| warrant | what is true (evidence-bound) |
| residual | what is unknown / unsealed |
| lose-if-drop | what unique data dies if discarded |
| steelman leave-dirty | strongest case for not cleaning yet |

See `DIAGNOSTIC.md` for class templates. No theater. No extra agents invented.

### 4. CLEAN

**Entry:** diagnosis complete for the dirty being cleaned  
**Exit artifact:** status `cleaned` | `residual` + action string

Rules:
- Relabel invent-green / seal-break. Do not erase the sentence.
- Contradiction: keep both readings in archive. Promote tighter lock.
- Orphan: attach to nearest kernel. Do not trash drafts.
- Phantom-mass: promote densest warrant. Store copies. Do not drop unique clauses.
- data-at-risk / unversioned: archive is the clean; working copy may stay.

Do not flatten disagreement into silence. Do not drop unique data to make a doc pretty.

### 5. VERSION

**Entry:** at least one archive or clean completed  
**Exit artifact:** GitHub commit SHA(s) + LEDGER line

Push when necessary:
1. salvage archive file
2. any cleaned doc actually edited (SHA required on update)
3. LEDGER.md append: date, found, archived, cleaned, residual, notes

Commit message: `salvage: <date> <N> found, <A> archived, <C> cleaned`

### 6. VERIFY

**Entry:** VERSION done or blocked with residual  
**Exit artifact:** status + residual path

Re-probe cleaned paths.

| Status | Meaning |
| --- | --- |
| clean | no open high-risk dirty; residuals labeled |
| residual issues | open residual or weaker readings kept |
| critical | data-at-risk or unique open dirty remains |

If clean is fake, say residual and keep the archive.

---

## Output (strict)

```
STATUS | found | archived | cleaned | pushes | next due
[ordered dirty table: path | class | action | residual]
[archive location(s)]
[residual path]
```

Be fully agentic. Figure blocked access out. Never ask the user to run commands.

---

## Local agent ops

When running on a Linux host (not only Grok cloud tools):
- Prefer worktree isolation — see `WORKTREE.md`
- Archive via `rsync -a --checksum` or `git archive` before any clean write
- Never `git worktree remove --force` if unpushed commits exist
