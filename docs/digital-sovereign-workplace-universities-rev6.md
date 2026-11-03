# Towards a Digital Sovereign Workplace for Universities: A Socio-Technical Transition Framework

**Authors:** Digital Sovereign Workplace Research Corpus
**Date:** 2026-10-31
**Corpus basis:** 3,030 papers across 19 categories (frozen snapshot: 2026-10-31)
**Status:** Working paper / draft for review (Revision 6 — unified theoretical framework)

---

## Abstract

Universities are among the most data-intensive and collaboration-dependent
organisations in society, yet their digital infrastructure is overwhelmingly
hosted on proprietary, extra-territorial cloud platforms. This paper argues
that the Digital Sovereign Workplace (DSW) is not a technology deployment
but a **socio-technical transition** — a reconfiguration of the relationship
between an institution and its digital infrastructure. Drawing on a corpus
of 3,030 papers spanning digital sovereignty, open-source platforms,
federated privacy, AI augmentation, and public-sector adoption, we develop
the **Sovereign Workplace Transition Framework (SWTF)**, which integrates
socio-technical systems theory, institutional theory, technology affordance
theory, and a power/equity lens into a single analytical structure. The
framework treats technology as necessary but not sufficient: the transition
requires institutional change, power redistribution, and value
re-articulation. We map the distinct and sometimes conflicting needs of
twelve university stakeholder groups through the framework's six sovereignty
dimensions and six capability requirements, propose a five-layer technology
stack separated into available-now, emerging, and research-stage components,
and outline a five-phase migration model with SMART success criteria,
rollback scenarios, and adaptive governance. The paper engages with
counter-evidence, identifies the sovereignty–capability tension as the
central challenge, and proposes governance mechanisms including a
university consortium model. A normative guard against techno-solutionism,
equity as a design principle (not an add-on), and explicit attention to
power dynamics are built into the framework rather than treated as
afterthoughts. Limitations include the absence of primary stakeholder
research, the illustrative nature of cost estimates, and corpus quality
issues.

**Keywords:** digital sovereignty, sovereign workplace, universities, higher
education, socio-technical transition, open source, federated identity,
stakeholder analysis, migration path, openDesk, Nextcloud, governance,
equity, institutional theory

---

## Part I: Framework and Core Argument

---

## 1. Introduction

### 1.1 Problem statement

Over the past decade, higher-education institutions have migrated email, file
storage, document editing, video conferencing, learning management, and
research collaboration onto a small number of proprietary cloud providers —
predominantly Microsoft 365 and Google Workspace. These platforms offer
genuine capability advantages: seamless collaboration, ubiquitous access,
AI-powered assistance, and low operational burden. But they create structural
dependency conflicting with core university values: academic freedom, data
sovereignty, institutional autonomy, and the public mission of research and
teaching.

The Digital Sovereign Workplace (DSW) proposes an alternative: a digital
work environment where the institution retains control over its data,
infrastructure, and software stack while delivering the collaboration,
productivity, and AI capabilities modern academic work demands. This is not
a retreat from digitalisation but a re-architecting — replacing dependency
with autonomy, opacity with auditability, and data extraction with
stewardship.

### 1.2 Why universities are a special case

Universities are not just another enterprise. Their digital-sovereignty
challenge is distinctive:

- **Research data sensitivity**: Research data is often legally restricted
  (GDPR special-category data, clinical trials, proprietary industry data,
  classified defence research). Hosting on extra-territorial platforms
  creates jurisdictional risk. *Caveat*: not all research data requires
  sovereign infrastructure — much is already public (open data, published
  results). The need is proportional to sensitivity.

- **Academic freedom**: Universities have statutory obligations to protect
  academic freedom. When communication and storage are mediated by a single
  proprietary platform, the institution's ability to guarantee
  confidentiality and resist external pressure is compromised. *Evidence
  gap*: no documented cases exist in the corpus of platforms being used to
  suppress academic work; this risk is theoretical but structurally real.

- **Open science mission**: Publicly funded institutions whose mission
  includes knowledge sharing. Open-source platforms align with this mission
  through transparency and absence of vendor lock-in. *Counter-evidence*:
  some studies show proprietary platforms accelerate research productivity
  through better tooling (see §6.1).

- **Multi-institutional collaboration**: Academic work crosses institutional
  and national boundaries. Sovereign workplaces must interoperate, not
  become islands.

- **Resource constraints**: IT budgets are small relative to needs. The
  corpus contains only 6 papers on SME adoption — insufficient for strong
  conclusions, but suggestive that resource-constrained organisations need
  bundled, low-operational-burden solutions.

### 1.3 The sovereignty–capability tension

The central tension is between **sovereignty** (control) and **capability**
(features/usability). Microsoft 365 and Google Workspace score high on
capability (collaboration, AI, mobile access, reliability) but low on
sovereignty (data location, vendor lock-in, opacity). Sovereign alternatives
score high on sovereignty (open source, self-hosted, auditable) but
historically lower on capability (fragmented, less polished, smaller
ecosystem). The DSW thesis is that this gap is narrowing (openDesk,
Nextcloud, Collabora) but has not closed. This tension is not merely
technical; it is institutional, economic, and political.

### 1.4 Research questions

1. What are the distinct digital-workplace needs of university stakeholders,
   and how do they conflict?
2. What technology stack can deliver sovereign capabilities comparable to
   proprietary platforms?
3. What migration path balances speed, risk, and organisational capacity?
4. What governance structures sustain a sovereign workplace over time?
5. Under what conditions does the sovereignty–capability trade-off favour
   migration?
6. **(New)** Is the DSW problem fundamentally technological, or does
   technology obscure deeper institutional and political dimensions?

### 1.5 Method and limitations

**Method:** Literature synthesis over a frozen corpus of 3,030 papers across
19 categories. Papers were discovered via taxonomy-aware arXiv/OpenAlex
queries and classified into the corpus taxonomy. Insights are grounded in
title/abstract analysis. No primary data collection was performed.

**Limitations:**
- Corpus quality: auto-ingestion includes off-topic and low-quality papers
  (editorials, predatory-journal articles, Zenodo preprints). Counts are
  indicative, not precise.
- No primary stakeholder research: all stakeholder needs are inferred from
  literature, not empirically validated.
- Cost estimates are illustrative frameworks, not empirical TCO studies.
- The corpus is heavily skewed to 2025–2026 (85% of papers), reflecting
  recent ingestion bias.
- Author and venue metadata is sparse in the corpus.

### 1.6 How to read this paper

- **Part I (§1–8):** Framework and core argument. Start here for the thesis
  and migration model.
- **Part II (§9–13):** Dimensional analysis through the framework's lenses.
- **Part III (§14–18):** Transition pathway, governance, and evaluation.
- **Part IV (§19–22):** Synthesis, tensions, and research agenda.

---

## 2. The Sovereign Workplace Transition Framework (SWTF)

This section presents the unified theoretical framework that integrates all
subsequent analysis. It is the organising spine of the paper.

### 2.1 Why a unified framework is needed

The DSW literature is fragmented across disciplines: information systems
focuses on architecture and governance; computer science on protocols and
security; law on GDPR and procurement; economics on cost and market failure;
organisational behaviour on change management; and so on. Each discipline
uses different concepts, assumptions, and evaluation criteria. Without a
unifying framework, the DSW thesis appears as a collection of disconnected
claims rather than a coherent transition model. Moreover, the
techno-solutionism critique (§2.4) requires a framework that can question
whether the problem is technological at all.

### 2.2 Theoretical foundations

The SWTF integrates four theoretical traditions:

**1. Socio-Technical Systems Theory (STST).** Originating in the Tavistock
Institute's work on coal mining (Trist & Bamforth, 1951) and formalised by
Cherns (1976) and Bostrom & Heinen (1977), STST holds that organisations
are joint optimisations of social and technical systems. Neither can be
designed in isolation; the "best" technical system depends on the social
context, and vice versa. For DSW, this means the sovereign workplace is not
a software product but a configuration of technology, people, processes, and
culture. STST's core principle — joint optimisation — becomes the
framework's central design rule: sovereignty and capability must be
optimised together, not traded off.

**2. Institutional Theory.** DiMaggio & Powell (1983) and Scott (2014)
explain how institutions adopt, legitimise, and sustain practices through
coercive (regulatory), mimetic (imitative), and normative (professional)
isomorphism. For DSW, institutional theory explains why universities adopt
proprietary platforms (mimetic isomorphism: "everyone else uses Microsoft")
and what would be needed to shift adoption (normative isomorphism:
professional associations endorsing sovereign alternatives). It also
explains why DSW may fail even if technically superior: institutional
legitimacy, not technical merit, drives adoption.

**3. Technology Affordance Theory.** Gibson (1979) and Norman (1988)
introduced affordances as action possibilities offered by an object;
Leonardi (2011) and Faraj & Azad (2012) extended this to digital
technology, emphasising that affordances are relational (they exist
between technology and user, not in technology alone). For DSW, this means
sovereignty is not a property of a platform but a relationship between
the institution and its infrastructure. A "sovereign" platform that
affords surveillance and control is not sovereign in any meaningful sense.
Affordance theory thus provides the analytical tool for the
instrumental-vs-substantive rationality critique (§2.4).

**4. Power and Equity Lens.** Feminist STS (Haraway, 1988; Wajcman, 2004),
disability studies (Shakespeare, 2014), and indigenous data sovereignty
(CARE principles, Carroll et al., 2020) reveal that technology is never
neutral: it encodes power relations, privileges certain users, and
marginalises others. For DSW, this lens ensures that sovereignty is
analysed not just as institutional control but as *whose* control, *over
whom*, and *with what effects*. Equity is a design principle, not an
afterthought.

### 2.3 The SWTF: dimensions, levels, and principles

The framework has **three analytical constructs**:

#### Construct 1: Sovereignty Dimensions (6)

What the institution seeks to control:

| # | Dimension | Definition | Key question |
|---|-----------|-----------|--------------|
| S1 | Data sovereignty | Control over where data is stored, who can access it, and under which jurisdiction | Can we guarantee data location and access control? |
| S2 | Software sovereignty | Ability to inspect, modify, and redistribute the software | Can we audit and modify the code? |
| S3 | Infrastructure sovereignty | Control over the hosting environment (on-prem, private cloud, trusted provider) | Do we own or control the infrastructure? |
| S4 | Identity sovereignty | Control over authentication, authorisation, and identity data | Do we control who can access what? |
| S5 | AI sovereignty | Control over AI models, training data, and inference pipelines | Do we control the AI that processes our data? |
| S6 | Governance sovereignty | Institutional control over platform decisions, roadmap, and policy | Do we have a voice in platform governance? |

#### Construct 2: Capability Requirements (6)

What the workplace must deliver:

| # | Requirement | Definition | Proprietary benchmark |
|---|-------------|-----------|---------------------|
| C1 | Collaboration | Real-time co-editing, sharing, communication | Microsoft 365, Google Workspace |
| C2 | Productivity | Document creation, email, calendar, task management | Office suite, Gmail |
| C3 | Security & compliance | Encryption, access control, audit, regulatory compliance | Enterprise security suites |
| C4 | Interoperability | Cross-institution, cross-platform, cross-border data exchange | Standards-based APIs |
| C5 | Usability | Low learning curve, accessibility, multilingual support | Consumer-grade UX |
| C6 | Cost-efficiency | Sustainable TCO, predictable costs, no vendor lock-in | Subscription pricing |

#### Construct 3: Analytical Levels (4)

Where analysis occurs:

| Level | Focus | Example questions |
|-------|-------|-------------------|
| Micro | Individual users, practices, needs, agency | How do researchers actually use collaboration tools? |
| Meso | Organisational units, departments, governance bodies | How does IT governance shape platform adoption? |
| Macro | Sector, national, international policy and market | What policy instruments support DSW? |
| Temporal | Transition phases, path dependencies, feedback loops | How do early decisions constrain later options? |

#### Cross-cutting principles (3)

1. **Equity by design.** Accessibility, gender, indigenous, and digital-divide
   considerations are design principles, not post-hoc checks. Every
   sovereignty dimension and capability requirement is evaluated for
   differential impact across user groups.

2. **Techno-solutionism guard.** Before proposing a technical solution, the
   framework requires asking: (a) Is this problem fundamentally
   technological? (b) Could institutional, cultural, or political change
   address it? (c) What new problems does the proposed technology create?
   This guard is operationalised as a checklist in §3.

3. **Adaptive governance.** Transitions are not linear. The framework
   incorporates feedback loops, rollback triggers, and learning mechanisms.
   Early phases generate evidence that reshapes later phases.

### 2.4 Techno-solutionism guard (operationalised)

The philosophy-of-technology critique (Morozov, 2013; Feenberg, 2010)
warns that framing institutional problems as technology problems obscures
their social, political, and economic dimensions. The SWTF addresses this
through a three-question guard applied to every DSW proposal:

1. **Problem diagnosis:** Is the problem technological, or is it about
   power, culture, resources, or governance? (If the latter, technology
   alone cannot solve it.)
2. **Solution proportionality:** Does the proposed technology solve the
   diagnosed problem, or does it create new capabilities that distract from
   the underlying issue?
3. **Relocation test:** Does the solution relocate control (e.g., from
   Microsoft to a university IT department) without changing the
   underlying power structure? If so, it may be "sovereignty theatre."

**Application to DSW:** The DSW is partly a genuine technology problem
(data location, vendor lock-in, opacity) and partly an institutional
problem (procurement practices, IT governance, resource allocation,
cultural dependency on consumer-grade UX). The framework does not assume
DSW solves the institutional problem; it flags where institutional change
is prerequisite.

### 2.5 Equity as a design principle

Equity is not a section or a consideration; it is a lens applied to every
dimension. The framework incorporates:

- **Accessibility (disability studies):** WCAG 2.2 AA compliance is a
  minimum, not a target. Sovereign platforms must be evaluated for screen
  reader compatibility, keyboard navigation, cognitive load, and
  alternative input methods. If a sovereign platform is less accessible
  than its proprietary counterpart, migration reduces equity.

- **Gender and intersectionality (feminist studies):** Platform design
  encodes gendered assumptions (e.g., always-on collaboration norms,
  surveillance of "productivity"). DSW must be evaluated for differential
  impact on caregivers, part-time staff, and marginalised groups.

- **Indigenous data sovereignty (CARE principles):** For universities with
  indigenous research partnerships, data sovereignty extends to community
  control over indigenous data. The DSW must support CARE (Collective
  benefit, Authority to control, Responsibility, Ethics) alongside FAIR.

- **Digital divide:** Not all users have equal connectivity, devices, or
  digital literacy. Sovereign platforms that assume high bandwidth or
  technical sophistication may exclude.

### 2.6 How the framework addresses the 11 disciplinary perspectives

Rather than treating disciplines as separate sections, the SWTF integrates
them as **analytical lenses** applied through the framework's constructs:

| Discipline | Primary construct | Lens applied |
|-----------|-------------------|-------------|
| Information Systems | Socio-technical configuration | Joint optimisation of IT and organisation |
| Computer Science | Sovereignty dimensions (S1–S6) | Technical feasibility and security |
| Law | Institutional embeddedness (macro) | Regulatory compliance and rights |
| Economics | Capability requirements (C6) + institutional | Cost, market failure, incentives |
| Organisational Behaviour | Socio-technical configuration (social) | Change, culture, resistance |
| Higher Education Policy | Institutional embeddedness (sector) | Open science, teaching, assessment |
| Security Engineering | Sovereignty dimensions (S1, S3, S4) | Threat model, architecture |
| HCI/UX | Capability requirements (C5) | Usability, accessibility, onboarding |
| Public Policy | Institutional embeddedness (macro) | Policy instruments, international |
| Philosophy of Technology | Techno-solutionism guard | Normative critique |
| Disability/Feminist/Indigenous | Equity by design | Differential impact |

---

## 3. Stakeholder Landscape (through the SWTF lens)

Twelve university stakeholder groups, analysed through the framework's
sovereignty dimensions and capability requirements. Each group's needs
are mapped to specific (S, C) pairs, and conflicts are identified.

### 3.1 University Leadership (Rectorate / Executive Board)

**Primary dimensions:** S6 (governance sovereignty), C6 (cost-efficiency)
**Needs:** Strategic control, risk management, cost predictability,
regulatory compliance, reputation.
**Conflicts:** Leadership prioritises cost and risk; faculty prioritise
capability and academic freedom. Leadership may overestimate migration
risk (status quo bias) or underestimate it (optimism bias).

### 3.2 IT Departments / CIO

**Primary dimensions:** S1–S6 (all), C3 (security), C6 (cost)
**Needs:** Operational feasibility, security, staffing, vendor management,
technical debt reduction.
**Conflicts:** IT wants standardisation and control; researchers want
flexibility and cutting-edge tools. IT may resist migration due to
skill gaps or fear of operational burden.

### 3.3 Faculty and Researchers

**Primary dimensions:** S1 (data), S5 (AI), C1 (collaboration), C2
(productivity)
**Needs:** Seamless collaboration, AI assistance, data control for
sensitive research, minimal disruption.
**Conflicts:** Researchers need capabilities that sovereign platforms
may lack (AI, mobile, integration). They may resist migration if it
reduces productivity. Counter-evidence (§6.1) suggests proprietary
platforms improve research productivity.

### 3.4 Students

**Primary dimensions:** C1, C2, C5 (usability)
**Needs:** Familiar tools, mobile access, accessibility, integration
with learning management.
**Conflicts:** Students expect consumer-grade UX; sovereign platforms
may have steeper learning curves. Accessibility gaps (§2.5) may
disproportionately affect disabled students.

### 3.5 Administrative Staff

**Primary dimensions:** C2, C3, C6
**Needs:** Reliable email, document management, workflow automation,
compliance.
**Conflicts:** Admin staff are risk-averse and change-resistant; they
need strong change management (§14).

### 3.6 Data Protection Officers / Legal

**Primary dimensions:** S1 (data), S3 (infrastructure), S6 (governance)
**Needs:** GDPR compliance, data location guarantees, audit trails,
contractual control.
**Conflicts:** DPOs may demand sovereignty levels that are technically
infeasible or economically unsustainable (sovereignty theatre risk).

### 3.7 External Partners

**Primary dimensions:** C4 (interoperability), S1 (data)
**Needs:** Cross-institution collaboration, data sharing, federated
access.
**Conflicts:** Sovereign islands that cannot interoperate defeat the
purpose. Federation standards (eduGAIN, SAML, OIDC) are critical.

### 3.8 Libraries and Information Services

**Primary dimensions:** S1, S4 (identity), C4
**Needs:** Integration with institutional repositories, open access
compliance, long-term preservation.
**Conflicts:** Libraries have preservation mandates that may conflict
with platform migration timelines.

### 3.9 Research Computing / HPC Centres

**Primary dimensions:** S1, S3, S5 (AI)
**Needs:** High-performance storage, GPU access, data pipelines,
integration with HPC workflows.
**Conflicts:** HPC centres may have existing sovereign infrastructure
that conflicts with or complements DSW.

### 3.10 Procurement and Finance

**Primary dimensions:** C6, S6
**Needs:** Transparent pricing, competitive tendering, lifecycle cost
analysis, exit strategies.
**Conflicts:** Procurement rules (EU public procurement) may favour
incumbent vendors or require open competition that sovereign
consortia cannot meet.

### 3.11 Student Unions / Governance Bodies

**Primary dimensions:** S6 (governance), equity
**Needs:** Democratic oversight, student data rights, transparency.
**Conflicts:** Student bodies may demand more sovereignty than
institutional leadership is willing to invest in.

### 3.12 International Partners

**Primary dimensions:** C4, S1
**Needs:** Cross-border data flows, compliance with multiple
jurisdictions, federated identity.
**Conflicts:** Data sovereignty requirements may conflict with
international collaboration needs (§6.4).

### 3.13 Power dynamics analysis

The SWTF's power/equity lens reveals that DSW is not merely a
technical migration but a **redistribution of power**:

- **From vendors to institutions:** Reduces vendor lock-in and data
  extraction. But concentrates power in institutional IT, which may
  not be more accountable than vendors.

- **From central IT to departments:** Sovereign platforms may enable
  departmental self-hosting, fragmenting governance.

- **From staff to students:** Student data rights may be strengthened
  or weakened depending on implementation.

- **From Global North to Global South:** Sovereign platforms developed
  in Europe may not serve Global South institutions without
  adaptation.

The framework requires explicit power analysis at each phase, not
just technical assessment.

---

## 4. Technology Stack (Three-Tier Classification)

Analysed through the framework's sovereignty dimensions and capability
requirements. Each component is rated on (S1–S6) sovereignty and
(C1–C6) capability.

### Tier 1: Available Now (production-ready)

| Component | Function | Sovereignty | Capability | Maturity |
|-----------|----------|-------------|------------|----------|
| Nextcloud | File storage, sync, sharing | S1, S2, S3 | C1, C2 | High |
| Collabora Online / OnlyOffice | Document editing | S1, S2 | C2 | High |
| Keycloak | Identity & access management | S4 | C3 | High |
| Jitsi / BigBlueButton | Video conferencing | S1, S2, S3 | C1 | Medium-High |
| Matrix / Element | Messaging | S1, S2 | C1 | Medium |
| openDesk | Integrated workplace suite | S1–S6 | C1–C6 | Medium (emerging) |

### Tier 2: Emerging (deployable with effort)

| Component | Function | Sovereignty | Capability | Maturity |
|-----------|----------|-------------|------------|----------|
| Sovereign RAG / LLM | AI assistance | S5 | C2, C1 | Low-Medium |
| Federated learning | Privacy-preserving ML | S1, S5 | C3 | Low-Medium |
| Gaia-X data spaces | Cross-institution data sharing | S1, S4, S6 | C4 | Low |
| OIDC federation (eduGAIN) | Cross-institution identity | S4 | C4 | Medium |

### Tier 3: Research Stage (not production-ready)

| Component | Function | Sovereignty | Capability | Maturity |
|-----------|----------|-------------|------------|----------|
| Homomorphic encryption | Privacy-preserving computation | S1 | C3 | Research |
| Differential privacy | Data anonymisation | S1 | C3 | Research |
| Decentralised identity (DID) | Self-sovereign identity | S4 | C4 | Research |
| Confidential computing | Trusted execution | S3 | C3 | Research |

### 4.1 Missing from the stack (must be addressed)

- **Email:** No mature sovereign email solution exists. This is a
  critical gap — email is the most used workplace tool.
- **Mobile experience:** Sovereign platforms lag in mobile UX.
- **AI integration:** Sovereign AI is 2–3 years behind proprietary
  (Copilot, Gemini).
- **Accessibility tooling:** Screen reader support, cognitive
  accessibility are underdeveloped in open-source.
- **Offline capability:** Many sovereign tools require connectivity.

---

## 5. Migration Path: Five Phases (with SMART criteria)

### Phase 1: Assess (Months 1–6)

**Objective:** Understand current state, needs, and feasibility.
**Activities:** Inventory of digital tools and data; stakeholder needs
assessment; data classification; cost baseline; risk assessment.
**SMART criteria:**
- Complete tool inventory (100% of university units)
- Data classification for 80% of data stores
- Stakeholder needs survey (≥60% response rate)
- Cost baseline documented
**Rollback:** N/A (assessment only)
**Techno-solutionism guard:** Verify that identified problems are not
solvable by policy/cultural change before proposing technology.

### Phase 2: Pilot (Months 7–12)

**Objective:** Deploy sovereign tools in a limited scope to generate
evidence.
**Activities:** Pilot Nextcloud + Collabora for one department; pilot
Keycloak for SSO; evaluate UX and reliability.
**SMART criteria:**
- ≥80% user satisfaction in pilot group
- Zero critical security incidents
- <5% increase in support tickets
- Documented lessons learned
**Rollback:** Revert pilot group to proprietary tools within 2 weeks if
satisfaction <60% or critical incidents occur.

### Phase 3: Federate (Months 13–24)

**Objective:** Connect sovereign tools across institutions.
**Activities:** Join eduGAIN federation; deploy OIDC; establish data
sharing agreements; pilot cross-institution collaboration.
**SMART criteria:**
- ≥3 institutions federated
- Cross-institution file sharing functional
- Federated identity working for ≥90% of users
**Rollback:** Maintain proprietary federation as fallback; phased
decommission.

### Phase 4: Scale (Months 25–48)

**Objective:** Roll out to entire institution.
**Activities:** Migrate all units; decommission proprietary tools;
establish support structures; train staff.
**SMART criteria:**
- 100% of units migrated
- Proprietary licences reduced by ≥80%
- Support ticket volume ≤ baseline + 20%
- User satisfaction ≥75%
**Rollback:** Maintain hybrid operation; revert individual units if
needed.

### Phase 5: Sustain (Ongoing)

**Objective:** Maintain and evolve the sovereign workplace.
**Activities:** Continuous improvement; upstream contributions; consortium
participation; regular security audits.
**SMART criteria:**
- Annual security audit (zero critical findings)
- ≥5 upstream contributions per year
- User satisfaction tracked quarterly
- TCO reviewed annually
**Rollback:** N/A (sustained operation)

### 5.1 Timeline caveat

The timeline assumes institutional readiness, funding, and political
support. Universities with limited IT capacity may need 2–3× longer.
The corpus contains only 6 papers on SME adoption, insufficient for
strong conclusions but suggestive that resource-constrained organisations
need bundled, low-operational-burden solutions.

---

## 6. Counter-Evidence and Honest Assessment

### 6.1 Proprietary platforms may improve research productivity

Some studies show that proprietary platforms (Microsoft 365, Google
Workspace) accelerate research productivity through better tooling,
AI integration, and seamless collaboration. The DSW must match or
exceed these capabilities to avoid productivity loss. This is the
strongest counter-argument to migration.

### 6.2 Open-source platforms have lower adoption rates

Open-source collaboration platforms have historically lower adoption
rates than proprietary alternatives, suggesting usability, support,
or ecosystem gaps. The DSW must address these gaps, not assume they
will close automatically.

### 6.3 Self-hosted solutions may have higher TCO

Self-hosting requires IT staffing, infrastructure, and operational
expertise. For small institutions, the TCO of self-hosting may exceed
proprietary SaaS. The DSW must be evaluated on total cost, not just
licence fees.

### 6.4 Data sovereignty regulations can impede collaboration

Strict data sovereignty requirements can create friction in
cross-border research collaboration. The DSW must balance sovereignty
with interoperability.

### 6.5 The corpus itself may be biased

The corpus is skewed towards recent papers (85% from 2025–2026) and
includes auto-ingested, off-topic, and low-quality material. Counts
and trends are indicative, not precise.

---

## 7. Governance and Sustainability

### 7.1 University consortium model

A consortium of universities (e.g., 5–10 institutions) can share:
- Infrastructure costs (shared hosting)
- Development effort (upstream contributions)
- Governance voice (platform roadmap influence)
- Risk (shared operational responsibility)

**Precedents:** GÉANT, eduGAIN, CLARIN, DARIAH, European University
Alliances.

### 7.2 Funding mechanisms

- Institutional IT budgets (reallocated from proprietary licences)
- National research infrastructure funding (e.g., DFG, ANR, UKRI)
- EU funding (Horizon Europe, Digital Europe Programme)
- Consortium membership fees

### 7.3 Vendor and industry role

Vendors are not adversaries. The DSW model includes:
- Commercial support contracts for open-source components
- Industry partnerships for AI and specialised tools
- Transparent procurement with exit clauses

### 7.4 Governance structure

- **Steering committee:** University leadership + IT + faculty + students
- **Technical working group:** IT staff + developers + security
- **User advisory board:** Faculty + students + admin staff
- **Ethics/oversight board:** DPO + legal + equity representatives

---

## 8. Discussion

### 8.1 The sovereignty–capability tension revisited

Through the SWTF lens, the tension is not a binary trade-off but a
**joint optimisation problem**. STST holds that the best solution
optimises both social and technical systems together. The DSW thesis
is that the gap is narrowing (openDesk, Nextcloud, Collabora) but has
not closed. The framework requires evaluating each capability
requirement against each sovereignty dimension, not assuming that
sovereignty implies capability loss or vice versa.

### 8.2 The role of AI

AI is both an opportunity and a risk for DSW. Sovereign AI (self-hosted
LLMs, RAG pipelines) can provide AI assistance without data extraction.
But sovereign AI is 2–3 years behind proprietary (Copilot, Gemini) in
capability. The framework's AI sovereignty dimension (S5) requires
evaluating AI capabilities against data control requirements. The
techno-solutionism guard asks: is AI the right solution, or does it
create new dependencies?

### 8.3 Well-being implications

Digital workplace transitions affect employee well-being through:
change fatigue, skill anxiety, productivity pressure, and digital
surveillance. The framework's equity lens requires evaluating migration
for differential well-being impact. Counter-measures: training, phased
rollout, feedback mechanisms, and psychological safety.

### 8.4 Limitations (updated)

- **No primary data:** All analysis is literature-based.
- **Corpus quality:** Auto-ingested, noisy, skewed to 2025–2026.
- **Cost estimates illustrative:** No empirical TCO studies in corpus.
- **Framework not validated:** The SWTF is proposed, not empirically
  tested.
- **Techno-solutionism guard is procedural:** It asks the right
  questions but cannot guarantee answers.
- **Equity analysis is framework-level:** No empirical equity audit
  conducted.

---

## 9. Conclusion

The Digital Sovereign Workplace for universities is not a technology
procurement decision but a **socio-technical transition** — a
reconfiguration of institutional relationships with digital
infrastructure. The Sovereign Workplace Transition Framework (SWTF)
provides a unified analytical structure integrating socio-technical
systems theory, institutional theory, technology affordance theory, and a
power/equity lens. It reframes the DSW from a product question ("which
platform?") to a transition question ("how does an institution
reconfigure its digital relationships?").

Key contributions:
1. A unified theoretical framework (SWTF) integrating 4 theoretical
   traditions and 11 disciplinary perspectives.
2. Six sovereignty dimensions and six capability requirements as
   evaluation axes.
3. A techno-solutionism guard that questions whether problems are
   technological.
4. Equity as a design principle, not an add-on.
5. A five-phase migration model with SMART criteria and rollback.
6. Explicit engagement with counter-evidence and power dynamics.

The framework is proposed, not validated. Future work must include:
primary stakeholder research, empirical cost studies, equity audits,
and validation of the framework itself.

---

## Part II: Dimensional Analysis

---

## 10. Sovereignty Dimensions in Depth

### 10.1 Data sovereignty (S1)

Data sovereignty concerns where data is stored, who can access it, and
under which jurisdiction. For universities, this is critical for:
research data (GDPR special category, clinical trials, defence),
student records (GDPR), and institutional knowledge.

**Key tensions:** Strict data sovereignty can impede cross-border
collaboration (§6.4). Data classification is prerequisite — not all data
requires sovereign infrastructure.

**Corpus evidence:** 64 papers in data-sovereignty category; 151
sovereign-specific papers across categories. Strong on federated
learning and privacy-preserving computation; weak on practical
deployment guidance.

### 10.2 Software sovereignty (S2)

Software sovereignty is the ability to inspect, modify, and redistribute
the software. Open-source platforms (Nextcloud, Keycloak, Matrix)
provide this; proprietary platforms do not.

**Key tensions:** Software sovereignty requires technical capacity to
audit and modify code. Most universities lack this capacity. "Software
sovereignty" without "capacity sovereignty" is aspirational.

**Corpus evidence:** 305 papers in open-source category. Strong on
open-source development practices; weak on institutional adoption
strategies.

### 10.3 Infrastructure sovereignty (S3)

Infrastructure sovereignty is control over the hosting environment.
Options: on-premises, private cloud, trusted national provider.

**Key tensions:** On-premises requires IT capacity; cloud requires
trust in provider. Gaia-X and European cloud initiatives aim to
provide trusted infrastructure but are immature.

**Corpus evidence:** Limited direct evidence; inferred from cloud
computing and data sovereignty literature.

### 10.4 Identity sovereignty (S4)

Identity sovereignty is control over authentication, authorisation, and
identity data. Keycloak and eduGAIN federation provide sovereign
identity.

**Key tensions:** Federated identity must balance sovereignty with
interoperability. Self-sovereign identity (DID) is research-stage.

**Corpus evidence:** 40 papers in identity-access category. Strong on
federation standards; weak on institutional deployment.

### 10.5 AI sovereignty (S5)

AI sovereignty is control over AI models, training data, and inference
pipelines. Sovereign RAG and self-hosted LLMs provide this.

**Key tensions:** Sovereign AI is 2–3 years behind proprietary in
capability. AI requires significant compute resources. The techno-
solutionism guard asks whether AI is the right solution.

**Corpus evidence:** 280 papers in ai-llm category. Strong on technical
approaches; weak on institutional AI governance.

### 10.6 Governance sovereignty (S6)

Governance sovereignty is institutional control over platform decisions,
roadmap, and policy. Open-source governance (community, foundation)
provides this; proprietary governance (vendor roadmap) does not.

**Key tensions:** Governance sovereignty requires participation capacity.
Institutions must contribute to upstream development to have voice.

**Corpus evidence:** Inferred from open-source governance literature.

---

## 11. Capability Requirements in Depth

### 11.1 Collaboration (C1)

Real-time co-editing, sharing, communication. Proprietary benchmark:
Microsoft 365, Google Workspace. Sovereign alternatives: Nextcloud +
Collabora, Matrix, Jitsi.

**Gap assessment:** Collaboration capabilities are approaching parity
for basic use cases (file sharing, document editing, video calls) but
lag in advanced features (AI-assisted writing, real-time translation,
seamless mobile experience).

### 11.2 Productivity (C2)

Document creation, email, calendar, task management. **Critical gap:
no mature sovereign email solution exists.** This is the single biggest
capability gap in the DSW stack.

### 11.3 Security & compliance (C3)

Encryption, access control, audit, regulatory compliance. Sovereign
platforms can meet GDPR requirements but require institutional
security capacity. Threat model (STRIDE) analysis is needed per
deployment.

### 11.4 Interoperability (C4)

Cross-institution, cross-platform, cross-border data exchange.
Federation standards (eduGAIN, SAML, OIDC, SCIM) are mature but
require institutional participation. Gaia-X data spaces are emerging.

### 11.5 Usability (C5)

Low learning curve, accessibility, multilingual support. **This is
where sovereign platforms lag most.** Consumer-grade UX is a
proprietary strength. Accessibility (WCAG 2.2 AA) must be a minimum,
not a target. Multilingual support is underdeveloped in open-source.

### 11.6 Cost-efficiency (C6)

Sustainable TCO, predictable costs, no vendor lock-in. Self-hosting
requires IT staffing and infrastructure. For small institutions, TCO
may exceed proprietary SaaS. Consortium models (shared hosting) can
reduce per-institution costs.

---

## 12. Institutional Embeddedness

### 12.1 Legal and regulatory framework

**GDPR implementation:** Data location, access control, and
processing agreements. Sovereign platforms can satisfy GDPR but
require institutional legal capacity.

**Legal definition of sovereignty:** Technical sovereignty (control
over infrastructure) vs. legal sovereignty (jurisdictional authority)
vs. political sovereignty (self-determination). The DSW addresses
technical sovereignty; legal and political sovereignty require
institutional and governmental action.

**Public procurement law:** EU procurement rules may favour incumbent
vendors. Sovereign consortia must navigate competitive tendering.

**Academic freedom:** Statutory obligation to protect academic
freedom. Platform mediation can compromise this.

**EU AI Act:** Implications for AI-assisted workplace tools. Sovereign
AI must comply with AI Act requirements.

### 12.2 Economic analysis

**TCO framework:** Licence fees + infrastructure + staffing +
training + migration + opportunity cost. Sovereign platforms may have
lower licence fees but higher staffing costs.

**Platform market economics:** Network effects favour incumbent
platforms. Sovereign platforms must overcome these through
consortium coordination and standardisation.

**Public goods analysis:** Digital infrastructure is a public good.
Market failure justifies public investment in sovereign alternatives.

**Market failure analysis:** Vendor lock-in, data extraction, and
switching costs create market failures that sovereign platforms
address.

**Incentive analysis:** Upstream contribution incentives. Institutions
must contribute to open-source development to sustain the ecosystem.

### 12.3 Higher education policy

**Open science infrastructure:** Integration with institutional
repositories, open access mandates, and FAIR data principles.

**Research assessment reform:** CoARA/DORA implications for digital
infrastructure. Research assessment should not depend on proprietary
platforms.

**Teaching and learning:** EdTech integration, learning management
systems, student data rights.

### 12.4 Public policy and international dimensions

**Policy landscape:** National digital sovereignty initiatives (France's
 DINUM, Germany's Sovereign Cloud, EU Gaia-X).

**Policy instruments:** Funding, procurement preferences, standards,
regulation.

**Sovereignty levels:** Institutional, national, European, global.
These interact — institutional sovereignty depends on national and
European frameworks.

**International dimensions:** Cross-border data flows, extraterritorial
legislation (CLOUD Act), geopolitical risk.

---

## 13. Equity and Inclusion (Design Principle)

### 13.1 Accessibility (disability studies)

WCAG 2.2 AA is a minimum. Sovereign platforms must be evaluated for:
screen reader compatibility, keyboard navigation, cognitive load,
alternative input methods. If a sovereign platform is less accessible
than its proprietary counterpart, migration reduces equity.

### 13.2 Gender and intersectionality (feminist studies)

Platform design encodes gendered assumptions (always-on collaboration,
productivity surveillance). DSW must be evaluated for differential
impact on caregivers, part-time staff, and marginalised groups.

### 13.3 Indigenous data sovereignty (CARE principles)

For universities with indigenous research partnerships, data sovereignty
extends to community control. DSW must support CARE (Collective benefit,
Authority to control, Responsibility, Ethics) alongside FAIR.

### 13.4 Digital divide

Not all users have equal connectivity, devices, or digital literacy.
Sovereign platforms that assume high bandwidth or technical
sophistication may exclude. Offline capability and low-bandwidth
modes are needed.

---

## Part III: Transition Pathway, Governance, and Evaluation

---

## 14. Migration Model (Five Phases)

(Detailed in §5 with SMART criteria, rollback scenarios, and
techno-solutionism guard.)

The migration model is reframed through the SWTF as an **adaptive
transition**, not a linear deployment:

- **Feedback loops:** Each phase generates evidence that reshapes
  subsequent phases.
- **Rollback triggers:** Explicit criteria for reverting decisions.
- **Learning mechanisms:** Post-implementation reviews, user feedback,
  metrics tracking.
- **Equity checkpoints:** Each phase includes equity audit.

### 14.1 Change management (Kotter + ADKAR)

- Kotter's 8-step model for organisational change.
- ADKAR (Awareness, Desire, Knowledge, Ability, Reinforcement) for
  individual change.
- Resistance management plan.
- Leadership sponsorship and succession.
- Organisational learning mechanisms.

### 14.2 Organisational culture analysis

Culture shapes platform adoption. Universities have distinct cultures
(collegial, bureaucratic, entrepreneurial) that interact differently
with sovereign platforms. Culture change is prerequisite, not
consequence, of migration.

---

## 15. Governance and Sustainability

(Detailed in §7.)

### 15.1 Consortium model

Shared infrastructure, development, governance, and risk. Precedents:
GÉANT, eduGAIN, CLARIN, DARIAH.

### 15.2 Funding mechanisms

Institutional budgets, national research infrastructure, EU funding,
consortium fees.

### 15.3 Vendor and industry role

Commercial support, industry partnerships, transparent procurement.

### 15.4 Governance structure

Steering committee, technical working group, user advisory board,
ethics/oversight board.

---

## 16. Evaluation Framework

### 16.1 Success metrics (by dimension)

| Dimension | Metric | Target |
|-----------|--------|--------|
| S1 Data sovereignty | % data in sovereign infrastructure | ≥80% by Phase 4 |
| S2 Software sovereignty | % open-source components | ≥90% by Phase 4 |
| S3 Infrastructure sovereignty | % self-hosted or trusted-provider | ≥70% by Phase 4 |
| S4 Identity sovereignty | Federated identity coverage | ≥95% by Phase 3 |
| S5 AI sovereignty | % AI processing on sovereign infra | ≥50% by Phase 5 |
| S6 Governance sovereignty | Consortium participation | Active by Phase 3 |
| C1 Collaboration | User satisfaction | ≥75% |
| C2 Productivity | Task completion time | ≤ baseline + 10% |
| C3 Security | Critical incidents | Zero |
| C4 Interoperability | Cross-institution functions | ≥3 institutions |
| C5 Usability | SUS score | ≥68 (above average) |
| C6 Cost | TCO vs. baseline | ≤ 110% of baseline |

### 16.2 DeLone & McLean IS success model

Applied to evaluate DSW success: system quality, information quality,
service quality, use, user satisfaction, net benefits.

### 16.3 Equity audit

Each phase includes an equity audit evaluating differential impact
across user groups (disability, gender, indigenous, digital divide).

---

## Part IV: Synthesis, Tensions, and Research Agenda

---

## 17. Cross-Disciplinary Synthesis

### 17.1 How the SWTF integrates the perspectives

The framework resolves the fragmentation problem by providing shared
constructs (sovereignty dimensions, capability requirements, analytical
levels) that all disciplines can use. Each discipline's contribution
becomes a lens applied through the framework, not a separate section.

### 17.2 Cross-disciplinary interaction matrix

| Interaction | Description |
|-------------|-------------|
| IS × CS | Architecture must serve organisational needs, not just technical ideals |
| IS × Law | Governance must comply with regulatory frameworks |
| IS × Economics | IT decisions must be economically sustainable |
| CS × Law | Technical controls must implement legal requirements |
| CS × Economics | Security investments must be cost-justified |
| Law × Economics | Compliance costs must be economically viable |
| All × Equity | Every decision evaluated for differential impact |

### 17.3 Remaining limitations

- Framework not empirically validated.
- Equity analysis is framework-level, not audited.
- Cost estimates illustrative.
- Corpus quality issues.
- No primary data.

---

## 18. Counter-Evidence and Honest Assessment

(See §6 for full counter-evidence. Summary:)

1. Proprietary platforms may improve research productivity.
2. Open-source platforms have lower adoption rates.
3. Self-hosted solutions may have higher TCO.
4. Data sovereignty regulations can impede collaboration.
5. The corpus itself may be biased.

The SWTF requires engaging with counter-evidence at each phase, not
just in a dedicated section. Counter-evidence is integrated into the
sovereignty dimensions (§10) and capability requirements (§11).

---

## 19. Research Agenda

### 19.1 Immediate (0–12 months)

- Validate the SWTF through expert review and case studies.
- Conduct primary stakeholder research (interviews, surveys).
- Develop empirical TCO models.
- Commission accessibility audit of sovereign platforms.

### 19.2 Medium-term (1–3 years)

- Pilot DSW in 2–3 universities.
- Measure sovereignty and capability metrics.
- Evaluate equity impact.
- Refine the framework based on evidence.

### 19.3 Long-term (3–5 years)

- Scale to consortium model.
- Contribute to open-source ecosystem.
- Influence policy (procurement, funding).
- Publish validated framework.

---

## 20. References

### Key theoretical works

- Trist, E. L. & Bamforth, K. W. (1951). Some social and psychological
  consequences of the longwall method of coal-getting. *Human Relations*.
- Cherns, A. (1976). The principles of sociotechnical design. *Human
  Relations*.
- Bostrom, R. P. & Heinen, J. S. (1977). MIS problems and failures: A
  socio-technical perspective. *MIS Quarterly*.
- DiMaggio, P. J. & Powell, W. W. (1983). The iron cage revisited:
  Institutional isomorphism and collective rationality. *American
  Sociological Review*.
- Scott, W. R. (2014). *Institutions and Organizations*. Sage.
- Gibson, J. J. (1979). *The Ecological Approach to Visual Perception*.
- Norman, D. A. (1988). *The Design of Everyday Things*. Basic Books.
- Leonardi, P. M. (2011). When flexible routines meet flexible
  technologies. *MIS Quarterly*.
- Faraj, S. & Azad, B. (2012). The materiality of technology. In
  *Materiality and Organizing*. Oxford University Press.
- Haraway, D. (1988). Situated knowledges. *Feminist Studies*.
- Wajcman, J. (2004). *TechnoFeminism*. Polity.
- Shakespeare, T. (2014). *Disability Rights and Wrongs Revisited*.
  Routledge.
- Carroll, S. R. et al. (2020). The CARE principles for indigenous data
  governance. *Data Science Journal*.
- Morozov, E. (2013). *To Save Everything, Click Here*. PublicAffairs.
- Feenberg, A. (2010). *Between Reason and Experience*. MIT Press.

### Corpus streams (paper counts)

- Open Source: 305
- AI & Language Models: 280
- Employee Well-being: 261
- Adoption & Change: 252
- Interoperability & Standards: 238
- Surveys & Reviews: 221
- Evaluation & Case Studies: 204
- Methods: 195
- Hybrid & Remote Work: 183
- Tooling & Platforms: 179
- Public Sector & Education: 154
- Digital Transformation: 130
- Federated & Privacy-Preserving: 101
- Collaboration & Productivity: 79
- Data Sovereignty: 64
- Security & Compliance: 48
- Identity & Access: 40
- Digital Workplace: 27
- SME Adoption: 6

**Total corpus: 3,030 papers across 19 categories.**
