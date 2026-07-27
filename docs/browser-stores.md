# T1555.003 — Browser Credential Stores

Research notes on the credential stores of major browsers.

## Chromium (Chrome, Edge, Brave, Opera)

- **Login Data** — SQLite at `%LOCALAPPDATA%\<Browser>\User Data\Default\`
- Passwords encrypted with AES-256-GCM; master key in `Local State` (`os_crypt.encrypted_key` field), wrapped via DPAPI
- **v20 / App-Bound Encryption (Chrome 127+)**: additional key protected by a system service that validates the executable path — requires elevation or injection into the browser process to reach the `IElevator` COM interface
- **Cookies** in `Network\Cookies`, same encryption scheme

## Firefox

- **`logins.json`** — credentials encrypted with 3DES/AES via NSS
- **`key4.db`** — SQLite holding the master key; without a master password, derivation uses a known fixed string
- The NSS library (`nss3.dll`) can be loaded to perform decryption in your own process

## Lab considerations

- File locks: SQLite WAL requires copying the file before reading (Volume Shadow Copy, or a plain copy when the browser is closed)
- App-Bound Encryption changed the landscape post-2024 — document behavior per Chrome version

## Public references

- Community-published App-Bound reversing documentation (2024)
- Chromium source: `components/os_crypt/`
