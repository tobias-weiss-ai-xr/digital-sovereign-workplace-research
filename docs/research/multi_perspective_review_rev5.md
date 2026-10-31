# Multi-Perspective Critical Review (Rev 5): "Towards a Digital Sovereign Workplace for Universities"

**Reviewers:** Multi-disciplinary review panel (third round)  
**Date:** 2026-10-31  
**Paper reviewed:** `docs/research/digital_sovereign_workplace_universities.md` (Rev 5, 2,790 lines)  
**Focus:** Ten new disciplinary perspectives not covered in previous review
rounds, assessing the paper's maturity after three rounds of review and
revision.

---

## Preamble

The paper has grown from 815 lines (Rev 2) to 2,790 lines (Rev 5) through
three rounds of multi-perspective review and revision. It now covers 11
disciplines across 21 sections organised into 3 parts. This third review
round brings 10 entirely new disciplinary perspectives to bear, testing
whether the paper has reached a point of diminishing returns or whether
significant gaps remain.

**Overall assessment:** Rev 5 is a remarkably comprehensive document. The
structural reorganization (3 parts, "How to read" guide) significantly
improves navigability. The 11 disciplinary perspectives provide broad
coverage. However, this third review reveals that the paper's very
comprehensiveness creates new problems: (1) the paper is now so long that
it risks being unreadable; (2) several perspectives reveal fundamental
tensions in the DSW thesis that the paper does not resolve; (3) the
paper's "framework-level" sections (§14-20) are still not at publication
standard despite deepening; (4) the paper lacks a coherent theoretical
framework that integrates the 11 perspectives. The most valuable
contribution of this review is identifying which gaps are genuinely
important vs. which are academic completeness for its own sake.

---

## Part I: New Disciplinary Perspectives

### 1. Philosophy of Technology Perspective

**Reviewer lens:** Technology ethics, techno-solutionism critique,
phenomenology of technology, philosophy of information.

**Relevance to DSW:** The paper treats technology as a solution to
institutional problems. Philosophy of technology asks whether this
framing is appropriate and whether it obscures non-technical
dimensions of the problem.

**Strengths (from Rev 5):**
- The counter-evidence section (§6) engages with limitations honestly.
- The legal definition of sovereignty (§11.2) distinguishes technical
  from political concepts.

**Weaknesses:**

1. **Techno-solutionism.** The paper frames digital sovereignty as a
   technology problem solvable by better technology (Nextcloud,
   Keycloak, sovereign RAG). Philosophy of technology (Morozov 2013)
   warns that this framing obscures the social, political, and economic
   dimensions. The DSW may be a "technological fix" for a problem that
   is fundamentally about power, governance, and institutional culture.

2. **Instrumental vs. substantive rationality.** The paper evaluates
   platforms by their features and capabilities (instrumental
   rationality) but does not question whether the features themselves
   serve human flourishing. Does a sovereign platform with the same
   surveillance capabilities as a proprietary one actually advance
   freedom? Or does it merely relocate control?

3. **The "neutrality" of open source.** The paper assumes open-source
   platforms are inherently more aligned with university values. But
   open-source software is not value-neutral; it embeds specific
   assumptions about collaboration, transparency, and community that
   may not suit all institutional contexts. The STS perspective
   (first review) raised this; philosophy of technology deepens it.

4. **Heideggerian critique.** Heidegger's "Question Concerning
   Technology" warns that technology's "essence" is not a tool but a
   mode of revealing that reduces everything to "standing-reserve"
   (resources to be exploited). Both proprietary and sovereign platforms
   may embody this reduction. The paper does not engage with whether
   DSW escapes or merely replicates technological enframing.

5. **Missing: normative framework.** The paper is descriptive and
   instrumental (how to achieve DSW) but lacks a normative theory of
   what universities *should* be in the digital age. What is the good
   university? What role should technology play? Without a normative
   framework, "sovereignty" is an empty signifier.

**Recommendations:**
- Add a normative framework section defining the "good digital
  university" and how DSW serves it.
- Engage with techno-solutionism critique explicitly.
- Question whether open-source platforms are value-neutral.
- Consider whether DSW is a technological fix or a socio-political
  transformation.

**Grade:** D (not addressed).

---

### 2. Disability Studies Perspective

**Reviewer lens:** Social model of disability, universal design,
accessibility as justice, neurodiversity.

**Relevance to DSW:** The paper mentions accessibility (§2.4, §20.3)
but frames it as compliance (WCAG 2.2, EN 301 549). Disability studies
asks whether compliance is sufficient and whether the DSW can be
designed for genuine inclusion.

**Strengths (from Rev 5):**
- §20.3 specifies WCAG 2.2 AA and EN 301 549.
- §20.3 includes assistive technology support.
- §15.4 mentions UDL.

**Weaknesses:**

1. **Compliance vs. inclusion.** WCAG compliance is a floor, not a
   ceiling. Disability studies distinguishes between "accessible"
   (technically compliant) and "inclusive" (genuinely usable by
   disabled people). The paper does not address this distinction.

2. **Social model of disability.** The medical model locates disability
   in the individual; the social model locates it in the environment.
   The paper's accessibility section (§20.3) implicitly uses the
   medical model (fix the user's assistive technology). Disability
   studies would ask: how does the platform itself create or remove
   barriers?

3. **Neurodiversity.** The paper does not address neurodivergent
   users (autism, ADHD, dyslexia). Sovereign platforms could offer
   customisable interfaces (reduced motion, simplified layouts,
   alternative colour schemes) that proprietary platforms do not.
   This is a sovereignty advantage not explored.

4. **Cognitive accessibility.** Beyond screen readers: plain language,
   consistent navigation, error prevention, and recovery. The paper
   mentions "cognitive load" (§20.4) but not cognitive accessibility
   standards (e.g., COGA, Plain Language guidelines).

5. **Missing: disabled users as co-designers.** The user research
   programme (§20.1) includes "user testing with disabled users" but
   does not position disabled people as co-designers. "Nothing about
   us without us" is a core disability studies principle.

**Recommendations:**
- Reframe accessibility from compliance to inclusion.
- Add neurodiversity and cognitive accessibility.
- Position disabled users as co-designers, not just testers.
- Add social model analysis of platform barriers.

**Grade:** D (compliance-focused, not inclusion-focused).

---

### 3. Feminist and Gender Studies Perspective

**Reviewer lens:** Gendered effects of technology, care work, digital
labour, intersectionality, feminist HCI.

**Relevance to DSW:** The paper's stakeholder analysis (§2) is
gender-neutral. Feminist studies asks how platform design and
migration affect different genders differently.

**Strengths (from Rev 5):**
- The well-being literature (261 papers) is cited.
- The power dynamics analysis (§2.13) acknowledges asymmetries.

**Weaknesses:**

1. **Gender-neutral stakeholder analysis.** The 12 stakeholder groups
   are not analysed for gender composition or gendered needs. In
   universities, administrative staff (predominantly women) and
   faculty (gender varies by discipline) have different relationships
   with digital tools. Care work (student support, mentoring) is
   gendered and platform-dependent.

2. **Digital labour and invisible work.** Platform migration creates
   invisible labour (helping colleagues, troubleshooting, training).
   This labour is often gendered (women more likely to provide
   informal tech support). The paper does not address this.

3. **Algorithmic bias.** The AI architecture (§10.4) mentions "bias
   auditing" but does not specify gender bias. LLMs trained on
   biased data reproduce gender stereotypes. Sovereign AI requires
   gender-aware evaluation.

4. **Intersectionality.** The paper's equity analysis (§15.4) addresses
   digital divide but not intersectional effects (e.g., a disabled
   woman of colour faces compounded barriers). Feminist HCI
   (Bardzell 2010) provides frameworks for this.

5. **Missing: feminist data practices.** Data collection in sovereign
   platforms can reproduce gendered surveillance (e.g., monitoring
   communication patterns, inferring care responsibilities). The
   paper's data governance (§11.1) does not address this.

**Recommendations:**
- Add gender analysis to stakeholder groups.
- Address invisible digital labour and its gendered distribution.
- Specify gender bias auditing for sovereign AI.
- Apply intersectional analysis to equity considerations.
- Add feminist data governance principles.

**Grade:** F (not addressed).

---

### 4. Indigenous Data Sovereignty Perspective

**Reviewer lens:** Indigenous data sovereignty, CARE principles,
decolonial computing, indigenous knowledge systems.

**Relevance to DSW:** Universities often hold indigenous research data
and collaborate with indigenous communities. The paper's "data
sovereignty" framing is Eurocentric and does not address indigenous
data sovereignty (IDS) principles.

**Strengths (from Rev 5):**
- The data architecture (§9.1) identifies research data as a domain.
- The international dimensions (§19.4) mention Global South.

**Weaknesses:**

1. **Eurocentric sovereignty.** The paper's sovereignty framework
   (§11.2) is based on EU law and European political concepts.
   Indigenous data sovereignty (Kukutai & Taylor 2016) defines
   sovereignty differently: as collective rights of indigenous peoples
   to govern data about their communities, lands, and knowledge.
   These frameworks are not compatible with institutional sovereignty.

2. **CARE principles.** The CARE (Collective benefit, Authority to
   control, Responsibility, Ethics) principles for indigenous data
   governance are not mentioned. The paper uses FAIR principles
   implicitly (findable, accessible, interoperable, reusable) but
   CARE adds indigenous-specific requirements (authority, ethics,
   collective benefit).

3. **Missing: indigenous research data.** Universities conducting
   research with indigenous communities hold data subject to
   indigenous data sovereignty. The DSW must support indigenous
   data governance (e.g., Te Mana Raraunga in New Zealand, Maiam
   nayri Wingara in Australia). This is not addressed.

4. **Decolonial computing.** The paper's technology stack is based on
   Western open-source projects (Nextcloud, Collabora, Matrix).
   Decolonial computing asks whether these tools can serve indigenous
   knowledge systems, which may have different epistemological
   foundations (relational, place-based, oral).

5. **Missing: indigenous stakeholders.** The 12 stakeholder groups
   do not include indigenous communities or indigenous research
   partners. This is a significant gap for universities in countries
   with indigenous populations.

**Recommendations:**
- Add indigenous data sovereignty as a distinct concern.
- Incorporate CARE principles alongside FAIR.
- Add indigenous research data governance to the data architecture.
- Consider decolonial implications of the technology stack.
- Add indigenous communities as a stakeholder group.

**Grade:** F (not addressed).

---

### 5. Media and Platform Studies Perspective

**Reviewer lens:** Platform capitalism, platform studies, algorithmic
culture, media ecology.

**Relevance to DSW:** The paper treats platforms as neutral
infrastructure. Media and platform studies (Gillespie 2010, van Dijck
2013) analyse platforms as socio-technical constructs that shape
behaviour, culture, and power.

**Strengths (from Rev 5):**
- The platform market economics (§12.2) analyses lock-in and network
  effects.
- The capability comparison (§1.3) compares features.

**Weaknesses:**

1. **Platform as construct.** The paper treats "platform" as a
   technical artifact (software stack). Platform studies defines
   platforms as "intermediaries" that organise social activity and
   create markets. The DSW is not just software; it is a platform
   that will shape academic work, social relations, and institutional
   culture. This shaping power is not analysed.

2. **Platform capitalism.** The paper's economic analysis (§12)
   addresses market failure but not platform capitalism (Srnicek
   2017). Proprietary platforms extract data as raw material for
   surveillance capitalism. Sovereign platforms may resist this, but
   the paper does not analyse the political economy of data
   extraction.

3. **Algorithmic culture.** The AI architecture (§10.4) deploys RAG
   and LLMs without analysing how algorithmic systems shape academic
   knowledge production (what gets retrieved, what gets generated,
   what gets cited). Media studies would ask: how does sovereign AI
   reshape epistemic practices?

4. **Media ecology.** The paper does not analyse how the DSW changes
   the "media environment" of the university. What happens to
   academic communication when all channels (email, chat, video,
   documents) are unified under one sovereign platform? Does this
   create a monoculture?

5. **Missing: platform governance.** The paper's governance section
   (§5) addresses institutional governance but not platform
   governance (how the platform itself is governed — content
   moderation, algorithmic transparency, user rights). Open-source
   platforms need platform governance too.

**Recommendations:**
- Analyse DSW as a platform that shapes social and academic
  practices.
- Engage with platform capitalism and data extraction critique.
- Analyse algorithmic effects on knowledge production.
- Add platform governance (content moderation, algorithmic
  transparency) to governance section.

**Grade:** D (not addressed).

---

### 6. Design Studies Perspective

**Reviewer lens:** Design thinking, participatory design, service
design, design justice.

**Relevance to DSW:** The paper specifies what to build (technology
stack) but not how to design it with users. Design studies provides
methodologies for human-centred platform design.

**Strengths (from Rev 5):**
- §20 provides user research and usability framework.
- §2.4 includes student needs.

**Weaknesses:**

1. **Technology-first, design-second.** The paper specifies the
   technology stack (§3) before any design process. Design studies
   would invert this: start with user needs and co-design the
   solution. The current approach risks "designing for" rather than
   "designing with" users.

2. **Missing: participatory design.** The user research programme
   (§20.1) includes interviews and surveys but not participatory
   design (co-design workshops, design sprints, prototype testing
   with users). Participatory design (Schuler & Namioka 1993) is
   particularly important for complex institutional systems.

3. **Service design.** The DSW is not just software; it is a service
   ecosystem (onboarding, support, training, governance). Service
   design (blueprinting, journey mapping, touchpoint analysis) is
   needed to design the full user experience, not just the interface.

4. **Design justice.** Design justice (Costanza-Chock 2020) asks who
   benefits from design and who is marginalised. The DSW's design
   process should centre marginalised users (disabled students,
   international students, precarious staff) rather than treating
   them as edge cases.

5. **Missing: design patterns.** The paper does not reference
   established design patterns for collaboration platforms (e.g.,
   Nielsen Norman Group heuristics, Material Design, GOV.UK Design
   System). Sovereign platforms should leverage proven patterns
   rather than reinventing.

**Recommendations:**
- Add participatory design methodology to the migration model.
- Include service design (journey mapping, touchpoint analysis).
- Apply design justice principles.
- Reference established design patterns and systems.

**Grade:** D (research framework exists but no design methodology).

---

### 7. Knowledge Management Perspective

**Reviewer lens:** Institutional knowledge, tacit knowledge, communities
of practice, knowledge sharing, organisational memory.

**Relevance to DSW:** Universities are knowledge organisations. The DSW
should support knowledge management, not just file storage. The paper
does not address how the DSW captures, shares, and preserves
institutional knowledge.

**Strengths (from Rev 5):**
- The AI architecture (§10.4) includes RAG for institutional knowledge
  search.
- The organisational learning section (§14.5) addresses knowledge
  capture.

**Weaknesses:**

1. **Tacit knowledge.** The paper addresses explicit knowledge
   (documents, files) but not tacit knowledge (expertise, experience,
   relationships). Sovereign platforms can support tacit knowledge
   sharing (communities of practice, mentoring, peer review) but this
   requires design, not just technology.

2. **Knowledge loss.** When staff leave, their knowledge leaves with
   them. The DSW should capture institutional knowledge (process
   documentation, decision records, contact networks) to prevent
   knowledge loss. The paper's organisational learning section (§14.5)
   mentions this but does not specify mechanisms.

3. **Knowledge silos.** Universities are siloed by department and
   discipline. The DSW should break down knowledge silos by making
   institutional knowledge discoverable across boundaries. The
   interoperability section (§3) addresses technical interoperability
   but not knowledge interoperability.

4. **Communities of practice.** The consortium model (§5.1) is a
   community of practice for DSW, but the paper does not address how
   DSW supports communities of practice within the university (e.g.,
   research groups, teaching communities, admin communities).

5. **Missing: knowledge metrics.** How do you measure whether the DSW
   improves knowledge sharing? Metrics: knowledge reuse rate, time to
   find information, cross-departmental collaboration frequency,
   institutional memory completeness.

**Recommendations:**
- Add knowledge management as a DSW capability.
- Address tacit knowledge capture and sharing.
- Add knowledge loss prevention mechanisms.
- Support communities of practice.
- Define knowledge metrics.

**Grade:** D (organisational learning mentioned but not KM framework).

---

### 8. Complexity Science Perspective

**Reviewer lens:** Systems thinking, emergence, feedback loops,
complex adaptive systems, resilience.

**Relevance to DSW:** A university is a complex adaptive system. The
paper's linear migration model (§4) assumes predictable, controllable
change. Complexity science suggests this is unrealistic.

**Strengths (from Rev 5):**
- The timeline caveat (§4.1) acknowledges non-linearity.
- The socio-technical co-evolution (§9.3) addresses interdependence.

**Weaknesses:**

1. **Linear model vs. complex reality.** The five-phase migration
   model (§4) is sequential and deterministic. Complexity science
   (Snowden's Cynefin framework) would classify DSW migration as
   "complex" (not "complicated"): cause and effect are only
   coherent in retrospect, and outcomes are emergent. The model should
   be adaptive, not predictive.

2. **Emergence.** The paper does not address what might emerge from
   DSW adoption that was not planned: new collaboration patterns,
   unexpected uses, unintended consequences (e.g., shadow IT
   migrating to sovereign shadow IT). These emergent phenomena
   should be monitored and managed.

3. **Feedback loops.** The DSW creates feedback loops: user
   satisfaction → adoption → network effects → more users → more
   satisfaction. But also: user frustration → resistance → shadow IT
   → more frustration. The paper does not identify or manage these
   feedback loops.

4. **Resilience.** The paper addresses security resilience (§10.3)
   but not organisational resilience: how does the university
   adapt to disruptions (vendor changes, technology obsolescence,
   staff turnover, funding cuts)? Complexity science suggests
   building adaptive capacity, not just robust systems.

5. **Missing: systems thinking tools.** The paper does not use
   systems thinking tools (causal loop diagrams, stock-and-flow
   models, system archetypes) to analyse the DSW ecosystem. These
   tools would reveal leverage points and unintended consequences.

**Recommendations:**
- Reframe migration model as adaptive, not deterministic.
- Identify and monitor emergent phenomena.
- Map feedback loops (positive and negative).
- Build organisational resilience, not just technical resilience.
- Use systems thinking tools (causal loop diagrams) in planning.

**Grade:** D (timeline caveat acknowledges non-linearity but no
complexity framework).

---

### 9. Political Science Perspective

**Reviewer lens:** Institutional theory, power analysis, governance
theory, state-university relations, policy networks.

**Relevance to DSW:** The paper's governance section (§5) proposes
mechanisms but does not analyse the political dynamics of university
governance. Political science provides frameworks for understanding
how power operates in universities.

**Strengths (from Rev 5):**
- The power dynamics analysis (§2.13) acknowledges asymmetries.
- The public policy section (§19) maps the policy landscape.

**Weaknesses:**

1. **Institutional theory.** The paper does not use institutional
   theory (DiMaggio & Powell 1983) to analyse why universities
   adopt certain technologies. Isomorphic pressures (coercive:
   regulatory mandates; mimetic: copying peer institutions;
   normative: professional standards) drive technology adoption.
   Understanding these pressures helps predict and manage adoption.

2. **State-university relations.** The paper assumes universities
   have autonomy to choose their digital infrastructure. But
   universities are state-funded (in most European countries) and
   subject to government digital strategies. The relationship
   between state digital sovereignty agendas and university
   autonomy is not analysed.

3. **Policy networks.** The consortium model (§5.1) is a policy
   network, but the paper does not analyse how policy networks
   form, operate, and influence outcomes. Who has power in the
   consortium? How are decisions made? What is the role of
   government actors?

4. **Governance theory.** The paper proposes a steering committee
   but does not engage with governance theory (e.g., Ostrom's
   principles for governing commons, which are directly relevant to
   shared digital infrastructure). Ostrom's 8 principles for
   governing commons (clearly defined boundaries, collective choice
   arrangements, monitoring, graduated sanctions, etc.) could
   structure the consortium governance.

5. **Missing: political economy of higher education.** The paper
   does not analyse how digital infrastructure relates to the
   political economy of higher education (marketisation,
   privatisation, commodification of knowledge). DSW may be a
   response to these trends, but the connection is not made.

**Recommendations:**
- Apply institutional theory to analyse adoption drivers.
- Analyse state-university relations in digital infrastructure.
- Use Ostrom's commons governance principles for consortium design.
- Add political economy analysis of HE digitalisation.

**Grade:** D (power dynamics mentioned but no political science
framework).

---

### 10. Innovation Studies Perspective

**Reviewer lens:** Diffusion of innovations, technology adoption
lifecycle, disruptive innovation, innovation ecosystems.

**Relevance to DSW:** The paper proposes a novel technology
configuration (sovereign workplace) that must diffuse through
universities. Innovation studies provides frameworks for understanding
and accelerating this diffusion.

**Strengths (from Rev 5):**
- The adoption literature (252 papers) is cited.
- The migration model (§4) provides a phased approach.

**Weaknesses:**

1. **Diffusion of innovations.** Rogers' diffusion model (relative
   advantage, compatibility, complexity, trialability, observability)
   is not applied. DSW has low relative advantage (proprietary
   platforms are better), low compatibility (different from familiar
   tools), high complexity, low trialability, and low observability.
   These factors predict slow diffusion. The paper should address
   how to improve each factor.

2. **Technology adoption lifecycle.** Moore's chasm (between early
   adopters and early majority) is not addressed. Universities are
   typically early majority (pragmatic, risk-averse). The DSW
   must cross the chasm from innovators (tech-savvy IT staff) to
   early majority (mainstream faculty). Strategies: whole product
   (complete solution, not just components), reference customers,
   industry standards.

3. **Disruptive innovation.** Christensen's framework suggests that
   sovereign platforms may be disruptive (initially inferior but
   improving, targeting underserved segments). The paper does not
   analyse whether DSW is disruptive or sustaining, and what this
   means for strategy.

4. **Innovation ecosystem.** The consortium model (§5.1) is an
   innovation ecosystem, but the paper does not analyse ecosystem
   dynamics (keystone vs. niche players, value co-creation,
   ecosystem governance). The open-source ecosystem has specific
   dynamics (community contributions, vendor competition,
   standardisation) that affect DSW viability.

5. **Missing: adoption barriers analysis.** The paper lists adoption
   barriers (§6.2) but does not systematically analyse them using
   innovation studies frameworks. A structured barrier analysis
   (technical, organisational, economic, cultural) with mitigation
   strategies would strengthen the migration model.

**Recommendations:**
- Apply Rogers' diffusion factors to DSW.
- Address the chasm between early adopters and early majority.
- Analyse whether DSW is disruptive or sustaining innovation.
- Develop an innovation ecosystem analysis.
- Conduct structured adoption barrier analysis.

**Grade:** D (adoption literature cited but no innovation framework).

---

## Part II: Cross-Cutting Synthesis (Third Round)

### Convergent themes (new)

1. **The paper is now too long for its audience.** At 2,790 lines,
   the paper is longer than most academic books. While comprehensive,
   it risks being unreadable. The "How to read" guide (§1.6) helps,
   but the fundamental tension between completeness and readability
   remains. Consider: is this one paper or a research programme
   with companion papers?

2. **Techno-solutionism is the paper's blind spot.** Philosophy of
   technology, STS, and feminist studies all identify that the paper
   treats DSW as a technology solution to institutional problems.
   The paper does not question whether the problem is technological
   or whether technology can solve it. This is the most significant
   conceptual gap remaining.

3. **Equity and inclusion are underdeveloped.** Disability studies,
   feminist studies, and indigenous data sovereignty all identify
   that the paper's equity analysis (§15.4) is superficial. The paper
   treats equity as an add-on rather than a design principle. This
   is a significant gap for a paper about public institutions.

4. **The paper lacks a coherent theoretical framework.** 11
   disciplinary perspectives are presented side by side but not
   integrated into a unified theoretical framework. Each section
   uses different concepts and assumptions. A theoretical synthesis
   (e.g., socio-technical systems theory, institutional theory, or
   a custom framework) would strengthen the paper.

5. **The "framework-level" sections (§14-20) are still not
   publication standard.** Despite deepening, they remain at
   framework level. The gap between §9-12 (publication standard) and
   §14-20 (framework level) is visible. Either deepen them further
   or explicitly frame them as "future work" appendices.

### Divergent perspectives (new)

1. **On paper length:** Complexity science and design studies want
   more (systems thinking, participatory design). Philosophy of
   technology and media studies want less (focus on core argument,
   move details to appendices). Innovation studies is neutral but
   wants structured analysis.

2. **On techno-solutionism:** Philosophy of technology and feminist
   studies are critical. IS and CS reviewers see technology as the
   appropriate level of analysis. Law and economics are neutral.
   This tension is fundamental and unresolved.

3. **On equity:** Disability studies, feminist studies, and indigenous
   data sovereignty want equity as a core design principle. The
   paper treats it as a consideration. This is a values tension,
   not just an analytical gap.

### Priority recommendations (updated, third round)

From previous rounds, status after Rev 5:

1. ✅ Define "digital sovereignty" precisely — DONE (§11.2).
2. ✅ Add system architecture — DONE (§10.1–10.6).
3. ❌ Conduct primary user research — NOT DONE (framework only).
4. ⚠️ Quantify costs — PARTIALLY DONE (§12.1 framework, no empirical data).
5. ✅ Develop a threat model — DONE (§10.3).
6. ❌ Map the policy landscape — PARTIALLY DONE (§19.1 table, limited analysis).
7. ⚠️ Integrate change management frameworks — DONE (§14.1, framework level).
8. ❌ Connect to open science infrastructure — PARTIALLY DONE (§15.2, limited).
9. ❌ Add usability evaluation framework — DONE (§20.2, framework level).
10. ✅ Analyse platform market economics — DONE (§12.2–12.5).
11. ⚠️ Workforce transition — DONE (§18.1, framework level).
12. ⚠️ Digital preservation — DONE (§16, framework level).
13. ⚠️ Environmental sustainability — DONE (§17, framework level).
14. ⚠️ Teaching/learning — DONE (§15.4, framework level).
15. ⚠️ Organisational culture — DONE (§14.2, framework level).
16. ⚠️ Policy landscape — PARTIALLY DONE (§19, framework level).
17. ⚠️ User research/usability — DONE (§20, framework level).
18. ✅ Restructure paper — DONE (3 parts).

**New recommendations (from this review round):**
19. Add normative framework (philosophy of technology).
20. Reframe accessibility from compliance to inclusion (disability studies).
21. Add gender analysis and intersectionality (feminist studies).
22. Add indigenous data sovereignty and CARE principles.
23. Analyse DSW as a platform that shapes social practices (media studies).
24. Add participatory design methodology (design studies).
25. Add knowledge management framework (KM).
26. Reframe migration model as adaptive (complexity science).
27. Apply institutional theory and Ostrom's commons governance (political science).
28. Apply diffusion of innovations and adoption barrier analysis (innovation studies).
29. **Decide: one paper or research programme?** The paper is now too long
    for a single article. Consider splitting into: (a) core argument paper
    (Part I), (b) IS/CS/Law/Economics deep-dive paper (Part II),
    (c) remaining perspectives as a separate paper or handbook (Part III).

---

## Conclusion (Third Round)

The paper has reached a point of diminishing returns for single-paper
comprehensiveness. Three rounds of review have added substantial
analytical depth (from 815 to 2,790 lines) and broadened coverage (from
4 to 11 disciplines). However, the third review round reveals that:

1. **The paper's fundamental conceptual gap** (techno-solutionism) has not
   been addressed. The paper assumes DSW is the answer without questioning
   whether the problem is technological.

2. **Equity and inclusion** are treated as considerations, not design
   principles. Disability, gender, and indigenous perspectives reveal
   this gap.

3. **The paper is too long** for its intended audience. The "How to read"
   guide mitigates this but does not solve it.

4. **The "framework-level" sections** (§14-20) are still not publication
   standard, creating an uneven quality distribution.

5. **The paper lacks a unified theoretical framework** integrating its
   11 perspectives.

**Recommended next step:** Rather than further expanding the paper,
consider:
- **Option A:** Split into 3 companion papers (core, deep-dives,
  perspectives) for journal submission.
- **Option B:** Develop a unified theoretical framework (socio-technical
  systems theory + institutional theory) that integrates all 11
  perspectives, and rewrite the paper around this framework.
- **Option C:** Accept the paper as a "handbook" or "research agenda"
  document (not a journal article) and publish as a technical report.

Each option serves a different purpose and audience. The choice should
be driven by the intended publication venue and reader.

---

*This is the third round of multi-perspective review, bringing 10 new
disciplinary perspectives. It should be read alongside the first
(multi_perspective_review.md) and second (multi_perspective_review_rev3.md)
reviews for complete coverage of 24 disciplinary perspectives across
three review rounds.*