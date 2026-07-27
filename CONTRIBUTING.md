# Contributing

Contributions are welcome **within the project scope**: documented credential access research, lab PoCs, and fixes to the technical notes.

## Rules

1. **Lab material only.** No real credentials, no dumps from production systems, no third-party data — not even anonymized.
2. **Every PoC needs documentation.** Each implementation in `src/` must ship with a note in `docs/` explaining the technique, prerequisites, and expected behavior.
3. **No operation-ready offensive code.** PoCs must be educational: verbose logging, visible artifacts, no obfuscation or AV evasion.
4. **Do not commit sensitive artifacts.** The `.gitignore` already covers dumps, tickets, and keys — respect it.

## Process

1. Open an issue describing the technique/module
2. Fork → branch `feat/<module>-<technique>`
3. PR referencing the issue, including the lab experiment result

## Standards

- Notes in English (keep it consistent within each file)
- Techniques mapped to MITRE ATT&CK (technique + sub-technique)
- Tables for method comparisons
