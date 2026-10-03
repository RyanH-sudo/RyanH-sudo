## Ryan Haig

**Forward Deployed Engineer, eMazzanti Technologies.** I take frontier AI models into real operating environments
and make them do reliable engineering work there: diagnosing servers, auditing firewalls, and walking each problem to
a verified fix, with a human in control of everything that touches production. My background is the infrastructure
itself: network engineering, Windows Server administration and architecture, and security operations at a managed
service provider.

**Recognition.** Winner, WatchGuard's 2026 AI Innovation Challenge. My submission, entered under my employer, was
one of five winners selected worldwide from hundreds of submissions across 19 countries, recognized at WatchGuard
IMPACT North America in Nashville, October 2026.

---

### Selected work

**NinjaToolKit: an agentic audit and remediation platform** (private company software; technical case study:
[read online](https://ryanh-sudo.github.io/ninjatoolkit-case-study/), [repository](https://github.com/RyanH-sudo/ninjatoolkit-case-study))

An engineer-facing platform for managed Windows Server estates and WatchGuard firewalls, shipped as one
self-contained executable and used by an MSP's engineering team across 189 servers, 48 client organizations and 37
firewalls. Evaluated in October 2026 on servers it had never seen, against answer keys written before each run, it
found 40 of 47 open problems in full and 4 in part, and made none of the claims the keys ruled out. A first diagnosis
costs about $4.50 a server and takes about 20 minutes.

- An adversarial multi-agent diagnosis: a first engineer reads the server's whole raw capture, a second tries to
  break that read, and a lead engineer rules on every claim and orders the work, with what each piece waits on and
  the machine its next data comes from.
- Every answer the code acts on is a strict tool or JSON schema; deciding quotes are verified against the server's
  own output in code; a reply that starts looping is stopped and read up to where the repeating began.
- A console that converses on the whole Job, with six tools and every call priced before it is sent: it writes
  reviewed fixes and read-only tests, reads the client's other servers, and writes the Job's time entry.
- A structural safety model: no transport to client machines, read-only tests under per-machine run tokens with a hash
  chain of custody, and fixes with a backup, a literal revert and a verification, held by a reviewer agent if the
  undo would not work and refused by the builder if anything above the apply switch would run.
- 56 deterministic server judges with their precision measured on the estate, a role checklist for seven server
  roles, a 52-check firewall engine mapped to 50 controls in PCI DSS, CIS, NIST CSF and CMMC, and a 47-section
  PowerShell collector.
- 210,000 lines of product code and 13,409 passing tests; every build walked from an empty folder, all 457 pages
  crawled, and every agent failure mode proven to end in a stated state; 57 version tags between March and October
  2026.

**MX Toolbox Enterprise** ([repository](https://github.com/RyanH-sudo/mxtoolbox-enterprise))

A self-hosted DNS and mail-deliverability suite (FastAPI, React, PostgreSQL, Redis, Celery): SPF, DKIM and DMARC
validation, blacklist monitoring, phishing classification and threat-intelligence scoring, deployable with Docker.

**Learning suites** ([FDETutor](https://github.com/RyanH-sudo/FDETutor), [NetTutor](https://github.com/RyanH-sudo/NetTutor),
[PyTutor](https://github.com/RyanH-sudo/PyTutor))

Self-paced learning applications for forward deployed engineering, network engineering and Python.

---

### Disciplines

| | |
|---|---|
| **Applied AI engineering** | Multi-agent orchestration, tool use, context engineering, evaluation and verification of model output, refusal-aware model routing, cost governance, the Claude API |
| **Network engineering** | WatchGuard, Cisco Catalyst, HPE Aruba CX, multi-vendor firewall security, Auvik network operations, Linux network services |
| **Server architecture and administration** | Windows Server 2012 R2 to 2025, Active Directory, Group Policy, Hyper-V and failover clustering, Exchange hybrid |
| **Cloud** | Microsoft Azure, Microsoft 365 multi-tenant administration, Entra ID, Intune, Purview, the Graph API, AWS, Google Cloud |
| **Security operations** | Microsoft Defender XDR, Microsoft Sentinel, Purview eDiscovery, incident response, business email compromise and mailbox forensics across 500+ tenants |
| **Software and DevOps** | Python, PowerShell, SQL, Flask, JavaScript, Git, single-file Windows builds, release gating and verification harnesses |

---

### How I work

- **Measure, never recall.** Every number I report is the output of a command run at the time.
- **Hold AI output to evidence in code.** A model proposes; code verifies; a person approves anything irreversible.
- **Test the artifact, not only the suite.** I walk the built product end to end, then run it on real data it has
  never seen, before I call it done, because passing tests have coexisted with wrong output.
- **Score AI against answers written in advance.** Accuracy is measured against keys written from each server's own
  evidence before the run: what a correct diagnosis must find, and what it must not claim.
- **Measure precision on the real estate.** A check that fires on 198 of 200 servers teaches an engineer to ignore it,
  so every check is re-measured on production data before a release.
- **Build with AI as an engineering partner.** I design the architecture and the process and own every decision that
  cannot be undone; the model writes and revises code under written plans, predictions before fixes, zero-cost
  stand-in testing and human gates at every release.

---

### Contact

[rytuality@gmail.com](mailto:rytuality@gmail.com) · [linkedin.com/in/rytuality](https://linkedin.com/in/rytuality)

US citizen, working remotely and available during US business hours.
