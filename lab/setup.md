# Setup do Laboratório

Ambiente de referência para todos os experimentos deste repositório. **Nenhum experimento deve rodar fora deste isolamento.**

## Topologia

```
┌─────────────────────────────────────────┐
│  Hypervisor (VMware Workstation /       │
│  Hyper-V / VirtualBox)                  │
│                                         │
│  ┌───────────────┐   ┌───────────────┐  │
│  │  Win 11 VM    │   │  Win Server   │  │
│  │  (target)     │   │  2022 DC      │  │
│  │               │   │  (opcional)   │  │
│  └───────┬───────┘   └───────┬───────┘  │
│          └──── host-only ────┘          │
│              (sem NAT/bridge)           │
└─────────────────────────────────────────┘
```

## VM alvo (Windows 10/11)

| Item | Configuração |
|---|---|
| Rede | Host-only ou NIC desabilitada |
| Snapshots | `clean-base` (pós-install), `creds-seeded` (credenciais fictícias), um por nível de hardening |
| Usuários | `labuser1` (admin local), `labuser2` (standard) — senhas fictícias documentadas no vault do lab, nunca no repo |
| Dados de teste | Logins salvos em navegador apontando para sites de teste (ex.: httpbin local), credenciais RDP/samba fictícias |

## Matriz de hardening (experimentos em etapas)

| Estágio | Configuração | O que valida |
|---|---|---|
| 0 | Baseline, sem proteções | Funcionamento básico da técnica |
| 1 | RunAsPPL (`HKLM\SYSTEM\...\Lsa\RunAsPPL=1`) | Bloqueio de acesso ao LSASS por não-PPL |
| 2 | Credential Guard (VBS) | Isolamento de segredos no LSAIso |
| 3 | WDigest desabilitado + LSA Protection | Redução de material em texto claro |
| 4 | Chrome 127+ | App-Bound Encryption em browser stores |

## Ferramentas do lab

- **Sysmon** (config SwiftOnSecurity ou olafhartong) — telemetria para comparar ruído de cada técnica
- **Process Monitor / Process Explorer** — validação de handles e acessos
- **Wireshark** (host-only) — confirmar que nada sai da rede
- Editor de registro, `vssadmin`, `esentutl` — nativos

## Procedimento por experimento

1. Restaurar snapshot apropriado ao estágio de hardening
2. Executar a PoC, gravar resultado + telemetria gerada
3. Documentar em `docs/` (comportamento observado × esperado)
4. Restaurar snapshot — nunca reutilizar VM "sujada"
