# T1003.002 — SAM / SECURITY Hives Offline

Notas de pesquisa sobre extração offline de credenciais locais.

## Artefatos

| Hive | Caminho | Conteúdo |
|---|---|---|
| SAM | `%WINDIR%\System32\config\SAM` | Hashes NTLM de contas locais |
| SYSTEM | `%WINDIR%\System32\config\SYSTEM` | BootKey/SysKey — necessária para decifrar o SAM |
| SECURITY | `%WINDIR%\System32\config\SECURITY` | LSA secrets, cached domain credentials (MSCASHv2) |

## Fluxo conceitual

1. Obter cópia dos hives — Volume Shadow Copy, boot offline, ou backup de registro (`reg save`, requer `SeBackupPrivilege`)
2. Extrair BootKey do hive SYSTEM
3. Decifrar estruturas do SAM (F-value, RID-encrypted hashes)
4. Para cached credentials: extrair NL$KM do SECURITY e decifrar MSCASHv2 (PBKDF2, lento de quebrar)

## Proteções relevantes

- Windows 11 22H2+ / Server 2025: desabilitação progressiva de NTLMv1 e mudanças no armazenamento
- Virtualization-Based Security pode proteger LSA secrets

## Referências públicas

- impacket `secretsdump.py` (parsing offline completo, open source)
- Documentação do formato SAM: "The Windows SAM registry file format"
