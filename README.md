# Christopher Guynes — Offensive Security Engineer & Bug-Bounty Researcher

**Headline:** Offensive Security Engineer | Penetration Tester & Bug Bounty Researcher

**Profile:** Offensive Security Engineer and bug-bounty researcher specializing in AI-agent security: multi-agent memory and process design, adversarial evaluation of automated workflows, and high-reliability technical leadership (U.S. Navy veteran).

**How I work:** I architect systems, define evaluation criteria and quality gates, and direct advanced coding models to implement under my oversight. I do not claim classic decade-deep personal line-by-line authorship of every module. I claim design ownership, process discipline, and measurable research outcomes.

**Contact:** [LinkedIn](https://www.linkedin.com/in/guyneschristopher) · cguynes2023@gmail.com

**Location:** Kingsland, GA  
**Work arrangement:** **U.S. remote only — not open to relocation** (fully remote-capable; no uprooting for San Francisco / Seattle / NYC onsite-only seats)  
**Clearance:** TS/SCI (inactive, not expired; eligible for reactivation). Granted May 2022.  
**Education:** Pursuing a B.S. in Cybersecurity at SANS Technology Institute (expected 2028). GIAC GSEC, GFACT. SANS SEC504 complete; GCIH exam in progress.

---

## 30-second pitch

I independently research vulnerabilities and design **agent-safe offensive workflows** plus the **memory systems** that make them durable across sessions. That work includes **Critical GitHub Actions `pull_request_target` supply-chain findings that resolved on HackerOne**, and authorized research across 25+ programs on HackerOne, Intigriti, Bugcrowd, and YesWeHack. Strongest fit: **Offensive Security Engineer / Penetration Tester / AI Agent Security**, not generic senior product SWE. Seeking **U.S. remote** roles only.

---

## Highlights

| Signal | Detail |
|--------|--------|
| **Critical findings** | HackerOne **#3619287** and **#3619288** — Critical, **resolved** — RCE + secret/PAT exposure via `pull_request_target` CI workflows (supply-chain class) |
| **Bug bounty breadth** | 25+ programs on HackerOne, Intigriti, Bugcrowd, and YesWeHack. Finding classes include high-severity SSRF via DNS rebinding, authentication bypass, S3 bucket enumeration, and hardcoded credentials in a decompiled Android APK. Chained P1+P2 PoC against OpenAI's MCP program on Bugcrowd. |
| **Agent memory** | Designed multi-store agent memory plane (SQL source of truth + LLM-facing AIDL mirror + journals + vectors) with ARMD-first lookup and write-back discipline |
| **Process law** | Encoded scope gates, PoC/callback requirements, and campaign-state memory so AI-assisted hunting stays authorized and non-regressive |
| **Threshold vault (designed)** | Designed passphrase-gated AES-256-GCM under Shamir **3-of-5** master key (no single superuser); SSS core implemented/tested; full production envelope is intentional completion path |
| **Experience** | Help Desk Manager / Security Officer, SimpleTech LLC (Sep 2025 – Nov 2026); Systems Analyst, Astraeus / Chenega (DoD STIG, 8 servers on Unclassified and Secret networks); U.S. Navy Lead Missile Technician |
| **Education & certs** | B.S. Cybersecurity in progress, SANS Technology Institute (expected 2028); GIAC GSEC, GFACT; SEC504 complete, GCIH exam in progress |

---

## 1. Critical offensive outcomes

### CI/CD supply-chain — `pull_request_target` (HackerOne, resolved Critical)

| Report | Severity | Status | Class |
|--------|----------|--------|-------|
| **#3619287** | Critical | Resolved | RCE + supply chain via privileged workflow on fork PRs |
| **#3619288** | Critical | Resolved | RCE + token/secret exposure via privileged workflow |

**Technical story:**

1. Privileged GitHub Actions workflows (`pull_request_target`) ran in a context with base-repo secrets.  
2. Checkout/install/build of untrusted PR material allowed attacker-controlled code execution on the runner.  
3. Secrets and tokens in the job environment became exfiltratable.  
4. Standard mitigation: do not run untrusted code in privileged contexts; use fork guards such as `if: ${{ !github.event.pull_request.head.repo.fork }}` and safer trigger patterns.

**Why this maps to AI Agent Security roles:** tool-using agents with privileged tokens share the same failure mode as CI runners with secrets—identity, sandboxing, and policy enforcement under automation.

### Broader authorized research

Research across 25+ programs on HackerOne, Intigriti, Bugcrowd, and YesWeHack. Submitted findings include high-severity SSRF via DNS rebinding and hostname-filter bypass, missing authentication on production APIs, S3 bucket enumeration via a misconfigured reverse proxy, and hardcoded production credentials in a decompiled Android APK. Built and verified a chained P1+P2 proof-of-concept against OpenAI's MCP program on Bugcrowd (credential exfiltration, session-log tampering, and a telemetry audit gap), including a working patch and full reproduction.

Supporting pipeline (secondary): multi-platform research CRM, DoD VDP engagement practice, lab automation with scope enforcement (lab-only validation).

---

## 2. ARMD — Agent memory architecture (designed & operated)

### Problem

Long agent sessions compact, lose infrastructure facts, re-ask for secrets, and regress on campaign state. Markdown “second brains” do not enforce scope, PoC, or write-back.

### Design

```
Agent session
    │ ARMD-first
    ├── SQL source of truth (structured ops + research state)
    ├── AIDB (AIDL + full-text, LLM-facing mirror)
    ├── Agent journals (per-agent event logs)
    └── Semantic store (vector fallback)
         │
         ├── Process law + campaign state + artifact registry + submissions CRM
         └── Secrets boundary → encrypted vault refs (no plaintext secrets in memory store)
```

### Operating doctrine

| Rule | Intent |
|------|--------|
| Memory before guess | Query structured memory before inventing infra facts |
| Write-back | Register new artifacts; no orphans |
| Scope gate | Check program scope before external action/submission |
| PoC requirement | Callback or observable effect before reporting |
| Callback-first | Proof channel before narrative writeup |
| Vault boundary | Secrets never stored as plaintext memory values |
| Cost-aware models | Cheap models by default; expensive only when justified |

### Authorship frame

> I architected the memory model, namespaces, process rules, and evaluation criteria. Implementation was AI-directed under my oversight. I own the design decisions and operational outcomes.

---

## 3. Covenant threshold vault (designed)

**Honest status:** designed architecture + Shamir SSS core implemented/tested; full AES-GCM envelope and distributed-share deployment are the intended completion path—not claimed as production-hardened LE deployment.

| Layer | Design |
|-------|--------|
| Human gate | Single authorized open path: passphrase/challenge ceremony |
| Symmetric seal | AES-256-GCM on sensitive material |
| Key derivation | Passphrase → KDF → key material |
| Threshold | Master key split Shamir **k-of-n** (default **3-of-5**) |
| Governance | No single superuser; Tier-3 short-lived vault sessions; audit intent |

**One-liner:** Designed a threshold vault so high-sensitivity material requires multi-party unseal—not one master password god-mode.

---

## 4. In development

The projects below are in development. None is a public product launch, and none claims customers or revenue.

### HackSim — Gamified Cybersecurity Curriculum Platform (in development)

Designed and built HackSim, a desktop cybersecurity training game (Electron, React, TypeScript) with a 19-node skill tree, an 8-axis competency web, and mission-based labs that run real tools inside isolated Docker Compose environments. Implemented seven mission definitions (recon, SQL injection, SSH password attacks, directory discovery, SSRF, EternalBlue, and credential dumping) plus an optional Express instructor API with authentication, progress tracking, cohort management, and LTI hooks for classroom use. Local MIT-licensed codebase; not published as a public product.

### Cortex — Independent Bug-Bounty Research Platform (in development)

Built and operate a Python research platform for authorized bug-bounty work: campaign state, program scope, and submission tracking, plus a SQLite knowledge store that maps MITRE ATT&CK techniques, OWASP entries, and tracked CVEs. Added a local FastAPI RAG service over that knowledge base and a separate bug-bounty intel index, using local embeddings (Ollama). The memory and process design (SQL source of truth, an LLM-facing mirror, journals, and write-back / scope / PoC gates) is summarized in this portfolio. Independent research on this platform includes the Critical, resolved HackerOne findings above.

### Gideon Kanban — Self-Hosted Security-Operations Board (in development)

Designed and deployed a FastAPI + SQLite kanban PWA for a multi-agent security workflow, running in Docker on a Raspberry Pi 5. The board imports an existing card database (documented 309-card snapshot), enforces role-scoped API tokens, and signs review webhooks. A companion reviewer service runs deterministic scope and evidence checks and a local-LLM advisory review; it cannot file reports or grant human approvals.

### Gideon Edge Node — On-Prem MSSP Architecture (in development)

Designed a managed-security edge-node architecture for small-site deployment: a containerized agent on a Raspberry Pi 5-class device with outbound-only remote access, local monitoring (logs, ARP/rogue-device detection, honeypot), and store-and-forward when the link drops. Documented a three-tier service model (Watchtower / Sentinel / Fortress) and a technician-console demo. This is a product design and prototype, not a claim of paying customers.

**CRISP / AITP** — AI traffic compression research prototype (in development).

---

## 5. Resume-ready bullets

- Designed a multi-store **agent memory plane** with mandatory memory-first lookup, write-back, and scope/PoC gates for AI-assisted offensive work.  
- Conducted independent research resulting in **Critical, resolved** HackerOne findings on GitHub Actions `pull_request_target` secret-exfiltration chains, plus authorized research across 25+ programs (SSRF via DNS rebinding, authentication bypass, S3 enumeration, hardcoded credentials in an APK, and a chained P1+P2 PoC on OpenAI's MCP program).  
- Designed a **threshold vault** (passphrase-gated AES-256-GCM under Shamir 3-of-5) so high-sensitivity secrets require multi-party unseal—no single superuser.  
- Built structured research CRM and methodology packs so humans and agents share campaign state, scope rules, and submission outcomes.  
- Led incident response and security operations as Help Desk Manager / Security Officer at SimpleTech LLC (Sep 2025 – Nov 2026); hardened DoD STIG baselines as a Systems Analyst at Astraeus / Chenega across 8 servers on Unclassified and Secret networks.  
- High-reliability technical leadership as a U.S. Navy Lead Missile Technician; GIAC GFACT/GSEC; SANS SEC504 complete, GCIH exam in progress; pursuing B.S. Cybersecurity at SANS Technology Institute (expected 2028); TS/SCI (inactive, not expired; eligible for reactivation). Granted May 2022.

---

## 6. Best-fit roles

1. **Offensive Security Engineer / Penetration Tester**
2. **AI Security Engineer / AI Red Team Engineer**
3. **Agent Security Researcher / Engineer**
4. **Security Engineer** (AI automation / hybrid SecOps) as accessible bridge

**Constraint:** U.S. remote (or remote-first). Not relocating. Skip hard onsite-only San Francisco / Seattle / London seats unless a real remote track exists.

---

## 7. Documents in this repo

| File | Purpose |
|------|---------|
| [README.md](./README.md) | This portfolio (public) |

**Security note:** This repository is intentionally free of credentials, private IPs, hostnames, tokens, and internal paths. Offensive writeups stay at the public technical-class level; program-specific non-public details are omitted.
