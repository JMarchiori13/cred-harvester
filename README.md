# cred-harvester

![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-TA0006-red)
![Platform](https://img.shields.io/badge/platform-Windows-blue)
![Status](https://img.shields.io/badge/status-research%20scaffold-yellow)
![License](https://img.shields.io/badge/license-MIT-green)

> **⚠️ Disclaimer**
> Este repositório é um projeto de **pesquisa em segurança ofensiva** para uso exclusivo em **laboratórios isolados** e **operações autorizadas** (red team engagements com escopo contratual e Rules of Engagement assinados). O uso de qualquer técnica aqui documentada contra sistemas sem autorização explícita é crime (Lei nº 12.737/2012 — Brasil; CFAA — EUA; legislação equivalente em outras jurisdições). O autor não se responsabiliza por uso indevido.

## Objetivo

Estudo estruturado das técnicas de **Credential Access** ([MITRE ATT&CK TA0006](https://attack.mitre.org/tactics/TA0006/)) em ambientes Windows, com notas de pesquisa, PoCs de laboratório e experimentos documentados por módulo.

## Índice

- [Estrutura do projeto](#estrutura-do-projeto)
- [Módulos](#módulos)
- [Laboratório](#laboratório)
- [Roadmap](#roadmap)
- [Referências](#referências)

## Estrutura do projeto

```
cred-harvester/
├── docs/                    # Notas de pesquisa por técnica
│   ├── lsass-dumping.md     # T1003.001 — métodos de dump de LSASS
│   ├── dpapi.md             # T1555.004 — DPAPI masterkeys e blobs
│   ├── browser-stores.md    # T1555.003 — credential stores de navegadores
│   └── sam-offline.md       # T1003.002 — extração offline de SAM/SYSTEM
├── src/                     # PoCs de laboratório (ver README de cada módulo)
│   ├── lsass/
│   ├── dpapi/
│   ├── browsers/
│   └── sam/
├── lab/                     # Setup e hardening do ambiente de testes
│   └── setup.md
├── CONTRIBUTING.md
└── LICENSE
```

## Módulos

| Módulo | ATT&CK | Descrição | Status |
|---|---|---|---|
| [`lsass`](src/lsass/) | T1003.001 | Comparação de métodos: `MiniDumpWriteDump`, `comsvcs.dll`, handles via syscalls | 📋 planejado |
| [`dpapi`](src/dpapi/) | T1555.004 | Estrutura de masterkeys, descriptografia em contexto de usuário/máquina | 📋 planejado |
| [`browsers`](src/browsers/) | T1555.003 | Login Data (Chromium, incl. App-Bound/v20), `logins.json` (Firefox) | 📋 planejado |
| [`sam`](src/sam/) | T1003.002 | Parsing offline de hives SAM/SYSTEM/SECURITY | 📋 planejado |

## Laboratório

Todos os experimentos rodam em ambiente isolado. Veja **[lab/setup.md](lab/setup.md)** para o guia completo:

- VM Windows 10/11 em rede host-only (ou sem NIC)
- Snapshots limpos para rollback entre experimentos
- Credenciais **fictícias** geradas apenas para teste
- Matriz de hardening (RunAsPPL, Credential Guard, App-Bound) aplicada em etapas

## Roadmap

- [x] Scaffold do repositório + disclaimers
- [x] Notas de pesquisa dos 4 módulos
- [x] Guia de setup do laboratório
- [ ] PoC: dump de LSASS via `MiniDumpWriteDump` (lab)
- [ ] PoC: parsing offline de SAM/SYSTEM
- [ ] PoC: leitura de Login Data Chromium (pré-v20)
- [ ] Estudo: App-Bound Encryption (Chrome 127+)
- [ ] Matriz de resultados: técnica × hardening × telemetria

## Referências

- [MITRE ATT&CK — Credential Access (TA0006)](https://attack.mitre.org/tactics/TA0006/)
- [impacket](https://github.com/fortra/impacket) — `secretsdump.py` (parsing offline)
- [pypykatz](https://github.com/skelsec/pypykatz) — implementação Python do Mimikatz
- [SharpDPAPI](https://github.com/GhostPack/SharpDPAPI) / [DonPAPI](https://github.com/login-securite/DonPAPI)
- [Mimikatz](https://github.com/gentilkiwi/mimikatz) — Benjamin Delpy
- MS Learn — [DPAPI](https://learn.microsoft.com/en-us/dotnet/standard/security/how-to-use-data-protection), LSA Protection, Credential Guard

## License

MIT — veja [LICENSE](LICENSE). O disclaimer acima permanece válido independentemente da licença.
