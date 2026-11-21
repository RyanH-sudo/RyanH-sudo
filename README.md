## Ryan Haig

**Forward Deployed Engineer.** I take frontier AI models into real operating environments
and make them do reliable engineering work there: diagnosing servers, auditing firewalls, and walking each problem to
a verified fix, with a human in control of everything that touches production. My background is the infrastructure
itself: network engineering, Windows Server administration and architecture, and security operations at a managed
service provider.

**Recognition.** Winner, WatchGuard's 2026 AI Innovation Challenge. My submission, entered under my employer, was
one of five winners selected worldwide from hundreds of submissions across 19 countries, recognized at WatchGuard
IMPACT North America in Nashville, October 2026.

---

### Flagship: NinjaToolKit v9

**A model reads the whole server. Code holds it to the evidence. An engineer decides every change.**

[The case study](https://ryanh-sudo.github.io/ninjatoolkit-case-study/case-study/) ·
[The film](https://ryanh-sudo.github.io/ninjatoolkit-case-study/film/) ·
[Source text and repository](https://github.com/RyanH-sudo/ninjatoolkit-case-study)

NinjaToolKit is an audit and remediation platform for managed Windows Server estates and WatchGuard firewalls. It
ships as one self-contained Windows program that runs on a server for a whole engineering team, with its own agents
on the servers it looks after. It is private company software, so the case study describes its architecture and
method without its source, and the film shows the released program working an estate that does not exist.

**v9.0.2 is the current release (November 20, 2026).** v9 is a rebuild on one schema, built and measured against a
real estate of 189 captured servers, 48 client organizations and 37 firewalls. I designed it, built it and released it.
Everything it does is laid out in the case study's [capability map](https://ryanh-sudo.github.io/ninjatoolkit-case-study/case-study/#11-the-capability-map).

| | |
|---|---|
| **Code** | 139,481 lines of Python in eleven layers whose imports go one way; 32,354 lines of JavaScript; a 4,165-line PowerShell collector |
| **Tests** | 6,145 passing in 670 files, 17 standing verification harnesses, a five-part release gate |
| **Deterministic checks** | 179: 117 for servers, 52 in the firewall engine, 10 on a Firebox's own settings, certificates and reach, mapped to the 287 controls of NIST SP 800-53 Rev 5 Moderate and to CSF 2.0 |
| **Models** | Claude Opus 5.5 with Opus 5 as fallback, GLiNER 2.5 running locally, a hosted calibrated decision model |
| **Load** | 80,161 requests through 2 hours 40 minutes with no error; fifty agents for an hour with no batch lost |
| **AI output held to facts** | 318 of 318 audit fields kept by code's check of what the model wrote; a Job's documents held to its facts the same way |
| **Firewall coverage** | Every one of 1,923 value-carrying element paths in 54 exports accounted for by a trace of the code: 1,531 read, 23 secrets never shown, 369 out of scope with reasons |
| **History** | 6,546 commits since March 2026, 63 version tags, 111 numbered design decisions |

**Under the hood**

| | |
|---|---|
| **Application** | One asynchronous Python package on Quart and Hypercorn; one process serves a whole office; one WebSocket per browser with subscribed topics, so a page hears of a change in the time the write takes |
| **Data** | SQLite in write-ahead mode with one writer and short transactions; one schema of 101 tables, changed only by forward-only numbered steps; an append-only work log; every write stamped by a trigger with the engineer who made it |
| **Agents** | Their own key, a single-use enrolment code, a certificate from the office's own authority, TLS 1.3 with mutual certificates, outbound only; work travels back on the answer to the agent's own report, and a script runs only if its digest matches |
| **Models** | One client for every call: priced before it is sent, held under a ceiling, written to a ledger, refusals resent once on the fallback; shared evidence as a cached prefix, background reads as half-price batches; GLiNER in its own local process; a decision model recalibrated by isotonic regression and accepted under a Clopper-Pearson bound |
| **Proof in code** | Quotes matched against the capture four ways; scripts proved read-only by PowerShell's own parser against allow lists, failing closed; audit prose checked name by name and number by number against the audit's facts |
| **Structure** | Eleven layers whose imports go one way, held by a test that reads the import graph; ratchets on connections, SDK imports, threads, environment reads, file and function size that may only fall |
| **Delivery** | One self-contained Windows folder with the local model inside; an install script that registers it to start after every boot; nightly verified backups with a second location; a support bundle with every secret scrubbed |

**What I built, and why each part is the way it is**

- **The model reads everything first, and code holds it to the evidence.** A server's entire raw output goes to
  Claude Opus in one call (224,423 tokens on the measured run), with no checklist to narrow it. I got there by
  measurement: an earlier design that let the model speak only when sure was right or partly right on 24 of 50
  replayed cases, where one conversation with a best read every turn was right on 40; and one read of a whole
  server named a root cause that 176 checks and twenty reads of its parts had not. Nothing in the product acts on
  a word of that read. A second pass files it into
  typed items, and code checks each one against the record before it can become work.
- **Quotes are pinned to the capture.** A model writes a record the way a person does in a note, not as the row
  stands in the file: an exact search found only 191 of 376 true quotes. So a quote is matched four ways, strictest
  first, and the match records how many rows it fits, so a quote that fits hundreds is known to pin nothing.
- **One loop from a first read to a fix.** The read's next questions are PowerShell the model writes. A script runs
  by itself only when code proves, by parsing it with PowerShell's own parser against allow lists, that it reads and
  changes nothing. About one in ten is refused, rewritten once, or left for an engineer. Proven checks go out as one
  script per server through that server's agent, and the model looks again when the output is back.
- **Small models where they are measurably right.** GLiNER reads names out of free text on the server's own
  processor and only ever proposes. A calibrated decision model places each finding into a kept catalogue of fixes.
  Its stated confidence is not trusted (answers it called 91.4% sure were right 76.1% of the time), so it is
  recalibrated by isotonic regression on labelled answers and accepted only above a line fitted with an exact
  binomial bound on the error rate. Everything else climbs to Opus, whose answer becomes next week's label.
- **A fix is written whole and proved from outside.** A read-only pre-check that is the problem's fingerprint, the
  change, the proof and the way back. It waits at an engineer's gate (two engineers where an office asks for it),
  runs through the agent only when the office allows changes, in waves with a canary, and is proved later by the
  fingerprint run again and by telemetry compared against untouched servers, or it is taken back. The gate is a
  table in code: whether a person is asked is never a question put to a model.
- **A firewall engine that computes exposure as a path.** One model read from a Firebox's configuration export, then
  every route traced from the internet through static NAT and the policy that carries it, past its gate, to the
  internal address and port, the server that holds it and the process that listens there. Six honest end states,
  including "nothing answers here" and "that address belongs to another client". Rule-base anomalies are computed on
  resolved address space, never on alias names, with zones read as the networks they hold, and a first-match
  simulator says which rule really answers each service. Policies carry Policy Manager's own numbers, because 1,428 of
  1,505 sit at a different position in the file. Every element path of 54 exports that carries a value is accounted
  for by a trace of the program's own code, and v9 raises every one of the previous engine's 1,124 faults on the same
  37 firewalls with the same check, severity and words.
- **Causes weighed in code.** Inside a diagnosis, a belief over a family's causes and "other" is updated by Bayes'
  rule as each observation arrives, a model's reading entering only as soft evidence at its calibrated probability.
  The next check is the one with the most expected information for its cost, and a cause is confirmed only on a real
  proof: a native tool's answer, a correlation, a control, or a before and after.
- **Agents and a standing watch.** Each agent reads through the Windows API and starts no other process. It makes
  its own key, is enrolled with a single-use code and a certificate from the platform's own authority, calls out over
  TLS 1.3 and holds the line open; nothing listens at a client. The watch measures which fields move by themselves
  from pairs of captures, with no hand-written ignore list, and drops 92% of records between two looks without
  losing one. When readings trip a rule a Job opens by itself, and servers that go silent together open one Job.
- **Two client audits written by the model and checked by code.** The model is given an audit's facts and nothing
  else; every name and number it writes is checked against them. On the release candidate 318 of 318 fields were
  kept, and three numbers the model invented were refused and rewritten. A Job's time entry, client email and report
  are held to the Job's own record the same way.
- **Engineered to be operated.** One schema of 101 tables with forward-only numbered steps. Sign-in by name, roles,
  nightly verified backups with a second location, a support bundle with every secret scrubbed. Every model call is
  priced before it is sent, held under a ceiling and written to a ledger; the AI is off in a new install. Before
  release the process was soaked, loaded with fifty engineers at once, and killed in the middle of an ingest and of a
  model call, and recovered both times.
- **A release process that finds its own defects.** The evening v9.0.0 shipped I ran it end to end with the real
  model on an invented estate. That run, and filming the fixed build, found four defects that 6,092 passing tests had not. Each was fixed with a
  test that fails on v9.0.0, and v9.0.1 shipped the next morning. Filming v9.0.1 found one more and checking its
  documents two more; v9.0.2 fixed all three the day after, with the firewall pillar completed.

| Release | Date | What changed |
|---|---|---|
| v9.0.2 | November 20, 2026 | The firewall pillar completed (every export path accounted for, zones as networks, every finding on the page); a Job's documents held to its facts; pages that see a new audit and a new export without a restart |
| v9.0.1 | November 19, 2026 | Four defects found by running v9.0.0 for real, fixed and proved in the built program |
| v9.0.0 | November 18, 2026 | A rebuild: one program on one schema, agents, a standing watch, one loop from a first read to a gated fix, both audits written by the model and checked by code |
| v8.3.2 | November 4, 2026 | The script loop made dependable for a whole office |
| v8.3.1 | October 17, 2026 | Every defect found in v8.3.0 fixed; the AI pipeline proven on a simulated fleet and for real |
| v8.0.0 to v8.3.0 | September to October 2026 | The engineer's console, agents that argue over a server's evidence, the Job as the thread of the work |
| v7.6 line | May to August 2026 | Report truthfulness, verification harnesses, firewall accuracy |

---

### Other work

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
| **Applied AI engineering** | Agent harness design, tool use, context engineering, verification of model output in code, evaluation against answer keys with exact error bounds, calibration of a decision model, Bayesian cause inference with checks chosen by expected information per cost, small-model routing (GLiNER, decision models), refusal-aware model routing, prompt caching and batch processing, cost governance, the Claude API |
| **Data engineering and analysis** | Readers for semi-structured captures, XML and telemetry, entity resolution from evidence, schema design with forward-only steps, provenance on every fact, a format's coverage measured by tracing the code that reads it, baselines and drift measured from the data, isotonic calibration, exact binomial bounds, measurement instruments and ledgers |
| **Network engineering** | WatchGuard, Cisco Catalyst, HPE Aruba CX, multi-vendor firewall security, NAT and policy analysis, rule-base anomaly and first-match analysis on resolved address space, VPN cryptography grading, mutual TLS and private certificate authorities, Auvik network operations, Linux network services |
| **Server architecture and administration** | Windows Server 2012 R2 to 2025, Active Directory, DNS, DHCP, Group Policy, Hyper-V and failover clustering, Exchange hybrid, PowerShell at fleet scale |
| **Cloud** | Microsoft Azure, Microsoft 365 multi-tenant administration, Entra ID, Intune, Purview, the Graph API, AWS, Google Cloud |
| **Security operations** | Microsoft Defender XDR, Microsoft Sentinel, Purview eDiscovery, incident response, business email compromise and mailbox forensics across 500+ tenants, NIST SP 800-53 and CSF 2.0 mapping, MITRE ATT&CK |
| **Software and DevOps** | Python (asyncio, Quart), PowerShell, SQL (SQLite), JavaScript (canvas, WebSockets), Git, self-contained Windows builds, release gating, soak, load and failure testing, verification harnesses |

---

### How I work

- **Measure, never recall.** Every number I report is the output of a command run at the time.
- **Hold AI output to evidence in code.** A model proposes; code verifies; a person approves anything irreversible.
- **Let a measurement overturn a design.** The harness I shipped is the inverse of the one I first built, because a
  replay of real cases said the first one was wrong.
- **Test the artifact, not only the suite.** I walk the built product end to end, then run it on real data it has
  never seen, before I call it done, because passing tests have coexisted with wrong output.
- **Score AI against answers written in advance.** Accuracy is measured against keys written from each server's own
  evidence before the run: what a correct diagnosis must find, and what it must not claim.
- **Say what is not proved.** Every release note and case study I write has a section for what is built and not yet
  shown in production.
- **Build with AI as an engineering partner.** I design the architecture and the process and own every decision that
  cannot be undone; the model writes and revises code under written plans, predictions before fixes, zero-cost
  stand-in testing and human gates at every release.

---

### Contact

[rytuality@gmail.com](mailto:rytuality@gmail.com) · [linkedin.com/in/rytuality](https://linkedin.com/in/rytuality)
