# T1003.002 — SAM / SECURITY Hives Offline

Research notes on offline extraction of local credentials.

## Artifacts

| Hive | Path | Contents |
|---|---|---|
| SAM | `%WINDIR%\System32\config\SAM` | NTLM hashes of local accounts |
| SYSTEM | `%WINDIR%\System32\config\SYSTEM` | BootKey/SysKey — required to decrypt the SAM |
| SECURITY | `%WINDIR%\System32\config\SECURITY` | LSA secrets, cached domain credentials (MSCASHv2) |

## Conceptual flow

1. Obtain copies of the hives — Volume Shadow Copy, offline boot, or registry backup (`reg save`, requires `SeBackupPrivilege`)
2. Extract the BootKey from the SYSTEM hive
3. Decrypt SAM structures (F-value, RID-encrypted hashes)
4. For cached credentials: extract NL$KM from SECURITY and decrypt MSCASHv2 (PBKDF2, slow to crack)

## Relevant protections

- Windows 11 22H2+ / Server 2025: progressive NTLMv1 deprecation and storage changes
- Virtualization-Based Security can protect LSA secrets

## Public references

- impacket `secretsdump.py` (complete offline parsing, open source)
- SAM format documentation: "The Windows SAM registry file format"
