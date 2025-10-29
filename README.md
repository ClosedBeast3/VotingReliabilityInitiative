# SPEC-1-US Voting Reliability Initiative

## Background

U.S. elections face reliability challenges that stem from a mix of technical, operational, and legal factors across a highly decentralized system. This project proposes a pragmatic, incremental architecture to raise end-to-end reliability while respecting federalism and existing law.

**Observed pain points** (synthesized from public post‑mortems and election research):

* **Decentralization & inconsistency:** 8k+ jurisdictions with varying processes, equipment, and standards cause uneven reliability and transparency.
* **Limited end-to-end verifiability:** Voters and the public often can’t independently verify that cast ballots were tallied as intended without specialized access.
* **Audit gaps:** Risk-limiting audits (RLA) are not universally implemented or standardized; audit data formats are often proprietary or hard to aggregate.
* **Long-tail operational risks:** Voter roll hygiene, provisional ballot handling, mail ballot processing, and chain-of-custody procedures vary, affecting accuracy and public confidence.
* **Technology heterogeneity:** Mix of paper-based scanners, BMDs, and legacy EMS software with inconsistent logging and observability.
* **Security & resilience:** Supply-chain risk, phishing of officials, DDoS on public info sites, ransomware against counties, and insider threats.
* **Accessibility & language access:** Not uniformly strong; verification flows may create barriers for voters with disabilities or limited English.
* **Public transparency:** Limited real-time, standardized, machine-readable reporting and audit artifacts that the public can inspect.

**Principles for this initiative**

* **Paper-first, software-verified:** Preserve voter-verifiable paper ballots as ground truth while improving digital verifiability and observability.
* **End-to-end verifiability (E2E-V):** Use cryptographic commitments and publishable proofs so any member of the public can independently verify tallies without compromising ballot secrecy.
* **Pragmatic adoption:** Complement (not replace) existing certified systems; pilot at county/state levels with opt-in modules.
* **Interoperability & openness:** Open standards, reference implementations, and permissive licenses to enable vendor-neutral uptake.
* **Human factors & accessibility:** Designs that simplify training, reduce manual error, and meet ADA/Section 203 requirements.
* **Privacy by design:** Protect ballot secrecy and personal data with strong, formally reviewed cryptographic schemes.
* **Auditability by default:** First-class support for RLAs and immutable, append-only, publicly replicated audit logs.

**Initial scope hypothesis**

* Deliver a **verifiable results and audit platform** that can be layered onto current paper-based workflows: cryptographic receipt issuance at cast, public bulletin board for commitments, standardized cast-vote records (CVRs), RLA tooling, and transparent, tamper‑evident publishing.
* Exclude designing new DRE/BMD hardware; integrate with existing EMS and scanner outputs via adapters.

## Requirements

### Must Have (M)

* Preserve voter‑verifiable **paper ballots** as ground truth; no change to certified scanners/BMDs.
* **Public, append‑only bulletin board** for commitments and artifacts (tamper‑evident, globally replicable).
* **Cryptographic commitments/receipts** at cast or ingest (non‑identifying, no link to voter identity).
* Publish **anonymized CVRs** in a standardized, machine‑readable format with privacy safeguards.
* **Deterministic open-source tally** pipeline with reproducible builds and public hash of binaries/configs.
* **Risk‑Limiting Audit (RLA)** support: ballot manifest ingestion, sampling, audit rounds, and reporting.
* **Chain‑of‑custody** logging (time, actor, location) across transport and storage, immutable once published.
* **Access control & least privilege** for officials; comprehensive authN/Z, audit logs, break‑glass workflows.
* **Security baseline:** code signing, supply‑chain SLSA‑level provenance, CIS hardening, backups, disaster recovery.
* **Accessibility & language access** in public portals (WCAG 2.2 AA, Section 203 locales configurable).
* **Interoperability adapters** for major EMS exports (e.g., CVR, ballot manifest, results) with validation.
* **Observability:** metrics, structured logs, integrity checks, and incident reporting API.

### Should Have (S)

* **Threshold signing** of results (e.g., t-of-n keys among officials) and hardware-backed key storage options.
* **Automated RLA sampling** (hypergeometric/Bernoulli) with jurisdictional parameters.
* **Real-time transparency dashboards** (turnout, processing, audit progress) sourced only from verified data.
* **Offline-first ops** with delayed-safe publication for low-connectivity counties.
* **Standardized data schemas** (open JSON/CSV + signed bundles) and versioned public datasets.
* **SIEM integration** and tamper alarms; immutable snapshots to external archives.
* **Training & runbooks** for officials and third-party observers.

### Could Have (C)

* **E2E verifiable tally** pilot (mixnet or homomorphic path) alongside paper audit, for public verification.
* **Public notary anchoring** (e.g., periodic hash anchoring to external ledgers) for extra tamper evidence.
* **Privacy-enhanced CVR publishing** (differential privacy / coarsening for low-turnout precincts).
* **Simulation tooling** for throughput, error injection, and audit sensitivity analyses.

### Won’t Have (W)

* Replacement of voting hardware or Internet/remote voting.
* Any linkage of ballots to voter identity or location beyond what is required for audit sampling.
* Live precinct-level vote counts before polls close; no speculative projections.
* Proprietary, unverifiable black-box components in the critical path.
