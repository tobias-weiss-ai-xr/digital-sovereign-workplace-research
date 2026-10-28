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
- [📚 Data Sovereignty](#data-sovereignty)
- [📚 Collaboration & Productivity](#collaboration-&-productivity)
- [📚 Identity & Access](#identity-&-access)
- [📚 Interoperability & Standards](#interoperability-&-standards)
- [📚 Open Source](#open-source)
- [📚 Public Sector & Education](#public-sector-&-education)
- [📚 SME Adoption](#sme-adoption)
- [📚 Security & Compliance](#security-&-compliance)
- [📚 Adoption & Change](#adoption-&-change)
- [📚 Architecture & Infrastructure](#architecture-&-infrastructure)
- [📚 Evaluation & Case Studies](#evaluation-&-case-studies)
- [📚 Surveys & Reviews](#surveys-&-reviews)
- [📚 Methods](#methods)
- [📚 Tooling & Platforms](#tooling-&-platforms)

### Digital Workplace

### Data Sovereignty

### Collaboration & Productivity

### Identity & Access

### Interoperability & Standards

### Open Source

### Public Sector & Education

### SME Adoption

### Security & Compliance

### Adoption & Change

### Architecture & Infrastructure

### Evaluation & Case Studies

### Surveys & Reviews

### Methods

### Tooling & Platforms

<!-- END PAPER LIST -->

<!-- BEGIN CORPUS STATISTICS -->

## 📊 Corpus Statistics

**0 papers** across **1 categories**.  

### Top categories

| Category | Papers | Recent | |
|----------|--------|--------|-|
| unknown | **0** | 0 | ░░░░░░░░░░░░ |

### Momentum (hottest categories)

| Category | Total | Rate | Recent | Score |
|----------|-------|------|--------|-------|
| Unknown | 0 | 0.0/mo | 0% | 0 |

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
