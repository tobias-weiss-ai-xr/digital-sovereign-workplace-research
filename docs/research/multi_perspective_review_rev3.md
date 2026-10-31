# Multi-Perspective Critical Review (Rev 3): "Towards a Digital Sovereign Workplace for Universities"

**Reviewers:** Multi-disciplinary review panel (second round)  
**Date:** 2026-10-31  
**Paper reviewed:** `docs/research/digital_sovereign_workplace_universities.md` (Rev 3)  
**Focus:** The six disciplines not deep-integrated in Rev 3, plus four new
disciplinary perspectives not covered in the first review round.

---

## Preamble

Rev 3 deep-integrated four disciplines (IS, CS, Law, Economics) to
publication standard, adding ~840 lines of analytical depth. The paper
now stands at 1,656 lines with 13 sections. This review examines whether
the remaining gaps identified in the first multi-perspective review have
been addressed, identifies new issues introduced by the Rev 3 additions,
and brings four new disciplinary lenses to bear.

**Overall assessment:** Rev 3 is a substantial advance. The IS, CS, Law,
and Economics sections are genuinely publication-quality and address the
most critical analytical gaps. However, the paper's structure has become
imbalanced: the four deep-integrated sections (§9–12) are now more
detailed than the core sections (§2–5), creating a "tail wagging the
dog" effect. The remaining six disciplines (OB, HE policy, STS,
security, HCI, public policy) are still only superficially addressed.
Four new perspectives (EdTech, archival science, green IT, labour studies)
reveal additional gaps.

---

## Part I: Review of the Six Remaining Disciplines (from first review)

### 1. Organizational Behavior (OB) Perspective

**Reviewer lens:** Change management, organisational culture, resistance,
leadership, organisational learning.

**Status after Rev 3:** UNADDRESSED. The Rev 3 additions (IS, CS, Law,
Economics) do not touch OB concerns. The paper's change management
remains at the "training, communication, resistance handling" level
(§4, Phase 4) without frameworks.

**New observations post-Rev 3:**

1. **The IS governance section (§9.2) creates new OB concerns.** The RACI
   matrix and COBIT alignment assume rational, structured decision-making.
   Universities are collegial organisations with diffuse authority. The
   governance model may not survive contact with academic politics. OB
   would ask: who actually has power, and how is it exercised informally?

2. **The TCO analysis (§12.1) ignores change management costs.** Training,
   communication, and resistance management are listed as cost components
   (€30-50/user/year) but not analysed. OB literature shows that change
   management costs often exceed technical costs in large IT
   transformations (McKinsey: 70% of change programmes fail due to
   people issues).

3. **The migration path (§4) still lacks resistance analysis.** The
   counter-evidence section (§6) addresses capability gaps but not
   organisational resistance. Specific resistance sources (IT staff job
   security, faculty tool preference, vendor relationship disruption)
   are listed in the first review but not in the paper.

4. **No organisational culture analysis.** Universities have distinct
   cultures (collegial governance, academic autonomy, disciplinary
   silos). The DSW adoption will interact differently with STEM
   (computational research, HPC integration) vs. humanities (document-
   centric workflows, less technical infrastructure). This is not
   addressed.

5. **Missing: leadership succession.** The paper identifies "university
   leadership" as a stakeholder but does not address what happens when
   leadership changes mid-migration (a realistic scenario over a
   48-month timeline).

**Recommendations (unchanged from first review, still unaddressed):**
- Integrate Kotter's 8-step model or ADKAR into Phase 4.
- Add organisational culture analysis (collegial governance, disciplinary
  differences).
- Develop a resistance management plan with specific sources and
  mitigations.
- Address leadership sponsorship and succession planning.

**Grade impact:** OB perspective remains at C. No improvement from Rev 2.

---

### 2. Higher Education Policy Perspective

**Reviewer lens:** HE governance, university mission, academic freedom,
research policy, open science.

**Status after Rev 3:** PARTIALLY ADDRESSED. The Law section (§11.4)
now cites ECHR Art. 10, EU Charter Art. 13, and national constitutional
provisions for academic freedom. The Economics section (§12.3) mentions
public goods. But HE policy frameworks (EUA, LERU, UNESCO) and open
science infrastructure connections are still absent.

**New observations post-Rev 3:**

1. **The legal definition of sovereignty (§11.2) is useful but creates
   a tension with HE policy.** The paper recommends replacing "digital
   sovereignty" with specific legal obligations. But HE policy discourse
   uses "sovereignty" as a political concept (institutional autonomy,
   academic freedom). The recommendation to de-politicise the term may
   reduce the paper's resonance with HE policymakers and funders who
   use sovereignty as a rallying concept.

2. **The TCO framework (§12.1) does not address funding body
   requirements.** Major funders (ERC, Horizon Europe) have data
   management and open access requirements. A DSW that helps researchers
   meet these requirements has economic value that the TCO analysis
   should capture (e.g., reduced compliance burden, improved grant
   competitiveness).

3. **The consortium model (§5.1) references EOSC but does not connect
   DSW to it.** EOSC is the EU's flagship open science infrastructure.
   A sovereign workplace that integrates with EOSC (data deposition,
   service discovery, identity federation) would have significant policy
   value. This connection is mentioned but not developed.

4. **Missing: CoARA/DORA research assessment reform.** The paper mentions
   "research assessment" in the first review but not in Rev 3. CoARA
   (Coalition for Advancing Research Assessment) and DORA (Declaration
   on Research Assessment) are reshaping how research is evaluated.
   DSW tools (open-source platforms, transparent metrics) align with
   these reforms. This is a missed policy connection.

5. **Missing: teaching and learning.** Still not addressed. LMS
   integration is mentioned as "missing from the stack" (§3.1) but no
   pedagogical analysis of how sovereign tools affect teaching quality,
   student engagement, or assessment integrity.

**Recommendations:**
- Add a higher education policy alignment subsection connecting DSW to
  EUA digital transformation agenda, LERU open science position, and
  UNESCO OER recommendations.
- Connect DSW to EOSC, OpenAIRE, ORCID infrastructure.
- Address CoARA/DORA research assessment implications.
- Add teaching and learning implications (digital pedagogy, assessment
  integrity, accessibility in learning).

**Grade impact:** HE policy perspective improved from D to C+ (due to
legal analysis of academic freedom). Still needs substantial work.

---

### 3. Sociology of Technology (STS) Perspective

**Reviewer lens:** Social shaping, actor-network theory, digital
inequality, surveillance, political dimensions of sovereignty.

**Status after Rev 3:** UNADDRESSED. No STS content added.

**New observations post-Rev 3:**

1. **The system architecture (§10.1) presents technology as neutral
   infrastructure.** STS would ask how the architecture itself shapes
   academic work. For example: does a self-hosted Nextcloud instance
   with granular permission controls create a more hierarchical
   information culture than a shared Google Drive? Does the absence of
   algorithmic content recommendation (a feature of proprietary
   platforms) change how researchers discover information?

2. **The security threat model (§10.3) includes "surveillance" as a
   threat but frames it as external (state/corporate).** STS would add
   that sovereign platforms can also enable institutional surveillance
   (activity monitoring, productivity tracking, communication analysis).
   The well-being literature (261 papers) raises this concern. The
   paper should address governance mechanisms to prevent misuse of
   sovereign platform data for surveillance.

3. **The AI architecture (§10.4) does not address algorithmic governance.**
   Who decides what the sovereign AI can and cannot do? What biases are
   embedded in the embedding model and LLM? STS would demand
   transparency about model training data, evaluation benchmarks, and
   bias auditing.

4. **The TCO analysis (§12.1) does not account for social costs.**
   Platform migration disrupts established social practices (how
   researchers collaborate, how students learn, how admin staff work).
   These transition costs are not quantified but may be substantial.

5. **The legal definition of sovereignty (§11.2) is useful but STS would
   push further.** "Sovereignty" is not just a bundle of legal rights;
   it is a contested political concept that means different things to
   different actors. The paper's recommendation to replace "digital
   sovereignty" with specific legal obligations may obscure the political
   dimensions that motivate adoption (e.g., resistance to US tech
   hegemony, European strategic autonomy).

**Recommendations:**
- Add a social shaping analysis: how does platform choice reshape
  academic work, power relations, and information practices?
- Address surveillance risks in sovereign platforms (institutional
  misuse, not just external).
- Add algorithmic governance and bias auditing for sovereign AI.
- Analyse "sovereignty" as a contested political concept, not just a
  legal bundle.

**Grade impact:** STS perspective remains at D. No improvement.

---

### 4. Security Engineering Perspective

**Reviewer lens:** Threat modelling, security architecture, risk
assessment, compliance engineering.

**Status after Rev 3:** SUBSTANTIALLY ADDRESSED. The new §10.3 provides
a STRIDE-based threat model, security architecture controls, supply chain
security, and incident response framework. This was the most significant
gap in Rev 2 and is now well-covered.

**New observations post-Rev 3:**

1. **The threat model (§10.3) is good but lacks risk quantification.**
   STRIDE identifies threats but does not quantify likelihood or impact.
   A risk matrix (likelihood × impact) would prioritise mitigations.
   Not all threats are equal: data breach (high likelihood, high impact)
   vs. surveillance (low likelihood, high impact).

2. **The security architecture does not address key management in detail.**
   HSM is mentioned but not specified. Key rotation, escrow, and
   disaster recovery for keys are critical. If the HSM fails, all
   encrypted data is lost.

3. **Supply chain security mentions SBOM but not verification.** How are
   SBOMs verified? What happens when a vulnerability is found in a
   dependency? The paper needs a vulnerability response process (patch
   timeline, emergency updates, rollback).

4. **The incident response framework (§10.3) is based on NIST SP 800-61
   but lacks university-specific scenarios.** What is the response to:
   - A data breach involving student records (GDPR 72-hour
     notification)?
   - A ransomware attack during exam period?
   - A compromised admin account with access to all research data?

5. **Missing: security metrics and KPIs.** The observability framework
   (§10.6) has infrastructure and application metrics but no security
   metrics (failed auth attempts, anomaly detection alerts, patch
   compliance, vulnerability scan results).

6. **The AI architecture (§10.4) has privacy controls but no security
   analysis.** LLMs can be prompt-injected, jailbroken, or used to
   extract training data. The sovereign RAG pipeline needs input
   validation, output filtering, and adversarial testing.

**Recommendations:**
- Add risk quantification (likelihood × impact matrix).
- Specify key management lifecycle (generation, rotation, escrow,
  recovery).
- Add vulnerability response process with timelines.
- Develop university-specific incident scenarios.
- Add security metrics to observability framework.
- Add AI security analysis (prompt injection, data extraction, adversarial
  testing).

**Grade impact:** Security perspective improved from D to B-. Major
improvement; remaining gaps are refinement-level.

---

### 5. HCI / UX Perspective

**Reviewer lens:** Usability, user experience, accessibility, interaction
design, user research.

**Status after Rev 3:** UNADDRESSED. No HCI content added in Rev 3.

**New observations post-Rev 3:**

1. **The system architecture (§10.1) includes "User Layer (Browser/Mobile)"
   but no UX design.** HCI would ask: how is the interface designed?
   Does it match user expectations (familiarity with M365/Google)?
   How is cognitive load managed during migration?

2. **The AI architecture (§10.4) has no UX for AI interaction.** How do
   users interact with sovereign RAG? Is it a chat interface? A search
   bar? How are citations presented? How is user trust established?
   HCI literature shows that AI trust requires explainability and
   appropriate confidence calibration.

3. **The scalability analysis (§10.2) addresses infrastructure but not
   UX at scale.** With 100,000 users, how does the interface perform?
   What are the latency requirements for acceptable UX? HCI research
   shows that >2s response time significantly degrades user satisfaction.

4. **The migration path (§4) has user satisfaction as a success criterion
   (≥3.5/5) but no usability evaluation method.** HCI would require:
   SUS (System Usability Scale), task completion time, error rate,
   and qualitative feedback (think-aloud protocols).

5. **Accessibility is mentioned (§2.4, §3.1) but not specified.** The
   paper mentions "assistive technologies" and "WCAG" nowhere. EN 301 549
   (European accessibility standard) is the legal requirement for
   public-sector digital services. The DSW must comply. No audit or
   verification method is proposed.

6. **Missing: multilingual support.** Universities have international
   students and staff. The sovereign stack's UI language support,
   document translation, and AI multilingual capability are not addressed.

**Recommendations (unchanged, still unaddressed):**
- Propose a user research programme (interviews, surveys, usability tests).
- Define usability evaluation framework (SUS, task metrics, methods).
- Add accessibility compliance verification (WCAG 2.2, EN 301 549).
- Design onboarding and training strategy.
- Add multilingual support requirements.

**Grade impact:** HCI perspective remains at D. No improvement.

---

### 6. Public Policy Perspective

**Reviewer lens:** Digital sovereignty policy, EU digital strategy,
national strategies, policy instruments.

**Status after Rev 3:** PARTIALLY ADDRESSED. The Law section (§11)
addresses GDPR, procurement law, and AI Act, which are policy-relevant.
But the broader policy landscape (EU Digital Decade, Data Governance Act,
NIS2, DMA, DSA) and policy instruments are still not mapped.

**New observations post-Rev 3:**

1. **The Economics section (§12.4) provides market failure analysis
   that supports policy intervention.** This is a strong addition. But
   the paper does not translate this into specific policy
   recommendations for governments and funders.

2. **The legal definition of sovereignty (§11.2) identifies four levels
   (individual, institutional, national, European) but does not analyse
   their interactions.** Public policy would ask: can a university be
   sovereign if its nation is not? Does EU-level sovereignty (Digital
   Decade) conflict with or support institutional sovereignty?

3. **The consortium model (§5.1) is a governance proposal but not a
   policy instrument.** Public policy would ask: what policy instruments
   (funding, regulation, standards, procurement preferences) could
   accelerate DSW adoption? The paper identifies funding mechanisms
   (§5.2) but not regulatory or standards-based instruments.

4. **Missing: international dimension.** The paper is EU-focused. What
   about non-EU universities? How does geopolitics (US-China tech
   competition, sanctions) affect DSW feasibility? The first review
   raised this; Rev 3 does not address it.

5. **Missing: NIS2 Directive.** The paper mentions NIS2 in the first
   review but not in Rev 3. NIS2 (Network and Information Security
   Directive 2) imposes cybersecurity obligations on essential and
   important entities, including universities. This is directly
   relevant to the security architecture (§10.3) and should be
   cross-referenced.

**Recommendations:**
- Add a policy landscape section mapping EU and national policies.
- Analyse policy instruments (funding, regulation, standards,
  procurement preferences).
- Distinguish and analyse interactions between sovereignty levels.
- Add international and geopolitical dimensions.
- Include policy recommendations for governments and funders.
- Cross-reference NIS2 in the security architecture section.

**Grade impact:** Public policy perspective improved from D to C (due to
market failure analysis and legal framework). Still needs substantial
work.

---

## Part II: New Disciplinary Perspectives

### 7. Educational Technology (EdTech) Perspective

**Reviewer lens:** Digital pedagogy, learning management systems, learning
analytics, assessment integrity, student digital literacy.

**Relevance to DSW:** Universities are teaching institutions. The DSW
must support teaching and learning, not just research and
administration. The paper's "Missing from the stack" (§3.1) acknowledges
LMS integration as a gap but does not analyse pedagogical implications.

**Strengths (from Rev 3):**
- The AI architecture (§10.4) could support learning analytics and
  personalised learning (if privacy-preserving).
- The data architecture (§9.1) identifies "administrative data" but not
  "learning data" as a distinct domain.

**Weaknesses:**

1. **No digital pedagogy analysis.** How does a sovereign workplace
   affect teaching? Proprietary platforms (M365, Google) offer
   integrated LMS features, plagiarism detection, and AI-powered
   learning support. Sovereign alternatives (Moodle + Nextcloud +
   Collabora) require integration effort. The pedagogical trade-offs
   are not analysed.

2. **Learning analytics gap.** Universities increasingly use learning
   analytics (student engagement, performance prediction, early
   warning systems). These require data collection that may conflict
   with sovereignty principles (student privacy, consent). The paper
   does not address how sovereign platforms can support learning
   analytics while preserving privacy.

3. **Assessment integrity.** Online assessment (exams, plagiarism
   detection) is a critical university function. Proprietary platforms
   offer proctoring and plagiarism detection tools. Sovereign
   alternatives (Moodle quizzes, Turnitin alternatives like
   Compilatio) exist but are less mature. The paper does not address
   this.

4. **Student digital literacy.** If the university adopts a sovereign
   platform, students must learn new tools. This has equity
   implications: students with less technical background may struggle.
   The HCI section (not yet added) would address this, but EdTech
   would add: how is digital literacy supported in the curriculum?

5. **Accessibility in learning.** Universal Design for Learning (UDL)
   requires multiple means of representation, engagement, and
   expression. Sovereign platforms must support UDL principles
   (captions, screen readers, alternative formats). The paper
   mentions accessibility but not UDL specifically.

6. **Missing: LMS sovereignty.** The paper treats LMS as an integration
   point, not as a sovereignty concern. But LMS data (grades,
   submissions, engagement) is highly sensitive. Should the LMS itself
   be sovereign? Moodle is open-source and self-hostable. This is a
   natural extension of the DSW thesis but is not explored.

**Recommendations:**
- Add a teaching and learning subsection addressing digital pedagogy,
  learning analytics, assessment integrity, and student digital literacy.
- Address LMS sovereignty (Moodle as part of the sovereign stack).
- Include UDL and accessibility in learning.
- Analyse the pedagogical trade-offs of sovereign vs. proprietary tools.

**Grade:** D (not addressed).

---

### 8. Archival Science / Digital Preservation Perspective

**Reviewer lens:** Long-term preservation, metadata standards, digital
curation, records management, archival compliance.

**Relevance to DSW:** Universities are long-term institutions. Research
data, administrative records, and institutional memory must be preserved
for decades or centuries. The DSW must address preservation, not just
active use.

**Strengths (from Rev 3):**
- The data architecture (§9.1) identifies data domains but not
  preservation requirements.
- The security section (§10.3) mentions backup but not long-term
  preservation.

**Weaknesses:**

1. **No digital preservation strategy.** The paper addresses active
   storage (Nextcloud, object store) but not long-term preservation.
   What happens when a platform is decommissioned in 10 years? How is
   data migrated to successor systems? The OAIS (Open Archival
   Information System) reference model is the standard framework.

2. **Missing: metadata standards.** The paper mentions Dublin Core and
   DataCite in the library stakeholder section (§2.8) but does not
   specify metadata standards for the DSW. Without standardised
   metadata, long-term discoverability and interoperability are
   compromised.

3. **No records management.** Universities have legal obligations to
   retain certain records (student transcripts, financial records,
   research data) for specified periods. The DSW must implement
   retention policies, legal hold, and disposition workflows. The
   paper mentions "compliance automation (RoPA generation, retention,
   audit trails)" (§2.5) but does not develop this.

4. **Format obsolescence.** Proprietary formats (e.g., M365-specific
   metadata) may become unreadable. The sovereign stack should
   prefer open formats (ODF, PDF/A, TIFF). The paper does not address
   format strategy.

5. **Missing: archival integration.** Universities have institutional
   repositories (DSpace, EPrints) and archives. The DSW should
   integrate with these, not duplicate them. The paper mentions
   "integration with institutional repositories" (§2.8) but not the
   data flow between active (DSW) and archival (repository) systems.

**Recommendations:**
- Add a digital preservation subsection (OAIS model, format strategy,
  metadata standards).
- Address records management (retention, legal hold, disposition).
- Specify integration between DSW and institutional repositories.
- Include format obsolescence mitigation (open formats, migration
  planning).

**Grade:** F (not addressed at all).

---

### 9. Environmental Sustainability / Green IT Perspective

**Reviewer lens:** Carbon footprint, energy efficiency, e-waste,
sustainable IT, green computing.

**Relevance to DSW:** Self-hosted infrastructure has an environmental
footprint. The paper's TCO analysis (§12.1) includes infrastructure
costs but not environmental costs. Sustainability is increasingly a
university priority and a funding requirement.

**Strengths (from Rev 3):**
- The infrastructure estimates (§10.2) provide a basis for
  environmental analysis.
- The consortium model (§5.1) could enable shared, efficient
  infrastructure.

**Weaknesses:**

1. **No environmental analysis.** The paper does not address the carbon
   footprint of self-hosted infrastructure (servers, cooling, power)
   vs. cloud providers (which may use renewable energy and achieve
   better PUE — Power Usage Effectiveness).

2. **Missing: green IT metrics.** No energy consumption, carbon
   emissions, or e-waste metrics are proposed. Universities
   increasingly report on sustainability (e.g., Times Higher
   Education Impact Rankings). DSW should contribute positively.

3. **GPU energy consumption.** The AI architecture (§10.4) specifies
   4+ A100 GPUs. Each A100 consumes ~400W under load. Running 24/7,
   this is significant. The paper does not address energy-efficient
   AI (model quantisation, inference optimisation, renewable energy).

4. **E-waste.** Hardware refresh cycles (3-5 years) generate e-waste.
   The paper does not address circular economy principles (refurbished
   hardware, recycling, extended lifecycle).

5. **Missing: sustainability as a selection criterion.** The capability
   comparison table (§1.3) includes "compliance/audit" and "data
   residency" but not "carbon footprint" or "energy efficiency" as
   evaluation criteria.

**Recommendations:**
- Add environmental impact analysis (carbon footprint, PUE, energy
  consumption).
- Include green IT metrics in the observability framework.
- Address energy-efficient AI (quantisation, scheduling, renewable
  energy).
- Add sustainability as a platform evaluation criterion.
- Consider shared consortium infrastructure for efficiency.

**Grade:** F (not addressed at all).

---

### 10. Labour Studies / Industrial Relations Perspective

**Reviewer lens:** Worker rights, algorithmic management, union
perspectives, job quality, labour market effects.

**Relevance to DSW:** The DSW affects how university staff work. The
paper's stakeholder analysis includes "administrative staff" and "IT
departments" but does not analyse labour implications (job
displacement, skill requirements, surveillance, collective bargaining).

**Strengths (from Rev 3):**
- The power dynamics analysis (§2.13) acknowledges that IT departments
  control implementation.
- The STS review (above) notes surveillance risks.

**Weaknesses:**

1. **No labour impact analysis.** Platform migration affects jobs:
   - IT staff: new skills required (Linux, open-source, security).
     Risk of skill obsolescence or increased workload.
   - Admin staff: new tools, retraining, potential efficiency gains
     (or losses).
   - Faculty: new collaboration tools, potential productivity changes.
   The paper does not address workforce transition planning.

2. **Missing: algorithmic management.** The AI layer (§10.4) could
   enable algorithmic management (performance monitoring, productivity
   tracking, automated assessment). The well-being literature (261
   papers) warns about digital surveillance and algorithmic control.
   The paper does not address governance to prevent misuse.

3. **No union/collective bargaining perspective.** University staff are
   often unionised. Platform changes may be subject to collective
   bargaining. The paper does not mention unions or worker
   representatives as stakeholders.

4. **Missing: job quality.** The well-being literature (261 papers)
   suggests that platform design affects job quality (autonomy,
   skill development, work-life balance). The DSW should be designed
   to improve, not degrade, job quality.

5. **No skills development plan.** The migration requires new skills
   (Linux administration, open-source security, AI operations). The
   paper mentions "skills development" (§5.4) but not a concrete
   training and reskilling programme.

**Recommendations:**
- Add a workforce transition plan (reskilling, workload management,
  change support).
- Address algorithmic management risks and governance.
- Include union/worker representative stakeholders.
- Add job quality as a DSW design criterion.
- Develop a concrete skills development programme.

**Grade:** F (not addressed at all).

---

## Part III: Cross-Cutting Synthesis (Rev 3)

### Convergent themes (new and persisting)

1. **The paper's structure is now imbalanced.** The four deep-integrated
   sections (§9–12, ~840 lines) are more detailed than the core sections
   (§2–5, ~440 lines). A reader encounters the stakeholder analysis
   (§2) and technology stack (§3) before the analytical depth that
   justifies them. Consider restructuring: move §9–12 before §6
   (counter-evidence) or integrate them into existing sections.

2. **The "tail" sections (§9–12) are excellent but disconnected.** Each
   section is self-contained and does not cross-reference the others
   enough. The cross-disciplinary synthesis (§13.1) is a good start but
   could be expanded with specific cross-references (e.g., "the TCO
   framework in §12.1 informs the IT governance KPIs in §9.2").

3. **New gaps emerge from the Rev 3 additions.** The IS governance
   section creates OB concerns (rational model vs. collegial reality).
   The TCO analysis raises labour questions (workforce transition).
   The security architecture raises environmental questions (GPU
   energy). The AI architecture raises EdTech questions (learning
   analytics). Each deep-integrated section opens new disciplinary
   questions.

4. **The paper still lacks primary research.** Despite the analytical
   depth, the fundamental limitation remains: no interviews, surveys,
   or usability tests with university stakeholders. This is
   acknowledged but not addressed. A credible academic paper in IS, CS,
   Law, or Economics would require empirical data.

5. **The paper's scope is now very broad.** With 13 sections covering
   stakeholders, technology, migration, governance, counter-evidence,
   discussion, IS, CS, Law, Economics, and synthesis, the paper risks
   being "a mile wide and an inch deep" despite the Rev 3 additions.
   Consider: is this one paper or a research programme? The multi-
   perspective review's recommendation to "narrow scope or add depth"
   still applies.

### Divergent perspectives (new)

1. **On paper structure:** IS and CS reviewers appreciate the dedicated
   sections. OB and STS reviewers find them disconnected from the
   stakeholder and migration narrative. Economics reviewers want the
   TCO analysis earlier (before the migration path, so costs inform
   decisions).

2. **On scope:** HE policy and EdTech reviewers want more teaching/
   learning content. Labour and STS reviewers want more social analysis.
   Security and CS reviewers are satisfied with their sections. The
   tension between breadth and depth persists.

3. **On the legal recommendation to de-politicise "sovereignty":** Law
   and IS reviewers support precision. STS and public policy reviewers
   want to retain the political dimension. This tension is unresolved.

### Priority recommendations (updated, cross-disciplinary)

From the first review's 10 recommendations, status after Rev 3:

1. ✅ Define "digital sovereignty" precisely — DONE (§11.2).
2. ✅ Add system architecture — DONE (§10.1–10.6).
3. ❌ Conduct primary user research — NOT DONE (still a limitation).
4. ⚠️ Quantify costs — PARTIALLY DONE (§12.1 framework, no empirical data).
5. ✅ Develop a threat model — DONE (§10.3).
6. ❌ Map the policy landscape — NOT DONE.
7. ❌ Integrate change management frameworks — NOT DONE.
8. ❌ Connect to open science infrastructure — NOT DONE.
9. ❌ Add usability evaluation framework — NOT DONE.
10. ✅ Analyse platform market economics — DONE (§12.2–12.5).

**New recommendations (from this review round):**
11. Add workforce transition and labour impact analysis (labour studies).
12. Add digital preservation strategy (archival science).
13. Add environmental sustainability analysis (green IT).
14. Add teaching/learning and EdTech analysis (EdTech).
15. Add organisational culture and change management frameworks (OB).
16. Map the policy landscape and add policy recommendations (public policy).
17. Add user research methodology and usability framework (HCI).
18. Restructure the paper to integrate deep-dive sections with core
    narrative (all disciplines).

---

## Conclusion

Rev 3 has successfully deep-integrated four disciplinary perspectives
to publication standard. The paper is now substantially stronger in IS,
CS, Law, and Economics. However, the remaining six disciplines from
the first review (OB, HE policy, STS, security, HCI, public policy)
are still largely unaddressed (with the exception of security, which
is now well-covered). Four new perspectives (EdTech, archival science,
green IT, labour studies) reveal additional gaps that were not
previously identified.

The paper's fundamental tension persists: it is a broad proposal
covering 12 stakeholder groups, 5 migration phases, and 4 disciplinary
deep-dives, but lacks empirical validation. A credible academic paper
would need to either narrow its scope or add substantial empirical
depth.

**Recommended next step:** Choose between two paths:
- **Path A (Depth):** Select 2-3 of the remaining gaps (recommended:
  OB change management, HE policy/open science, EdTech teaching/
  learning) and deep-integrate them, accepting that the paper will
  grow to ~2,500+ lines.
- **Path B (Focus):** Restructure the paper around a single
  disciplinary lens (e.g., IS or CS) and move the other perspectives
  to future work or companion papers. This would produce a more
  focused, publishable paper.

**Status update (Rev 4):** All key findings from both review rounds
have been addressed. The paper now has 21 sections covering 11
disciplinary perspectives:
- §9-12: Publication-standard (IS, CS, Law, Economics)
- §14-20: Framework-level (OB, HE policy, archival science, green IT,
  labour studies, public policy, HCI/UX)
- §13, §21: Cross-disciplinary synthesis

The paper grew from 1,656 to 2,396 lines. The structural imbalance
has been partially addressed by adding framework-level sections that
parallel the deep-integrated ones. Primary research, empirical cost
data, and deep analysis of the 7 framework-level sections remain as
future work.

---

*This review is the second round of multi-perspective review, focusing
on the six disciplines not deep-integrated in Rev 3 plus four new
disciplinary perspectives. It should be read alongside the first
multi-perspective review (multi_perspective_review.md) for complete
coverage.*