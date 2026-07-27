# src/sam — Parsing offline de hives SAM/SYSTEM/SECURITY

📖 Notas de pesquisa: [docs/sam-offline.md](../../docs/sam-offline.md)

## Escopo do módulo

Parsing **offline** dos registry hives do lab. Este módulo não interage com o sistema vivo — opera sobre cópias dos hives obtidas via Volume Shadow Copy ou `reg save` no lab.

## Experimentos planejados

| # | Experimento | Artefato |
|---|---|---|
| S1 | Obtenção das cópias: `vssadmin` + cópia do shadow, e `reg save` (SeBackupPrivilege) | SAM, SYSTEM, SECURITY |
| S2 | Extração da BootKey do hive SYSTEM | SYSTEM |
| S3 | Parser da estrutura SAM (F-value, V-value, RID) — referência: impacket | SAM |
| S4 | Enumeração de LSA secrets e cached credentials (estrutura, sem crack) | SECURITY |

## Convenções

- Linguagem: Python 3 — impacket como referência de implementação, mas com código próprio documentado linha a linha para fins didáticos
- Hives copiados para `lab/hives/` ficam **fora do git** (`.gitignore`)
