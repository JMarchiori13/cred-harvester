# src/sam — Offline parsing of SAM/SYSTEM/SECURITY hives

📖 Research notes: [docs/sam-offline.md](../../docs/sam-offline.md)

## Module scope

**Offline** parsing of the lab's registry hives. This module never touches a live system — it operates on hive copies obtained via Volume Shadow Copy or `reg save` in the lab.

## Planned experiments

| # | Experiment | Artifact |
|---|---|---|
| S1 | Obtaining the copies: `vssadmin` + shadow copy, and `reg save` (SeBackupPrivilege) | SAM, SYSTEM, SECURITY |
| S2 | BootKey extraction from the SYSTEM hive | SYSTEM |
| S3 | SAM structure parser (F-value, V-value, RID) — reference: impacket | SAM |
| S4 | LSA secrets and cached credentials enumeration (structure, no cracking) | SECURITY |

## Conventions

- Language: Python 3 — impacket as implementation reference, but with original code documented line by line for educational purposes
- Hives copied to `lab/hives/` stay **out of git** (`.gitignore`)
