# Salvage host AppArmor protocol

Seals open. Host not live-scanned from this file. train_ok=false · endpointAssumed=false

Companion: PROTOCOL.md (DETECT now probes confinement) · DIAGNOSTIC.md (confine-break).

## Warrant (research, 2026-08)

Ubuntu 24.04 Noble enables kernel.apparmor_restrict_unprivileged_userns=1 via /usr/lib/sysctl.d/10-apparmor.conf when AppArmor userspace is installed.

Unprivileged processes may create user namespaces only if an AppArmor profile grants userns. Without it: bwrap: setting up uid map: Permission denied. Agent sandbox AGENT_CRASHED.

Ubuntu shipped then reverted default-enable of bwrap-userns-restrict after Flatpak regressions (LP#2072811). Current Noble often has no bwrap profile out of the box. The extras profile lives in apparmor-profiles, not enabled by default.

## Hard locks

1. Do not persist kernel.apparmor_restrict_unprivileged_userns=0. That is the weak fix.
2. Grant userns only to /usr/bin/bwrap via a scoped profile.
3. Prefer restrict (parent userns + children stacked to unpriv_bwrap with audit deny capability) over the five-line flags=(unconfined) stub.
4. Enable kernel.apparmor_restrict_unprivileged_unconfined=1 so unconfined processes cannot aa-exec into chrome/flatpak/trinity userns profiles (Qualys-class bypass).
5. If LXD is running, the userns restriction is a no-op. Disclose residual.

## DETECT probe (host)

- sysctl kernel.apparmor_restrict_unprivileged_userns
- sysctl kernel.apparmor_restrict_unprivileged_unconfined
- aa-status grep bwrap|unpriv
- bwrap --unshare-user --uid 0 echo ok

If userns=1 and no bwrap profile / probe EPERM, open confine-break.

## CLEAN (confine-break)

Archive this file + the restrict profile before any host write.

Install: apparmor apparmor-utils apparmor-profiles bubblewrap git rsync inotify-tools acl

Load restrict profile with apparmor_parser -r. Enable unconfined-restrict via /etc/sysctl.d/10-apparmor-hardening.conf.

Never write a sysctl.d file that sets userns=0.

Status after: residual until aa-status from the actual box confirms the profile is enforce-loaded.

## Permission rings

- kernel: userns restrict = 1
- profile: only bwrap gets userns; children lose capabilities
- identity: dedicated salvage user; no passwordless sudo on agent path
- paths: ACL rwx on ~/worktrees + versioning/salvage vault; deny write ~/.ssh and /etc
- git: one worktree per run; never worktree remove --force if unpushed

## Residual

- This file does not equal a live aa-status.
- LXD disables the restriction.
- Stub profile works but does not strip child capabilities.
- Restrict profile previously broke some Flatpaks; salvage agent is not Flatpak — still disclose if desktop Flatpak shares the host.
