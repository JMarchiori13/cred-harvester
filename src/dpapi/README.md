# src/dpapi — DPAPI blob manipulation PoCs

📖 Research notes: [docs/dpapi.md](../../docs/dpapi.md)

## Module scope

Lab experiments with the Data Protection API: creating, inspecting, and decrypting DPAPI blobs **created by the lab itself**, and studying the masterkey structure.

## Planned experiments

| # | Experiment | Context |
|---|---|---|
| D1 | Encrypt/decrypt a blob with `CryptProtectData`/`CryptUnprotectData` in the logged-in user's context | User |
| D2 | DPAPI blob structure parser (GUID, salt, HMAC, data) — no decryption | Offline |
| D3 | Masterkey enumeration in `%APPDATA%\Microsoft\Protect\{SID}\` | User |
| D4 | Offline masterkey decryption with a known lab password (reference: pypykatz) | Offline |

## Conventions

- Language: C# (.NET 8) or Python 3 (pypykatz as parsing reference)
- All secrets used are lab-generated and fictitious
