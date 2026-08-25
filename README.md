## Ryan Haig

Network, systems, and cloud engineer working at customer-engagement cadence at a New York / New Jersey MSP. Builder-side focus on production agentic-AI systems — multi-vendor security audit, evidence-grounded AI narrative generation, and closed-loop verification at MSP scale.

I build the thing, ship it to real clients, then instrument it until I can prove it is correct. The instrumenting is the part I would bring to your team.

### Disciplines

**Cloud** — Microsoft Azure infrastructure · Microsoft 365 multi-tenant administration · Microsoft Entra ID identity and access management · Microsoft Purview · Microsoft Intune · Microsoft Graph API automation · AWS · Google Cloud Platform.

**Systems** — Windows Server hybrid administration (2012 R2 → 2025) · Active Directory multi-domain forensics · Group Policy · Hyper-V and Failover Clustering · Microsoft Exchange Hybrid Messaging.

**Network** — WatchGuard / Cisco Catalyst / HPE Aruba CX · Auvik network operations · multi-vendor firewall security · Linux network services.

**Security operations** — Microsoft Defender XDR · Microsoft Sentinel SIEM · Microsoft Purview eDiscovery · live-call incident response · BEC and mailbox forensics across 500+ tenants.

### Production projects

- **NinjaToolKit — agentic configuration-audit platform** (private company IP · **v7.6.13** · 53 GitHub Releases across 55 tags) — multi-vendor firewall configuration audit (WatchGuard · Palo Alto PAN-OS · Fortinet FortiOS · Cisco ASA) driven by a **12,139-line audit engine running 52 checks**, a **47-section Windows Server collector**, a **5-layer chained-Claude narrative pipeline**, and a canonical findings schema that structurally enforces evidence-first emission across both pillars. **~157,000 lines of production application code**, plus 19,000 lines of standing verification harnesses and **112,000 lines of tests**. 50 compliance controls mapped across PCI DSS v4.0 · CIS v8 · NIST CSF 2.0 · CMMC 2.0, with a canonical envelope carrying ten frameworks. Deployed across 46 client environments / 192 servers.
- **MX Toolbox Enterprise** ([repo](https://github.com/RyanH-sudo/mxtoolbox-enterprise)) — self-hosted FastAPI + React DNS / mail-deliverability suite. SPF/DKIM/DMARC validation, phishing classification, threat intelligence scoring. Docker + Azure deployable.
- **MSP pricing automation** (private) — Python Flask service-catalog + pricing engine.

### How I work

The part of the record I would actually put in front of an engineering panel is not the line count. It is the **forensic campaign** I ran against my own platform in August 2026: a complete code crawl of both pillars, ~1,300 findings triaged, ~86 fixes landed, and a prediction discipline where **every fix's expected numbers were written down before the edit**.

**66 of those predictions held. 32 were refuted.** Several refutations caught a defect *in the repair* before it shipped. In one cycle, **four recorded prescriptions would each have introduced a new defect** if applied literally — measuring first changed the fix, not the estimate. That produced the working rule the platform now runs on: **locations are reliable; prescriptions are hypotheses.**

Representative finds, all measured rather than inferred:

- **A delivered client report asserted "No internet-facing RDP exposures detected"** while ten enabled policies published RDP to named internal hosts via static NAT on non-standard ports. The check followed the policy port; the only path that followed the NAT translation was dead.
- **Finding IDs were list position** — 25 of 26 changed meaning between two runs. Made content-derived, which made the entire back-catalogue comparable and made audit-over-audit diffing possible.
- **A cross-client data-bleed defect** where two concurrent uploads under a 4-thread WSGI server could save one client's configuration under another client's name. Four obvious fixes were each ruled out by measurement before the one that worked — a per-request context registry that left all 97 call sites untouched.
- **A coverage instrument** built to answer a question nobody could: *what does the capture hold that the dashboards never show?* Measured answer: site 78.0%, firewall 51.7%.

Two standing harnesses now prove those fixes are still closed rather than asserting it — re-run 2026-08-24: **96/96 and 68/68, exit 0.** Their design note is the honest one: *tests prove structure; this proves the specific defects are still closed, because green tests have repeatedly coexisted with wrong output.*

### Forward scope

Currently architecting **NTK-ONE**, a modular rebuild driven by a hard constraint: every module must be small enough to load, reason about and refactor in a single context window without mapping the whole codebase. The measured motivation — one renderer in the current platform is 25,966 lines, which is roughly a third of a 1M-token window just to read once.

In design: a **third audit pillar for Microsoft 365 / Entra ID tenants**, built to the same shape as the server pillar — because a pillar here is an ingest module plus aggregators plus report chapters against one canonical envelope, so it inherits stable finding identity, diffing, the AI pipeline and the evidence-first rendering discipline rather than reimplementing them. Alongside it: a **vendor-neutral firewall configuration model** (read → normalise → edit → diff in vendor-native syntax → push → re-read → verify), an **engineer console** over in-box SSH and PowerShell Remoting, **change-driven agentic monitoring** that reasons only on what a deterministic policy gate escalates, and **exposure-window tracking** (first-seen · days-open · audits-carried) — a metric a point-in-time scanner structurally cannot produce.

### Engineering case study

Full architecture write-up: [ninjatoolkit-case-study](https://github.com/RyanH-sudo/ninjatoolkit-case-study).

### Open to

Solutions Engineer · Applied AI Engineer · Cloud Engineer (Azure / M365) · Senior Network Engineer · Senior Systems Engineer · Platform Engineer · Solutions Architect · Forward Deployed Engineer. Remote or 1099 contracting through Mercor / direct.

### Background

US Citizen · currently in Chiang Mai, Thailand · available US business hours. Started building PCs in the early '90s. Three years in India, nearly a decade in Northern California building permaculture farms, Asia teaching, Europe travel. Returned to engineering full-time in 2022.

### Contact

[rytuality@gmail.com](mailto:rytuality@gmail.com) · +1 347 279 6198 · [linkedin.com/in/rytuality](https://linkedin.com/in/rytuality)

---

*Every figure above was measured against the source tree on 2026-08-25, not carried forward from a previous revision.*
