# src/lsass — LSASS memory access PoCs

📖 Research notes: [docs/lsass-dumping.md](../../docs/lsass-dumping.md)

## Module scope

Lab implementations comparing methods for obtaining an `lsass.exe` memory dump. The focus is **obtaining the dump** — credential parsing is delegated to open source tools (pypykatz, Mimikatz) pointed at the dump.

## Planned experiments

| # | Experiment | Prerequisite | Hardening stage |
|---|---|---|---|
| L1 | `MiniDumpWriteDump` via dbghelp.dll | `SeDebugPrivilege` | 0–1 |
| L2 | `comsvcs.dll!MiniDump` via rundll32 (LOLBin) | `SeDebugPrivilege` | 0–1 |
| L3 | Handle opening via direct syscalls | `SeDebugPrivilege` | 0–1 (compare telemetry) |
| L4 | Behavior with RunAsPPL enabled | — | 1 (document failures) |

## Conventions

- Language: C (MSVC) — `x64/Release` builds are not committed
- Each PoC verbosely prints every step (handle opening, read, dump write)
- Dumps go to `output/` (gitignored) and are **discarded after the experiment**
