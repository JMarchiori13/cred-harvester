# cred-harvester

> **Aviso / Disclaimer**
> Este repositório é um projeto de **pesquisa em segurança ofensiva** para uso exclusivo em **laboratórios isolados** e **operações autorizadas** (red team engagements com escopo contratual). O uso de qualquer técnica aqui documentada contra sistemas sem autorização explícita é crime (Lei nº 12.737/2012 — Brasil; CFAA — EUA; legislação equivalente em outras jurisdições). O autor não se responsabiliza por uso indevido.

## Objetivo

Estudo estruturado das técnicas de **Credential Access** (MITRE ATT&CK TA0006) em ambientes Windows, com implementações de laboratório organizadas por fonte de credencial.

## Estrutura do projeto

```
cred-harvester/
├── docs/                    # Notas de pesquisa por técnica
│   ├── lsass-dumping.md     # T1003.001 — métodos de dump de LSASS
│   ├── dpapi.md             # T1555.004 — DPAPI masterkeys e blobs
│   ├── browser-stores.md    # T1555.003 — credential stores de navegadores
│   └── sam-offline.md       # T1003.002 — extração offline de SAM/SYSTEM
├── src/
│   ├── lsass/               # PoCs de acesso à memória do LSASS (lab)
│   ├── dpapi/               # PoCs de manipulação de blobs DPAPI (lab)
│   ├── browsers/            # PoCs de leitura de stores (Chrome/Edge/Firefox)
│   └── sam/                 # Parsing offline de hives SAM/SYSTEM
├── lab/                     # Setup do ambiente de testes (VMs, snapshots)
└── README.md
```

## Módulos planejados

| Módulo | ATT&CK | Descrição |
|---|---|---|
| `lsass` | T1003.001 | Comparação de métodos: `MiniDumpWriteDump`, `comsvcs.dll`, handles via syscalls |
| `dpapi` | T1555.004 | Estrutura de masterkeys, descriptografia com contexto de usuário/máquina |
| `browsers` | T1555.003 | Login Data (Chromium), `logins.json` (Firefox), v10/v20 encryption |
| `sam` | T1003.002 | Parsing offline de hives em volume montado / shadow copy |

## Requisitos do laboratório

- VM Windows 10/11 isolada (sem rede ou rede host-only)
- Snapshots limpos para rollback
- Credenciais fictícias geradas apenas para teste
- EDR/AV do lab documentado por experimento

## Referências

- MITRE ATT&CK — Credential Access (TA0006)
- Documentação pública: Mimikatz (Benjamin Delpy), pypykatz, SharpDPAPI, DonPAPI
- MSDN/MS Learn — DPAPI, LSASS protection (RunAsPPL), Credential Guard
