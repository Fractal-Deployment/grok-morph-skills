# Salvage protocol v2.1
Active agent. Not a reporter.
Companion files:
- DIAGNOSTIC.md — class → priority → warrant → lose-if-drop → steelman → action
- WORKTREE.md — local isolation for agent ops
- APPARMOR.md — Noble host confinement, bwrap profiles, permission rings
- LEDGER.md — run history
## Cadence
Hourly heartbeat 06:00–22:00 America/Detroit.
- No dirty AND last salvage < 3h → CLEAN heartbeat only. Stop.
- Any dirty OR last salvage ≥ 3h → full protocol.
- Dirty found before 3h gate → full protocol anyway.
## Invariant
Save as much data as possible. Never delete, overwrite, or clean a surface until its current bytes are archived.
If any step is blocked: keep the archive, disclose residual, do not invent a clean state.
Never persist kernel.apparmor_restrict_unprivileged_userns=0 to make the agent start. That is a confine-break left dirty, not a clean.
## Phase contracts
### 1. DETECT
Entry: heartbeat or manual run.
Exit: ordered dirty list {path, class, evidence, priority, bytes?, unique?}.
Cheap probe first:
- GitHub trees, recent commits, untracked surfaces when local access exists
- Drive modified_after last salvage
- Host AppArmor: sysctl userns + unconfined-restrict, aa-status bwrap, bwrap --unshare-user probe. If userns=1 and profile missing → open confine-break. See APPARMOR.md.
Name only what you can warrant. Host probe without live aa-status must be labeled assumed.
### 2. ARCHIVE
Entry: ≥1 dirty with evidence.
Exit: salvage vault file exists (or full content in run output if push blocked).
Capture current content before any rewrite.
Preferred: grok-morph-skills/versioning/salvage/YYYY-MM-DDTHH-MMZ.md
Fallback: reason-telos-lookup → gist → inline.
Hard gate: do not enter DIAGNOSE/CLEAN without an archive artifact.
### 3. DIAGNOSE
Entry: archive exists.
Exit: per-dirty diagnosis card (warrant, residual, lose-if-drop, steelman).
One dirty at a time, highest priority first. See DIAGNOSTIC.md.
### 4. CLEAN
Entry: diagnosis complete for the dirty being cleaned.
Exit: status cleaned | residual + action string.
- Contradiction: keep both readings. Promote tighter lock.
- Orphan: attach to nearest kernel. Do not trash drafts.
- Phantom-mass: promote densest warrant. Store copies.
- data-at-risk / unversioned: archive is the clean; working copy may stay.
- confine-break: ship scoped bwrap-userns-restrict; enable unconfined-restrict; never global userns=0. Status stays residual until live aa-status.
### 5. VERSION
Push when necessary: salvage archive, cleaned docs (SHA required), LEDGER append.
Commit: salvage: <date> <N> found, <A> archived, <C> cleaned
### 6. VERIFY
Re-probe cleaned paths. Re-probe bwrap if confine-break was in the run.
- clean: no open high-risk dirty; residuals labeled
- residual issues: open residual or weaker readings kept
- critical: data-at-risk or unique open dirty remains
If clean is fake, say residual and keep the archive.
## Local agent ops
- Worktree isolation — WORKTREE.md
- Confinement — APPARMOR.md. Keep userns restriction on.
- Archive via rsync -a --checksum or git archive before any clean write
- Never git worktree remove --force if unpushed commits exist
