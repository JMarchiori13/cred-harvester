# src/browsers — PoCs de leitura de credential stores de navegadores

📖 Notas de pesquisa: [docs/browser-stores.md](../../docs/browser-stores.md)

## Escopo do módulo

Leitura e parsing dos stores de credenciais de navegadores no lab, com credenciais fictícias salvas pelo próprio pesquisador.

## Experimentos planejados

| # | Experimento | Alvo |
|---|---|---|
| B1 | Cópia segura do `Login Data` (SQLite, handling de lock/WAL) | Chromium |
| B2 | Extração da chave `os_crypt.encrypted_key` do `Local State` + unwrap DPAPI (pré-v20) | Chromium ≤126 |
| B3 | Parsing do `logins.json` + `key4.db` via NSS | Firefox |
| B4 | Estudo do App-Bound Encryption: comportamento, requisitos, limitações | Chrome 127+ |

## Convenções

- Linguagem: Python 3 (parsing) — PoCs leem apenas perfis de teste criados no lab
- Navegadores do lab nunca logados em contas reais
- Resultados vão para `output/` (gitignored)
