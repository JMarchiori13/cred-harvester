---
name: New experiment / PoC
about: Propose a new lab experiment or PoC for an existing module
title: "[Experiment] <module> — <technique>"
labels: experiment
assignees: ""
---

## Objective

<!-- What does this experiment demonstrate? One or two sentences. -->

## Module

<!-- e.g. lsass / dpapi / browsers / sam — and the planned experiment ID (L5, D5, ...) -->

## Scope checklist

- [ ] Runs only inside the isolated lab (see `lab/setup.md`)
- [ ] Uses only fictitious, lab-generated credentials/artifacts
- [ ] Includes a documentation note in `docs/` (technique, prerequisites, expected behavior)
- [ ] No obfuscation, anti-analysis, or AV/EDR evasion
- [ ] No real third-party data of any kind (not even anonymized)
- [ ] Mapped to MITRE ATT&CK (technique + sub-technique)

## Lab requirements

<!-- Hardening stage, snapshots, tooling, privileges needed (e.g. SeDebugPrivilege) -->

## Acceptance criteria

- [ ] Experiment executes and produces the documented result in the lab
- [ ] Telemetry generated is recorded (Sysmon event IDs, alerts)
- [ ] Results documented in `docs/` (observed vs. expected)
- [ ] Artifacts (dumps, hives, binaries) are gitignored and discarded after the run
