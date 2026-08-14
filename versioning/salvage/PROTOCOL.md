# Salvage protocol

Seals open. No invent-green.

Active agent. Not a reporter.

## Cadence

Hourly heartbeat 06:00–22:00 America/Detroit.
Full salvage if any dirty is found, or if last salvage is ≥3 hours old.
Prefer 3–4h spacing. Never skip a dirty because the clock is early.

## Invariant

Save as much data as possible.
Never delete, overwrite, or clean a surface until its current bytes are archived.

Order is locked:

1. DETECT
2. ARCHIVE
3. DIAGNOSE
4. CLEAN
5. VERSION
6. VERIFY

If a step is blocked, keep the archive and disclose residual. Do not invent a clean state.

## Dirty classes

- data-at-risk — only copy lives on a dirty surface
- unversioned — unique delta not on GitHub
- invent-green — claim without evidence
- contradiction — identity / non-contradiction failure
- orphan — no inbound lock
- seal-break — residual presented as proven
- phantom-mass — duplication / slop

## Clean rules

- Archive first, always.
- Relabel invent-green and seal-breaks. Do not erase the sentence.
- Contradictions: keep both readings in the archive. Promote the tighter lock.
- Orphans: attach to nearest kernel. Do not trash drafts.
- Phantom-mass: promote densest warrant. Store copies. Do not drop unique clauses.
- GitHub push when necessary: archive file, cleaned docs (with SHA), LEDGER append.

## Store

`versioning/salvage/YYYY-MM-DDTHH-MMZ.md`
`versioning/salvage/LEDGER.md`
