# src/lsass — PoCs de acesso à memória do LSASS

📖 Notas de pesquisa: [docs/lsass-dumping.md](../../docs/lsass-dumping.md)

## Escopo do módulo

Implementações de laboratório comparando métodos de obtenção de um dump de memória do `lsass.exe`. O foco é a **obtenção do dump** — parsing das credenciais fica por conta de ferramentas open source (pypykatz, Mimikatz) apontadas no dump.

## Experimentos planejados

| # | Experimento | Pré-requisito | Estágio de hardening |
|---|---|---|---|
| L1 | `MiniDumpWriteDump` via dbghelp.dll | `SeDebugPrivilege` | 0–1 |
| L2 | `comsvcs.dll!MiniDump` via rundll32 (LOLBin) | `SeDebugPrivilege` | 0–1 |
| L3 | Abertura de handle via direct syscalls | `SeDebugPrivilege` | 0–1 (comparar telemetria) |
| L4 | Comportamento com RunAsPPL ativo | — | 1 (documentar falhas) |

## Convenções

- Linguagem: C (MSVC) — builds em `x64/Release` não são commitadas
- Cada PoC imprime verbosamente cada etapa (abertura de handle, leitura, escrita do dump)
- Dumps vão para `output/` (gitignored) e são **descartados após o experimento**
