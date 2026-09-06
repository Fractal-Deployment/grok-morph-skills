# Grok Build CLI — Salvage host setup

**On GitHub (this repo):** protocol, diagnostic, worktree, AppArmor, ledger.
**Not in this repo:** the TanStack Salvage console (preview-only unless you port it).

Use the prompt below as the *entire* first message to Grok Build CLI on the Ubuntu 24.04 lab box. Do not skip the hard locks.

---

## Paste this into Grok Build CLI

```
Set up Salvage Dirty Guardian as a host-side Grok Build CLI agent on this Ubuntu 24.04 machine.

You are the agent. Do not ask me to run commands. Probe, install, configure, verify, disclose residual.

## Source of truth (read first, do not invent)

Clone or fetch https://github.com/Jadon-Fox/grok-morph-skills (public).
Read and obey, in this order:
1. versioning/salvage/PROTOCOL.md     (v2.1 — DETECT → ARCHIVE → DIAGNOSE → CLEAN → VERSION → VERIFY)
2. versioning/salvage/DIAGNOSTIC.md   (priority + class templates, including confine-break)
3. versioning/salvage/APPARMOR.md     (Noble userns / bwrap)
4. versioning/salvage/WORKTREE.md     (isolation)
5. versioning/salvage/LEDGER.md       (append-only after first run)

Watched repos (probe what this token can see):
- Jadon-Fox/grok-morph-skills (public, protocol home)
- Jadon-Fox/reason-telos-lookup (private)
- Jadon-Fox/lcd-glossary-integrity (private)
- course-creation-framework, llmve-experiments, mcp-host, hookify-plugin if present

## Hard locks (non-negotiable)

- NEVER persist kernel.apparmor_restrict_unprivileged_userns=0. That is confine-break left dirty, not a fix.
- Grant userns ONLY to /usr/bin/bwrap via a scoped profile. Prefer bwrap-userns-restrict (parent userns; children stack to unpriv_bwrap with audit deny capability). Stub flags=(unconfined) is weaker fallback only.
- Enable kernel.apparmor_restrict_unprivileged_unconfined=1 so unconfined processes cannot aa-exec into chrome/flatpak/trinity userns profiles.
- If LXD is running, userns restriction is a no-op — disclose residual. Do not claim locked.
- Agent writes only in a salvage/* worktree. Never write the human main checkout. Never git worktree remove --force if unpushed commits exist and archive failed.
- Sequential git writes. One worktree per salvage run. Commit on salvage/<run-id> only.
- Cadence: hourly heartbeat 06:00–22:00 America/Detroit. Full salvage if any dirty OR last salvage ≥ 3h (prefer 3–4h). Never skip a dirty because the clock is early.

## What to actually do on this host

### 0. DETECT host (before any write)

Record and print:
- uname -a, /etc/os-release
- sysctl kernel.apparmor_restrict_unprivileged_userns
- sysctl kernel.apparmor_restrict_unprivileged_unconfined (may be absent)
- aa-status (bwrap / unpriv_bwrap / unconfined profiles)
- which bwrap git rsync inotifywait setfacl
- bwrap --unshare-user --uid 0 echo ok   (expect EPERM if profile missing)
- whether lxd/incus is running
- id, groups, sudo -n true

If userns=1 and no bwrap profile / probe EPERM → open dirty class confine-break.
If you cannot sudo, stop host writes, archive the probe, residual the rest.

### 1. Packages

Install only what is missing:
apparmor apparmor-utils apparmor-profiles bubblewrap git rsync inotify-tools acl

### 2. AppArmor (CLEAN confine-break)

Archive APPARMOR.md + the profile text into versioning/salvage/ BEFORE loading policy.

Install /etc/apparmor.d/bwrap-userns-restrict from upstream extras (parent userns + unpriv_bwrap deny capability). Load with apparmor_parser -r. Do not enable a global userns=0 sysctl.d file.

Write /etc/sysctl.d/10-apparmor-hardening.conf with:
kernel.apparmor_restrict_unprivileged_unconfined=1
and sysctl --load it.

Re-probe bwrap --unshare-user --uid 0 echo ok.
Status stays residual until aa-status shows bwrap enforce-loaded AND the probe succeeds.

### 3. Permission rings

- Dedicated identity if missing: user `salvage` in group `salvage`. No passwordless sudo on the agent path except the minimum needed for apparmor_parser/sysctl on first setup. After setup, routine salvage runs as salvage with no sudo.
- Layout:
  ~/worktrees/grok-morph-skills/.bare   (bare clone)
  ~/worktrees/grok-morph-skills/main    (human; agent does not write)
  ~/worktrees/grok-morph-skills/salvage-<utc>  (agent worktree)
  ~/worktrees/vault/                    (rsync archive target if GitHub push blocked)
- ACL: default rwx for salvage on worktrees + vault. Deny write to ~/.ssh and /etc for the salvage user.

Follow WORKTREE.md exactly for create/remove.

### 4. Agent loop (systemd user timer preferred)

Create a user unit that:
- On the hour 06–22 America/Detroit: cheap DETECT (git status/fetch + AppArmor probe + inotify backlog).
- If any dirty OR last salvage ≥ 3h: run full PROTOCOL in a fresh worktree.
- ARCHIVE first (rsync -a --checksum dirty paths into versioning/salvage/YYYY-MM-DDTHH-MMZ.md).
- DIAGNOSE per DIAGNOSTIC.md, one dirty at a time, data-at-risk first.
- VERSION: commit on salvage/<run-id>, push that branch, append LEDGER.md, open/update PR to main if needed. Commit message: salvage: <date> <N> found, <A> archived, <C> cleaned
- VERIFY: re-probe cleaned paths + bwrap. STATUS clean | residual issues | critical. Never fake clean.

If GitHub push fails: keep the vault copy, gist or inline residual, do not delete.

### 5. First live run

Run DETECT now (not wait for the timer). Append one LEDGER line with real numbers. If no unique dirty exists, heartbeat CLEAN is enough — do not invent dirties.

### 6. Output (strict)

STATUS | found | archived | cleaned | pushes | next due
[ordered dirty table: path | class | action | residual]
[archive location(s)]
[aa-status bwrap line + bwrap probe result]
[residual path]

```

---

## After it finishes

Expect residual if: no sudo, LXD present, Flatpak shares the host, or GitHub token cannot see private repos.
Paste the STATUS block back here if you want the console/protocol updated from live numbers.
