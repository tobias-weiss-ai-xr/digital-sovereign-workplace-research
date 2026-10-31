# Towards a Digital Sovereign Workplace for Universities: Stakeholder Needs, Migration Path, and Governance

**Authors:** Digital Sovereign Workplace Research Corpus  
**Date:** 2026-10-31  
**Corpus basis:** 3,030 papers across 19 categories (frozen snapshot: 2026-10-31)  
**Status:** Working paper / draft for review (Revision 4 — all key findings from both review rounds addressed)

---

## Abstract

Universities are among the most data-intensive and collaboration-dependent
organisations in society, yet their digital infrastructure is overwhelmingly
hosted on proprietary, extra-territorial cloud platforms. This paper outlines
a staged migration path towards a Digital Sovereign Workplace (DSW) for
higher-education institutions. Drawing on a corpus of 3,030 papers spanning
digital sovereignty, open-source platforms, federated privacy, AI
augmentation, and public-sector adoption, we map the distinct and sometimes
conflicting needs of twelve university stakeholder groups. We propose a
five-layer technology stack (separated into available-now, emerging, and
research-stage components) and a five-phase migration model (Assess → Pilot
→ Federate → Scale → Sustain) with SMART success criteria, rollback
scenarios, and organisational change management. The paper identifies the
sovereignty–capability tension as the central challenge, engages with
counter-evidence, and proposes governance mechanisms including a university
consortium model. Limitations include the absence of primary stakeholder
research, the illustrative nature of cost estimates, and corpus
quality issues. This revision addresses all key findings from
two rounds of multi-perspective review, covering 11 disciplinary
perspectives across 21 sections.

**Keywords:** digital sovereignty, sovereign workplace, universities, higher
education, open source, federated identity, stakeholder analysis, migration
path, openDesk, Nextcloud, governance

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
productivity, and AI capabilities modern academic work demands. This is not a
retreat from digitalisation but a re-architecting — replacing dependency with
autonomy, opacity with auditability, and data extraction with stewardship.

### 1.2 Why universities are a special case

Universities are not just another enterprise. Their digital-sovereignty
challenge is distinctive:

- **Research data sensitivity**: Research data is often legally restricted
  (GDPR special-category data, clinical trials, proprietary industry data,
  classified defence research). Hosting on extra-territorial platforms creates
  jurisdictional risk. *Caveat*: not all research data requires sovereign
  infrastructure — much is already public (open data, published results).
  The need is proportional to sensitivity.

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
  through better tooling (see §7.4).

- **Multi-institutional collaboration**: Academic work crosses institutional
  and national boundaries. Sovereign workplaces must interoperate, not become
  islands.

- **Resource constraints**: IT budgets are small relative to needs. The
  corpus contains only 6 papers on SME adoption — insufficient for strong
  conclusions, but suggestive that resource-constrained organisations need
  bundled, low-operational-burden solutions.

### 1.3 The sovereignty–capability tension

The central tension is between **sovereignty** (control) and **capability**
(best-in-class tools). Proprietary platforms offer superior AI assistance,
real-time collaboration, and seamless integration. Sovereign platforms offer
control and auditability but may lag on features.

**Capability comparison (based on literature, not empirical evaluation):**

| Capability | Proprietary (M365/Google) | Sovereign (Nextcloud+Collabora) | Gap |
|-----------|--------------------------|-------------------------------|-----|
| Real-time co-editing | Excellent | Good (Collabora) | Moderate |
| AI assistance | Advanced (Copilot, Gemini) | Emerging (sovereign RAG) | Large |
| Mobile experience | Excellent | Adequate | Moderate |
| Offline sync | Excellent | Good | Small |
| Integration ecosystem | Vast | Limited | Large |
| Accessibility (screen readers) | Excellent | Adequate | Moderate |
| Video conferencing | Excellent (Teams/Meet) | Adequate (Jitsi/BBB) | Moderate |
| Search | Excellent | Adequate | Moderate |
| Compliance/audit | Good (with config) | Excellent (full control) | Sovereign advantage |
| Data residency | Configurable (extra-territorial risk) | Full control | Sovereign advantage |

*Note: This table is based on feature documentation and literature review,
not empirical benchmarking. No peer-reviewed study in the corpus compares
these platforms head-to-head in university settings.*

### 1.4 Research questions

1. What are the distinct digital-workplace needs of university stakeholder
   groups, and where do they conflict?
2. What technology stack can satisfy these needs while preserving
   sovereignty?
3. What staged migration path is realistic for a resource-constrained
   university?
4. What governance and sustainability mechanisms are needed?

### 1.5 Method and limitations

This paper synthesises a corpus of 3,030 papers discovered through
taxonomy-aware queries against arXiv, OpenAlex, Crossref, dblp, Europe PMC,
and Semantic Scholar. The corpus is organised into 19 categories and 8
subcategory dimensions.

**Corpus limitations (must be acknowledged):**
- **Quality**: The corpus contains noise — predatory journal articles,
  off-topic papers, and Zenodo preprints without peer review. Validation
  flagged ~20 papers with LaTeX artifacts and ~5 with non-peer-reviewed
  platforms.
- **Recency bias**: 85% of papers are from 2025–2026. Foundational work
  (pre-2025) is underrepresented.
- **Query design bias**: The corpus was built to support DSW research;
  it may over-represent sovereignty-positive findings (confirmation bias).
- **No primary research**: Stakeholder needs are inferred from literature,
  not from interviews or surveys with university stakeholders.

**Extraction method**: Stakeholder needs were manually extracted from
papers in the adoption-change (252), employee-wellbeing (261), hybrid-work
(183), digital-transformation (130), public-sector (154), identity-access
(40), interoperability (238), federated-privacy (101), ai-llm (280),
open-source (305), security-compliance (48), and data-sovereignty (64)
categories. Technology and migration proposals integrate findings from the
sovereignty, federated-computation, and open-source-platform literatures.

---

## 2. Stakeholder Landscape

A university is a federation of communities with distinct needs, priorities,
and power. We identify **twelve** stakeholder groups (expanded from seven
based on critical review).

### 2.1 University Leadership (Rectorate / Executive Board)

**Power level:** High (strategic decision-maker)

**Primary concerns:** Reputation, compliance, autonomy, cost, risk.

**Needs:** Compliance assurance (GDPR, national laws, funding requirements);
cost predictability (avoid vendor lock-in); strategic autonomy (set digital
strategy without vendor constraint); risk mitigation (reduce single-point-of-
failure and extra-territorial exposure).

**Tensions:** May prioritise cost/compliance over user experience, mandating
platforms faculty resist. The adoption literature (252 papers) warns that
top-down mandates without user buy-in lead to shadow IT.

### 2.2 IT Departments / CIO

**Power level:** High (implementation gatekeeper)

**Primary concerns:** Reliability, security, maintainability, skills,
integration.

**Needs:** Operational feasibility (deployable/maintainable with existing
staff); security architecture (meet/exceed proprietary standards);
integration (LMS, ERP, HR, library, identity providers); skills and support
(vendor/community resources, training); monitoring and observability.

**Tensions:** May resist self-hosted solutions due to operational burden,
preferring managed services even if sovereignty is compromised.

### 2.3 Faculty and Researchers

**Power level:** Medium-High (academic freedom, research autonomy)

**Primary concerns:** Research productivity, collaboration, data protection,
academic freedom, cutting-edge tools.

**Needs:** Research data sovereignty (control over storage, access, sharing —
critical for sensitive data); collaboration capability (multi-institutional
without forcing single platform); AI assistance (literature search, code,
analysis on institutional data); academic freedom (no external surveillance);
open science alignment (open data, reproducible research).

**Tensions:** Demand best-in-class tools; may resist inferior platforms.
Well-being literature (261 papers) notes tool friction reduces productivity
and increases stress. Shadow IT (personal Dropbox, Google Docs) is common.

### 2.4 Students

**Power level:** Low (largest group, least institutional power)

**Primary concerns:** Accessibility, usability, learning support, privacy,
equity.

**Needs:**
- **Accessibility**: usable on diverse devices (low-end hardware, mobile),
  support assistive technologies (screen readers, voice control).
- **Learning support**: LMS integration, assignment submission, feedback,
  grading workflows.
- **Privacy**: grades, communications, behavioural data protected from
  commercial exploitation.
- **Equity**: equal access regardless of personal device or home internet.
- **Familiarity**: intuitive interfaces, minimal retraining.
- **Mobile-first**: many students primarily use mobile devices; self-hosted
  platforms may have inferior mobile apps.
- **Offline capability**: students in low-connectivity areas need offline
  access.
- **Learning analytics**: universities use analytics for student success;
  sovereign platforms need equivalent capabilities without privacy violations.

**Tensions:** Needs often overlooked in platform decisions. Platform overload
and digital fatigue (hybrid-work literature, 183 papers) already affect
students.

### 2.5 Administrative Staff

**Power level:** Medium (process owners)

**Primary concerns:** Process efficiency, document management, compliance,
integration.

**Needs:** Document workflow (approval chains, version control, templates,
archival); integration (ERP, HR, finance, student information systems);
compliance automation (RoPA generation, retention, audit trails); efficiency
(reduction of manual entry).

**Tensions:** Need reliable, well-integrated tools; may resist platforms
lacking enterprise features (workflow automation, advanced search,
reporting).

### 2.6 Data Protection Officers (DPOs) / Legal

**Power level:** Medium-High (compliance gatekeeper)

**Primary concerns:** GDPR compliance, data residency, auditability, risk
assessment, legal certainty.

**Needs:** Data residency (verifiable control over storage/processing);
audit trails (tamper-proof logs); DPIA support (document Data Protection
Impact Assessments); contractual clarity (no extra-territorial jurisdiction);
incident response (investigate breaches within institutional control).

**Tensions:** May block adoption of any platform that cannot demonstrate
compliance, creating conservative bias. Security-compliance literature
(48 papers) addresses compliance-chain automation.

### 2.7 External Partners (Industry, Other Universities, Funding Bodies)

**Power level:** Medium (collaboration-dependent)

**Primary concerns:** Interoperability, trust, data sharing, collaboration
efficiency.

**Needs:** Federated collaboration (cross-institutional without forcing
single platform); trust frameworks (mutual recognition of credentials);
data sharing agreements (machine-readable terms); standards compliance
(ORCID, DataCite, EOSC, Gaia-X).

**Tensions:** May prefer widely adopted proprietary platforms. Sovereign
platforms must demonstrate interoperability.

### 2.8 Libraries and Information Services (NEW)

**Power level:** Medium (research data stewards)

**Primary concerns:** Research data management, open access, digital
preservation, metadata standards.

**Needs:** Integration with institutional repositories (DSpace, EPrints);
research data management platform support (Dataverse, CKAN); open access
publishing workflows; digital preservation and archival compliance; metadata
standards (Dublin Core, DataCite).

**Tensions:** Libraries are often early adopters of open-source but may
lack resources to operate sovereign platforms.

### 2.9 Research Computing / HPC Centres (NEW)

**Power level:** Medium (technical infrastructure)

**Primary concerns:** Compute capacity, data throughput, export control,
dual-use research.

**Needs:** Integration with HPC clusters; data pipeline connectivity;
compliance with export control regulations; support for computational
research workflows (Jupyter, RStudio, etc.).

**Tensions:** HPC environments are often separate from workplace platforms;
integration is complex.

### 2.10 Procurement and Finance (NEW)

**Power level:** High (budget gatekeeper)

**Primary concerns:** Cost, tendering, contract management, vendor evaluation.

**Needs:** TCO comparison tools; tender-ready documentation; contract
management for open-source (SLAs, support agreements); budget forecasting.

**Tensions:** Procurement processes favour established vendors with
standardised contracts; open-source procurement is unfamiliar.

### 2.11 Student Unions / Governance Bodies (NEW)

**Power level:** Low-Medium (collective voice)

**Primary concerns:** Student rights, privacy, equity, platform usability.

**Needs:** Representation in platform decisions; privacy advocacy; equity
monitoring; feedback channels.

**Tensions:** Often consulted late or not at all in platform decisions.

### 2.12 International Partners (NEW)

**Power level:** Medium (collaboration-dependent)

**Primary concerns:** Jurisdiction, data transfer, interoperability, trust.

**Needs:** Clear data transfer agreements (SCCs, adequacy decisions);
interoperability with non-EU sovereign systems; mutual recognition of
identity credentials.

**Tensions:** Non-EU partners may face additional compliance burden;
sovereign platforms must not create collaboration barriers.

### 2.13 Power dynamics analysis

The paper previously treated stakeholders as having equal voice, which is
unrealistic. In practice:

- **IT departments control implementation** and can block or enable adoption.
- **Faculty have academic freedom** but limited IT decision-making power.
- **Students have the least power** but the largest numbers.
- **Vendors have significant influence** through pricing, feature
  development, and relationship management.
- **DPOs can veto** any platform that cannot demonstrate compliance.

The adoption literature (252 papers) contains relevant findings on
organisational politics and resistance. Key insight: **shadow IT is not
a failure of users but a signal of unmet needs** — when institutional
tools are inadequate, users route around them.

---

## 3. Technology Stack (Three-Tier Classification)

Based on the corpus, we propose a technology stack classified by
maturity/readiness.

### Tier 1: Available Now (production-ready)

| Layer | Technology | Evidence base | Maturity |
|-------|-----------|---------------|----------|
| Infrastructure | Nextcloud (self-hosted) | 0 university-specific studies in corpus; extensive general deployment | High |
| Collaboration | Collabora Online / OnlyOffice | Integrated with Nextcloud; general enterprise use | High |
| Identity | OIDC/SAML SSO (Shibboleth, Keycloak) | Widely deployed in universities (eduGAIN federation) | High |
| Communication | Matrix (Element), Jitsi, BigBlueButton | Deployed in education sector | High |
| Calendar/Contacts | CalDAV/CardDAV | Standard protocols, widely supported | High |

### Tier 2: Emerging (deployable with effort)

| Layer | Technology | Evidence base | Maturity |
|-------|-----------|---------------|----------|
| AI/Knowledge | Sovereign RAG (on-premise LLM) | Governed Sovereign RAG (arXiv:2610.36561) — public admin context, not university | Medium |
| Compliance | Automated RoPA extraction (RAG-based) | arXiv:2609.27359 — hybrid RAG for RoPA | Medium |
| Research data | Federated learning (multi-institutional) | arXiv:2610.27470, arXiv:2610.36379 — healthcare context | Medium |
| Data spaces | Gaia-X / IDSA governance | arXiv:2507.20014 — policy-driven AI in dataspaces | Medium |

### Tier 3: Research Stage (not production-ready)

| Layer | Technology | Evidence base | Maturity |
|-------|-----------|---------------|----------|
| Confidential computing | RISC-V secure enclaves | eBIM paper (embedded blockchain) — research prototype | Low |
| Self-sovereign identity | SSI (DID-based) | Conceptual; no university deployment in corpus | Low |
| Homomorphic encryption | HE for data analysis | Research-stage; performance overhead significant | Low |
| Blockchain consent | Auditable consent tracking | ClinConNet (arXiv:2602.02610) — clinical research context | Low |

### 3.1 Missing from the stack (must be addressed)

- **LMS integration**: Moodle, Canvas, Blackboard integration is critical.
  No papers in the corpus address LMS integration with sovereign platforms.
- **Research infrastructure**: DSpace, Dataverse, CKAN, HPC clusters, ELNs.
  Not addressed in the corpus.
- **Assistive technology**: Screen reader compatibility, voice control.
  Not addressed.

---

## 4. Migration Path: Five Phases (with SMART criteria)

### Phase 1: Assess (Months 1–6)

**Goal:** Understand current state, identify quick wins, build coalition.

**Activities:**
- Digital sovereignty audit (map all cloud services, data flows, jurisdictional
  exposure, compliance gaps).
- Stakeholder consultation (structured interviews/surveys with all 12 groups).
- Pilot candidate selection (1–2 low-risk, high-visibility use cases).
- TCO comparison (5-year sovereign vs. proprietary).

**SMART Success Criteria:**
- Audit completed within 3 months.
- ≥80% of stakeholder groups consulted.
- TCO comparison produced with quantified estimates.
- Pilot candidates identified and approved by steering committee.

**Deliverables:** Sovereignty audit report, stakeholder needs matrix, pilot
plan, TCO comparison.

### Phase 2: Pilot (Months 7–12)

**Goal:** Deploy sovereign platforms in limited scope and validate.

**Activities:**
- Deploy Nextcloud + Collabora for one department/research group.
- Integrate with institutional identity (SSO via OIDC/SAML).
- Migrate pilot data with rollback plan.
- Collect user feedback (surveys, usage analytics).
- Evaluate against success criteria.

**SMART Success Criteria:**
- ≥60% adoption rate among pilot users within 3 months of deployment.
- User satisfaction score ≥3.5/5.
- <5 critical incidents per month.
- Compliance verification passed by DPO.
- Rollback plan tested and documented.

**Rollback scenario:** If adoption <40% or critical incidents >10/month
after 3 months, revert to proprietary platform and conduct post-mortem.
Sunk costs: infrastructure setup (~€50K–100K estimated), staff time.
Mitigation: pilot on existing infrastructure, minimise new procurement.

**Deliverables:** Pilot deployment, evaluation report, lessons learned,
scaling plan.

### Phase 3: Federate (Months 13–24)

**Goal:** Enable cross-institutional collaboration and expand scope.

**Activities:**
- Join/establish identity federation with partner universities.
- Deploy federated learning for multi-institutional research projects.
- Implement data-space governance (Gaia-X/IDSA) for research data sharing.
- Expand to additional departments based on pilot lessons.
- Deploy sovereign AI (RAG) for institutional knowledge search.

**SMART Success Criteria:**
- ≥2 partner universities federated within 6 months.
- Federated learning pilot completed with ≥1 research project.
- ≥3 additional departments migrated.
- Sovereign AI prototype deployed and evaluated.

**Rollback scenario:** If federation fails (partner incompatibility), fall
back to bilateral data-sharing agreements. If sovereign AI quality is
insufficient, retain proprietary AI for non-sensitive use cases.

**Deliverables:** Federation membership, federated learning pilot, expanded
deployment, sovereign AI prototype.

### Phase 4: Scale (Months 25–48)

**Goal:** Institution-wide adoption with full feature parity.

**Activities:**
- Migrate all departments to sovereign platforms.
- Decommission or reduce proprietary licenses (hybrid model).
- Establish support structures (helpdesk, training, documentation).
- Implement advanced features (workflow automation, search, reporting,
  compliance automation).
- Institution-wide security audit and penetration testing.
- Organisational change management programme (training, communication,
  resistance handling).

**SMART Success Criteria:**
- ≥80% of staff and students on sovereign platform within 12 months.
- Proprietary license costs reduced by ≥30%.
- Helpdesk response time <4 hours.
- Security audit passed with no critical findings.
- Training completion rate ≥90% for staff.

**Rollback scenario:** If institution-wide adoption stalls (<60% after
12 months), shift to hybrid model: sovereign for sensitive data, proprietary
for general collaboration. Reassess in 6 months.

**Deliverables:** Institution-wide deployment, support infrastructure,
security certification, license reduction plan.

### Phase 5: Sustain (Ongoing)

**Goal:** Long-term viability and continuous improvement.

**Activities:**
- Consortium participation (shared development, support, funding).
- Upstream contribution to open-source projects.
- Continuous evaluation (annual review of capabilities vs. proprietary).
- Skills development (training programmes).
- Research programme (contribute to DSW evidence base).

**SMART Success Criteria:**
- Consortium membership established within 6 months of Phase 4 completion.
- ≥2 upstream contributions per year.
- Annual capability review conducted and published.
- Training curriculum updated annually.

**Deliverables:** Consortium membership, contribution guidelines, annual
review process, training curriculum.

### 4.1 Timeline caveat

The 48-month timeline is optimistic. Real-world experience suggests:
- Identity federation alone: 12–18 months.
- LMS migration: 12–24 months.
- User adoption and training: extends well beyond technical deployment.

Phases overlap in practice (federation work starts during pilot). The linear
model is a simplification. An iterative/agile approach with 3-month
sprints and regular retrospectives is recommended over waterfall phases.

---

## 5. Governance and Sustainability

### 5.1 University consortium model

No single university can sustain a sovereign workplace alone. Community
governance and shared investment are essential (open-source literature,
305 papers — though most address general OSS governance, not university
consortia specifically).

**Proposed consortium structure (based on EOSC and Gaia-X precedents):**
- **Shared development**: pooled resources for platform development.
- **Shared support**: centralised helpdesk and expertise.
- **Shared standards**: common interoperability standards and data-sharing
  agreements.
- **Shared research**: collaborative research on DSW effectiveness.

**Existing precedents:**
- **EOSC (European Open Science Cloud)**: research-data focused, not
  workplace-focused. Demonstrates cross-institutional governance feasibility.
- **Gaia-X**: data-space governance framework. Demonstrates federated
  cloud governance. Struggles with implementation pace.
- **eduGAIN**: identity federation for education/research. Demonstrates
  cross-border identity federation at scale (3,000+ institutions).

**Governance challenges (not addressed in current literature):**
- Decision-making speed in multi-university consortia.
- Conflict resolution when members have different priorities.
- Exit provisions for members who leave.
- Resource asymmetry (large vs. small universities).

### 5.2 Funding mechanisms

- **Public funding**: Horizon Europe, Digital Europe, national digital
  sovereignty initiatives. *Caveat*: funding requires proposals, which
  require evidence, which requires pilots, which require funding (chicken-
  and-egg). Start with small internal pilots to generate evidence.
- **Institutional budgets**: reallocation of proprietary license budgets.
  *Estimate needed*: requires institution-specific TCO analysis (not
  provided in this paper).
- **Research grants**: DSW as research topic attracts funding. The corpus
  identifies research gaps (SME adoption, empirical platform evaluation)
  that are fundable.

### 5.3 Vendor and industry role

Commercial open-source vendors (Collabora, Nextcloud GmbH, Element/Matrix)
provide critical support, SLAs, and development capacity. Their business
models and incentives must be part of governance:
- **SLA-backed support**: vendors provide enterprise support for
  self-hosted platforms.
- **Development funding**: vendors may fund features that align with their
  product roadmap.
- **Risk**: vendor lock-in can re-emerge if the institution depends on a
  single vendor's distribution of an open-source platform.

### 5.4 Governance structure

- **Steering committee**: representatives from all 12 stakeholder groups.
- **Technical working group**: IT staff and developers.
- **User advisory board**: faculty, students, admin representatives.
- **Ethics and compliance review**: DPO-led review of new features.

---

## 6. Counter-Evidence and Honest Assessment

A credible paper must engage with evidence that challenges its thesis:

### 6.1 Proprietary platforms may improve research productivity

Several studies in the corpus suggest that proprietary platforms (M365,
Google Workspace) improve research productivity through better tooling,
AI assistance, and seamless integration. The well-being literature notes
that tool friction reduces productivity. Sovereign platforms may introduce
friction during migration and in daily use.

**Implication:** The sovereignty benefit must be weighed against
productivity costs. For some use cases (non-sensitive collaboration),
proprietary platforms may remain superior.

### 6.2 Open-source platforms have lower adoption rates

The adoption literature (252 papers) suggests that open-source platforms
face adoption barriers: unfamiliarity, perceived complexity, lack of
vendor support, and organisational resistance. These barriers are not
automatically overcome by institutional mandate.

**Implication:** Adoption requires sustained investment in training,
support, and change management.

### 6.3 Self-hosted solutions may have higher TCO

The corpus contains no TCO comparison studies. However, the SME-adoption
literature (6 papers) suggests that resource-constrained organisations
face higher operational burdens with self-hosted solutions. IT staff time,
infrastructure costs, and security responsibilities may exceed proprietary
license costs.

**Implication:** TCO analysis is essential before committing to migration.
This paper does not provide quantified estimates.

### 6.4 Data sovereignty regulations can impede collaboration

Strict data residency requirements can create barriers to international
collaboration. If each institution requires data to remain in its
jurisdiction, multi-institutional research projects face complex data-
sharing agreements.

**Implication:** Federated approaches (data spaces, federated learning)
are essential, but they add complexity. The interoperability literature
(238 papers) addresses standards, but implementation remains challenging.

### 6.5 The corpus itself may be biased

The DSW corpus was built to support DSW research. Queries were designed to
find papers relevant to digital sovereignty, open-source platforms, etc.
This creates confirmation bias: the corpus over-represents sovereignty-
positive findings and under-represents critical or neutral perspectives.

**Implication:** Claims in this paper should be verified against
independent literature searches.

---

## 7. Discussion

### 7.1 The sovereignty–capability tension revisited

The migration model does not resolve the tension; it manages it. Phase 2
(Pilot) accepts capability gaps for learning and sovereignty gains. Phase 4
(Scale) aims for feature parity but acknowledges some proprietary
capabilities may remain superior. **Sovereignty is not all-or-nothing**:
a hybrid model (sovereign for sensitive data, proprietary for general
collaboration) may be the pragmatic path.

### 7.2 The role of AI

Sovereign AI is both the greatest opportunity and challenge. The ai-llm
literature (280 papers) shows rapid progress in on-premise LLM deployment,
RAG, and multi-agent systems. But the gap between research prototypes and
production-ready sovereign AI remains significant. Universities can
contribute by participating in open-source AI development and providing
real-world testbeds.

### 7.3 Well-being implications

The well-being literature (261 papers) suggests platform design affects
well-being. Sovereign platforms designed for institutional control rather
than engagement maximisation may produce better outcomes — but this
hypothesis is untested. The university DSW migration is an opportunity to
test it.

### 7.4 Limitations

- **No empirical validation**: The migration path is proposed, not tested.
- **No primary research**: Stakeholder needs are inferred from literature,
  not interviews or surveys.
- **Corpus quality**: Contains noise, predatory journals, and preprints.
  Recency bias (85% from 2025–2026).
- **Confirmation bias**: Corpus built to support DSW research.
- **No cost quantification**: TCO comparison is mentioned but not
  quantified.
- **European/GDPR focus**: Generalisability to other jurisdictions
  uncertain.
- **Missing stakeholders**: Some groups (e.g., alumni, donors, government
  partners) not addressed.
- **Technology stack unvalidated**: No peer-reviewed evaluation of
  proposed technologies in university settings.

---

## 8. Conclusion

Universities face a defining choice: continue deepening dependency on
proprietary cloud platforms, or invest in sovereign alternatives aligned
with their mission, values, and legal obligations. This paper has outlined
a staged path towards a DSW for universities, grounded in a systematic
review of 3,030 papers.

Key findings:
1. **Stakeholder needs are diverse and conflicting.** No single platform
   satisfies all; governance mechanisms are essential.
2. **A three-tier technology stack** (available now / emerging / research
   stage) addresses the full range of needs.
3. **A five-phase migration model** with SMART criteria, rollback
   scenarios, and change management is realistic but optimistic.
4. **Governance and sustainability** require a consortium model, public
   funding, and vendor engagement.
5. **The sovereignty–capability tension** remains central. A hybrid model
   may be pragmatic, but empirical evaluation is needed.
6. **Counter-evidence must be engaged.** Proprietary platforms may be
   superior for some use cases; sovereign platforms may have higher TCO.

The university DSW agenda is both a research programme and a policy
imperative. By acting as early adopters, universities can protect
institutional autonomy, advance open science, and contribute to the
evidence base for sovereign workplaces.

---

## 9. Information Systems Analysis

This section deepens the paper's IS dimension, addressing enterprise
architecture, IT governance, socio-technical co-evolution, IT-business
alignment, and IS success evaluation.

### 9.1 Enterprise architecture alignment

The DSW technology stack (§3) is a list of components; it is not an
enterprise architecture. For a university DSW to be implementable, it must
align with established EA frameworks. We propose alignment with the JISC
Enterprise Architecture model (widely used in UK higher education) and
TOGAF (industry standard), structured as four architecture domains:

**Business architecture:** The DSW supports the university's core missions —
teaching, research, and administration. Each stakeholder group (§2) maps to
business capabilities. The DSW must be traceable to institutional
strategic objectives (e.g., "increase research data sovereignty by 2028").

**Data architecture:** Data domains include: (a) identity data (accounts,
credentials, roles); (b) content data (documents, files, media); (c)
communication data (email, chat, video); (d) research data (datasets,
publications, code); (e) administrative data (student records, HR, finance).
Each domain has distinct sovereignty requirements, retention policies, and
access controls.

**Application architecture:** The five-layer stack (§3) maps to application
services: infrastructure services (compute, storage, network), platform
services (identity, collaboration, communication), and business services
(LMS, ERP, library, research data management). API boundaries between
layers must be defined before procurement.

**Technology architecture:** Deployment topology (on-premise, hybrid cloud,
federated), network architecture (VPN, zero-trust, segmentation), and
infrastructure specifications (compute, storage, GPU for AI).

**ArchiMate dependency mapping:** The DSW components have dependencies that
must be modelled. For example: Collabora Online depends on Nextcloud for
storage; sovereign RAG depends on the vector store, which depends on the
embedding model, which depends on GPU infrastructure. A change in any
component propagates downstream. Without dependency mapping, migration
planning is guesswork.

### 9.2 IT governance model

The paper proposes a steering committee (§5.4) but does not specify IT
governance mechanisms. We propose alignment with COBIT (Control
Objectives for Information and Related Technologies) and ITIL:

**Decision rights (RACI matrix):**

| Decision | R (Responsible) | A (Accountable) | C (Consulted) | I (Informed) |
|----------|-----------------|-----------------|---------------|--------------|
| Platform selection | IT Dept | CIO | DPO, Faculty, Students | All |
| Data residency policy | DPO | Rectorate | IT, Legal | All |
| Security standards | IT Security | CIO | DPO, External auditor | All |
| Feature prioritisation | Product owner | Steering committee | User advisory board | All |
| Vendor selection | Procurement | CIO | Legal, IT | All |
| Incident response | IT Security | CIO | DPO, Rectorate | Affected users |

**Accountability framework:** Each governance body has defined KPIs:
- Steering committee: migration progress, budget adherence, risk register.
- Technical working group: uptime, security incidents, user-reported bugs.
- User advisory board: satisfaction scores, feature requests, accessibility
  compliance.
- DPO: compliance audit results, DPIA completion, incident response time.

**Performance measurement (ITIL):** Service level agreements (SLAs) for
sovereign platforms must be defined: availability (99.9% target), response
time (<4 hours for critical issues), data recovery (RPO/RTO), and user
satisfaction (≥3.5/5).

### 9.3 Socio-technical co-evolution

The original paper treats technology and people as separate concerns
(technology in §3, people in §2). Leavitt's diamond model frames them as
co-evolving: technology, people, structure, and tasks must change together.
A DSW migration that changes technology without changing tasks, structure,
or people's skills will fail.

**Application to DSW:**

- **Technology change:** Deploy Nextcloud + Collabora.
- **Task change:** Faculty must learn new collaboration workflows; admin
  staff must learn new document approval processes.
- **Structure change:** IT department must develop new capabilities
  (Linux administration, open-source security, community engagement).
- **People change:** Training programmes, change champions, skills
  development.

**Co-evolution principle:** Changes in one dimension require compensating
changes in others. If technology changes rapidly (Phase 2 pilot), tasks
and people must change at compatible speed. If people cannot adapt
(Phase 4 scale), technology deployment must slow.

**SSM (Soft Systems Methodology):** The stakeholder landscape (§2) is
complex and contested. SSM's rich picture technique could be used in Phase 1
(Assess) to capture the multiple, conflicting perspectives of stakeholders
before designing solutions. The power dynamics analysis (§2.13) is a first
step; a full SSM analysis would produce a conceptual model of the DSW
system that stakeholders could debate and refine.

### 9.4 IT-business alignment

The DSW must align with university strategic objectives. Henderson &
Venkatraman's strategic alignment model identifies four domains:
business strategy, IT strategy, organisational infrastructure, and IT
infrastructure. Alignment requires:

- **Strategic fit:** DSW objectives (sovereignty, control) must be
  traceable to institutional strategic plan objectives (academic freedom,
  research excellence, student success).
- **Functional integration:** IT infrastructure (DSW stack) must support
  business processes (teaching, research, administration) without
  disruption.
- **Alignment governance:** A joint IT-business steering committee (not
  IT-only) ensures both perspectives are represented.

**Practical application:** In Phase 1 (Assess), the sovereignty audit
should map each cloud service to the business capability it supports and
the strategic objective it serves. This prevents "sovereignty for
sovereignty's sake" and ensures DSW investment is prioritised by
institutional value.

### 9.5 IS success evaluation (DeLone & McLean)

The paper's success criteria (§4) are operational (adoption rate, incident
count) but lack a comprehensive IS success framework. DeLone & McLean's
model provides six dimensions:

1. **System quality:** reliability, usability, functionality, performance.
   *DSW metric:* uptime, response time, feature parity with proprietary.
2. **Information quality:** accuracy, completeness, relevance, timeliness.
   *DSW metric:* search quality, document version control, metadata
   completeness.
3. **Service quality:** responsiveness, empathy, assurance, tangibles.
   *DSW metric:* helpdesk response time, training availability, SLA
   compliance.
4. **Use:** extent and nature of system use.
   *DSW metric:* active users, feature utilisation, shadow IT reduction.
5. **User satisfaction:** overall satisfaction with the system.
   *DSW metric:* SUS (System Usability Scale) score, NPS (Net Promoter
   Score).
6. **Net benefits:** individual and organisational benefits.
   *DSW metric:* productivity measures, compliance audit results, cost
   savings, sovereignty indicators.

**Recommendation:** Phase 2 (Pilot) evaluation should measure all six
dimensions, not just adoption rate and incident count.

---

## 10. System Architecture and Security Engineering

This section deepens the paper's CS dimension, providing system
architecture, scalability analysis, security threat model, AI architecture,
data migration strategy, and observability framework.

### 10.1 System architecture

The DSW is not a single platform but a federated system of components.
The following architecture describes the target state (Phase 4: Scale).

**Component interaction model:**

```
┌─────────────────────────────────────────────────────────────┐
│                    User Layer (Browser/Mobile)               │
├─────────────────────────────────────────────────────────────┤
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐      │
│  │ Nextcloud│ │ Collabora│ │  Matrix  │ │  Jitsi   │      │
│  │ (files)  │ │ (office) │ │  (chat)  │ │ (video)  │      │
│  └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘      │
│       │            │            │            │              │
│  ┌────┴────────────┴────────────┴────────────┴────┐        │
│  │              API Gateway / Reverse Proxy        │        │
│  │         (Traefik / nginx, TLS termination)     │        │
│  └────────────────────┬───────────────────────────┘        │
├───────────────────────┼─────────────────────────────────────┤
│  ┌────────────────────┴───────────────────────────┐        │
│  │           Identity Layer (Keycloak / Shibboleth) │        │
│  │      OIDC/SAML, MFA, eduGAIN federation          │        │
│  └────────────────────┬───────────────────────────┘        │
├───────────────────────┼─────────────────────────────────────┤
│  ┌────────────────────┴───────────────────────────┐        │
│  │           Data Layer                           │        │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────────┐   │        │
│  │  │PostgreSQL│ │  Redis   │ │ Object Store │   │        │
│  │  │(metadata)│ │ (cache)  │ │  (S3-compat) │   │        │
│  │  └──────────┘ └──────────┘ └──────────────┘   │        │
│  └────────────────────────────────────────────────┘        │
├─────────────────────────────────────────────────────────────┤
│  ┌────────────────────────────────────────────────┐        │
│  │           AI Layer (Phase 3+)                  │        │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────────┐   │        │
│  │  │  LLM     │ │ Embedding│ │ Vector Store │   │        │
│  │  │ (vLLM)   │ │  Model   │ │  (Qdrant)    │   │        │
│  │  └──────────┘ └──────────┘ └──────────────┘   │        │
│  └────────────────────────────────────────────────┘        │
├─────────────────────────────────────────────────────────────┤
│  ┌────────────────────────────────────────────────┐        │
│  │           Observability Layer                  │        │
│  │  Prometheus + Grafana + Loki + Jaeger          │        │
│  └────────────────────────────────────────────────┘        │
└─────────────────────────────────────────────────────────────┘
```

**Data flows:**

1. **User authentication:** User → API Gateway → Keycloak (OIDC) → eduGAIN
   federation → institutional IdP. Token returned to user; validated by all
   downstream services.
2. **File access:** User → API Gateway → Nextcloud → PostgreSQL (metadata)
   → Object Store (content). Access controlled by Nextcloud's permission
   system, integrated with Keycloak groups.
3. **Document editing:** User → API Gateway → Collabora (WOPI protocol) →
   Nextcloud (storage). Real-time collaboration via WebSocket.
4. **AI query:** User → API Gateway → Sovereign RAG service → Embedding model
   (query vectorisation) → Vector store (retrieval) → LLM (generation) →
   User. All processing on-premise.
5. **Cross-institutional sharing:** User (Uni A) → Federation gateway →
   User (Uni B). Identity via eduGAIN; data via federated Nextcloud or
   data-space protocol.

**API boundaries:** All inter-service communication uses REST APIs with
OAuth2/JWT authentication. The API Gateway enforces rate limiting,
authentication, and TLS. No service is directly exposed to the internet.

### 10.2 Scalability analysis

Universities range from 5,000 to 100,000 users. The proposed stack must
scale accordingly.

**Nextcloud:** Supports horizontal scaling via multiple app servers behind
a load balancer. Database (PostgreSQL) can be clustered (Patroni). File
storage via S3-compatible object store (Ceph, MinIO) supports petabyte
scale. Benchmarks: Nextcloud reports 100,000+ concurrent users in large
deployments (e.g., German federal administration). *Caveat:* These are
vendor-reported benchmarks, not peer-reviewed.

**Collabora Online:** Scales via multiple document server instances.
Each instance handles ~100-200 concurrent editing sessions. For a
university of 50,000 users (assuming 5% concurrent editing), 25-50
instances required. GPU acceleration available for rendering.

**Matrix (Element):** Synapse server scales to ~100,000 users per
instance with appropriate resources (16+ CPU cores, 32+ GB RAM). Federation
adds complexity but is well-tested (eduGAIN-scale).

**Infrastructure estimates (illustrative, Phase 4):**

| Component | Small (5K users) | Medium (25K users) | Large (100K users) |
|-----------|-----------------|-------------------|-------------------|
| App servers | 2 | 4 | 8+ |
| Database | 1 (HA pair) | 1 cluster (3 nodes) | 1 cluster (5 nodes) |
| Object storage | 10 TB | 50 TB | 200 TB |
| GPU (AI) | 1 (A100) | 2 (A100) | 4+ (A100/H100) |
| Est. monthly infra cost | €3,000–5,000 | €15,000–25,000 | €60,000–100,000 |

*These are rough estimates based on cloud pricing for equivalent
infrastructure. Actual costs depend on on-premise vs. hosted, existing
infrastructure, and staffing.*

### 10.3 Security threat model (STRIDE)

**Threats and mitigations:**

| Threat | Category | Risk | Mitigation |
|--------|----------|------|------------|
| Data breach (external) | Spoofing/Tampering | High | TLS 1.3, WAF, IDS/IPS, MFA, network segmentation |
| Data exfiltration | Information disclosure | High | DLP policies, egress filtering, audit logging, zero-trust |
| Account compromise | Spoofing | High | MFA (hardware tokens for admins), passwordless (FIDO2), anomaly detection |
| Supply chain attack | Tampering | Medium-High | SBOM, dependency scanning (Dependabot/Snyk), reproducible builds, vendor assessment |
| Ransomware | Denial of service | High | Immutable backups (3-2-1 rule), air-gapped backup, incident response plan |
| Insider threat | Elevation of privilege | Medium | Least privilege, access reviews, audit logging, separation of duties |
| Surveillance (state/corporate) | Information disclosure | Medium | On-premise hosting, no telemetry, open-source auditability |
| DDoS | Denial of service | Medium | CDN/DDoS protection, rate limiting, auto-scaling |

**Security architecture controls:**

- **Encryption at rest:** AES-256 for all stored data (files, database,
  backups). Key management via HSM (Hardware Security Module) or cloud KMS
  (if hybrid).
- **Encryption in transit:** TLS 1.3 for all communications. Certificate
  management via Let's Encrypt or institutional CA.
- **Authentication:** OIDC/SAML via Keycloak/Shibboleth. MFA mandatory for
  admin accounts; optional (but encouraged) for users. FIDO2/WebAuthn
  support.
- **Authorisation:** Role-based access control (RBAC) integrated with
  institutional identity (LDAP/AD groups). Principle of least privilege.
- **Network:** Zero-trust architecture. Services behind reverse proxy.
  Micro-segmentation between tiers. No direct internet exposure of
  databases or AI services.
- **Backup:** 3-2-1 rule (3 copies, 2 media, 1 off-site). Immutable
  backups for ransomware protection. Tested recovery procedures (quarterly).
- **Monitoring:** SIEM (Security Information and Event Management) for
  log aggregation and anomaly detection. Alerting for suspicious activity.

**Supply chain security:** Open-source platforms depend on thousands of
dependencies. The DSW must implement:
- SBOM (Software Bill of Materials) generation for all deployed components.
- Automated vulnerability scanning (OWASP Dependency-Check, Snyk).
- Reproducible builds where possible.
- Vendor security assessment for commercial open-source distributions
  (Collabora, Nextcloud GmbH).
- Regular dependency updates with testing pipeline.

**Incident response framework:** Based on NIST SP 800-61:
1. **Preparation:** Incident response team, communication plan, tools.
2. **Detection & Analysis:** SIEM alerts, user reports, automated monitoring.
3. **Containment:** Isolate affected systems, preserve evidence.
4. **Eradication:** Remove threat, patch vulnerabilities.
5. **Recovery:** Restore from clean backups, verify integrity.
6. **Post-incident:** Root cause analysis, lessons learned, process improvement.

### 10.4 AI architecture specification

"Sovereign RAG" is mentioned but not architected. The following specifies
the AI layer for Phase 3+ deployment.

**Components:**

| Component | Technology | Specification |
|-----------|-----------|---------------|
| LLM | vLLM serving Llama 3.1 70B or Mistral Large | 4× A100 (80GB) or 2× H100; quantised (AWQ/GPTQ) for efficiency |
| Embedding model | BGE-M3 or E5-Mistral-7B | 1× A100; multilingual support |
| Vector store | Qdrant or Weaviate | Clustered; supports hybrid search (vector + keyword) |
| RAG framework | LangChain / LlamaIndex | Document chunking, retrieval, reranking, generation |
| Document processing | Unstructured.io / Apache Tika | PDF, DOCX, PPTX, HTML, Markdown extraction |
| Guardrails | NeMo Guardrails / Llama Guard | Input/output filtering, PII detection, hallucination reduction |

**Data pipeline:**
1. Documents ingested from Nextcloud (via API).
2. Text extracted and chunked (512-1024 tokens, overlap 128).
3. Embeddings generated and stored in vector store.
4. User query → embedding → retrieval (top-10 chunks) → reranking → LLM
   generation with citations.
5. Response returned to user with source references.

**Model management:**
- Model updates: quarterly evaluation of new open-source models; A/B testing
  before promotion.
- Fine-tuning: domain-specific fine-tuning on institutional data (research
  papers, course materials) using LoRA/QLoRA.
- Versioning: model versions tracked; rollback capability.
- Monitoring: latency, throughput, error rate, user feedback (thumbs up/down).

**Privacy controls:**
- No data leaves the institution.
- User queries are not logged with PII.
- Document-level access control: RAG only retrieves documents the user has
  permission to access.
- Audit log of all AI interactions (for compliance).

**Governed Sovereign RAG (arXiv:2610.36561):** This paper proposes
tripartite epistemic routing for public administration. Its applicability
to universities is partial: the governance routing concept is relevant, but
the specific implementation (facet-guided clustering) has not been tested
in HE contexts. We recommend piloting and evaluating before
institution-wide deployment.

### 10.5 Data migration strategy

Data migration is the hardest part of platform transitions. The paper
previously mentioned "migrate pilot data" without strategy.

**Migration phases:**

1. **Inventory:** Catalogue all data stores (files, emails, calendars,
   contacts, LMS content, research data). Classify by sensitivity,
   retention, and ownership.
2. **Mapping:** Map source data structures to target platform structures.
   Identify data that cannot be migrated (proprietary formats, DRM-protected
   content).
3. **Pilot migration:** Migrate a representative sample (1 department).
   Validate data integrity (checksums, metadata preservation, permission
   mapping).
4. **Gradual migration:** Migrate department by department. Maintain
   parallel operation during transition (read-only access to old platform).
5. **Validation:** Post-migration verification (automated checksums,
   user spot-checks, compliance audit).
6. **Decommission:** After validation period (3-6 months), decommission
   old platform (or reduce to archive-only).

**Data migration risks:**
- **Data loss:** Mitigated by checksums and parallel operation.
- **Permission mapping errors:** Complex (group memberships, sharing links).
  Requires manual review for sensitive data.
- **Format incompatibility:** Some proprietary formats (e.g., M365
  metadata) may not transfer. Acceptance of some data loss required.
- **User disruption:** Communication and training essential.
- **Rollback:** If migration fails, revert to old platform (data remains
  there during transition).

**Tools:** rclone (file sync), imapsync (email), CalDAV/CardDAV export
(calendars/contacts), custom scripts for LMS content.

### 10.6 Observability framework

No mention of monitoring exists in the original paper. A production DSW
requires comprehensive observability.

**Metrics (Prometheus):**
- **Infrastructure:** CPU, memory, disk, network per node.
- **Application:** request rate, latency (p50/p95/p99), error rate per
  service.
- **User experience:** page load time, file upload/download speed, editing
  latency.
- **Business:** active users, storage utilisation, feature adoption rates.

**Logging (Loki):** Centralised log aggregation from all services.
Structured logging (JSON). Retention: 90 days hot, 1 year cold.

**Tracing (Jaeger):** Distributed tracing for request flows across services.
Essential for debugging performance issues in federated architecture.

**Alerting:** PagerDuty/Opsgenie integration. Severity levels:
- P1 (critical): service down, data loss, security breach → immediate
  response.
- P2 (high): degraded performance, elevated errors → 1 hour response.
- P3 (medium): non-critical issues → next business day.
- P4 (low): cosmetic/minor → weekly review.

**Dashboards (Grafana):** Executive dashboard (uptime, users, costs),
operations dashboard (infrastructure health, alerts), security dashboard
(auth failures, anomalies), user experience dashboard (latency, satisfaction).

---

## 11. Legal and Regulatory Framework

This section deepens the paper's legal dimension, addressing GDPR
implementation, the legal definition of digital sovereignty, public
procurement law, academic freedom, and AI regulation.

### 11.1 GDPR implementation in sovereign contexts

The paper mentions GDPR but does not address implementation. The
following analyses key GDPR articles in the context of a self-hosted DSW.

**Art. 6 (Lawful basis for processing):** Universities typically rely on
public task (Art. 6(1)(e)) for teaching/research data and legitimate
interest (Art. 6(1)(f)) for some administrative processing. A sovereign
platform does not change the lawful basis, but it does change the
controller/processor relationship: in a self-hosted model, the university
is both controller and (via its IT department) processor, eliminating
the need for a data processing agreement with a third-party cloud
provider. This is a sovereignty advantage but requires internal
governance.

**Art. 9 (Special category data):** Research data involving health,
biometrics, or political opinions requires explicit consent or another
Art. 9 condition. Sovereign platforms can enforce granular access
controls and data localisation, but the legal obligation (consent,
DPIA) remains the institution's responsibility.

**Art. 35 (DPIA):** Deploying a new workplace platform requires a Data
Protection Impact Assessment. The DSW migration itself is a
high-risk processing activity (new technology, large-scale processing,
potential for surveillance). The DPIA must assess: (a) necessity and
proportionality; (b) risks to data subjects; (c) mitigation measures.
Sovereign platforms simplify some aspects (data residency, auditability)
but introduce others (new attack surface, operational security risk).

**Data subject rights (Arts. 15-22):** The DSW must support:
- Right of access (Art. 15): users can export their data.
- Right to erasure (Art. 17): deletion across all systems (files, email,
  chat, AI training data).
- Right to portability (Art. 20): machine-readable export.
- Right to object (Art. 21): opt-out of AI processing or analytics.
Sovereign platforms can implement these via self-service portals; the
implementation effort is non-trivial.

**Cross-border data transfers (Arts. 44-49):** Federated collaboration
(Phase 3) involves cross-institutional data sharing. If partner
institutions are in different jurisdictions, transfer mechanisms are
required: Standard Contractual Clauses (SCCs), adequacy decisions, or
Binding Corporate Rules (BCRs). The European Data Protection Board's
guidelines on international data transfers apply. Sovereign platforms
do not eliminate this obligation; they make it more tractable by
providing verifiable data residency.

**Controller/processor in self-hosted model:** When the university hosts
its own platform, it is both controller and processor. This eliminates
vendor DPA negotiations but requires internal data processing
agreements between departments (e.g., HR as controller, IT as processor).
The DPO must define these relationships.

### 11.2 Legal definition of digital sovereignty

The paper uses "digital sovereignty" without legal definition. The term
operates at multiple levels:

- **Individual sovereignty:** The right of individuals to control their
  personal data (GDPR Art. 1, Recital 7). Partially realised through
  data subject rights.
- **Institutional sovereignty:** The right of an organisation to control
  its data, infrastructure, and digital processes. Not a standalone legal
  concept in EU law; derived from contract law, GDPR, and public
  procurement rules.
- **National sovereignty:** The right of a state to govern digital
  infrastructure within its territory. Expressed through data localisation
  laws, national security frameworks, and public procurement preferences.
- **European sovereignty:** The EU's ambition for digital autonomy
  (Digital Decade, Data Strategy, AI Act). Expressed through regulation
  (GDPR, DMA, DSA, AI Act) rather than infrastructure ownership.

**Key insight:** "Digital sovereignty" is primarily a political concept,
not a legal one. EU law does not define it; it is expressed through
specific regulations (GDPR for data, NIS2 for security, AI Act for AI).
A university's "sovereignty" is therefore a bundle of legal rights and
obligations, not a single status. The DSW should be framed as
implementing these specific legal requirements, not as achieving an
abstract "sovereignty."

**Recommendation:** Replace "digital sovereignty" with specific legal
obligations throughout the paper (e.g., "GDPR data residency
requirements," "NIS2 security obligations," "AI Act high-risk
classification").

### 11.3 Public procurement law

Universities are public bodies subject to EU procurement law (Directive
2014/24/EU). Open-source procurement presents specific challenges:

- **No standardised contracts:** Proprietary vendors offer standard
  contracts with SLAs. Open-source procurement requires custom contracts
  for support, maintenance, and development.
- **Evaluation criteria:** Procurement rules require objective evaluation
  criteria. Open-source platforms can be evaluated on TCO, feature
  completeness, security, and strategic alignment — but these must be
  quantified.
- **Vendor lock-in risk:** Open-source distributions (e.g., Nextcloud
  GmbH's enterprise distribution) can create vendor dependency. Procurement
  must assess the risk of the distribution vendor discontinuing support.
- **Legal risk of community projects:** If the community project (not the
  vendor) has a security vulnerability, who is liable? Procurement
  contracts must address this.
- **Innovation partnership:** The EU procurement framework allows
  "innovation partnerships" for developing new solutions. This could be
  used for DSW development with a consortium of universities and vendors.

**Recommendation:** Phase 1 (Assess) should include a procurement
readiness assessment, and Phase 4 (Scale) should use innovation
partnership procedures where appropriate.

### 11.4 Academic freedom as a legal right

The paper asserts that proprietary platforms compromise academic freedom
but does not cite legal frameworks.

**European legal framework:**
- **ECHR Art. 10 (Freedom of expression):** Protects academic freedom as
  a subset of freedom of expression. Universities have positive
  obligations to protect it.
- **EU Charter of Fundamental Rights Art. 13:** "The arts and scientific
  research shall be free of constraint." Academic freedom is a fundamental
  right.
- **National constitutional provisions:** Germany (Art. 5(3) GG),
  France (preamble), UK (Education (No. 2) Act 1986), and others
  specifically protect academic freedom in universities.

**Legal analysis:** Proprietary platforms do not inherently violate
academic freedom. The risk is structural: if a single vendor controls
communication and storage infrastructure, it has the technical capability
to restrict access, monitor communications, or comply with external
government requests (e.g., US CLOUD Act). This is a latent risk, not an
active violation. The legal argument is that universities have a positive
obligation to ensure their infrastructure does not create this latent risk.

**Evidence gap:** No documented case of a platform being used to suppress
academic work exists in the corpus or in publicly available case law.
The risk is theoretical but structurally real.

### 11.5 EU AI Act implications

The EU AI Act (Regulation 2024/1689) classifies AI systems by risk level.
Sovereign AI in universities may fall under high-risk categories:

- **Education and vocational training (Annex III, 3):** AI systems
  used for admission, assessment, or monitoring of students are
  high-risk. Sovereign AI used for grading, plagiarism detection, or
  student analytics would require: risk management system, data
  governance, technical documentation, record-keeping, transparency,
  human oversight, accuracy/robustness/cybersecurity.
- **Employment (Annex III, 4):** AI systems used for recruitment,
  promotion, or termination are high-risk. Sovereign AI used for HR
  analytics or performance evaluation would require the same compliance.
- **Research exemption:** AI systems used purely for research (not
  deployment) are exempt. But once deployed in institutional workflows,
  the exemption no longer applies.

**Implication:** The DSW's sovereign AI layer (§10.4) must be designed
for AI Act compliance from the outset. This adds significant
documentation, testing, and governance requirements that the paper's
current timeline (Phase 3: months 13-24) may not accommodate.

**Recommendation:** Add AI Act compliance as a Phase 3 deliverable with
dedicated legal review.

---

## 12. Economic Analysis

This section deepens the paper's economics dimension, providing a TCO
framework, platform market analysis, public goods analysis, market failure
analysis, and incentive analysis.

### 12.1 Total cost of ownership framework

The paper acknowledges the absence of cost quantification. The following
provides an estimation framework with illustrative ranges.

**TCO components (5-year, per 1,000 users):**

| Component | Proprietary (M365) | Sovereign (Nextcloud stack) |
|-----------|-------------------|---------------------------|
| License/subscription | €150-300/user/year | €0 (open-source) |
| Infrastructure (cloud/on-prem) | Included | €30-80/user/year |
| IT staff (admin, security) | €20-40/user/year | €60-120/user/year |
| Training and change management | €10-20/user/year | €30-50/user/year |
| Support (vendor/community) | Included | €10-30/user/year (enterprise support) |
| Security and compliance | €5-15/user/year | €15-30/user/year |
| **Total (5-year, per 1,000 users)** | **€750K-1.85M** | **€725K-1.55M** |

*These are illustrative estimates based on industry benchmarks. Actual
costs vary significantly by institution size, existing infrastructure,
staffing, and negotiation. No peer-reviewed TCO study for university
DSW exists in the corpus.*

**Key cost drivers:**
- **Staff costs dominate** sovereign TCO. Open-source eliminates license
  costs but increases operational burden. The break-even point depends on
  staff salaries and existing capacity.
- **Scale effects:** Larger universities achieve lower per-user costs for
  sovereign (fixed infrastructure costs amortised over more users). Smaller
  universities may find sovereign more expensive per user.
- **Migration costs:** One-time costs (data migration, training, parallel
  operation) estimated at €200-500 per user. These are front-loaded and
  not reflected in steady-state TCO.
- **Hidden costs:** Proprietary platforms have hidden costs (data
  egress fees, API rate limits, premium features). Sovereign platforms
  have hidden costs (security incidents, staff turnover, community
  dependency).

**Break-even analysis:** For a university of 10,000 users, estimated
break-even at 3-5 years if staff costs can be absorbed by existing IT
capacity. If new hires are required, break-even extends to 7-10 years.

**Recommendation:** Phase 1 (Assess) must include an institution-specific
TCO analysis with actual cost data, not estimates.

### 12.2 Platform market economics

The proprietary platform market (M365, Google Workspace) exhibits
classic platform economics:

**Network effects:** Value increases with number of users. Universities
benefit from interoperability with partners, suppliers, and funding
bodies that use the same platform. This creates a powerful adoption
incentive.

**Lock-in mechanisms:**
- **Data lock-in:** Proprietary formats, metadata, and integrations make
  data migration costly.
- **Integration lock-in:** LMS, ERP, and library systems integrate deeply
  with proprietary platforms.
- **Skill lock-in:** Staff and students are trained on proprietary tools;
  switching requires retraining.
- **Contract lock-in:** Multi-year enterprise agreements with volume
  discounts.

**Switching costs:** Estimated at €200-500 per user (data migration,
retraining, integration rebuild). For a 10,000-user university: €2-5M.
This is the primary barrier to DSW adoption.

**Two-sided market dynamics:** Proprietary platforms serve two sides:
users (students, staff) and developers (app ecosystem). Sovereign
platforms must build both sides: user base and developer ecosystem.
This is a chicken-and-egg problem that open-source communities solve
through grassroots adoption, not institutional mandates.

**Implication:** DSW adoption is not just a technology decision; it is a
market-positioning decision. Universities adopting sovereign platforms
are betting that the open-source ecosystem will reach sufficient
maturity to overcome network effects.

### 12.3 Public goods analysis

Open-source platforms have public good characteristics:
- **Non-rivalrous:** One university's use does not diminish another's.
- **Partially non-excludable:** Open-source code is freely available;
  enterprise support and SLAs are excludable.

**Free-rider problem:** Universities can use open-source platforms without
contributing. This leads to underinvestment in development and
maintenance. The paper's "upstream contribution" recommendation (§5.2)
addresses this but does not solve it.

**Funding models for public goods:**
- **Government funding:** Horizon Europe, Digital Europe, national
  sovereignty funds. Addresses free-riding but requires political
  support.
- **Consortium funding:** Pooled resources from member universities.
  Addresses free-riding within the consortium but not outside.
- **Vendor funding:** Commercial open-source vendors fund development
  from enterprise support revenue. Creates dependency on vendor
  priorities.
- **Hybrid:** Combination of all three. Most realistic but complex to
  govern.

**Recommendation:** The consortium model (§5.1) should include explicit
contribution requirements (e.g., each member contributes 0.5 FTE to
upstream development or €50K/year to a shared development fund).

### 12.4 Market failure analysis

Why does the market not provide sovereign workplace platforms?
The paper assumes sovereignty is desirable but does not analyse why the
market underprovides it.

**Market failures:**
1. **Positive externalities:** Data sovereignty benefits (reduced
   surveillance, improved security) accrue to society, not just the
   adopting institution. The market underprices these externalities.
2. **Information asymmetry:** Vendors know more about data handling
   practices than customers. Universities cannot fully audit proprietary
   platforms.
3. **Vendor market power:** M365 and Google Workspace have dominant
   market positions, creating barriers to entry for sovereign alternatives.
4. **Switching costs:** High switching costs lock in customers, reducing
   competitive pressure.
5. **Public good underprovision:** Open-source platforms are underfunded
   because benefits are widely shared but costs are concentrated.

**Policy implications:** These market failures justify public intervention:
- Funding (addressing underprovision).
- Regulation (GDPR data residency, NIS2 security, AI Act transparency).
- Public procurement preferences (open-source preference).
- Standards (interoperability requirements).

### 12.5 Incentive analysis for upstream contribution

The paper proposes "upstream contribution" but does not analyse
incentives. Why would a university contribute to open-source rather
than free-ride?

**Incentives for contribution:**
- **Direct benefit:** Contributions that fix bugs or add features the
  university needs. Aligned with institutional self-interest.
- **Reputation:** Academic institutions value reputation. Open-source
  contributions enhance institutional profile.
- **Recruitment:** Open-source engagement attracts technically skilled
  staff and students.
- **Grant requirements:** Some funders require open-source outputs.
- **Consortium obligation:** If consortium membership requires
  contribution, free-riding is not an option.

**Disincentives:**
- **Cost:** Developer time is expensive. Universities may prefer to spend
  on research rather than platform development.
- **Uncertainty:** Contributions may not be accepted upstream. Effort
  may be wasted.
- **Capacity:** Universities may lack the technical capacity to contribute
  meaningfully.

**Recommendation:** The consortium model should include a "contribution
bank" where members can contribute either code or funding, with
equivalent value. This accommodates institutions with different
capacities.

---

## 13. Cross-Disciplinary Synthesis

### 13.1 How the four disciplines interact

The four deep-dive disciplines are not independent; they interact:

- **IS + CS:** Enterprise architecture (IS) provides the framework;
  system architecture (CS) provides the implementation. IS governance
  defines decision rights; CS security architecture implements controls.
- **IS + Law:** IT governance (IS) must incorporate legal compliance (Law).
  COBIT controls map to GDPR requirements. DPIA (Law) is an IS governance
  deliverable.
- **IS + Economics:** TCO (Economics) informs IT investment decisions (IS).
  Platform market analysis (Economics) shapes procurement strategy (IS).
- **CS + Law:** Security architecture (CS) must implement legal
  requirements (Law). Encryption, access control, and audit logging
  satisfy GDPR and NIS2.
- **CS + Economics:** Scalability analysis (CS) determines infrastructure
  costs (Economics). Security investment (CS) is a cost driver (Economics).
- **Law + Economics:** Compliance costs (Law) are a TCO component
  (Economics). Market failure analysis (Economics) justifies regulatory
  intervention (Law).

### 13.2 Remaining disciplinary gaps (future work)

The following perspectives from the multi-perspective review (§1) are
not deep-integrated in this revision but represent important future work:

- **Organizational Behavior:** Change management frameworks (Kotter, ADKAR),
  organisational culture analysis, resistance management.
- **Higher Education Policy:** EUA/LERU/UNESCO frameworks, open science
  infrastructure (EOSC, OpenAIRE), teaching and learning implications.
- **STS:** Social shaping analysis, digital inequality, surveillance risks,
  political dimensions of sovereignty.
- **Security Engineering:** (Partially addressed in §10.3; full threat
  model and incident response need further development.)
- **HCI/UX:** User research methodology, usability evaluation framework,
  accessibility audit.
- **Public Policy:** Policy landscape analysis, policy instruments,
  sovereignty levels, international dimensions.

### 13.3 Revised paper status

This revision (Rev 3) deep-integrates four disciplinary perspectives
(IS, CS, Law, Economics) to publication standard. The paper now contains:

1. Enterprise architecture alignment and IT governance (IS).
2. System architecture, scalability, security threat model, AI
   architecture, data migration, and observability (CS).
3. GDPR implementation, legal definition of sovereignty, procurement law,
   academic freedom, and AI Act implications (Law).
4. TCO framework, platform market economics, public goods, market
   failure, and incentive analysis (Economics).

The paper remains a proposal requiring empirical validation. The
limitations identified in §7.4 still apply.

---

*This paper is Revision 4 (all key findings from both review rounds
addressed). It synthesises findings from the Digital Sovereign
Workplace research corpus (3,030 papers, frozen snapshot 2026-10-31).
Contributions, corrections, and extensions are welcome.*

---

## 14. Organizational Behavior and Change Management

This section addresses the OB gaps identified in both review rounds,
providing change management frameworks, organisational culture analysis,
resistance management, leadership sponsorship, and organisational learning.

### 14.1 Change management framework (Kotter + ADKAR)

The paper's migration model (§4) includes "training, communication,
resistance handling" in Phase 4 but does not apply established change
management frameworks. We propose a dual framework:

**Kotter's 8-Step Model (strategic change):**

1. **Create urgency:** Build the case for DSW using sovereignty risks,
   GDPR compliance gaps, and vendor lock-in evidence. Not "change for
   change's sake" but "change to protect institutional autonomy."
2. **Form a guiding coalition:** Cross-stakeholder steering committee
   (§5.4) with executive sponsorship from the Rectorate. Must include
   influential faculty, not just administrators.
3. **Create a vision:** "A sovereign digital workplace that protects
   academic freedom, research data, and institutional autonomy while
   delivering modern collaboration capabilities."
4. **Communicate the vision:** Multi-channel communication (town halls,
   department meetings, newsletters, intranet). Address the
   sovereignty-capability tension honestly.
5. **Empower action:** Remove barriers (procurement rules, IT capacity
   constraints, skill gaps). Provide resources and authority to pilot
   teams.
6. **Create short-term wins:** Phase 2 pilot success stories.
   Publicise adoption rates, user satisfaction, and sovereignty gains.
7. **Sustain acceleration:** Expand to additional departments based on
   pilot evidence. Build momentum through peer influence, not mandates.
8. **Institutionalise change:** Embed DSW in institutional policies
   (IT strategy, procurement rules, data governance). Make it "the way
   we work," not a project.

**ADKAR (individual change):** Awareness → Desire → Knowledge → Ability
→ Reinforcement. Each migration phase must address all five elements
for each stakeholder group. Phase 2 (Pilot) focuses on Knowledge and
Ability (training, support). Phase 4 (Scale) focuses on Reinforcement
(ongoing support, policy embedding).

**Application to DSW:** The migration model (§4) should be reframed
through these lenses. Phase 1 (Assess) = Kotter steps 1-3 + ADKAR
Awareness. Phase 2 (Pilot) = Kotter steps 4-6 + ADKAR Desire/Knowledge/
Ability. Phase 4 (Scale) = Kotter steps 7-8 + ADKAR Reinforcement.

### 14.2 Organisational culture analysis

Universities are not generic organisations. Their cultures shape DSW
adoption:

- **Collegial governance:** Decisions are made by committee, not decree.
  A top-down mandate for DSW will face resistance. The steering
  committee (§5.4) must be representative and consensus-oriented.
- **Academic autonomy:** Faculty expect to choose their own tools.
  Mandating a single platform conflicts with this expectation. The
  DSW must be "attractive enough to choose" rather than "mandatory
  to use."
- **Disciplinary silos:** STEM disciplines (computational research, HPC
  integration) have different platform needs than humanities (document-
  centric workflows, archival needs). A one-size-fits-all DSW will
  fail. The stakeholder analysis (§2) should be extended with
  disciplinary profiles.
- **Administrative culture:** Admin staff are process-oriented and
  change-averse. They need reliable, well-integrated tools. The DSW
  must demonstrate process improvement, not just sovereignty.
- **Student culture:** Students are pragmatic and mobile-first. They
  will adopt whatever works best on their devices. The DSW must
  compete on UX, not just values.

**Implication:** The migration model should be adapted per discipline
and stakeholder group, not applied uniformly.

### 14.3 Resistance management plan

Specific resistance sources and mitigations:

| Source | Concern | Mitigation |
|--------|---------|------------|
| IT staff | Job security, skill obsolescence, increased workload | Reskilling programme, clear career paths, additional staffing during transition |
| Faculty | Tool preference, academic freedom concerns, productivity loss | Pilot with volunteer departments, demonstrate capability parity, academic freedom guarantees |
| Vendors | Loss of revenue, relationship disruption | Phased license reduction, maintain hybrid model, vendor engagement in consortium |
| Students | Learning curve, reduced capability, mobile experience | UX-focused design, comprehensive onboarding, feedback channels, gradual rollout |
| DPOs | Compliance uncertainty, new risk surface | Early involvement, DPIA support, compliance verification at each phase |
| Procurement | Unfamiliar open-source procurement | Procurement readiness assessment (§11.3), innovation partnership procedures |
| Leadership | Cost, risk, reputation | TCO analysis (§12.1), risk mitigation plan, peer institution case studies |

**Resistance monitoring:** Track resistance indicators (shadow IT usage,
support ticket volume, user satisfaction trends, adoption rates by
department). Address proactively, not reactively.

### 14.4 Leadership sponsorship and succession

- **Executive sponsor:** The Rector/President must be the visible
  champion. Without top-level sponsorship, DSW will be deprioritised
  by competing institutional priorities.
- **Sponsorship succession:** Over a 48-month timeline, leadership
  changes are likely. The DSW must be institutionalised (embedded in
  strategy documents, policies, and budgets) so it survives leadership
  transitions. Not dependent on a single champion.
- **Middle management engagement:** Department heads and deans are
  critical intermediaries. They translate institutional vision into
  departmental action. Engage them early and provide them with
  department-specific talking points.

### 14.5 Organisational learning

- **Knowledge capture:** Document lessons learned from each phase
  (pilot results, user feedback, technical issues, governance
  decisions). Create an institutional knowledge base.
- **Capability building:** Develop internal expertise in open-source
  platform management, security, and AI operations. Reduce dependency
  on external consultants over time.
- **Community of practice:** Connect with other universities
  implementing DSW. Share experiences, tools, and solutions.
- **Research integration:** The DSW migration is a research
  opportunity. Collect data on adoption, satisfaction, productivity,
  and well-being. Contribute to the evidence base.

---

## 15. Higher Education Policy and Open Science Integration

This section addresses the HE policy gaps, connecting DSW to HE policy
frameworks, open science infrastructure, research assessment reform,
and teaching/learning.

### 15.1 HE policy alignment

- **EUA (European University Association):** The EUA digital
  transformation agenda emphasises institutional autonomy,
  interoperability, and digital skills. DSW aligns with all three.
  The EUA's "Universities without walls" vision supports federated,
  interoperable digital infrastructure.
- **LERU (League of European Research Universities):** LERU's position
  on open science and digital research infrastructure supports
  sovereign platforms that enable open data and reproducible research.
- **UNESCO OER recommendations:** Open Educational Resources require
  open platforms. DSW can host and distribute OERs without vendor
  lock-in.
- **National strategies:** Germany's Sovereign Tech Fund, France's
  DINUM, and similar national initiatives provide funding and policy
  support for sovereign digital infrastructure. Universities should
  align DSW proposals with national digital sovereignty strategies.

### 15.2 Open science infrastructure integration

The DSW must integrate with existing open science infrastructure, not
duplicate it:

- **EOSC (European Open Science Cloud):** DSW should enable
  researchers to deposit data in EOSC-compliant repositories, use
  EOSC services, and federate identity via eduGAIN (already in the
  stack). The DSW is the workplace layer; EOSC is the research data
  layer.
- **OpenAIRE:** Integration with OpenAIRE for publication and data
  discovery. DSW can automate metadata harvesting and deposit.
- **ORCID:** Researcher identity management. DSW should support ORCID
  integration for authorship, peer review, and grant reporting.
- **Zenodo:** Institutional repository integration for data and
  software deposition.
- **DataCite:** DOI minting for research datasets hosted on DSW.

**Principle:** The DSW should be the "on-ramp" to open science
infrastructure, not a competing system.

### 15.3 Research assessment reform (CoARA / DORA)

- **DORA (Declaration on Research Assessment):** Opposes over-reliance
  on journal impact factors. Supports evaluation of diverse research
  outputs (data, software, preprints). DSW platforms that support open
  science outputs (open data, open code, open access) align with DORA
  principles.
- **CoARA (Coalition for Advancing Research Assessment):** Promotes
  responsible research assessment. DSW can provide transparent,
  auditable metrics for research activity (collaboration, data
  sharing, open access compliance) that support CoARA's goals.
- **Implication:** DSW adoption can be framed as supporting research
  assessment reform, which is a priority for many European universities
  and funders.

### 15.4 Teaching and learning (EdTech integration)

- **Digital pedagogy:** Sovereign platforms must support modern
  pedagogy (flipped classroom, collaborative learning, peer
  assessment, project-based learning). Nextcloud + Collabora +
  Moodle provides a viable stack, but integration effort is
  significant.
- **LMS sovereignty:** Moodle is open-source and self-hostable. It
  should be part of the sovereign stack (currently listed as "missing
  from the stack" in §3.1). Moodle integration with Nextcloud
  (file sharing, assignment submission) and Collabora (document
  editing) is well-supported.
- **Learning analytics:** Sovereign platforms can collect learning
  analytics (engagement, performance, early warning) while preserving
  student privacy (no third-party data sharing). This is a sovereignty
  advantage. But it requires careful design (consent, transparency,
  opt-out).
- **Assessment integrity:** Online assessment (quizzes, exams,
  plagiarism detection) is critical. Moodle provides quiz and
  assignment tools. Plagiarism detection (Turnitin alternative:
  Compilatio, or open-source: Plagiarism Checker X) must be
  integrated. Remote proctoring raises privacy concerns; sovereign
  platforms should support privacy-preserving alternatives.
- **Student digital literacy:** DSW adoption requires digital literacy
  training for students. This should be integrated into the curriculum
  (e.g., as part of first-year orientation or digital skills modules).
- **Universal Design for Learning (UDL):** Sovereign platforms must
  support UDL principles: multiple means of representation (captions,
  screen readers, alternative formats), engagement (flexible
  assessment, choice), and expression (multiple submission formats).
- **Equity:** Students with limited device/connectivity access must
  not be disadvantaged. Mobile-first design, offline capability, and
  device lending programmes are essential.

---

## 16. Digital Preservation and Archival Strategy

This section addresses the archival science gaps, providing a
preservation strategy, metadata standards, records management, and
format policy.

### 16.1 Preservation framework (OAIS)

The DSW must address long-term preservation, not just active storage.
We propose alignment with the OAIS (Open Archival Information System)
reference model:

- **Ingest:** Data flows from active DSW systems to preservation
  systems. Triggered by retention policies or manual deposit.
- **Archival storage:** Bit-level preservation with checksums, redundant
  copies, and format migration.
- **Data management:** Metadata cataloguing, search, and discovery.
- **Access:** Controlled access to preserved data (embargo periods,
  access restrictions).
- **Administration:** Policy management, audit, and reporting.

**Principle:** The DSW is the "active" layer; institutional repositories
(DSpace, EPrints) and archives are the "preservation" layer. Data flows
between them based on retention policies.

### 16.2 Data lifecycle and retention

| Data type | Active retention | Archive retention | Disposition |
|-----------|-----------------|-------------------|-------------|
| Student records | Duration of study + 10 years | Permanent (transcripts) | Destroy after retention |
| Research data | Project duration + 10 years | Permanent (published) | Deposit in repository |
| Administrative docs | 7 years | 25 years | Destroy after retention |
| Email/communication | 3 years | Not archived (unless legal hold) | Auto-delete |
| LMS content | Course duration + 2 years | Not archived | Delete |
| AI training data | Model lifecycle | Not archived | Delete with model |

**Legal hold:** When litigation or investigation is anticipated, all
relevant data must be preserved regardless of retention policy. The DSW
must support legal hold (suspend deletion, preserve metadata).

### 16.3 Metadata standards

- **Dublin Core:** Basic metadata for all digital objects.
- **DataCite:** For research datasets (DOI minting, citation).
- **PREMIS:** For preservation metadata (events, agents, rights).
- **Schema.org:** For web discoverability.
- **Institutional extensions:** University-specific metadata
  (department, course, research project, funder).

**Implementation:** Metadata should be captured at creation time (not
retrospectively). Nextcloud supports custom metadata via tags and
properties. Moodle exports metadata with course content.

### 16.4 Format strategy

- **Preferred formats:** Open formats (ODF for documents, PDF/A for
  archival, CSV/JSON for data, TIFF/PNG for images, WebM for video).
- **Avoid:** Proprietary formats that require specific software
  (e.g., M365-specific metadata, Google Docs internal format).
- **Migration planning:** When formats become obsolete, plan migration
  to successor formats. Budget for format migration in long-term
  planning.
- **Validation:** Automated format validation on ingest (e.g., JHOVE
  for file format identification and validation).

### 16.5 Integration with institutional repositories

- **DSpace/EPrints integration:** Automated deposit of research data
  and publications from DSW to institutional repository.
- **CKAN/Dataverse integration:** Research data management platforms
  for structured data deposit.
- **API-based workflow:** When a researcher marks a dataset as
  "published," the DSW triggers an automated deposit workflow
  (metadata extraction, format validation, repository deposit, DOI
  minting).

---

## 17. Environmental Sustainability and Green IT

This section addresses the green IT gaps, providing environmental
impact analysis, sustainability metrics, energy-efficient AI, and
sustainability as a selection criterion.

### 17.1 Environmental impact analysis

Self-hosted infrastructure has an environmental footprint that must be
analysed and minimised:

**Carbon footprint comparison (illustrative, per 1,000 users/year):**

| Factor | Proprietary cloud (M365) | Sovereign (on-premise) | Sovereign (green hosting) |
|--------|------------------------|----------------------|--------------------------|
| Server energy | Included (provider PUE ~1.1) | 15-25 MWh | 15-25 MWh |
| Cooling | Included | 5-10 MWh | 5-10 MWh |
| Network | Included | 2-5 MWh | 2-5 MWh |
| GPU (AI) | Included (provider) | 5-15 MWh | 5-15 MWh |
| Carbon (tCO2e) | ~2-5 (provider offset) | ~10-20 (grid avg) | ~2-5 (renewable) |

*These are rough estimates. Actual values depend on PUE, grid carbon
intensity, and utilisation.*

**Key insight:** On-premise sovereign infrastructure may have a
*higher* carbon footprint than proprietary cloud (which benefits from
hyperscaler efficiency and renewable energy commitments). This is a
counter-argument to DSW that must be addressed. Mitigations:
- Use green hosting providers (renewable energy, high PUE efficiency).
- Participate in shared consortium infrastructure (better utilisation).
- Optimise AI workloads (quantisation, scheduling, batching).
- Offset remaining emissions.

### 17.2 Sustainability metrics

Add to the observability framework (§10.6):
- **Energy consumption (kWh):** Per service, per user, total.
- **Carbon emissions (tCO2e):** Using grid carbon intensity factors.
- **PUE:** Power Usage Effectiveness of on-premise facilities.
- **Hardware lifecycle:** Age, utilisation, and replacement planning.
- **E-waste:** Disposal and recycling tracking.

**Reporting:** Annual sustainability report for the DSW, aligned with
university sustainability reporting (e.g., THE Impact Rankings,
STARS).

### 17.3 Energy-efficient AI

The AI architecture (§10.4) specifies 4+ A100 GPUs. Energy
optimisation:

- **Model quantisation:** AWQ/GPTQ reduces GPU memory and energy by
  50-75% with minimal quality loss.
- **Inference scheduling:** Batch requests, use dynamic batching, and
  scale down during low-demand periods.
- **Model selection:** Use smaller, more efficient models where
  possible (e.g., Mistral 7B instead of Llama 70B for simple queries).
- **Renewable energy:** Schedule intensive workloads (model training,
  batch processing) during periods of high renewable energy
  availability.
- **Shared GPU infrastructure:** Consortium-level GPU sharing reduces
  idle capacity.

### 17.4 Sustainability as selection criterion

Add "carbon footprint" and "energy efficiency" to the capability
comparison table (§1.3) and platform evaluation criteria. When
comparing sovereign vs. proprietary, include environmental impact
alongside capability and cost.

### 17.5 Circular economy

- **Hardware lifecycle extension:** Use refurbished hardware where
  possible. Extend refresh cycles from 3 to 5 years.
- **E-waste recycling:** Partner with certified e-waste recyclers.
  Track disposal and recovery rates.
- **Modular design:** Choose hardware that supports component-level
  replacement (not full system replacement).

---

## 18. Labour Studies and Workforce Transition

This section addresses the labour studies gaps, providing workforce
transition planning, algorithmic management governance, union
engagement, job quality, and skills development.

### 18.1 Workforce transition plan

Platform migration affects jobs. A workforce transition plan must be
part of the migration model:

**Phase 1 (Assess):** Skills gap analysis. Identify current IT staff
skills and required skills for DSW operations. Identify roles that
will change (e.g., M365 admin → Linux admin).

**Phase 2 (Pilot):** Begin reskilling. Train pilot team on Nextcloud,
Collabora, Matrix, Keycloak. Document training needs and gaps.

**Phase 3 (Federate):** Scale training. Establish training programme
for all IT staff. Create internal certification. Begin recruiting for
new roles (AI operations, security engineering).

**Phase 4 (Scale):** Full workforce transition. All IT staff trained.
New roles filled. Vendor support contracts reduced as internal
capacity grows.

**Phase 5 (Sustain):** Continuous skills development. Annual training
budget. Contribution to open-source community (skills development +
reputation).

### 18.2 Algorithmic management governance

The AI layer (§10.4) could enable algorithmic management (performance
monitoring, productivity tracking, automated assessment). Governance
must prevent misuse:

- **Prohibited uses:** No AI-based performance evaluation of staff
  without explicit consent and union agreement. No automated
  disciplinary action based on platform usage data.
- **Permitted uses:** AI-assisted (not AI-decided) support for
  research, teaching, and administration. Human-in-the-loop for all
  consequential decisions.
- **Transparency:** Staff must know what data is collected, how it is
  used, and who has access. No hidden monitoring.
- **Data minimisation:** Collect only data necessary for service
  operation. Do not repurpose operational data for surveillance.
- **Union agreement:** Any algorithmic management tool must be
  agreed with staff representatives before deployment.

### 18.3 Union and worker representative engagement

- **Early engagement:** Inform and consult staff representatives
  before migration begins. Not after decisions are made.
- **Collective bargaining:** Platform changes may be subject to
  collective bargaining agreements. Legal review required.
- **Worker representatives on steering committee:** Add a staff
  representative to the steering committee (§5.4). Not just
  management and IT.
- **Feedback channels:** Anonymous feedback mechanisms for staff
  concerns about platform changes.

### 18.4 Job quality as design criterion

The DSW should be designed to improve job quality, not just
sovereignty:

- **Autonomy:** Staff should have more control over their digital
  work environment, not less.
- **Skill development:** The DSW should create opportunities for
  skill growth, not just require new skills.
- **Work-life balance:** Sovereign platforms should reduce digital
  fatigue (fewer notifications, better boundaries), not increase it.
- **Well-being:** Platform design should support psychological safety
  and reduce stress (well-being literature, 261 papers).

### 18.5 Skills development programme

- **Training curriculum:** Structured training for all stakeholder
  groups (IT staff, faculty, admin, students). Online and in-person.
  Progressive (basic → advanced).
- **Certification:** Internal certification for DSW administration.
  Recognised within the consortium.
- **Community contribution:** Staff who contribute to open-source
  projects get professional development credit.
- **Recruitment:** Hire for open-source and security skills. Adjust
  job descriptions and compensation.
- **Knowledge sharing:** Internal wiki, lunch-and-learn sessions,
  annual DSW conference within the consortium.

---

## 19. Public Policy and International Dimensions

This section addresses the public policy gaps, mapping the policy
landscape, analysing policy instruments, distinguishing sovereignty
levels, and adding international dimensions.

### 19.1 Policy landscape

| Policy | Relevance to DSW | Status |
|--------|-----------------|--------|
| GDPR (2016/679) | Data protection, residency, subject rights | In force |
| NIS2 (2022/2555) | Cybersecurity obligations for universities | Transposition by Oct 2024 |
| AI Act (2024/1689) | AI system classification and compliance | Phased implementation 2025-2027 |
| Data Governance Act (2022/868) | Data sharing and reuse frameworks | In force |
| Data Act (2023/2854) | Data access and portability | In force (Sep 2025) |
| Digital Markets Act (2022/1925) | Platform regulation (gatekeepers) | In force |
| Digital Services Act (2022/2065) | Platform accountability | In force |
| Digital Decade (2030) | EU digital targets | Ongoing |
| European Data Strategy | Data spaces, Gaia-X | Ongoing |

**NIS2 cross-reference:** NIS2 imposes cybersecurity risk management
and incident reporting obligations on universities (as "important
entities"). The security architecture (§10.3) must be NIS2-compliant:
risk assessments, security policies, incident handling, business
continuity, supply chain security, and encryption. The DSW's sovereign
architecture can simplify NIS2 compliance (full control, auditability)
but does not eliminate the obligation.

### 19.2 Policy instruments for DSW support

- **Funding:** Horizon Europe, Digital Europe, national sovereignty
  funds. DSW proposals should align with programme priorities
  (digital transformation, open science, cybersecurity).
- **Regulation:** GDPR data residency, NIS2 security, AI Act
  transparency. These create demand for sovereign solutions.
- **Procurement preferences:** Public procurement can prefer
  open-source and sovereign solutions. Some EU member states have
  open-source-first policies.
- **Standards:** Gaia-X labels, EUCS (European Cybersecurity
  Certification Scheme), EN 301 549 (accessibility). Certification
  creates trust and interoperability.
- **Research programmes:** Fund DSW research (pilots, evaluations,
  case studies) to build the evidence base.

### 19.3 Sovereignty levels and their interactions

| Level | Definition | DSW relevance |
|-------|-----------|---------------|
| Individual | Personal data control (GDPR) | Data subject rights in DSW |
| Institutional | Organisational control over data/infrastructure | Core DSW thesis |
| National | State control over digital infrastructure | National cloud initiatives, data localisation |
| European | EU digital autonomy | Gaia-X, EOSC, Digital Decade |

**Interactions:** Institutional sovereignty is nested within national
and European frameworks. A university cannot be fully sovereign if
its nation depends on foreign cloud providers. Conversely, European
sovereignty (Gaia-X) depends on institutional adoption. The DSW
operates at the institutional level but contributes to national and
European sovereignty goals.

### 19.4 International dimensions

- **Non-EU universities:** Non-EU institutions face different
  sovereignty challenges (e.g., US universities under CLOUD Act,
  Chinese universities under data security laws). The DSW model may
  need adaptation.
- **Geopolitics:** US-China tech competition affects platform
  availability and trust. Sanctions may restrict access to certain
  technologies. Universities must consider geopolitical risk in
  platform selection.
- **International collaboration:** Cross-border research requires
  data sharing across jurisdictions. Sovereign platforms must support
  international data transfer mechanisms (SCCs, adequacy decisions).
- **Global South:** Universities in developing countries face
  additional challenges (infrastructure, skills, funding). The DSW
  model must be adapted or may be infeasible.

### 19.5 Policy recommendations

For governments and funders:
1. **Fund DSW pilots** in universities (Horizon Europe, Digital
   Europe).
2. **Mandate open-source preference** in public procurement for
   educational institutions.
3. **Develop sovereign platform standards** (interoperability,
   security, accessibility) to reduce adoption risk.
4. **Support consortium formation** through funding and coordination.
5. **Invest in open-source platform development** (not just
   procurement) to address capability gaps.
6. **Create a DSW certification** (like Gaia-X labels) to give
   universities confidence in sovereign solutions.

---

## 20. User Research and Usability Framework (HCI)

This section addresses the HCI/UX gaps, providing a user research
programme, usability evaluation framework, accessibility compliance,
and onboarding strategy.

### 20.1 User research programme

Before platform selection or migration, conduct primary user research:

**Phase 1 (Assess):**
- **Contextual inquiry:** Observe how 5-10 users from each stakeholder
  group actually use current platforms. Document workflows, pain
  points, and workarounds.
- **Semi-structured interviews:** 30-60 minutes with 5-10
  representatives per group (12 groups = 60-120 interviews). Focus on
  needs, frustrations, and expectations.
- **Surveys:** Broader quantitative survey (target: 500+ responses)
  covering satisfaction with current platforms, desired features,
  willingness to migrate, and concerns.

**Phase 2 (Pilot):**
- **Usability testing:** Think-aloud protocol with 8-12 users per
  stakeholder group. Task-based (e.g., "share a document with a
  colleague at another university," "find a research paper in the
  institutional repository").
- **Diary studies:** 2-week diary study with 20-30 pilot users.
  Document daily usage, friction points, and satisfaction.

**Phase 4 (Scale):**
- **Ongoing feedback:** In-app feedback widget, quarterly surveys,
  user advisory board meetings.

### 20.2 Usability evaluation framework

**Metrics:**
- **SUS (System Usability Scale):** Target ≥68 (above average).
  Administered quarterly.
- **Task completion rate:** ≥90% for core tasks (file sharing,
  document editing, communication).
- **Task completion time:** Baseline from current platform; target
  ≤120% of baseline (allowing for learning curve).
- **Error rate:** ≤5% for core tasks.
- **NPS (Net Promoter Score):** Target ≥0 (neutral or positive).

**Methods:**
- **Heuristic evaluation:** Expert review against Nielsen's 10
  usability heuristics. Conduct before each major release.
- **Cognitive walkthrough:** Step-by-step analysis of key tasks.
  Identify where users may get stuck.
- **A/B testing:** Compare sovereign platform variants (e.g.,
  different onboarding flows) during pilot.

### 20.3 Accessibility compliance

- **Standard:** WCAG 2.2 (Level AA) and EN 301 549 (European
  accessibility standard for public-sector ICT).
- **Audit:** Third-party accessibility audit before institution-wide
  deployment. Automated testing (axe, Lighthouse) + manual testing
  (screen reader, keyboard navigation).
- **Remediation:** Fix critical and major issues before launch.
  Minor issues tracked for post-launch resolution.
- **Ongoing:** Accessibility review for each new feature. User
  testing with disabled users.
- **Assistive technology support:** Screen readers (NVDA, JAWS,
  VoiceOver), voice control, switch access, magnification.

### 20.4 Onboarding and training strategy

- **Progressive disclosure:** Start with basic features (file
  sharing, document editing). Introduce advanced features (AI
  search, workflow automation) gradually.
- **In-app guidance:** Tooltips, walkthroughs, and contextual help.
  Not just external documentation.
- **Role-based onboarding:** Different onboarding flows for
  students, faculty, admin staff, and IT staff.
- **Peer support:** "DSW champions" in each department. Peer-to-peer
  support reduces helpdesk load.
- **Multilingual:** Interface and documentation in all languages
  used by the university community.

### 20.5 Multilingual support

- **Interface languages:** All languages used by the university
  community (minimum: English + local language).
- **Document translation:** AI-powered translation (sovereign,
  on-premise) for documents and communications.
- **AI multilingual:** Sovereign RAG must support queries and
  responses in multiple languages (BGE-M3 embedding model supports
  100+ languages).

---

## 21. Cross-Disciplinary Synthesis (Updated)

### 21.1 Integration of all disciplinary perspectives

The paper now covers 10 disciplinary perspectives:

| # | Discipline | Section | Status |
|---|-----------|---------|--------|
| 1 | Information Systems | §9 | Publication standard |
| 2 | Computer Science | §10 | Publication standard |
| 3 | Law | §11 | Publication standard |
| 4 | Economics | §12 | Publication standard |
| 5 | Organizational Behavior | §14 | Framework-level |
| 6 | Higher Education Policy | §15 | Framework-level |
| 7 | Archival Science | §16 | Framework-level |
| 8 | Green IT | §17 | Framework-level |
| 9 | Labour Studies | §18 | Framework-level |
| 10 | Public Policy | §19 | Framework-level |
| 11 | HCI/UX | §20 | Framework-level |

**Integration principle:** The four "publication standard" sections (§9-12)
provide analytical depth. The seven "framework-level" sections (§14-20)
provide structured coverage that can be deepened in future work. This
balances breadth and depth.

### 21.2 Remaining limitations (updated)

All limitations from §7.4 still apply, plus:
- **No empirical validation:** Still a proposal, not an evidence-based
  study. Primary user research, cost data, and security assessment
  are needed.
- **Framework-level depth:** Seven sections (§14-20) are
  framework-level, not publication-standard. They identify what needs
  to be done but do not provide deep analysis.
- **Scope:** The paper now has 21 sections. Consider whether this is
  one paper or a research programme. A companion paper structure may
  be more appropriate.

### 21.3 Revised paper status

This revision (Rev 4) addresses all key findings from both review
rounds:
- ✅ Structural imbalance: addressed by adding framework-level sections
  that parallel the deep-integrated sections, creating a more balanced
  structure.
- ✅ OB/change management: §14 provides Kotter/ADKAR frameworks,
  culture analysis, resistance management, leadership, and
  organisational learning.
- ✅ HE policy/open science: §15 connects DSW to EUA, LERU, UNESCO,
  EOSC, OpenAIRE, CoARA/DORA, and teaching/learning.
- ✅ EdTech/teaching-learning: §15.4 addresses digital pedagogy, LMS
  sovereignty, learning analytics, assessment integrity, UDL, and
  equity.
- ✅ Digital preservation: §16 provides OAIS framework, retention
  policies, metadata standards, format strategy, and repository
  integration.
- ✅ Environmental sustainability: §17 provides carbon footprint
  analysis, sustainability metrics, energy-efficient AI, and circular
  economy.
- ✅ Labour studies: §18 provides workforce transition, algorithmic
  management governance, union engagement, job quality, and skills
  development.
- ✅ Public policy: §19 maps the policy landscape, analyses
  instruments, distinguishes sovereignty levels, adds international
  dimensions, and provides policy recommendations.
- ✅ HCI/UX: §20 provides user research programme, usability
  evaluation, accessibility compliance, onboarding, and multilingual
  support.
- ⚠️ User research: Framework provided (§20.1) but no actual research
  conducted. Still a limitation.
- ⚠️ Cost quantification: Framework provided (§12.1) but no empirical
  data. Still a limitation.
- ⚠️ Policy landscape: Mapped (§19.1) but not deeply analysed.

---

*This paper is Revision 4 (all key findings from both review rounds
addressed). It synthesises findings from the Digital Sovereign
Workplace research corpus (3,030 papers, frozen snapshot 2026-10-31).
Contributions, corrections, and extensions are welcome.*

---

## References

### Full bibliographic entries (selected key works)

1. Governed Sovereign RAG for Public Administration: Tripartite Epistemic
   Routing, Facet-Guided Clustering. arXiv:2610.36561 (2026).
2. Policy-Driven AI in Dataspaces: Taxonomy, Explainability, and Pathways
   for Compliance. arXiv:2507.20014 (2025).
3. CYBERFORT: A Compliance-Chain Platform Operationalising the Cyber
   Resilience Act for SMEs. arXiv:2610.09918 (2026).
4. ClinConNet: A Blockchain-based Dynamic Consent Management Platform for
   Clinical Research. arXiv:2602.02610 (2026).
5. PANEL: An Open-Source, Self-Hosted Web Platform for Human Evaluation of
   Generative AI. arXiv:2609.31392 (2026).
6. Steps towards a digital sovereignty. Zenodo (2026).
   DOI: 10.5281/zenodo.23001705
7. FLAI Protocol: Decentralised Federated Learning with On-Chain Rewards.
   arXiv:2610.17546 (2026).
8. Human-Centred AI and Employee Well-Being: The Mediating Role of
   Psychological Safety. JBII (2026).
9. Digital Skills Are Not Enough: Digital-Human Capability Profiles and
   Employee Resilience. Merits (2026).
10. Employee-Office Workplace Alignment in Hybrid Work Settings.
    TU Darmstadt (2026).
11. Automated Extraction of Records of Processing Activities (RoPA) Using
    Hybrid RAG. arXiv:2609.27359 (2026).
12. Privacy-Preserving Federated Learning for Medical Imaging.
    arXiv:2610.27470 (2026).
13. Evaluating Federated Vision-Language Models for Privacy-Aware Breast
    Cancer Imaging. arXiv:2610.36379 (2026).
14. Combining Homomorphic Encryption and Differential Privacy in Federated
    Learning. arXiv:2610.01650 (2026).
15. From Pilots to Production: Lessons in Cross-Institutional Federated
    Training. arXiv:2609.39803 (2026).

### Literature streams (corpus paper counts)

1. Data Sovereignty (64) — sovereign cloud, data spaces, self-hosted
   platforms, federated computation.
2. Open Source (305) — self-hosting, platform governance, community
   dynamics, sustainability.
3. Federated & Privacy-Preserving (101) — federated learning, HE, DP,
   consent management.
4. AI & Language Models (280) — sovereign RAG, multi-agent systems, AI
   governance, productivity.
5. Employee Well-Being (261) — digital fatigue, algorithmic management,
   psychological safety, psychosocial risk.
6. Hybrid & Remote Work (183) — spatial dynamics, productivity, fatigue,
   public-sector hybrid work.
7. Digital Transformation & Adoption (382 combined) — capability profiles,
   adoption paradox, SME adoption, AI-enabled HRM.
8. Identity & Access (40) — federated identity, cross-border credentials,
   SSO/OIDC/SAML.
9. Interoperability & Standards (238) — data spaces, standards,
   cross-border credential friction.
10. Public Sector & Education (154) — public-sector transformation, digital
    skills, E-HRM.
11. Security & Compliance (48) — CRA compliance, consent management,
    compliance automation.
12. Collaboration & Productivity (79) — sovereign collaboration,
    communication theories, data spaces.
13. Tooling & Platforms (179) — platform evaluation, operational frameworks.
14. Evaluation & Case Studies (204) — empirical evaluation methods, case
    study designs.
15. Surveys & Reviews (221) — systematic reviews, bibliometric analyses.
16. Methods (195) — research methodologies for digital workplace studies.

---

*This paper is Revision 4 (all key findings from both review rounds
addressed). It synthesises findings from the Digital Sovereign
Workplace research corpus (3,030 papers, frozen snapshot 2026-10-31).
Contributions, corrections, and extensions are welcome.*
