# T1555.004 — Windows DPAPI

Notas de pesquisa sobre a Data Protection API e seus artefatos.

## Arquitetura

- **Masterkey** (512 bits, rotacionada a cada ~90 dias) derivada da senha do usuário (contexto de usuário) ou da senha da máquina (contexto de sistema, via DPAPI_SYSTEM LSA secret)
- Armazenadas em `%APPDATA%\Microsoft\Protect\{SID}\` (usuário) e `%WINDIR%\System32\Microsoft\Protect\` (máquina)
- Blobs DPAPI contêm GUID da masterkey, salt, HMAC e dados cifrados (3DES/AES)

## Superfícies de ataque documentadas

| Cenário | Requisito |
|---|---|
| Usuário logado | `CryptUnprotectData` no contexto do próprio usuário |
| Offline, senha conhecida | Derivação da masterkey a partir do hash da senha |
| Offline, DPAPI_SYSTEM | Backup keys do domain controller (domínio) |

## Onde DPAPI aparece

- Cookies e senhas de navegadores Chromium (chave AES embrulhada em DPAPI)
- Credential Manager / Vault
- Chaves privadas de certificados, Wi-Fi profiles, RDP saved credentials

## Referências públicas

- SharpDPAPI (harmj0y), DonPAPI, pypykatz
- "DPAPI in depth" — posts da comunidade (SpecterOps, eladshamir)
