# GitHub Pages Migration Design

## Goal

Migrate the formal AI-SDLC documentation from Confluence to a public GitHub Pages site while keeping `tkieron/ai-sdlc` as the public technical source repository and preserving the logical documentation hierarchy.

## Scope

Publish only the formal AI-SDLC path rooted at **AI-SDLC Home**. Exclude the Confluence scratchpad **Draft of AI-SDLC**, the Confluence space overview, and Atlassian-provided templates.

The published structure includes:

- AI-SDLC Home
- 00 Principles & Governance
- 01 Level 1 – Development Landscape
- 02 Level 2 – Development Process Map
- 03 Level 3 – Process Specifications
  - 03.01 Idea & Discovery
  - 03.02 Analysis
  - 03.03 Architecture
  - 03.04 Refinement
  - 03.05 Planning
  - 03.06 Test Design
  - 03.07 Implementation Design
  - 03.08 Implementation
  - 03.09 Review
  - 03.10 Verification & Acceptance
  - 03.11 Release & Deployment
  - 03.12 Production Feedback
- 04 Level 4 – Engineering Playbooks
  - Development
  - Testing
  - Review
    - Review Output – AI Review Findings
    - Review Output – Human Review Record
    - Review Output – Pair Review & Defence Record
    - Review Output – Review Decision Record
    - Review Playbook – Code Review Book & Checklist
    - Review Playbook – AI Review Agent Instructions
    - Review Playbook – Author IDE Review Checklist
    - Review Playbook – Pair Review & Defence
    - Review Guide – Java
    - Review Guide – Spring
    - Review Guide – Database
    - Review Guide – Messaging
    - Review Playbook – Risk-Based Review Process
    - Review Gate – Automated Pre-Flight Checklist
    - Review Gate – Human Pre-Flight Checklist
  - Release
  - AI Agents & Skills
- 05 Risk Model R0–R4
- 06 Metrics & Evaluation
- 07 Change Log & Decision Records

## Repository model

Use the existing public repository `tkieron/ai-sdlc`.

- `README.md` remains the public teaser and technical entry point.
- `docs/` becomes the source of the full public documentation site.
- `mkdocs.yml` defines navigation and site settings.
- `.github/workflows/docs.yml` builds and deploys GitHub Pages.

No second repository is introduced.

## Publishing model

The approved workflow after migration is:

`discussion -> working content -> feature branch -> commit/PR -> human approval -> merge -> GitHub Pages publication`

The public site represents only merged, approved documentation. Draft content is not published.

## URL model

Use stable semantic paths based on documentation hierarchy, for example:

- `/` — AI-SDLC Home
- `/00-principles/`
- `/01-landscape/`
- `/02-process-map/`
- `/03-process-specifications/03.09-review/`
- `/04-playbooks/review/risk-based-review-process/`
- `/05-risk-model/`
- `/06-metrics/`
- `/07-decisions/`

README links currently pointing to Confluence are replaced with the corresponding GitHub Pages URLs once the site structure is in place.

## Rendering

Use MkDocs Material for a documentation-oriented interface with hierarchical navigation, search, code blocks, tables and callouts. Preserve content semantics rather than attempting pixel-perfect reproduction of Confluence-specific macros.

## Migration rules

1. Preserve page titles and logical hierarchy.
2. Preserve Markdown content, headings, tables, lists, code blocks and links where representable.
3. Convert internal Confluence links to site-relative links.
4. Keep external links unchanged.
5. Preserve images/attachments when retrievable; otherwise keep explicit references rather than inventing replacements.
6. Exclude Confluence-only templates and scratch content from public navigation.
7. Do not publish from the migration branch; publication starts after merge to `main`.

## Acceptance criteria

- Formal AI-SDLC pages are represented in `docs/` with equivalent logical hierarchy.
- MkDocs navigation mirrors the Confluence hierarchy.
- README no longer points users to Confluence for the formal specification.
- Internal documentation links resolve within the Pages structure.
- GitHub Actions configuration can build and deploy the site from `main`.
- Changes are delivered through a reviewable pull request.