# Literature Review: Digital Sovereign Workplace

**Corpus:** 2,972 papers · 19 categories · 8 subcategory dimensions  
**Sources:** arXiv (1,013) · DOI-registered venues (1,694) · Other (265)  
**Time span:** 2003–2026 (median year 2019; 85% of papers published 2025–2026)  
**Generated:** 2026-10-29

---

## 1. Introduction

The Digital Sovereign Workplace (DSW) research program sits at the intersection of three
converging currents: the political-economic movement for **digital sovereignty** (the
right of organisations and states to control their data, infrastructure, and software
stacks), the technical maturation of **open-source collaboration platforms** (Nextcloud,
openDesk, Collabora, OnlyOffice, identity-federation stacks), and the organisational
transformation of work itself through **hybrid arrangements, AI augmentation, and
employee well-being** concerns. This literature review synthesises a curated corpus of
2,972 papers discovered through taxonomy-aware queries against arXiv, OpenAlex,
Crossref, dblp, Europe PMC, and Semantic Scholar.

The corpus is deliberately broad. The DSW concept cannot be understood through any single
disciplinary lens: data sovereignty is a legal and architectural concern; open-source
platform adoption is a socio-technical one; employee well-being under digital
transformation is an organisational-behaviour one. The taxonomy's 19 categories and 8
subcategory dimensions (theory, application, method, systems, survey, evaluation,
development, mechanism) were designed to surface papers from all these angles and to
reveal where they connect—or fail to.

The review is organised thematically around the major research streams the corpus
reveals, followed by a synthesis of cross-cutting tensions, an assessment of research
gaps, and a forward-looking agenda.

---

## 2. Digital Sovereignty and Data Sovereignty

**Category:** `data-sovereignty` (64 papers) · 151 sovereign-specific papers across the corpus

Digital sovereignty—the principle that organisations, states, and individuals should
retain control over their data, digital infrastructure, and software—has moved from a
policy slogan to an active research programme, particularly in the European context.
The corpus contains 151 papers that engage directly with sovereignty concepts, dispersed
across categories: collaboration (61), data-sovereignty (64), digital-workplace (14),
interoperability (9), open-source (6), and security-compliance (4). This dispersion is
itself a finding: sovereignty is not a single field but a concern that permeates
platform design, governance, health-data sharing, and public-sector strategy.

### 2.1 Sovereign cloud and data-space infrastructure

The Gaia-X initiative and related European data-space architectures anchor the
infrastructural strand. A 2025 arXiv paper on *Policy-Driven AI in Dataspaces*
(arXiv:2507.20014) provides a taxonomy for explainable, compliance-aware AI within
federated data spaces—directly relevant to DSW because sovereign workplaces require
data to remain under organisational control even when AI services process it. Work on
federated data spaces for agri-food ecosystems (Zenodo, 2026) and trusted data spaces
for agricultural supply chains (DOAJ, 2026) demonstrates that the data-space paradigm
is maturing from concept to deployment, with governance frameworks for cross-organisational
data sharing that preserve sovereignty per participant.

The tension between sovereignty and interoperability is a recurring theme. Several
papers on cross-border credential friction and compliance risks in global workforce
mobility (Zenodo, 2026) argue that sovereign identity systems must interoperate across
jurisdictional boundaries to be practical, yet doing so requires trust frameworks that
do not erode the sovereignty they are meant to protect.

### 2.2 Self-hosted and sovereign platform architectures

A smaller but technically focused set of papers addresses self-hosted platforms as the
concrete realisation of workplace sovereignty. Work on *PANEL: An Open-Source,
Self-Hosted Web Platform for Human Evaluation of Generative AI* (arXiv:2609.31392) and
*HiMe: Real-Time Self-Hosted Personal Agent Platform for Health Insights* (arXiv:2607.21019)
demonstrates that self-hosting is moving beyond file storage (the Nextcloud model) into
AI-augmented personal and organisational services. The *Governed Sovereign RAG for
Public Administration* paper (arXiv:2610.36561) is particularly relevant: it proposes
tripartite epistemic routing for retrieval-augmented generation in government settings,
addressing the core DSW challenge of running capable AI on sovereign infrastructure
without leaking data to external providers.

### 2.3 Federated and privacy-preserving computation

The `federated-privacy` category (101 papers) represents the technical engine of
data sovereignty: if data cannot leave its jurisdiction, computation must be brought
to the data. Papers on federated learning for medical imaging (arXiv:2610.27470),
privacy-preserving federated vision-language models for breast cancer screening
(arXiv:2610.36379), and combining homomorphic encryption with differential privacy
in federated learning (arXiv:2610.01650) show a maturing toolkit. The *FLAI Protocol*
(arXiv:2610.17546) proposes decentralised federated learning with on-chain reward
mechanisms—connecting sovereignty to incentive design.

However, the federated-privacy literature remains overwhelmingly domain-specific
(medical imaging, healthcare, IoT). Only a handful of papers address federated
approaches in general workplace collaboration or office-productivity contexts, which
is a significant gap for DSW research.

---

## 3. Open-Source Collaboration Platforms

**Category:** `open-source` (305 papers, the largest in the corpus)

Open-source software is the practical substrate of digital sovereignty. The corpus's
largest category reflects this: 305 papers engage with open source, though many address
open-source methods and culture broadly rather than workplace platforms specifically.
The DSW-relevant subset concerns self-hosted collaboration infrastructure—Nextcloud,
openDesk, Collabora, OnlyOffice, identity-federation stacks—and the socio-technical
dynamics of adopting them.

### 3.1 Self-hosting as sovereign practice

Several papers frame self-hosting not merely as a deployment choice but as an expression
of organisational autonomy. The *Steps towards a digital sovereignty* contribution
(Zenodo, 2026) explicitly positions self-hosted infrastructure as a precondition for
sovereign digital operations. Work on open-source platforms for cultural heritage
(AmalthAI, arXiv:2608.13343) and for generative AI evaluation (PANEL,
arXiv:2609.31392) shows self-hosting expanding into new domains.

A notable gap: despite the DSW taxonomy's explicit inclusion of Nextcloud and openDesk
as seed concepts, the corpus contains very few papers that study these platforms
empirically in workplace settings. This reflects a broader pattern—open-source
collaboration platforms are widely deployed but under-studied in academic literature
compared to proprietary equivalents (Microsoft 365, Google Workspace).

### 3.2 Open-source AI and sovereignty

The intersection of open-source and AI is a fast-growing subtheme. Papers on open-source
LLM platforms, self-hosted personal AI agents, and open evaluation frameworks suggest
that the sovereign-AI stack is being built bottom-up. The *DeepEdu-v1* paper
(arXiv:2609.31568) on efficient agentic LLMs for education, while domain-specific,
demonstrates the pattern: sovereign infrastructure enables domain-specific AI without
external data dependency.

### 3.3 Community and governance dynamics

A substantial portion of the open-source category addresses governance, contribution
dynamics, and sustainability of open-source communities—relevant to DSW because
sovereign platforms depend on healthy upstream communities. The corpus's breadth here
(305 papers spanning software engineering, community dynamics, and platform evaluation)
provides context for understanding the long-term viability of sovereign workplace
solutions.

---

## 4. Employee Well-Being and the Human Side of Digital Work

**Category:** `employee-wellbeing` (261 papers)

The well-being literature is one of the corpus's most voluminous and rapidly growing
streams. It examines how digital transformation, AI augmentation, and remote/hybrid work
affect psychological safety, engagement, burnout, and productivity.

### 4.1 AI and workplace well-being

A central tension in the literature is whether AI in the workplace augments or diminishes
the human work experience. Papers on *Human-Centred AI and Employee Well-Being*
(JBII, 2026) identify psychological safety as a mediating variable: AI systems that
erode employee autonomy and transparency correlate with reduced well-being, while
human-centred AI design that preserves agency shows positive effects. Systematic reviews
of AI and workplace well-being (African Scientific Journal, 2026) synthesise evidence
from 2020–2025, finding mixed outcomes that depend heavily on implementation context.

### 4.2 Digital fatigue and always-on culture

The concepts of digital fatigue, digital anxiety, and online vigilance appear repeatedly.
Work on *Online Vigilance and Digital Well-Being* (JBII, 2026) examines how constant
digital communication in the workplace impacts workers' psychology, mediated by digital
anxiety and availability expectations. This is directly relevant to DSW: sovereign
workplace platforms that replace always-on proprietary communication tools must be
designed to avoid replicating the same psychological harms.

### 4.3 Algorithmic management and employee autonomy

Papers on *The Human Side of Algorithmic Management* (JBII, 2026) explore how employees
experience and negotiate AI-driven performance monitoring. Findings on autonomy, privacy,
fairness, and work intensification in Pakistani workplaces resonate with DSW concerns:
sovereign infrastructure is partly about avoiding opaque algorithmic management by
external platform providers. The *Amplifier Effect* paper (arXiv:2610.07866) on
human-factor risks of AI-suggested correlation in GRC platforms extends this concern to
compliance automation.

### 4.4 Recovery, resilience, and psychosocial risk

A growing subtheme addresses employee recovery and organisational resilience under
digital transformation. Editorials on managing recovery and resilience (Emerald, 2026)
and on the impact of employee competence on organisational survival through crises
connect well-being to organisational outcomes. A deterministic relational graph
architecture for psychosocial risk assessment (Zenodo, 2026) proposes formal methods
for measuring psychosocial risk in digital workplaces—relevant to EU regulatory
frameworks that sovereign employers must comply with.

---

## 5. Hybrid and Remote Work Transformation

**Category:** `hybrid-work` (183 papers) · 12-month growth: +17,900%

Hybrid work is the fastest-growing category in the corpus, with 98% of its papers
published in the last 12 months. This explosive growth reflects the post-pandemic
normalisation of distributed work and its centrality to the DSW agenda: sovereign
workplaces must support collaboration across locations without depending on
proprietary cloud infrastructure.

### 5.1 Employee-office alignment and spatial dynamics

Research on *Employee-Office Workplace Alignment in Hybrid Work Settings* (TU Darmstadt,
2026) examines how organisations match employees to physical and digital workspaces.
Placemaking, interpersonal trust, and temporal structuring in hybrid arrangements
(University of Edinburgh, 2026) provide qualitative evidence that hybrid work is not
simply "remote + office" but a reconfiguration of how work is spatially and temporally
organised. These findings inform the design of sovereign collaboration platforms, which
must support asynchronous, trust-mediated work.

### 5.2 Productivity, engagement, and fatigue

A large subliterature addresses whether hybrid and remote work affect productivity and
job satisfaction. Reviews of remote work fatigue and employee engagement (Zenodo, 2026)
and studies of the impact of remote and hybrid models on productivity (IJSS, 2026) find
context-dependent effects: productivity is maintained or improved for knowledge work
but can decline for roles requiring close coordination. Remote work fatigue is an
emerging construct distinct from general digital fatigue.

### 5.3 Public-sector hybrid work

Evidence from the Canadian public sector (Canadian Public Administration, 2026) on
9-month hybrid arrangements is particularly relevant to DSW, since public-sector
organisations are primary candidates for sovereign workplace adoption. The findings—
that hybrid work is viable in government settings with appropriate policy support—
strengthen the case for sovereign platforms in public administration.

---

## 6. AI and Large Language Models in the Workplace

**Category:** `ai-llm` (280 papers) · 12-month growth: +6,700%

The AI & LLM category is the second-largest and one of the fastest-growing, with 97% of
papers from the last 12 months. This stream examines how AI—particularly large language
models—is reshaping work, decision-making, and organisational practices.

### 6.1 AI as co-worker and productivity augmenter

A substantial literature frames AI as a co-worker rather than a tool. *Artificial
Intelligence as a Co-Worker: Transforming Employment, Skills, Productivity* (Zenodo,
2026) proposes a task-based framework for understanding automation, augmentation, and
workforce reskilling. The *Economic Implications of AI for Employment and Labour
Productivity* study (IJSS, 2026) synthesises 2020–2025 enterprise AI-adoption evidence,
finding productivity gains concentrated in routine cognitive tasks. These findings
matter for DSW because sovereign AI systems must deliver comparable productivity
benefits to displace proprietary alternatives.

### 6.2 Multi-agent systems and collaboration

Papers on LLM-based multi-agent collaboration under partial observability (MASBench,
arXiv:2610.04672) and collaborative learning over model slices (arXiv:2610.12927)
represent the technical frontier. Multi-agent systems are directly relevant to sovereign
workplaces: distributed AI agents running on self-hosted infrastructure could provide
collaboration augmentation without external data dependency. However, the gap between
benchmarks and deployed workplace systems remains wide.

### 6.3 RAG and sovereign AI

Retrieval-augmented generation is a recurring theme. The *Governed Sovereign RAG for
Public Administration* paper (arXiv:2610.36561) and *Automated Extraction of Records of
Processing Activities Using Hybrid RAG* (arXiv:2609.27359) demonstrate RAG architectures
designed for sovereign deployment—processing sensitive organisational data without
sending it to external model providers. This is a critical capability for DSW: it allows
organisations to use capable AI on their own data within their own infrastructure.

### 6.4 AI governance and ethical concerns

Editorials on intelligent technologies and the future of work (Frontiers in Sociology,
2026) and on STARA (smart technology, AI, robotics, algorithms) implications for
contemporary workplaces (Emerald, 2026) raise governance questions central to DSW: who
controls AI systems, how are decisions auditable, and what happens to worker autonomy.
The sovereign-workplace proposition—that organisations should control their AI
infrastructure—directly addresses these concerns.

---

## 7. Digital Transformation and Adoption

**Category:** `digital-transformation` (130 papers) · `adoption-change` (252 papers)  
**12-month growth:** Digital Transformation +12,100%; Adoption & Change 100% recent

Digital transformation and adoption dynamics form a major stream, examining how
organisations adopt, adapt to, and are changed by digital technologies. For DSW, this
literature is essential: sovereign platforms will only succeed if organisations can
actually adopt them.

### 7.1 Digital capability and organisational resilience

Work on *Digital Skills Are Not Enough: Digital-Human Capability Profiles and Employee
Resilience* (Merits, 2026) argues that digital skills alone are insufficient for
transformation success—organisations need integrated human-digital capability profiles.
The *Exponential SME Framework* (arXiv:2610.01129) proposes non-linear growth through
digital capabilities, relevant to DSW because SMEs are a key adoption segment for
sovereign platforms but face capability constraints.

### 7.2 Digital fatigue and the adoption paradox

The *Digital Workplace, Digital Fatigue, Digital Minimalism* study (Zenodo, 2026) and
work on digital workload and psychological well-being (Zenodo, 2026) reveal a paradox:
digital transformation can simultaneously enable productivity and erode well-being.
The protective role of digital minimalism suggests that sovereign platforms should be
designed for mindful use, not engagement maximisation—a contrast with the attention
economy dynamics of proprietary platforms.

### 7.3 AI-enabled HRM and organisational performance

Papers on AI-enabled human resource management practices (Acta Innovationes, 2026) and
AI as a catalyst for leadership transformation in SMEs (LODJ, 2026) examine how AI
changes management practices. The DSW implication is that sovereign AI infrastructure
should support HRM functions (recruitment, performance evaluation, learning) without
the opacity and data-extraction dynamics of proprietary HR platforms.

### 7.4 The SME adoption gap

The `sme-adoption` category is the corpus's thinnest at only 6 papers, with zero papers
in method, evaluation, and application subcategories. This is a critical gap: SMEs are
the largest segment of the economy and the hardest to serve with sovereign platforms
due to limited IT capacity. The few papers available—on AI use in workplace tasks and
firm-level value (Zenodo, 2026) and navigating the infrastructure-innovation gap
(IGI Global, 2026)—suggest that SME adoption of sovereign solutions requires bundled,
low-operational-burden offerings.

---

## 8. Identity, Access, and Interoperability

**Categories:** `identity-access` (40 papers) · `interoperability` (238 papers)

Identity and interoperability are the connective tissue of sovereign workplaces: without
federated identity, cross-organisational collaboration, and standards-based
interoperability, sovereign platforms become isolated islands.

### 8.1 Federated identity and cross-border credentials

The corpus contains work on trust infrastructure for cross-border credential friction
(Zenodo, 2026), directly addressing the problem of sovereign identity systems that must
interoperate across jurisdictions. The ID Union and IDSA paradigms—decentralised,
self-sovereign identity—are the architectural answer to the DSW identity challenge,
though the corpus has limited empirical evaluation of these systems in production
workplace settings.

### 8.2 Interoperability standards and data spaces

The interoperability category (238 papers) is the fifth-largest, reflecting the
importance of standards-based integration. Papers on privacy-preserving AI for real-time
ECG monitoring (arXiv:2610.25094) and consumer empowerment frameworks (arXiv:2610.04877)
span the technical and policy dimensions of interoperability. European data-space
initiatives (Gaia-X, IDSA) provide the governance frameworks within which sovereign
workplace platforms must interoperate.

### 8.3 The identity-access research gap

The `identity-access` category is relatively small (40 papers) and has notable gaps:
only 1 paper each in method, application, and systems subcategories. Given that identity
federation (SSO, OIDC, SAML) is a core DSW capability, this under-representation
suggests that academic literature has not caught up with the practical importance of
federated identity in sovereign deployments.

---

## 9. Public Sector, Education, and Security

### 9.1 Public sector and education

**Category:** `public-sector` (154 papers)

Public-sector organisations are primary candidates for sovereign workplace adoption due
to regulatory requirements for data control and digital autonomy. The corpus addresses
public-sector digital transformation broadly: E-HRM as a behavioural enabler of
public-sector transformation (Malque, 2026), digital financial reporting and audit
technologies (2026), and assessments of the relationship between digital transformation
and employment indicators (Ekonomisti, 2026).

Education is a significant subtheme (475 keyword hits for "education"), spanning digital
skills training, AI in education, and instructional design for workplace-oriented
courses. The DSW relevance is twofold: education systems need sovereign platforms, and
workforce digital skills are a precondition for sovereign platform adoption.

### 9.2 Security and compliance

**Category:** `security-compliance` (48 papers)

Security and compliance are enabling concerns for DSW: sovereign platforms must meet the
same regulatory standards as proprietary ones. The *CYBERFORT* paper (arXiv:2610.09918)
on a compliance-chain platform operationalising the Cyber Resilience Act for SMEs is
directly relevant—it addresses how small organisations can demonstrate compliance in a
fragmented regulatory landscape. The *ClinConNet* blockchain-based dynamic consent
management platform (arXiv:2602.02610) demonstrates how consent can be managed in a
sovereign, auditable way—a capability transferable to workplace data governance.

The security-compliance category is smaller than expected (48 papers), suggesting that
the academic literature on sovereign-specific security architectures (as opposed to
general cybersecurity) remains underdeveloped.

---

## 10. Cross-Cutting Themes and Synthesis

### 10.1 The sovereignty–capability tension

A recurring tension across the corpus is between sovereignty (control over data and
infrastructure) and capability (access to best-in-class tools). Papers on AI productivity
gains (ai-llm category) and on digital transformation benefits (adoption-change)
demonstrate the value of advanced digital tools. Simultaneously, the sovereignty
literature argues for control and autonomy. The DSW proposition is that open-source,
self-hosted, and federated approaches can deliver both—but the corpus provides limited
empirical evidence that sovereign platforms match proprietary ones on capability. This
is the central research question the field must answer.

### 10.2 The well-being–technology nexus

The employee-well-being literature (261 papers) and the AI-in-workplace literature
(280 papers) are largely separate streams that should be in dialogue. Digital fatigue,
algorithmic management, and always-on culture are well-documented harms of current
digital workplaces. Sovereign platforms offer an opportunity to redesign workplace
technology with well-being as a first-class design goal rather than an afterthought—
but no papers in the corpus explicitly test this hypothesis.

### 10.3 Federated computation as the sovereignty engine

The federated-privacy literature (101 papers) provides the technical foundation for
data sovereignty: keeping data in place while enabling collaborative computation. Yet
this work is concentrated in medical imaging and healthcare, with very little in
general workplace collaboration or office-productivity contexts. Transferring federated
techniques from healthcare to workplace collaboration is a significant opportunity.

### 10.4 Open source as substrate

The open-source category (305 papers) is the largest, but much of it addresses
open-source software engineering and community dynamics broadly rather than workplace
platforms specifically. The DSW-specific subset—self-hosted collaboration platforms,
sovereign AI stacks, identity-federation tools—is thin. This reflects a maturity gap:
the academic literature has not yet caught up with the deployment of sovereign
workplace platforms in practice.

### 10.5 The temporal concentration

A striking feature of the corpus is its recency: 85% of papers are from 2025–2026, and
the 12-month growth rates for hybrid work (+17,900%), digital transformation (+12,100%),
and AI/LLM (+6,700%) are extraordinary. This reflects both the rapid acceleration of
digital transformation research and the query design's recency bias. The implication for
DSW research is that the field is being defined right now, with a window for
foundational contributions.

---

## 11. Research Gaps

The corpus analysis reveals several significant gaps that the DSW research programme
should address:

| Gap | Evidence | Priority |
|-----|----------|----------|
| **SME adoption of sovereign platforms** | `sme-adoption` has only 6 papers; method, evaluation, and application subcategories are empty | High — SMEs are the largest economic segment and face the highest adoption barriers |
| **Empirical evaluation of sovereign workplace platforms** | `digital-workplace/systems` has 1 paper; `data-sovereignty/method` has 1 paper | High — without empirical evidence, the sovereignty–capability tension remains unresolved |
| **Identity and access in sovereign contexts** | `identity-access` has 40 papers with method/application/systems subcategories nearly empty | High — federated identity is a core DSW capability but under-studied academically |
| **Federated computation for workplace collaboration** | `federated-privacy` is 101 papers but overwhelmingly healthcare-focused | Medium — techniques exist but have not been transferred to workplace collaboration |
| **Well-being effects of sovereign vs. proprietary platforms** | No papers directly compare well-being outcomes across platform sovereignty models | Medium — a novel hypothesis that DSW can uniquely test |
| **Open-source collaboration platforms in production** | Very few empirical studies of Nextcloud/openDesk/Collabora in workplace settings despite their deployment | Medium — practice is ahead of theory |
| **Security architectures specific to sovereign deployments** | `security-compliance` has 48 papers, mostly general cybersecurity | Medium — sovereign security has distinct requirements (self-hosted trust, federated audit) |
| **Economic models for sovereign platform sustainability** | Limited work on the business and sustainability models for open-source sovereign platforms | Medium — long-term viability depends on sustainable models |

---

## 12. Research Agenda

Based on the corpus synthesis and gap analysis, the following research agenda emerges
for the Digital Sovereign Workplace programme:

1. **Empirical platform evaluation:** Conduct controlled studies comparing sovereign
   platforms (Nextcloud, openDesk) with proprietary equivalents (Microsoft 365, Google
   Workspace) on productivity, well-being, and capability dimensions. The corpus
   provides strong baselines for productivity and well-being measures but no
   head-to-head sovereign-vs-proprietary comparisons.

2. **Federated collaboration infrastructure:** Transfer federated learning and
   privacy-preserving computation techniques from healthcare to workplace collaboration.
   The technical toolkit is mature (homomorphic encryption, differential privacy,
   federated learning) but has not been applied to office-productivity and
   collaboration contexts.

3. **SME adoption pathways:** Investigate bundled, low-operational-burden sovereign
   platform offerings for SMEs, addressing the capability and resource constraints
   identified in the adoption literature. The `sme-adoption` gap is the corpus's most
   acute.

4. **Well-being-centred design:** Test the hypothesis that sovereign platforms—designed
   for organisational control rather than engagement maximisation—produce better
   well-being outcomes than proprietary platforms. The well-being literature provides
   the measurement instruments; the sovereign platform literature provides the
   intervention.

5. **Identity federation at scale:** Study federated identity (SSO, OIDC, SAML,
   self-sovereign identity) in multi-organisational sovereign deployments, addressing
   the cross-border credential friction identified in the interoperability literature.

6. **Sovereign AI architectures:** Build on the RAG and agentic-LLM work to develop
   AI-augmented collaboration capabilities that run entirely on sovereign infrastructure,
   addressing the governance and autonomy concerns raised in the AI-in-workplace
   literature.

7. **Economic and sustainability models:** Develop and test business models for
   open-source sovereign platforms that ensure long-term viability without replicating
   the data-extraction dynamics of proprietary platforms.

---

## 13. Methodology

This review synthesises a corpus of 2,972 papers discovered through taxonomy-aware
queries against arXiv, OpenAlex, Crossref, dblp, Europe PMC, and Semantic Scholar. The
taxonomy (19 categories, 8 subcategory dimensions) is defined in
`config/taxonomy.yaml`. Papers are auto-classified into the taxonomy and validated by
`scripts/validate_papers.py`. Corpus statistics are generated by
`scripts/standard_stats.py`; trend analysis by `tools/trend_scanner.py`; landscape
analysis by `tools/landscape_analyzer.py`; concept graph by `tools/extract_concepts.py`
and `tools/relate_concepts.py` (65 concepts). The auto-generated category-level review
in `docs/research/literature_review.md` provides per-category detail; this document
provides the thematic synthesis. The full pipeline is reproducible via `make all`.

---

## 14. Conclusion

The Digital Sovereign Workplace research programme sits at the confluence of digital
sovereignty, open-source infrastructure, AI augmentation, and workplace transformation.
The corpus of 2,972 papers reveals a field that is rapidly growing (85% of papers from
2025–2026), intellectually diverse (19 categories spanning computer science, information
systems, organisational behaviour, and public policy), and rich with opportunity. The
central finding is a sovereignty–capability tension: the literature demonstrates the
value of advanced digital tools and the harms of opaque, proprietary platforms, but
provides little empirical evidence that sovereign alternatives can match proprietary ones
on capability while delivering on autonomy, privacy, and well-being. Resolving this
tension—through empirical platform evaluation, federated collaboration infrastructure,
SME adoption pathways, and well-being-centred design—is the agenda this review
identifies for the DSW research programme.
