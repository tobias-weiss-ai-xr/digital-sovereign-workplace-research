# Towards a Digital Sovereign Workplace for Universities: Stakeholder Needs, Migration Path, and Governance

**Authors:** Digital Sovereign Workplace Research Corpus  
**Date:** 2026-10-31  
**Corpus basis:** 3,030 papers across 19 categories (frozen snapshot: 2026-10-31)  
**Status:** Working paper / draft for review (Revision 2 — all critical review fixes applied)

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
research, unquantified costs, and corpus quality issues.

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

*This paper is Revision 2 (all critical review fixes applied). It
synthesises findings from the Digital Sovereign Workplace research corpus
(3,030 papers, frozen snapshot 2026-10-31). Contributions, corrections,
and extensions are welcome.*
