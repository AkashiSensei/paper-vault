# Reference Skills For Paper Vault

This document records external skills and repositories worth studying while
implementing the `paper-vault` skill layer. The goal is not to copy them
wholesale, but to borrow useful workflow patterns, guardrails, schemas, and
small task designs.

## Target Repositories

- [Orchestra-Research/AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs)
- [Imbad0202/academic-research-skills-codex](https://github.com/Imbad0202/academic-research-skills-codex)
- [Imbad0202/academic-research-skills](https://github.com/Imbad0202/academic-research-skills)
- [brycewang-stanford/Awesome-Agent-Skills-for-Empirical-Research](https://github.com/brycewang-stanford/Awesome-Agent-Skills-for-Empirical-Research)

## Cross-Cutting References

### Skill Structure And Progressive Disclosure

Source:

- `Orchestra-Research/AI-Research-SKILLs`

Useful patterns:

- Keep each `SKILL.md` focused on the active workflow.
- Put detailed schemas, examples, and policy rules in `references/`.
- Use a small number of well-scoped skills instead of one large universal
  research skill.
- Treat skills as procedural memory: they should tell the agent how to act in a
  specific workflow, not explain every concept from scratch.

Use in `paper-vault`:

- Each of `paper-discover`, `paper-ingest`, `paper-refine`, and `paper-query`
  should have a concise `SKILL.md`.
- Shared detailed rules should live in reference files such as
  `paper-note-schema.md`, `relation-types.md`, `source-verification.md`, and
  `index-policy.md`.

### Citation Hallucination Prevention

Source:

- `Orchestra-Research/AI-Research-SKILLs/20-ml-paper-writing/ml-paper-writing`
- `Imbad0202/academic-research-skills-codex/.../semantic_scholar_api_protocol.md`
- `Imbad0202/academic-research-skills-codex/.../crossref_api_protocol.md`
- `Imbad0202/academic-research-skills-codex/.../openalex_api_protocol.md`

Useful patterns:

- Never invent bibliographic metadata from memory.
- Prefer programmatic verification through DOI, Semantic Scholar, CrossRef,
  OpenAlex, arXiv, or official publisher pages.
- Mark unverified metadata explicitly instead of silently guessing.
- Store verification provenance so later agents know what was checked.

Use in `paper-vault`:

- `paper-ingest` should verify title, authors, year, venue, DOI/arXiv, and
  official URL before creating or finalizing a paper note.
- `paper-discover` can list candidates with weaker confidence, but `paper-ingest`
  should upgrade or mark verification status.

## References For `paper-discover`

### Searching Scientific Literature

Source:

- `brycewang-stanford/Awesome-Agent-Skills-for-Empirical-Research`
- Path: `skills/05-kthorn-research-superpower/research/searching-literature`

Useful patterns:

- Parse the user request into keywords, data needs, constraints, and synonyms.
- Use Boolean query expansion to balance recall and precision.
- Treat discovery output as a candidate list with metadata, not as final notes.
- Save search results separately before relevance evaluation.

Use in `paper-vault`:

- `paper-discover` should produce an inbox/discovery note with candidate papers,
  relevance rationale, source links, and suggested priority.
- It should not create formal `papers/*.md` files unless the user explicitly asks
  for ingestion.

### Traversing Citation Networks

Source:

- `brycewang-stanford/Awesome-Agent-Skills-for-Empirical-Research`
- Path: `skills/05-kthorn-research-superpower/research/traversing-citations`

Useful patterns:

- Use backward citations to find foundational work.
- Use forward citations to find later improvements or applications.
- Filter before traversal to avoid citation-network explosion.
- Deduplicate papers by DOI, Semantic Scholar ID, arXiv ID, or normalized title.
- Limit traversal depth.

Use in `paper-vault`:

- `paper-discover` should follow citations only for highly relevant seed papers.
- Candidate notes should record why a paper was found, such as
  `backward_from: [[Seed Paper]]` or `forward_from: [[Seed Paper]]`.
- Citation traversal is for discovery, not automatic relation creation.

### Literature Monitoring Strategies

Source:

- `Imbad0202/academic-research-skills-codex`
- Path: `skills/academic-research-suite/ars/deep-research/references/literature_monitoring_strategies.md`

Useful patterns:

- Re-run searches over time with stable queries.
- Distinguish broad discovery from targeted monitoring.
- Track search scope and time boundaries.

Use in `paper-vault`:

- Later versions of `paper-discover` can support recurring topic watchlists or
  saved queries, but this is not part of the first MVP.

## References For `paper-ingest`

### Literature Corpus Entry Schema

Source:

- `Imbad0202/academic-research-skills-codex`
- Path: `skills/academic-research-suite/ars/shared/contracts/passport/literature_corpus_entry.schema.json`

Useful patterns:

- Required fields: stable citation key, title, authors, year, and source pointer.
- Optional fields: venue, DOI, tags, abstract, user notes, acquisition status,
  verification method, and provenance.
- Authors can be represented in CSL-style structured form.
- Source acquisition and source verification are separate concepts.

Use in `paper-vault`:

- Paper notes should have machine-readable frontmatter.
- At minimum, store citekey, title, authors, year, venue, DOI/arXiv/URL,
  source pointers, status, tags, and verification state.
- Do not claim `source_verified_against_original: true` unless the source was
  actually inspected.

### Obsidian Adapter

Source:

- `Imbad0202/academic-research-skills-codex`
- Path: `skills/academic-research-suite/ars/scripts/adapters/obsidian.py`

Useful patterns:

- Skip `.obsidian/`, `_templates/`, and hidden directories.
- Prefer frontmatter conventions for robust machine parsing.
- Support a fallback convention from H1, authors, and year when needed.
- Build stable `obsidian://` pointers.
- Reject malformed notes explicitly instead of silently coercing them.

Use in `paper-vault`:

- `paper-ingest` should create notes that future adapters can parse reliably.
- Our schema should avoid ambiguous free-text-only metadata.
- Invalid or incomplete ingest attempts should be reported clearly.

### Source Verification And Source Quality

Source:

- `Imbad0202/academic-research-skills-codex`
- Paths:
  - `deep-research/references/semantic_scholar_api_protocol.md`
  - `deep-research/references/source_quality_hierarchy.md`

Useful patterns:

- Use title similarity and DOI lookup to verify whether a paper exists.
- A failed index lookup is not proof a paper is fake, especially for recent or
  niche work.
- Evidence quality can be graded, but field-specific norms matter.

Use in `paper-vault`:

- `paper-ingest` should store verification status with nuance:
  `verified`, `partially_verified`, or `unverified`, plus notes.
- For computer science papers, official venue pages, arXiv pages, DOI records,
  and author/project pages are more relevant than medical-style evidence levels.

### Paper Reading Assistant Template

Source:

- `brycewang-stanford/Awesome-Agent-Skills-for-Empirical-Research`
- Path: `skills/43-wentorai-research-plugins/skills/research/paper-review/paper-reading-assistant`

Useful patterns:

- Use a consistent note template: metadata, summary, problem, method, results,
  strengths, weaknesses, questions, relevance, and key references.
- Support different depth levels: quick survey, standard note, deep note.

Use in `paper-vault`:

- `paper-ingest` should create a useful initial note even before the user has
  deeply read the paper.
- `paper-refine` should later expand the same note rather than creating a second
  parallel note.

## References For `paper-refine`

### Three-Pass Reading Method

Source:

- `brycewang-stanford/Awesome-Agent-Skills-for-Empirical-Research`
- Path: `skills/43-wentorai-research-plugins/skills/research/paper-review/paper-reading-assistant`

Useful patterns:

- Pass 1: survey title, abstract, intro, headings, figures, conclusion.
- Pass 2: understand the full paper and summarize each section.
- Pass 3: challenge assumptions and think about improvements.

Use in `paper-vault`:

- `paper-refine` should ask what reading depth the user wants.
- It should preserve the user's own understanding, questions, and critique
  separately from AI-generated summaries.

### Academic Research Suite Writing And Review Agents

Source:

- `Imbad0202/academic-research-skills-codex`
- Paths:
  - `academic-paper/agents/literature_strategist_agent.md`
  - `academic-paper-reviewer/`
  - `deep-research/agents/source_verification_agent.md`

Useful patterns:

- Separate source-grounded claims from interpretation.
- Use integrity checks around citations and claims.
- Treat review and revision as structured passes.

Use in `paper-vault`:

- `paper-refine` should not turn uncertain user impressions into paper-grounded
  facts.
- Refined notes should distinguish `Paper Claims`, `My Understanding`,
  `Questions`, and `Critique`.

## References For `paper-query`

### Obsidian Citation Guide

Source:

- `brycewang-stanford/Awesome-Agent-Skills-for-Empirical-Research`
- Path: `skills/43-wentorai-research-plugins/skills/writing/citation/obsidian-citation-guide`

Useful patterns:

- Literature notes should be linkable by citekey and wiki links.
- Index/MOC notes can provide many views over the same paper set.
- Dataview-style querying can produce dynamic literature dashboards.
- Zotero and Obsidian can be separated: Zotero stores PDFs, Obsidian stores
  synthesis.

Use in `paper-vault`:

- `paper-query` should search notes, indexes, tags, frontmatter, and relation
  blocks.
- Future versions can generate Dataview-compatible views if the vault adopts the
  plugin.

### Citation Network Builder

Source:

- `brycewang-stanford/Awesome-Agent-Skills-for-Empirical-Research`
- Path: `skills/43-wentorai-research-plugins/skills/tools/knowledge-graph/citation-network-builder`

Useful patterns:

- Distinguish direct citation, co-citation, and bibliographic coupling.
- Use directed edges for citation lineage.
- Use graph metrics only when the corpus is large enough to make them meaningful.

Use in `paper-vault`:

- `paper-query` can explain the local note graph using relation blocks.
- Full graph export or visualization should be a later feature, not part of the
  first query MVP.

### Literature Corpus Consumers

Source:

- `Imbad0202/academic-research-skills-codex`
- Path: `academic-pipeline/references/literature_corpus_consumers.md`

Useful patterns:

- Treat the literature corpus as shared input for downstream tasks.
- Consumers should respect provenance and verification fields.

Use in `paper-vault`:

- `paper-query` should surface confidence and provenance when answering.
- If an answer is based on AI-generated summaries rather than user-refined notes
  or verified source text, it should say so.

## References To Defer

These are interesting but probably too heavy for the first version:

- Full `autoresearch` loops from Orchestra.
- Full ARS `academic-pipeline` integrity gates.
- Zotero API integration.
- Graph export with NetworkX, Gephi, or VOSviewer.
- Recurring literature monitoring.
- Public web dashboard generation.

The MVP should stay focused: reliable discovery, careful ingestion, user-centered
refinement, and query over already-ingested notes.
