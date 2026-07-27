# src/dpapi — PoCs de manipulação de blobs DPAPI

📖 Notas de pesquisa: [docs/dpapi.md](../../docs/dpapi.md)

## Escopo do módulo

Experimentos com a Data Protection API em contexto de laboratório: criar, inspecionar e descriptografar blobs DPAPI **criados pelo próprio lab**, e estudar a estrutura das masterkeys.

## Experimentos planejados

| # | Experimento | Contexto |
|---|---|---|
| D1 | Cifrar/decifrar blob com `CryptProtectData`/`CryptUnprotectData` no contexto do usuário logado | User |
| D2 | Parser da estrutura de blob DPAPI (GUID, salt, HMAC, dados) — sem descriptografia | Offline |
| D3 | Enumeração de masterkeys em `%APPDATA%\Microsoft\Protect\{SID}\` | User |
| D4 | Descriptografia offline de masterkey com senha conhecida do lab (referência: pypykatz) | Offline |

## Convenções

- Linguagem: C# (.NET 8) ou Python 3 (pypykatz como referência de parsing)
- Todos os segredos usados são gerados no lab e fictícios
