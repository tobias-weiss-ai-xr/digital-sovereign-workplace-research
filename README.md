<h1 align="center">
  <strong>Digital Sovereign Workplace</strong>
</h1>
<h3 align="center">Evidence base for digital sovereign workplace research</h3>

### 🔗 Links

- **License**: https://github.com/tobias-weiss-ai-xr/digital-sovereign-workplace-research/blob/main/LICENSE
- **CI**: https://github.com/tobias-weiss-ai-xr/digital-sovereign-workplace-research/actions/workflows/validate.yml
- **GitHub Pages**: https://tobias-weiss-ai-xr.github.io/digital-sovereign-workplace-research/


> 📚 **Digital sovereign workplace research corpus:** evidence base for sovereign,
> open, and interoperable digital workplaces. Part of the family of consistent
> `*-research` corpora.

## What you get

| Capability | How |
|------------|-----|
| 📄 **Curated corpus** | `papers.yaml` is the source of truth — one structured entry per paper |
| ✅ **Auto-validation** | `scripts/validate_papers.py` checks schema, duplicates, URL normalization, LaTeX artifacts |
| 🧾 **Auto-generated README** | `scripts/generate_readme.py` renders the paper list grouped by your taxonomy |
| 📊 **Statistics & trends** | `scripts/standard_stats.py` → `statistics.json` (momentum, gaps, bursts, venues, authors) |
| 🔍 **Literature review report** | `scripts/analysis/generate_reports.py` → `docs/research/literature_review.md` + `trends.md` |
| 🧭 **Topic planning** | `tools/topic_planner.py`, `tools/trend_scanner.py`, `tools/landscape_analyzer.py`, `tools/brief_generator.py` |
| 🔎 **New paper discovery** | `scripts/fetch/fetch_new_papers.py` (arXiv), `fetch_other_sources.py` (dblp/crossref/europepmc), `fetch_openalex_bulk.py` |
| 🐙 **GitHub repos discovery** | `scripts/fetch/fetch_github_repos.py` (optional, config-driven via `github_queries` in taxonomy.yaml) |
| 🦊 **GitLab projects discovery** | `scripts/fetch/fetch_gitlab_repos.py` (optional, config-driven via `gitlab_queries` in taxonomy.yaml) |
| 🏠 **Codeberg repos discovery** | `scripts/fetch/fetch_codeberg_repos.py` (optional, config-driven via `codeberg_queries` in taxonomy.yaml) |
| 📰 **News / intelligence digest** | `run_pipeline.py` — RSS/Atom + arXiv + GitHub releases + catalogs (e.g. CISA KEV) → scored, de-duplicated daily digest (`data/latest.md`/`.html`/`.json`) |
| 🖥️ **GitHub Pages site** | `docs/index.html` — searchable, filterable paper browser |
| 🤖 **Agentic workflow** | `AGENTS.md` + `config/taxonomy.yaml` make this repo agent-friendly by design |

## 🎯 Overview

This repository is the evidence base for the **digital sovereign workplace**
research program: a corpus of papers on sovereign, open, and interoperable
digital workplaces (collaboration suites, identity & access, data sovereignty,
public-sector and SME adoption), analyzed with the taxonomy → momentum → burst
→ gap pipeline shared by the `*-research` corpus family.

**Research target:** the definitive, corpus-grounded guides on
(1) **designing and operating** sovereign digital workplaces and
(2) **adopting** them in public-sector and SME contexts.

### Research Scope

| Metric | Value |
|--------|-------|
| **Papers Analyzed** | 0 (seed in progress) |
| **Categories** | 15 |
| **Research Aspects** | 10 |

## 📖 How it works

```
config/taxonomy.yaml ──► papers.yaml ──► validate_papers.py
                          │   ▲              │
                          ▼   └── fetch_* ───┘
                   generate_readme.py ──► README.md paper list (auto)
                          │
                          ▼
                  standard_stats.py ──► statistics.json, docs/papers.json,
                                        README.md corpus statistics (auto)
                          │
                          ▼
              analysis/generate_reports.py ──► docs/research/*.md
```

The generated README sections (paper list + corpus statistics) are
**marker-delimited** (`<!-- BEGIN … -->` … `<!-- END … -->`) and are owned by
the pipeline: `generate_readme.py` and `standard_stats.py` regenerate exactly
their section on every run. Everything else in the README is user-owned prose
and is left untouched. If a repo drops a section entirely (e.g. the paper list
lives on the GitHub Pages site), the owning script skips it gracefully instead
of erroring.

- **Never edit the generated README sections by hand** — run the pipeline.
- The **taxonomy lives in one place** (`config/taxonomy.yaml`); every script reads it via `scripts/research_config.py`, which now validates the config up front so mistakes fail loudly.
- **CI (validate.yml)** runs on every push/PR and weekly to discover new papers. The `validate` job re-checks that all generated outputs are fresh (README, statistics, reports), and a `test` job runs the pytest suite.

## 🧪 Local pipeline (all in one)

```bash
make all          # validate → check freshness → generate → test
# …or run the raw steps:
python3 scripts/validate_papers.py && \
python3 scripts/generate_readme.py && \
python3 scripts/standard_stats.py && \
python3 scripts/analysis/generate_reports.py

# Freshness checks (non-destructive; exit 1 if stale) — used by CI
python3 scripts/generate_readme.py --check
python3 scripts/standard_stats.py --check
python3 scripts/analysis/generate_reports.py --check

# Unit tests
python3 -m pytest
```

## 📰 News / Intelligence Digest (`run_pipeline.py`)

A complementary pipeline that ingests **RSS/Atom feeds**, **arXiv queries**,
**GitHub release feeds**, and **structured catalogs** (e.g. CISA KEV), then
classifies + scores each item, de-duplicates against a seen-history, and renders
a daily digest (`data/latest.md`, `data/latest.html`, `data/raw.json`).

```bash
python3 run_pipeline.py --dry-run   # ingest + score only (no writes)
python3 run_pipeline.py              # full run → writes digest + marks seen
python3 run_pipeline.py --top 30     # smaller digest
```

Sources, weights and keyword classification live in `config/sources.yml`.

### Anti-saturation controls

Without guards, static catalogs (CISA KEV's 1,600+ entry list) and full-archive
feeds (Snyk's 1,600+ post history) recycle old items every run, and one
high-volume feed (e.g. a project blog) can crowd out everything else. Three
config knobs in `config/sources.yml` prevent this:

| Knob | Effect |
|------|--------|
| `recent_days` (per source) / `default_recent_days` | Drop items published/added older than N days. Applied to RSS + catalog sources; **opt in only on archive/catalog feeds** — normal blogs already return recent items, so leave the default at `0` to avoid starving low-frequency, high-signal feeds. |
| `max_items` (per source) | Hard cap on raw items kept from one source (e.g. 15 for an archive feed). |
| `max_source_share` (global) | Hard ceiling on how many digest slots a single source may occupy (default `0.40` → no source takes >40% of the digest). |

> Why `default_recent_days: 0`? Only archive/catalog feeds recycle. A blanket
> window would silently drop infrequent but high-signal feeds (e.g. Project
> Zero, which posts monthly). Set `recent_days` explicitly on the feeds that
> need it.

## 🔎 Discovery & utility scripts

Beyond the core pipeline, several scripts remain available for manual / scheduled use:

| Script | What it does |
|---|---|
| `scripts/fetch/fetch_new_papers.py` | arXiv discovery; `--create-pr` opens a weekly PR (used by CI) |
| `scripts/fetch/fetch_openalex_bulk.py` | OpenAlex bulk discovery per category (`--months`, `--local`) |
| `scripts/fetch/fetch_other_sources.py` | dblp / crossref / Europe PMC / Semantic Scholar discovery |
| `scripts/fetch/fetch_metadata.py` | backfill authors/abstracts/venues for existing arXiv papers |
| `scripts/fetch/saturate_papers.py` | expand queries & loop arXiv until corpus saturates |
| `scripts/fetch/fetch_github_repos.py` / `fetch_gitlab_repos.py` / `fetch_codeberg_repos.py` | discover topic-relevant code repos → `repos.yaml` |
| `scripts/fetch/search_arxiv_html.py` / `search_arxiv_offline.py` | alternate/ad-hoc arXiv search helpers |
| `scripts/export_bibtex.py` | write `paper/references.bib` from `papers.yaml` |
| `scripts/visualize_statistics.py` | visualise `statistics.json` |

The repo-discovery fetchers share rate-limit/backoff + relevance logic in `scripts/fetch/repos_common.py`.

## 🤖 Agentic workflow (AGENTS.md)

This repo is designed to be driven by coding agents (OpenCode, Claude Code, …):

- **Spec-style guardrails** in `AGENTS.md` — agents know the pipeline, never edit README, always re-validate.
- **One config file** to change → one re-run to verify (low context cost for agents).
- **Auto-validation** gives agents an objective pass/fail signal.
- **Weekly discovery** keeps the corpus fresh without human babysitting.

<!-- BEGIN PAPER LIST -->

## 📚 Paper list

- [📚 Digital Workplace](#digital-workplace)
  - [Theory](#theory)
  - [Systems](#systems)
- [📚 Data Sovereignty](#data-sovereignty)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
- [📚 Collaboration & Productivity](#collaboration-&-productivity)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
  - [Systems](#systems)
- [📚 Identity & Access](#identity-&-access)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
  - [Systems](#systems)
- [📚 Interoperability & Standards](#interoperability-&-standards)
  - [Theory](#theory)
  - [Systems](#systems)
- [📚 Open Source](#open-source)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
- [📚 Public Sector & Education](#public-sector-&-education)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
  - [Survey](#survey)
  - [Systems](#systems)
  - [Development](#development)
- [📚 SME Adoption](#sme-adoption)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
  - [Evaluation](#evaluation)
- [📚 Security & Compliance](#security-&-compliance)
  - [Application](#application)
- [📚 Adoption & Change](#adoption-&-change)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
  - [Survey](#survey)
  - [Systems](#systems)
  - [Evaluation](#evaluation)
  - [Mechanism](#mechanism)
- [📚 Architecture & Infrastructure](#architecture-&-infrastructure)
- [📚 Evaluation & Case Studies](#evaluation-&-case-studies)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
  - [Survey](#survey)
  - [Systems](#systems)
  - [Evaluation](#evaluation)
- [📚 Surveys & Reviews](#surveys-&-reviews)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
  - [Survey](#survey)
  - [Systems](#systems)
- [📚 Methods](#methods)
  - [Method](#method)
  - [Theory](#theory)
  - [Systems](#systems)
  - [Evaluation](#evaluation)
- [📚 Tooling & Platforms](#tooling-&-platforms)
  - [Method](#method)
  - [Theory](#theory)
  - [Application](#application)
  - [Systems](#systems)
  - [Evaluation](#evaluation)

### Digital Workplace

#### Theory

##### 2026

- [2026] **Judicial Interpretation And The Development Of International Law: A Study Of Emerging Norms And Standards** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23368520)]
- [2026] **AGNES NUMPSA COURT CASE SOON ROI EU** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23056800)]
- [2026] **Toward Sovereign Personal Artificial Intelligence: Applying the (B)+(F)=Nf Framework to Unified Personal AI, Shared Emotional Memory, and Witnessing Objects** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20451821)]
- [2026] **Struggles for Recognition in the Digitalizing Workplace** *Springer eBooks* [[paper](https://doi.org/10.1007/978-3-032-34028-3_3)]
- [2026] **Inversion of the Sovereign Human: Youth, Agency and the Pathology of Managed Societies** *Figshare* [[paper](https://doi.org/10.6084/m9.figshare.32143636)]
- [2026] **Who Governs Sovereign Software? Funding Instruments and Administrative Authority in France and Germany** *SSRN Electronic Journal* [[paper](https://doi.org/10.2139/ssrn.7253718)]

##### 2025

- [2025] **The Digital Sovereign: India's Strategic Evolution in the Global Trade Order – Structural Transformations, Regulatory Architecture, and Economic Statecraft (2025)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.18451140)]
- [2025] **Geopolitical Pressures and Digital Sovereignity: Indonesia’s Strategic Response to US-China Data Hegemony** *Jurnal Hubungan Internasional* [[paper](https://doi.org/10.20473/jhi.v18i2.76019)]

##### 2024

- [2024] **Digital Mobilities and Smart Borders** [[paper](https://doi.org/10.1515/9783110714050)]
- [2024] **Digital identities, algorithms and exclusion** *Digital Mobilities and Smart Borders* [[paper](https://doi.org/10.1515/9783110714050-004)]
- [2024] **Index** *Digital Mobilities and Smart Borders* [[paper](https://doi.org/10.1515/9783110714050-010)]

##### 2023

- [2023] **Exploring the Applications, Data and Services Needed for a Cloud-Based Workplace for the Public Sector** *Communications in computer and information science* [[paper](https://doi.org/10.1007/978-3-031-36001-5_36)]
- [2023] **Self-Sovereign Identity: An Examination of the Pragmatics Behind Idealistic Digital Identity Management** *Research Square* [[paper](https://doi.org/10.21203/rs.3.rs-3406616/v1)]
- [2023] **The Working Sovereign: A conversation with Axel Honneth** *Journal of Classical Sociology* [[paper](https://doi.org/10.1177/1468795x231170980)]

##### 2022

- [2022] **Sovereign Wealth Funds** *Agenda Publishing eBooks* [[paper](https://doi.org/10.2307/j.ctv2tjdhjj)]

##### 2021

- [2021] **Emerging Trends for Digital Workplace Learning** *Transformative Digital Technology for Effective Workplace Learning* [[paper](https://doi.org/10.1201/9781003149132-9)]
- [2021] **The Digital Future of the Workplace: Three Possible Scenarios** *Transformative Digital Technology for Effective Workplace Learning* [[paper](https://doi.org/10.1201/9781003149132-5)]

##### 2020

- [2020] **Digital Workplace Development** *Build a Next-Generation Digital Workplace* [[paper](https://doi.org/10.1007/978-1-4842-5512-4_4)]
- [2020] **Sovereigns, Viruses, and the Law** *Law in context* [[paper](https://doi.org/10.26826/law-in-context.v37i1.117)]

##### 2018

- [2018] **How We Learn at the Digital Workplace** *Digital Workplace Learning* [[paper](https://doi.org/10.1007/978-3-319-46215-8_1)]
- [2018] **Massive Open Online Courses in Digital Workplace Learning** *Digital Workplace Learning* [[paper](https://doi.org/10.1007/978-3-319-46215-8_9)]
- [2018] **Designing Flipped Learning for Digital Workplace Learning** *Digital Workplace Learning* [[paper](https://doi.org/10.1007/978-3-319-46215-8_6)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **Resisting Through Dependence: Microsoft 365 And Digital Sovereignty In France** *Journal of the Association for Information Systems* [[paper](https://aisel.aisnet.org/treos_ecis2026/69)]

[⬆ Back to top](#paper-list)

### Data Sovereignty

#### Method

##### 2026

- [2026] **Inspirational leadership and its role in enhancing strategic sovereigntyAn analytical study of the opinions of a sample of administrative leaders at AlAin Iraqi Private University.** *Al-Furat Journal of Innovations in Management Sciences* [[paper](https://afjims.atu.edu.iq/index.php/ms/article/view/119)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **Towards a Cloud Fog Edge System for Smart Building** [[paper](https://arxiv.org/abs/2610.01647)]
- [2026] **FLAI Protocol: Decentralized Federated Learning with On-Chain Rewards and sPEG-Based Contribution Scoring** [[paper](https://arxiv.org/abs/2610.17546)]
- [2026] **Governed Sovereign RAG for Public Administration: Tripartite Epistemic Routing, Facet-Guided Clarification, and Deterministic Numeric Verification in Citizen Services** [[paper](https://arxiv.org/abs/2610.36561)]
- [2026] **THE EL-RAKHAWI GLOBAL FRAMEWORK FOR NEURO-RIGHTS AND BRAIN-COMPUTER INTERFACE GOVERNANCE Protecting Cognitive Liberty in the Age of Neural Integration** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23296815)]
- [2026] **Human+AI Co-presence: Designing for Presence in Shared Intelligence-Augmenting Spaces** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23647529)]
- [2026] **A Deterministic Relational Graph Architecture for Psychosocial Risk Assessment: Complete Methodological Suite, Mathematical Proofs, Field Implementation Guidelines, and Executable Calculation Engine (Main Paper and Technical Annexes A–E)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23368463)]
- [2026] **Dynamic Flow, Static Graph: KV Cache Reuse for Efficient LLM Serving on Mobile NPUs** [[paper](https://arxiv.org/abs/2609.34727)]
- [2026] **From Pilots to Production: Lessons in Cross-Institutional Federated Training and Artificial Intelligence for Science** [[paper](https://arxiv.org/abs/2609.39803)]
- [2026] **DeepEdu-v1: Efficient and Scalable Agentic LLMs for Vietnamese Education** [[paper](https://arxiv.org/abs/2609.31568)]
- [2026] **Automated Extraction of Records of Processing Activities (RoPA) Using Hybrid RAG and Locally Deployed Large Language Models** [[paper](https://arxiv.org/abs/2609.27359)]
- [2026] **The Human Cost of Artificial Intelligence: Opportunities for a Future of AI Made For All in Australia A submission to the Joint Select Committee on Artificial Intelligence** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22926308)]
- [2026] **LABOR MARKET CHALLENGES IN BUSINESS TRANSFORMATION BY AI: EMPIRICAL EXPERIENCE OF SELECTED EUROPEAN COUNTRIES** *Collection of papers New economy* [[paper](https://doi.org/10.61432/cpne0401061r)]
- [2026] **From compliance to innovation: Reframing occupational noise-induced hearing loss prevention in Africa through health equity and the Fourth Industrial Revolution** *South African Journal of Communication Disorders* [[paper](https://doi.org/10.4102/sajcd.v73i1.1182)]
- [2026] **Editorial: Legal and ethical reforms for neurotechnological advancements in the global south: perspective and challenges** *Frontiers in Human Neuroscience* [[paper](https://doi.org/10.3389/fnhum.2026.1985765)]
- [2026] **Open Source as Enabler for Smart Data Ecosystems – How collaboration shapes sovereignty and interoperability across industrial applications** *Industry 4.0 Science* [[paper](https://doi.org/10.30844/i4se.26.4.1)]
- [2026] **Harnessing the Wisdom of LLM Crowds through Complementarity-Driven Iterative Collaboration** [[paper](https://arxiv.org/abs/2607.29087)]
- [2026] **zk-ScalHard: Scalable and Hardware-Rooted Privacy-Preserving Authentication for Secure OTA Updates in Zonal SDVs** [[paper](https://arxiv.org/abs/2607.07371)]
- [2026] **Inference Economics of Enterprise Coding Agents: A Case Study of Cloud vs. On-Premise LLMs** [[paper](https://arxiv.org/abs/2607.13080)]
- [2026] **Securing LLMs in the Wild: Privacy and Security Challenges at the Edge** [[paper](https://arxiv.org/abs/2607.13088)]
- [2026] **CHARLIE: An On-Premise Multi-Agent Retrieval-Augmented Generation System for Evidential Reasoning in Forensic Science** [[paper](https://arxiv.org/abs/2607.05428)]
- [2026] **Embedded Blockchain Infrastructure Management (eBIM): A RISC-V-Empowered Hardware--Software Co-Design Framework Towards Trustworthy Blockchain** [[paper](https://arxiv.org/abs/2607.07625)]
- [2026] **Does the Responsible AI Guidance Adequately Protect Māori in Predictive Workplace Safety Regulation?** *New Zealand journal of health and safety practice.* [[paper](https://doi.org/10.26686/nzjhsp.v3i2.10605)]
- [2026] **A White Paper on Human Augmentation for Economy Productivity Shift, Human-Machine Interaction, Sovereignty and Individual Agency Preservation** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21526825)]
- [2026] **Multi-Agent Retrieval-Augmented Generation for Efficient Cloud Knowledge Base Search in Telecom SNOC Environment** [[paper](https://arxiv.org/abs/2609.01618)]
- [2026] **Deep Learning in Seismic Interpretation: Federated Advances in Salt Dome Segmentation** [[paper](https://arxiv.org/abs/2606.14905)]
- [2026] **Commons-Governed Artificial Intelligence: A Taxonomy of Collective Governance** [[paper](https://arxiv.org/abs/2606.15466)]
- [2026] **Continuous improvement in the age of AI: human and relational barriers in public higher education** *The TQM Journal* [[paper](https://doi.org/10.1108/tqm-04-2026-0262)]
- [2026] **Autonomic Federated-Market Orchestration for the Edge-Cloud Continuum** [[paper](https://arxiv.org/abs/2605.27106)]
- [2026] **OpenAaaS: An Open Agent-as-a-Service Framework for Distributed Materials-Informatics Research** [[paper](https://arxiv.org/abs/2605.13618)] [[code](https://github.com/Wolido/OpenAaaS)]
- [2026] **When Migration Policy Becomes Persecution: An Analysis of ICE Practices and the Trump Administration’s Migration Policies in Light of Human Rights and Crimes Against Humanity.** *RCMOS - Revista Científica Multidisciplinar O Saber* [[paper](https://doi.org/10.51473/rcmos.v1i1.2026.2326)]
- [2026] **THE NEW PARADIGM OF EDUCATION IN VOCATIONAL TRAINING UNDER DIGITAL TRANSFORMATION: GLOBAL EXPERIENCE AND THE CHINESE PATH** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21218100)]
- [2026] **QoS-Aware Token Scheduling and Private Data Valuation for Multi-Modal Agentic Networks** [[paper](https://arxiv.org/abs/2606.15573)]
- [2026] **Structural Dissolution: How Artificial Intelligence Dismantles Coordination Architecture and Reconfigures the Political Economy of Production** [[paper](https://arxiv.org/abs/2604.27435)]
- [2026] **Take the Train: Africa at the Crossroad of Modern AI** [[paper](https://arxiv.org/abs/2603.21795)]
- [2026] **Scalable Cross-Facility Federated Learning for Scientific Foundation Models on Multiple Supercomputers** [[paper](https://arxiv.org/abs/2603.19544)]
- [2026] **SuperLocalMemory V3: Information-Geometric Foundations for Zero-LLM Enterprise Agent Memory** [[paper](https://arxiv.org/abs/2603.14588)]
- [2026] **Berta: an open-source, modular tool for AI-enabled clinical documentation** [[paper](https://arxiv.org/abs/2603.23513)]
- [2026] **Privacy-Preserving Federated Fraud Detection in Payment Transactions with NVIDIA FLARE** [[paper](https://arxiv.org/abs/2603.13617)]
- [2026] **Quecto-V1: Empirical Analysis of 8-bit Quantized Small Language Models for On-Device Legal Retrieval** [[paper](https://arxiv.org/abs/2602.16640)]
- [2026] **From Static Repositories to Agentic Knowledge Webs: ResearchTwin and the S-Index for Federated Human-AI Research Discovery** [[paper](https://arxiv.org/abs/2603.00080)]
- [2026] **FedAvg-Based CTMC Hazard Model for Federated Bridge Deterioration Assessment** [[paper](https://arxiv.org/abs/2602.20194)]
- [2026] **MemTrust: A Zero-Trust Architecture for Unified AI Memory System** [[paper](https://arxiv.org/abs/2601.07004)]

##### 2025

- [2025] **RAGdb: A Zero-Dependency, Embeddable Architecture for Multimodal Retrieval-Augmented Generation on the Edge** [[paper](https://arxiv.org/abs/2602.22217)]

##### 2023

- [2023] **New Digital Work and Digital Sovereignty at the Workplace – An Introduction** *New Digital Work* [[paper](https://doi.org/10.1007/978-3-031-26490-0_1)]

##### 2020

- [2020] **Indigenous Data Sovereignty** *Indigenous Data Sovereignty and Policy* [[paper](https://doi.org/10.4324/9780429273957-10)]
- [2020] **Conversational Collaboration Platforms** *The AI-Powered Workplace* [[paper](https://doi.org/10.1007/978-1-4842-5476-9_8)]

##### 2016

- [2016] **Indigenous data sovereignty: a Māori health perspective** *Indigenous Data Sovereignty* [[paper](https://doi.org/10.22459/caepr38.11.2016.11)]
- [2016] **Governing data and data for governance: the everyday practice of Indigenous sovereignty** *Indigenous Data Sovereignty* [[paper](https://doi.org/10.22459/caepr38.11.2016.07)]
- [2016] **Indigenising demographic categories: a prolegomenon to indigenous data sovereignty** *Indigenous Data Sovereignty* [[paper](https://doi.org/10.22459/caepr38.11.2016.06)]

##### 2013

- [2013] **Complex modeling and analysis of workplace collaboration data** *2013 International Conference on Collaboration Technologies and Systems (CTS)* [[paper](https://doi.org/10.1109/cts.2013.6567289)]

[⬆ Back to top](#paper-list)

#### Application

##### 2025

- [2025] **Demonstration Trials of AI/ML Edge+Cloud Suite (CRADA Final Report)** [[paper](https://doi.org/10.2172/3017673)]

##### 2017

- [2017] **Virtualization and Private Cloud with VMware Cloud Suite** [[paper](https://doi.org/10.1201/9781315225777)]
- [2017] **Introduction to Cloud Computing** *Virtualization and Private Cloud with VMware Cloud Suite* [[paper](https://doi.org/10.1201/9781315225777-2)]
- [2017] **Bibliography** *Virtualization and Private Cloud with VMware Cloud Suite* [[paper](https://doi.org/10.1201/9781315225777-16)]
- [2017] **vCloud Director** *Virtualization and Private Cloud with VMware Cloud Suite* [[paper](https://doi.org/10.1201/9781315225777-12)]
- [2017] **Front Matter** *Virtualization and Private Cloud with VMware Cloud Suite* [[paper](https://doi.org/10.1201/9781315225777-1)]

[⬆ Back to top](#paper-list)

### Collaboration & Productivity

#### Method

##### 2026

- [2026] **Mapping Quantum Supply Chains: Towards European technology sovereignty in an emerging industry** *TNO Repository* [[paper](https://resolver.tno.nl/uuid:3d252c89-f22b-4c24-8c54-724dc2222005)]
- [2026] **Procedimento integrado para a gestão do conhecimento e da inovação em uma empresa de eletrônicos** *Cooperativismo y Desarrollo: COODES* [[paper](https://coodes.upr.edu.cu/index.php/coodes/article/view/1025)]
- [2026] **The erosion of sociability: rescuing collaboration** *Przegląd Krytyczny* [[paper](https://doi.org/10.14746/pk.2026.8.1.1)]
- [2026] **NLZiet and NPO’s tiered VoD strategy: Balancing universal access and platform sovereignty** *Convergence The International Journal of Research into New Media Technologies* [[paper](https://doi.org/10.1177/13548565261459259)]
- [2026] **Building Evaluation Sovereignty - In Healthcare** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20488146)]
- [2026] **Forty+ Years of Post-Earthquake Reconnaissance: Methodological Evolution Across Three Phases of EEFIT Activity** [[paper](https://eartharxiv.org/repository/object/12999/download/23050/)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **Data Sherpa: An AI-Powered Assistant for Scientific Collaboration Knowledge Management** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22804318)]
- [2026] **Implementing a First Nation data-sovereign and agile modelling platform for pandemic management: lessons from Manitoba** *International Journal of Circumpolar Health* [[paper](https://doi.org/10.1080/22423982.2026.2749170)]
- [2026] **Il ruolo delle banche per la diffusione dell’Euro digitale, fra bene pubblico e innovazione** [[paper](https://doi.org/10.54103/milanoup.313.c804)]
- [2026] **From Institutional Silos to Shared Infrastructure: Building eln.nrw with eLabFTW** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23665594)]
- [2026] **Introduction** [[paper](https://doi.org/10.1093/9780197779033.003.0001)]
- [2026] **Steps towards a digital sovereignty** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23001705)]
- [2026] **S5 - Governance and Collaboration Structures Designing High-Capability Governance with Human Sovereignty, Rights, Transparency, Appeal, Polycentricity and Restart Capacity** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22777854)]
- [2026] **Communication Theories in Food Systems: A Conceptual Synthesis of Policy, Safety, Security, Sovereignty, and Digital Transformation** *International Journal of Sustainable Social Science (IJSSS)* [[paper](https://doi.org/10.59890/ijsss.v4i4.316)]
- [2026] **Generative Video and the Platformization of Animation Production** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-3373-8587-7.ch003)]
- [2026] **From Pilots to Services: Admission Mechanisms for Scalable Federated Health Data Collaboration - Design and Proof-of-Concept Study** *UCL Discovery (University College London)* [[paper](https://discovery.ucl.ac.uk/id/eprint/10231765/)]
- [2026] **The Cognitive Civilization S1 — Cognitive and Intelligence Structure A Civilization-Scale Architecture for Human Agency, AI Co-Reasoning, Verification, Cognitive Diversity, and Cognitive Sovereignty** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22771965)]
- [2026] **How do UAVs govern data sovereignty in decentralized federated sensing networks? Tokenized access control via policy-driven smart contracts** *Ad Hoc Networks* [[paper](https://doi.org/10.1016/j.adhoc.2026.104430)]
- [2026] ****A Multidisciplinary Investigation into the Promise, Challenges, and Policy Imperatives of Artificial Intelligence in India — Integrating the Perspectives of Industry Leaders Anand Mahindra and Nandan Nilekani with Contemporary Debates on Ethics, Inclusion, Sovereignty, and Sustainable Technological Development** ---** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22762375)]
- [2026] **Le macchine non pensano rilevano** *Figshare* [[paper](https://doi.org/10.6084/m9.figshare.33990754)]
- [2026] **Reconstructing Archaeology Education in Post-Conflict Sudan: Challenges, Resilience, and Institutional Renewal** *Public Archaeology* [[paper](https://doi.org/10.1080/14655187.2026.2687420)]
- [2026] **Interregional cooperation as a tool for reducing spatial differentiation: governance mechanisms and success factors** *DOAJ (DOAJ: Directory of Open Access Journals)* [[paper](https://doaj.org/article/d7603a7ab5e94b9789a74a453dfc222d)]
- [2026] **AI-Assisted Grammar Documentation for Senhaja Berber: Conversational Questionnaires Meet Hybrid Grammar Inference** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22819808)]
- [2026] **Correction: Technological innovation in healthcare: challenges, opportunities and impact on sustainability** *Frontiers in Digital Health* [[paper](https://doi.org/10.3389/fdgth.2026.1936077)]
- [2026] **Defending ecology and evolution in an age of democratic backsliding and environmental crisis** *Frontiers in Ecology and Evolution* [[paper](https://doi.org/10.3389/fevo.2026.1761637)]
- [2026] **From reactive trials to regional vaccine sovereignty: a pan-ebolavirus vaccine-readiness framework for East Africa’s Sudan virus and Bundibugyo virus threats** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1890576)]
- [2026] **Engineering the Intelligent Enterprise: The Complete Guide to Data and AI Platform Engineering** [[paper](https://doi.org/10.70593/978-81-69589-46-8)]
- [2026] **An Integrated Network for Commercial Spaceports: A Unified Vision for Global Space Access** *New Space* [[paper](https://doi.org/10.1177/21680256261476888)]
- [2026] **After the Cold War – the United States, Russia and Ukraine Trilateral Partnership from Non-Proliferation to Missile Conversion for Space Purposes** *Università degli Studi di Napoli Federico II* [[paper](https://doi.org/10.6093/unina/fedoa/17166)]
- [2026] **The AI Logbook - Ten Months into the Unknown** [[paper](https://doi.org/10.13140/rg.2.2.14451.90408)]
- [2026] **ECA-SDN - Federated data space for the Agri-food Cooperative Ecosystem** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22212812)]
- [2026] **Evolution of scholarly communication models from publisher-driven to scholar/funder-driven: a narrative review** *Science Editing* [[paper](https://doi.org/10.6087/kcse.407)]
- [2026] **ScholaForge** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21855396)]
- [2026] **Development of a Blockchain-Based Platform to Enable Indigenous Data Sovereignty and Shared Research Participation With Indigenous Communities: Technology Prototyping and Community Engagement Study** *Journal of Medical Internet Research* [[paper](https://doi.org/10.2196/90247)]
- [2026] **Open at the interface, closed at the core: neutrality claims in AI-enabled geoscience infrastructure focusing on Africa - The case of Deep-Time Digital Earth and GeoGPT** *JOURNAL OF GEOETHICS AND SOCIAL GEOSCIENCES* [[paper](https://doi.org/10.4401/jgsg-119)]
- [2026] **Ethical Governance of Virtual Learning and Student Privacy in Foreign Cloud-Hosted Learning Environments in Rwanda: A Systematic Review** *SJ Education Research Africa* [[paper](https://doi.org/10.51168/5ccazz42)]
- [2026] **Enhancing Community Resilience and Disaster Preparedness Through AI-Assisted Open Mapping** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-2600-2701-1.ch011)]
- [2026] **SPATIAL IMAGINATION OF CYBERSPACE SECURITY CHALLENGES FOR EUROPE AND TURKEY** *Güvenlik Çalışmaları Dergisi* [[paper](https://doi.org/10.54627/gcd.1756492)]
- [2026] **Redefining the geography of pharmaceutical innovation: Kelly Chibale as a harbinger for integrated drug discovery in Africa** *Frontiers in Drug Discovery* [[paper](https://doi.org/10.3389/fddsv.2026.1884834)]
- [2026] **The Model of Digital Education Development in the United States and Sino–American Cooperation in Digital Education** *Общество политика экономика право* [[paper](https://doi.org/10.24158/pep.2026.6.17)]
- [2026] **Trusted Data Space for the Agricultural Industry Chain: Theoretical Framework, Operating Mechanism, and Implementation Path** *DOAJ (DOAJ: Directory of Open Access Journals)* [[paper](https://doaj.org/article/9e83122252dd4291afa3441acc88ef52)]
- [2026] **From Local Data to European Intelligence Federated Governance and Semantic Interoperability in Mobility Data Spaces** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21298142)]
- [2026] **Conference Summary at the Jakarta Geopolitical Forum X/2026: Strengthening Multilateralism: Survival Amid Global Turbulence and a Fragmented World** *Proceeding Jakarta Geopolitical Forum* [[paper](https://doi.org/10.55960/jgf.v10i1.321)]
- [2026] **A Unified Interoperable Payment Infrastructure A Systems-Engineering Framework for Scalable National and Cross-Border Integration** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21284028)]
- [2026] **False dilemmas and real challenges: GenAI and the algorithmization of experience** *Frontiers in Communication* [[paper](https://doi.org/10.3389/fcomm.2026.1932398)]
- [2026] **Cognitive Sovereignty Architecture: A Dual-Timeline Personal Identity Layer Agent Framework** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20821869)]
- [2026] **Cybercrime Regulation and Digital Sovereignty in OIC Countries: Emerging Legal Trends and Future Directions** *International Journal of Law and Social Sciences* [[paper](https://doi.org/10.65960/ijlss.2.2.2026.16)]
- [2026] **Cloud computing-based collaborations on health research: A systematic review of applications, barriers to adoption, and migration strategies** *Digital Medicine* [[paper](https://doi.org/10.1097/dm-2026-00006)]
- [2026] **Blockchain Digital Transformation: Enhancing Port Efficiency and Competitiveness in Egyptian Maritime Logistics** *AIN Journal* [[paper](https://doi.org/10.59660/52721)]
- [2026] **Municipal adoption of complementary currencies in Europe** *HAL* [[paper](https://hal.science/emse-05661319v1)]
- [2026] **Building an Inclusive Circular Economy in Bangladesh’s Extended Global Apparel Value Chain: Policy Challenges and Actions** *VBN Forskningsportal (Aalborg Universitet)* [[paper](https://vbn.aau.dk/da/publications/8d7fa4ad-9325-4a97-aaf9-709845e440c0)]
- [2026] **Invisible victims of border conflict: health and wellbeing of border communities between Cambodia and Thailand** *International Journal of Public Health* [[paper](https://doi.org/10.3389/ijph.2026.1609740)]
- [2026] **Kimberley Aboriginal Health Research Alliance (KAHRA) – Improving Indigenous Health Research engagement and collaboration in the Kimberley as a regional response.** *ResearchOnline@ND (The University of Notre Dame)* [[paper](https://researchonline.nd.edu.au/nulungu_researchweek/2026/schedule/7)]
- [2026] **A sustainable platform for federated health data access, AI innovation, and regulatory acceptance in alignment with the European Health Data Space principles** *Open Research Europe* [[paper](https://doi.org/10.12688/openreseurope.23459.1)]
- [2026] **Advancing Canada's Diamond Open Access Infrastructure** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20415791)]
- [2026] **Book review: Tourism, Global Crises and Justice: Tourism Transition to a More Just and Sustainable Future** *Journal of Tourism Futures* [[paper](https://doi.org/10.1108/jtf-06-2026-351)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **ECCSEL ERIC Value Proposition** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23257068)]
- [2026] **DIGITAL DOMINANCE: TECHNOLOGY, AI, CYBERSECURITY AND GEO-POLITICS IN THE NEW WORLD ORDER** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21497884)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **Layered narrative sovereignty: communicative authority and hybrid infrastructures in Mexican Indigenous and community media** *Frontiers in Communication* [[paper](https://doi.org/10.3389/fcomm.2026.1995028)]
- [2026] **Choosing Together: How Dyadic Negotiation Shapes Adaptive Kitchen Design Preferences for Older Adults with Cognitive Impairment and Their Care Partners** [[paper](https://arxiv.org/abs/2609.13700)]
- [2026] **Digital Sovereignty and Strategic Autonomy in the Age of AI** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-2600-0898-0.ch005)]
- [2026] **Building a Grey Literature Clearinghouse on Families in Canada: Early Insights into Relationship-Building and Metadata Crosswalks** *GreyNet International* [[paper](https://doi.org/10.26069/greynet-2026-000.946-gn)]
- [2026] **RACER: Reinforced Agent Collaboration for Explainable Reasoning on Knowledge Graphs** [[paper](https://arxiv.org/abs/2608.29263)]
- [2026] **CausalSteward: An Agentic Divide-Conquer-Combine Copilot for Causal Discovery** [[paper](https://arxiv.org/abs/2607.01936)]
- [2026] **Drivers of Vaccine Uptake for Aboriginal and Torres Strait Islander Children to Inform Tailored Strategies: A Qualitative Study Exploring Health Service Provider Perspective** *The Medical Journal of Australia* [[paper](https://doi.org/10.5694/mja2.70233)]
- [2026] **PAPEL: A Collaborative System for Parental Guidance during Preschool Play-Based English Learning** [[paper](https://arxiv.org/abs/2606.11896)]
- [2026] **Safeguarding Digital Classrooms: Cybersecurity Implications of AI-Driven Tools in Cambodian Education** *Journal of Education Innovation and Language Teaching (JEILT)* [[paper](https://doi.org/10.63381/jeilt.v2i1.86)]
- [2026] **Building a trusted hub for grey literature on families in Canada** *GreyNet International* [[paper](https://doi.org/10.26069/greynet-2026-000.931-gn)]
- [2026] **Among Us: Measuring and Mitigating Malicious Contributions in Model Collaboration Systems** [[paper](https://arxiv.org/abs/2602.05176)]
- [2026] **Beyond Pixels: Visual Metaphor Transfer via Schema-Driven Agentic Reasoning** [[paper](https://arxiv.org/abs/2602.01335)] [[project](https://yuci-gpt.github.io/Beyond-Pixels/)]
- [2026] **MoCo: A One-Stop Shop for Model Collaboration Research** [[paper](https://arxiv.org/abs/2601.21257)]

##### 2025

- [2025] **DepthScape: Authoring 2.5D Designs via Depth Estimation, Semantic Understanding, and Geometry Extraction** [[paper](https://arxiv.org/abs/2512.02263)]
- [2025] **A2VISR: An Active and Adaptive Ground-Aerial Localization System Using Visual Inertial and Single-Range Fusion** [[paper](https://arxiv.org/abs/2512.16367)]

[⬆ Back to top](#paper-list)

### Identity & Access

#### Method

##### 2026

- [2026] **Behavioral Governance for Autonomous AI Agents: The AgentBound Framework** [[paper](https://arxiv.org/abs/2606.30970)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **Editorial: Rethinking the role of social media in learning** *Frontiers in Education* [[paper](https://doi.org/10.3389/feduc.2026.2015852)]
- [2026] **From space to signal: How identity-driven workplaces are reshaping corporate real estate strategy** *Corporate real estate journal* [[paper](https://doi.org/10.69554/fjtk3261)]
- [2026] **Diversity management in European companies: intersectionality and individual experiences of bias at work** *Edward Elgar Publishing eBooks* [[paper](https://doi.org/10.4337/9781035361243.00012)]
- [2026] **‘I am in no position to express myself.’ An ethnographic case study of multilingualism at a Finnish food corporation** *Warwick Research Archive Portal (University of Warwick)* [[paper](https://wrap.warwick.ac.uk/151330/1/WRAP_Theses_Humonen_2019.pdf)]
- [2026] **Equity as strategy: Addressing burnout and building resilient healthcare organisations** *Management in healthcare.* [[paper](https://doi.org/10.69554/vwqs8152)]
- [2026] **The skills reset: redesigning learning before AI redesigns roles** *Strategic HR Review* [[paper](https://doi.org/10.1108/shr-06-2026-0069)]
- [2026] **Nurse Leader Well-Being Through Resilience by Strengthening Social Support on Organizational-Level Interventions** *Workplace Health & Safety* [[paper](https://doi.org/10.1177/21650799261491877)]
- [2026] **Human inclusion Credit** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22823182)]
- [2026] **The Dynamics of Flexible Working and Work-Family Balance: Implications on the Wellbeing of Global Majority Women in the U.K. Health Sector.** *BCU Open Access Repository (Birmingham City University)* [[paper](https://www.open-access.bcu.ac.uk/17253/1/Mutiat%20Ayodele%20Owolewa%20PhD%20Thesis_Final%20Version_Final%20Award%20September%202026.pdf)]
- [2026] **Operational and organizational training for managing work stress among police investigation officers: a global perspective** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2026.1919749)]
- [2026] **Organizational Socialization of Employees Representing Sexual Minorities in Pakistan** *Pakistan Journal of Positive Psychology* [[paper](https://doi.org/10.67785/pjpp.1.177)]
- [2026] **Editorial: Pathways to mental health resilience in emergency personnel: protective strategies and occupational challenges** *Frontiers in Psychiatry* [[paper](https://doi.org/10.3389/fpsyt.2026.1967089)]
- [2026] **The Role of Artificial Intelligence in Building Resilient and Sustainable Supply Chains: A Multiple-Case Study with an Extension to Pakistan Textile and Manufacturing Sector** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i8.147)]
- [2026] **Navigating neurodiversity: managerial narratives on inclusive leadership in technology-driven workplaces** *Journal of Organizational Effectiveness People and Performance* [[paper](https://doi.org/10.1108/joepp-08-2025-0688)]
- [2026] **Governing Enterprise AI: A Three-Layer Defense-in-Depth Model** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21347812)]
- [2026] **Deep Learning-Based Face Authentication For Secure Attendance Applications** *International journal of engineering science and advanced technology.* [[paper](https://doi.org/10.64771/ijesat.2026.v26.i7.3681)]
- [2026] **Occupational Physicians Should Not Rely Solely on Artificial Intelligence in Fitness-for-Work Decisions** *Voices in Bioethics* [[paper](https://doi.org/10.52214/vib.v12i.14828)]
- [2026] **Guest editorial: EDI in resilient labour markets: socioeconomic and policy perspectives** *Equality Diversity and Inclusion An International Journal* [[paper](https://doi.org/10.1108/edi-08-2026-880)]
- [2026] **The Master Narrative of Prioritized Parenthood: Bifurcated Identities and Doxastic Damage in the Postpandemic Workplace** *Gender Work and Organization* [[paper](https://doi.org/10.1111/gwao.70166)]
- [2026] **HYDRO ACCESS: SMART WATER DISPENSER WITH QR AUTHENTICATION** [[paper](https://iejse.com/journals/index.php/iejse/article/view/309)]
- [2026] **Transformasi Komunikasi Organisasi pada Era Work From Home dan Hybrid Work: Implikasi terhadap Budaya dan Konflik Organisasi** *PRODUKTIF Jurnal Kepegawaian dan Organisasi* [[paper](https://doi.org/10.37481/jko.v5i1.266)]
- [2026] **Towards a contemporary approach to continuing professional development in policing** *Edinburgh Napier Research Repository (Edinburgh Napier University)* [[paper](https://napier-repository.worktribe.com/output/5113515)]
- [2026] **Guest editorial: Organizational ethnography and practice theories in the digital transformation of work** *Journal of Organizational Ethnography* [[paper](https://doi.org/10.1108/joe-07-2026-159)]
- [2026] **Guest editorial: Managing the ‘digitalized’ public sector: building communities and creating knowledge around an evolving DNA** *International Journal of Public Sector Management* [[paper](https://doi.org/10.1108/ijpsm-07-2026-593)]
- [2026] **Guest editorial: Metaverse and organizations: perspectives from emerging economies** *International journal of organizational analysis* [[paper](https://doi.org/10.1108/ijoa-08-2026-029)]
- [2026] **P447 Empowering the endoscopy workforce: evaluating the endoscopy practice programme for healthcare assistants** *E-Posters* [[paper](https://doi.org/10.1136/gutjnl-2026-bsg.551)]
- [2026] **From Gender as Attribute to Gender as Generative Resonance: Toward a UPCT-Based Theory of Participation** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20989951)]
- [2026] **Cultural Diversity and Social Inclusion: Challenges and Opportunities** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21623435)]
- [2026] **Guest editorial: STARA (smart technology, AI, robotics and algorithms): implications for career research** *Career Development International* [[paper](https://doi.org/10.1108/cdi-06-2026-665)]
- [2026] **Editorial: World mental health day: mental health in the workplace** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1844073)]
- [2026] **Työpaikkaviestinnän neuvotteluja: Nuorten korkeasti koulutettujen maahanmuuttajien kokemuksia kohteliaisuudesta, osallisuudesta ja kuulumisen tunteesta Suomessa** *Työväentutkimus Vuosikirja* [[paper](https://hdl.handle.net/10138/634084)]
- [2026] **Editorial: The new organizational landscape: technology, leadership, and the human experience at work** *Organization Management Journal* [[paper](https://doi.org/10.1108/omj-05-2026-982)]
- [2026] **Guest editorial: AI for a better future – advances, challenges and future research directions** *Internet Research* [[paper](https://doi.org/10.1108/intr-06-2026-034)]
- [2026] **Invisible Barriers and Gendered Resistance in Nursing Leadership: A Phenomenological Study** *Advances in Nursing Science* [[paper](https://doi.org/10.1097/ans.0000000000000660)]
- [2026] **From NASA to Novels: What Can Adler Teach Physicians?** *Plastic & Reconstructive Surgery* [[paper](https://doi.org/10.1097/prs.0000000000012554)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **Understanding Workplace Needs and Constraints of Professionals with Chronic Illness** *International ACM SIGACCESS Conference on Computers and Accessibility (ASSETS)* [[paper](https://doi.org/10.1145/3797867.3841209)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **Autistic Adults’ Experiences of Navigating Disclosure, Camouflaging, and Workplace Inclusion in Indonesia** *Neurodiversity* [[paper](https://doi.org/10.1177/27546330261490696)]
- [2026] **64 A paradox of supply and demand: unemployed doctors amid NHS waiting lists** [[paper](https://doi.org/10.1136/bmjoq-2026-qsho.64)]
- [2026] **When Access Extracts: Household Experiences with Predatory Financial Services, Workplace Benefits, and Identity-Based Discrimination** *Journal of Poverty* [[paper](https://doi.org/10.1080/10875549.2026.2671663)]

[⬆ Back to top](#paper-list)

### Interoperability & Standards

#### Theory

##### 2026

- [2026] **Strategies for Developing Civil Servant Competencies through a Collaborative Ecosystem** *Jurnal Administrasi dan Kebijakan Publik* [[paper](https://doi.org/10.25077/jakp.11.2.224-242.2026)]
- [2026] **Case Study Analysis of Intelligent Lighting Systems in Contemporary Interior Spaces: A Review of Adaptive Technologies, Human-Centric Design, and Sustainable Applications** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23554708)]
- [2026] **Reimagining Museum Storage: A Robotic Proof of Concept for Automated Handling and Digitisation** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23527252)]
- [2026] **D2.1 Healthcare Technology Competences and Barrier Analysis in Tunisia Report** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23646818)]
- [2026] **Mentorship as a Catalyst for AI-Ready Health Information Management in Nigeria: Building an Ethical and Future-Ready Digital Health Workforce** *The Eurasia Proceedings of Health Environment and Life Sciences* [[paper](https://doi.org/10.55549/ephels.172)]
- [2026] **Integrated Lifelong Learning Ecosystems for Upskilling and Reskilling in Formal, Non-Formal, and Informal Education** [[paper](https://doi.org/10.68050/jams.2026.460)]
- [2026] **Mining Industry 5.0: A 6S Framework for Sustainable and Human-Centric Mining Systems** *Mining* [[paper](https://doi.org/10.3390/mining6030075)]
- [2026] **Seeing Care Whole: A Professional Autoethnography on Envisioning Integrated Care for Persons Living with Inherited Retinal Diseases** *International Journal of Integrated Care* [[paper](https://doi.org/10.5334/ijic.icic26521)]
- [2026] **Advancing human-centric sustainable construction: barriers and adoption of neuro-safety wearable technologies** *Smart and Sustainable Built Environment* [[paper](https://doi.org/10.1108/sasbe-02-2026-0153)]
- [2026] **From Burnout to Balance: Cultivating Joy with Blockchain in High-performance Environments** *Emerald Group Publishing Limited eBooks* [[paper](https://doi.org/10.1108/978-1-80686-125-520261004)]
- [2026] **AI-Mediated Continuous Assessment Infrastructure (AIM-CAI): Connecting Learning Evidence Across Contexts and Time** *Information* [[paper](https://doi.org/10.3390/info17080806)]
- [2026] **Training as a Strategic Lever for Blockchain Process Integration in Moroccan Organizations: An Educational Science Perspective** *African Scientific Journal* [[paper](https://africanscientificjournal.com/index.php/AfricanScientificJournal/article/view/2068)]
- [2026] **Artificial Intelligence and Workforce Analytics Transforming Strategic Human Resource Management Through Data-Driven Decision-Making** *Journal of Intelligent Decision Making and Information Science* [[paper](https://doi.org/10.59543/jidmis.v3.2133)]
- [2026] **The adoption of AI technologies and data to support workplace learning in the corporate sector: A scoping review** *Review of Education* [[paper](https://doi.org/10.1002/rev3.70198)]
- [2026] **The Qualification Portability in Vocational Education: Evidence from Uzbekistan's International Mobility Reforms** *Academia Open* [[paper](https://doi.org/10.21070/acopen.11.2026.14884)]
- [2026] **Toward a Tri-Axial Perspective on Smart Space-Based Immersive Metaverse Systems: Technological Layers, Spatial Linkage, and Application Domains** *Metaverse* [[paper](https://doi.org/10.54517/m260021)]
- [2026] **Quantum–Neuromorphic Intelligence for Gerontechnology, Mechatronics and Human–Machine Adaptation** [[paper](https://doi.org/10.62311/nesx/rb10jy-978-81-688729-0-5)]
- [2026] **Artificial Intelligence-Enabled Predictive Decision Support Systems for Smart Enterprise and Industrial Applications** *Journal of Intelligent Decision Making and Information Science* [[paper](https://doi.org/10.59543/jidmis.v3.1164)]
- [2026] **Artificial Intelligence Integration in Competency-Based Short-Term Vocational Education in Thailand: Policy, Practice, and Future Directions** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21714882)]
- [2026] **The Trust Infrastructure Paradigm: Solving Cross-Border Credential Friction and Compliance Risks in Global Workforce Mobility** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21424933)]
- [2026] **Editorial** *SAMVAD* [[paper](https://doi.org/10.53739/samvad/2026/v32/174660)]
- [2026] **BIM-Driven Safety Management for Enhancing Hazard Prediction: A Systematic Review** *EPiC series in built environment* [[paper](https://doi.org/10.29007/mn17)]
- [2026] **Closing the implementation gap: the Joint Action on Cardiovascular Diseases and Diabetes (JACARDI) as a proof of-concept for Europe’s Safe Hearts Plan** *International Journal of Public Health* [[paper](https://doi.org/10.3389/ijph.2026.1609906)]
- [2026] **Simulation-based decision support in real estate and facility management : a multi-level integrative framework for workplace, hospitality, real estate, and smart building management** *Zürcher Hochschule für Angewandte Wissenschaften digital collection (Zurich University of Applied Sciences)* [[paper](https://hdl.handle.net/11475/36609)]
- [2026] **Enhancing Trust in Digital Credentials: Granular Skills Recognition with SkillsAware** *PLA Inside Out: An International Journal on Theory, Research and Practice in Prior Learning Assessment* [[paper](https://www.plaio.org/index.php/index/article/view/381)]
- [2026] **Building Trust in Skills: Designing a UK-Wide Digital Credentialing Infrastructure for Inclusive Recognition and Economic Growth** *PLA Inside Out: An International Journal on Theory, Research and Practice in Prior Learning Assessment* [[paper](https://www.plaio.org/index.php/index/article/view/440)]
- [2026] **Consumers’ Information Systems: Managing Consumption within Households and in Interaction with Digital Firms** *Recherche und Kataloge (Universitätsbibliothek Siegen)* [[paper](https://doi.org/10.25819/ubsi/11129)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **Towards End-to-End Privacy-Preserving AI for Real-Time ECG Monitoring** [[paper](https://arxiv.org/abs/2610.25094)]
- [2026] **Polarized Scheme: duality of computation, delimited control, and continuation-passing macro Interleaving** [[paper](https://arxiv.org/abs/2610.26266)]
- [2026] **Consumer empowerment: need, definition, quantification, outcomes and challenges** [[paper](https://arxiv.org/abs/2610.04877)]
- [2026] **Synthetic populations for epidemic, demographic and mobility modeling** [[paper](https://arxiv.org/abs/2610.21784)]
- [2026] **SIESTA-QCOMP: Bridging Classical and Quantum Computing for Strongly Correlated Systems** [[paper](https://arxiv.org/abs/2610.24616)]
- [2026] **OctoSense: Building a Unified Ecosystem for Open-Source Wireless Sensing** [[paper](https://arxiv.org/abs/2610.12405)]
- [2026] **From Digital Competence to Demonstrated Digital Capability: Positioning the International Digital Driving License Against DigComp and UNESCO Frameworks** [[paper](https://arxiv.org/abs/2609.19406)]
- [2026] **Involving before Evolving: A Vision for Trustworthy Enterprise Digital Twin Engineering** [[paper](https://arxiv.org/abs/2609.13071)]
- [2026] **Agentic AI-enabled Semantic Commissioning of a Cognitive Digital Twin for Reconfigurable Manufacturing** [[paper](https://arxiv.org/abs/2609.09503)]
- [2026] **Agentic Settlement Protocol: An Application Profile for Refundable, Delayed-Fulfilment Agent Commerce on Stablecoin Rails** [[paper](https://arxiv.org/abs/2609.02208)]
- [2026] **Advancing the Physical Internet with GraphRAG: A New Way to Review and Integrate Existing Research** [[paper](https://arxiv.org/abs/2609.29083)]
- [2026] **A Community-Developed Domain Ontology for Magnetic Materials** [[paper](https://arxiv.org/abs/2609.11464)]
- [2026] **Cross-Organizational SysML Model Integration: A Survey of Challenges and AI-Supported Tasks** [[paper](https://arxiv.org/abs/2609.37000)]
- [2026] **From Semantic to Token Communication: The Next Paradigm for Large-Model-Driven 6G Intelligent Connectivity** [[paper](https://arxiv.org/abs/2609.10714)]
- [2026] **Quality Metrics for LLM-Generated Asset Administration Shells: A Perturbation-Based Evaluation Approach** [[paper](https://arxiv.org/abs/2609.07290)]
- [2026] **Making Cross-Continental Federated Learning Repeatable with FLIP: a Multi-Application Study** [[paper](https://arxiv.org/abs/2609.36001)]
- [2026] **An Agent Model Abstraction for Human-AI Teaming Cognitive Coupling** [[paper](https://arxiv.org/abs/2609.05552)]
- [2026] **From Language Models to World-Acting Systems: Progress and Limits of Agentic AI across Digital, Social, Virtual, and Physical Environments** [[paper](https://arxiv.org/abs/2609.04894)]
- [2026] **LOCO 2026 Lightning Talk Abstracts: 2nd International Workshop on Low Carbon Computing** [[paper](https://arxiv.org/abs/2609.13355)]
- [2026] **Teaching Micro-credentials through Learning Management Systems: A Systematic Review of Pedagogical Designs, Assessment Practices, and Learner Outcomes** *Research Square* [[paper](https://doi.org/10.21203/rs.3.rs-10758652/v1)]
- [2026] **A Blueprint for Collaborative Cybersecurity Operations Centres with Capacity for Shared Situational Awareness, Coordinated Response, and Joint Preparedness** [[paper](https://arxiv.org/abs/2608.08011)]
- [2026] **Removing Infrastructure Barriers in Human-Robot Collaboration Through Wireless Reconfigurable Cells** [[paper](https://arxiv.org/abs/2608.09658)]
- [2026] **Use of the Common Information Model (IEC 61970) for Standardized Data Exchange in HVDC Digital Twin Systems** [[paper](https://arxiv.org/abs/2608.09259)]
- [2026] **A Multi-Viewpoint Modeling Framework for Digital Twin Integration and Reuse with LLM-Assisted Compatibility Analysis** [[paper](https://arxiv.org/abs/2608.23115)]
- [2026] **BZKO: An Ontology for the Card Index of German Post-War Compensation Records** [[paper](https://arxiv.org/abs/2608.06918)] [[code](https://github.com/ISE-FIZKarlsruhe/bzko)]
- [2026] **Designing, Deployment and Field Testing of C2Stack for Networked Intelligent Software-Defined UAVs** [[paper](https://arxiv.org/abs/2608.28854)]
- [2026] **UrbanAgent: A Tool-Augmented Agent for Cross-System Urban Tasks** [[paper](https://arxiv.org/abs/2608.03018)]
- [2026] **Trans-Domain Digital Twin: Conceptual Foundations, Architecture, and Research Outlook** [[paper](https://arxiv.org/abs/2607.15908)]
- [2026] **Model-Driven Digital Twin Framework for Quantum Networks** [[paper](https://arxiv.org/abs/2607.10367)]
- [2026] **A Verifier-Centric Conceptual Model for Digital Credential Ecosystems** [[paper](https://arxiv.org/abs/2607.10747)]
- [2026] **Umulsai: A Plain-Text Format and In-Browser Engraving System for Jeongganbo, Korean Mensural Notation** [[paper](https://arxiv.org/abs/2607.24230)]
- [2026] **Human-Robot Interaction in GenAI Architectures via the Agent-Client Protocol** [[paper](https://arxiv.org/abs/2607.14919)]
- [2026] **Advanced Information Security and Assurance: A Literature Review of Zero Trust Architecture, Artificial Intelligence, and Cybersecurity Resilience** *International Journal of Latest Technology in Engineering Management & Applied Science* [[paper](https://doi.org/10.51583/ijltemas.2026.150600161)]
- [2026] **Collaborative Human-Agent Protocol (CHAP)** [[paper](https://arxiv.org/abs/2606.09751)] [[code](https://github.com/BrightbeamAI/chap)]
- [2026] **A Deployment Case Study in Robotic Apparel Automation: Digital Twin Integration, Interoperability, and Workforce Enablement** [[paper](https://arxiv.org/abs/2606.16078)]
- [2026] **Integrating Heterogeneous Digital Twins in Federated Ecosystems** [[paper](https://arxiv.org/abs/2606.22791)]
- [2026] **Toward Model-Driven Digital Twin Configuration: Separating Structure Semantics and Runtime with SysML SAREF and Ditto** [[paper](https://arxiv.org/abs/2609.04213)]
- [2026] **Integrated cloud-based architecture for robot-robot and human-robot collaboration using ROS 2--MQTT in Mediterranean Greenhouses** [[paper](https://arxiv.org/abs/2606.22682)]
- [2026] **Analyzing and Encoding the Al-Mawrid Arabic-English Dictionary with the ISO Language Markup Framework and TEI Lex-0** [[paper](https://arxiv.org/abs/2606.18205)]
- [2026] **DACP: A Scientific Data Access and Collaboration Protocol** [[paper](https://arxiv.org/abs/2605.03411)]
- [2026] **The Evolution of Digital Twins from Reactive to Agentic Systems** [[paper](https://arxiv.org/abs/2605.26066)]
- [2026] **EDA-Schema-V2: A Multimodal Schema, Open Datasets, and Benchmarks for Machine Learning in Digital Physical Design** [[paper](https://arxiv.org/abs/2605.06952)]
- [2026] **PPAI: Enabling Personalized LLM Agent Interoperability for Collaborative Edge Intelligence** [[paper](https://arxiv.org/abs/2605.18067)]
- [2026] **Housing Potential Common Data Model and City Digital Twin** [[paper](https://arxiv.org/abs/2605.05535)]
- [2026] **Disarranged Harmonization of Transparency Reporting by Social Media Platforms Under the Digital Services Act** [[paper](https://arxiv.org/abs/2605.17655)]
- [2026] **Case Studies and Reflections on Agentic Software Engineering for Rapid Development of Digital Music Instruments** [[paper](https://arxiv.org/abs/2605.14016)]
- [2026] **Beyond Metadata: The Role of DOI, ORCID, and ROR in Shaping Transparent and Interoperable Library Systems** [[paper](https://arxiv.org/abs/2606.00591)]
- [2026] **Global AI Regulations for FAIR and Ethics in High-Risk Use Cases: A Comparative Review** [[paper](https://arxiv.org/abs/2608.14562)]
- [2026] **SS-ZKR: Spatial-Semantic Zero-Knowledge Routing for Privacy-Preserving Multi-Agent Collaboration** [[paper](https://arxiv.org/abs/2606.00962)]
- [2026] **Delivering Science as a Service: Sci-Orchestra's Cloud-Native Approach to HPC** [[paper](https://arxiv.org/abs/2605.08396)]
- [2026] **Searching for European Alternatives: Digital Sovereignty, Digital Patriotism, and the Emerging Geopolitics of Software Adoption** [[paper](https://arxiv.org/abs/2604.15767)]
- [2026] **AONA: A Comprehensive Architecture and Workflow Design for Global Agentic Collaboration** [[paper](https://arxiv.org/abs/2606.20573)]
- [2026] **From Brain Models to Executable Digital Twins: Execution Semantics and Neuro-Neuromorphic Systems** [[paper](https://arxiv.org/abs/2604.13574)]
- [2026] **A Proposed Biomedical Data Policy Framework to Reduce Fragmentation, Improve Quality, and Incentivize Sharing in Indian Healthcare in the era of Artificial Intelligence and Digital Health** [[paper](https://arxiv.org/abs/2604.11125)]
- [2026] **MPAC: A Multi-Principal Agent Coordination Protocol for Interoperable Multi-Agent Collaboration** [[paper](https://arxiv.org/abs/2604.09744)]
- [2026] **Doctoral Theses in France (1985-2025): A Linked Dataset of PhDs, Academic Networks, and Institutions** [[paper](https://arxiv.org/abs/2604.08619)]
- [2026] **The Missing Pillar in Quantum-Safe 6G: Regulation and Global Compliance** [[paper](https://arxiv.org/abs/2604.13314)]
- [2026] **QLLVM: A Scalable Quantum-Classical Co-Compilation Framework based on LLVM** [[paper](https://arxiv.org/abs/2604.15094)]
- [2026] **Binary Star Evolution Modules in REBOUNDx** [[paper](https://arxiv.org/abs/2604.06386)] [[code](https://github.com/malidib/ReboundS)]
- [2026] **Fostering Knowledge Infrastructures in Science Communication and Aerospace Engineering** [[paper](https://arxiv.org/abs/2603.05984)]
- [2026] **From Digital Twins to World Models:Opportunities, Challenges, and Applications for Mobile Edge General Intelligence** [[paper](https://arxiv.org/abs/2603.17420)]
- [2026] **Cenergy3: An Open Software Package for City Energy 3D Modeling** [[paper](https://arxiv.org/abs/2603.20361)]
- [2026] **Public Sector Open Source Program Offices -- Archetypes for how to Grow (Common) Institutional Capabilities** [[paper](https://arxiv.org/abs/2603.04891)]
- [2026] **Information and communications technologies for carbon sinks from economics and engineering perspectives** [[paper](https://arxiv.org/abs/2603.01787)]
- [2026] **A learning health system in Neurorehabilitation as a foundation for multimodal patient representation** [[paper](https://arxiv.org/abs/2604.22763)]
- [2026] **Governing frontier general-purpose AI in the public sector: adaptive risk management and policy capacity under uncertainty through 2030** [[paper](https://arxiv.org/abs/2604.06215)]
- [2026] **Methods for Knowledge Graph Construction from Text Collections: Development and Applications** [[paper](https://arxiv.org/abs/2603.25862)]
- [2026] **The Vertical Challenge of Low-Altitude Economy: Why We Need a Unified Height System?** [[paper](https://arxiv.org/abs/2603.04866)]
- [2026] **STEM Agent: A Self-Adapting, Tool-Enabled, Extensible Architecture for Multi-Protocol AI Agent Systems** [[paper](https://arxiv.org/abs/2603.22359)]
- [2026] **AWCP: A Workspace Delegation Protocol for Deep-Engagement Collaboration across Remote Agents** [[paper](https://arxiv.org/abs/2602.20493)] [[code](https://github.com/SII-Holos/awcp)]
- [2026] **Towards complete digital twins in cultural heritage with ART3mis 3D artifacts annotator** [[paper](https://arxiv.org/abs/2602.12761)]
- [2026] **Digital Twins &amp; ZeroConf AI: Structuring Automated Intelligent Pipelines for Industrial Applications** [[paper](https://arxiv.org/abs/2602.04385)]
- [2026] **VQ-DSC-R: Robust Vector Quantized-Enabled Digital Semantic Communication With OFDM Transmission** [[paper](https://arxiv.org/abs/2602.15045)]
- [2026] **CA20108 COST Action: A Methodology for Developing FAIR Micrometeorological Networks** [[paper](https://arxiv.org/abs/2602.23921)]
- [2026] **Beyond Context Sharing: A Unified Agent Communication Protocol (ACP) for Secure, Federated, and Autonomous Agent-to-Agent (A2A) Orchestration** [[paper](https://arxiv.org/abs/2602.15055)]
- [2026] **A Secure and Interoperable Architecture for Electronic Health Record Access Control and Sharing** [[paper](https://arxiv.org/abs/2602.20830)]
- [2026] **Archives, archival bond, and digital representation: A case study with the International Image Interoperability Framework** [[paper](https://arxiv.org/abs/2601.14823)]
- [2026] **Digital Twin Synchronization: towards a data-centric architecture** [[paper](https://arxiv.org/abs/2601.23051)]
- [2026] **Design and Evaluation of Next-Generation Cellular Networks through Digital and Physical Open and Programmable Platforms** [[paper](https://arxiv.org/abs/2601.19027)]
- [2026] **Interoperable Architecture for Digital Identity Delegation for AI Agents with Blockchain Integration** [[paper](https://arxiv.org/abs/2601.14982)]
- [2026] **Communications-Incentivized Collaborative Reasoning in NetGPT through Agentic Reinforcement Learning** [[paper](https://arxiv.org/abs/2602.00766)]
- [2026] **Schema-Grounded LLM Extraction for FHIR Patient Digital Twins** [[paper](https://arxiv.org/abs/2601.05847)]
- [2026] **Development of an end-to-end hardware and software pipeline for affordable and feasible ergonomics assessment in the automotive industry** [[paper](https://arxiv.org/abs/2601.17574)]
- [2026] **Communication Technologies for Intelligent Transportation Systems: From Railways to UAVs and Beyond** [[paper](https://arxiv.org/abs/2601.14106)]
- [2026] **An Empirical Evaluation of Modern MLOps Frameworks** [[paper](https://arxiv.org/abs/2601.20415)]
- [2026] **Self-Sovereign Identity and eIDAS 2.0: An Analysis of Control, Privacy, and Legal Implications** [[paper](https://arxiv.org/abs/2601.19837)]
- [2026] **Exploring Blockchain Interoperability: Frameworks, Use Cases, and Future Challenges** [[paper](https://arxiv.org/abs/2601.02949)]

##### 2025

- [2025] **A Container-based Approach For Proactive Asset Administration Shell Digital Twins** [[paper](https://arxiv.org/abs/2512.15452)]
- [2025] **A Framework for Scalable Digital Twin Deployment in Smart Campus Building Facility Management** [[paper](https://arxiv.org/abs/2512.12149)]
- [2025] **Towards 6G Native-AI Edge Networks: A Semantic-Aware and Agentic Intelligence Paradigm** [[paper](https://arxiv.org/abs/2512.04405)]
- [2025] **Semantic Grounding of Digital Twin Metamodels Using RDF Graphs** [[paper](https://arxiv.org/abs/2512.15281)]
- [2025] **Forking Anatomy: How MorphoDepot Applies the Open-Source Development Model to 3D Digital Morphology** [[paper](https://arxiv.org/abs/2601.00030)]
- [2025] **Digital health transformation in Quebec: assessment of interoperability and governance strategies** [[paper](https://arxiv.org/abs/2601.06051)]
- [2025] **interID -- An Ecosystem-agnostic Verifier Application for Self-sovereign Identity** [[paper](https://arxiv.org/abs/2512.23383)]
- [2025] **Towards a point-to-point CV-QKD system: Implementation challenges and perspectives** [[paper](https://arxiv.org/abs/2512.19834)]
- [2025] **Cenergy3: An API for City Energy 3D Modeling** [[paper](https://arxiv.org/abs/2512.06459)]
- [2025] **SciCom Wiki: A Digital Library to Support the Science Communication Knowledge Infrastructure for Videos and Podcasts** [[paper](https://arxiv.org/abs/2511.09248)]
- [2025] **A Brief History of Digital Twin Technology** [[paper](https://arxiv.org/abs/2511.20695)]
- [2025] **Design and Performance Assessment of a Virtualized IED for Digital Substations** [[paper](https://arxiv.org/abs/2511.21310)]
- [2025] **The Future of Food: How Artificial Intelligence is Transforming Food Manufacturing** [[paper](https://arxiv.org/abs/2511.15728)]
- [2025] **The SolarEV City Paradox: A Critical Review of the Fragmented Integration of Rooftop Photovoltaics and Electric Vehicles for Urban Decarbonization** [[paper](https://arxiv.org/abs/2511.15091)]
- [2025] **On Addressing Isolation in Blockchain-Based Self-Sovereign Identity** [[paper](https://arxiv.org/abs/2511.18379)]

[⬆ Back to top](#paper-list)

### Open Source

#### Method

##### 2026

- [2026] **Functional Scars: A Runtime Mechanism for Persistent Corrections in AI Agent Systems** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23106788)]
- [2026] **A dataset of tear metabolomics for predicting delirium during anesthesia emergence and postoperative period in elderly patients undergoing abdominal surgery (2022-2023)** *ScienceDB* [[paper](https://doi.org/10.57760/sciencedb.37534)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **Re-Architecture of Proprietary Software Suites into Open-Source Alternatives** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23414149)]
- [2026] **Development and Experimental Validation of an Open-Source Computational Engine for 3D Datum Transformations, Rigorous Gauss-Markov Network Adjustments, and Hybrid Geoid Modeling** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23454946)]
- [2026] **Introduction to Macros in a Spreadsheet (using LibreOffice)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23196840)]
- [2026] **Combat PTSD & Veteran Mental Health Cohort (30,000 Veterans, 24-Month Follow-Up)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23376218)]
- [2026] **Architecture, Resilience and Evolutionary Optimization of Finland's Public IT Infrastructure** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22690944)]
- [2026] **LUSicurezza** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22354618)]
- [2026] **The Yorkshire & Humber Office for Data Analytics (YHODA) Data Pipeline** *ORDA - The University of Sheffield Research Data Catalogue and Repository* [[paper](https://doi.org/10.15131/shef.data.33208968)]
- [2026] **Beyond the Editing Canvas: Evidence Divergence in OOXML-to-LLM Ingestion** *arXiv (Cornell University)* [[paper](https://arxiv.org/abs/2608.25880)]
- [2026] **SVCF open source physics** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21248274)]
- [2026] **Architectural Cases for Lighting Simulation** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21325222)]
- [2026] **IMPROVER tools for physically consistent realizations** [[paper](https://doi.org/10.5194/ems2026-396)]
- [2026] **Why the dispute between Google and green recursive utility service LLC is contractual not and intellectual property dispute** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20767798)]
- [2026] **R Code for Regional Analysis: A Visualization Prototype of MOJ Registry Office Maps Using Leaflet – A Case Study of Chita City 地域分析のためのRコード:Leafletを用いた法務省登記所備付地図の可視化プロトタイプ ―知多市を事例として―** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20201919)]
- [2026] **ITU and Music & Arts: A Single-Axiom View of Acoustics, Music Theory, Music Perception, Composition, AI Music (Suno/Udio/MusicGen), Visual Arts, AI Art (DALL-E/Midjourney/Stable Diffusion), and Aesthetics — Pass-1 Extension Paper #4, Block C 2/6** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20262861)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **ParaTaxe: a Suite of Tools for Processing and Publishing Multi-parallel Corpora** [[paper](https://arxiv.org/abs/2610.32796)]
- [2026] **PyPottery: an AI-powered end-to-end suite for pottery processing and publication** [[paper](https://arxiv.org/abs/2610.02072)]
- [2026] **TestSuiteBench: Coding Agents Struggle to Generate Strong Test Suites from Specifications** [[paper](https://arxiv.org/abs/2610.13065)]
- [2026] **Design and Characterization of a Unified Continuum Robot Actuation Platform** [[paper](https://arxiv.org/abs/2610.19798)]
- [2026] **Jaxnasium: Embracing PyTrees For Any-Agent, Cross-Suite Reinforcement Learning** [[paper](https://arxiv.org/abs/2610.36075)] [[code](https://github.com/ponseko/jaxnasium)]
- [2026] **PhoneBot: A Low-Cost Open Humanoid Robot Platform Reusing Smartphones** [[paper](https://arxiv.org/abs/2610.08737)]
- [2026] **ClimbLab: MATLAB Simulation Platform for Legged Climbing Robotics** [[paper](https://arxiv.org/abs/2610.09315)]
- [2026] **Skywing: A Platform for Decentralized Mathematical Computing in Unreliable Environments** [[paper](https://arxiv.org/abs/2609.03145)]
- [2026] **Cnuas: A Software-Defined AI/HPC Rack-scale Emulation Platform and Hyperscale Data Center Facility Twin** [[paper](https://arxiv.org/abs/2609.15889)]
- [2026] **Catena: A Comprehensive Software Suite for Large-Scale Connectomics** [[paper](https://arxiv.org/abs/2609.21887)] [[code](https://github.com/Mohinta2892/catena.git)]
- [2026] **AgentWorld: Benchmarking Long-Horizon Collaboration of Multi-agent LLMs** *COLM 2026. Project website* [[paper](https://arxiv.org/abs/2609.31590)]
- [2026] **PANEL: An Open-Source, Self-Hosted Web Platform for Human Evaluation of Generative Models** [[paper](https://arxiv.org/abs/2609.31392)] [[code](https://github.com/matteospanio/panel)]
- [2026] **Entangle: Uncovering Collaboration in the GitHub Quantum Software Ecosystem** [[paper](https://arxiv.org/abs/2609.28349)]
- [2026] **PowerMarketJax: A JAX Benchmark Suite for Multi-Agent Reinforcement Learning in Power Markets** [[paper](https://arxiv.org/abs/2609.37321)] [[code](https://github.com/powermarketjax/PowerMarketJax)]
- [2026] **DD-suite: A cross-platform package to build Decision Diagrams for optimization purposes** [[paper](https://arxiv.org/abs/2608.10957)]
- [2026] **An Open-Source Benchmark Suite of 3D-IC Testcases** [[paper](https://arxiv.org/abs/2608.25155)]
- [2026] **An Open-Source Power Measurement Platform for System-Level Semiconductor Testing** [[paper](https://arxiv.org/abs/2608.05888)]
- [2026] **VibeJam: A User Study Platform for Web Development with Agents** [[paper](https://arxiv.org/abs/2608.29889)]
- [2026] **WatchLens: A Configurable Platform for Online Video Recommendation Experiments** [[paper](https://arxiv.org/abs/2608.04807)]
- [2026] **AmalthAI: An Open-Source Computer Vision Platform for Cultural Heritage** [[paper](https://arxiv.org/abs/2608.13343)] [[code](https://github.com/TEXTaiLES/AmalthAI)]
- [2026] **WIP: LLM Odyssey: A Game-Based Platform for Teaching LLM Engineering Concepts** [[paper](https://arxiv.org/abs/2608.16924)]
- [2026] **Hardware-Enabled Fuzzy Inference: Architectures, Platforms, and Emerging Trends** [[paper](https://arxiv.org/abs/2608.04031)]
- [2026] **CheMLFlow: An Open-Source Platform for Cheminformatics and Materials Informatics Applications** [[paper](https://arxiv.org/abs/2608.04942)]
- [2026] **Anamnesis: An Open-Source Platform for Large-Scale Backstory-Conditioned Survey Simulation** [[paper](https://arxiv.org/abs/2607.10628)]
- [2026] **OmegaUse-OfficeVal: Benchmarking LLM Agents on Long-Horizon Office-Suite Tasks with Economic Grounding** [[paper](https://arxiv.org/abs/2607.27155)]
- [2026] **ForMoSA: Forward Modeling tool for Spectral Analysis** [[paper](https://arxiv.org/abs/2607.26243)]
- [2026] **ParasGB: A Graph Benchmark Suite for Parasitic Estimation on AMS Circuits** [[paper](https://arxiv.org/abs/2607.23225)] [[code](https://github.com/ShenShan123/ParasGB.git)]
- [2026] **The Open Ant: A Robot Platform for Reinforcement Learning Research** [[paper](https://arxiv.org/abs/2607.18488)]
- [2026] **CATKit2-HCI: a collaborative framework for advancing high-contrast coronagraph testbeds** [[paper](https://arxiv.org/abs/2607.19921)]
- [2026] **HighTide: An Agent-Curated Open-Source VLSI Benchmark Suite** [[paper](https://arxiv.org/abs/2606.04126)]
- [2026] **CollaboratoR: A scalable workflow for collaborative data entry and management** [[paper](https://arxiv.org/abs/2606.19280)]
- [2026] **Beyond Coverage and Kill Scores: Empirically Measuring Test Suite Behavioural Gaps** [[paper](https://arxiv.org/abs/2606.10417)]
- [2026] **SwarmFly: A simulation platform for UAV swarm experiment design and validation** [[paper](https://arxiv.org/abs/2606.25146)] [[code](https://github.com/abhishekphadke/SwarmFly.git)]
- [2026] **OpenEAI-Platform: An Open-source Embodied Artificial Intelligence Hardware-Software Unified Platform** [[paper](https://arxiv.org/abs/2606.03392)]
- [2026] **QCI Connect: A Modular Full-Stack Quantum Computing Platform** [[paper](https://arxiv.org/abs/2606.14456)]
- [2026] **tap: A File-Based Protocol for Heterogeneous LLM Agent Collaboration** [[paper](https://arxiv.org/abs/2606.14445)]
- [2026] **Knowledge-Based Pull Requests: A Trusted Workflow for Agent-Mediated Knowledge Collaboration** [[paper](https://arxiv.org/abs/2606.26721)]
- [2026] **CoLI: A Reproducible Platform for Continuum Robot Learning via Monolithic 3D Printing and Isomorphic Teleoperation** [[paper](https://arxiv.org/abs/2606.20389)]
- [2026] **From Prompts to Preferences: An Open-Source Platform for Generative AI-Enhanced Conjoint Analysis** [[paper](https://arxiv.org/abs/2606.12972)]
- [2026] **DeskCraft: Benchmarking Desktop Agents on Professional Workflows and Human-in-the-Loop Collaboration** [[paper](https://arxiv.org/abs/2606.03103)] [[code](https://github.com/mrwwk/DeskCraft)]
- [2026] **ORCA: A Platform for Open-Source Dexterity Research** [[paper](https://arxiv.org/abs/2606.14561)]
- [2026] **PatRe: A Full-Stage Office Action and Rebuttal Generation Benchmark for Patent Examination** [[paper](https://arxiv.org/abs/2605.03571)]
- [2026] **Method-level Change-proneness: A Better Metric for Black-box Test Suite Minimization** [[paper](https://arxiv.org/abs/2605.15232)]
- [2026] **OpenHealth Lake: Designing and testing a data lakehouse platform for health applications** [[paper](https://arxiv.org/abs/2605.19922)]
- [2026] **Building an Open Source Operational Technology Pentesting Platform: Lessons from LINICS** [[paper](https://arxiv.org/abs/2605.22590)]
- [2026] **LLARS: Enabling Domain Expert &amp; Developer Collaboration for LLM Prompting, Generation and Evaluation** *IJCAI-ECAI 2026 Demonstrations Track. Demo video* [[paper](https://arxiv.org/abs/2605.10593)]
- [2026] **Medmarks: A Comprehensive Open-Source LLM Benchmark Suite for Medical Tasks** [[paper](https://arxiv.org/abs/2605.01417)] [[code](https://github.com/MedARC-AI/Medmarks)]
- [2026] **stable-worldmodel: A Platform for Reproducible World Modeling Research and Evaluation** [[paper](https://arxiv.org/abs/2605.21800)]
- [2026] **OpenCompass: A Universal Evaluation Platform for Large Language Models** [[paper](https://arxiv.org/abs/2605.19276)]
- [2026] **Randompack: Cross-Platform Reproducible Random Number Generation and Distribution Sampling** [[paper](https://arxiv.org/abs/2605.05099)]
- [2026] **VisAnalog: A Diagnostic Suite for Visual Concept Transfer on Natural Images** *CVPR 2026 as a non-archival report* [[paper](https://arxiv.org/abs/2605.23141)] [[project](https://huggingface.co/datasets/zli99/VisAnalog)]
- [2026] **BenGER Platform: A Collaborative Web Platform for End-to-End Benchmarking of German Legal Tasks** [[paper](https://arxiv.org/abs/2604.13583)]
- [2026] **Augmenting unit test suites from integration tests** [[paper](https://arxiv.org/abs/2604.17508)]
- [2026] **CommonMorph: Participatory Morphological Documentation Platform** [[paper](https://arxiv.org/abs/2604.04515)]
- [2026] **FUTURAL: A Metasearch Platform for Empowering Rural Areas with Smart Solutions** [[paper](https://arxiv.org/abs/2604.23817)]
- [2026] **TestDecision: Sequential Test Suite Generation via Greedy Optimization and Reinforcement Learning** [[paper](https://arxiv.org/abs/2604.01799)]
- [2026] **An Affordable, Wearable Stereo-Eye-Tracking Platform** [[paper](https://arxiv.org/abs/2604.24331)]
- [2026] **COMB: Common Open Modular robotic platform for Bees** [[paper](https://arxiv.org/abs/2604.04980)]
- [2026] **From OSS to Open Source AI: an Exploratory Study of Collaborative Development Paradigm Divergence** [[paper](https://arxiv.org/abs/2604.08888)]
- [2026] **AgentSim: A Platform for Verifiable Agent-Trace Simulation** [[paper](https://arxiv.org/abs/2604.26653)]
- [2026] **ACT: Automated CPS Testing for Open-Source Robotic Platforms** [[paper](https://arxiv.org/abs/2604.11708)]
- [2026] **LEGO: An LLM Skill-Based Front-End Design Generation Platform** [[paper](https://arxiv.org/abs/2604.23355)] [[code](https://github.com/loujc/LEGO-An-LLM-Skill-Based-Front-End-Design-Generation-Platform)]
- [2026] **AutoREC: A reinforcement learning platform for equivalent circuit model generation** [[paper](https://arxiv.org/abs/2604.27266)]
- [2026] **The ecosystem of machine learning competitions: Platforms, participants, and their impact on AI development** [[paper](https://arxiv.org/abs/2604.08001)]
- [2026] **SimEval-IR: A Unified Toolkit and Benchmark Suite for Evaluating User Simulators and Search Sessions** [[paper](https://arxiv.org/abs/2604.27878)]
- [2026] **R2G: A Multi-View Circuit Graph Benchmark Suite from RTL to GDSII** [[paper](https://arxiv.org/abs/2604.08810)] [[code](https://github.com/ShenShan123/R2G)]
- [2026] **Metriq: A Collaborative Platform for Benchmarking Quantum Computers** [[paper](https://arxiv.org/abs/2603.08680)]
- [2026] **GeoBenchr: An Application-Centric Benchmarking Suite for Spatiotemporal Database Platforms** [[paper](https://arxiv.org/abs/2603.09398)]
- [2026] **Votiverse: A Configurable Governance Platform for Democratic Decision-Making** [[paper](https://arxiv.org/abs/2604.20863)]
- [2026] **Robotic Agentic Platform for Intelligent Electric Vehicle Disassembly** [[paper](https://arxiv.org/abs/2603.18520)]
- [2026] **RADIUS: Ranking, Distribution, and Significance - A Comprehensive Alignment Suite for Survey Simulation** [[paper](https://arxiv.org/abs/2603.19002)]
- [2026] **An Open-Source Robotics Research Platform for Autonomous Laparoscopic Surgery** [[paper](https://arxiv.org/abs/2603.08490)]
- [2026] **EnterpriseLab: A Full-Stack Platform for developing and deploying agents in Enterprises** [[paper](https://arxiv.org/abs/2603.21630)]
- [2026] **Evaluation and Benchmarking Suite for Financial Large Language Models and Agents** [[paper](https://arxiv.org/abs/2602.19073)]
- [2026] **ICSSPulse: A Modular LLM-Assisted Platform for Industrial Control System Penetration Testing** [[paper](https://arxiv.org/abs/2602.20663)]
- [2026] **AIRS-Bench: a Suite of Tasks for Frontier AI Research Science Agents** [[paper](https://arxiv.org/abs/2602.06855)]
- [2026] **VirtualEnv: A Platform for Embodied AI Research** [[paper](https://arxiv.org/abs/2601.07553)]
- [2026] **ArabicDialectHub: A Cross-Dialectal Arabic Learning Resource and Platform** [[paper](https://arxiv.org/abs/2601.22987)]
- [2026] **Lantern: A Minimalist Robotic Object Platform** [[paper](https://arxiv.org/abs/2601.22381)]
- [2026] **OpenISAC: An Open-Source Real-Time Experimentation Platform for OFDM-ISAC** [[paper](https://arxiv.org/abs/2601.03535)]
- [2026] **FTCircuitBench: A Benchmark Suite for Fault-Tolerant Quantum Compilation and Architecture** [[paper](https://arxiv.org/abs/2601.03185)]
- [2026] **CORE: Collaborative Reasoning via Cross Teaching** [[paper](https://arxiv.org/abs/2601.21600)]
- [2026] **Securing LLM-as-a-Service for Small Businesses: An Industry Case Study of a Distributed Chatbot Deployment Platform** [[paper](https://arxiv.org/abs/2601.15528)]
- [2026] **ECGomics: An Open Platform for AI-ECG Digital Biomarker Discovery** [[paper](https://arxiv.org/abs/2601.15326)] [[code](https://github.com/PKUDigitalHealth/ECGomics)]
- [2026] **Investigating Notable Metadata Practices in PyPI Libraries: An Empirical Study about Repository and Donation Platform URLs** [[paper](https://arxiv.org/abs/2601.15139)]
- [2026] **MHDash: An Online Platform for Benchmarking Mental Health-Aware AI Assistants** [[paper](https://arxiv.org/abs/2602.00353)]
- [2026] **An Open-Source Platform for Industrial Collaboration on CO2-Impurity Studies** *World CCUS Conference 2026* [[paper](https://doi.org/10.3997/2214-4609.202622087)]

##### 2025

- [2025] **The HEAL Data Platform** [[paper](https://arxiv.org/abs/2512.17506)]
- [2025] **Kaapana: A Comprehensive Open-Source Platform for Integrating AI in Medical Imaging Research Environments** [[paper](https://arxiv.org/abs/2512.09644)] [[code](https://github.com/kaapana/kaapana)]
- [2025] **Model Gateway: Management Platform for Model-Driven Drug Discovery** [[paper](https://arxiv.org/abs/2512.05462)]
- [2025] **AI4EOSC: a Federated Cloud Platform for Artificial Intelligence in Scientific Research** [[paper](https://arxiv.org/abs/2512.16455)]
- [2025] **Scalable Relay Switching Platform for Automated Multi-Point Resistance Measurements** [[paper](https://arxiv.org/abs/2512.20419)]
- [2025] **DeepQuantum: A PyTorch-based Software Platform for Quantum Machine Learning and Photonic Quantum Computing** [[paper](https://arxiv.org/abs/2512.18995)]
- [2025] **The SCIP Optimization Suite 10.0** [[paper](https://arxiv.org/abs/2511.18580)]
- [2025] **Preemption-Enhanced Benchmark Suite for FPGAs** [[paper](https://arxiv.org/abs/2511.06736)]
- [2025] **AfriSpeech-MultiBench: A Verticalized Multidomain Multicountry Benchmark Suite for African Accented English ASR** [[paper](https://arxiv.org/abs/2511.14255)]
- [2025] **FsimNNs: An Open-Source Graph Neural Network Platform for SEU Simulation-based Fault Injection** [[paper](https://arxiv.org/abs/2511.09131)] [[code](https://github.com/luli2021/FsimNNs)]
- [2025] **DISCO: A Browser-Based Privacy-Preserving Framework for Distributed Collaborative Learning** [[paper](https://arxiv.org/abs/2511.19750)] [[code](https://github.com/epfml/disco)]
- [2025] **Latent Collaboration in Multi-Agent Systems** [[paper](https://arxiv.org/abs/2511.20639)] [[code](https://github.com/Gen-Verse/LatentMAS)]
- [2025] **Retraction: The construction of ecosystem and collaboration platform for enterprise open innovation** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2025.1675298)]

##### 2019

- [2019] **Issue Reports Analysis in Enterprise Open Source Systems** *Proceedings of the 21st International Conference on Enterprise Information Systems* [[paper](https://doi.org/10.5220/0007757803370344)]

##### 2011

- [2011] **A FEATURE-BASED ANALYSIS OF OPEN SOURCE TOOLS FOR ENTERPRISE 2.0 - Open Source Tools for Team Collaboration in SMEs** *Proceedings of the International Conference on Knowledge Management and Information Sharing* [[paper](https://doi.org/10.5220/0003638400570066)]

##### 2007

- [2007] **The Open Source Platform** *Open Source* [[paper](https://doi.org/10.1017/cbo9780511619526.004)]

##### 2005

- [2005] **Learning-Based Computer Vision with Intels Open Source Computer Vision Library** *Understanding the Platform Requirements of Emerging Enterprise Solutions* [[paper](https://doi.org/10.1535/itj.0902.03)]

[⬆ Back to top](#paper-list)

### Public Sector & Education

#### Method

##### 2026

- [2026] **SlangLane Public Sector, Municipal Libraries, Youth Online Safety & Civic Digital Literacy Dataset (2026 Release)** *Harvard Dataverse* [[paper](https://doi.org/10.7910/dvn/uq0xlo)]
- [2026] **Work-related health information literacy: a factor analytic feasibility study of an adapted health information literacy screening tool (EHILS@work)** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1974525)]
- [2026] **Transformational and Inclusive Leadership Communication in Driving Public Sector Organizational Change in the Digital Transformation Era** *International Journal of Economics and Management Research* [[paper](https://doi.org/10.55606/ijemr.v5i2.741)]
- [2026] **Professional development for workplace learning: evidence from community skills instructors in Malaysia** *Journal of Workplace Learning* [[paper](https://doi.org/10.1108/jwl-07-2026-0449)]
- [2026] **Expectativas del sector empresarial sobre las competencias de egresados en mercadotecnia en Tlaxcala** *Revista Colombiana de Ciencias Administrativas* [[paper](https://doi.org/10.52948/rcca.v8i1.1336)]
- [2026] **The influence of digital leadership and work environment on employee performance at BPKPD of Tebing Tinggi City** *Economic Journal Economic and Business* [[paper](https://doi.org/10.56495/ejeb.v5i3.1666)]
- [2026] **АДАПТАЦИЯ МОЛОДЫХ СПЕЦИАЛИСТОВ НА ГОССЛУЖБЕ: ПРОБЛЕМЫ И ПУТИ ИХ РЕШЕНИЯ** *Reputaciologiâ.* [[paper](https://doi.org/10.34925/2071-9094.2026.79.1.005)]
- [2026] **Harnessing Counselling Practice to Empower Youth for National Development** *INTERNATIONAL JOURNAL OF EDUCATION AND EVALUATION* [[paper](https://doi.org/10.56201/ijee.v12.no.2.2026.pg995.1007)]
- [2026] **Digital transformation: The strain of being an “immigrant” in the digital workplace** *Psychology the Journal of the Hellenic Psychological Society* [[paper](https://doi.org/10.12681/psy_hps.46304)]
- [2026] **Systematic Literature Review: Public Understanding of Artificial Intelligence Amid the Development of Digital Technology** *Devotion Journal of Research and Community Service* [[paper](https://doi.org/10.59188/devotion.v7i7.25723)]
- [2026] **FACTORS CONTRIBUTING TO STUDENT SUCCESS AND FAILURE IN OPEN DISTANCE E-LEARNING AMONG OFFICIALS STUDYING IN SOUTH AFRICA** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21652797)]
- [2026] **GCC Bottled Water Industry Expands Through Water Security and Consumer Demand** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21353080)]
- [2026] **NAVIGATING THE AI-DRIVEN TRANSFORMATION OF EMPLOYMENT RELATIONS IN SABAH PUBLIC SECTOR: A PRELIMINARY STUDY** *Quantum Journal of Social Sciences and Humanities* [[paper](https://doi.org/10.55197/qjssh.v7i3.1421)]
- [2026] **LEADERSHIP STYLE AND ORGANIZATIONAL PERFORMANCE IN NIGERIA'S PUBLIC SERVICE: ASSESSING TRANSFORMATIONAL LEADERSHIP PRACTICES IN KADUNA STATE CIVIL SERVICE** *KASU Journal of Management Sciences* [[paper](https://doi.org/10.68022/kjms.2026.ipxi63ti)]
- [2026] **Designing Motivating Digital Workplaces: An Evidence-Based Brief for Leaders Navigating the Technology–Motivation Interface** *Human capital leadership.* [[paper](https://doi.org/10.70175/hclreview.2020.34.3.6)]
- [2026] **MECHANISMS OF STATE MANAGEMENT OF THE DEVELOPMENT OF PSYCHOLOGICAL RESILIENCE OF PUBLIC SERVICE PERSONNEL IN THE CONDITIONS OF THE RUSSIAN-UKRAINIAN WAR** *Coordinates of Public Administration* [[paper](https://doi.org/10.62664/cpa.2026.01.17)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **E-HRM as a behavioural enabler of public sector digital transformation** *Multidisciplinary Reviews* [[paper](https://malque.pub/ojs/index.php/mr/article/view/21533)]
- [2026] **Strategic Human Capital Disclosure, Agile Work Culture, And Public Trust Via Workplace Pro Environmental Behavior** *EKOMBIS REVIEW Jurnal Ilmiah Ekonomi dan Bisnis* [[paper](https://doi.org/10.37676/ekombis.v14i4.10359)]
- [2026] **Flexible Work Arrangements and Organizational Outcomes: Evidence from the Public Sector** *Journal of Public Policy and Administration* [[paper](https://doi.org/10.11648/j.jppa.20261004.11)]
- [2026] **Innovating public sector education: integrating lean and micro-credentials for sustainable governance in Brazil** *Journal of International Cooperation in Education* [[paper](https://doi.org/10.1108/jice-07-2025-0040)]
- [2026] **Workplace Mental Health and Psychological Safety: A Systematic Review of Interventions and Outcomes** [[paper](https://doi.org/10.31235/osf.io/ehcwa_v1)]
- [2026] **SlangLane Workplace Register-Switching, Organizational Idioms & Intergenerational Communication Pragmatics Dataset (2026 — Volume 14)** *DataverseNL* [[paper](https://doi.org/10.34894/hkamln)]
- [2026] **An Analysis Of The Impact Of Workplace Telepressure On Cognitive Fatigue Among Civil Servants At Bkn Regional I: The Moderating Role Of Tenure** *Jurnal Perilaku dan Strategi Bisnis* [[paper](https://ejurnal.mercubuana-yogya.ac.id/index.php/JPSB/article/view/5653)]
- [2026] **Digital Leadership in Digital Transformation: A Bibliometric Analysis of Current Trends and Future Directions** *Research Square* [[paper](https://doi.org/10.21203/rs.3.rs-11364835/v1)]
- [2026] **Job Demands, Resources, and Digital Job Stress: The Roles of Knowledge Diversity and Interruption Overload in Digitalized Work Settings** *SAGE Open* [[paper](https://doi.org/10.1177/21582440261494250)]
- [2026] **Digital Competency and Artificial Intelligence Integration in Modern Administration: Current Demands, Gaps, and Strategic Pathways** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23601312)]
- [2026] **SlangLane Adult ESL Literacy, Community College Bridge Programs & Workplace Idioms Dataset (2026 — Volume 68)** *DataverseNL* [[paper](https://doi.org/10.34894/lfycbl)]
- [2026] **The AI Tsunami: Transforming Employment, Skills, and the Future of Work in the Digital Economy — An Integrated Analysis of Automation, Human–AI Collaboration, Workforce Reskilling, and Socioeconomic Transformation** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23342959)]
- [2026] **Aligning enterprise viability with population health: a public health–oriented food entrepreneurship framework for urban food systems** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1963621)]
- [2026] **Mental health for Viksit Bharat@2047: Building a resilient, productive and inclusive India** *International Journal of Psychology Sciences* [[paper](https://doi.org/10.33545/26648377.2026.v8.i10a.200)]
- [2026] **Sustainable Working Lives in Ageing Societies: Policy Lessons from the Nordic–Baltic Region** *European Journal of Public Health* [[paper](https://doi.org/10.1093/eurpub/ckag169.372)]
- [2026] **Beyond AI Skills** *VETNET Conference Series* [[paper](https://doi.org/10.21240/vetcon/2026/ecer/94)]
- [2026] **SlangLane Open Reference Corpus (220 Entries, 30 Interactive Tools): Conversational English, Sociology, Psychology & CEFR ESL Dataset (2026)** *DataRepositoriUM* [[paper](https://doi.org/10.34622/datarepositorium/0vzfb6)]
- [2026] **SlangLane Vocational ESL, Hospitality & Customer-Facing Pragmatics Training Dataset (2026 — Volume 88)** *DataverseNL* [[paper](https://doi.org/10.34894/5d1r1y)]
- [2026] **THE INFLUENCE OF AI READINESS ON EMPLOYEE PERFORMANCE: THE ROLE OF ORGANIZATIONAL SUPPORT** *Journal of Organizational Management and Strategic Studies (JOMSS)* [[paper](https://jocsses.com/index.php/index/article/view/110)]
- [2026] **Health Policy for Obesity and Metabolic Syndrome in Asian Health Systems: Three Design Principles, Three Binding Constraints, and the Governance That Decides between Them** *Journal of Obesity & Metabolic Syndrome* [[paper](https://doi.org/10.7570/jomes26017)]
- [2026] **Y.11.PK.2. From Evidence to Action: EU studies on occupational risk and diseases** *European Journal of Public Health* [[paper](https://doi.org/10.1093/eurpub/ckag169.764)]
- [2026] **The Role of Inclusive HR Practice in Neurodiverse Talent Retention in International Business Environment: A Qualitative Inquiry** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i10.259)]
- [2026] **Nowe wektory zarządzania: Ekonomia behawioralna dla świadomych i różnorodnych organizacji** [[paper](https://doi.org/10.13166/awsge/236047)]
- [2026] **PREreview of "Differential Effects of Artificial Intelligence Components on Administrative Outcomes in Nigerian Tertiary Institutions: A Comparative Analysis of OCR, CVA, and RPA"** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23269199)]
- [2026] **Editorial: Socio-legal, ethical, technical and medical considerations on neuroprivacy and brain-machine interaction technologies in the era of A.I.** *Frontiers in Human Dynamics* [[paper](https://doi.org/10.3389/fhumd.2026.1836498)]
- [2026] **AI-Driven Feedback Systems, Digital Labour, and Silent Quitting: Transforming African Workplaces** *arXiv (Cornell University)* [[paper](https://arxiv.org/abs/2609.16192)]
- [2026] **Learning in the workplace** [[paper](https://doi.org/10.4102/aosis.2026.bk586.06)]
- [2026] **Factors Influencing Malaysian Public Sector Employee Performance in a Work-From-Home Context** *International Journal of Human Resource Studies* [[paper](https://doi.org/10.5296/ijhrs.v16i2.23580)]
- [2026] **From evidence to action: Why employers must address prolonged sitting in modern workplaces** *Public Health* [[paper](https://doi.org/10.1016/j.puhe.2026.106484)]
- [2026] **WOMEN WORK AND WORKPLACE SAFETY IN CONTEMPORARY INDIA A Sociological Study of Employment Digitalisation Social Security and Emerging Gender Issues** *International Journal of Versatile Research and Analysis* [[paper](https://doi.org/10.56975/ijvra.v4i9.710930)]
- [2026] **PSYCHOSOCIAL DETERMINANTS OF ORGANIZATIONAL CONFLICT IN A DIGITAL WORK ENVIRONMENT: A NARRATIVE REVIEW** *Collection of papers New economy* [[paper](https://doi.org/10.61432/cpne0401219p)]
- [2026] **Artificial Intelligence Adoption and Employee Productivity: The Mediating Role of Digital Competence** *Academia International Research Journal (Multi Disciplinary)* [[paper](https://academia.edu.pk/index.php/AIRJ/article/view/2473)]
- [2026] **ASSESSMENT OF THE RELATIONSHIP BETWEEN THE LEVEL OF DIGITAL TRANSFORMATION AND EMPLOYMENT INDICATORS (THE CASE OF AZERBAIJAN)** *EKONOMISTI* [[paper](https://doi.org/10.52340/ekonomisti.2026.03.08)]
- [2026] **Human-Centered Leadership in the Age of AI and Automation** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-3373-5509-2.ch004)]
- [2026] **Serene Mind Mental Health Data Index: Anonymized Corporate and Community Triage Insights (Uganda)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22795803)]
- [2026] **ARCHIVAL PERFORMANCE MODEL: THE ROLE OF LEADERSHIP, ORGANIZATIONAL COMMUNICATION, HUMAN CAPITAL QUALITY, WORK CULTURE, AND ELECTRONIC RECORDS MANAGEMENT SYSTEM** *Acta Innovations* [[paper](https://doi.org/10.62441/actainnovations.v63i.1941)]
- [2026] **Evaluation of Educational and Occupational Determinants on Societal Compliance with Health Protocols During the Pandemic Period in Indonesia** *Contagion Scientific Periodical Journal of Public Health and Coastal Health* [[paper](https://doi.org/10.30829/contagion.v8i3.29534)]
- [2026] **Humanoid Workforce Safety Monitoring and Intervention System** [[paper](https://doi.org/10.62311/nesx/rb-51sep-978-81-17475-49-2)]
- [2026] **Developing a Productivity Management Framework for Service Organizations with a Focus on Improving Service Delivery Processes** *DOAJ (DOAJ: Directory of Open Access Journals)* [[paper](https://doaj.org/article/282a8d7d20d3401ab66fb2b4e4023d7b)]
- [2026] **International approaches to career development for working people** *UDORA* [[paper](https://doi.org/10.48773/1eza-sk68)]
- [2026] **Youth Policy and Democratic Governance in Georgia: Theoretical and Policy Analysis** *EKONOMISTI* [[paper](https://doi.org/10.52340/ekonomisti.2026.03.14)]
- [2026] **Environmental Factors and Corporate Strategy-Structure Choices for Organizational Effectiveness** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i9.228)]
- [2026] **Conceptual Fragmentation in Green Human Resource Management: A Bibliometric Analysis of Its Path Toward Theoretical Integration** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i9.190)]
- [2026] **CASTLE2 Opening Research Report** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22689157)]
- [2026] **Transformational leadership as a mediator of the influence of digital workplace and digital culture on employee engagement (Evidence from the Indonesian public sector)** *Jurnal Mantik* [[paper](https://iocscience.org/ejournal/index.php/mantik/article/view/7344)]
- [2026] **DIGITAL WORKPLACE STRESS AND EMPLOYEE WELL-BEING PSYCHOLOGICAL AND ORGANIZATIONAL PERSPECTIVES** *Journal of Social Research Development* [[paper](https://doi.org/10.59075/jsrd.v7i6.516)]
- [2026] **Digital Competence as a Predictor of AI Readiness in Public Sector Organizations: Evidence from Indonesian Civil Servants** *International Journal of Management and Business Intelligence* [[paper](https://doi.org/10.59890/ijmbi.v4i4.38)]
- [2026] **Beyond the Hype: Do Industry 4.0 Competencies Improve Job Performance? Empirical Evidence from the Omani Public Sector** *Human Resources Management and Services* [[paper](https://doi.org/10.18282/hrms6002)]
- [2026] **Public Policy Imperatives for Emerging AI Surveillance Technologies** *Journal of the Association for Information Systems* [[paper](https://aisel.aisnet.org/treos_amcis2026/127)]
- [2026] **Bridging the Divide: Integrating Public Health and Psychiatry to Address the Global Mental Health Crisis** *Journal of Psychiatry and Psychological Sciences* [[paper](https://doi.org/10.67238/jppc.2026.v2.17)]
- [2026] **Developing a candidate competency framework for early-career pharmacists in Chinese public hospitals: A two-round modified Delphi study** *Intelligent Pharmacy* [[paper](https://doi.org/10.1016/j.ipha.2026.08.007)]
- [2026] **Organizational Readiness and Employees’ Intention to Adopt Artificial Intelligence in Local Government: Evidence from Greece** *Preprints.org* [[paper](https://doi.org/10.20944/preprints202608.0305.v1)]
- [2026] **การพฒนาแผนกลยทธการสงเสรมสขภาพประชาชนวยทำงานระดบประเทศ พ.ศ. 2568-2580** *JOURNAL OF REGIONAL HEALH PROMOTION CENTRE 7 KHONKAEN* [[paper](https://he01.tci-thaijo.org/index.php/johpc7/article/view/290393)]
- [2026] **A bibliometric analysis of biophilic architectural principles: global trends and research evolution** *Frontiers in Research Metrics and Analytics* [[paper](https://doi.org/10.3389/frma.2026.1914242)]
- [2026] **Beyond Automation: Reimagining Human-Centered Systems for AI-Mediated Institutions** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21844490)]
- [2026] **Artificial Intelligence (AI) on Construction Projects: Regulatory Position and Governance Gaps** [[paper](https://doi.org/10.31224/8076)]
- [2026] **Impact of Artificial Intelligence Adoption on Worker Commitment in Nigeria** *INTERNATIONAL JOURNAL OF SOCIAL SCIENCES AND MANAGEMENT RESEARCH* [[paper](https://doi.org/10.56201/ijssmr.vol.12no6.2026.pg558.571)]
- [2026] **Artificial Intelligence and Blockchain-Enabled Human Resource Analytics for Strategic Workforce Intelligence** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i8.145)]
- [2026] **Health Governance Review Volume 31, Issue 3: Evidence synthesis for health governance** *International Journal of Health Governance* [[paper](https://doi.org/10.1108/ijhg-09-2026-227)]
- [2026] **Correction: Factors associated with work-life balance among emergency physicians, nurses, and paramedics: a systematic review** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1951408)]
- [2026] **Work-Life Balance as a Predictor of Performance in Female Workers in the Public Sector in the Digital Era** *Publik (Jurnal Ilmu Administrasi)* [[paper](https://journal.umgo.ac.id/index.php/Publik/article/view/5556)]
- [2026] **Navigating Digital Transformation in Chinese Workplaces: Developing the ESCQ Competency Framework** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.12288abstract)]
- [2026] **Digital capability development in the public sector: an HRD-Informed framework from the NSTA** *European journal of training and development* [[paper](https://doi.org/10.1108/ejtd-10-2025-0240)]
- [2026] **Post-Pandemic HR Innovations and Employee Well-Being in Nigerian Universities: Interrogating Digitalization Compliance in Public Sector Resilience** *Public Organization Review* [[paper](https://doi.org/10.1007/s11115-026-01035-y)]
- [2026] **Determinants of information security policy compliance: integrating task-technology fit and threat avoidance appraisals in the digital workplace** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2026.1861737)]
- [2026] **Cyber incivility, cyberslacking, and negative reciprocity: moderation of digital well-being** *Service Industries Journal* [[paper](https://doi.org/10.1080/02642069.2026.2705880)]
- [2026] **HR Strategic Approaches in Public Sector Higher Education Institutions: The Role of Human Resource Development in Achieving Optimal Person-Job Fit** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i7.104)]
- [2026] **Work From Anywhere and Public Service Responsiveness in Indonesia: The Mediating Mechanisms of Employee Engagement and Performance** *F1000Research* [[paper](https://doi.org/10.12688/f1000research.184616.1)]
- [2026] **Preventable yet persistent: silicosis and gaps in public health policy – a narrative review** *Monaldi Archives for Chest Disease* [[paper](https://doi.org/10.4081/monaldi.2026.3937)]
- [2026] **The Effect of Digital Competence on Employee Performance: The Mediating Roles of Self-Efficacy and Job Satisfaction (A Case Study of the Tangerang City Regional Revenue Agency)** *Prosperia Journal of Economic Development Accounting and Global Markets* [[paper](https://doi.org/10.65310/z8d8an75)]
- [2026] **Guest editorial: Beyond Industry 4.0: humancentricity, resilience and sustainability in the age of digital transformation** *Journal of strategy and management* [[paper](https://doi.org/10.1108/jsma-08-2026-526)]
- [2026] **Understanding how and when servant leadership inhibits employees’ cyberloafing behaviors at work. A moderated mediation model** *Current Psychology* [[paper](https://doi.org/10.1007/s12144-026-09038-0)]
- [2026] **Penerapan Green Human Resource Management (GHRM) dan Dampaknya terhadap Kinerja Aparatur Sipil Negara di Pemerintah Kota Medan** *Journal of Digital Business and Management* [[paper](https://doi.org/10.32639/jpyqzh12)]
- [2026] **Futures of work** *publish.UP (University of Potsdam)* [[paper](https://nbn-resolving.org/urn:nbn:de:kobv:517-opus4-707867)]
- [2026] **The Impact of Training, Knowledge Management, and Discipline on Employee Effectiveness, with the Work Environment as A Moderating Variable at the Ministry of Health of the Republic of Indonesia** *Indonesian Journal of Multidisciplinary Science* [[paper](https://doi.org/10.55324/ijoms.v5i10.1312)]
- [2026] **Assessing construction companies’ commitment to employees’ mental well-being: A content analysis of website disclosures** *Journal of Workplace Behavioral Health* [[paper](https://doi.org/10.1080/15555240.2026.2702508)]
- [2026] **แอนแทรกซ: การจดการอาชวอนามยและความปลอดภยภายใตแนวทางสขภาพหนงเดยว: Anthrax: Occupational Health and Safety Management under the One Health Approach** *Advanced Science Journal* [[paper](https://li02.tci-thaijo.org/index.php/adscij/article/view/1209)]
- [2026] **Editor's note** *Revista Ibérica do Direito* [[paper](https://revistaibericadodireito.pt/index.php/capa/article/view/242)]
- [2026] **Psychological Empowerment and Workforce Agility: The Mediating Role of Transformational Leadership Among Teaching Staff** *Jurnal Psikologi Wijaya Putra (Psikowipa)* [[paper](https://doi.org/10.38156/psikowipa.v7i1.544)]
- [2026] **Navigating the Demographic Shift and Solving the Elderly Mental Healthcare Needs-The Call for A Kerala State Senior Citizen Mental Health Policy** *Kerala Journal of Psychiatry* [[paper](https://doi.org/10.30834/kjp.39.1.2026.646)]
- [2026] **Editorial: Non-ionizing radiation: impacts on human health from exposures in occupational settings** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1880564)]
- [2026] **Sustainability Integration through AI-Driven Marketing Intelligence: Emerging Strategies and Implications** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i7.119)]
- [2026] **Editorial: Exploring meaningful extended reality (XR) experiences: psychological, educational, and data-driven perspectives** *Frontiers in Virtual Reality* [[paper](https://doi.org/10.3389/frvir.2026.1935335)]
- [2026] **Guest editorial: Entrepreneurial strategy and cultural practices towards sustainable business growth: language and sensemaking** *Baltic Journal of Management* [[paper](https://doi.org/10.1108/bjm-08-2026-923)]
- [2026] **Managerial resistance to digital workplace surveillance in a local government authority** *Government Information Quarterly* [[paper](https://doi.org/10.1016/j.giq.2026.102162)]
- [2026] **Job Crafting in the Digital Workplace: A Systematic Literature Review Using the CIMO Framework** *West Science Business and Management* [[paper](https://doi.org/10.58812/wsbm.v4i02.2887)]
- [2026] **EFFECT OF WORKPLACE INCIVILITY ON EMOTIONAL INTELLIGENCE** *Center for Management Science Research* [[paper](https://cmsrjournal.com/index.php/Journal/article/view/1049)]
- [2026] **VISION CARE IN WORKPLACE SETTINGS, ERGONOMICS AND MANAGING ENVIRONMENTAL RISK FACTORS** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennuraoi2)]
- [2026] **Editorial: Navigating environmental hazards in the workplace: impacts and interventions** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1893964)]
- [2026] **Individually Driven, Institutionally Under-Supported: AI Readiness for Public Service Innovation in Romania** *Urban Science* [[paper](https://doi.org/10.3390/urbansci10070360)]
- [2026] **Bureaucratic Bullying in Government Organizations: Power Relations, Merit System, and Public Governance** *Jurnal Ilmiah Guru Madrasah.* [[paper](https://doi.org/10.69548/jigm.v5i1.118)]
- [2026] **DECENT JOBS AND DIGITAL GOVERNANCE: A HUMAN-CENTERED HRM ECOSYSTEM IN KAZAKHSTAN'S CIVIL SERVICE** *Bangladesh Journal of Multidisciplinary Scientific Research* [[paper](https://doi.org/10.46281/bjmsr.v11i3.2901)]
- [2026] **Digitalization-Driven Green HRM Practices and Employee Green Behavior in a Metropolitan Municipality** *Administrative Sciences* [[paper](https://doi.org/10.3390/admsci16060289)]
- [2026] **Reimagining the Workplace After the Pandemic: The Influence of Post-COVID HR Practices on Engagement among Mid-Level BFSI Professionals in India** *IARJSET* [[paper](https://doi.org/10.17148/iarjset.2026.13649)]
- [2026] **Occupational health and safety in the wake of COVID-19: insights from India's workforce** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1807940)]
- [2026] **Future of Work-G7 Nations: Trends, Insights and Automation Effects** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21662468)]
- [2026] **Striving for Adopting and Adapting Information Technology: A Qualitative Study of Informal Skills Learners in Nepal** *Journal of Training and Development* [[paper](https://doi.org/10.3126/jtd.v8i1.95888)]
- [2026] **ผลกระทบตอการคกคามโดยใชอำนาจของผบงคบบญชาในสถานประกอบการอตสาหกรรมไทยในดานความเปนอยและการทำงานของพนกงาน** *Journal of MCU Dvravati Review* [[paper](https://so10.tci-thaijo.org/index.php/jmdr/article/view/3167)]
- [2026] **Letter to the Editor: Integrating Health Literacy Into National Diabetes Prevention Policies** *International Journal of Advanced Multidisciplinary Research and Studies* [[paper](https://doi.org/10.62225/2583049x.2026.6.3.6421)]
- [2026] **The Role of Self-Control in Reducing Burnout within Toxic Work Environments: A Narrative Review of Self-Regulation Theory in Indonesian Multisector Organizations (2024–2025)** *Oase* [[paper](https://journal.oaseinstitute.org/index.php/OASE/article/view/190)]
- [2026] **Sustaining the workforce: job retention and workforce challenges among community pharmacists in Northern Ireland** *Journal of Pharmaceutical Policy and Practice* [[paper](https://doi.org/10.1080/20523211.2026.2677776)]
- [2026] **The Impact of Women’s Training and Empowerment on Leadership Effectiveness in Ethiopia: A Systematic Review** *Asian Journal of Economics Business and Accounting* [[paper](https://doi.org/10.9734/ajeba/2026/v26i62310)]
- [2026] **Recruitment and Selection** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003560173-2)]
- [2026] **Guest editorial: Knowing and learning in the age of intelligent machines** *Journal of Workplace Learning* [[paper](https://doi.org/10.1108/jwl-07-2026-412)]
- [2026] **When Complexity Becomes the Norm: Cardiovascular Multimorbidity** *The Journal of Cardiovascular Nursing* [[paper](https://doi.org/10.1097/jcn.0000000000001351)]
- [2026] **Síndrome de burnout e fibromialgia: relação e impactos na saúde dos trabalhadores** *Humanidades em Perspectivas* [[paper](https://www.cadernosuninter.com/index.php/humanidades/article/view/3388)]
- [2026] **The role of Emotional Intelligence during Stressed and Demoralized Environments Inside Organizations** *Inverge Journal of Social Sciences* [[paper](https://doi.org/10.63544/ijss.v5i3.304)]
- [2026] **Digital Transformation of the Public Sector** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003787952)]
- [2026] **Strengthening Inclusive Governance: Collaborative and Digital Pathways to People with Disability in Bali’s Tourism Sector** *KOLABORASI JURNAL ADMINISTRASI PUBLIK* [[paper](https://doi.org/10.26618/kjap.v12i1.20042)]
- [2026] **From Bureaucrats to Data Stewards: New Competency Models for the Digital Era** *International Journal of Innovative Science and Research Technology (IJISRT)* [[paper](https://doi.org/10.38124/ijisrt/26may955)]
- [2026] **HUMAN–AI TEAMING AS A NEW PARADIGM OF ENTERPRISE MANAGEMENT IN THE DIGITAL ECONOMY** *Scientific periodicals of Ukraine* [[paper](https://confmanagement-proc.kpi.ua/article/view/360822)]
- [2026] **Hybrid Work and Organisational Transformation** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003752165)]
- [2026] **Analyzing total rewards perceptions of marketing professionals through linkedin discourse: a natural language processing approach** *Scientific Reports* [[paper](https://doi.org/10.1038/s41598-026-49083-0)]
- [2026] **The Importance of Sports in Improving Health and Quality of Life** *Research Square* [[paper](https://doi.org/10.21203/rs.3.rs-9761977/v1)]
- [2026] **AN EXPLORATORY REVIEW ON DATA PRIVACY IN HRM: REVIEW LESSONS FROM SOUTH AFRICA** *Veredas do Direito Direito Ambiental e Desenvolvimento Sustentável* [[paper](https://doi.org/10.18623/rvd.v23.6089)]
- [2026] **DRY EYE SYNDROME PADA PEKERJA KANTOR: TINJAUAN PUSTAKA** *Medical Profession Journal of Lampung* [[paper](https://www.journalofmedula.com/index.php/medula/article/view/1779)]
- [2026] **MENGELOLA PERUBAHAN ORGANISASI DI ERA AI, ADAPTASI BUDAYA DAN PERILAKU** *Al-Mumtaz Jurnal Manajemen Pendidikan Islam* [[paper](https://doi.org/10.47945/al-mumtaz.v3i1.2810)]
- [2026] **Cultural immersion into maritime heritage: Our experiences in using maritime heritage to enhance wellbeing** *Internet Archaeology* [[paper](https://doi.org/10.11141/ia.73.3)]
- [2026] **Work-from-Home Culture: Productivity and Employee Satisfaction Post-COVID-19** *NOLEGEIN-Journal of Performance Management & Retention Strategies* [[paper](https://mbajournals.in/index.php/JoPMRS/article/download/1878/1706)]
- [2026] **Developing the "Recognition Function" within Organizations** *PLA Inside Out: An International Journal on Theory, Research and Practice in Prior Learning Assessment* [[paper](https://www.plaio.org/index.php/index/article/view/452)]
- [2026] **Editorial: Managing recovery and resilience in organizations: the impact of employee competence and development on firm recovery – a multidimensional conceptualization** *Management Decision* [[paper](https://doi.org/10.1108/md-05-2026-491)]
- [2026] **Editorial: Resignation and strategic retention: shaping the future workforce** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2026.1865793)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **Digital financial reporting and modern digital audit technologies in the public sector: prospects for increasing transparency and reliability of information** *Scientific Notes of Lviv University of Business and Law* [[paper](https://doi.org/10.66556/2663-0117.52.topolenko-n)]
- [2026] **Цифрова фінансова звітність і сучасні цифрові технології аудиту в державному секторі: перспективи підвищення прозорості та достовірності інформації** *Scientific Notes of Lviv University of Business and Law* [[paper](https://nzlubp.org.ua/index.php/journal/article/view/2452)]
- [2026] **Impact of Leadership on Performance Employee (A Case Study on State Bank of India)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23491590)]
- [2026] **ARTIFICIAL INTELLIGENCE ADOPTION ACROSS EMPLOYMENT SECTORS: A COMPARATIVE STUDY** *Quantum Journal of Engineering Science and Technology* [[paper](https://doi.org/10.55197/qjoest.v7i3.293)]
- [2026] **Artificial Intelligence Evolution, Emerging Risks and Safety Challenges: Implications For National Security and Society** *Central Asian Journal of Theoretical and Applied Science* [[paper](https://cajotas.casjournal.org/index.php/CAJOTAS/article/view/1754)]
- [2026] **Cybersecurity Competencies Required by Business Education Lecturers for Effective Workplace Digital Records Management in Rivers State Universities** *British Journal of Contemporary Education* [[paper](https://doi.org/10.52589/bjce-rmeuxsu3)]
- [2026] **Adoption of Voice Biometrics in the Kuwaiti Public Sector: A Study of User Perceptions and Acceptance Factors** *Journal of Computing and Data Analytics* [[paper](https://doi.org/10.68264/jcda.2026.013)]
- [2026] **AN EMPIRICAL STUDY OF FINANCIAL AWARENESS AMONG SALARIED WOMEN IN BILASPUR DIVISION** *International Journal of Economic Social Science and Management LAW* [[paper](https://doi.org/10.64751/c4hd4x88)]

[⬆ Back to top](#paper-list)

#### Survey

##### 2026

- [2026] **Types and prevalence of digital harassment from external and unknown individuals and prospective associations with employee health outcomes** *Scientific Reports* [[paper](https://doi.org/10.1038/s41598-026-72442-w)]
- [2026] **Alignment between Curriculum Content and 21st Century Skill Requirements: Perceptions of Social Sciences Graduates at Public Universities in Pakistan** *Journal of Religion and Society* [[paper](https://islamicreligious.com/index.php/Journal/article/view/558)]
- [2026] **Exploring the Relationship Between HRM, Technology and Behaviours in the Digitalised Public Sector** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003787952-2)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **When Budget Efficiency Constrains Training: Workplace Learning Adaptation in Local Government** *MUQADDIMAH Jurnal Ekonomi Manajemen Akuntansi dan Bisnis* [[paper](https://journal.insyaka.ac.id/index.php/index/article/view/2469)]
- [2026] **SlangLane Digital Sociology of Work, Remote Team Communication & Async Register Dataset (2026 — Volume 44)** *DataverseNL* [[paper](https://doi.org/10.34894/n6rbge)]
- [2026] **Work-from-home in the public sector: Perceived benefits, challenges, and policy implications** *Multidisciplinary Reviews* [[paper](https://doi.org/10.31893/multirev.2027242)]

[⬆ Back to top](#paper-list)

#### Development

##### 2026

- [2026] **Navigating Organisational Change in the Australian Public Service: Demographic Shifts and Leadership Perception** *Administrative Sciences* [[paper](https://doi.org/10.3390/admsci16090454)]

[⬆ Back to top](#paper-list)

### SME Adoption

#### Method

##### 2026

- [2026] **Underestimated Impact: How Analogue Card Games Can Foster Digital and AI Competence among SMEs** *Journal of the Association for Information Systems* [[paper](https://aisel.aisnet.org/pacis2026/di_entren/di_entren/12)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **Navigating the Infrastructure-Innovation Gap** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-2600-0955-0.ch011)]
- [2026] **Artificial intelligence as a catalyst for leadership transformation and organizational performance in Tunisian SMEs** *Leadership & Organization Development Journal* [[paper](https://doi.org/10.1108/lodj-10-2025-0887)]
- [2026] **Creative Workforces for Sustainable Futures: An Empowerment Perspective** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i8.136)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **Generative AI, Digitally Delivered Services and Global Competitiveness: Productivity, Labour Reallocation and Trade Policy** *Ovidius University Annals Economic Sciences Series* [[paper](https://doi.org/10.61801/ouaess.2026.1.44)]

[⬆ Back to top](#paper-list)

#### Evaluation

##### 2026

- [2026] **The impact and benefits of AI use in workplace tasks and firm-level value** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23385666)]

[⬆ Back to top](#paper-list)

### Security & Compliance

#### Application

##### 2026

- [2026] **CYBERFORT: A Compliance-Chain Platform Operationalising the Cyber Resilience Act for SMEs** [[paper](https://arxiv.org/abs/2610.09918)]
- [2026] **The Amplifier Effect: Human-Factor Risks of AI-Suggested Correlation and Auto-Propagation in Multi-Framework GRC Self-Assessment** [[paper](https://arxiv.org/abs/2610.07866)]
- [2026] **Correlation-Guided Fast Machine Unlearning via Hessian Analysis** [[paper](https://arxiv.org/abs/2609.12620)]
- [2026] **From Siloed Algorithms to Compliance-First Agentic Platforms: A Multi-Layered Architecture for Hospital AI Systems** [[paper](https://arxiv.org/abs/2608.06112)]
- [2026] **Lethe: How Hard Is It to Forget? A Benchmark for Federated Unlearning in Medical Imaging** [[paper](https://arxiv.org/abs/2608.01094)]
- [2026] **Zero-Knowledge Predicate Proofs Between AI Agents: A Measured, Cross-Protocol Gateway and the Source-Integrity Gap** [[paper](https://arxiv.org/abs/2608.30083)]
- [2026] **AIx4Soccer: A Unified Platform Architecture for Football Club Management and Structured Athlete Development** [[paper](https://arxiv.org/abs/2607.28531)]
- [2026] **Privacy Preserving Recommender Systems Balancing Personalization with Privacy** [[paper](https://arxiv.org/abs/2607.13328)]
- [2026] **A history of GDPR cookie banner compliance: the roles of publishers, regulators and CMPs** [[paper](https://arxiv.org/abs/2606.31485)]
- [2026] **Predicting the risk of colorectal anastomotic leak based on preoperative mapping of the blood supply of the bowel** [[paper](https://arxiv.org/abs/2606.02156)]
- [2026] **From Distorted Mirrors to Sovereign Reflections: Resisting the Grotesque Depiction of Our Digital Selves** [[paper](https://arxiv.org/abs/2606.15728)]
- [2026] **GovAI-Pipe: A Layered AI Governance Pipeline for Citizen-Facing AI in Turkey's e-Government Gateway** [[paper](https://arxiv.org/abs/2606.01417)]
- [2026] **Graph Federated Unlearning for Privacy Preservation** [[paper](https://arxiv.org/abs/2605.02297)]
- [2026] **Identification and Anonymization of Named Entities in Unstructured Information Sources for Use in Social Engineering Detection** [[paper](https://arxiv.org/abs/2604.09016)]
- [2026] **A Hardware-Anchored Privacy Middleware for PII Sharing Across Heterogeneous Embedded Consumer Devices** [[paper](https://arxiv.org/abs/2604.07839)]
- [2026] **Consent Chain Degradation in Embodied Multi-Agent Systems: Bridging the Gap Between AI Agent Governance and Robot Ethics** [[paper](https://arxiv.org/abs/2605.16300)]
- [2026] **When the Abyss Looks Back: Unveiling Evolving Dark Patterns in Cookie Consent Banners** [[paper](https://arxiv.org/abs/2603.21515)]
- [2026] **Attack by Unlearning: Unlearning-Induced Adversarial Attacks on Graph Neural Networks** [[paper](https://arxiv.org/abs/2603.18570)]
- [2026] **Does Ad-Free Mean Less Data Collection? An Empirical Study of Platform Data Practices and User Expectations** [[paper](https://arxiv.org/abs/2602.01231)]
- [2026] **ClinConNet: A Blockchain-based Dynamic Consent Management Platform for Clinical Research** [[paper](https://arxiv.org/abs/2602.02610)]
- [2026] **CUBO: Self-Contained Retrieval-Augmented Generation on Consumer Laptops 10 GB Corpora, 16 GB RAM, Single-Device Deployment** [[paper](https://arxiv.org/abs/2602.03731)] [[code](https://github.com/PaoloAstrino/CUBO)]
- [2026] **Trustworthy Blockchain-based Federated Learning for Electronic Health Records: Securing Participant Identity with Decentralized Identifiers and Verifiable Credentials** [[paper](https://arxiv.org/abs/2602.02629)]
- [2026] **Local Language Models for Context-Aware Adaptive Anonymization of Sensitive Text** [[paper](https://arxiv.org/abs/2601.14683)]
- [2026] **Federated Proximal Optimization for Privacy-Preserving Heart Disease Prediction: A Controlled Simulation Study on Non-IID Clinical Data** [[paper](https://arxiv.org/abs/2601.17183)]

##### 2025

- [2025] **Federated Learning for Pediatric Pneumonia Detection: Enabling Collaborative Diagnosis Without Sharing Patient Data** [[paper](https://arxiv.org/abs/2511.11714)]
- [2025] **Comparative Security Performance of Workday Cloud ERP Across Key Dimensions** [[paper](https://arxiv.org/abs/2511.15840)]

[⬆ Back to top](#paper-list)

### Adoption & Change

#### Method

##### 2026

- [2026] **Digital Skills Are Not Enough: Digital–Human Capability Profiles and Employee Resilience in the Changing Workplace** *Merits* [[paper](https://doi.org/10.3390/merits6040031)]
- [2026] **The Impact of AI Literacy on Employee Career Resilience and Adaptability in the Workplace** *International Journal of Versatile Research and Analysis* [[paper](https://doi.org/10.56975/ijvra.v4i10.711798)]
- [2026] **Redefining Talent Management for the Modern Service Sector** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-2600-0955-0.ch005)]
- [2026] **The Productivity Paradox in Digital Organizations as a Source of Cognitive Fatigue – Psychological and Organizational Consequences of Attention Fragmentation** [[paper](https://doi.org/10.13166/awsge/237414)]
- [2026] **Talenta Society 5.0 dan Transformasi Kerja: Tantangan dan Peluang Pengembangan Sumber Daya Manusia di Era Digital** *Journal of Business Economics and Management* [[paper](https://doi.org/10.62379/jbem.v3i2.1933)]
- [2026] **Workplace Welfare Services in Promoting Employee’s Work-Life Balance; Ecological System Perspective at PT. USSI Pinbuk Prima Software** *Glosains Jurnal Sains Global Indonesia* [[paper](https://doi.org/10.59784/glosains.v7i4.841)]
- [2026] **Software Engineering in the Agent Era From Trustworthy Change to Human Agent Software Organizations** [[paper](https://arxiv.org/abs/2609.04630)]
- [2026] **Human Side of Digital Transformation Strengthening Human Resource Management in Navigating Employee Adaptation in Intelligent Workplaces** *Jurnal Nasional Manajemen Pemasaran & SDM* [[paper](https://doi.org/10.47747/jnmpsdm.v7i3.3495)]
- [2026] **Challenges and Strategies for Employee Adaptation in Face Digital Transformation in the Shipping Industry** *Journal Research of Social Science Economics and Management* [[paper](https://doi.org/10.59141/jrssem.v6i2.1740)]
- [2026] **One Size Does Not Fit All: Digital Readiness and Differentiated Learning in Age- Diverse Hotel Front Office Teams** *International Journal of Social Science and Human Research* [[paper](https://doi.org/10.47191/ijsshr/v9-i9-24)]
- [2026] **Artificial Intelligence and the Future of Careers Transforming Jobs, Skills and Employment Opportunities in the Digital Era** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://www.srsshodhsansthan-org.cloudns.ch)]
- [2026] **PENGUATAN KOMPETENSI GURU PENDAMPING LKS MPLB MELALUI WORKSHOP ADMINISTRASI PERKANTORAN BERBASIS KEBUTUHAN INDUSTRI** *BESIRU Jurnal Pengabdian Masyarakat* [[paper](https://doi.org/10.62335/besiru.v3i9.2993)]
- [2026] **How Technological Transformation Reshapes Employment** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22833898)]
- [2026] **Talent management in the context of AI adoption: implications for talent and firms** *Personnel Review* [[paper](https://doi.org/10.1108/pr-11-2025-1289)]
- [2026] **Penguatan Keterampilan Teknis Digital Dan Literasi Digital Bagi Pekerja Migran Indonesia Di Kuala Lumpur, Malaysia** *Interdisciplinary Explorations in Research Journal* [[paper](https://doi.org/10.62976/ierj.v4i2.2036)]
- [2026] **Integrating Sustainability into Workforce Management** *NLDIMSR Innovision Journal of Management Research* [[paper](https://doi.org/10.31794/nldimsr.8.1.2024.13-32)]
- [2026] **The Future of Talent Management: AI, Analytics, and Workforce Agility** [[paper](https://doi.org/10.70593/978-93-7185-913-4)]
- [2026] **Work-Life Balance and Stress Management among Women Educators in the age of AI** *International Journal of Research in Library Science* [[paper](https://doi.org/10.26761/ijrls.12.3.2026.2140)]
- [2026] **AI-DRIVEN BURNOUT MANAGEMENT SYSTEM 4.0: A CENTRALIZED APPROACH TO REDUCING BURNOUT IN THE IT INDUSTRY USING WORK PATTERN MONITORING, AGENTIC AI, TEMPORAL MACHINE LEARNING, RETRIEVAL-AUGMENTED GENERATION, DIGITAL TWINS, AND COUNTERFACTUAL REASONING** *INTERNATIONAL JOURNAL OF MANAGEMENT* [[paper](https://doi.org/10.34218/ijm_17_04_009)]
- [2026] **AI-Enabled Gig Platforms and Workforce Management: Implications for Skill Development, Worker Protection, and Sustainable Employment in India** *International Journal For Multidisciplinary Research* [[paper](https://doi.org/10.36948/ijfmr.2026.v08i04.86086)]
- [2026] **Workplace health coaching for chronic disease management in a maritime industry workforce: a mixed-methods evaluation** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1760520)]
- [2026] **From digital eye strain to tech neck: Homoeopathic management of screen-related and ergonomic disorders** *International Journal of Homoeopathic Sciences* [[paper](https://doi.org/10.33545/26164485.2026.v10.i7.a.2958)]
- [2026] **Intercultural Human Resource Management Strategies for Organizations** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21709575)]
- [2026] **ROLE OF ARTIFICIAL INTELLIGENCE IN MODERN HUMAN RESOURCE MANAGEMENT** *Journal of Science Engineering Technology and Management Sciences* [[paper](https://doi.org/10.64771/jsetms.2026.v03.i07.pp512-519)]
- [2026] **ROLE OF ARTIFICIAL INTELLIGENCE IN TRANSFORMING EMPLOYEE ENGAGEMENT AND DECISION-MAKING IN HUMAN RESOURCE MANAGEMENT** *ShodhPrabandhan Journal of Management Studies* [[paper](https://doi.org/10.29121/shodhprabandhan.v3.i2.2026.117)]
- [2026] **Strategi Kompensasi Dan Tunjangan Berbasis Fleksibilitas Dalam Meningkatkan Retensi Karyawan Generasi Z Pada Era Transformasi Digital** *Journal of Business Economics and Management* [[paper](https://jurnal.globalscients.com/index.php/jbem/article/view/1676)]
- [2026] **Penguatan Kompetensi Digital Dan Kemampuan Berpikir Solutif Bagi Pemuda Di Perum Griya Sindang Sejahtera** *Jurnal Pengabdian Kepada Masyarakat Multidisiplin.* [[paper](https://sihojurnal.com/index.php/jupengen/article/view/2152)]
- [2026] **The Gen Z Effect: Bagaimana Generasi Baru Mengubah Paradigma Manajemen Modern** *Jurnal Manuhara Pusat Penelitian Ilmu Manajemen dan Bisnis* [[paper](https://doi.org/10.61132/manuhara.v4i3.2598)]
- [2026] **Wykorzystanie narzędzi informatycznych w obszarze BHP w polskich zakładach pracy – wyniki badania ankietowego Authors** *Studia i Materiały Wydziału Zarządzania UW* [[paper](https://doi.org/10.7172/1733-9758.2026.44.4)]
- [2026] **Overcoming Challenges in Agile and DevOps Integration: A Qualitative Study** [[paper](https://arxiv.org/abs/2606.01676)]
- [2026] **Gendered Impacts of AI-Driven Work Platforms: Income Security, Digital Skills, and Workplace Voice** *Social Trends and Policy Review* [[paper](https://socialtrendsreview.com/index.php/index/article/view/63)]
- [2026] **REIMAGINING ORGANIZATIONAL DEVELOPMENT IN THE AI-DRIVEN WORKPLACE: CHALLENGES AND STRATEGIC OPPORTUNITIES** *ACCENT JOURNAL OF  ECONOMICS ECOLOGY  & ENGINEERING* [[paper](https://ajeee.co.in/index.php/ajeee/article/download/6635/5378)]
- [2026] **The impact of digitalization and organizational changes on older workers' insecurity in the finance sector in Sweden and Czechia** *Frontiers in Sociology* [[paper](https://doi.org/10.3389/fsoc.2026.1835265)]
- [2026] **The Importance of Education for Successful Digital Transformation of Work** *Review of Socio-Economic Perspectives* [[paper](https://doi.org/10.2478/rsep-2026-0004)]
- [2026] **O uso da tecnologia na gestão de pessoas: avanços e desafios.** *Revista fisio&terapia.* [[paper](https://doi.org/10.69849/x7pr2p98)]
- [2026] **DETERMINAN USE BEHAVIOR DALAM ADOPSI SISTEM INFORMASI MANAJEMEN: IMPLIKASI PEDAGOGIS DALAM PEMBELAJARAN TEKNOLOGI PERKANTORAN** *EDUTECH Jurnal Inovasi Pendidikan Berbantuan Teknologi* [[paper](https://doi.org/10.51878/edutech.v6i3.12131)]
- [2026] **HUMAN RESOURCE PRACTICES AND EMPLOYEE ENGAGEMENT IN DIGITALLY TRANSFORMING WORK ENVIRONMENTS: PERSPECTIVES ON DIGITAL CULTURE, ETHICS, AND SOCIETAL CHANGE** *Research* [[paper](https://doi.org/10.5281/zenodo.20379339)]
- [2026] **ARTIFICIAL INTELLIGENCE, GIG WORK AND WORKPLACE CULTURE: RETHINKING TALENT ACQUISITION IN A TRANSFORMING SOCIETY** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20341259)]
- [2026] **Employee Adaptation To Artificial Intelligence In The Workplace: A Phenomenological Study In South Sulawesi Companies** *Economics and Business Journal (ECBIS)* [[paper](https://ecbis.net/index.php/go/article/view/379)]
- [2026] **Wellbeing, Energy, and Work Functioning Among Autistic and ADHD Employees: A Mixed-Methods Longitudinal Study of the Hybrid Digital Support Tool Brain in Hand** [[paper](https://doi.org/10.31234/osf.io/gd6rt_v1)]
- [2026] **Urgensi Penerapan Manajemen SDM Pada Generasi Z Dalam Meningkatkan Karier di Masa Depan** *Jurnal Bisnis Dan Kajian Strategi Manajemen* [[paper](https://doi.org/10.35308/jbksm.v10i1.15265)]

##### 2025

- [2025] **The Impact of Artificial Intelligence on Enterprise Decision-Making Process** [[paper](https://arxiv.org/abs/2512.02048)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **THE IMPACT OF DIGITAL WORKPLACE, DIGITAL FATIGUE, DIGITAL MINIMALISM ON EMPLOYEE PRODUCTIVITY IN THE BANKING INDUSTRY IN GREATER JAKARTA** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23120060)]
- [2026] **AI-ENABLED HUMAN RESOURCE MANAGEMENT PRACTICES AND EMPLOYEE PERFORMANCE: THE MEDIATING ROLE OF EMPLOYEE ADAPTABILITY IN THE DIGITAL WORKPLACE** *Acta Innovations* [[paper](https://doi.org/10.62441/actainnovations.vi.2137)]
- [2026] **Historical Origins of Workplace Monitoring: From Ancient Oversight to Digital Taylorism** *Z Problematyki Prawa Pracy i Polityki Socjalnej* [[paper](https://doi.org/10.31261/zpppips.2026.24.05)]
- [2026] **Remote Work and the Changing Organization: Management, Productivity and Employee Well-Being in the Post-Pandemic Workplace** *Jurisocial Journal of Social Sciences* [[paper](https://doi.org/10.68740/jjss22)]
- [2026] **The impact of Generation Z on the Workplace: A scoping review** *SA Journal of Human Resource Management* [[paper](https://doi.org/10.4102/sajhrm.v24i0.3670)]
- [2026] **Ethical Labour and Workforce Transformation in the Digital Economy** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-2600-4609-8.ch004)]
- [2026] **Adaptive FM strategies in small and medium enterprises (SMEs): ensuring workplace continuity during business interruptions** *Journal of Facilities Management* [[paper](https://doi.org/10.1108/jfm-10-2025-0162)]
- [2026] **Talent Management and Work Design in an Artificial Intelligence-Enabled Future** *UJ Press eBooks* [[paper](https://doi.org/10.64449/9781997499084-02)]
- [2026] **Career transition as an assemblage of learning : a multiple case study of Korean millennials who left socially desirable workplaces** *cIRcle (University of British Columbia)* [[paper](https://hdl.handle.net/2429/95740)]
- [2026] **Digital HRM Transformation and Employee Well-Being: A Thematic Review of Work–Life Balance and Emotional Intelligence** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23118244)]
- [2026] **THE APPLICATION OF ARTIFICIAL INTELLIGENCE IN HUMAN RESOURCES MANAGEMENT, THEORETICAL PERSPECTIVE** *Journal of Baku Engineering University Economics and Administration* [[paper](https://doi.org/10.30546/2521-6341.2025.01.021)]
- [2026] **Industry Expectations And Curriculum Development In Higher Education: Bridging The Gap Between Academic Learning And Workplace Requirements** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23119817)]
- [2026] **Digital-Based Career Counseling in the Era of Revolusi Industri 4.0 : Systematic Literature Review** *Jurnal Ragam Pengabdian* [[paper](https://doi.org/10.62710/j1r6x250)]
- [2026] **Navigating boundaries: daily boundary dynamics and work–life balance among digital nomads: a 9-day diary study** *BMC Public Health* [[paper](https://doi.org/10.1186/s12889-026-29345-2)]
- [2026] **Leading from the middle: how mid-level managers shape digital strategy and innovation** *Strategy and Leadership* [[paper](https://doi.org/10.1108/sl-07-2026-0370)]
- [2026] **IMPROVING THE PERSONNEL TRAINING MECHANISM IN JOINT-STOCK COMPANIES UNDER DIGITAL TRANSFORMATION: A COMPETENCY-BASED AND SKILLS-FIRST APPROACH** *IQRO* [[paper](https://wordlyknowledge.uz/index.php/iqro/article/view/9423)]
- [2026] **WHEN THE CHAINS CHANGE SUBSTRATE: Formal Liberty, Usable Lawful Liberty, and the Changing Architecture of Constraint** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23137137)]
- [2026] **When Silence Speaks: Exploring the Career, Climate, and Care Dimensions of Silent Quitting Behaviors of Professional Women in the Digital Age** *Emerald Group Publishing Limited eBooks* [[paper](https://doi.org/10.1108/978-1-80686-545-120261010)]
- [2026] **Strategi Pengembangan Kompetensi Talenta dalam Menghadapi Persaingan Global** *Maeswara Jurnal Riset Ilmu Manajemen dan Kewirausahaan* [[paper](https://doi.org/10.61132/maeswara.v4i5.2956)]
- [2026] **Psychological Safety and Workforce Readiness in Higher Education: The Mediating Role of Work Engagement** *Archives des sciences a multidisciplinary journal* [[paper](https://doi.org/10.68304/as/76408)]
- [2026] **Digital Workplace Technologies and Organizational Structure at HCL Company** *International Journal of Data Science and IoT Management System* [[paper](https://doi.org/10.64751/ijdim.2026.v5.n3.1315)]
- [2026] **LEADERSHIP COMMUNICATION IN DIGITAL AND AI-ENABLED WORKPLACES: A SCOPING REVIEW** *Journal of Information System and Technology Management* [[paper](https://doi.org/10.35631/jistm.1144031)]
- [2026] **Competency Gaps between the 2004 Office Technology and Management Curriculum and Contemporary Workplace Requirements** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22870650)]
- [2026] **Artificial Intelligence Anxiety and Employee Performance in the Digital Workplace: The Mediating Role of Job Insecurity** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22763317)]
- [2026] **Digital Transformation Strategies in the Project Management Office: Navigating Organizational Change** *ScholarWorks (Walden University)* [[paper](https://scholarworks.waldenu.edu/dissertations/20819)]
- [2026] **AI-Augmented Human Resource Decision Making: Predictive Talent Analytics, Employee Well-Being, and Organizational Agility in the Digital Workplace** *Computer and decision making.* [[paper](https://doi.org/10.1922/comdem.v3i4s.18715)]
- [2026] **Intergenerational Diversity in the Workplace: An Empirical Review of Work Values and Conflict Management Approaches in Nigerian Private Organisations** *IIARD INTERNATIONAL JOURNAL OF ECONOMICS AND BUSINESS MANAGEMENT* [[paper](https://doi.org/10.56201/ijebm.vol.11.no10.2025.pg233.240)]
- [2026] **Human resource digital risk management and sustainable work–life balance in digital work environments: examining the sequential roles of mindful technology use and techno-boundary crafting** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1889460)]
- [2026] **Changing the model of workplace e-learning : a platform to facilitate autonomous social e-learning for adult learners : Innovation report** *Warwick Research Archive Portal (University of Warwick)* [[paper](https://wrap.warwick.ac.uk/59108/2/WRAP_THESIS_Betts_2013.pdf)]
- [2026] **The Impact of Digitalization of Financial and Accounting Processes on the Efficiency of an Enterprise** *EUROPEAN RESEARCH STUDIES JOURNAL* [[paper](https://doi.org/10.35808/ersj/4452)]
- [2026] **DIGITAL TOOLS AND EMPLOYEE WELL-BEING IN THE MODERN WORKFORCE: A THEMATIC REVIEW** *Journal of Information System and Technology Management* [[paper](https://doi.org/10.35631/jistm.1144028)]
- [2026] **Vectors of transformation of the legal nature of labor relations in the digital environment in Ukraine** *Visnik Nacional’nogo universitetu «Lvivska politehnika» Seria Uridicni nauki* [[paper](https://doi.org/10.23939/law2026.51.189)]
- [2026] **DIGITALIZATION OF PROFESSIONAL LIFE AND THE TRANSFORMATION OF SOCIAL CONNECTEDNESS AMONG URBAN KNOWLEDGE WORKERS** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22694982)]
- [2026] **Sociology of Work and Changing Employment Relationships** *Recent Issues In Human Resource Management* [[paper](https://crcltd.org/index.php/RIHRM/article/view/104)]
- [2026] **Assessment of Challenges Related to AI-Driven Digital Transformation for Supply Chain Performance in Context of Circular Economy** *i-manager s Journal on Computer Science* [[paper](https://doi.org/10.26634/jcom.14.2.1449)]
- [2026] **EDUCATIONAL MANAGEMENT AS A STRATEGIC CHOICE FOR CADRE DEVELOPMENT TO REVITALIZE TRADE UNION ORGANIZATIONS: A CASE STUDY OF ASPEK INDONESIA** *SOSIOEDUKASI JURNAL ILMIAH ILMU PENDIDIKAN DAN SOSIAL* [[paper](https://doi.org/10.36526/sosioedukasi.v15i3.9413)]
- [2026] **How Does a Digital Marketing Course in Indore Help Build Practical Career Skills?** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22882500)]
- [2026] **HR Technology and The Future of Work: Implications for HR Leaders** *WORLD JOURNAL OF INNOVATION AND MODERN TECHNOLOGY* [[paper](https://doi.org/10.56201/wjimt.v10.no3.2026.pg154.162)]
- [2026] **Reframing Human Resource Leadership Through Human-Centred AI** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-3373-9599-9.ch009)]
- [2026] **The Future of Work. An Interdisciplinary Approach** *Peter Lang eBooks* [[paper](https://doi.org/10.3726/b23977)]
- [2026] **Bridging the Digital Divide: Reimagining HRM Education for an AI-Driven Workplace** *TEM Journal* [[paper](https://doi.org/10.18421/tem153-80)]
- [2026] **Digitalisation as a driver of psychosocial risks in post-pandemic workplaces with implications for psychosocial risk management** *Proceedings of the Estonian Academy of Sciences* [[paper](https://doi.org/10.3176/proc.2026.3.08)]
- [2026] **The Dynamics of Interaction and the Meaning of Presence in a Digital Work Environment: Efforts to Maintain Human Values in the Modern Workplace** *International Journal Administration Business and Organization* [[paper](https://doi.org/10.61242/ijabo.26.638)]
- [2026] **Experience-First AI Transformation: A Practitioner-Scholar Framework for the AI-Native Digital Workplace** *OSF Preprints (OSF Preprints)* [[paper](https://osf.io/zbw5m)]
- [2026] **Workplace-Based Multicomponent Weight Management Interventions for Employees with Overweight or Obesity: A Systematic Review** *한국생활환경학회지* [[paper](https://doi.org/10.21086/ksles.2026.8.33.4.454)]
- [2026] **The empowering impact of a strong sense of belonging in the workplace: A conceptual study** *International journal of applied research* [[paper](https://doi.org/10.22271/allresearch.2026.v12.i8c.14028)]
- [2026] **Digital Connectivity versus Human Connectivity: A Multidimensional Study of Changing Interpersonal Communication Skills in the Digital Era** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21898742)]
- [2026] **Competency Gaps among Graduates of Islamic Religious Higher Education Institutions in the Digital Era: Stakeholder Perspectives and Implications for Curriculum Management** *Management of Education Jurnal Manajemen Pendidikan Islam* [[paper](https://doi.org/10.18592/moe.v12i2.20429)]
- [2026] **Gen Z Workplace Expectations and Organizational Culture: A Thematic Analysis and Review of Contemporary Research** *International Journal of Global Innovations and Modern Research* [[paper](https://doi.org/10.66304/ijgimr.2026.v1i2.04)]
- [2026] **IMPACT OF INNOVATION TECHNOLOGY IN HUMAN RESOURCE MANAGEMENT** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennurv6b3318c8)]
- [2026] **Transformation of Office Facilities and Infrastructure Role in the Digital Era** *International Journal Administration Business and Organization* [[paper](https://doi.org/10.61242/ijabo.26.669)]
- [2026] **MODERN TRENDS AND INNOVATIONS IN HUMAN RESOURCE MANAGEMENT** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennurv6b3318)]
- [2026] **Dynamics of Employee Adaptation, Anxiety, and Role Change Under AI Integration in Indonesia** *International Journal of Applied Business and International Management* [[paper](https://doi.org/10.32535/ijabim.v11i2.4658)]
- [2026] **Analysis of Employer Branding and Digital HR Practices on Employee Performance Agility Through Employee Engagement** *International Journal of Management Economic and Accounting* [[paper](https://journal.ysmk.or.id/index.php/index/article/view/797)]
- [2026] **Training Strategies for Employees to Use Electronic Human Resource Management Systems** *ScholarWorks (Walden University)* [[paper](https://scholarworks.waldenu.edu/dissertations/20575)]
- [2026] **From Digital Storytelling to Critical Consciousness: Adapting Critical Pedagogy Through Medical Memes in a Hierarchical Context** *Teaching and Learning in Medicine* [[paper](https://doi.org/10.1080/10401334.2026.2711096)]
- [2026] **Scaling Human Capabilities: A Learning Architecture for Knowledge Management** *European Conference on Knowledge Management* [[paper](https://doi.org/10.34190/eckm.27.2.5224)]
- [2026] **Sustainable Workforce Management Through Green HRM: Practices, Outcomes, and Challenges** *NLDIMSR Innovision Journal of Management Research* [[paper](https://doi.org/10.31794/nldimsr.8.2.2024.47-61)]
- [2026] **LEADING WITHOUT A ROOM: ALGORITHMIC MANAGEMENT AND THE FUTURE OF LABOUR LAW IN INDIA'S GIG ECONOMY** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21851668)]
- [2026] **ЦИФРОВАЯ ЗРЕЛОСТЬ ОРГАНИЗАЦИОННОЙ КУЛЬТУРЫ ПРЕДПРИЯТИЯ: РАЗРАБОТКА МОДЕЛИ КОМПЛЕКСНОЙ ОЦЕНКИ** *Iqtisodiy taraqqiyot va tahlil* [[paper](https://doi.org/10.60078/2992-877x-2026-vol4-iss8-pp258-264)]
- [2026] **Swedish unions’ strategies in the digitalised world of work: The importance of institutional context and power resources** *Economic and Industrial Democracy* [[paper](https://doi.org/10.1177/0143831x261481316)]
- [2026] **Advanced Administrative Strategies and Commercial Growth Frameworks in Modern Business Environments** *The American Journal of Management and Economics Innovations* [[paper](https://theamericanjournals.com/index.php/tajmei/article/view/8251)]
- [2026] **Концепція гнучкої організації праці в цифрових компаніях** *Scientific Notes of Lviv University of Business and Law* [[paper](https://nzlubp.org.ua/index.php/journal/article/view/2275)]
- [2026] **TRAINERS’ PERCEPTIONS OF THE MOST IMPORTANT SOFT SKILLS FOR HIGH SCHOOL STUDENTS** *Tudásmenedzsment* [[paper](https://doi.org/10.15170/tm.2026.27.k2.6)]
- [2026] **การบรหารและการจดการศกษาเชงพทธในยคพลกผน เพอการขบเคลอนองคกรแหงความสข** *Interdisciplinary Journal of Administration and Business* [[paper](https://so09.tci-thaijo.org/index.php/interad/article/view/9706)]
- [2026] **TANTANGAN KEPEMIMPINAN PENDIDIKAN DI ERA ARTIFICIAL INTELLIGENCE: PERSPEKTIF PERILAKU ORGANISASI** *Jurnal Manajemen Pendidikan* [[paper](https://ejurnal.stkip-pessel.ac.id/index.php/jmp/article/view/3365)]
- [2026] **COMMERCE 5.0: MANAGEMENT OF BUSINESS IN THE DIGITAL ERA** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennur3244)]
- [2026] **The role of Human Resource Management in the Prevention and Mitigation of Work-Related Stress in the Digital Era** *Harokopio University* [[paper](https://doi.org/10.26258/heal.hua.7697)]
- [2026] **Business, Society and Change: Contemporary Issues in Humanities, Commerce and Management** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21704030)]
- [2026] **Navigating The AI-Augmented Workplace: How Digital Leadership and The AMO Framework Impact Job Insecurity and Human-Algorithm Symbiosis** *Fundamental and Applied Management Journal* [[paper](https://doi.org/10.66314/famj.v4i2.788)]
- [2026] **THE PURPOSE-DRIVEN SHIFT: A THEORETICAL OVERVIEW ON GENERATION Z WORKPLACE DYNAMICS AND HUMAN RESOURCE ADAPTABILITY** *NOLEGEIN Journal of Human Resource Management & Development* [[paper](https://mbajournals.in/index.php/JoHRMD/article/view/1959)]
- [2026] **# "WOMEN'S LEADERSHIP AND CAREER ADVANCEMENT: A Comprehensive Scientific Framework for Empowerment, Confidence Building, Professional Development, and Gender Equity in the Modern Workplace" ---** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21719590)]
- [2026] **Linking Presenteeism Climate and Digital Mindsets to Employee Well-Being in Public Administration** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.17176abstract)]
- [2026] **Agricultural inclusive digital transformation: enhancing neurodiversity through organizational practices and technology** *Journal of Organizational Effectiveness People and Performance* [[paper](https://doi.org/10.1108/joepp-07-2025-0612)]
- [2026] **“We Are In This Together”: Role-Differentiated Experiences of Transition Management** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.21138poster)]
- [2026] **Adaptation and feasibility of a digital psychological intervention for UK nursing professionals’ psychological well-being** *Nottingham ePrints (University of Nottingham)* [[paper](https://repository.nottingham.ac.uk/handle/123456789/67437)]
- [2026] **Long-Term Associations of a Mobile-Based Chronic Disease Management Program With Employee Health: Four-Year Retrospective Cohort Study** *Journal of Medical Internet Research* [[paper](https://doi.org/10.2196/82822)]
- [2026] **TRANSFORMASI DIGITAL DALAM PENDIDIKAN ISLAM NONFORMAL DI LINGKUNGAN PERKANTORAN BUMN WIKA : INTEGRASI ARTIFICIAL INTELLIGENCE, BIG DATA, DAN PEMBELAJARAN IMERSIF MENUJU INDONESIA EMAS 2045** *Pendas Jurnal Ilmiah Pendidikan Dasar* [[paper](https://journal.unpas.ac.id/index.php/pendas/article/view/55905)]
- [2026] **การบรหารทรพยากรมนษยในศตวรรษท 21** *Journal of Buddhist Education and Research (JBER)* [[paper](https://so06.tci-thaijo.org/index.php/jber/article/view/296367)]
- [2026] **An Analysis of Corporate Training Psychology and the System of Training Psychological Techniques** *Education insights.* [[paper](https://soapubs.com/index.php/EI/article/view/2556)]
- [2026] **Calidad de vida, bienestar y felicidad en el trabajo: una revisión sistemática de la literatura científica 2011-2025** *POLIANTEA* [[paper](https://doi.org/10.15765/fkjfp059)]
- [2026] **Organizing work processes in the workplace amid a company’s digital transformation abstract** *Economic Herald of SHEI USUCT* [[paper](https://doi.org/10.32434/2415-3974-2026-23-1-257-265)]
- [2026] **Rethinking Workplace Training: Artificial Intelligence, Digital Ecosystems, and Emerging Talent Development Practices** *Digital Education Review* [[paper](https://doi.org/10.1344/der.2026.49.79-94)]
- [2026] **DIGITAL TRANSFORMATION AND ORGANIZATIONAL CULTURE IN HUMAN RESOURCE MANAGEMENT: DRIVERS OF WORKFORCE EVOLUTION** *Research* [[paper](https://doi.org/10.5281/zenodo.21707552)]
- [2026] **Integration technology into health care: a scoping review of digital interventions for adult obesity management** *BMC Public Health* [[paper](https://doi.org/10.1186/s12889-026-27904-1)]
- [2026] **Educational Institutions Strategies to Coping with Workplace Challenges: A Study of Current Practices** *IOSR Journal of Business and Management* [[paper](https://doi.org/10.9790/487x-2806016070)]
- [2026] **Guest editorial: Digital technologies and mental health management: opportunities and challenges** *Industrial Management & Data Systems* [[paper](https://doi.org/10.1108/imds-07-2026-998)]
- [2026] **Psychological Well-Being and Employee Performance in IT Organizations: The Mediating Role of Workplace Stress and Anxiety** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20938323)]
- [2026] **Methodological basis for the development of a digital twin of an employee of the company** *Russian Journal of Industrial Economics* [[paper](https://doi.org/10.17073/2072-1633-2026-2-1548)]
- [2026] **Digital transformation and its influence on employee engagement** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21319063)]
- [2026] **STRATEGI PENINGKATKAN KETERAMPILAN PUSTAKAWAN DALAM MENGHADAPI DISRUPSI DIGITAL** *Jurnal Manajemen Pendidikan* [[paper](https://ejurnal.stkip-pessel.ac.id/index.php/jmp/article/view/3481)]
- [2026] **Determinants of Employee Work Motivation During Digital Banking Transformation in Vietnam** *International Journal of Innovative Science and Research Technology (IJISRT)* [[paper](https://doi.org/10.38124/ijisrt/26jun341)]
- [2026] **From Theory to Practice: Examining the Curriculum-Industry Gap Through a Digital Marketing Internship in International Education** *Jurnal Multidisiplin West Science* [[paper](https://doi.org/10.58812/jmws.v5i06.3470)]
- [2026] **NEW HORIZONS IN HUMAN RESOURCE MANAGEMENT AND ORGANIZATIONAL DEVELOPMENT – VOLUME 6 2026 S1018B4** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennurnhhrv6b4)]
- [2026] **NEW HORIZONS IN HUMAN RESOURCE MANAGEMENT AND ORGANIZATIONAL DEVELOPMENT – VOLUME 6 2026 S1018B3** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennurnhhrv6b3)]
- [2026] **NEW HORIZONS IN HUMAN RESOURCE MANAGEMENT AND ORGANIZATIONAL DEVELOPMENT – VOLUME 6 2026 S1018B1** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennurnhhrv6b1)]
- [2026] **NEW HORIZONS IN HUMAN RESOURCE MANAGEMENT AND ORGANIZATIONAL DEVELOPMENT – VOLUME 6 2026 S1018B2** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennurnhhrv6b2)]
- [2026] **Technological Change, Work and Power: A Framework for Analyzing how Actors and Institutions Distribute Power in the AI-Driven Technological Change Process** *Work and Occupations* [[paper](https://doi.org/10.1177/07308884261457838)]
- [2026] **Blockchain and Data Security Management in Financial Services: A Strategic Evaluation with the COBIT 2019 Framework** *Journal of Digital Business and Innovation Management* [[paper](https://doi.org/10.26740/jdbim.v5i1.67033)]
- [2026] **Implementasi Smart HRM dan pengukuran digital Employee-Human Development Index untuk kesejahteraan karyawan** *Community Empowerment Journal* [[paper](https://doi.org/10.61251/cej.v4i2.386)]
- [2026] **The Effect Of Digital Hr Transformation And Work Flexibility On Employee Performance Through Employee Engagement With The Moderating Role Of Employee Well-Being In The Hospitality Sector** *JHSS (JOURNAL OF HUMANITIES AND SOCIAL STUDIES)* [[paper](https://doi.org/10.33751/jhss.v10i2.157)]
- [2026] **A Study on Management of Industrial Dispute & Collective Bargaining Process in the Era of Artificial Intelligence (AI)** *International Journal of Science Strategic Management and Technology* [[paper](https://doi.org/10.55041/ijsmt.v2i6.116)]
- [2026] **Impact of Gamification in Behaviour Change Intervention: A Randomised Controlled Trial with YuLife’s Health and Wellbeing App** *medRxiv* [[paper](https://doi.org/10.64898/2026.05.31.26354543)]
- [2026] **Accidentally Visible and Unmuted** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003563662-11)]
- [2026] **HRM APPROACHES FOR AGILITY AT ICICI PRUDENTIAL AMC** *IJSIT* [[paper](https://doi.org/10.5281/zenodo.20483013)]
- [2026] **AI-Driven Personalised Marketing Tools and Their Influence on Work-Life Balance and Technostress among Marketing Professionals: A Theoretical Perspective** *International Journal on Science and Technology* [[paper](https://doi.org/10.71097/ijsat.v17.i2.11276)]
- [2026] **Foundation of Organizational Behaviour: Understanding People and Performance by Dr. Rahul Pathak, Ms. Nishita Patel, and Mr. Vipul Sharma** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20926981)]
- [2026] **Impact of Remote Working on Employee Productivity** *Iconic Research and Engineering Journals* [[paper](https://doi.org/10.64388/irev9i12-1719276)]
- [2026] **Beyond the scale: exploring the role of social media engagement in enhancing adherence within a workplace weight management program** *Proceedings of The Nutrition Society* [[paper](https://doi.org/10.1017/s0029665126102638)]
- [2026] **MANAGERIAL LEADERSHIP QUALITIES AS A DETERMINANT OF CONFLICT MANAGEMENT IN THE MODERN DIGITAL AND BEHAVIORAL BUSINESS ENVIRONMENT** *Proceedings of Scientific Works of Cherkasy State Technological University Series Economic Sciences* [[paper](https://doi.org/10.24025/2306-4420.79(2).2026.358468)]
- [2026] **Inclusive algorithmic work design: the moderating role of DEI interventions and diversity-supportive culture in AI-driven workplace transformation** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2026.1833850)]
- [2026] **Strategic silence and concrete corrective actions in employer brand image recovery : Brands amid workplace well-being controversies** *UTUPub (University of Turku)* [[paper](https://www.utupub.fi/handle/11111/60836)]
- [2026] **A Study on the Impact of Training and Development Practices on Employee Performance in Digital Marketing at Hirehappi, Bengaluru** *International Journal of Science Strategic Management and Technology* [[paper](https://doi.org/10.55041/ijsmt.v2i5.427)]
- [2026] **From Static Fit to Dynamic Alignment: The Emergence and Evolution of HR Ecosystems in Fragmented Workplaces** *Human Resource Management* [[paper](https://doi.org/10.1002/hrm.70076)]
- [2026] **Transformasi Digital dan Manajemen SDM di Masa Depan Kerja: Tinjauan Sistematis terhadap Inklusivitas dan Keberlanjutan** *MASMAN Master Manajemen* [[paper](https://doi.org/10.59603/masman.v4i2.1341)]
- [2026] **DECOUPLED CONTROL: ALGORITHMIC MANAGEMENT AND LABOUR GOVERNANCE IN THE INDIAN PLATFORM ECONOMY** *ShodhKosh Journal of Visual and Performing Arts* [[paper](https://doi.org/10.29121/shodhkosh.v6.i1.2025.9079)]
- [2026] **HUMAN RESOURCE MANAGEMENT TOOLS IN CONSTRUCTION COMPANIES WITHIN THE FRAMEWORK OF SUSTAINABLE DEVELOPMENT** *Economic scope* [[paper](https://doi.org/10.30838/ep.212.263-270)]
- [2026] **"Why Hospitality Education Is Evolving Fast in 2026: Choosing the Right Hotel Management Program for a Global Career"** *IEEE DataPort* [[paper](https://doi.org/10.21227/hg3n-vg46)]
- [2026] **AI IN HUMAN RESOURCES: A SOCIOLOGICAL ANALYSIS OF POWER, INEQUALITY, AND ORGANIZATIONAL CHANGE** *DOAJ (DOAJ: Directory of Open Access Journals)* [[paper](https://doaj.org/article/c903223ffc164ce7bd7b3481c765007e)]
- [2026] **ЛІДЕРСЬКІ ЯКОСТІ МЕНЕДЖЕРА ЯК ФАКТОР УПРАВЛІННЯ КОНФЛІКТАМИ У СУЧАСНОМУ ЦИФРОВОМУ ТА ПОВЕДІНКОВОМУ БІЗНЕС-СЕРЕДОВИЩІ** *Scientific periodicals of Ukraine* [[paper](https://ven.chdtu.edu.ua/article/view/358468)]
- [2026] **Social Issues in Nepal (2018–2026) Affecting Human Resource Practices at The Organizational and Societal Level** *SADGAMAYA.* [[paper](https://doi.org/10.3126/sadgamaya.v3i1.94075)]
- [2026] **Shifting of HR Functions: From Traditional to Post Modern Concept in Hospitality Industry in Nepal** [[paper](https://doi.org/10.33774/coe-2026-3ghkn)]
- [2026] **IMPLEMENTASI MANAJEMEN PENDIDIKAN DALAM PENGELOLAAN PROGRAM TEACHING FACTORY KOLABORASI DI SMK MUHAMMADIYAH 2 PEKANBARU** *Pendas Jurnal Ilmiah Pendidikan Dasar* [[paper](https://journal.unpas.ac.id/index.php/pendas/article/view/46733)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **Digital Acumen as a Workforce Capability: A Systematic Review of Digital Learning Activities in Accounting Education** *International Journal of Applied Research in Business and Management* [[paper](https://doi.org/10.51137/wrp.ijarbm.929)]
- [2026] **Business Transformation In Emerging Markets: Insights From Vietnam** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21820879)]
- [2026] **Network FM: An essential technology in real estate and facility management** *Corporate real estate journal* [[paper](https://doi.org/10.69554/hfms8378)]
- [2026] **Competing strain and resource pathways linking AI-enabled work systems to employee wellbeing.** *MED* [[paper](https://doi.org/10.3389/frai.2026.1922774)]
- [2026] **Assessing Feasibility and Readiness for 3D Printing Integration in Prosthetics and Orthotics: A Cross-Sectional Study** *PMC* [[paper](https://europepmc.org/article/pmc/PMC13664817)]
- [2026] **Are all digital hoarding behavior alike? Uncovering the pathways to digital hoarding behavior in the workplace.** *MED* [[paper](https://doi.org/10.3389/fpsyg.2026.1823038)]
- [2026] **Adoption of App-Based Peer Support by Canadian Health Care Providers: Mixed Methods Organizational Implementation Study.** *MED* [[paper](https://doi.org/10.2196/85658)]
- [2026] **Evaluating Workforce Readiness for Digital Transformation in the Automotive Industry: The Case of North Africa** *PPR* [[paper](https://doi.org/10.21203/rs.3.rs-11183699/v1)]
- [2026] **Digital intelligence in dental technology education: curriculum and practical teaching reform.** *MED* [[paper](https://doi.org/10.3389/fmed.2026.1912754)]
- [2026] **Competency-based medical education and entrustable professional activities in dental education: Global perspectives and implications for Taiwan.** *MED* [[paper](https://doi.org/10.1016/j.jds.2025.07.3473)]
- [2026] **e-Learning, Distance Education, and Virtual and Augmented Reality in Orthopedic Training: European Cross-Sectional Survey of Trainee Acceptance Guided by the Technology Acceptance Model and Unified Theory of Acceptance and Use of Technology.** *MED* [[paper](https://doi.org/10.2196/79418)]
- [2026] **From Tool to Social Actor: A Systematic Review of the Psychological Mechanisms Through Which Conversational AI Reshapes the Employee Experience.** *MED* [[paper](https://doi.org/10.3390/bs16091704)]
- [2026] **Attitudinal openness to AI as supervisor or colleague/subordinate in Japan: the role of advanced digital technology familiarity.** *MED* [[paper](https://doi.org/10.3389/frai.2026.1920376)]

[⬆ Back to top](#paper-list)

#### Survey

##### 2026

- [2026] **Remote Work, Employer Branding, Employee Retention, Human Resource Transformation, Workplace Flexibility.** *International Journal of Science Strategic Management and Technology* [[paper](https://doi.org/10.55041/ijsmt.v2i5.604)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **A Study on the Impact Industrial Relations Practices on Employee Productivity in Manufacturing Unit** *INTERANTIONAL JOURNAL OF SCIENTIFIC RESEARCH IN ENGINEERING AND MANAGEMENT* [[paper](https://doi.org/10.55041/ijsrem67197)]
- [2026] **Digital Transformation in Human Resource Management: A Study Among HR Professionals in the Information Technology Sector** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22123248)]
- [2026] **The Effect of Changes and Dynamics in the Digital Environment on the Work Readiness of Management Students, Faculty of Economics and Business, Universitas Muhammadiyah Makassar in the Era of Digital Transformation** *Journal Social Society.* [[paper](https://doi.org/10.54065/jss.6.3.2026.1370)]
- [2026] **Workplace Smoking Cessation Interventions: A Systematic Review of Randomized Controlled Trials** [[paper](https://osf.io/tdk92)]
- [2026] **Perceived Employability Under Digital Transformation: A Multilevel Systematic Review of Antecedents and Contextual Influences** *Qubahan Academic Journal* [[paper](https://doi.org/10.48161/qaj.v6n3a2494)]
- [2026] **What Keeps GoTo Competitive? Employee Perspectives on Agility and Human Capital** *International Journal of Advanced Multidisciplinary* [[paper](https://doi.org/10.38035/ijam.v5i2.2205)]
- [2026] **A STUDY ON CHALLENGES IN HUMAN RESOURCE MANAGEMENT** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennurnhhrb3p3c2)]
- [2026] **Technology, Sustainability and Innovations in Human Resource Management (HRM)** *Routledge eBooks* [[paper](https://doi.org/10.1201/9781042007769-39)]
- [2026] **Evolution of Cloud Architecture for Global Corporate Learning Management Systems** *International Journal of Computer (IJC)* [[paper](https://ijcjournal.org/InternationalJournalOfComputer/article/view/2540)]
- [2026] **The Role of Human Resource Management in Enhancing Employee Engagement in the Digital Workplace** *International Journal for Research in Applied Science and Engineering Technology* [[paper](https://doi.org/10.22214/ijraset.2026.82716)]

[⬆ Back to top](#paper-list)

#### Evaluation

##### 2026

- [2026] **The Impact of the Aging Workforce on Occupational Medicine: A Narrative Review** *Cureus* [[paper](https://doi.org/10.7759/cureus.113037)]

[⬆ Back to top](#paper-list)

#### Mechanism

##### 2026

- [2026] **Towing the Identity Line: Navigating Risks and Rewards of Self-Presentation at Work** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.13734symposium)]

[⬆ Back to top](#paper-list)

### Architecture & Infrastructure

### Evaluation & Case Studies

#### Method

##### 2026

- [2026] **The Influence of Digital Transformation on Employee Productivity and Workplace Efficiency in Modern Organizations** *International Journal For Multidisciplinary Research* [[paper](https://doi.org/10.36948/ijfmr.2026.v08i05.88987)]
- [2026] **Injury patterns and workplace safety characteristics of traumatic upper limb amputations in industrial press workers** *Journal of Musculoskeletal Surgery and Research* [[paper](https://doi.org/10.25259/jmsr_340_2026)]
- [2026] **A digital leadership cycle for strengthening primary teachers’ lesson planning** *Research and Development in Education (RaDEn)* [[paper](https://doi.org/10.22219/raden.v6i2.46285)]
- [2026] **Digital assessment of ergonomic risk factors in the operation of transport and handling equipment** *Transport & Logistics the International Journal* [[paper](https://people.fberg.tuke.sk/tnl/index.php/tnl/article/view/216)]
- [2026] **Developing Human Resource Strategy Through Internal and External Environmental Analysis: A Case Study of Kunawa Cafe Makassar** *Economics and Business Journal (ECBIS)* [[paper](https://ecbis.net/index.php/go/article/view/620)]
- [2026] **International Students’ Agency in Their Use of AI Tools for University Studies: A Qualitative Enquiry** *Emerald Group Publishing Limited eBooks* [[paper](https://doi.org/10.1108/978-1-80592-979-620261010)]
- [2026] **Exploring the Impact of Digital Leadership Transformation on Employee Engagement and Employee Performance** *EKONOMIS Journal of Economics and Business* [[paper](https://doi.org/10.33087/ekonomis.v10i2.2179)]
- [2026] **From Timeline To Me Time: Implementasi Modul Psikoedukasi Untuk Mengatasi Digital Fatigue** *Jurnal Pengabdian Inovasi Masyarakat Indonesia* [[paper](https://doi.org/10.29303/jpimi.v5i2.9152)]
- [2026] **Pelatihan Sistem Administrasi Berbasis Digital untuk Meningkatkan Kesiapan Kerja Siswa** *VIDHEAS Jurnal Nasional Abdimas Multidisiplin* [[paper](https://vinicho.id/index.php/vidheas/article/view/199)]
- [2026] **Dependability of Entrustable Professional Activity Portfolios in Otorhinolaryngology Residency: Nationwide Generalizability and Decision Study** *JMIR Medical Education* [[paper](https://doi.org/10.2196/104628)]
- [2026] **Case Study 1 (YES Lab) data outputs for PhD thesis "A Critical Analysis of 21st-Century Skills Development through Within-Class, Inter-Year and Virtual Exchange Interactions in Spanish for Specific Purposes."** *University of Limerick Research Repository* [[paper](https://hdl.handle.net/10344/32151)]
- [2026] **Sequential simulation-based clinical ethics education for clerkship students: A mixed-methods pre–post study** *Figshare* [[paper](https://doi.org/10.6084/m9.figshare.33164946)]
- [2026] **The Role of Artificial Intelligence to Improve Workplace Satisfaction and Productivity: A Qualitative Case Study of Healthcare Workers in Indonesian Hospitals** *Fundamental and Applied Management Journal* [[paper](https://doi.org/10.66314/famj.v4i3.1036)]
- [2026] **Emojis in Professional Communication: A Double-Edged Sword in Cross-Cultural Interactions between Zimbabweans and Chinese Employees in Zimbabwean Workplaces** *Management and Economics Research Journal* [[paper](https://doi.org/10.18639/merj.2026.9900124)]
- [2026] **Digital Transformation and AI in Human Resource Practices – an Analytical Review** *International Journal of Integrative Studies (IJIS)* [[paper](https://doi.org/10.63856/ijis/v2i7/02)]
- [2026] **Organizational adaptation in judicial digital transformation: building an inclusive work environment at the Bandung High Court** *Asian Anthropology* [[paper](https://doi.org/10.1080/1683478x.2026.2705044)]
- [2026] **Men's Roles in Unpaid Domestic Work: A Case Study of Paternal Involvement in Indonesia** *Journal of Feminism and Gender Studies* [[paper](https://jfgs.jurnal.unej.ac.id/index.php/FGS/article/view/53714)]
- [2026] **From Workshops to Workflows: Boundary Infrastructure and the Transfer of Design Thinking into Everyday Work** *Journal of Management Science and Operations* [[paper](https://itip-submit.com/index.php/JMSO/article/view/267)]
- [2026] **Digital Platform Work Beyond the Workplace: Household Risk and Welfare Inaccessibility among Delivery Rider Families in China** [[paper](https://doi.org/10.31235/osf.io/6nw8q_v1)]
- [2026] **Estimating Entrustable Professional Activity Portfolio Sufficiency Using a Digital Workplace Assessment Platform in Competency-Based Residency Training: Nationwide Cross-Sectional Generalizability and Decision Study (Preprint)** [[paper](https://doi.org/10.2196/preprints.104628)]
- [2026] **Implementing Learning Management Systems To Support Digital Transformation In Education: A Case Study Of Business English Learning** *PIJAR Jurnal Pendidikan dan Pengajaran* [[paper](https://doi.org/10.58540/pijar.v4i3.1854)]
- [2026] **HRM Practices for Marketing Employees on Digital Platforms: KPI Pressure and Performance** *Agregat Jurnal Ekonomi dan Bisnis* [[paper](https://doi.org/10.22236/agregat_vol9.i2/23186)]
- [2026] **Professional Communication Education: Culture, Digital Ethics, and AI for Indonesia Migrant Workers in Japan** *Jurnal Ragam Pengabdian* [[paper](https://doi.org/10.62710/6v5s3f94)]
- [2026] **Informal learning spaces and student experience: a mixed-methods case study at an Austrian university** *Frontiers in Education* [[paper](https://doi.org/10.3389/feduc.2026.1762719)]
- [2026] **GENDERED NARRATIVES IN WOMEN-ORIENTED MICRO-SHORT PLAYS: A CROSS-CULTURAL STUDY** *International Journal of Law Government and Communication* [[paper](https://doi.org/10.35631/ijlgc.1144005)]
- [2026] **Innovative Practice and Learning Effectiveness of Integrating AI Marketing into SPA Brand Courses: A Case Study of a Five-Year Junior College Program in Cosmetics Application Management** *Journal of AI* [[paper](https://doi.org/10.61969/jai.1908263)]
- [2026] **Two Ways to Rome** *European Journal of Workplace Innovation* [[paper](https://doi.org/10.46364/ejwi.v10i2.1631)]
- [2026] **Transforming Hospitality and Tourism Education** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-3373-5806-2.ch015)]
- [2026] **The Role of the Digital Workplace in Enhancing Productive Organizational Energy: An Analytical Study at the University of Fallujah** *F1000Research* [[paper](https://doi.org/10.12688/f1000research.174088.2)]
- [2026] **THE IMPACT OF DIGITAL RECRUITMENT ON INTERNSHIP EMPLOYEES WORKPLACE READINESS** *Journal of Management and Leadership* [[paper](https://doi.org/10.47970/jml.v9i1.1149)]
- [2026] **Optimalisasi Digital Workplace Berbasis Sistem Informasi Terhadap Kinerja PegawaiPada Sistem Work From Home** *JOURNAL OF SCIENCE AND SOCIAL RESEARCH* [[paper](https://jurnal.goretanpena.com/index.php/JSSR/article/view/6170)]
- [2026] **Academic Case Study-Real dangers of digital violence-Dismantling the Digital hit** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20320174)]
- [2026] **Peer Review Report For: The Role of the Digital Workplace in Enhancing Productive Organizational Energy: An Analytical Study at the University of Fallujah [version 2; peer review: 2 approved]** [[paper](https://doi.org/10.5256/f1000research.197968.r486398)]
- [2026] **Vocational outcomes following assistive technology and digital workplace supports for people with disabilities: a systematic review** *Disability and Rehabilitation Assistive Technology* [[paper](https://doi.org/10.1080/17483107.2026.2666392)]
- [2026] **Embedding Microsoft Certifications and GMetrix into Accounting Education: Enhancing Digital Skills, Student Engagement, and Graduate Employability** *Arrow - TU Dublin (Technological University Dublin)* [[paper](https://arrow.tudublin.ie/teachingcasedig/61)]
- [2026] **Digitalisation, human factors, and mental health among primary care professionals aged ≥ 50 years: a mixed-methods case study in Portugal** *BMC Health Services Research* [[paper](https://doi.org/10.1186/s12913-026-14671-3)]
- [2026] **Study of financial growth and employee relations in major Indian fintech companies** *International Journal of Research in Management* [[paper](https://doi.org/10.33545/26648792.2026.v8.i5b.905)]
- [2026] **INNOVATIVE APPROACHES TO THE EFFECTIVE USE OF INDUSTRIAL TERMINOLOGY IN ENGLISH LANGUAGE TEACHING THROUGH EXERCISE INTEGRATION** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20307224)]
- [2026] **PTC PTC WCImpPr PDF** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20035919)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **The ecosystemic workplace: Erotic content creation and the spatial transformation of digital labour** *Platforms & Society* [[paper](https://doi.org/10.1177/29768624261492473)]
- [2026] **Socio-technical co-adaptation: Digital integration and workplace learning** *Human Technology* [[paper](https://doi.org/10.14254/1795-6889.2026.22-2.8)]
- [2026] **Empirical Case Studies of Digital-Era Transformation in Higher Education Management** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781042001422-22)]
- [2026] **Digital Confidence and Workplace Support in Reported Generative AI Use Among Adults Aged 45 and Above** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23449234)]
- [2026] **A participatory work study model for AI-supported workplace learning in Finnish SMEs** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23266820)]
- [2026] **Analysis of Obstacles in the Implementation of Workplace Safety Laws and Proposing Effective Solutions** *International Journal of Law Management & Humanities* [[paper](https://doi.org/10.63108/ijlmh.12939)]
- [2026] **Assessing Workplace Technology Impacts on Employee Work and Wellbeing: A Post-Adoption Blind Spot** *International Journal of Human-Computer Interaction* [[paper](https://doi.org/10.1080/10447318.2026.2744837)]
- [2026] **STRATEGI KOMUNIKASI DIGITAL BERBASIS VRIO DALAM PENGELOLAAN KAMPANYE #SAYABERBUDAYASAFETY OLEH CORPORATE COMMUNICATION KPP MINING** *NIVEDANA Jurnal Komunikasi dan Bahasa* [[paper](https://jurnal.radenwijaya.ac.id/index.php/NIVEDANA/article/view/2802)]
- [2026] **DUE DILIGENCE NA ERA DIGITAL: : NOVOS MECANISMOS DE PREVENÇÃO E DETECÇÃO DO TRABALHO ESCRAVO** *Revista Direito Mackenzie* [[paper](https://editorarevistas.mackenzie.br/rmd/article/view/18392)]
- [2026] **Visible but learning-weak: trace visibility and within-phase distortions in digitally supported continuous improvement** *Journal of Workplace Learning* [[paper](https://doi.org/10.1108/jwl-04-2026-0203)]
- [2026] **Beyond the algorithm: understanding how HR professionals in Guwahati preserve human values in an era of digital transformation** *Journal of Organizational Effectiveness People and Performance* [[paper](https://doi.org/10.1108/joepp-09-2025-0811)]
- [2026] **Advancing an integrated framework for benefits realization: a case of industrial robotic projects** *International Journal of Managing Projects in Business* [[paper](https://doi.org/10.1108/ijmpb-01-2026-0031)]
- [2026] **Reframing CSR in the Age of AI** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-2600-4609-8.ch010)]
- [2026] **Faculty-supervised AI-supported BOPPPS-CBL and performance on a simulated neurological-emergency assessment among junior-college medical interns: a batch-stratified randomized educational study** *Frontiers in Medicine* [[paper](https://doi.org/10.3389/fmed.2026.1945397)]
- [2026] **Learning across Boundaries in VET Contexts** *VETNET Conference Series* [[paper](https://doi.org/10.21240/vetcon/2026/ecer/71)]
- [2026] **Leadership in Neurodiverse AI-Augmented Organizations** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23494433)]
- [2026] **Human-Centered AI in HR Transforming Employee Well-Being and Workplace Culture in the Digital Era** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-3373-9599-9.ch007)]
- [2026] **SOCIAL MEDIA MONITORING AND WORKPLACE TRUST: A PARADOX?** *International Journal of Financial Research and Management Science* [[paper](https://doi.org/10.70382/tijfrms.v13i7.082)]
- [2026] **Workplace Surveillance in the Post-Digital Personal Data Protection (DPDP) Act, 2023 Era: Reconciling Legitimate Employer Interests with Employee Right to Privacy** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23020885)]
- [2026] **The role of digitalization in transforming training practices and employee learning perceptions: case study of an Algerian mobile network operator** *Journal of Workplace Learning* [[paper](https://doi.org/10.1108/jwl-04-2026-0205)]
- [2026] **Bridging Classroom Mandarin and Workplace Communication: Challenges and Adaptive Strategies among Student Interns in a Chinese Company** *International Journal of Post Axial Futuristic Teaching and Learning* [[paper](https://doi.org/10.59944/postaxial.v4i3.1873)]
- [2026] **Empowering Industry 5.0 Education through Digital Ergonomics and Simulation** *CRC Press eBooks* [[paper](https://doi.org/10.1201/9781003546290-21)]
- [2026] **Writing Toward the Workplace: Vocational Students’ Experience with LinkedIn in a Genre-Based Classroom** *IDEAS Journal on English Language Teaching and Learning Linguistics and Literature* [[paper](https://ejournal.iainpalopo.ac.id/index.php/ideas/article/view/12309)]
- [2026] **Conceptualising digital nomadic practice: evidence from a technology-intensive firm** *Warwick Research Archive Portal (University of Warwick)* [[paper](https://wrap.warwick.ac.uk/86753/1/WRAP_Theses_Kadnarova_2016.pdf)]
- [2026] **Gender Equality, Human Capital and Regional GDP: Contrasting Hangzhou's Digital Economy with Tangshan's Industrial Model** *Advances in Economics Management and Political Sciences* [[paper](https://doi.org/10.54254/2754-1169/2026.36594)]
- [2026] **Social Capital in the Digital Transformation: How Assistance Systems in Production Reshape Communication and Knowledge Transfer** *management revue* [[paper](https://doi.org/10.31083/mrev58245)]
- [2026] **Family Communication Patterns of Female Civil Servants within Bureaucratic Work Culture and Digital Transformation** *Jurnal Riset Komunikasi* [[paper](https://doi.org/10.38194/jurkom.v9i2.1628)]
- [2026] **Curriculum evolution and documentary evidence of competency alignment in a hospital-embedded undergraduate health services and management programme in China: a longitudinal case study** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1956968)]
- [2026] **Comparative case study on the implementation of the multi- space concept in a healthcare facility: study protocol** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2026.1964644)]
- [2026] **Encouraging Youth Entrepreneurship Through Computer Science Education and Digital Skills Development: A Pathway to Sustainable Socioeconomic Growth** *WORLD JOURNAL OF ENTREPRENEURIAL DEVELOPMENT STUDIES* [[paper](https://doi.org/10.56201/wjeds.v10.no7.2025.pg203.218)]
- [2026] **Operational Responsiveness and Technostress in Instant Messaging: Evaluating Field Communication Efficiency and Digital Governance Needs** *Journal of Communication Research* [[paper](https://doi.org/10.61105/jcr.v2i2.487)]
- [2026] **Artificial Intelligence in E-commerce Education: Bridging the Gap Between Academic Learning, Digital Competencies and Industry Readiness** *International Journal For Multidisciplinary Research* [[paper](https://doi.org/10.36948/ijfmr.2026.v08i05.87024)]
- [2026] **CASE STUDY OF UITM KEDAH ON THEMATIC ANALYSIS OF INDUSTRIAL TRAINING REPORTS FROM LIBRARY MANAGEMENT STUDENTS** *International Journal of Education Psychology and Counseling* [[paper](https://doi.org/10.35631/ijepc.1164011)]
- [2026] **Navigating Digital Transformation: Sociological and Educational Factors in Corporate AI Strategy Adoption** *European Journal of Social Sciences Education and Research* [[paper](https://doi.org/10.26417/mck5nml6)]
- [2026] **Could Hybrid Work Pave the Way for More Inclusive Internal Communication in Geographically Dispersed Organizations?** *The Journal of Communication and Media Studies* [[paper](https://doi.org/10.18848/2470-9247/cgp/a157)]
- [2026] **The “Strawberry Generation” in the Teaching Factory: Multi-Perspective Qualitative Study of Soft Skills Assessment Dilemmas in Indonesian Vocational High Schools** *International Journal of Learning Teaching and Educational Research* [[paper](https://doi.org/10.26803/ijlter.25.9.9)]
- [2026] **Mpox preventive practices and associated factors among adults in a travel-connected setting in Southern Sarawak, Malaysia: a community-based cross-sectional study** *BMC Public Health* [[paper](https://doi.org/10.1186/s12889-026-29271-3)]
- [2026] **Intergenerational Leadership Succession, Learning, and Knowledge Transfer** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-3373-8074-2.ch008)]
- [2026] **Workplace Safety in the AI Era** *Chapman & Hall/CRC eBooks* [[paper](https://doi.org/10.1201/9781003754213-2)]
- [2026] **Aligning Civil Service Training with Workplace Competencies: Examining the Law and Administration Course in Bangladesh** *Bangladesh Journal of Administration and Management* [[paper](https://doi.org/10.56379/bjam.v38i2.104)]
- [2026] **Developing a Cybersecurity Education Framework to Prepare the Future Construction Workforce for Digital Resilience** *ASCE Construction Research Congress (CRC)* [[paper](https://doi.org/10.1061/9780784486993.013)]
- [2026] **Dwelling in Mobility: Reconstructing Everyday Life Meaning among Digital Nomads through Rural Sojourns** *Academic Journal of Management Science and Engineering* [[paper](https://doi.org/10.62051/ajmse.v1n4.05)]
- [2026] **A case study on the work and learning of work-from-home employees in Silicon Valley: lessons from the pandemic** *European journal of training and development* [[paper](https://doi.org/10.1108/ejtd-07-2025-0142)]
- [2026] **DIGITAL TRANSFORMATION IN SHARIA-BASED ORGANIZATIONS: STRUCTURAL SHIFTS, CULTURAL ADAPTATIONS, AND VALUE-ORIENTED STRATEGIES** *ASY SYAR IYYAH JURNAL ILMU SYARI AH DAN PERBANKAN ISLAM* [[paper](https://doi.org/10.32923/gt2t3t09)]
- [2026] **Integrating Smart Health Systems in the Era of Digital Cities** *CRC Press eBooks* [[paper](https://doi.org/10.1201/9781003741589-11)]
- [2026] **Language, Discourse, and Professional Communication: An English Studies Approach to Contemporary Contexts** *Minnesota Journal of Business Law and Entrepreneurship* [[paper](https://kommerstad.org/journal/article/view/778)]
- [2026] **Assessing computational thinking through integrated approaches: the case of ModeLLer** *Behaviour and Information Technology* [[paper](https://doi.org/10.1080/0144929x.2026.2711028)]
- [2026] **A study on skill gap in Mumbai B.com Graduated as per HR Manager** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23360337)]
- [2026] **The Case for Health Communications Technology: Why Phone Calls Need a Neurodivergent-First Redesign** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21978704)]
- [2026] **AI-Driven Decision-Making in Finance** *CRC Press eBooks* [[paper](https://doi.org/10.1201/9781003656463)]
- [2026] **Applying Generative AI to the Learning Analytics Cycle to Support Competency Development in Health Professions Education** *Journal of Learning Analytics* [[paper](https://doi.org/10.18608/jla.2026.9145)]
- [2026] **From Hashtag to Power** *Inquiry Queen s Undergraduate Research Conference Proceedings* [[paper](https://doi.org/10.24908/iqurcp21686)]
- [2026] **Chronic Workplace Interpersonal Trauma with Acute Psychological Manifestations: A Case Report Integrating Clinical Models and AI-Assisted Structured Reflective Digital Support** *Archives of Trauma and Emergency Medicine* [[paper](https://doi.org/10.33696/trauma.2.008)]
- [2026] **Digital cohesion and organizational effectiveness in hybrid work: a multi-case qualitative study of digital social capital** *Journal of Organizational Effectiveness People and Performance* [[paper](https://doi.org/10.1108/joepp-12-2025-1107)]
- [2026] **A BUDDHIST-APPROACH TRAINING PROGRAM FOR EMPLOYEE WELL-BEING IN TECHNOLOGY-OVERUSED WORKPLACE** *Journal of Buddhist Anthropology* [[paper](https://so04.tci-thaijo.org/index.php/JSBA/article/view/287308)]
- [2026] **Digital celebrity feminist activism in Pakistan** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003290582-32)]
- [2026] **Workplace-Based Assessment in Postgraduate Medical Education: A Narrative Review of Tools, Validity, and Educational Impact** *Bangladesh Journal of Medical Education* [[paper](https://doi.org/10.3329/bjme.v17i2.91790)]
- [2026] **Digital Dignity in Algorithmic Management and Inclusive Innovation in Southeast Asian Workspaces** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-3373-5213-8.ch022)]
- [2026] **School education for future XR workplaces: preparing teachers through a dual training pathway** *Journal of Ambient Intelligence and Humanized Computing* [[paper](https://doi.org/10.1007/s12652-026-05107-1)]
- [2026] **ETNOGRAFI VIRTUAL PRAKTIK DIGITAL VIGILANTISM NETIZEN DI THREADS PADA KASUS TUMBLER TUKU** *Pendas Jurnal Ilmiah Pendidikan Dasar* [[paper](https://journal.unpas.ac.id/index.php/pendas/article/view/59439)]
- [2026] **Rethinking Job Demands–Resources Theory: Insights from Digital Transformation in Chinese SOEs** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.14148poster)]
- [2026] **Enhancing Medical Education through Gamified Microteaching and Digital Reinforcement in a new University Hospital Setting** *Saudi Journal of Emergency Medicine* [[paper](https://doi.org/10.24911/sjemed.12-2525)]
- [2026] **Beyond Bandura: Enhancing Organizational Cloud Competency Using Connectivism** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.11290abstract)]
- [2026] **From Manufacturing Consent to Materializing Matters: Performing Control in Liquid Organizing** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.18760abstract)]
- [2026] **Challenges and Innovations in Implementing Dual Mentorship for ESD: A Global Comparative Analysis** *Springer Link (Chiba Institute of Technology)* [[paper](https://www.e3s-conferences.org/10.1051/e3sconf/202672006002/pdf)]
- [2026] **Designing for Dignity** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-3373-5213-8.ch017)]
- [2026] **Towards an Inclusive Integration of Digital Technologies for Workplace Learning in Brunei** *innsbruck university press* [[paper](https://doi.org/10.15203/99106-195-3-04)]
- [2026] **From Awareness to Action in Industry 5.0: A Qualitative Case-Based Study on the Influence of POSH Training on Workplace Behaviour** *International Journal on Research and Development - A Management Review* [[paper](https://doi.org/10.65521/ijrdmr.v15i2.3702)]
- [2026] **Ergonomic governance and workplace integrity in workforce diversity: A digital approach to musculoskeletal risk assessment in Malaysian automotive manufacturing** *Journal of Governance and Integrity* [[paper](https://doi.org/10.15282/jgi.9.1.2026.14393)]
- [2026] **Triadic pressure and teacher resilience: A qualitative case study of mathematics teachers navigating instructional accountability, administrative workload and digital distraction** *International Journal of Science and Research Archive* [[paper](https://doi.org/10.30574/ijsra.2026.19.3.1285)]
- [2026] **Design, Development, and Validation of a Chatbot to Support Health Care Professionals Experiencing Workplace Aggression: Protocol for a Mixed Methods Study** *JMIR Research Protocols* [[paper](https://doi.org/10.2196/92511)]
- [2026] **Managerial perspectives on digital upskilling and reskilling in Western Australia: A consulting industry case study** *Research Online (Edith Cowan University)* [[paper](https://ro.ecu.edu.au/theses/3080)]
- [2026] **Instructional Leadership and Teacher Commitment: The Mediating Role of Workplace Harmony in Educational Settings** *International Journal of Drug Delivery Technology* [[paper](https://doi.org/10.25258/ijddt.16.51s.78)]
- [2026] **Early Detection of Workplace Stress Using NLP and Sentiment Analysis on Employee Communication Data** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20507971)]
- [2026] **Caring for the caregivers: implementing collaborative governance practices in healthcare workplaces during the COVID-19 pandemic** *Employee Relations* [[paper](https://doi.org/10.1108/er-06-2025-0505)]
- [2026] **Business Ethics: Principles, Practices, and Case Studies** [[paper](https://doi.org/10.70593/978-93-7185-466-5)]
- [2026] **A SWOT Analysis of the BS-Level Education Curriculum Using the Logic Model: Workplace Readiness at Abdul Wali Khan University Mardan** *Journal for Current Sign* [[paper](https://www.currentsignreview.com/index.php/JCS/article/view/883)]
- [2026] **Development of the multicomponent PATH@work intervention for musculoskeletal disorders among blue-collar workers Integrating evidence-based clinical care and workplace interventions** *Research Square* [[paper](https://doi.org/10.21203/rs.3.rs-9867601/v1)]
- [2026] **Teachers’ digital competence and educational quality in rural vocational schools** *Indonesian Research Journal in Education |IRJE|* [[paper](https://online-journal.unja.ac.id/index/article/view/54998)]
- [2026] **‘Place’ and clinical reasoning development in context: An ethnographic case study** *Medical Teacher* [[paper](https://doi.org/10.1080/0142159x.2026.2691077)]
- [2026] **Beyond Infrastructure: The Practitioner-Led Innovation Framework A Professional Case Study of Technology Leadership Through the Career of Nitin Dhingra** *International Journal of Creative and Open Research in Engineering and Management* [[paper](https://doi.org/10.55041/ijcope.v2i6.034)]
- [2026] **Professional Development and Digital Governance in One-Stop Service Transformation: An Educational Perspective** *AL-ISHLAH Jurnal Pendidikan* [[paper](https://doi.org/10.35445/alishlah.v18i2.9875)]
- [2026] **Academic Readiness and University–Industry Collaboration in Online and Flexible Learning Pathways: A Multi-University Case Study in Indonesia** *Online Learning In Educational Research (OLER)* [[paper](https://doi.org/10.58524/oler.v6i2.1049)]
- [2026] **IMPLEMENTASI INTEGRASI API DALAM WORKFLOW AUTOMATION MENGGUNAKAN N8N UNTUK MENDUKUNG TRANSFORMASI DIGITAL** *AMMA : Jurnal Pengabdian Masyarakat* [[paper](https://journal.mediapublikasi.id/index.php/amma/article/view/6426)]
- [2026] **Evaluating Policy Interventions for Promoting Decent Work and Gender Inclusion in Metro Rail Employment: A Case Study from South India** *Routledge eBooks* [[paper](https://doi.org/10.1201/9781042005550-44)]
- [2026] **Leadership and Communication Dynamics in Digital Project Teams: Exploring Their Influence on Team Performance** *Buletin Poltanesa* [[paper](https://doi.org/10.51967/tanesa.v27i1.3645)]
- [2026] **Blurring boundaries: how remote and hybrid work reshape learning in SMEs after the pandemic** *European journal of training and development* [[paper](https://doi.org/10.1108/ejtd-09-2025-0188)]
- [2026] **Challenges of the 21st Century: Work, Lifetech and Capability** *innsbruck university press* [[paper](https://doi.org/10.15203/99106-195-3-02)]
- [2026] **Re-Imagining Gender Beyond The Binary In Information Technology Work** *Journal of the Association for Information Systems* [[paper](https://aisel.aisnet.org/ecis2026/conf_theme/conf_theme/3)]
- [2026] **Harassment in labor relations: national practice and international experience** *Uzhhorod National University Herald Series Law* [[paper](https://doi.org/10.24144/2307-3322.2026.94.2.25)]
- [2026] **Харасмент у трудових відносинах: національна практика та міжнародний досвід** *The Scientific Issues of Ternopil Volodymyr Hnatiuk National Pedagogical University Series pedagogy* [[paper](https://visnyk-pravo.uzhnu.edu.ua/article/view/364379)]
- [2026] **Research on the Construction of Chinese Women's Self-discourse Power and Independent Resistance Path from the Perspective of Contemporary Society** *Academic Journal of Education* [[paper](https://doi.org/10.54097/rz02tk08)]
- [2026] **Development and Implementation of Information Technology-Based Learning Media in Project-Based Animation Learning at State Vocational School 4 Madiun** *Journal on Smart Learning Technologies* [[paper](https://journal.unesa.ac.id/index.php/jslt/article/view/53207)]
- [2026] **Multilayered Liability Closes Gaps in Technology Based Office Embezzlement** *Academia Open* [[paper](https://doi.org/10.21070/acopen.11.2026.14535)]
- [2026] **Designing student-centred digital learning for belonging, engagement and employability: a case study of the University of Limerick’s transformative digital ecosystem** *Information and Learning Sciences* [[paper](https://doi.org/10.1108/ils-09-2025-0171)]
- [2026] **Decoding the Code: Multimodal Workplace Attire and Corporate Identity Construction on Goldman Sachs’ Instagram** *International Journal of Business Communication* [[paper](https://doi.org/10.1177/23294884261453046)]
- [2026] **POORNAPRAJNA BUSINESS TEACHING CASE STUDIES-2026** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20373101)]
- [2026] **A Millennials Journey to Revive Workplace Culture at XYZ Ltd.** *International Journal for Research in Applied Science and Engineering Technology* [[paper](https://doi.org/10.22214/ijraset.2026.82373)]
- [2026] **Pencil versus red pen : tutoring techniques in the print and digital newsroom** [[paper](https://doi.org/10.32469/10355/112678)]
- [2026] **Age, inclusion and adaptation in digital learning for work: advancing a learner-centred Education 5.0 framework** *Studies in Continuing Education* [[paper](https://doi.org/10.1080/0158037x.2026.2667829)]
- [2026] **Mycelium: A Peer-to-Peer Chat System for Metadata-Minimizing Communication; Balancing Efficiency and Humanity: How AI Adoption Shapes Workplace Productivity and Job Satisfaction** *Libra* [[paper](https://doi.org/10.18130/vqmb-fk72)]
- [2026] **How could body-augmenting technology enable human digital twins to facilitate spiritual experiences?** *AI & Society* [[paper](https://doi.org/10.1007/s00146-025-02782-0)]
- [2026] **The illusion of empowerment: commercializing women’s health in the digital age** *Health Promotion International* [[paper](https://doi.org/10.1093/heapro/daag074)]
- [2026] **Evaluation of Occupational Health, Safety and Environmental Systems in Construction Industry: A Case Study Approach** *Iconic Research and Engineering Journals* [[paper](https://doi.org/10.64388/irev9i11-1717713)]
- [2026] **Be on Path: A Digital Career Path Intelligence System for Monitoring OJT Progression** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20035411)]
- [2026] **AI-Enabled Innovation in Education and Work: Philosophical Reflections on Digital Transformation and Human Adaptation** *Philosophies* [[paper](https://doi.org/10.3390/philosophies11030073)]
- [2026] **Future-Oriented ESP for Business Professionals** *Future Education Review* [[paper](https://doi.org/10.53893/fer.v1i1.507)]
- [2026] **Redefining Recruitment in the it Sector: A Comparative Study of Skill-Based and Degree-Based Hiring Practices** *International Journal of Science Strategic Management and Technology* [[paper](https://doi.org/10.55041/ijsmt.v2i5.429)]
- [2026] **Håll dem informerade: Organisationskommunikation vid digitala teknologiska förändringar, en kvalitativ fallstudie** *Aaltodoc (Aalto University)* [[paper](https://aaltodoc.aalto.fi/handle/123456789/145660)]
- [2026] **Designing a Carbon-Aware Dashboard for Visualizing Environmental Costs of Digital Actions; The Environmental Impact of AI Development and Integration: An Analysis of Primary Contributors** *Libra* [[paper](https://doi.org/10.18130/84ta-fa37)]
- [2026] **Cultivating Future Leaders** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-3373-2155-4.ch004)]
- [2026] **Strategic Human Resource Management in the Age of Generative AI and Platform-Based Services** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-2600-1845-3.ch001)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **Women Empowerment in Tourism and Hospitality: Challenges and Opportunities in Digital Marketing** *BENTHAM SCIENCE PUBLISHERS eBooks* [[paper](https://doi.org/10.2174/97988988175031260101)]
- [2026] **Employer Branding as a Strategic Marketing Asset: A Multiple-Case Study of High-Growth Startups in Indonesia** *International Journal of Management and Business Intelligence* [[paper](https://doi.org/10.59890/ijmbi.v4i5.79)]
- [2026] **Exploring Strategic AI Adoption and Entrepreneurial Opportunities Through University Industry Ecosystem Learning** *ADI Journal on Recent Innovation (AJRI)* [[paper](https://doi.org/10.34306/ajri.v8i2.1577)]
- [2026] **The Role of Spiritual Leadership in Building Religious Culture in the Digital Era: Case Study at MW Rona Jaya Jombang** *International Journal of Educational Review Law And Social Sciences (IJERLAS)* [[paper](https://radjapublika.com/index.php/IJERLAS/article/view/5911)]
- [2026] **Gamification, Serious Games and Industry 4.0** *IntechOpen eBooks* [[paper](https://doi.org/10.5772/intechopen.1017964)]
- [2026] **„Működtetni tudom, de nem értem…”** *Socio hu* [[paper](https://doi.org/10.18030/socio.hu.2026.2.1)]
- [2026] **Human–AI Collaboration and Intelligent Automation: The Role of AI Readiness and Digital Skills** *Turing Ledger Journal of Engineering & Technology* [[paper](https://scholarclub.org/index.php/TLJET/article/view/298)]
- [2026] **Compliance with mandatory ID badge policies in Tanzanian public hospitals: A case study of Dar-es-Salaam referral hospitals** *International Journal of Research in Business and Social Science (2147-4478)* [[paper](https://doi.org/10.20525/ijrbs.v15i3.4935)]
- [2026] **Executive Brief 02: When One Employee Downloads Free Software — How a Small Convenience Can Become an Enterprise Risk** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20785804)]

[⬆ Back to top](#paper-list)

#### Survey

##### 2026

- [2026] **Bridging Gender Gaps in Information Technology: Women’s Contribution to Economic Growth and Development** [[paper](https://doi.org/10.31235/osf.io/3gcdm_v1)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **Occupational Accidents and the Transformation of Social Security Law in the Digital Workplace: The Case of Kazakhstan** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22031018)]
- [2026] **The Impact of Oracle HCM Cloud on Employee Retention Strategies in Digital Workplaces** *E-Journal of Science and Emerging Technologies (EJSET)* [[paper](https://ejset.org/index.php/index/article/view/55)]

[⬆ Back to top](#paper-list)

#### Evaluation

##### 2026

- [2026] **Detoxifying Toxic Communication: A Design Science Approach to Responsible AI** [[paper](https://arxiv.org/abs/2609.00361)]

[⬆ Back to top](#paper-list)

### Surveys & Reviews

#### Method

##### 2026

- [2026] **Digital Fatigue in the Digital Workplace: Emerging Occupational Risks and the Georgian Context** *MODERN ISSUES OF MEDICINE AND MANAGEMENT* [[paper](https://doi.org/10.56580/geomedi87)]
- [2026] **Digital Health Among Educators: A Scoping Review** *Healthcare* [[paper](https://doi.org/10.3390/healthcare14193313)]
- [2026] **Digital Musculoskeletal Assessment: A Narrative Review of Self-Report, Telehealth, Sensor-Based, and Conversational AI Modalities, with Implications for Workplace Screening** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22785025)]
- [2026] **Discrimination in the Digital Workplace: New Manifestations and Responses** *Ius Novum* [[paper](https://ojs.lazarski.pl/index/article/view/2391)]
- [2026] **Auditor Capabilities and Workplace Pressures in Shaping Audit Quality: A Systematic Literature Review and Future Research Agenda** *International Journal of Education Vocational and Social Science* [[paper](https://e-journal.citakonsultindo.or.id/index.php/IJEVSS/article/view/6622)]
- [2026] **WORK-BASED LEARNING DIGITAL UNTUK MENINGKATKAN KESIAPAN KERJA SISWA PENDIDIKAN VOKASI: SYSTEMATIC REVIEW** *ACADEMIA Jurnal Inovasi Riset Akademik* [[paper](https://doi.org/10.51878/academia.v6i4.13855)]
- [2026] **Self-reported pain on a digital workplace assessment: identifying the score that flags desk-based workers for earlier occupational health review** *Frontiers in Digital Health* [[paper](https://doi.org/10.3389/fdgth.2026.1919657)]
- [2026] **Peer and Workplace RA among Adults Scale development: A Modified Delphi Approach** [[paper](https://doi.org/10.31234/osf.io/7ytnq_v2)]
- [2026] **ASSESSING THE EFFECTIVENESS OF WORK-FROM-HOME IMPLEMENTATION AND PERFORMANCE MONITORING IN THE DIGITAL WORKPLACE: A DIGITAL HRM PERSPECTIVE** *Jurnal Riset Multidisiplin Edukasi* [[paper](https://journal.hasbaedukasi.co.id/index.php/jurmie/article/view/2351)]
- [2026] **A systematic review of technological approaches to managing workplace violence against healthcare workers** *Safety Science* [[paper](https://doi.org/10.1016/j.ssci.2026.107364)]
- [2026] **Scopus Bibliometric Dataset: Digital Work, Psychosocial Risks, Organizational Trust, and Workplace Conflict (2010–2026)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21788789)]
- [2026] **Digital Literacy in the Age of AI** *International Journal of Computer Information Systems and Industrial Management Applications* [[paper](https://doi.org/10.70917/ijcisim-2026-2710)]
- [2026] **Remote Work Paradox: Examining the Tension between Workplace Flexibility, Employee Productivity and Organisational Performance** *Britain International of Humanities and Social Sciences (BIoHS) Journal* [[paper](https://doi.org/10.5281/zenodo.21615050)]
- [2026] **Workplace interventions for chronic musculoskeletal disorders: a systematic review** *BMJ Open* [[paper](https://doi.org/10.1136/bmjopen-2025-115276)]
- [2026] **Digital harassment and its mental health impact among healthcare professionals: A scoping review** *Psychiatry and Clinical Neurosciences Reports* [[paper](https://doi.org/10.1002/pcn5.70362)]
- [2026] **Paraphrasing For Safety: How GenAI Shapes Privacy Perceptions On Digital Employer Review Platforms** *Journal of the Association for Information Systems* [[paper](https://aisel.aisnet.org/ecis2026/security/security/9)]
- [2026] **NAVIGATING DIGITAL TRANSFORMATION AND SUSTAINABLE PERFORMANCE: A SYSTEMATIC LITERATURE REVIEW ON THE HUMAN-CENTRIC PARADIGM IN INDUSTRY 4.0** *Advanced International Journal of Business Entrepreneurship and SMEs* [[paper](https://doi.org/10.35631/aijbes.828010)]
- [2026] **DIGITAL TECHNOLOGIES IN BREEDING AND SEED PRODUCTION: REVIEW AND EVALUATION OF EFFECTIVENESS** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20544745)]
- [2026] **DIGITAL MENTAL HEALTH SUPPORT FOR HEALTHCARE PROFESSIONALS: A NARRATIVE REVIEW OF TELEPSYCHIATRY AND AI-DRIVEN CHATBOTS IN BURNOUT MITIGATION** *International Journal of Innovative Technologies in Social Science* [[paper](https://doi.org/10.31435/ijitss.2(50).2026.5736)]
- [2026] **DIGITAL DISRUPTIONS AND THE FUTURE OF WORK** *International Journal of Arts Humanities & Social Sciences* [[paper](https://doi.org/10.56815/irjahs/2026.v(2026)i1.55-68)]
- [2026] **On methodological fit and interpretive boundaries in qualitative synthesis within the recent article: How do female healthcare staff experience the menopause transition in the workplace? A critical meta-synthesis** *Maturitas* [[paper](https://doi.org/10.1016/j.maturitas.2026.109012)]
- [2026] **Literature Review: Peran Komunikasi Interpersonal dalam Menjembatani Gap Generasi pada Era Digital di Dunia Kerja** *MUKASI Jurnal Ilmu Komunikasi* [[paper](https://doi.org/10.54259/mukasi.v5i2.6365)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **Innovative Job Performance in Digitally Enabled Workplaces: A Systematic Review and Bibliometric Synthesis of Individual-Level Innovative Work Behavior** *Indonesian Journal of Business and Entrepreneurship Research* [[paper](https://doi.org/10.62794/ijober.v4i4.545)]
- [2026] **Peer Review Report For: Bridging the Electronic Surveillance Gap: A Comparative Legal Analysis of Workplace Privacy in the Digital Age. [version 1; peer review: 1 approved with reservations]** [[paper](https://doi.org/10.5256/f1000research.201366.r530562)]
- [2026] **The Impact of Communication Overload and Fragmented Messaging on Productivity in Digital Workplaces** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23103478)]
- [2026] **Digital Mindfulness and Employee Wellness: A Systematic Literature Review** *International Journal of Contemporary Business Research* [[paper](https://doi.org/10.4038/ijcbr.v5i1.62)]
- [2026] **ORGANIZATIONAL BEHAVIOUR AND WORKPLACE PSYCHOLOGY** [[paper](https://doi.org/10.65655/ocp.m30.c119)]
- [2026] **The AI Trias Politica: Redefining Roles in the Modern Workplace** *IFIP advances in information and communication technology* [[paper](https://doi.org/10.1007/978-3-032-41234-8_3)]
- [2026] **TRANSGENDER EMPLOYMENT LAW AND WORKPLACE INCLUSION IN CORPORATE INDIA** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23408877)]
- [2026] **Prompt Literacy as a Core Workplace Competency: Development of the Prompt Literacy Index (PLI-20) for Non-Technical Professionals** [[paper](https://doi.org/10.64823/ijstm.2601003)]
- [2026] **Employee Well-being and Mental Health: The Role of the Leader in Preventing Burnout, Promoting Psychological Safety, and Creating Mentally Healthy Workplaces** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23414274)]
- [2026] **Intersectionality, legitimacy and women's digital leadership in AI-enabled workplaces: a systematic review** *Equality Diversity and Inclusion An International Journal* [[paper](https://doi.org/10.1108/edi-02-2026-0125)]
- [2026] **Technostress in the Digital Workplace: A Systematic Literature Review of Antecedents, Employee Outcomes, and Mitigation Strategies** *Journal of Economic Education and Entrepreneurship Studies* [[paper](https://doi.org/10.62794/je3s.v7i5.515)]
- [2026] **From emergency telework to hybrid workplace learning: a systematic review of digital upskilling, organisational support and performance** *European journal of training and development* [[paper](https://doi.org/10.1108/ejtd-06-2026-0179)]
- [2026] **The Impact of Artificial Intelligence on Education and the Workplace: A Comprehensive Literature Review** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22705489)]
- [2026] **A Review of Employee Voice Literature: Evolving Models and Modern Workplace** *The European Proceedings of Social & Behavioural Sciences* [[paper](https://doi.org/10.15405/epsbs.2026.09.30)]
- [2026] **TRACING THE EVOLUTION OF WORKPLACE E-LEARNING TRANSFER RESEARCH: A BIBLIOMETRIC AND THEMATIC REVIEW** *International Journal of Modern Education* [[paper](https://doi.org/10.35631/ijmoe.831036)]
- [2026] **Employee silence and voice in AI-driven workplace learning: an integrative literature review** *European journal of training and development* [[paper](https://doi.org/10.1108/ejtd-05-2026-0142)]
- [2026] **AI AND AGEISM: DIGITAL EXCLUSION AND WORKPLACE CHALLENGES FOR OLDER INDIVIDUALS** *Akademi Sosyal Bilimler Dergisi* [[paper](https://doi.org/10.65083/asbider.1984719)]
- [2026] **AI-Human Collaborative Intervention Models in Workplace Mental Health: A Scoping Review Under the Stepped Care Framework** *Open Science Framework* [[paper](https://doi.org/10.17605/osf.io/x2wpe)]
- [2026] **USER EXPERIENCE (UX) AND BEHAVIORAL ADOPTION DRIVERS OF CORPORATE DIGITAL HEALTH PLATFORMS IN REMOTE-FIRST ORGANIZATIONS: IMPLICATIONS FOR NIGERIAN WORKPLACES** *Global Journal of Engineering and Technology Advances* [[paper](https://doi.org/10.30574/gjeta.2026.28.3.0237)]
- [2026] **Mapping and theorizing gig work and digital technology: A bibliometric and integrative review** *Digital Business* [[paper](https://doi.org/10.1016/j.digbus.2026.100187)]
- [2026] **Ethical Leadership and Gen Z Engagement in the Digital Era: A Systematic Review** *Jurnal Ilmiah Manajemen Kesatuan* [[paper](https://doi.org/10.37641/jimkes.v14i5.5454)]
- [2026] **The performative office: applying dramatic theory to workplace relationships and impression management** *Interpersona An International Journal on Personal Relationships* [[paper](https://doi.org/10.54899/iij.v20i1.1216)]
- [2026] **WORKPLACE INFORMATION PRACTICES IN HYBRID WORK: Fracture of the Information Landscape, Sensemaking, and Configuration Work** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23100030)]
- [2026] **Governing relational opportunity in hybrid work: structural relational deprivation and the reproduction of workplace inequality** *Frontiers in Sociology* [[paper](https://doi.org/10.3389/fsoc.2026.1955187)]
- [2026] **Linking Communication Systems to Employee Voice and Organizational Commitment: Evidence from Empirical Studies in Public and Private Workplaces** *IIARD INTERNATIONAL JOURNAL OF ECONOMICS AND BUSINESS MANAGEMENT* [[paper](https://doi.org/10.56201/ijebm.vol.11.no11.2025.pg224.235)]
- [2026] **ChatGPT and the digital humanities: A cross-domain review of human-AI collaboration in education, work, and culture, and the question of trust for advancing SDG 4** *Research Journal in Advanced Humanities* [[paper](https://royalliteglobal.com/advanced-humanities/article/view/2932)]
- [2026] **The algorithmic management paradox: a structured integrative review of perceived autonomy on performance in digital workplaces** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2026.1829522)]
- [2026] **Visual Presenteeism in the digital workplace: A scoping review of dry eye disease, digital eye strain and work productivity** *Journal of Medical and Biosciences Research.* [[paper](https://doi.org/10.70164/jmbr.v3i4.1298)]
- [2026] **Toward a multilevel understanding of knowledge hiding in digital workplaces: Insights and opportunities** *Technology in Society* [[paper](https://doi.org/10.1016/j.techsoc.2026.103524)]
- [2026] **Human Factors in Information Security: A Capability Framework for Administrative Professionals in the Digital Workplace** *WORLD JOURNAL OF INNOVATION AND MODERN TECHNOLOGY* [[paper](https://doi.org/10.56201/wjimt.v10.no5.2026.pg154.179)]
- [2026] **Counterproductive Work Behavior among Generation Z in The Workplace: A Systematic Literature Review** *Insight Jurnal Ilmiah Psikologi* [[paper](https://ejurnal.mercubuana-yogya.ac.id/index.php/psikologi/article/view/4739)]
- [2026] **The Impact of Digital Addiction on Employees’ Work Productivity: A Narrative Review** *Psychiatry International* [[paper](https://doi.org/10.3390/psychiatryint7040183)]
- [2026] **Human centered leadership strengthening employee adaptability through emotional intelligence and digital workplace collaboration during transformation** *Jurnal Indovisi* [[paper](https://doi.org/10.32698/19075408)]
- [2026] **Artificial Intelligence’s Transformative Impact on Management, Strategy, and Workplace Dynamics: A Systematic Literature Review** *JPAIR Multidisciplinary Research* [[paper](https://doi.org/10.7719/jpair.v66i1.1065)]
- [2026] **A Systematic Literature Review of School‑Workplace Integration within Vocational Education and Training (VET)** *International Journal of Education and Training (InjET)* [[paper](https://doi.org/10.47836/injet.12.2.05)]
- [2026] **Integrating Artificial Intelligence in the Workplace** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-2600-3570-2.ch004)]
- [2026] **Digital Detox and Employee Well-Being: A Systematic Literature Review** *CRC Press eBooks* [[paper](https://doi.org/10.1201/9781042025091-23)]
- [2026] **Driving sustainability and creativity at work: A review of the role of digital transformation, leadership, and culture** *Corporate Governance and Sustainability Review* [[paper](https://doi.org/10.22495/cgsrv10i3sip16)]
- [2026] **Facilitating Conflict Communication in Distributed Workplaces: A Systems-Informed Framework for Practice** *Applied Dispute Resolution Journal* [[paper](https://journals.calstate.edu/adrj/article/view/7495)]
- [2026] **AI-Powered Automation: Impact on the Future Workplace—Opportunities, Challenges, and Strategic Implications** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22043633)]
- [2026] **Occupational Medicine In The Prevention And Management Of Workplace Related Cancer: Mechanisms, Strategies And Emerging Challenges** *Adolescencia e Saude* [[paper](https://doi.org/10.67440/ahj.v21i5s.1473)]
- [2026] **Employee Resilience and Well-Being in the Era of Digital Transformation** *INTERNATIONAL JOURNAL OF SOCIAL SCIENCES AND MANAGEMENT RESEARCH* [[paper](https://doi.org/10.56201/ijssmr.vol.12no5.2026.pg197.207)]
- [2026] **Employee Engagement in the Hybrid Work Era: Exploring the Relationship between Leadership Styles and Workplace Productivity** *Natural Resources for Human Health* [[paper](https://doi.org/10.53365/nrfhh.944)]
- [2026] **Adaptive Stability and Workplace Culture Amid Continuous Technological Disruption** *International Journal of Service Science, Management, Engineering, and Technology* [[paper](https://ejournalisse.com/index.php/isse/article/view/278)]
- [2026] **Discourse, sentiment, and resonance of workplace burnout on Chinese social media: A computational analysis** *PLoS ONE* [[paper](https://doi.org/10.1371/journal.pone.0346396)]
- [2026] **HRM Practices, Employee Well-Being, and Workplace Incivility in Khyber Pakhtunkhwa’s Tourism Industry** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i8.171)]
- [2026] **Artificial Intelligence and Workplace Well-being: A Systematic Literature Review Following the PRISMA 2020 Protocol Balancing Organizational Health and Psychosocial Risk: Conditions for Responsible Adoption** *African Scientific Journal* [[paper](https://africanscientificjournal.com/index.php/AfricanScientificJournal/article/view/2111)]
- [2026] **Technostress and Burnout in Early-Career Employees: A Scoping Review of Digital Workload, Always-On Culture, and Burnout Risk in the Early Employment Phase** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21756657)]
- [2026] **Developing Digital Interactive Media for Writing Using LUMI for International Class Students** *JURNAL MULTIDISIPLIN ILMU AKADEMIK* [[paper](https://ejurnal.kampusakademik.co.id/index.php/jmia/article/view/12572)]
- [2026] **Leadership Challenges in Digital Work Environments: Current Issues and Future Directions** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21918433)]
- [2026] **Digital workplace competencies and their outcomes: A systematic literature review** *Technological Forecasting and Social Change* [[paper](https://doi.org/10.1016/j.techfore.2026.124832)]
- [2026] **AI governance and employee well-being in digital workplaces: A systematic literature review** *Digital Theory Culture & Society* [[paper](https://doi.org/10.61126/dtcs.v4i1.152)]
- [2026] **Fear of Digital Exclusion and Workplace Anxiety in Contemporary Organisations: A Conceptual Review and Research Agenda** *Intercontinental Journal of Social Sciences* [[paper](https://doi.org/10.62583/62fqcc68)]
- [2026] **EMPLOYEE ENGAGEMENT AS A MEDIATING MECHANISM BETWEEN PERCEIVED ORGANIZATIONAL SUPPORT AND JOB PERFORMANCE IN THE DIGITAL WORKPLACE: A SYSTEMATIC LITERATURE REVIEW** *Jurnal Manajemen Terapan dan Keuangan* [[paper](https://doi.org/10.22437/jmk.v15i03.58896)]
- [2026] **Loneliness in Digital Workplaces: Antecedents, Outcomes, and a Typology of Work Configurations** *Complex Systems Informatics and Modeling Quarterly* [[paper](https://doi.org/10.7250/csimq.2026-47.01)]
- [2026] **The Digital Mindfulness Scale: Development and Longitudinal Validation in the Workplace, 2025** *UK Data Archive* [[paper](https://doi.org/10.5255/ukda-sn-858653)]
- [2026] **Generation Z’s Resilience in The Workplace: A Systematic Literature Review** *Journal Of Social Research* [[paper](https://doi.org/10.55324/josr.v5i8.3368)]
- [2026] **The digital mindfulness scale: Development and longitudinal validation in the workplace** *Computers in Human Behavior* [[paper](https://doi.org/10.1016/j.chb.2026.109124)]
- [2026] **HR Challenges in Industry 5.0 and Smart Workplaces: A Review of Emerging Issues and Future Directions** *International Journal of Economics and Business Management Research* [[paper](https://doi.org/10.64137/31079423/ijebmr-v2i3p101)]
- [2026] **Unveiling the Dark Side of Workplace Connectivity** *Golden Ratio of Mapping Idea and Literature Format* [[paper](https://doi.org/10.52970/grmilf.v6i3.2474)]
- [2026] **Mental Health Psychology in a Biopsychosocial Perspective: Applications in Family, Workplace, Education, Older Adults, and Digital Technology** *International Journal of Natural and Health Sciences* [[paper](https://doi.org/10.59890/ijnhs.v4i3.292)]
- [2026] **Assessment and Development of Soft Skills for Workplace Internships in Vocational Education and Training: A Systematic Literature Review** *Administrative Sciences* [[paper](https://doi.org/10.3390/admsci16070318)]
- [2026] **Small Firms, Big Shifts: A Systematic Review of How Hybrid Work Redefines the Small-and-Medium-Enterprise Workplace** *Administrative Sciences* [[paper](https://doi.org/10.3390/admsci16070346)]
- [2026] **Systematic review of mobile applications for workplace mental health and psychological well-being in Spain: study protocol** [[paper](https://osf.io/ueg2w)]
- [2026] **What Research Tells Us about Digital Video Genres: A Scoping Review** *Journal of Communication Language and Culture* [[paper](https://doi.org/10.33093/jclc.2026.6.2.10)]
- [2026] **Navigating Employee Well-Being in the Age of Digital Transformation: A PRISMA-Based Systematic Review** *Societies* [[paper](https://doi.org/10.3390/soc16070213)]
- [2026] **Digital Leadership, Employee Competence, and Employee Performance in Private Companies: An Integrative Literature Review** *ENDLESS International Journal of Future Studies* [[paper](https://endless-journal.com/index.php/endless/article/view/398)]
- [2026] **Digital leadership in the era of digital transformation** *International Journal of Educational Administration Management and Leadership* [[paper](https://doi.org/10.51629/ijeamal.v6i2.321)]
- [2026] **Workplace Communication, Leadership Language, and Soft Skills Training in Saudi Organizational Development** *Iconic Research and Engineering Journals* [[paper](https://doi.org/10.64388/irev10i1-1719742)]
- [2026] **Preventing workplace aggression through a multi-actor perspective: bridging the gap between evidence and public policies** *Evidence & Policy* [[paper](https://doi.org/10.1332/17442648y2026d000000100)]
- [2026] **The Influence of Career Sensing Agility, Digital Literacy, and Psychological Capital on Career Adaptability among Oil and Gas Industry Employees: A Systematic Literature Review** *Dinasti International Journal of Management Science* [[paper](https://doi.org/10.38035/dijms.v7i6.7065)]
- [2026] **Integrating Artificial Intelligence into Workplace Conflict Management: A Socio-Technical Justice Framework for HR Policy, Ethical Governance, and Capability Development** *Administrative Sciences* [[paper](https://doi.org/10.3390/admsci16070327)]
- [2026] **English Proficiency and Job Opportunities in Digital Era: A Bridge or a Barrier?** *Journal of Advanced Multidisciplinary Research* [[paper](https://doi.org/10.30659/jamr.7.1.11-21)]
- [2026] **Revisitando el constructo entorno digital de trabajo** *Sociologia del trabajo/Sociología del trabajo* [[paper](https://doi.org/10.5209/stra.108247)]
- [2026] **Psychological Safety as a Strategic Driver of Knowledge-Based Innovation in the Digital Economy** *Inisiatif Jurnal Ekonomi Akuntansi dan Manajemen* [[paper](https://doi.org/10.30640/inisiatif.v5i3.6887)]
- [2026] **Online Vigilance and Digital Well-Being: Exploring the Roles of Digital Anxiety and Availability Norms in Knowledge Work** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i7.109)]
- [2026] **Digital workplace technologies and tacit knowledge sharing on employees’ digital competency: A systematic review** *Edelweiss Applied Science and Technology* [[paper](https://doi.org/10.55214/2576-8484.v10i6.12960)]
- [2026] **Electronic Performance Monitoring in the Digital Workplace: an Updated Systematic Literature Review (2016–2026)** *Community Engagement and Emergence Journal (CEEJ)* [[paper](https://journal.yrpipku.com/index.php/index/article/view/11315)]
- [2026] **CHAPTER 2: PREPARING HEALTH PROFESSIONALS for WORKPLACE VIOLENCE: A SYSTEMATIC REVIEW of DIGITAL SIMULATION-BASED TRAINING INTERVENTIONS** *Axiom Academic Publishers.* [[paper](https://doi.org/10.62869/001c.162831)]
- [2026] **Workplace Risks for IT Professionals Associated with Barriers to Healthy Behavior: A Review of International Research in the Context of the Healthy Workplace Model** *Вестник Российского университета дружбы народов. Серия: Психология и педагогика* [[paper](https://doi.org/10.22363/2313-1683-2025-22-4-671-691)]
- [2026] **Reimagining Workplace Learning: Artificial Intelligence, Digital Ecosystems, and Emerging Talend Development Practices** *Digital Education Review* [[paper](https://doi.org/10.1344/der.2026.49.1-12)]
- [2026] **Human-Centered Leadership and Employee Well-Being: Evidence from the Digital Workplace** *Maneggio* [[paper](https://ejournal-nawalaedu.com/index.php/MJ/article/view/2786)]
- [2026] **Peer Review Report For: A Systematic Literature Review and Bibliometric Analysis of Workplace Coaching [version 2; peer review: 3 approved]** [[paper](https://doi.org/10.5256/f1000research.198611.r480892)]
- [2026] **Humanoid robots with embedded intelligence: A comprehensive review on challenges, opportunities, and workplace applications** *ChemRxiv* [[paper](https://doi.org/10.26434/chemrxiv.15004244/v1)]
- [2026] **Employee Well-Being di Era Digital Workplace: Tinjauan Literatur Sistematis tentang Kesehatan, Keterikatan, dan Produktivitas Pegawai** *El-Mal Jurnal Kajian Ekonomi & Bisnis Islam* [[paper](https://doi.org/10.47467/elmal.v7i6.12837)]
- [2026] **Employee Well-being Challenges in the Digital Era: A Review of Digital Stress** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22193409)]
- [2026] **Emotional AI in the Workplace: Systematic Review of Effects on Employee Well-Being, Productivity, and Organizational Performance** *International Journal of Combinatorial Optimization Problems and Informatics.* [[paper](https://doi.org/10.61467/2007.1558.2026.v17i3.1398)]
- [2026] **Effects, Competence, Adoption, and Agency as Approaches to Digital Inclusion and Learning at Work: Research Review, Finland** *innsbruck university press* [[paper](https://doi.org/10.15203/99106-195-3-08)]
- [2026] **The Transformation of Human Resources Management in Dealing with Generation Z in the Workplace** *Maneggio* [[paper](https://ejournal-nawalaedu.com/index.php/MJ/article/view/2760)]
- [2026] **When AI Becomes the Boss: Algorithmic Management, Digital Workplace Surveillance, and AI-Induced Job Insecurity as Determinants of Employee Psychological Well-Being** *Contemporary Issues in Social Sciences and Management Practices* [[paper](https://doi.org/10.61503/cissmp.v5i2.420)]
- [2026] **Review of Digital Transformation in Management Control Systems: Challenges, Strategic Opportunities, and Organizational Adaptation** *Jurnal Profesi Dan Manajemen Pendidikan* [[paper](https://doi.org/10.63987/jpmp.v1i2.322)]
- [2026] **Self-Efficacy and Innovation Performance in The Contemporary Workplace: A Systematic Literature Review and Future Research Agenda** *American Journal of Economic and Management Business (AJEMB)* [[paper](https://doi.org/10.58631/ajemb.v5i6.483)]
- [2026] **A Scoping Review of Burnout, Digital Workload, and Technostress Among Nurses in the Post-Pandemic Era** *International Journal of Drug Delivery Technology* [[paper](https://doi.org/10.25258/ijddt.16.46s.64)]
- [2026] **WORKFORCE INTERACTION IN THE DIGITAL ERA** *ACCENT JOURNAL OF  ECONOMICS ECOLOGY  & ENGINEERING* [[paper](https://ajeee.co.in/index.php/ajeee/article/download/6565/5327)]
- [2026] **Impact of artificial intelligence and work digitalization on mental health and occupational well-being: a scoping review** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1857108)]
- [2026] **REIMAGINING WOMEN'S EMPOWERMENT THROUGH HYBRID WORK: IMPLICATIONS FOR EMPLOYEE WELL-BEING AND WORKPLACE MORALE** *ACCENT JOURNAL OF  ECONOMICS ECOLOGY  & ENGINEERING* [[paper](https://ajeee.co.in/index.php/ajeee/article/download/6398/5220)]
- [2026] **Computer Operating and Programming Assistant (COPA) Training and Economic Upliftment of Persons with Disabilities in India: A Systematic Review of Employability, Digital Inclusion and Livelihood Opportunities** *International Journal of Economic Social Science and Management LAW* [[paper](https://ijeml.com/journal/index.php/ijeml/article/view/750)]
- [2026] **Peer Review Report For: Digitalization of Indonesian State-Owned Enterprises (SOEs) and Employee Mental Health: Mitigating Digital Anxiety in Finance Functions [version 2; peer review: 1 approved, 2 approved with reservations]** [[paper](https://doi.org/10.5256/f1000research.197977.r487968)]
- [2026] **Ergonomic and Digital Interventions to Support Occupational Safety, Health, and Work Ability Among Older Workers** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21001527)]
- [2026] **DIGITAL TECHNOLOGY AND COMMUNICATION IN THE MODERN WORKPLACE: A CONCEPTUAL REVIEW** *African Journal of Social and Behavioural Sciences* [[paper](https://journals.aphriapub.com/index.php/AJSBS/article/view/3714)]
- [2026] **GEN Z AND PSYCHOLOGICAL CRISIS IN THE MODERN WORKPLACE: A NARRATIVE REVIEW** *Tạp chí Y học Cộng đồng* [[paper](https://doi.org/10.52163/yhc.v67ie1.5286)]
- [2026] **Always Online: Communication Fatigue, Workplace Stress, and Sustainable Digital Communication Practices in Hybrid Organizations** *Journal of Computers and Applications* [[paper](https://doi.org/10.58613/jca212)]
- [2026] **Peer Review Report For: A Systematic Literature Review and Bibliometric Analysis of Workplace Coaching [version 2; peer review: 2 approved]** [[paper](https://doi.org/10.5256/f1000research.198611.r480897)]
- [2026] **An Overview of the Applications and Conditions for Using Artificial Intelligence and Digitalization in Occupational Health and Safety in the Workplace** *بهداشت و ایمنی کار* [[paper](https://doi.org/10.18502/jhsw.v15i3.21422)]
- [2026] **A bibliometric review on digital inclusion and inequalities at work: Scope and future perspectives** *African Quarterly Social Science Review* [[paper](https://doi.org/10.51867/aqssr.3.2.28)]
- [2026] **Organizational Culture Adaptation in Banking Workplaces in the FinTech Era: A Systematic Review of Transformation Strategies** *Tasharruf Journal of Islamic Economics and Business* [[paper](https://doi.org/10.55757/tasharruf.v7i1.1309)]
- [2026] **Exploring ways to support university teachers’ identity and agency in uncertain times: a literature review adopting Illeris’ workplace learning framework** *The International Journal for Academic Development* [[paper](https://doi.org/10.1080/1360144x.2026.2675016)]
- [2026] **Humans as Objects and Subjects in Digital Human Resource Management: A Systematic Literature Review** *JURISMA Jurnal Riset Bisnis & Manajemen* [[paper](https://doi.org/10.34010/jurisma.v16i1.19070)]
- [2026] **Technology-driven workplace transformation: changes, challenges, and opportunities** *Management & Sustainability An Arab Review* [[paper](https://doi.org/10.1108/msar-08-2025-0295)]
- [2026] **Application of Health Informatics in Workplace Violence Surveillance and Prevention in Nursing Practice: Implications for Low-Resource Settings** *Iconic Research and Engineering Journals* [[paper](https://doi.org/10.64388/irev9i10-1716914)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **DIGITAL PLATFORMS, INDUSTRY 4.0, AND REGIONAL ECONOMIC RESILIENCE: RECOVERY PATHWAYS AND POLICY IMPLICATIONS FROM THE SYSTEMATIC LITERATURE REVIEW** *Acta Innovations* [[paper](https://doi.org/10.62441/actainnovations.v63i.1365)]
- [2026] **Digital disconnection: A systematic review of phubbing behavior** *Acta Psychologica* [[paper](https://doi.org/10.1016/j.actpsy.2026.107559)]
- [2026] **Mental Health and Well-Being in the Digital Health Care Workplace: A Multilevel Systematic Review** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.15190abstract)]
- [2026] **Systematic Review and Distillation of Guidelines for the Implementation and Deployment of Augmented Workplace Systems** *Research Square* [[paper](https://doi.org/10.21203/rs.3.rs-9192938/v1)]
- [2026] **AN OBSERVATORY STUDY ON DIGITAL HR ECOSYSTEMS: FROM E-HRM TO SMART WORKPLACES** *Iterative International Publishers eBooks* [[paper](https://doi.org/10.58532/nbennurnhhrb2p3c1)]
- [2026] **Virtual Workplace and Employee Engagement** *Journal of Fundamental & Applied Business Research* [[paper](https://doi.org/10.70623/pewy7418)]

[⬆ Back to top](#paper-list)

#### Survey

##### 2026

- [2026] **Digital Workplace Technologies and the Inclusion of Disabled Workers: A Realist Review and Synthesis of Evidence and Workers' Perspectives** *New Technology Work and Employment* [[paper](https://doi.org/10.1111/ntwe.70042)]
- [2026] **TACIT KNOWLEDGE TRANSFER IN WORKPLACE LEARNING: A SCOPING REVIEW OF HUMAN-CENTRED PRACTICES, DIGITAL SUPPORT, AND RESEARCH GAPS** *EDULEARN proceedings* [[paper](https://doi.org/10.21125/edulearn.2026.0805)]
- [2026] **Addressing workplace practices: combating the rising prevalence of computer vision syndrome** *Annals of Medicine and Surgery* [[paper](https://doi.org/10.1097/ms9.0000000000005204)]
- [2026] **Adaptabilitas Generasi Z dalam Menghadapi Era Disrupsi Digital Menuju Indonesia Emas 2045: Literatur Review** *Figshare* [[paper](https://doi.org/10.6084/m9.figshare.32825015)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **Workplace Wearables and Digital Labor Surveillance: Managerial Control, Psychosocial Risk, and Data Governance** *Fiscaoeconomia* [[paper](https://doi.org/10.25295/fsecon.1993638)]
- [2026] **Strategi dan Faktor Protektif dalam Manajemen Stres akibat Workplace telepressure: Systematic Literature Review** *Arus Jurnal Psikologi dan Pendidikan.* [[paper](https://doi.org/10.57250/ajpp.v5i3.3441)]
- [2026] **Technostress and Work- Family Balance in the Digital Workplace: A Systematic Literature Review and Future Research -Underlying Data** *OSF Preprints (OSF Preprints)* [[paper](https://osf.io/kb76r)]
- [2026] **Technostress and Work- Family Balance in the Digital Workplace: A Systematic Literature Review and Future Research Agenda-Extended Data** *OSF Preprints (OSF Preprints)* [[paper](https://osf.io/cbzdv)]
- [2026] **Transformational Leadership and Employee Engagement: A Systematic Review in the Digital Age** *Greenation International Journal of Economics and Accounting* [[paper](https://doi.org/10.38035/gijea.v4i4.1086)]
- [2026] **AI TOOLS IN THE WORKPLACE: PRODUCTIVITY GAINS, DESKILLING RISKS AND THE ROLE OF CONTINUOUS EMPLOYEE EDUCATION** *SCIENCE International Journal* [[paper](https://doi.org/10.35120/sciencej0503369p)]
- [2026] **Workplace Interventions to Improve Physical Activity, Reduce Sedentary Behavior, and Promote Healthy Diet Among Employees in Low- and Middle- Income Countries: A Systematic Review** *Research Square* [[paper](https://doi.org/10.21203/rs.3.rs-9730653/v1)]
- [2026] **A Literature Review on the Impact of Digital Hindrance Stressors on Employees' Psychological Need Satisfaction** *Academic journal of management and social sciences* [[paper](https://doi.org/10.54097/fmpy4s62)]
- [2026] **Mapping the digital landscape of competency recognition: findings from a systematic review of RPL tools and practices** *R-libre (Université Téluq)* [[paper](https://r-libre.teluq.ca/4127/1/Mapping_the_Digital_Landscape_of_Competency_Recognition_.pdf)]

[⬆ Back to top](#paper-list)

### Methods

#### Method

##### 2026

- [2026] **Enriching Learning at Work Through the Inclusive Use of Digital Technologies and Innovation** *VETNET Conference Series* [[paper](https://doi.org/10.21240/vetcon/2026/ecer/80)]
- [2026] **Teacher-Facing Generative AI and Workplace Mental Health in Higher Education: Perceived Demands and Resources** *Mental Health Global Challenges Journal* [[paper](https://doi.org/10.56508/mhgcj.v9i1.374)]
- [2026] **A PRELIMINARY STUDY OF AI-BASED PSYCHIATRIC COUNSELLING TO MANAGE EMPLOYEES STRESS AND TO ASSESS WORKPLACE MENTAL HEALTH BY THE END OF THIS DECADE (2030)** *Advances in Clinical Medical Research* [[paper](https://doi.org/10.5281/zenodo.23333736)]
- [2026] **From classroom confidence to workplace readiness: Reimagining future skills development in higher education** *Futures* [[paper](https://doi.org/10.1016/j.futures.2026.103950)]
- [2026] **CHALLENGES AND SOLUTIONS IN PREPARING EDUCATION BACHELORS FOR WORKPLACE-BASED PROFESSIONAL ACTIVITIES: INSIGHTS FROM UZBEKISTAN** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20668491)]
- [2026] **Assessing digital technology use for clinical learning in undergraduate health professional education in Ethiopia** *African Journal of Health Professions Education* [[paper](https://doi.org/10.7196/ajhpe.2026.v18i3.4489)]
- [2026] **‘Is This the Workplace for Me?’ A Qualitative Study of Nursing Students' Construction of Workplace Attractiveness in Clinical Placement** *Nursing Open* [[paper](https://doi.org/10.1002/nop2.70868)]
- [2026] **Healthcare Practitioners' Perspectives on the Integration of Digital Health Education in Undergraduate Curricula: A Workforce-Readiness Mixed-Methods Study** *Research Square* [[paper](https://doi.org/10.21203/rs.3.rs-10854277/v1)]
- [2026] **A Smartphone-Based Ecological Momentary Intervention for Workplace Mental Health: Randomized Controlled Trial** *JMIR mhealth and uhealth* [[paper](https://doi.org/10.2196/72435)]
- [2026] **WORKPLACE GYMNASTICS AS A PREVENTIVE STRATEGY FOR NECK AND LOWER BACK PAIN COMPLAINTS IN WORKERS OF AN AGRO-INDUSTRIAL COOPERATIVE IN THE CITY OF CARAMBEÍ – PR** *Revista Ação Ergonômica* [[paper](https://doi.org/10.4322/rae.v20n1.e202606.en)]
- [2026] **Communication Barriers in Digital Interaction among IT Company Employees** *Общество социология психология педагогика* [[paper](https://doi.org/10.24158/spp.2026.8.6)]
- [2026] **Implementation of Port Operations Digitalization at the Talang Duku Port Container Terminal Jambi** *Dinasti International Journal of Economics Finance & Accounting* [[paper](https://doi.org/10.38035/dijefa.v7i4.7352)]
- [2026] **PENGARUH WORKLOAD TERHADAP TECHNOSTRESS PADA PEKERJA DI BIDANG INDUSTRI MULTIMEDIA KREATIF DIGITAL** *Pendas Jurnal Ilmiah Pendidikan Dasar* [[paper](https://journal.unpas.ac.id/index.php/pendas/article/view/63328)]
- [2026] **Workplace violence from the ambulance personnel’s perspective, a qualitative study** *Scandinavian Journal of Trauma Resuscitation and Emergency Medicine* [[paper](https://doi.org/10.1186/s13049-026-01680-8)]
- [2026] **Psychological barriers to technology acceptance in South African workplaces: Investigating socio-economic status as a moderator** *SA Journal of Industrial Psychology* [[paper](https://doi.org/10.4102/sajip.v52i0.2342)]
- [2026] **Burden of workplace stress on employee performance: job satisfaction as a mediator among online food-delivery workers in Ayodhya** *International Journal of Financial Management and Economics* [[paper](https://doi.org/10.33545/26179210.2026.v9.i8.922)]
- [2026] **Prevalence and Patterns of Workplace Violence among Psychiatric Nurses in a Tertiary Neuropsychiatric Hospital in Southeast Nigeria** *Journal of Public Health Policy and Society* [[paper](https://doi.org/10.54117/afnczt98)]
- [2026] **Adoption of Digital Dentistry in Restorative Practice in Saudi Arabia: A Step Toward Healthcare Digitalization** *Journal of Contemporary Dental Sciences* [[paper](https://doi.org/10.4103/jcds.jcds_17_26)]
- [2026] **Digital Health Competence and Attitudes Toward AI Among Health Care Professionals: Convergent Mixed Methods Study** *Journal of Medical Internet Research* [[paper](https://doi.org/10.2196/96170)]
- [2026] **The mediating role of social appearance anxiety in the relationship between instagram social comparison and cosmetic surgery acceptance: Implications for workplace wellbeing** *Work* [[paper](https://doi.org/10.1177/10519815261478115)]
- [2026] **EFL Learners’ English Engagement in LinkedIn-Based Professional Digital Practices: Exploring Career-Oriented Motivation** *IJORER International Journal of Recent Educational Research* [[paper](https://doi.org/10.46245/ijorer.vi.1540)]
- [2026] **Mixed-Method Process Evaluation of a Mobile Technology-Based Tailored Workplace Health Promotion Program** *Advances in Nursing Science* [[paper](https://doi.org/10.1097/ans.0000000000000655)]
- [2026] **G²LM|LIC - LinkinOut Harassment: A Targeted Social Media Experiment to Reduce Workplace Harassment towards Women** [[paper](https://doi.org/10.15185/glmlic.1048.1)]
- [2026] **Acquisition of workplace knowledge through individual and cooperative self-regulated learning** *International Journal of Mechanical Engineering Education* [[paper](https://doi.org/10.1177/03064190261468488)]
- [2026] **Digital Literacy, Access, Training, and Attitudes Toward Digital Health Technologies among Healthcare Workers in Selected Health Facilities in Port Harcourt, Nigeria: A Cross-Sectional Study** *Archives of Current Research International* [[paper](https://doi.org/10.9734/acri/2026/v26i82067)]
- [2026] **Digital-Based Work Environment to Improve the Performance of MSMES Employees in the City of Malang** *IC-ITECHS* [[paper](https://doi.org/10.32664/9mqqch82)]
- [2026] **ANALISIS KOMPETENSI DIGITAL MAHASISWA TEKNOLOGI PENDIDIKAN SETELAH MENGIKUTI PROGRAM MAGANG STUDI INDEPENDEN BERSERTIFIKAT DI PUSBANGKOM DPR RI** *Pendas Jurnal Ilmiah Pendidikan Dasar* [[paper](https://journal.unpas.ac.id/index.php/pendas/article/view/62250)]
- [2026] **Workplace Safety Training Videos: Improve Employee Learning, Compliance & Safety Culture** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20793368)]
- [2026] **Adaptation of Generation Z Employees to Artificial Intelligence in the Workplace Implications for HR Management** *Jurnal Nasional Manajemen Pemasaran & SDM* [[paper](https://doi.org/10.47747/jnmpsdm.v7i2.3435)]
- [2026] **DIGITAL TECHNOLOGY INTEGRATION IN TEXT-BASED ENGLISH FOR FRONT OFFICE INSTRUCTION IN VOCATIONAL TOURISM EDUCATION: A MIXED METHOD STUDY** *LANGUAGE LITERACY Journal of Linguistics Literature and Language Teaching* [[paper](https://doi.org/10.30743/ll.v10i1.13245)]
- [2026] **ASSESSING BUSINESS ENGLISH COMMUNICATION SKILLS THROUGH DIGITAL TASKS** *IJEE (Indonesian Journal of English Education)* [[paper](https://doi.org/10.15408/ijee.v13i1.50509)]
- [2026] **IMPROVING EFL LEARNERS’ SPEAKING PROFICIENCY THROUGH ROLE PLAY AND DIGITAL MEDIA** *JEE (Journal of English Education)* [[paper](https://doi.org/10.30606/jee.v12i1.4375)]
- [2026] **Strengthening Civil Servants' Digital Talent Through Peer Learning: Building Digital Champions as the Foundation of Agile Government in North Pontianak District, Pontianak City, West Kalimantan Province** *Golden Ratio of Community Services and Dedication* [[paper](https://doi.org/10.52970/grcsd.v6i2.2487)]
- [2026] **Utilizing Digital Transformation for Enhancing Service Delivery in Well Construction Oil & Gas** *Midocean Journal for Research and Studies* [[paper](https://doi.org/10.71335/kzbjqt90)]
- [2026] **Physiotherapists Experience With and View on Digital Health Technologies; a Qualitative Study From Norway (Preprint)** [[paper](https://doi.org/10.2196/preprints.105613)]
- [2026] **E-recruitment Vs. Poaching in Recruitment: a Comparative Analysis of Digital Efficiency and Ethical Considerations** *International Journal For Multidisciplinary Research* [[paper](https://doi.org/10.36948/ijfmr.2026.v08i03.80192)]
- [2026] **Generation Z Work Experience In The Digital Workplace** *Journal of Business Management* [[paper](https://doi.org/10.70963/jbusman.v2i2.767)]
- [2026] **PUBLIC SPEAKING 5.0: EFFECTIVE COMMUNICATION TRAINING FOR GEN Z IN THE COMPETITIVE DIGITAL WORKPLACE** *IRPITAGE JOURNAL* [[paper](https://radjapublika.com/index.php/IRPITAGE/article/view/5622)]
- [2026] **AN EMPIRICAL ANALYSIS: WORK–LIFE IMBALANCE AND ORGANISATIONAL WORKPLACE CULTURE AMONG BANKING EMPLOYEES IN THENI DISTRICT** *JOURNAL OF MANAGEMENT* [[paper](https://doi.org/10.34218/jom_13_02_001)]
- [2026] **Addressing Cyberloafing through Gamification Strategy to Increase Productivity in the Digital Era** *Journal of Indonesian Economy and Business* [[paper](https://doi.org/10.22146/jieb.v41i2.11620)]
- [2026] **Transformasi dan Tantangan Karir di Era Digital: Strategi dan Pendekatan Bimbingan Karir** *Jurnal Konseling Komprehensif Kajian Teori dan Praktik Bimbingan dan Konseling* [[paper](https://doi.org/10.36706/jkk.v13i1.30)]
- [2026] **Empowering Batik Bambu Mujur MSMEs with Smart Canting, Production Ergonomics, Digital Management, and Marketing 4.0** *Engagement Jurnal Pengabdian Kepada Masyarakat* [[paper](https://engagement.fkdp.or.id/index.php/engagement/article/view/2255)]
- [2026] **When digital systems meet human-centred work: a qualitative study of information behaviour** *Information Research* [[paper](https://doi.org/10.47989/ir31isic65231)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **INSTRUCTIONAL DESIGN OF A WORKPLACE-ORIENTED GENERAL AIGC COURSE IN THE ERA OF DIGITAL INTELLIGENCE** *Educational research and human development.* [[paper](https://doi.org/10.61784/erhd3064)]
- [2026] **Explainable AI for resource-aware intervention prioritization of digital burnout in healthcare workplaces** *Health Information Science and Systems* [[paper](https://doi.org/10.1007/s13755-026-00485-4)]
- [2026] **RELEVANCE OF TRADITIONAL HR METHODS IN THE CONTEMPORARY WORKPLACE: ADVOCATING FOR A HYBRID HUMAN-CENTRIC MODEL** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.18139718)]
- [2026] **From curriculum to career: Aligning English communication skills with hiring and workplace success** *International Journal of Advanced Academic Studies* [[paper](https://doi.org/10.33545/27068919.2026.v8.i10a.2189)]
- [2026] **Digital Ethnography of Workers' Inquiry** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003677604-11)]
- [2026] **Digital Transformation in Service Professions** *VETNET Conference Series* [[paper](https://doi.org/10.21240/vetcon/2026/ecer/68)]
- [2026] **Empowering Workplace Communication: Collaborative Strategies for a Productive and Harmonious Work Environment Among Indonesian Muslim Migrant Workers in Malaysia** *Indonesian Journal of Devotion and Empowerment* [[paper](https://doi.org/10.15294/ijde.v1i1.34792)]
- [2026] **How employees appropriate AI in the workplace: Effects of task characteristic and organizational culture** *Technological Forecasting and Social Change* [[paper](https://doi.org/10.1016/j.techfore.2026.124932)]
- [2026] **The Human Side of Algorithmic Management: Exploring How Employees Negotiate AI-Driven Performance Monitoring, Autonomy, Privacy, and Workplace Trust** *Journal of Business Insight and Innovation* [[paper](https://doi.org/10.63544/jbii.v5i10.263)]
- [2026] **Exploring Digital Competence Configurations and Attention Performance Through fsQCA and Machine Learning** *Journal of Computing & Biomedical Informatics* [[paper](https://doi.org/10.56979/1201/2026/1624)]
- [2026] **Digital competence and AI readiness among nurses: lessons for public health workforce training** *European Journal of Public Health* [[paper](https://doi.org/10.1093/eurpub/ckag169.501)]
- [2026] **Fostering a human-centric, age-inclusive workplace in the digital era** *Industrial and Commercial Training* [[paper](https://doi.org/10.1108/ict-07-2025-0095)]
- [2026] **Personality Recognition Based on Digital Footprints for Better Online Workplace** *Communications in computer and information science* [[paper](https://doi.org/10.1007/978-3-032-27235-5_56)]
- [2026] **How Digital Technology–Business Strategy Alignment Translates into Firm Performance: The Roles of Digital Experience Support and Digital Talent Capacity in a Mixed-Method Study** *OSF Preprints (OSF Preprints)* [[paper](https://osf.io/eg49c)]
- [2026] **Transforming Emotional Well-being in the Workplace** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003587712-12)]
- [2026] **Associations between home, workplace, and third-place satisfaction and mental health among young adults: a sequential mixed-methods study in Greater Jakarta** *Cities & Health* [[paper](https://doi.org/10.1080/23748834.2026.2731786)]
- [2026] **The impact of perceived algorithmic management on employees' physical and mental health: a chain mediation analysis of frustrated work autonomy and workplace AI replacement anxiety** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1877221)]
- [2026] **Social isolation, loneliness, and unsafe behavior in the digital environment** *Journal of Modern Foreign Psychology* [[paper](https://doi.org/10.17759/jmfp.2026150302)]
- [2026] **When Technology is Not Enough: Understanding Employee Trust Formation Through Digital HR Practices and Inclusion Climate** *Inkubis Jurnal Ekonomi dan Bisnis* [[paper](https://doi.org/10.59261/inkubis.v8i3.418)]
- [2026] **DEVELOPMENT OF A WEBSITE-BASED OCCUPATIONAL SAFETY EDUCATIONAL MEDIUM TO ENHANCE KNOWLEDGE REGARDING WORKPLACE ACCIDENT PREVENTION** *Bulletin of Engineering Science Technology and Industry* [[paper](https://bestijournal.org/index.php/go/article/view/257)]
- [2026] **FROM ACTIVITY-BASED WORKPLACES TO PUBLIC EMPLOYEE PERFORMANCE: DIGITALIZATION AS THE MEDIATING MECHANISM** *Jurnal Ilmiah Ilmu Terapan Universitas Jambi|JIITUJ|* [[paper](https://doi.org/10.22437/jiituj.v10i4.57236)]
- [2026] **Causal Mobility Profiles of Digital-Nomad Adaptation across City and Workplace Contexts** *International Journal of Quantitative and Qualitative Research* [[paper](https://ijqqr.com/index.php/ijqqr/article/view/74)]
- [2026] **Digital strain in the workplace: the role of instrumental social platform use on employee emotional exhaustion** *Frontiers in Sociology* [[paper](https://doi.org/10.3389/fsoc.2026.1878074)]
- [2026] **Industry-Academy-Research-Government-Bank-Enterprise-Guarantee under Digital Talent Service: Workplace Psychological Matching, Mental Health, Talent Retention and Innovation Output** *Schizophrenia Bulletin* [[paper](https://doi.org/10.1093/schbul/sbag159.118)]
- [2026] **Digital Literacy and Knowledge Sharing Among Young Professionals: A Mixed-Methods Study** *European Conference on Knowledge Management* [[paper](https://doi.org/10.34190/eckm.27.1.5023)]
- [2026] **The Digital Work Capacity Index: A Framework for Phenotyping Digital Work (Preprint)** [[paper](https://doi.org/10.2196/preprints.110155)]
- [2026] **Transformative Education in the Digital Age: Evaluating the Impact of Digital Literacy Training on Graduate Employability in Kenya** *Journal of Education Management and Leadership (JEML)* [[paper](https://doi.org/10.51317/jeml.v5i1.1102)]
- [2026] **The Relevance of Islamic Leadership For Generation Z in The Digital Era** *Jurnal Ekonomika dan Bisnis Islam* [[paper](https://doi.org/10.26740/jekobi.v9n2.p22-39)]
- [2026] **Employee Well-being and Organizational Performance in the Post-Pandemic Workplace: An Empirical Analysis of Hybrid Work Models, Psychological Safety, and Engagement** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21739085)]
- [2026] **The Impact of Artificial Intelligence on Business Communication and Managerial Decision-Making in the Digital Economy** *Minnesota Journal of Business Law and Entrepreneurship* [[paper](https://kommerstad.org/journal/article/view/886)]
- [2026] **Can a Digital Provider Tame the In-Basket? A Multisite Evaluation** *ScholarWorks -A service of University of Vermont Libraries (University of Vermont)* [[paper](https://hdl.handle.net/20.500.14849/10677)]
- [2026] **Office workers’ perspectives on implementing active breaks supported by a digital intervention to alleviate spinal pain: a qualitative study** *Brazilian Journal of Physical Therapy* [[paper](https://doi.org/10.1016/j.bjpt.2026.101634)]
- [2026] **Factors Influencing Career Development in a Digitally Transforming Workplace** *MARGINAL JOURNAL OF MANAGEMENT ACCOUNTING GENERAL FINANCE AND INTERNATIONAL ECONOMIC ISSUES* [[paper](https://doi.org/10.55047/marginal.v5i3.2320)]
- [2026] **Cross-cultural impact of information anxiety on employee mental health in digital workplaces: a comparative study between Chinese and Western contexts** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2026.1775912)]
- [2026] **The Relationship Between School Principals’ Toxic Leadership Behaviours and Teachers’ Exposure to Workplace Cyberbullying** *Journal of School Leadership* [[paper](https://doi.org/10.1177/10526846261474282)]
- [2026] **Positioning AI-Driven Technologies as Support for Effective Workplace Collaborations: A Study Based on the Oil and Gas Sector in the United Arab Emirates (UAE)** *Array* [[paper](https://doi.org/10.1016/j.array.2026.101077)]
- [2026] **Industrial-organisational psychologists’ evolving role in workplace counselling: A cross-temporal qualitative study in South Africa (2023–2024)** *SA Journal of Industrial Psychology* [[paper](https://doi.org/10.4102/sajip.v52i0.2442)]
- [2026] **The Role of Digital Affordance on the Hospitality Employees’ Well-Being** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.14102abstract)]
- [2026] **The discourse of ‘beast of burden’ (niuma) on Xiaohongshu: A critical analysis of digital labor and self-deprecation** *Discourse Context & Media* [[paper](https://doi.org/10.1016/j.dcm.2026.101047)]
- [2026] **Pengaruh Penggunaan Artificial Intelligence terhadap Kinerja Karyawan di Era Transformasi Digital** *Jurnal Manajemen dan Ekonomi Kreatif* [[paper](https://doi.org/10.59024/jumek.v4i3.792)]
- [2026] **Determinants of implementation success for a digital single-session intervention for workplace mental health: Mixed methods evaluation in a cluster trial** *Internet Interventions* [[paper](https://doi.org/10.1016/j.invent.2026.100970)]
- [2026] **Dynamic Capability Framework for Digital Workplaces and Innovation Driven Performance** *Aptisi Transactions On Technopreneurship (ATT)* [[paper](https://doi.org/10.34306/att.v8i2.1004)]
- [2026] **Connectivity expectations as psychological contract terms in the digital workplace** *Frontiers in Psychology* [[paper](https://doi.org/10.3389/fpsyg.2026.1852486)]
- [2026] **Bridging the Electronic Surveillance Gap: A Comparative Legal Analysis of Workplace Privacy in the Digital Age.** *F1000Research* [[paper](https://doi.org/10.12688/f1000research.182428.1)]
- [2026] **When machines join the team: how AI digital employee integration reshapes organizational boundaries and collective dynamics in the digital workplace** *Internet Research* [[paper](https://doi.org/10.1108/intr-08-2025-1244)]
- [2026] **Investigating Workplace Mistreatment Through the Lens of Various Actors : Exploring Incivility in Physical and Digital Meetings: Associations with Work Motivation and Social Support** *Lund University Publications (Lund University)* [[paper](https://lup.lub.lu.se/record/a3d33fac-2d1d-4d32-b4b6-d665cec69775)]
- [2026] **Global perspectives: Doing LGBTQ+ workplace research in the Middle East** *Edward Elgar Publishing eBooks* [[paper](https://doi.org/10.4337/9781035336807.00019)]
- [2026] **DEVELOPMENT OF BACK-ON-LINETM, DIGITAL INTERVENTION TO SUPPORT SELF-MANAGEMENT OF LOW BACK PAIN IN WORKPLACE, USING CO-PRODUCTION AND NORMALISATION PROCESS THEORY** *World Physiotherapy Congress Archive* [[paper](https://doi.org/10.82161/jrmc-fb56)]
- [2026] **Empathetic leadership in the age of AI: humanizing the algorithmic workplace** *Strategy and Leadership* [[paper](https://doi.org/10.1108/sl-12-2025-0437)]
- [2026] **Male Greeting Practices in Iraqi Culture: Workplace Etiquette and Generational Variation from a Linguistic Perspective** *International Journal of Educational Sciences and Arts* [[paper](https://doi.org/10.59992/ijesa.2026.v5n6p2)]
- [2026] **Gendering Digitalization: Technology Change in Feminized Supermarket Work** *Gender Work and Organization* [[paper](https://doi.org/10.1111/gwao.70206)]
- [2026] **The Impact of Digital Technologies on Skills‐to‐Job Mismatches** *New Technology Work and Employment* [[paper](https://doi.org/10.1111/ntwe.70036)]
- [2026] **The Effect of Digital Literacy on Employee Performance at LLDIKTI Region X Padang** *Journal of Multidisciplinary Science MIKAILALSYS* [[paper](https://doi.org/10.58578/mikailalsys.v4i2.10487)]
- [2026] **A framework for assessing the impact of digital twin on cognitive ergonomics** *International Journal of Industrial Ergonomics* [[paper](https://doi.org/10.1016/j.ergon.2026.103992)]
- [2026] **MENEMBUS SEKAT DIGITAL DENGAN MEMBERDAYAKAN SPIRITUALITAS PADA GURU DAN TENAGA KEPENDIDIKAN** *Jurnal Abdimas Musi Charitas* [[paper](https://doi.org/10.32524/jamc.v10i1.2040)]
- [2026] **The Impact of Artificial Intelligence Knowledge and Perception on Accounting Students' Career Readiness in the Digital Era** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21030160)]
- [2026] **Digital Transformation and Circular Economy Integration for Triple Bottom Line Performance in Industrial Companies** *International Journal of Leading Research Publication.* [[paper](https://doi.org/10.70528/ijlrp.v7.i6.2254)]
- [2026] **The Mediating Role of Digital Readiness in Human Capital Strategy and Employability Skills of Vocational Students** *Journal of Vocational Informatics and Computer Education* [[paper](https://doi.org/10.66053/voice.v4i2.932)]
- [2026] **Role of the Environment Digital Work and Career Development on Employee Performance with Organizational Commitment as Intervening Variables** *PESHUM Jurnal Pendidikan Sosial dan Humaniora* [[paper](https://doi.org/10.56799/peshum.v5i4.16957)]
- [2026] **Driving the Green Transition in the Digital Economy: How Leader Prosocial Motivation and Workplace Digitalization Shape Employee Green Innovation Intention** *Sustainability* [[paper](https://doi.org/10.3390/su18094600)]
- [2026] **AI embeddedness and employee job crafting in the digital workplace: A cross-level study based on cognitive appraisal theory** *International Journal of Information Management* [[paper](https://doi.org/10.1016/j.ijinfomgt.2026.103086)]
- [2026] **Leveraging AI deployment and mindful workplace on employee body and mental wellness** *Cogent Business & Management* [[paper](https://doi.org/10.1080/23311975.2026.2674264)]
- [2026] **A mixed methods study of sexual harassment attitudes across generational cohorts and gender and how these variables relate to prevention and intervention efforts in the workplace.** *UTC Scholar (University of Tennessee at Chattanooga)* [[paper](https://scholar.utc.edu/theses/1057)]
- [2026] **Design and evaluation of educational animation to enhance professional ethics and employee performance in the workplace** *ECOBIZTECH Journal of Economics Business and Technology* [[paper](https://doi.org/10.65881/ecobiztech.v1i2.60)]
- [2026] **Entrepreneurial and servant leadership in knowledge sharing: unveiling the roles of psychological safety and workplace bullying** *The Learning Organization* [[paper](https://doi.org/10.1108/tlo-03-2025-0078)]
- [2026] **Role Perceptions and Workplace Challenges Among Oncology Nurses: A Comparative Study of Türkiye and Australia** *Seminars in Oncology Nursing* [[paper](https://doi.org/10.1016/j.soncn.2026.152243)]
- [2026] **“It Is Comparison That Makes People Miserable”: Enterprise Social Media Visibility, Social Comparison Orientation, and Workplace Impostor Thoughts** *Behavioral Sciences* [[paper](https://doi.org/10.3390/bs16050782)]
- [2026] **Generative AI in the workplace: how job demands and resources influence employee innovative performance – a JD-R theory perspective** *European Journal of Innovation Management* [[paper](https://doi.org/10.1108/ejim-11-2025-1496)]
- [2026] **Contextual ESP Learning Through Digital Comics in Occupational Safety and Health Education** *PROJECT (Professional Journal of English Education)* [[paper](https://journal.ikipsiliwangi.ac.id/project/article/view/19167)]
- [2026] **The Future of Work in the Age of Ai and Automatlon: A Christian Criticism of Digital Capitalism** *Scholar Commons (Santa Clara University)* [[paper](https://scholarcommons.scu.edu/jst_dissertations/170)]
- [2026] **Assessing nurses’ digital competence for public health systems: validation of a brief instrument and factors associated with competence** *Frontiers in Public Health* [[paper](https://doi.org/10.3389/fpubh.2026.1808439)]
- [2026] **Legal Issues Facing the Termination of Employment Contracts in the Digital Work Environment: A Descriptive and Analytical Study** *Majallah al-dawlīyah lil-buḥūth wa-al-dirāsāt al-qānūnīyah =* [[paper](https://doi.org/10.59992/ijlrs.2026.v5n5p10)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **Dynamic in Situ Assessment of Work Load: Multi-platform Integration in Digital Ergonomics** *Mobile Networks and Applications* [[paper](https://doi.org/10.1007/s11036-026-02554-0)]

[⬆ Back to top](#paper-list)

#### Evaluation

##### 2026

- [2026] **Optimizing Radiation Oncology Workplace Productivity and Well-Being Through Digital Media: A Performance Evaluation of the "Time Titans" Podcast** *International Journal of Radiation Oncology*Biology*Physics* [[paper](https://doi.org/10.1016/j.ijrobp.2026.06.1018)]
- [2026] **Optimizing Radiation Oncology Workplace Productivity and Well-being through Digital Media: A Performance Evaluation of the 'Time Titans' Podcast** *International Journal of Radiation Oncology*Biology*Physics* [[paper](https://doi.org/10.1016/j.ijrobp.2026.04.073)]

[⬆ Back to top](#paper-list)

### Tooling & Platforms

#### Method

##### 2026

- [2026] **Workplace, Corporate & Digital Culture Lexicon: Algorithmic and Online Pragmatics (SlangLane Volume 2)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23544770)]
- [2026] **NeuralCoach: a Smartphone-Based Brain-Computer Interface for Workplace Well-Being and Safety** *HAL* [[paper](https://hal.science/hal-05772549v1)]
- [2026] **Planning for platform urbanism** *plaNext - Next Generation Planning* [[paper](https://doi.org/10.24306/plnxt/130)]
- [2026] **Streamlining Workplace Milestone Celebrations in Digital Research Environments** *Figshare* [[paper](https://doi.org/10.6084/m9.figshare.33288000)]
- [2026] **Financial Precarity in the Platform Economy: An Empirical Analysis of Algorithmic Strain, Earnings Volatility and Financial Well-Being among Gig Workers** *International Journal of Advanced Research in Commerce Management & Social Science* [[paper](https://doi.org/10.62823/ijarcmss/9.3(ii).9291)]
- [2026] **AI-Driven Inclusive Employment Platform for Elderly and Persons with Disabilities: Enhancing Job Matching and Workplace Accessibility** *IC-ITECHS* [[paper](https://doi.org/10.32664/gamqmk47)]
- [2026] **The Relationship between Digitalization and the Labor Market: A Bibliometric Analysis** *Annals of Faculty of Economics* [[paper](https://doi.org/10.47535/1991auoes35(1)001)]
- [2026] **Hostile Algorithms: Platform Labour and the Digital Bordering of West African and Moroccan Migrant Workers in Post-Brexit London** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21842443)]
- [2026] **Digital Communication Tools and Preferences in the Work Environment** *Media Literacy and Academic Research* [[paper](https://doi.org/10.34135/mlar-26-01-13)]
- [2026] **Role of Digital Training and Development in Enhancing Employee Performance** *International Scientific Journal of Engineering and Management* [[paper](https://doi.org/10.55041/isjem07118)]

[⬆ Back to top](#paper-list)

#### Theory

##### 2026

- [2026] **Crowd Discrimination in the Digital Workplace: How AI and Platforms Translate Public Bias into Employment Practices** *SMU Law Review* [[paper](https://doi.org/10.25172/smulr.79.3.8)]
- [2026] **Rethinking Continuance Intentions in the AI-Augmented Digital Workplace** *Journal of Computer Information Systems* [[paper](https://doi.org/10.1080/08874417.2026.2745888)]
- [2026] **Employee narcissism and online workplace interpersonal capitalization: insights from trait activation theory** *Baltic Journal of Management* [[paper](https://doi.org/10.1108/bjm-02-2026-0147)]
- [2026] **Economic Disempowerment and Workplace Harassment: A Critical Analysis of Female Gig Workers’ Working Conditions in Indonesia** *Journal of Contemporary Asia* [[paper](https://doi.org/10.1080/00472336.2026.2742934)]
- [2026] **Digital Employee Experience in the Era of Artificial Intelligence** *Advances in computational intelligence and robotics book series* [[paper](https://doi.org/10.4018/979-8-2600-4780-4.ch007)]
- [2026] **Technology-Facilitated and Face-to-Face Workplace Sexual Harassment Perpetration: Prevalence, Predictors, and Perpetration Patterns** *Journal of Interpersonal Violence* [[paper](https://doi.org/10.1177/08862605261490516)]
- [2026] **Design and Construction of a Virtual‐Simulation Training Platform for Basic Nursing Techniques** *Medicine insights.* [[paper](https://soapubs.com/index.php/MI/article/view/3021)]
- [2026] **Platformed affective withdrawal: Quiet quitting and the refusal of gendered emotional labour on TikTok** *New Media & Society* [[paper](https://doi.org/10.1177/14614448261488701)]
- [2026] **DIGITAL TRANSFORMATION AND THE EVOLUTION OF EMPLOYMENT MODELS: CHALLENGES AND OPPORTUNITIES FOR EMERGING ECONOMIES** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.23658168)]
- [2026] **Digital communication and occupational well-being in 25 European countries** *Cognition Technology & Work* [[paper](https://doi.org/10.1007/s10111-026-00902-4)]
- [2026] **Production or Extraction: The Dual Logic of Platform Economy in Reshaping Urban Space** *Journal of Education Humanities and Social Sciences* [[paper](https://doi.org/10.54097/zenwd135)]
- [2026] **What Drivers Want vs. What Drivers Take: A Worker-Centered View of Fairness in Ridehail Platforms** *Proceedings of the AAAI/ACM Conference on AI Ethics and Society* [[paper](https://doi.org/10.1609/aies.v9i1.43178)]
- [2026] **Women Workers in the Gig Economy in India: A Study of Employment Insecurity, Gender Wage Disparities, and Workplace Harassment** [[paper](https://doi.org/10.66788/9788168611320/8)]
- [2026] **Yoga-based workplace health promotion: an organizational framework for employee well-being and sustainable workplace performance** *PHINISI* [[paper](https://doi.org/10.64282/phi.v3i3.134)]
- [2026] **What constitutes a comprehensive workplace-based assessment programme?** [[paper](https://doi.org/10.4102/aosis.2026.bk586.02)]
- [2026] **Engagement to Quiet Quitting: The Workplace Behavior Life Cycle and the Re-stabilization of the Effort Bargain** *DergiPark (Istanbul University)* [[paper](https://dergipark.org.tr/en/pub/ssad/article/1984961)]
- [2026] **SafeVoice-AI-Release: An Artificial Intelligence-Based Early Intervention Ecosystem for Workplace Psychosocial Risk Management** *International Journal of Academic Research in Business and Social Sciences* [[paper](https://doi.org/10.6007/ijarbss/v16-i9/28926)]
- [2026] **Digital Communication, Information Overload and Telework Stress in Nigeria: A Critical Appraisal** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22262367)]
- [2026] **DIGITAL INTERRUPTIONS, ATTENTIONAL FATIGUE, AND SELF-REGULATION IN HYBRID WORK ENVIRONMENTS** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22696725)]
- [2026] **Data Privacy And Reputational Harm (Privacy In The Digital Age)** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22879697)]
- [2026] **Managerial Buffering and the Sustainability Paradox: How Intermediary Organizations Shape the Social Sustainability of Platform Labor** *Sustainability* [[paper](https://doi.org/10.3390/su18189416)]
- [2026] **Emotional Intelligence and Quality of Work Life in Digital Workplaces: A Conceptual Framework Integrating Digital Work Stress and Digital Resilience** *Minnesota Journal of Business Law and Entrepreneurship* [[paper](https://doi.org/10.52783/mjble.759)]
- [2026] **Workplace Conflict And Job Satisfaction In Digital Learning Institutions: Moderating Role Of Professional Ethics** *Adolescencia e Saude* [[paper](https://doi.org/10.67440/ahj.v21i5s.1300)]
- [2026] **REMOTE WORK AND THE EXPANDING SCOPE OF THE POSH ACT: WORKPLACE SAFETY IN THE DIGITAL ERA** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21851499)]
- [2026] **The Mediating Role of Communication Quality in Digital Platform Usage and Interpersonal Interaction** *International Journal of Computer Information Systems and Industrial Management Applications* [[paper](https://doi.org/10.70917/ijcisim-2026-4408)]
- [2026] **Governing artificial intelligence-enabled labour surveillance: A multi-level framework for legal, organisational and collective governance in the digital workplace** *Journal of Industrial Relations* [[paper](https://doi.org/10.1177/00221856261478209)]
- [2026] **Employee Voice in Digital Service Platform Environments: The Roles of Perceived Digital System Support and Psychological Empowerment** *Behavioral Sciences* [[paper](https://doi.org/10.3390/bs16091466)]
- [2026] **Industrial Democracy as a Strategic Framework for Overcoming Organizational Conflict in the Global Workplace** *INTERNATIONAL JOURNAL OF SOCIAL SCIENCES AND MANAGEMENT RESEARCH* [[paper](https://doi.org/10.56201/ijssmr.vol.12no1.2026.pg166.172)]
- [2026] **‘ A Legal Whack‐a‐Mole’ . Escaping the Rider Law in Spain: Platform Strategies and the Hollowing of Enforcement Under Platform Capitalism** *New Technology Work and Employment* [[paper](https://doi.org/10.1111/ntwe.70043)]
- [2026] **Impact of E-Learning Platforms on Skills Development and Engagement in Corporate Setting** *Psychology and Education A Multidisciplinary Journal* [[paper](https://doi.org/10.70838/pemj.620104)]
- [2026] **Gamifying Workplaces: Applying AI-driven Esports and Sports Simulation Models to Boost Employee Motivation, Engagement, and Psychological Well-being** *Emerald Group Publishing Limited eBooks* [[paper](https://doi.org/10.1108/978-1-80686-125-520261011)]
- [2026] **The Impact of Digital Technologies on Labour Laws and Gig Economy Workers’ Rights** *American Journal of Multidisciplinary AI & Technology* [[paper](https://doi.org/10.66572/ajomait.2026.v5.i12.83752)]
- [2026] **Study on Employee Well-being in the Digital Gig Economy: Challenges, Opportunities, and Emerging Perspectives** *International Journal For Multidisciplinary Research* [[paper](https://doi.org/10.36948/ijfmr.2026.v08i04.85557)]
- [2026] **Digital AI Revolution Changing the Pace of Work Culture in IT And Telecom Industry: India** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22732374)]
- [2026] **Enhancing Service Quality Through Digital Learning: Evidence from Typsy-Based Training in the Hotel Industry** *Eduvest - Journal Of Universal Studies* [[paper](https://doi.org/10.59188/eduvest.v6i8.53348)]
- [2026] **DEVELOPMENT OF AN AI-BASED DHAMMA TIKTOK PLATFORM INSPIRED BY BUDDHIST TEACHINGS TO PROMOTE PSYCHOLOGICAL RESILIENCE AMONG THE WORKFORCE** *Journal of Buddhist Anthropology* [[paper](https://so04.tci-thaijo.org/index.php/JSBA/article/view/288614)]
- [2026] **Menopause in the French Workplace: Embodiment, Regulation, and Digital Resistance** *Gender Work and Organization* [[paper](https://doi.org/10.1111/gwao.70224)]
- [2026] **Driving Job Satisfaction in the Evolving Digital Banking Workplace through Employee Empowerment** *South Asian Journal of Social Studies and Economics* [[paper](https://doi.org/10.9734/sajsse/2026/v23i71354)]
- [2026] **Humanity Lost and Found: Workplace Dehumanization in the Age of Algorithms and AI** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.18117symposium)]
- [2026] **From flexibility to friction: intended and unintended consequences of hot-desking in workplaces** *Journal of Enterprise Information Management* [[paper](https://doi.org/10.1108/jeim-01-2026-0092)]
- [2026] **Affect and Belonging in the Workplace: Dynamics of Sensemaking in Hybrid Work** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.13991poster)]
- [2026] **The digital sublime and the hidden abode** *Repository of the University of Ljubljana (University of Ljubljana)* [[paper](https://repozitorij.uni-lj.si/IzpisGradiva.php?id=185096)]
- [2026] **Evaluasi Usability Aplikasi Zoom Workplace Berdasarkan Model Nielsen Menggunakan Pendekatan PLS-SEM** *Figshare* [[paper](https://doi.org/10.6084/m9.figshare.32881652)]
- [2026] **Digital Health and Emotional Resilience in Global Markets** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-3373-8357-6.ch017)]
- [2026] **Beyond The Platform: Algorithmic Control Spillover Into Gig Workers’ Family Deviance** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.283bp)]
- [2026] **When Online Support Is Not Enough: Digital Sensemaking and the Limits of Collective Coping** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.21564abstract)]
- [2026] **Task design and job performance in the hybrid workplace: the moderating role of paradox mindset** *Personnel Review* [[paper](https://doi.org/10.1108/pr-04-2025-0356)]
- [2026] **ARTIFICIAL INTELLIGENCE-ASSISTED BEHAVIORAL HEALTH ANALYTICS OF IT EMPLOYEES USING DIGITAL INTERACTION DATA** *Transformative Education A Multidisciplinary Journal* [[paper](https://temjournals.com/temj/index.php/index/article/view/661)]
- [2026] **Knowledge sharing and telework in the new workplace: The role of organizational support in shaping employee outcomes** *German Journal of Human Resource Management Zeitschrift für Personalforschung* [[paper](https://doi.org/10.1177/23970022261460618)]
- [2026] **Interrupted but Activated: How Digital Work Interruptions Drive Innovation and Well-Being** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.16780abstract)]
- [2026] **Impact of Remote Work Platform Adoption and Employee Job Performance in Polytechnics in Benue State, Nigeria: A Conceptual Review** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21628495)]
- [2026] **Business Plan for a Gamified Digital Platform for Occupational Health and Safety, eLearning, and Workplace Well-Being** *Repositorio Académico UPC (Universidad Peruana de Ciencias Aplicadas)* [[paper](https://hdl.handle.net/10757/691790)]
- [2026] **Consent, Privacy and the Digital Employee: Ethical Boundaries of AI Data Collection in Workplace Learning Platforms** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20638887)]
- [2026] **The Impact of Generative AI on Knowledge Creation and Retention: Strategies for the Modern Digital Workplace** *OTS Canadian Journal* [[paper](https://doi.org/10.58840/r3h00k79)]
- [2026] **Visibility by Design: How HRM Architectural Choices Shape Workplace Relationships in Digitally Surveilled Environments** *Human Resource Management Journal* [[paper](https://doi.org/10.1111/1748-8583.70053)]
- [2026] **Performing the Workplace: Self-Presentation of Workplace Vloggers from the Perspective of Dramaturgical Theory** *Social Sciences and Humanities* [[paper](https://doi.org/10.63313/ssh.9109)]
- [2026] **Organizational Citizenship Behavior in AI-Driven Workplaces: Effects of Transformational Leadership and Digital Work Self-Efficacy** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20586994)]
- [2026] **Beyond Individual Vulnerability: A European, Critical Work and Organizational Psychology Perspective on Work Addiction in the Digital Workplace.** [[paper](https://doi.org/10.31235/osf.io/t7ha2_v1)]
- [2026] **Between freedom and fatigue: reimagining workplace happiness in the modern gig workforces** *Journal of Management Development* [[paper](https://doi.org/10.1108/jmd-11-2025-0631)]
- [2026] **LATEST TRENDS IN REWARD SYSTEMS: AN EMPIRICAL STUDY OF HYPER-PERSONALIZATION, DIGITAL PLATFORMS, AND THE MONETARY VERSUS NON-MONETARY REWARD DICHOTOMY** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20846655)]
- [2026] **Artificial Intelligence and Employee Well-being: Strengthening Mental Health for Sustainable and Resilient Workplaces** *Routledge eBooks* [[paper](https://doi.org/10.1201/9781042005550-23)]
- [2026] **Motivational Ergonomics in Gamified and Artificial Intelligence-Supported Learning: An ARCS Study with Implications for Workplace Training** [[paper](https://doi.org/10.35542/osf.io/g4bek_v1)]
- [2026] **Analisis Implementasi Layanan Digital Dan Manajemen Arsip** *EMASHA Jurnal Ekonomi Manajemen dan Akuntansi Syariah* [[paper](https://doi.org/10.35961/emasha.v3i1.2968)]
- [2026] **INNOVATIVE APPROACHES TO TRAINING AND DEVELOPMENT IN THE MODERN WORKPLACE AT CREAMLINE DAIRY PRODUCTS LIMITED** *American Journal of Management and IOT Medical Computing* [[paper](https://ajmimc.com/journal/index.php/ajmimc/article/view/375)]
- [2026] **Occupational Safety and Health Education ODA for Migrant Workers to Mitigate the Migrantisation of Risk : Focusing on the 4th Master Plan for International Development Cooperation and an AI‑Based Digital Safety Education Platform** *Forum of Public Safety and Culture* [[paper](https://doi.org/10.52902/kjsc.2026.55.381)]
- [2026] **Employee Digital Well-Being, Work-Life Balance And Productivity** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22199262)]
- [2026] **GIG ECONOMY WORKERS AND LABOUR PROTECTION IN INDIA: REIMAGINING EMPLOYMENT RIGHTS IN THE DIGITAL AGE** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.21182395)]
- [2026] **Training Communication Through Tools Designing the TIEC Model for Real-World Digital Environments** *IGI Global eBooks* [[paper](https://doi.org/10.4018/979-8-3373-4647-2.ch008)]
- [2026] **Digital Organisational Identity in the Hybrid Workplace** *Routledge eBooks* [[paper](https://doi.org/10.4324/9781003752165-1)]
- [2026] **Right to Disconnect: Employee Well-being and Legal Awareness in the Digital Workplace** *International Journal of Advanced Research in Commerce Management & Social Science* [[paper](https://doi.org/10.62823/ijarcmss/09.02(i).8899)]
- [2026] **Digital Workplace Communication: Collaboration, Morale, and Inclusion in Hybrid and Neurodiverse Work Environments** *ThinkTech (Texas Tech University)* [[paper](https://hdl.handle.net/2346/109241)]
- [2026] **Sexual Harassment in The Digital Era in IT Sectors** *CRC Press eBooks* [[paper](https://doi.org/10.1201/9781003771104-83)]
- [2026] **Digital Communication and Its Impact on Human Relationships, Society, and Technology** *International Journal for Research in Applied Science and Engineering Technology* [[paper](https://doi.org/10.22214/ijraset.2026.83002)]
- [2026] **Artificial Intelligence, Digitalization, and Smart Carbon Capture Systems** [[paper](https://doi.org/10.1002/9781394436408.ch17)]
- [2026] **EFFECT OF DIGITAL BURNOUT ON EMPLOYEE RETENTION: A CONCEPTUAL FRAMEWORK** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.19974552)]
- [2026] **Role of Artificial Intelligence in Shaping Employee Happiness and Employee Engagement in the Digital Economy- A Conceptual Approach** *International Journal on Research and Development - A Management Review* [[paper](https://doi.org/10.65521/ijrdmr.v15i1.2853)]
- [2026] **Future of Work, Learning and Innovation in the Digital Era** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20377874)]
- [2026] **AI-Powered Cloud Platform and Employee Job Performance in the Construction Industry: A Conceptual Framework** *International Journal of Academic Research in Business and Social Sciences* [[paper](https://doi.org/10.6007/ijarbss/v16-i5/28125)]
- [2026] **Delegation and Retention of Public Functions in the Digital Environments for Career Adaptation of War Veterans** *State Formation* [[paper](https://doi.org/10.26565/1992-2337-2026-1-24)]
- [2026] **Synergising Employer Branding with Sustainable Leadership and Employee Performance in the Digital Era** *Journal of Modern Management & Entrepreneurship* [[paper](https://doi.org/10.62823/jmme/16.02.8892)]
- [2026] **Manage One AI: A Unified AI-Driven Productivity and Collaboration Platform for Intelligent Task and Workflow Management** *International Research Journal on Advanced Engineering and Management (IRJAEM)* [[paper](https://doi.org/10.47392/irjaem.2026.0235)]

[⬆ Back to top](#paper-list)

#### Application

##### 2026

- [2026] **GIG-OSH Stock-Taking Report. Regulating Occupational Safety and Health in the Platform Economy** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.22255051)]
- [2026] **Streamlining Smart HR Digital Platform to Refine Staff Satisfaction and Retention in MTUN Institutions** *Journal of Human Development and Communication (JoHDeC)* [[paper](https://doi.org/10.58915/johdec.v15.2026.3439)]
- [2026] **AI POWERED RISK ASSESSMENT PLATFORM FOR WORKPLACE SAFETY** *International Journal of Drug Delivery Technology* [[paper](https://doi.org/10.25258/ijddt.16.46s.111)]
- [2026] **Digital carbon platforms enable measurable demand-side mitigation: evidence from large-scale behavioral data** *Environmental Research Letters* [[paper](https://doi.org/10.1088/1748-9326/ae7815)]
- [2026] **Responsibly adopting workplace mental well-being platforms** *Journal of Responsible Technology* [[paper](https://doi.org/10.1016/j.jrt.2026.100168)]
- [2026] **Impact Of Digital Workload On Employee Stress Management: An Empirical Study** *International Journal of Research Publication and Reviews* [[paper](https://doi.org/10.55248/gengpi.07.0526.c1338)]
- [2026] **An Examination of Customer Perceptions of Online Food Delivery Platforms in the Klang Valley, Malaysia** *International Journal of Academic Research in Economics and Management Sciences* [[paper](https://doi.org/10.6007/ijarems/v15-i2/28020)]
- [2026] **E-commerce as a battlefield in the US–China tech race: Effects on the global workplace in Brazil** *Journal of Industrial Relations* [[paper](https://doi.org/10.1177/00221856261454712)]

[⬆ Back to top](#paper-list)

#### Systems

##### 2026

- [2026] **Dismantling the Digital Nudge: A Three-Arm Pragmatic Randomized Controlled Trial Evaluating Individual, Competitive, and Collaborative WhatsApp-Driven Gamification to Disrupt Workplace Sedentary Behavior.** *Open Science Framework* [[paper](https://doi.org/10.17605/osf.io/gzdra)]
- [2026] **Socializing Our Research: Using Team Communication Platforms to Build Collaboration and Professionalization in Early-Career Researchers** *ACM International Conference on Design of Communication (SIGDOC)* [[paper](https://doi.org/10.1145/3772063.3841679)]
- [2026] **Digital Detox: Reducing Screen Time and Improving Mental Health** *JOURNAL OF ADVANCE AND FUTURE RESEARCH* [[paper](https://doi.org/10.56975/jaafr.v4i9.514626)]
- [2026] **PENGARUH WORKPLACE FRIENDSHIP, KERJASAMA TIM, DAN MOTIVASI KERJA TERHADAP KINERJA KARYAWAN PADA PT ADHITAMA MITRA NUSANTARA DI SIDOARJO** *Gemah Ripah* [[paper](https://doi.org/10.69957/grjb.v6i03.3043)]
- [2026] **Beyond Bullying: Digital Platforms, Power and the New Landscape of Violence Against Nurses** *Issues in Mental Health Nursing* [[paper](https://doi.org/10.1080/01612840.2026.2676205)]
- [2026] **Digital Transformation of Work: The Rise of Post-Human Entanglements in the Civil Service** *Academy of Management Proceedings* [[paper](https://doi.org/10.5465/amproc.2026.17882abstract)]
- [2026] **Roads as means of production and a class construct: Ethnographic perspective on value creation in food delivery gig platforms** *Urban Studies* [[paper](https://doi.org/10.1177/00420980261466165)]
- [2026] **Workplace Telepressure and Cognitive Load in MSME Online Entrepreneurs: A Relationship Study** *Zenodo (CERN European Organization for Nuclear Research)* [[paper](https://doi.org/10.5281/zenodo.20596660)]
- [2026] **Sociocultural adaptation in the transnational lives of newcomer migrant adolescents: Digital social networking practices and sociodemographic factors shaping adaptive performance in school and workplace settings** *International Journal of Intercultural Relations* [[paper](https://doi.org/10.1016/j.ijintrel.2026.102464)]
- [2026] **Direct and Indirect Platform Labour: Cleaning for Short-Term Rental (STR) platforms** *TSpace (University of Toronto)* [[paper](https://hdl.handle.net/1807/153620)]
- [2026] **Affective (non)sense-making: Digital nonsense, precarity, and the affective rhetoric of “Crazy Literature”** *International Journal of Cultural Studies* [[paper](https://doi.org/10.1177/13678779261462580)]
- [2026] **Technology Adaptation Patterns and Third-Level Digital Divide: Analyzing Workplace Communication at PT. Pesta Pora Abadi** *INJECT (Interdisciplinary Journal of Communication)* [[paper](https://doi.org/10.18326/inject.v11i2.6824)]

[⬆ Back to top](#paper-list)

#### Evaluation

##### 2026

- [2026] **Adult mental health in digital environments: workplace overload, social comparison, relationships and clinical assessment** *Clinics in Integrated Care* [[paper](https://doi.org/10.1016/j.intcar.2026.100337)]

[⬆ Back to top](#paper-list)

<!-- END PAPER LIST -->

<!-- BEGIN CORPUS STATISTICS -->

## 📊 Corpus Statistics

**1363 papers** across **14 categories**.  
Sources: **arXiv** 271 (20%).  

### Top categories

| Category | Papers | Recent | |
|----------|--------|--------|-|
| adoption-change | **191** | 191 | ████████████ |
| evaluation | **164** | 164 | ██████████░░ |
| public-sector | **153** | 153 | ██████████░░ |
| survey | **151** | 151 | █████████░░░ |
| interoperability | **129** | 129 | ████████░░░░ |
| open-source | **120** | 115 | ████████░░░░ |
| method | **118** | 118 | ███████░░░░░ |
| tooling | **112** | 112 | ███████░░░░░ |
| collaboration | **73** | 73 | █████░░░░░░░ |
| data-sovereignty | **57** | 45 | ████░░░░░░░░ |
| identity-access | **40** | 40 | ███░░░░░░░░░ |
| security-compliance | **26** | 26 | ██░░░░░░░░░░ |
| digital-workplace | **23** | 7 | █░░░░░░░░░░░ |
| sme-adoption | **6** | 6 | █░░░░░░░░░░░ |

### By year

| Year | Papers | |
|------|--------|-|
| 2005 | 1 | █░░░░░░░░░░░ |
| 2007 | 1 | █░░░░░░░░░░░ |
| 2011 | 1 | █░░░░░░░░░░░ |
| 2013 | 1 | █░░░░░░░░░░░ |
| 2016 | 3 | █░░░░░░░░░░░ |
| 2017 | 5 | █░░░░░░░░░░░ |
| 2018 | 3 | █░░░░░░░░░░░ |
| 2019 | 1 | █░░░░░░░░░░░ |
| 2020 | 4 | █░░░░░░░░░░░ |
| 2021 | 2 | █░░░░░░░░░░░ |
| 2022 | 1 | █░░░░░░░░░░░ |
| 2023 | 4 | █░░░░░░░░░░░ |
| 2024 | 3 | █░░░░░░░░░░░ |
| 2025 | 37 | █░░░░░░░░░░░ |
| 2026 | 1296 | ████████████ |

### Momentum (hottest categories)

| Category | Total | Rate | Recent | Score |
|----------|-------|------|--------|-------|
| Open Source | 120 | 9.6/mo | 96% | 11496 |
| Digital Workplace | 23 | 0.6/mo | 30% | 280 |
| Adoption Change | 191 | 15.9/mo | 100% | 100 |
| Collaboration | 73 | 6.1/mo | 100% | 100 |
| Evaluation | 164 | 13.7/mo | 100% | 100 |
| Identity Access | 40 | 3.3/mo | 100% | 100 |
| Interoperability | 129 | 10.8/mo | 100% | 100 |
| Method | 118 | 9.8/mo | 100% | 100 |
| Public Sector | 153 | 12.8/mo | 100% | 100 |
| Security Compliance | 26 | 2.2/mo | 100% | 100 |
| Sme Adoption | 6 | 0.5/mo | 100% | 100 |
| Survey | 151 | 12.6/mo | 100% | 100 |
| Tooling | 112 | 9.3/mo | 100% | 100 |
| Data Sovereignty | 57 | 3.8/mo | 79% | 79 |

### Trending keywords

| Keyword | Papers | Burst |
|---------|--------|-------|
| workplace | 964 | 1.02 |
| platform | 456 | 1.02 |
| review | 388 | 1.02 |
| education | 283 | 1.02 |
| evaluation | 220 | 1.02 |
| adoption | 182 | 1.02 |
| survey | 163 | 1.02 |
| security | 161 | 1.02 |

### Top venues

| Venue | Papers |
|-------|--------|
| Zenodo (CERN European Organization for Nuclear Research) | 129 |
| Academy of Management Proceedings | 15 |
| Frontiers in Public Health | 14 |
| Routledge eBooks | 13 |
| Advances in computational intelligence and robotics book series | 11 |
| Journal of Business Insight and Innovation | 11 |
| Iterative International Publishers eBooks | 10 |
| Frontiers in Psychology | 9 |
| IGI Global eBooks | 9 |
| MED | 8 |

### Research gaps (thinnest cells)

| Cell | Papers |
|------|--------|
| `identity-access/method` | 1 |
| `evaluation/evaluation` | 1 |
| `digital-workplace/systems` | 1 |
| `data-sovereignty/method` | 1 |
| `identity-access/application` | 1 |

*Generated 2026-10 by `scripts/standard_stats.py`.*

<!-- END CORPUS STATISTICS -->

## 📖 Citation

If you use this corpus, please cite:

```bibtex
@misc{digital-sovereign-workplace-research,
  author = {Weiß, Tobias},
  title = {Digital Sovereign Workplace — Data-Driven Agentic Literature Review},
  year = {2026},
  publisher = {GitHub},
  url = {https://github.com/tobias-weiss-ai-xr/digital-sovereign-workplace-research}
}
```

## 📄 License

MIT — see [LICENSE](LICENSE).
