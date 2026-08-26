# Security & verification — what the Audit seat contributes

**Dane Brown — Kairo Vault Technologies GK** (Huge Green Candle), OneXah DAO council, Audit & security.
Point-in-time as of **2026-08-19** — re-run before formal submission rather than quoting from here.

A summary of the on-chain verification behind the Audit seat. Full method and evidence live in the audit
repo, where several sitting members already have access.

---

## What has been verified

**Both raven guard builds running on OneXah accounts have no fund-moving path.**

| | v4.8 | v4.6 |
|---|---|---|
| `HookHash` | `91366A46…F46D02` | `D9BD75DD…` |
| Size | 30,800 B | 25,512 B |
| Source == deployed | ✅ | ✅ (from the `live/raven-D9BD75DD` tag) |
| Emission templates | 4 × `Invoke`, 1 × `TrustSet` | identical |
| `Payment` template | **none** | **none** |

A guard installed on an account holding user funds therefore cannot move those funds. The guard runs
fleet-wide — the DAO, all three AMM pools, both lending pools, and perps. Source-to-deployment
verification was last re-run **2026-08-19** on the then-current build (`91366A46…`); the current fleet
build (`4B04925A…`) is re-verified by the same method before formal submission. Full live-build list:
**[live-hooks.md](live-hooks.md)**.

## Scope

Verification is in-house and fully reproducible — a hook counts as verified only when repository source
compiles to bytecode whose hash matches the live `HookDefinition`, re-checkable by any member from public
chain data. The guard fails open on a registry-read miss **by design** — an availability choice that never
lets it move funds. Full method, per-build provenance, and audit evidence are available to sitting members
on request.

## Method, briefly

Reads come from two node endpoints (`xahau.network`, `xahau.org`) with distinct `pubkey_node`, and
disagreement stops the check rather than being resolved by preference — though that is endpoint diversity,
not operator diversity, since both are Xahau-core-associated. A hook counts as verified only when
repository source builds to bytecode whose hash matches the live `HookDefinition`, and behaviour is read
from the import table rather than from documentation.
