# Salvage diagnostic matrix

Seals open. No invent-green.

Used in PROTOCOL phase 3 (DIAGNOSE). Priority is salvage order — highest first.

---

## Priority order

| Rank | Class | Why first |
| --- | --- | --- |
| 0 | data-at-risk | Only copy; irreversible loss |
| 1 | unversioned | Unique delta not on remote |
| 2 | contradiction | Identity failure across locks |
| 3 | orphan | No inbound lock; draft may be unique |
| 4 | seal-break | Residual presented as proven |
| 5 | invent-green | Claim without board |
| 6 | phantom-mass | Duplication; usually recoverable |

---

## Per-class templates

### data-at-risk

| Field | Template |
| --- | --- |
| warrant | Unique bytes exist only on this surface. No remote SHA. |
| residual | Whether a second copy exists offline (unknown until probed). |
| lose-if-drop | Full byte count of the surface. Irreversible if discarded. |
| steelman leave-dirty | Leave dirty until a second copy exists. Archive first always. |
| action | Archive full bytes. Snapshot commit. Working copy left intact. |
| status after | cleaned (if archived) or critical (if archive failed) |

### unversioned

| Field | Template |
| --- | --- |
| warrant | Working tree holds uncaptured delta vs last salvage SHA. |
| residual | Which hunks are unique vs already mirrored elsewhere. |
| lose-if-drop | Examples, later edits, uncommitted structure. |
| steelman leave-dirty | Wait for human commit. Risk is accidental clobber. |
| action | Archive delta. Commit snapshot. Do not force-clean working tree. |
| status after | cleaned |

### invent-green

| Field | Template |
| --- | --- |
| warrant | Claim presented as sealed without measurement board / evidence atom. |
| residual | Author may hold a private board not in repo. |
| lose-if-drop | Usually nothing unique if only relabeling. Sentence stays. |
| steelman leave-dirty | Private board may exist. Relabel as residual; do not delete. |
| action | Relabel claim as residual. Sentence retained. |
| status after | cleaned + residual note |

### contradiction

| Field | Template |
| --- | --- |
| warrant | Two locked definitions cannot both be identity-true. |
| residual | Which lock is tighter is a judgment with evidence. |
| lose-if-drop | Dropping either reading erases a real disagreement. |
| steelman leave-dirty | Keep both until a higher lock adjudicates. |
| action | Both readings archived. Tighter lock promoted. Weaker kept residual. |
| status after | residual |

### orphan

| Field | Template |
| --- | --- |
| warrant | No inbound lock from kernel / schema / parent doc. |
| residual | Content may still be unique draft material. |
| lose-if-drop | Often the only draft of a later lock. |
| steelman leave-dirty | Attach later; do not trash for neatness. |
| action | Attach to nearest kernel schema. Draft retained. |
| status after | cleaned |

### seal-break

| Field | Template |
| --- | --- |
| warrant | Residual presented as proven. |
| residual | Operational notes beside the overclaim may be unique. |
| lose-if-drop | Tone only — unless unique ops notes sit beside it. |
| steelman leave-dirty | Restore residual label. Keep operational note. |
| action | Restore residual label. Operational note kept. |
| status after | cleaned |

### phantom-mass

| Field | Template |
| --- | --- |
| warrant | Near-duplicates inflate mass without new warrant. |
| residual | One wording variant may hide a unique clause. |
| lose-if-drop | Unique clause if any. |
| steelman leave-dirty | Archive all variants before promoting densest. |
| action | Densest recap promoted. Duplicates archived as copies. |
| status after | cleaned + residual note on copies |

---

## Diagnosis card format (emit per dirty)

```
path: <repo>/<path>
class: <class>
priority: <0-6>
bytes: <n or unknown>
unique: true|false|unknown
warrant: ...
residual: ...
lose-if-drop: ...
steelman: ...
action: ...
status: open|archived|cleaned|residual|critical
```

## Logic locks

- Identity: a dirty is the same object before and after archive (content SHA).
- Non-contradiction: do not claim cleaned if archive missing.
- Excluded middle: status is one of the closed set above — not "mostly clean."
