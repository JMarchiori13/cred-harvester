# src/browsers — Browser credential store reading PoCs

📖 Research notes: [docs/browser-stores.md](../../docs/browser-stores.md)

## Module scope

Reading and parsing browser credential stores in the lab, using fictitious credentials saved by the researcher.

## Planned experiments

| # | Experiment | Target |
|---|---|---|
| B1 | Safe copy of `Login Data` (SQLite, lock/WAL handling) | Chromium |
| B2 | Extraction of `os_crypt.encrypted_key` from `Local State` + DPAPI unwrap (pre-v20) | Chromium ≤126 |
| B3 | Parsing of `logins.json` + `key4.db` via NSS | Firefox |
| B4 | App-Bound Encryption study: behavior, requirements, limitations | Chrome 127+ |

## Conventions

- Language: Python 3 (parsing) — PoCs read only test profiles created in the lab
- Lab browsers are never signed into real accounts
- Results go to `output/` (gitignored)
