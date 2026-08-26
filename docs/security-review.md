# Security & verification — what the Audit seat contributes

**Dane Brown — Kairo Vault Technologies GK** (Huge Green Candle), OneXah DAO council, Audit & security.
Point-in-time — re-verify against chain before formal submission rather than quoting from here.

A summary of the on-chain verification behind the Audit seat. Full method and evidence live in the audit
repo, where several sitting members already have access.

---

## What has been verified

**The raven guard carries no fund-moving path.** Its entire emission surface is `Invoke` + `TrustSet` —
there is **no `Payment` template** in the build — so a guard installed on an account holding user funds
cannot move those funds.

| | Raven guard — v4.9 (current fleet) |
|---|---|
| `HookHash` | `4B04925A…CFC8741` |
| Source == deployed | ✅ repository source rebuilds to the live hash (re-checked 2026-08-25) |
| Emission surface | `Invoke` + `TrustSet` |
| `Payment` template | **none** |

v4.9 is v4.8 hardened with audit fixes #152/#153 (report-gating on cooldown-persist + emit-success). The
guard runs fleet-wide — the DAO, all three AMM pools, both lending pools, and perps. Full live-build list:
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
