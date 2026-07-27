# Lab Setup

Reference environment for every experiment in this repository. **No experiment should run outside this isolation.**

## Topology

```
┌─────────────────────────────────────────┐
│  Hypervisor (VMware Workstation /       │
│  Hyper-V / VirtualBox)                  │
│                                         │
│  ┌───────────────┐   ┌───────────────┐  │
│  │  Win 11 VM    │   │  Win Server   │  │
│  │  (target)     │   │  2022 DC      │  │
│  │               │   │  (optional)   │  │
│  └───────┬───────┘   └───────┬───────┘  │
│          └──── host-only ────┘          │
│              (no NAT/bridge)            │
└─────────────────────────────────────────┘
```

## Target VM (Windows 10/11)

| Item | Configuration |
|---|---|
| Network | Host-only or NIC disabled |
| Snapshots | `clean-base` (post-install), `creds-seeded` (fictitious credentials), one per hardening stage |
| Users | `labuser1` (local admin), `labuser2` (standard) — fictitious passwords documented in the lab vault, never in the repo |
| Test data | Saved browser logins pointing to test sites (e.g., local httpbin), fictitious RDP/SMB credentials |

## Hardening matrix (staged experiments)

| Stage | Configuration | What it validates |
|---|---|---|
| 0 | Baseline, no protections | Basic technique functionality |
| 1 | RunAsPPL (`HKLM\SYSTEM\...\Lsa\RunAsPPL=1`) | Blocking of LSASS access by non-PPL processes |
| 2 | Credential Guard (VBS) | Secret isolation in LSAIso |
| 3 | WDigest disabled + LSA Protection | Reduction of cleartext material |
| 4 | Chrome 127+ | App-Bound Encryption in browser stores |

## Lab tooling

- **Sysmon** (SwiftOnSecurity or olafhartong config) — telemetry to compare the noise of each technique
- **Process Monitor / Process Explorer** — handle and access validation
- **Wireshark** (host-only) — confirm nothing leaves the network
- Registry editor, `vssadmin`, `esentutl` — built-in

## Per-experiment procedure

1. Restore the snapshot matching the hardening stage
2. Run the PoC, record the result + generated telemetry
3. Document in `docs/` (observed vs. expected behavior)
4. Restore the snapshot — never reuse a "dirty" VM
