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
[ninjatoolkit-case-study](https://github.com/RyanH-sudo/ninjatoolkit-case-study))

An engineer-facing platform for managed Windows Server estates and WatchGuard firewalls, shipped as one
self-contained executable and in production use across 224 servers and 48 client organizations.

- An adversarial multi-agent diagnosis: a proposer, a challenger whose task is to break the proposal, an arbiter that
  rules on every claim, and a writer that turns rulings into issues, with claims streamed into the interface as they
  are written.
- Agent output held to evidence in code: a fixed claim format, issues dropped if they cite anything the rulings do not
  support, readings kept only on quoted lines of real output, fixes held if their backup or revert would fail.
- A structural safety model: no transport to client machines, read-only tests under run tokens with a hash chain of
  custody, fixes with a backup, a literal revert and a verification, and a human approval on every change.
- 55 deterministic server judges, a 52-check firewall engine mapped to 50 controls in PCI DSS, CIS, NIST CSF and CMMC,
  and a 47-section PowerShell collector.
- 204,000 lines of product code, 13,875 tests, 19 standing verification harnesses, and 56 tagged releases in six
  months, each walked end to end in the built executable before it shipped.

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
| **Applied AI engineering** | Multi-agent orchestration, context engineering, evaluation and verification of model output, refusal-aware model routing, cost governance, the Claude API |
| **Network engineering** | WatchGuard, Cisco Catalyst, HPE Aruba CX, multi-vendor firewall security, Auvik network operations, Linux network services |
| **Server architecture and administration** | Windows Server 2012 R2 to 2025, Active Directory, Group Policy, Hyper-V and failover clustering, Exchange hybrid |
| **Cloud** | Microsoft Azure, Microsoft 365 multi-tenant administration, Entra ID, Intune, Purview, the Graph API, AWS, Google Cloud |
| **Security operations** | Microsoft Defender XDR, Microsoft Sentinel, Purview eDiscovery, incident response, business email compromise and mailbox forensics across 500+ tenants |
| **Software and DevOps** | Python, PowerShell, SQL, Flask, JavaScript, Git, single-file Windows builds, release gating and verification harnesses |

---

### How I work

- **Measure, never recall.** Every number I report is the output of a command run at the time.
- **Hold AI output to evidence in code.** A model proposes; code verifies; a person approves anything irreversible.
- **Test the artifact, not only the suite.** I walk the built product end to end before I call it done, because
  passing tests have coexisted with wrong output.
- **Build with AI as an engineering partner.** I design the architecture and the process and own every decision that
  cannot be undone; the model writes and revises code under written plans, predictions before fixes, zero-cost
  stand-in testing and human gates at every release.

---

### Contact

[rytuality@gmail.com](mailto:rytuality@gmail.com) · [linkedin.com/in/rytuality](https://linkedin.com/in/rytuality)

US citizen, working remotely and available during US business hours.
