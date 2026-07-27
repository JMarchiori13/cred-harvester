# T1003.001 — LSASS Memory Dumping

Notas de pesquisa sobre acesso à memória do `lsass.exe` para extração de material de autenticação.

## Por que o LSASS

O Local Security Authority Subsystem Service mantém em memória credenciais de sessões interativas: hashes NTLM, tíquetes Kerberos, e (em sistemas sem hardening) segredos em texto claro via WDigest.

## Métodos documentados

| Método | Observações |
|---|---|
| `MiniDumpWriteDump` (dbghelp/dbgcore) | Método clássico; requer `SeDebugPrivilege` e handle com `PROCESS_VM_READ` |
| `comsvcs.dll` via rundll32 | LOLBin — `MiniDump` export; sem tool externa |
| Task Manager / ProcDump | Ferramentas legítimas assinadas; dump manual |
| Direct syscalls | Evita hooks de EDR em `OpenProcess`/`ReadProcessMemory` em user-mode |
| Handle duplication / fork | Acesso indireto via handles existentes |

## Hardening que afeta a técnica

- **RunAsPPL** (LSA Protection) — bloqueia abertura de processo por processos não-PPL
- **Credential Guard** (VBS) — isola segredos no LSAIso
- **WDigest `UseLogonCredential=0`** — remove segredos em texto claro

## Lab checklist

- [ ] Baseline: VM sem RunAsPPL, credenciais fictícias logadas
- [ ] Repetir com RunAsPPL habilitado e documentar diferença de comportamento
- [ ] Comparar telemetria gerada (Sysmon Event ID 10 — ProcessAccess)
