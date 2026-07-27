# T1555.003 — Browser Credential Stores

Notas de pesquisa sobre os credential stores dos principais navegadores.

## Chromium (Chrome, Edge, Brave, Opera)

- **Login Data** — SQLite em `%LOCALAPPDATA%\<Browser>\User Data\Default\`
- Senhas cifradas com AES-256-GCM; chave mestra em `Local State` (campo `os_crypt.encrypted_key`), embrulhada via DPAPI
- **v20 / App-Bound Encryption (Chrome 127+)**: chave adicional protegida por serviço do sistema com validação de caminho do executável — requer elevação ou injeção no processo do navegador para `IElevator` COM
- **Cookies** em `Network\Cookies`, mesmo esquema de cifra

## Firefox

- **`logins.json`** — credenciais cifradas com 3DES/AES via NSS
- **`key4.db`** — SQLite com a chave mestra; sem master password, a derivação usa string fixa conhecida
- Biblioteca NSS (`nss3.dll`) pode ser carregada para descriptografia em processo próprio

## Considerações de laboratório

- Locks de arquivo: SQLite WAL requer cópia do arquivo antes da leitura (Volume Shadow Copy ou cópia simples quando o navegador está fechado)
- App-Bound Encryption mudou o cenário pós-2024 — documentar comportamento por versão do Chrome

## Referências públicas

- Documentação de reversing do App-Bound publicada pela comunidade (2024)
- Chromium source: `components/os_crypt/`
