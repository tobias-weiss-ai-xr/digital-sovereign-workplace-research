# Multi-Perspective Critical Review: "Towards a Digital Sovereign Workplace for Universities" (Rev 2)

**Reviewers:** Multi-disciplinary review panel  
**Date:** 2026-10-31  
**Paper reviewed:** `docs/research/digital_sovereign_workplace_universities.md` (Rev 2)  
**Format:** Disciplinary perspective reviews with cross-cutting synthesis

---

## Preamble

This review examines the revised paper (Rev 2) from ten disciplinary
perspectives. Each reviewer assesses the paper's strengths, weaknesses,
and blind spots from their field's standpoint. A cross-cutting synthesis
identifies convergent themes and unresolved tensions.

**Overall assessment:** Rev 2 is a substantial improvement over the
original draft. The addition of counter-evidence, SMART criteria, power
dynamics, and three-tier technology classification significantly
strengthens the paper. However, disciplinary-specific gaps remain.

---

## 1. Information Systems (IS) Perspective

**Reviewer lens:** Socio-technical systems, IT governance, enterprise
architecture, IS adoption.

### Strengths

- The paper correctly frames DSW as a socio-technical system, not merely a
  technical migration. The stakeholder analysis captures the social
  dimension well.
- The five-layer technology stack maps cleanly onto enterprise architecture
  layers (infrastructure, identity, application, AI, security).
- The migration path follows established IS implementation frameworks
  (assess → pilot → scale → sustain), consistent with IS change management
  literature.

### Weaknesses

1. **Missing enterprise architecture framework.** The paper does not
   reference or align with established EA frameworks for universities
   (TOGAF, ArchiMate, or the JISC Enterprise Architecture model). The
   technology stack would benefit from EA layering and dependency mapping.

2. **No IT governance model.** The paper proposes a steering committee but
   does not address IT governance mechanisms (decision rights, accountability
   frameworks, performance measurement). COBIT or ITIL alignment would
   strengthen the governance section.

3. **Socio-technical systems theory is underutilised.** Leavitt's diamond
   (technology, people, structure, tasks) or the SSM (Soft Systems
   Methodology) could frame the stakeholder analysis more rigorously. The
   paper treats technology and people as separate concerns rather than
   co-evolving.

4. **Missing: IT-business alignment.** The paper does not address how DSW
   aligns with university strategic plans, academic mission, or research
   strategy. IT alignment theory (Henderson & Venkatraman) is absent.

5. **No IS success model.** The paper does not reference DeLone & McLean
   IS success model or similar frameworks for evaluating platform success
   (system quality, information quality, service quality, use, satisfaction,
   net benefits).

### Recommendations

- Add an enterprise architecture alignment section.
- Reference IS success models for evaluation criteria.
- Frame the migration as socio-technical co-evolution, not sequential phases.

---

## 2. Computer Science Perspective

**Reviewer lens:** Distributed systems, security engineering, AI/ML,
software architecture.

### Strengths

- The three-tier technology classification (available now / emerging /
  research stage) is technically honest and useful.
- The capability comparison table, while not empirically validated, provides
  a reasonable feature-level assessment.
- Federated learning and privacy-preserving computation are correctly
  identified as research-stage for university workplaces.

### Weaknesses

1. **No system architecture.** The paper proposes a "five-layer technology
   stack" but does not provide a system architecture diagram, component
   interaction model, or deployment topology. How do the layers interact?
   What are the API boundaries? What are the data flows?

2. **Missing: scalability analysis.** Universities have 10,000–100,000
   users. The paper does not address whether Nextcloud, Collabora, or Matrix
   can scale to this level, what infrastructure is required, or what
   performance benchmarks exist.

3. **Security architecture is superficial.** The security-compliance
   literature (48 papers) is cited but not engaged. The paper mentions
   "security audit" and "penetration testing" without specifying:
   - Threat model (STRIDE or similar)
   - Security controls (encryption at rest/transit, key management, HSM)
   - Incident response procedures
   - Zero-trust architecture considerations

4. **AI architecture is underspecified.** "Sovereign RAG" is mentioned
   but not architected. What LLM? What embedding model? What vector store?
   What is the inference infrastructure (GPU requirements)? How is
   model updates handled? The Governed Sovereign RAG paper
   (arXiv:2610.36561) is cited but not analysed for technical
   applicability.

5. **No data model.** The paper does not address how data is structured,
   stored, or migrated between systems. Data migration is the hardest part
   of platform transitions.

6. **Missing: observability and monitoring.** No mention of logging,
   metrics, tracing, or alerting for the sovereign stack.

### Recommendations

- Add a system architecture section with component diagram and data flows.
- Include scalability benchmarks or estimates.
- Develop a security threat model.
- Specify AI infrastructure requirements.
- Add a data migration strategy.

---

## 3. Law and Data Protection Perspective

**Reviewer lens:** GDPR, data protection law, digital sovereignty law,
contract law, public procurement.

### Strengths

- The paper correctly identifies GDPR compliance, data residency, and
  auditability as DPO priorities.
- The inclusion of DPOs as a distinct stakeholder group is appropriate.
- The paper acknowledges jurisdictional risk from extra-territorial hosting.

### Weaknesses

1. **GDPR analysis is shallow.** The paper mentions GDPR but does not
   address:
   - Lawful basis for processing (Art. 6) and special category data
     (Art. 9) in a sovereign context.
   - Data Protection Impact Assessment (DPIA) requirements for new
     platforms (Art. 35).
   - Data subject rights (access, erasure, portability) implementation.
   - Cross-border data transfer mechanisms (SCCs, adequacy decisions,
     BCRs) for federated collaboration.
   - Controller/processor relationships in a self-hosted model.

2. **No legal analysis of "digital sovereignty."** The term is used
   throughout but never legally defined. What does "sovereignty" mean in
   law? Is it a legal concept or a political one? The paper conflates
   technical control, legal jurisdiction, and political autonomy.

3. **Public procurement law is absent.** Universities are public bodies
   subject to procurement regulations (EU Directive 2014/24/EU). The
   paper's "procurement and finance" stakeholder section mentions
   "tender-ready documentation" but does not address:
   - Open-source procurement challenges (no standardised contracts).
   - Vendor evaluation criteria for open-source vs. proprietary.
   - Legal risk of vendor dependency on open-source distributions.

4. **Missing: academic freedom as a legal right.** The paper asserts
   academic freedom is compromised by proprietary platforms but does not
   cite legal frameworks (European Court of Human Rights, national
   constitutional provisions) or case law.

5. **No analysis of AI regulation.** The EU AI Act (2024) classifies
   AI systems by risk. Sovereign AI in universities (student assessment,
   research analysis) may fall under high-risk categories. The paper
   ignores this.

### Recommendations

- Add a legal analysis section addressing GDPR implementation in sovereign
  contexts.
- Define "digital sovereignty" legally and distinguish from technical control.
- Address public procurement law for open-source platforms.
- Add EU AI Act implications for sovereign AI in universities.

---

## 4. Organizational Behavior and Management Perspective

**Reviewer lens:** Change management, organisational culture, power
dynamics, resistance, leadership.

### Strengths

- The power dynamics analysis (§2.13) is a significant improvement over
  the original draft. Acknowledging that IT departments control
  implementation and students have least power is important.
- The shadow IT insight (unmet needs, not user failure) is well-founded.
- The five-phase model includes change management activities in Phase 4.

### Weaknesses

1. **Change management is underdeveloped.** Phase 4 mentions "training,
   communication, resistance handling" but does not draw on established
   change management frameworks (Kotter's 8 steps, ADKAR, Lewin's
   unfreeze-change-refreeze). The organisational change literature is
   rich and relevant.

2. **No organisational culture analysis.** Universities have distinct
   cultures (collegial governance, academic autonomy, disciplinary silos).
   The paper does not address how DSW adoption interacts with these
   cultures. For example: will faculty accept a centrally mandated
   platform? How do disciplinary differences (STEM vs. humanities) affect
   platform needs?

3. **Missing: leadership and sponsorship.** The paper identifies
   "university leadership" as a stakeholder but does not address the
   critical role of executive sponsorship in large-scale IT change. Who
   champions DSW? What happens when leadership changes?

4. **No resistance analysis.** The paper mentions "resistance handling"
   but does not identify specific resistance sources:
   - IT staff resistance (job security, skill obsolescence).
   - Faculty resistance (tool preference, academic freedom concerns).
   - Vendor resistance (loss of revenue, relationship disruption).
   - Student resistance (learning curve, reduced capability).

5. **Missing: organisational learning.** The paper does not address how
   the university learns from the migration experience, captures knowledge,
   or builds institutional capability for ongoing platform management.

### Recommendations

- Integrate established change management frameworks.
- Add organisational culture analysis.
- Develop a resistance management plan.
- Address leadership sponsorship and succession.

---

## 5. Higher Education Policy Perspective

**Reviewer lens:** Higher education governance, university mission,
academic freedom, research policy, open science.

### Strengths

- The paper correctly identifies universities as distinct from enterprises
  and frames DSW in terms of university mission and values.
- The open science alignment argument is compelling.
- The public-sector stakeholder group captures government and funding
  body perspectives.

### Weaknesses

1. **No higher education policy framework.** The paper does not reference
   relevant HE policy frameworks:
   - European University Association (EUA) digital transformation agenda.
   - League of European Research Universities (LERU) position on open
     science.
   - UNESCO recommendations on open educational resources.
   - National digital sovereignty strategies (e.g., Germany's Sovereign
     Tech Fund, France's DINUM).

2. **Missing: open science infrastructure.** The paper mentions "open
   science alignment" but does not connect DSW to existing open science
   infrastructure (EOSC, OpenAIRE, Zenodo, ORCID). How does a sovereign
   workplace integrate with these?

3. **No analysis of research assessment.** Research assessment reform
   (CoARA, DORA) affects how researchers use digital tools. The paper
   does not address how DSW supports or hinders new assessment practices.

4. **Missing: teaching and learning.** The paper mentions LMS integration
   but does not address:
   - Digital pedagogy and sovereign tools for teaching.
   - Student digital literacy.
   - Assessment integrity (plagiarism detection, exam proctoring).
   - Accessibility in learning (universal design for learning).

5. **No funding body perspective.** Major funders (ERC, Horizon Europe,
   national research councils) have data management and open access
   requirements. How does DSW help researchers meet these?

### Recommendations

- Add a higher education policy alignment section.
- Connect DSW to open science infrastructure.
- Address teaching and learning implications.
- Include funding body requirements.

---

## 6. Economics Perspective

**Reviewer lens:** Cost-benefit analysis, TCO, market failure, platform
economics, public goods.

### Strengths

- The paper acknowledges the absence of quantified cost analysis (an
  improvement over the original).
- The funding mechanisms section identifies public funding and
  institutional budget reallocation.
- The consortium model addresses economies of scale.

### Weaknesses

1. **No economic model.** The paper does not provide any economic
   analysis:
   - No TCO comparison (even estimated ranges).
   - No cost-benefit analysis framework.
   - No break-even analysis for migration investment.
   - No sensitivity analysis for key cost drivers.

2. **Missing: platform economics.** The paper does not analyse the
   economics of platform markets:
   - Network effects and lock-in (why proprietary platforms dominate).
   - Switching costs (data migration, retraining, integration).
   - Economies of scale in cloud infrastructure.
   - Two-sided market dynamics (users vs. developers).

3. **No public goods analysis.** Open-source platforms have public good
   characteristics (non-rivalrous, partially non-excludable). The paper
   does not analyse the free-rider problem or how to fund public goods
   provision.

4. **Missing: market failure analysis.** Why does the market not provide
   sovereign workplace platforms? The paper assumes sovereignty is
   desirable but does not analyse why the market underprovides it (e.g.,
   positive externalities of data control, information asymmetry, vendor
   market power).

5. **No incentive analysis.** The paper proposes "upstream contribution"
   but does not analyse incentives for contribution. Why would a
   university contribute to open-source rather than free-ride?

### Recommendations

- Add a TCO estimation framework with illustrative ranges.
- Analyse platform market economics and lock-in.
- Frame open-source platforms as public goods with funding implications.
- Analyse incentives for upstream contribution.

---

## 7. Sociology of Technology (STS) Perspective

**Reviewer lens:** Technology and society, actor-network theory, social
shaping of technology, digital inequality.

### Strengths

- The stakeholder analysis captures social dimensions of technology
  adoption.
- The power dynamics section acknowledges asymmetries.
- The well-being implications discussion is a good STS insight.

### Weaknesses

1. **No social shaping analysis.** The paper treats technology as a
   neutral tool to be adopted, not as a social construct that shapes and
   is shaped by its users. STS would ask: How does the choice of platform
   shape academic work? How does it reshape power relations within the
   university?

2. **Missing: digital inequality.** The paper mentions student equity
   but does not analyse:
   - Digital divide within the student body (device quality, connectivity).
   - Accessibility for disabled students and staff.
   - Language and cultural barriers (non-English interfaces).
   - Gender and intersectional effects of platform design.

3. **No actor-network analysis.** The paper identifies stakeholders but
   does not map the network of actors (humans and non-humans) that
   constitute the DSW. How do platforms, standards, regulations, and
   people co-constitute the sovereign workplace?

4. **Missing: surveillance and control.** The paper frames sovereignty as
   control but does not analyse how sovereign platforms might also be
   used for surveillance (e.g., activity monitoring, productivity
   tracking). The well-being literature raises this concern.

5. **No analysis of "sovereignty" as a political concept.** The paper
   uses "sovereignty" technically but does not engage with its political
   dimensions: national sovereignty, institutional autonomy, individual
   self-determination, and their tensions.

### Recommendations

- Add a social shaping analysis of platform choice.
- Deepen digital inequality analysis.
- Map actor networks in the DSW ecosystem.
- Address surveillance risks in sovereign platforms.
- Analyse "sovereignty" as a contested political concept.

---

## 8. Security Engineering Perspective

**Reviewer lens:** Threat modelling, security architecture, risk
assessment, compliance engineering.

### Strengths

- The security-compliance stakeholder group is well-defined.
- The paper mentions security audits and penetration testing.
- The three-tier classification correctly identifies security-relevant
  technologies.

### Weaknesses

1. **No threat model.** The paper does not define what threats the
   sovereign stack is designed to counter. Without a threat model, security
   claims are unfounded. Key threats for university DSW:
   - Data breach (external attacker, insider threat).
   - Data exfiltration (to non-EU jurisdictions).
   - Account compromise (phishing, credential stuffing).
   - Supply chain attack (compromised open-source dependencies).
   - Ransomware (encryption of institutional data).
   - Surveillance (state or corporate monitoring).

2. **No security architecture.** The paper does not specify:
   - Encryption standards (at rest, in transit, end-to-end).
   - Key management (HSM, key rotation, escrow).
   - Authentication (MFA, passwordless, hardware tokens).
   - Network segmentation (zero-trust, micro-segmentation).
   - Backup and disaster recovery.

3. **Supply chain security is ignored.** Open-source platforms depend on
   thousands of dependencies. The paper does not address:
   - Dependency auditing (SBOM, vulnerability scanning).
   - Software composition analysis.
   - Reproducible builds.
   - Vendor security assessment for open-source distributions.

4. **No incident response plan.** The paper mentions "incident response"
   as a DPO need but does not propose a response framework.

5. **Missing: security vs. usability trade-off.** Stronger security
   (MFA, encryption) reduces usability. The paper does not address this
   tension.

### Recommendations

- Develop a threat model (STRIDE or similar).
- Specify security architecture and controls.
- Add supply chain security analysis.
- Propose an incident response framework.
- Address security-usability trade-offs.

---

## 9. Human-Computer Interaction (HCI) / UX Perspective

**Reviewer lens:** Usability, user experience, accessibility, interaction
design, user research.

### Strengths

- The student needs section now includes accessibility, mobile, and
  offline considerations (Rev 2 improvement).
- The paper acknowledges that platform friction affects productivity and
  well-being.
- User advisory board is proposed as a governance mechanism.

### Weaknesses

1. **No user research methodology.** The paper infers user needs from
   literature but does not propose primary user research (interviews,
   surveys, usability testing, contextual inquiry). HCI would demand
   empirical user research before platform selection.

2. **No usability evaluation framework.** The paper mentions "user
   satisfaction" as a success criterion but does not specify:
   - Usability metrics (task completion time, error rate, SUS score).
   - Evaluation methods (heuristic evaluation, cognitive walkthrough,
     user testing).
   - Accessibility standards (WCAG 2.2, EN 301 549).

3. **Missing: interaction design.** The paper does not address how the
   sovereign stack's user interface should be designed to:
   - Match user expectations (familiarity with proprietary platforms).
   - Reduce cognitive load during migration.
   - Support diverse user populations (multilingual, multi-device).

4. **No accessibility audit.** The paper mentions "assistive technologies"
   but does not propose an accessibility audit or compliance verification
   against EN 301 549 (European accessibility standard).

5. **Missing: user onboarding and training.** The paper mentions
   "training" but does not design onboarding flows, progressive
   disclosure, or in-app guidance for new users.

### Recommendations

- Propose a user research programme (interviews, surveys, usability tests).
- Define usability evaluation framework with specific metrics.
- Add accessibility compliance verification.
- Design onboarding and training strategy.

---

## 10. Public Policy and Digital Sovereignty Perspective

**Reviewer lens:** Digital sovereignty policy, public administration,
EU digital strategy, national sovereignty initiatives.

### Strengths

- The paper frames DSW in terms of institutional autonomy and public
  mission, which resonates with digital sovereignty policy discourse.
- The Gaia-X/IDSA references connect to EU digital sovereignty
  initiatives.
- The public-sector stakeholder group captures government perspectives.

### Weaknesses

1. **No policy landscape analysis.** The paper does not map the policy
   environment:
   - EU Digital Decade targets (2030).
   - European Data Strategy and Data Governance Act.
   - NIS2 Directive (cybersecurity).
   - AI Act (AI regulation).
   - Digital Markets Act (platform regulation).
   - National digital sovereignty strategies.

2. **Missing: policy instruments.** The paper proposes a consortium model
   but does not analyse policy instruments that could support DSW:
   - Public procurement preferences for open-source.
   - Funding programmes (Horizon, Digital Europe, national).
   - Regulatory mandates (data residency requirements).
   - Standards and certification (Gaia-X labels, EUCS).

3. **No analysis of sovereignty levels.** "Digital sovereignty" operates
   at multiple levels (individual, institutional, national, European).
   The paper conflates these. A university's sovereignty is nested within
   national and European sovereignty frameworks.

4. **Missing: international dimension.** The paper focuses on European
   context but does not address:
   - How non-EU universities approach sovereignty.
   - International data transfer and collaboration.
   - Geopolitical dimensions (US-China tech competition, sanctions).

5. **No policy recommendation.** The paper is descriptive, not
   prescriptive for policymakers. What should governments do to support
   university DSW adoption?

### Recommendations

- Add a policy landscape section mapping relevant EU and national policies.
- Analyse policy instruments for DSW support.
- Distinguish sovereignty levels (individual/institutional/national/EU).
- Add international and geopolitical dimensions.
- Include policy recommendations for governments and funders.

---

## Cross-Cutting Synthesis

### Convergent themes (identified by ≥3 disciplines)

1. **The paper lacks empirical grounding.** IS, economics, HCI, and
   security all note the absence of empirical data (user research, cost
   analysis, security assessment, usability testing). The paper is a
   proposal, not an evidence-based study.

2. **Stakeholder analysis needs deepening.** OB, STS, and HCI all note
   that stakeholder needs are inferred from literature, not primary
   research. Power dynamics, culture, and user experience are
   underdeveloped.

3. **Technology stack needs architecture.** CS, IS, and security all
   note the absence of system architecture, scalability analysis, and
   security design. The stack is a list, not an architecture.

4. **Governance is underdeveloped.** IS, OB, and public policy all note
   that governance mechanisms are proposed but not analysed. Consortium
   governance, IT governance, and policy frameworks are missing.

5. **The paper should be more honest about its limitations.** All
   disciplines note that the paper overstates confidence in some areas
   (sovereignty benefits, migration feasibility) while understating in
   others (costs, risks, capability gaps).

### Divergent perspectives (disciplines disagree)

1. **On the pace of migration:** CS and security want slower, more
   careful migration with extensive testing. OB and HE policy want
   faster adoption to avoid falling further behind. Economics is neutral
   but wants cost data first.

2. **On the role of proprietary platforms:** Economics and IS see value
   in hybrid models. STS and public policy are more skeptical of any
   proprietary dependency. CS is pragmatic (use what works).

3. **On the definition of "sovereignty":** Law wants a precise legal
   definition. CS wants a technical definition. STS wants a political
   definition. Public policy wants a policy definition. The paper
   conflates all four.

### Unresolved tensions

1. **Sovereignty vs. capability** (all disciplines) — remains the
   central unresolved tension. No discipline has a clear answer.

2. **Resource constraints vs. ambitious scope** (economics, OB) — the
   paper proposes a 48-month migration with 12 stakeholder groups and
   5 technology layers, but universities are resource-constrained.

3. **Open-source idealism vs. operational reality** (CS, economics,
   security) — open-source platforms require significant operational
   capacity that universities may not have.

4. **Institutional autonomy vs. federation** (law, public policy) —
   sovereignty at the institutional level may conflict with federation
   at the European level.

### Priority recommendations (cross-disciplinary)

1. **Define "digital sovereignty" precisely** — legal, technical,
   political, and policy dimensions.
2. **Add system architecture** — component diagram, data flows,
   scalability analysis, security design.
3. **Conduct primary user research** — interviews, surveys, usability
   tests with all 12 stakeholder groups.
4. **Quantify costs** — TCO framework with illustrative ranges.
5. **Develop a threat model** — STRIDE-based security analysis.
6. **Map the policy landscape** — EU and national policies, instruments,
   and recommendations.
7. **Integrate change management frameworks** — Kotter, ADKAR, resistance
   management.
8. **Connect to open science infrastructure** — EOSC, OpenAIRE, ORCID.
9. **Add usability evaluation framework** — metrics, methods, accessibility
   standards.
10. **Analyse platform market economics** — lock-in, switching costs,
    public goods.

---

## Conclusion

The paper has improved substantially in Rev 2 but remains a proposal
rather than an evidence-based study. The multi-disciplinary review
reveals that the paper's greatest strength (breadth of stakeholder
analysis) is also its greatest weakness (depth of any single dimension).
A credible academic paper would need to narrow its scope or add
substantial empirical and analytical depth in at least 3–4 of the
dimensions identified above.

**Recommended next step:** Select 3–4 disciplinary perspectives for deep
integration (recommended: IS, CS, Law, Economics) and develop those
sections to publication standard. Use the remaining perspectives as
future work or collaborative extensions.

**Status update (Rev 3):** The recommended deep-integration has been
completed. Sections 9–13 of the paper now provide publication-standard
coverage of:
- Information Systems (§9): enterprise architecture, IT governance,
  socio-technical co-evolution, IS-business alignment, IS success model.
- Computer Science (§10): system architecture, scalability, STRIDE threat
  model, AI architecture, data migration, observability.
- Law (§11): GDPR implementation, legal definition of sovereignty,
  procurement law, academic freedom, EU AI Act.
- Economics (§12): TCO framework, platform market economics, public
  goods, market failure, incentive analysis.
- Cross-disciplinary synthesis (§13): interaction matrix, remaining
  gaps, revised status.

Remaining disciplinary gaps (OB, HE policy, STS, HCI, public policy)
are identified as future work in §13.2.

---

*This review was generated by a multi-disciplinary review panel. Each
perspective represents a distinct disciplinary lens applied to the same
document. Convergent themes indicate robust findings; divergent
perspectives indicate areas requiring further research.*
MDEOF
echo "Written"