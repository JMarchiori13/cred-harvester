# T1555.004 — Windows DPAPI

Research notes on the Data Protection API and its artifacts.

## Architecture

- **Masterkey** (512 bits, rotated every ~90 days) derived from the user's password (user context) or the machine password (system context, via the DPAPI_SYSTEM LSA secret)
- Stored in `%APPDATA%\Microsoft\Protect\{SID}\` (user) and `%WINDIR%\System32\Microsoft\Protect\` (machine)
- DPAPI blobs contain the masterkey GUID, salt, HMAC, and encrypted data (3DES/AES)

## Documented attack surfaces

| Scenario | Requirement |
|---|---|
| Logged-in user | `CryptUnprotectData` in the user's own context |
| Offline, known password | Masterkey derivation from the password hash |
| Offline, DPAPI_SYSTEM | Domain controller backup keys (domain) |

## Where DPAPI shows up

- Chromium browser cookies and passwords (AES key wrapped in DPAPI)
- Credential Manager / Vault
- Certificate private keys, Wi-Fi profiles, saved RDP credentials

## Public references

- SharpDPAPI (harmj0y), DonPAPI, pypykatz
- "DPAPI in depth" — community posts (SpecterOps, eladshamir)
