# Salvage diagnostic matrix
Used in PROTOCOL phase 3 (DIAGNOSE). Priority is salvage order — highest first.
## Priority order
| Rank | Class | Why first |
| --- | --- | --- |
| 0 | data-at-risk | Only copy; irreversible loss |
| 1 | unversioned | Unique delta not on remote |
| 2 | confine-break | Agent sandbox / userns profile gap; run may crash |
| 3 | contradiction | Identity failure across locks |
| 4 | orphan | No inbound lock; draft may be unique |
| 7 | phantom-mass | Duplication; usually recoverable |
## confine-break
| Field | Template |
| --- | --- |
| warrant | Noble userns restriction is on and no (or stub-only) bwrap profile is loaded. LP#2072811 reverted default-enable. |
| residual | Live aa-status unknown unless the lab box was scanned. LXD presence unknown. |
| lose-if-drop | Not unique prose — the agent path. Unsandboxed run or AGENT_CRASHED. |
| steelman leave-dirty | Global sysctl userns=0 would start bwrap. It also opens every unprivileged process. |
| action | Keep userns=1. Ship bwrap-userns-restrict. Enable unconfined-restrict=1. Archive the profile. |
| status after | residual until live aa-status confirms enforce |
## Logic locks
- Identity: a dirty is the same object before and after archive (content SHA).
- Non-contradiction: do not claim cleaned if archive missing.
- Excluded middle: status is one of the closed set — not mostly clean.
- Confinement: do not claim host locked without live aa-status.
