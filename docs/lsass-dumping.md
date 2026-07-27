# T1003.001 — LSASS Memory Dumping

Research notes on accessing `lsass.exe` memory to extract authentication material.

## Why LSASS

The Local Security Authority Subsystem Service keeps credentials from interactive sessions in memory: NTLM hashes, Kerberos tickets, and (on systems without hardening) cleartext secrets via WDigest.

## Documented methods

| Method | Notes |
|---|---|
| `MiniDumpWriteDump` (dbghelp/dbgcore) | Classic method; requires `SeDebugPrivilege` and a handle with `PROCESS_VM_READ` |
| `comsvcs.dll` via rundll32 | LOLBin — `MiniDump` export; no external tooling |
| Task Manager / ProcDump | Signed legitimate tools; manual dump |
| Direct syscalls | Avoids EDR user-mode hooks on `OpenProcess`/`ReadProcessMemory` |
| Handle duplication / fork | Indirect access via existing handles |

## Hardening that affects the technique

- **RunAsPPL** (LSA Protection) — blocks process opening by non-PPL processes
- **Credential Guard** (VBS) — isolates secrets in LSAIso
- **WDigest `UseLogonCredential=0`** — removes cleartext secrets

## Lab checklist

- [ ] Baseline: VM without RunAsPPL, fictitious credentials logged in
- [ ] Repeat with RunAsPPL enabled and document the behavior difference
- [ ] Compare generated telemetry (Sysmon Event ID 10 — ProcessAccess)
