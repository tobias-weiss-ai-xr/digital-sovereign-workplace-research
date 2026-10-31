# Towards a Digital Sovereign Workplace for Universities: Stakeholder Needs and Migration Path

**Authors:** Digital Sovereign Workplace Research Corpus  
**Date:** 2026-10-31  
**Corpus basis:** 3,030 papers across 19 categories (digital-sovereign-workplace-research)  
**Status:** Working paper / draft for review

---

## Abstract

Universities are among the most data-intensive and collaboration-dependent
organisations in society, yet their digital infrastructure is overwhelmingly
hosted on proprietary, extra-territorial cloud platforms. This paper outlines
an *avenue* — a staged migration path — towards a **Digital Sovereign
Workplace (DSW)** for higher-education institutions. Drawing on a corpus of
3,030 papers spanning digital sovereignty, open-source platforms, federated
privacy, AI augmentation, employee well-being, hybrid work, identity and
interoperability, and public-sector adoption, we map the distinct and
sometimes conflicting needs of seven university stakeholder groups: university
leadership, IT departments, faculty and researchers, students, administrative
staff, data-protection officers, and external partners. We propose a
five-phase migration model (Assess → Pilot → Federate → Scale → Sustain)
that reconciles these needs through a sovereign technology stack built on
self-hosted collaboration platforms (Nextcloud, openDesk, Collabora,
OnlyOffice), federated identity (OIDC/SAML/SSI), privacy-preserving
computation, and sovereign AI (RAG on institutional data). The paper
identifies the critical tension between sovereignty (control) and capability
(best-in-class tools) as the central research and policy challenge, and
proposes governance mechanisms — including a university consortium model and
open-source sustainability funding — to make sovereign workplaces viable
at scale.

**Keywords:** digital sovereignty, sovereign workplace, universities, higher
education, open source, federated identity, data sovereignty, stakeholder
analysis, migration path, openDesk, Nextcloud

---

## 1. Introduction

The digital transformation of universities has been, in large part, a story of
platform dependency. Over the past decade, higher-education institutions have
migrated email, file storage, document editing, video conferencing, learning
management, and research collaboration onto a small number of proprietary
cloud providers — predominantly Microsoft 365 and Google Workspace. These
platforms offer genuine capability advantages: seamless collaboration,
ubiquitous access, AI-powered assistance, and low operational burden. But they
also create a structural dependency that conflicts with core university
values: academic freedom, data sovereignty, institutional autonomy, and the
public mission of research and teaching.

The concept of a **Digital Sovereign Workplace (DSW)** proposes an alternative:
a digital work environment in which the institution retains control over its
data, infrastructure, and software stack, while still delivering the
collaboration, productivity, and AI capabilities that modern academic work
demands. This is not a retreat from digitalisation but a re-architecting of
it — replacing dependency with autonomy, opacity with auditability, and
data extraction with data stewardship.

Universities are a particularly important and challenging case for DSW
adoption. They are:

- **Data-intensive**: research data, student records, personnel files, and
  intellectual property are among the most sensitive assets an organisation
  can hold.
- **Collaboration-dependent**: academic work is inherently multi-institutional,
  cross-border, and interdisciplinary.
- **Resource-constrained**: IT budgets are small relative to the scale and
  diversity of needs; staff are few.
- **Governance-complex**: universities are federated organisations with
  strong departmental autonomy, academic freedom, and multiple legal
  frameworks (GDPR, national research-data laws, funding-body requirements).
- **Mission-driven**: the public good, open science, and knowledge sharing
  are core values that align with open-source and sovereign approaches.

This paper outlines an *avenue* — a realistic, staged path — towards DSW
adoption in universities, with particular attention to the diverse and
sometimes conflicting needs of university stakeholders. It is grounded in a
systematic review of 3,030 papers spanning 19 research categories including
digital sovereignty, open-source platforms, federated privacy, AI and language
models, employee well-being, hybrid work, identity and interoperability,
public-sector adoption, and security compliance.

### 1.1 Research questions

1. What are the distinct digital-workplace needs of different university
   stakeholder groups, and where do they conflict?
2. What technology stack can satisfy these needs while preserving
   institutional sovereignty?
3. What staged migration path is realistic for a resource-constrained
   university?
4. What governance and sustainability mechanisms are needed to make sovereign
   workplaces viable at scale?

### 1.2 Method

This paper is a synthesis of a curated literature corpus of 3,030 papers
discovered through taxonomy-aware queries against arXiv, OpenAlex, Crossref,
dblp, Europe PMC, and Semantic Scholar. The corpus is organised into 19
categories and 8 subcategory dimensions (theory, application, method,
systems, survey, evaluation, development, mechanism). Stakeholder needs were
extracted from papers in the adoption-change, employee-wellbeing,
hybrid-work, digital-transformation, public-sector, identity-access,
interoperability, federated-privacy, ai-llm, open-source, security-compliance,
and data-sovereignty categories. The migration path and technology stack
proposals integrate findings from the sovereignty, federated-computation, and
open-source-platform literatures.

---

## 2. The University as a Special Case for Digital Sovereignty

### 2.1 Why universities matter

Universities are not just another enterprise. Their digital-sovereignty
challenge is distinctive in several ways:

**Research data sensitivity.** Universities generate and steward research
data that is often legally restricted (GDPR special-category data, clinical
trial data, proprietary industry data, classified defence research). Hosting
this data on extra-territorial platforms creates jurisdictional risk and may
violate funding-body or regulatory requirements. The literature on data
sovereignty and federated computation (101 papers in the federated-privacy
category) provides technical approaches — federated learning, homomorphic
encryption, differential privacy — that allow collaborative research without
centralising sensitive data.

**Academic freedom and institutional autonomy.** Universities have a
constitutional or statutory obligation to protect academic freedom. When
communication, collaboration, and document storage are mediated by a single
proprietary platform, the institution's ability to guarantee confidentiality,
audit data access, and resist external pressure is compromised. The
sovereignty literature (64 papers in data-sovereignty) frames this as a
rights issue, not merely a technical preference.

**Open science and public mission.** Universities are publicly funded
institutions whose mission includes knowledge sharing. The open-source
literature (305 papers) demonstrates that open-source platforms align with
this mission in ways that proprietary platforms do not: transparency,
community governance, and the absence of vendor lock-in.

**Multi-institutional collaboration.** Academic work routinely crosses
institutional and national boundaries. A sovereign workplace must not become
an island — it must interoperate with other institutions' sovereign systems
and with the broader research infrastructure (data repositories, identity
federations, publication systems). The interoperability literature (238
papers) addresses standards (OIDC, SAML, SCIM, OAI-PMH, DataCite) that make
this possible.

**Resource constraints.** Universities have limited IT budgets and staff.
The SME-adoption literature (6 papers, the corpus's thinnest category)
highlights that resource-constrained organisations need bundled,
low-operational-burden solutions. This is directly applicable to universities,
which face similar constraints at the departmental level.

### 2.2 The sovereignty–capability tension

The central tension in DSW adoption — identified across multiple literature
streams — is between **sovereignty** (control over data and infrastructure)
and **capability** (access to best-in-class tools). Proprietary platforms
offer superior AI assistance, real-time collaboration, and seamless
integration. Sovereign platforms offer control, auditability, and alignment
with institutional values but may lag on features.

For universities, this tension is acute: faculty expect the same productivity
tools they use in industry, while the institution must protect research data
and comply with regulations. Resolving this tension — through open-source
platforms that match proprietary capability, sovereign AI that runs on
institutional data, and federation that enables cross-institutional
collaboration — is the defining challenge of the university DSW agenda.

---

## 3. Stakeholder Landscape

A university is not a single organisation but a federation of communities
with distinct needs, priorities, and power. Any DSW migration must account
for all of them. Based on the adoption, well-being, and hybrid-work
literatures, we identify seven stakeholder groups.

### 3.1 University Leadership (Rectorate / Executive Board)

**Primary concerns:** Institutional reputation, regulatory compliance,
strategic autonomy, cost efficiency, risk management.

**Needs:**
- **Compliance assurance**: demonstrable control over where data resides and
  who can access it (GDPR, national research-data laws, funding-body
  requirements).
- **Cost predictability**: avoidance of vendor lock-in and unpredictable
  licensing costs; the ability to negotiate from a position of strength.
- **Strategic autonomy**: the ability to set institutional digital strategy
  without being constrained by a single vendor's roadmap.
- **Risk mitigation**: reduction of single-point-of-failure risk and
  extra-territorial jurisdiction exposure.

**Tensions:** Leadership may prioritise cost and compliance over user
experience, potentially mandating platforms that faculty resist. The
adoption literature (252 papers) warns that top-down mandates without
user buy-in lead to shadow IT and workarounds.

### 3.2 IT Departments / CIO

**Primary concerns:** Operational reliability, security, maintainability,
skills availability, integration complexity.

**Needs:**
- **Operational feasibility**: self-hosted platforms must be deployable and
  maintainable with existing staff and budget. The SME-adoption literature
  highlights that resource constraints are the primary barrier.
- **Security architecture**: sovereign platforms must meet or exceed the
  security standards of proprietary equivalents. The security-compliance
  literature (48 papers) addresses compliance-chain automation and audit
  capabilities.
- **Integration capability**: seamless connection to existing systems (LMS,
  ERP, HR, library systems, identity providers).
- **Skills and support**: access to vendor support, community resources,
  and training for open-source platforms.
- **Monitoring and observability**: ability to monitor, troubleshoot, and
  audit sovereign infrastructure.

**Tensions:** IT departments may resist self-hosted solutions due to
operational burden, preferring managed services even if they compromise
sovereignty. The tooling literature (179 papers) addresses platform
evaluation and operational frameworks.

### 3.3 Faculty and Researchers

**Primary concerns:** Research productivity, collaboration, data protection,
academic freedom, access to cutting-edge tools.

**Needs:**
- **Research data sovereignty**: control over where research data is stored,
  who can access it, and how it is shared. This is especially critical for
  sensitive data (health, social science, proprietary industry data).
- **Collaboration capability**: seamless multi-institutional collaboration
  without forcing partners onto a single platform.
- **AI assistance**: access to capable AI tools (literature search, code
  assistance, data analysis) that run on institutional data without leaking
  it to external providers. The ai-llm literature (280 papers) covers
  sovereign RAG and agentic systems.
- **Academic freedom**: assurance that communication and document storage
  are not subject to external surveillance or takedown.
- **Open science alignment**: platforms that support open data, open
  access, and reproducible research.

**Tensions:** Faculty demand best-in-class tools and may resist platforms
that feel inferior to proprietary alternatives. The well-being literature
(261 papers) notes that tool friction reduces productivity and increases
stress. Shadow IT (personal Dropbox, Google Docs) is common when
institutional tools are inadequate.

### 3.4 Students

**Primary concerns:** Accessibility, usability, learning support, privacy,
equity.

**Needs:**
- **Accessibility**: platforms must be usable on diverse devices, including
  low-end hardware and mobile, and must support assistive technologies.
- **Learning support**: integration with learning management systems (LMS),
  assignment submission, feedback, and grading workflows.
- **Privacy**: student data (grades, communications, behavioural data) must
  be protected from commercial exploitation.
- **Equity**: all students must have equal access regardless of personal
  device or home internet quality.
- **Familiarity**: platforms should not require extensive retraining;
  interfaces should be intuitive.

**Tensions:** Students are the largest user group but have the least
institutional power. Their needs are often overlooked in platform
decisions. The hybrid-work literature (183 papers) on digital fatigue and
always-on culture is relevant: students already experience platform
overload.

### 3.5 Administrative Staff

**Primary concerns:** Process efficiency, document management, compliance,
integration with business systems.

**Needs:**
- **Document workflow**: approval chains, version control, template
  management, and archival compliance.
- **Integration**: connection to ERP, HR, finance, and student information
  systems.
- **Compliance automation**: automated records-of-processing (RoPA)
  generation, retention policies, and audit trails. The RAG literature
  includes work on automated RoPA extraction.
- **Efficiency**: reduction of manual data entry and paper-based processes.

**Tensions:** Administrative staff need reliable, well-integrated tools and
may resist platforms that lack enterprise features (workflow automation,
advanced search, reporting).

### 3.6 Data Protection Officers (DPOs) / Legal

**Primary concerns:** GDPR compliance, data residency, auditability,
risk assessment, legal certainty.

**Needs:**
- **Data residency**: clear, verifiable control over where data is stored
  and processed.
- **Audit trails**: comprehensive, tamper-proof logs of data access and
  processing.
- **DPIA support**: ability to conduct and document Data Protection Impact
  Assessments for new tools.
- **Contractual clarity**: clear data-processing agreements without
  extra-territorial jurisdiction complications.
- **Incident response**: ability to investigate and respond to data
  breaches within institutional control.

**Tensions:** DPOs may block adoption of any platform that cannot
demonstrate compliance, creating a conservative bias. The security-compliance
literature (48 papers) addresses compliance-chain automation.

### 3.7 External Partners (Industry, Other Universities, Funding Bodies)

**Primary concerns:** Interoperability, trust, data sharing agreements,
collaboration efficiency.

**Needs:**
- **Federated collaboration**: ability to collaborate across institutional
  boundaries without forcing partners onto a single platform.
- **Trust frameworks**: mutual recognition of identity and security
  credentials.
- **Data sharing agreements**: clear, machine-readable terms for
  cross-institutional data sharing.
- **Standards compliance**: adherence to research infrastructure standards
  (ORCID, DataCite, EOSC, Gaia-X).

**Tensions:** External partners may prefer widely adopted proprietary
platforms for ease of collaboration. Sovereign platforms must demonstrate
interoperability to be acceptable.

---

## 4. The Sovereign Technology Stack for Universities

Based on the corpus, we propose a five-layer technology stack that addresses
the needs identified above.

### Layer 1: Infrastructure (Self-Hosted or Federated Cloud)

- **Self-hosted on-premise or national cloud**: Nextcloud, openDesk, or
  equivalent platforms deployed on university-owned or nationally hosted
  infrastructure.
- **Federated cloud**: Gaia-X / IDSA data spaces for cross-institutional
  resource sharing.
- **Confidential computing**: hardware-rooted privacy (e.g., RISC-V
  secure enclaves) for sensitive data processing.

### Layer 2: Identity and Access (Federated)

- **Federated identity**: OIDC/SAML-based SSO integrated with institutional
  identity providers (Shibboleth, Keycloak).
- **Self-sovereign identity (SSI)**: for cross-institutional and
  cross-border collaboration where institutional federation is insufficient.
- **Role-based access control (RBAC)**: fine-grained permissions aligned
  with academic roles (student, faculty, researcher, admin, guest).

### Layer 3: Collaboration (Open-Source Office Suite)

- **File storage and sync**: Nextcloud (or equivalent) with end-to-end
  encryption options.
- **Document editing**: Collabora Online or OnlyOffice (integrated into
  Nextcloud) for real-time collaborative editing.
- **Communication**: Matrix-based messaging, Jitsi or BigBlueButton for
  video conferencing.
- **Calendar and contacts**: integrated CalDAV/CardDAV.

### Layer 4: AI and Knowledge (Sovereign)

- **Sovereign RAG**: retrieval-augmented generation over institutional
  data, running entirely on-premise. The Governed Sovereign RAG for Public
  Administration paper (arXiv:2610.36561) provides a template.
- **Multi-agent systems**: LLM-based agents for research assistance,
  literature search, and data analysis, operating on sovereign infrastructure.
- **Automated compliance**: RAG-based extraction of Records of Processing
  Activities (RoPA) from institutional data.

### Layer 5: Privacy-Preserving Computation

- **Federated learning**: for multi-institutional research collaboration
  without centralising sensitive data.
- **Differential privacy and homomorphic encryption**: for statistical
  analysis and model training on protected data.
- **Consent management**: blockchain-based or auditable consent tracking
  for research data use.

---

## 5. Migration Path: Five Phases

Based on the adoption and digital-transformation literatures, we propose a
five-phase migration model that is realistic for resource-constrained
universities.

### Phase 1: Assess (Months 1–3)

**Goal:** Understand current state, identify quick wins, build coalition.

**Activities:**
- **Digital sovereignty audit**: map all cloud services in use, data flows,
  jurisdictional exposure, and compliance gaps.
- **Stakeholder consultation**: structured interviews and surveys with all
  seven stakeholder groups to prioritise needs.
- **Pilot candidate selection**: identify one or two low-risk, high-visibility
  use cases (e.g., departmental file sharing, research data repository).
- **Cost-benefit analysis**: compare total cost of ownership (TCO) of
  sovereign vs. proprietary platforms over 5 years.

**Deliverables:** Sovereignty audit report, stakeholder needs matrix,
pilot plan, TCO comparison.

### Phase 2: Pilot (Months 4–9)

**Goal:** Deploy sovereign platforms in a limited scope and validate.

**Activities:**
- **Deploy Nextcloud + Collabora** for a single department or research group.
- **Integrate with institutional identity** (SSO via OIDC/SAML).
- **Migrate pilot data** with clear rollback plan.
- **Collect user feedback** through surveys and usage analytics.
- **Evaluate against success criteria**: adoption rate, user satisfaction,
  incident count, compliance verification.

**Deliverables:** Pilot deployment, evaluation report, lessons learned,
scaling plan.

### Phase 3: Federate (Months 10–18)

**Goal:** Enable cross-institutional collaboration and expand scope.

**Activities:**
- **Join or establish identity federation** with partner universities.
- **Deploy federated learning infrastructure** for multi-institutional
  research projects.
- **Implement data-space governance** (Gaia-X / IDSA) for research data
  sharing.
- **Expand to additional departments** based on pilot lessons.
- **Deploy sovereign AI** (RAG) for institutional knowledge search.

**Deliverables:** Federation membership, federated learning pilot, expanded
deployment, sovereign AI prototype.

### Phase 4: Scale (Months 19–36)

**Goal:** Institution-wide adoption with full feature parity.

**Activities:**
- **Migrate all departments** to sovereign platforms.
- **Decommission or reduce proprietary platform licenses** (hybrid model:
  keep proprietary for specific high-value use cases if needed).
- **Establish support structures**: helpdesk, training, documentation.
- **Implement advanced features**: workflow automation, advanced search,
  reporting, compliance automation.
- **Conduct institution-wide security audit** and penetration testing.

**Deliverables:** Institution-wide deployment, support infrastructure,
security certification, license reduction plan.

### Phase 5: Sustain (Ongoing)

**Goal:** Long-term viability and continuous improvement.

**Activities:**
- **Consortium participation**: join or form a university consortium for
  shared development, support, and funding of open-source platforms.
- **Upstream contribution**: contribute improvements back to open-source
  projects.
- **Continuous evaluation**: annual review of platform capabilities vs.
  proprietary alternatives; adjust strategy as needed.
- **Skills development**: training programmes for IT staff and users.
- **Research programme**: contribute to the DSW research agenda (empirical
  platform evaluation, federated collaboration, SME adoption).

**Deliverables:** Consortium membership, contribution guidelines, annual
review process, training curriculum.

---

## 6. Governance and Sustainability

### 6.1 University consortium model

No single university can sustain a sovereign workplace alone. The
open-source literature (305 papers) demonstrates that community governance
and shared investment are essential for long-term viability. We propose a
**university consortium model**:

- **Shared development**: pooled resources for platform development and
  maintenance, reducing per-institution cost.
- **Shared support**: centralised helpdesk and expertise available to all
  members.
- **Shared standards**: common interoperability standards and data-sharing
  agreements.
- **Shared research**: collaborative research on DSW effectiveness,
  contributing to the evidence base.

### 6.2 Funding mechanisms

- **Public funding**: national and EU funding programmes (Horizon Europe,
  Digital Europe, national digital sovereignty initiatives) for sovereign
  infrastructure.
- **Institutional budgets**: reallocation of proprietary license budgets
  to sovereign infrastructure and consortium membership.
- **Research grants**: DSW as a research topic (empirical evaluation,
  federated collaboration, sovereign AI) attracts research funding.

### 6.3 Governance structure

- **Steering committee**: representatives from all stakeholder groups
  (leadership, IT, faculty, students, admin, DPO, external partners).
- **Technical working group**: IT staff and developers responsible for
  platform operations and development.
- **User advisory board**: faculty, students, and admin representatives
  providing feedback on usability and features.
- **Ethics and compliance review**: DPO-led review of new features and
  data-processing activities.

---

## 7. Discussion

### 7.1 The sovereignty–capability tension revisited

The five-phase migration model does not resolve the sovereignty–capability
tension; it manages it. Phase 2 (Pilot) explicitly accepts capability gaps
in exchange for learning and sovereignty gains. Phase 4 (Scale) aims for
feature parity but acknowledges that some proprietary capabilities (e.g.,
advanced AI features) may remain superior. The key insight from the
literature is that **sovereignty is not all-or-nothing**: a hybrid model
that uses sovereign platforms for sensitive data and collaboration while
retaining proprietary tools for specific high-value use cases may be the
pragmatic path.

### 7.2 The role of AI

Sovereign AI is both the greatest opportunity and the greatest challenge.
The ai-llm literature (280 papers) shows rapid progress in on-premise LLM
deployment, RAG, and multi-agent systems. But the gap between research
prototypes and production-ready sovereign AI remains significant. Universities
can contribute to closing this gap by participating in open-source AI
development and by providing real-world testbeds.

### 7.3 Well-being implications

The well-being literature (261 papers) suggests that platform design affects
employee (and student) well-being. Sovereign platforms that are designed for
institutional control rather than engagement maximisation may produce better
well-being outcomes — but this hypothesis has not been tested. The university
DSW migration is an opportunity to conduct such tests, contributing to both
the well-being and the sovereignty literatures.

### 7.4 Limitations

- This paper is a synthesis of existing literature, not an empirical study.
  The proposed migration path has not been validated in a university setting.
- The corpus is biased towards recent publications (85% from 2025–2026) and
  may not capture older, foundational work.
- The stakeholder analysis is based on literature synthesis, not primary
  research with university stakeholders.
- Cost estimates (TCO comparison) are not quantified; this requires
  institution-specific analysis.

---

## 8. Conclusion

Universities face a defining choice: continue deepening their dependency on
proprietary cloud platforms, or invest in sovereign alternatives that align
with their mission, values, and legal obligations. This paper has outlined
an *avenue* — a realistic, staged path — towards a Digital Sovereign
Workplace for universities, grounded in a systematic review of 3,030 papers.

The key findings are:

1. **Stakeholder needs are diverse and sometimes conflicting.** Leadership
   prioritises compliance and cost; IT prioritises operability; faculty
   prioritise capability and academic freedom; students prioritise
   accessibility and privacy; admin prioritises efficiency; DPOs prioritise
   compliance; external partners prioritise interoperability. No single
   platform satisfies all; governance mechanisms (steering committee, user
   advisory board) are essential for balancing these needs.

2. **A five-layer technology stack** (infrastructure, identity, collaboration,
   AI, privacy-preserving computation) can address the full range of
   stakeholder needs while preserving sovereignty.

3. **A five-phase migration model** (Assess → Pilot → Federate → Scale →
   Sustain) is realistic for resource-constrained universities, starting with
   low-risk pilots and building towards institution-wide adoption.

4. **Governance and sustainability** require a consortium model, public
   funding, and upstream contribution to open-source communities.

5. **The sovereignty–capability tension** remains the central challenge. A
   hybrid model that combines sovereign platforms with targeted use of
   proprietary tools may be the pragmatic path, but empirical evaluation is
   needed.

The university DSW agenda is both a research programme and a policy
imperative. By acting as early adopters, universities can simultaneously
protect their institutional autonomy, advance open science, and contribute
to the evidence base that will make sovereign workplaces viable for all
organisations — including the SMEs and public-sector bodies that face even
greater resource constraints.

---

## References

This paper synthesises findings from the following literature streams (paper
counts from the DSW corpus):

1. Data Sovereignty (64 papers) — sovereign cloud, data spaces, self-hosted
   platforms, federated computation.
2. Open Source (305 papers) — self-hosting, platform governance, community
   dynamics, sustainability.
3. Federated & Privacy-Preserving (101 papers) — federated learning,
   homomorphic encryption, differential privacy, consent management.
4. AI & Language Models (280 papers) — sovereign RAG, multi-agent systems,
   AI governance, productivity augmentation.
5. Employee Well-Being (261 papers) — digital fatigue, algorithmic
   management, psychological safety, psychosocial risk.
6. Hybrid & Remote Work (183 papers) — spatial dynamics, productivity,
   fatigue, public-sector hybrid work.
7. Digital Transformation & Adoption (382 papers combined) — capability
   profiles, adoption paradox, SME adoption, AI-enabled HRM.
8. Identity & Access (40 papers) — federated identity, cross-border
   credentials, SSO/OIDC/SAML.
9. Interoperability & Standards (238 papers) — data spaces, standards,
   cross-border credential friction.
10. Public Sector & Education (154 papers) — public-sector transformation,
    digital skills, E-HRM.
11. Security & Compliance (48 papers) — CRA compliance, consent management,
    compliance automation.
12. Collaboration & Productivity (79 papers) — sovereign collaboration,
    communication theories, data spaces.
13. Tooling & Platforms (179 papers) — platform evaluation, operational
    frameworks.
14. Evaluation & Case Studies (204 papers) — empirical evaluation methods,
    case study designs.
15. Surveys & Reviews (221 papers) — systematic reviews, bibliometric
    analyses.
16. Methods (195 papers) — research methodologies for digital workplace
    studies.

**Key cited works (from corpus):**

- Governed Sovereign RAG for Public Administration (arXiv:2610.36561) —
  tripartite epistemic routing for sovereign AI.
- Policy-Driven AI in Dataspaces (arXiv:2507.20014) — taxonomy for
  explainable AI in federated data spaces.
- CYBERFORT: Compliance-Chain Platform for SMEs (arXiv:2610.09918) —
  operationalising the Cyber Resilience Act.
- ClinConNet: Blockchain-Based Dynamic Consent Management
  (arXiv:2602.02610) — auditable consent for sensitive data.
- PANEL: Open-Source Self-Hosted Web Platform (arXiv:2609.31392) —
  self-hosting as sovereign practice.
- Steps towards a digital sovereignty (Zenodo, 2026) — self-hosted
  infrastructure as precondition for sovereignty.
- FLAI Protocol: Decentralised Federated Learning (arXiv:2610.17546) —
  federated learning with on-chain incentives.
- Human-Centred AI and Employee Well-Being (JBII, 2026) — psychological
  safety as mediator.
- Digital Skills Are Not Enough (Merits, 2026) — digital-human capability
  profiles.
- Employee-Office Workplace Alignment in Hybrid Work (TU Darmstadt, 2026) —
  spatial dynamics of hybrid work.

---

*This paper is a working draft. It synthesises findings from the Digital
Sovereign Workplace research corpus (3,030 papers). Contributions,
corrections, and extensions are welcome.*
PY