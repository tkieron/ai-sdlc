# GitHub Pages Migration Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish the formal AI-SDLC Confluence hierarchy as a MkDocs Material GitHub Pages site in `tkieron/ai-sdlc` and replace public Confluence links with site links.

**Architecture:** Keep one repository. `README.md` remains the teaser/technical entry point; `docs/` is the full documentation source. A GitHub Actions workflow deploys MkDocs Material from `main`, so only merged content becomes public.

**Tech Stack:** GitHub, GitHub Pages, GitHub Actions, Python, MkDocs, MkDocs Material, Markdown

**Spec:** `docs/superpowers/specs/2026-08-22-github-pages-migration-design.md`

## Global Constraints

- Publish only the formal hierarchy rooted at `AI-SDLC Home`.
- Exclude `Draft of AI-SDLC`, the Confluence space overview and Atlassian template pages.
- Preserve the Confluence logical hierarchy and page titles.
- Use semantic site-relative URLs.
- Do not deploy from the migration branch; deployment is triggered from `main` after merge.
- Do not invent missing attachment content.

---

### Task 1: Site scaffold and navigation

**Files:**
- Create: `mkdocs.yml`
- Create: `.github/workflows/docs.yml`
- Create: `requirements-docs.txt`

**Interfaces:**
- Consumes: Markdown pages under `docs/`.
- Produces: deterministic `mkdocs build --strict` and GitHub Pages deployment from `main`.

- [ ] Create `requirements-docs.txt` pinning `mkdocs-material` to a compatible major/minor range.
- [ ] Create `mkdocs.yml` with site title, Material theme, search, Markdown extensions and complete formal navigation.
- [ ] Create `.github/workflows/docs.yml` that installs dependencies, runs `mkdocs build --strict`, uploads the Pages artifact and deploys only on `main`.
- [ ] Verify configuration paths match all planned Markdown files.
- [ ] Commit scaffold.

### Task 2: Migrate formal Confluence content

**Files:**
- Create/replace: `docs/index.md`
- Create: `docs/00-principles/index.md`
- Create: `docs/01-landscape/index.md`
- Create: `docs/02-process-map/index.md`
- Create: `docs/03-process-specifications/index.md` and `03.01` through `03.12` pages
- Create: `docs/04-playbooks/index.md` plus Development, Testing, Review, Release and AI Agents & Skills pages
- Create: all formal L4 Review descendant pages
- Create: `docs/05-risk-model/index.md`
- Create: `docs/06-metrics/index.md`
- Create: `docs/07-decisions/index.md`

**Interfaces:**
- Consumes: Confluence Markdown bodies for the formal hierarchy.
- Produces: site-local Markdown preserving titles, headings, tables, lists, code and link semantics.

- [ ] Retrieve every formal page body from Confluence as Markdown.
- [ ] Normalize filenames and hierarchy according to the design spec.
- [ ] Replace internal Confluence page links with site-relative links.
- [ ] Preserve external links unchanged.
- [ ] Keep attachment references only where attachment bytes are unavailable.
- [ ] Verify every page in MkDocs navigation has a corresponding Markdown source file.
- [ ] Commit migrated documentation.

### Task 3: Public entry-point link migration

**Files:**
- Modify: `README.md`
- Inspect/modify if needed: `docs/framework-overview.md`
- Inspect/modify if needed: `docs/manifesto.md`
- Inspect/modify if needed: `CONTRIBUTING.md`
- Inspect/modify if needed: `VERSION.md`

**Interfaces:**
- Consumes: stable GitHub Pages paths from Tasks 1–2.
- Produces: no public navigation dependency on Confluence.

- [ ] Search public repository text for `atlassian.net` and Confluence page URLs.
- [ ] Replace formal-specification links with site-relative or canonical Pages links.
- [ ] Update wording that says the full specification lives in Confluence.
- [ ] Re-run repository search for remaining public Confluence links and classify any intentional historical references.
- [ ] Commit link migration.

### Task 4: Verification and pull request

**Files:**
- Verify all files changed by Tasks 1–3.

**Interfaces:**
- Consumes: completed migration branch.
- Produces: reviewable pull request into `main`.

- [ ] Validate navigation/file parity from `mkdocs.yml`.
- [ ] Validate no formal Confluence URL remains in README/site content.
- [ ] Validate Markdown has no obvious broken internal targets introduced by migration.
- [ ] Review branch diff against `main` for scope creep.
- [ ] Open a pull request titled `docs: migrate AI-SDLC documentation to GitHub Pages` with migration scope, exclusions and post-merge deployment notes.