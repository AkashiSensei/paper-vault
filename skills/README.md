# Paper Vault Skills

This directory contains AI-readable workflow instructions for maintaining this
paper note vault. The skills are designed to be portable: they use plain
Markdown, stable file conventions, and explicit rules instead of depending on a
specific AI client or runtime.

## Current Contents

- `design.md`: Describes the intended skill workflow:
  `paper-discover -> paper-ingest -> paper-refine`, with `paper-query` able to
  read any ingested note whether or not it has been refined.
- `references.md`: Records external research-skill repositories and patterns
  worth learning from. These are references, not direct dependencies.
- `paper-ingest/`: The first implemented skill. It creates or updates canonical
  paper notes in `papers/*.md` from a specified paper, with metadata
  verification, structured summaries, relation blocks, and index updates.

## Design Highlights

- Multi-dimensional indexing: one paper can appear in multiple area, scenario,
  topic, method, venue, dataset, course, or project indexes. The vault does not
  force a single taxonomy path.
- Applicability-aware notes: each paper should state its research area and use
  scenario, then separately explain the assumptions, constraints, non-goals, and
  cases where the result may weaken.
- Related-work network: important previous or related papers are recorded with
  typed relation blocks, explaining what the current paper extends, improves,
  uses, compares against, or treats as a baseline.
- Content-first related work: related-work entries emphasize the work's title,
  authors, URL, contribution, and role. Obsidian links are added only after that
  paper has been ingested.
- Public-vault hygiene: PDFs and local filesystem paths are kept out of the
  repository, while official URLs and verification notes remain in the paper
  note.
