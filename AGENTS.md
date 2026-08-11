# Repository Agent Instructions

## Repository Semantics

This repository is a paper knowledge base. Markdown is the primary artifact,
so commit types must describe the knowledge workflow rather than the file type.
Do not default to `docs(...)` merely because a change edits Markdown.

Use commit subjects in the form `<type>(<scope>): <imperative description>`:

- `ingest(<citekey>)`: add one explicitly selected paper, its canonical note,
  and the directly corresponding index updates.
- `intake(<YYYY-MM-DD>)`: record one configuration-driven intake cycle,
  including its selected papers, discovery/history record, and index updates.
- `framework(<component>)`: change skills, templates, format contracts,
  taxonomies, schemas, or another reusable vault mechanism.
- `refine(<target>)`: substantively revise an existing paper note, relation,
  index explanation, or reading interpretation.
- `automation(<id>)`: change a recurring automation, permission profile, or
  automation-specific environment.
- `meta(<scope>)`: maintain the repository itself without changing the paper
  knowledge or ingestion framework.

Use `docs(...)` only for documentation that is genuinely separate from the
vault's paper knowledge and workflows. Keep subjects concise and do not end
them with a period.

## Commit Boundaries

- Keep framework, schema, taxonomy, and Skill changes separate from newly
  ingested papers unless they are inseparable for correctness.
- Keep one reviewed daily intake coherent: its paper notes, discovery/history
  record, and generated index updates belong in the same `intake(...)` commit.
- Use `ingest(...)` for a standalone paper addition outside a batch intake.
- Stage exact task-relevant paths. Preserve unrelated tracked, untracked, and
  previously staged work.

## Repositories Without `.context`

- Resolve the current Git repository root before looking for project context.
- Use `.context/` only when it exists inside this repository. Never search a
  parent directory's sibling repositories or borrow another checkout's context.
- When `.context/` is absent, skip `ACTIVE_TASK.md` and `ROADMAP.md` Auto-Sync.
- In that mode, `commit-helper` may be used for status, diff, staged-scope, and
  safety checks only. This file is authoritative for commit semantics.

## Git Safety

- History rewrites and force pushes require explicit user authorization.
- A local history rewrite does not authorize pushing rewritten commits.
- Never mix unrelated dirty-worktree content into a commit for convenience.
