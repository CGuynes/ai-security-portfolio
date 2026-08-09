# Christopher Guynes — AI Systems & Offensive Security Portfolio

**Profile:** AI systems designer and offensive security practitioner specializing in multi-agent memory/process design, adversarial evaluation of automated workflows, and high-reliability technical leadership (U.S. Navy veteran).  

**How I work:** I architect systems, define evaluation criteria and quality gates, and direct advanced coding models to implement under my oversight. I do not claim classic decade-deep personal line-by-line authorship of every module. I claim design ownership, process discipline, and measurable research outcomes.

**Contact:** [LinkedIn](https://www.linkedin.com/in/guyneschristopher) · cguynes2023@gmail.com  

**Location:** Kings Bay, GA (remote-capable)  
**Clearance:** TS/SCI (granted May 2022; eligible for reactivation through May 2027)

---

## 30-second pitch

I design **agent-safe offensive workflows** and the **memory systems** that make them durable across sessions. Independently, I research CI/CD and agent-adjacent attack surface—including **Critical GitHub Actions `pull_request_target` supply-chain findings that resolved on HackerOne**. Strongest fit: **AI Agent Security / AI Red Team / Agent Security Research**, not generic senior product SWE.

---

## Highlights

| Signal | Detail |
|--------|--------|
| **Critical findings** | HackerOne **#3619287** and **#3619288** — Critical, **resolved** — RCE + secret/PAT exposure via `pull_request_target` CI workflows (supply-chain class) |
| **Agent memory** | Designed multi-store agent memory plane (SQL source of truth + LLM-facing AIDL mirror + journals + vectors) with ARMD-first lookup and write-back discipline |
| **Process law** | Encoded scope gates, PoC/callback requirements, and campaign-state memory so AI-assisted hunting stays authorized and non-regressive |
| **Threshold vault (designed)** | Designed passphrase-gated AES-256-GCM under Shamir **3-of-5** master key (no single superuser); SSS core implemented/tested; full production envelope is intentional completion path |
| **Ops background** | Navy Lead Technical Supervisor; Help Desk Manager / Security Officer; DoD STIG environments; GIAC GFACT, GSEC; GCIH in progress |

---

## 1. Critical offensive outcomes

### CI/CD supply-chain — `pull_request_target` (HackerOne, resolved Critical)

| Report | Severity | Status | Class |
|--------|----------|--------|-------|
| **#3619287** | Critical | Resolved | RCE + supply chain via privileged workflow on fork PRs |
| **#3619288** | Critical | Resolved | RCE + token/secret exposure via privileged workflow |

**Technical story (public-safe):**

1. Privileged GitHub Actions workflows (`pull_request_target`) ran in a context with base-repo secrets.  
2. Checkout/install/build of untrusted PR material allowed attacker-controlled code execution on the runner.  
3. Secrets and tokens in the job environment became exfiltratable.  
4. Standard mitigation: do not run untrusted code in privileged contexts; use fork guards such as `if: ${{ !github.event.pull_request.head.repo.fork }}` and safer trigger patterns.

**Why this maps to AI Agent Security roles:** tool-using agents with privileged tokens share the same failure mode as CI runners with secrets—identity, sandboxing, and policy enforcement under automation.

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

## 4. Related systems (supporting, not primary hire reasons)

| System | What it is | How to read it |
|--------|------------|----------------|
| **Gideon** | Directed multi-component lab/BBP platform with scope enforcement, tests, Docker lab fleet | Lab methodology + agent orchestration—not a multi-tenant SaaS claim |
| **CRISP / AITP** | AI traffic compression research prototype with measurement focus and patent packaging | Systems-thinking + measurement discipline—secondary differentiator |
| **Scope Covenant (PPA-004 framing)** | Multi-barrier scope enforcement concept for autonomous assessment agents | Agent governance / liability control |

---

## 5. Resume-ready bullets

- Designed a multi-store **agent memory plane** with mandatory memory-first lookup, write-back, and scope/PoC gates for AI-assisted offensive work.  
- Conducted independent research resulting in **Critical, resolved** HackerOne findings on GitHub Actions `pull_request_target` secret-exfiltration chains.  
- Designed a **threshold vault** (passphrase-gated AES-256-GCM under Shamir 3-of-5) so high-sensitivity secrets require multi-party unseal—no single superuser.  
- Built structured research CRM and methodology packs so humans and agents share campaign state, scope rules, and submission outcomes.  
- High-reliability technical leadership (U.S. Navy); GIAC GFACT/GSEC; GCIH in progress; TS/SCI-eligible.

---

## 6. Best-fit roles

1. **AI Security Engineer / AI Red Team Engineer**  
2. **Agent Security Researcher / Engineer**  
3. **Forward-deployed / Solutions** roles for agentic platforms (security flavor)  
4. **Security Engineer** (AI automation / hybrid SecOps) as accessible bridge  

See [`TARGET_COMPANIES.md`](./TARGET_COMPANIES.md) for organizations that historically pay for this mix.

---

## 7. Honest gaps (say this if asked)

- Implementation is **AI-directed**; not positioning as pure leetcode / classic senior product SWE.  
- Personal research/ops platforms—not multi-tenant products with external customer SLAs.  
- CRISP is a measured prototype, not the primary hire reason.  
- Covenant vault: **designed + SSS core**; full production envelope not claimed complete.

---

## 8. Documents in this repo

| File | Purpose |
|------|---------|
| [README.md](./README.md) | This portfolio (public) |
| [TARGET_COMPANIES.md](./TARGET_COMPANIES.md) | Companies/orgs that pay for this skillset |
| [HONESTY_PASS.md](./HONESTY_PASS.md) | Claim matrix—what to say / not say |
| [INTERVIEW.md](./INTERVIEW.md) | 15–20 min demo plan + pitch |

**Security note:** This repository is intentionally free of credentials, private IPs, hostnames, tokens, and internal paths. Offensive writeups stay at the public technical-class level; program-specific non-public details are omitted.
