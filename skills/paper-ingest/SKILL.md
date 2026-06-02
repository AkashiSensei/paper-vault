---
name: paper-ingest
description: Add a specified academic paper to an Obsidian-style paper vault as a structured, verified Markdown note. Use when the user provides a paper title, DOI, arXiv ID, URL, PDF link, citation, or discovery item and wants it analyzed and added to the knowledge base.
---

# Paper Ingest

Add one specified paper to the vault as a durable literature note. This skill is
the formal write path for `papers/*.md`; discovery skills may propose papers,
but ingestion creates the canonical paper note.

## Scope

Use this skill when the user provides a specific paper and asks to add it,
analyze it, summarize it, or put it into the vault.

Do not use this skill for broad literature search, reading guidance on an
existing note, or vault-wide synthesis unless ingestion is explicitly part of
the task.

## Core Rules

- Keep the workflow tool-agnostic: use plain files, explicit paths, and
  portable Markdown/YAML conventions rather than client-specific commands.
- When online search is needed, prefer AnySearch if that skill/tool is available
  and appropriate. If AnySearch is unavailable, fails, or is not present in the
  current AI environment, fall back to the environment's built-in search or
  other reliable metadata lookup tools.
- Create exactly one canonical paper note per ingested paper.
- Follow `references/format-contract.md` for frontmatter, headings, relation
  blocks, and index update rules.
- Verify bibliographic metadata before treating it as final.
- If metadata cannot be verified, mark it as unverified instead of guessing.
- Do not store copyrighted PDF files in the public repository.
- Link only conceptually important previous work, not every reference.
- Do not create empty placeholder notes for referenced papers that are not being
  ingested. Describe them without Obsidian links until they are ingested.
- Add later-work relationships from the newer paper to the older paper; do not
  broadly backfill old notes unless the user asks.
- Preserve the difference between paper-grounded claims, AI analysis, and user
  interpretation.

## Vault Assumptions

Prefer this layout when present:

```text
papers/
indexes/
  areas/
  scenarios/
  topics/
  venues/
  methods/
  datasets/
  courses/
  projects/
inbox/
templates/
skills/
```

If the vault does not yet have these directories, create only the directories
needed for the current ingestion.

## Workflow

### 1. Identify The Paper

Accept any of these inputs:

- DOI
- arXiv ID or arXiv URL
- official paper page
- PDF URL
- title
- BibTeX or citation text
- an item from a discovery note

Extract candidate metadata:

- title
- authors
- year
- venue
- DOI
- arXiv ID
- official URL
- PDF URL
- project/code URL, if relevant

### 2. Verify Metadata

Use available sources such as:

- official venue or publisher page
- arXiv page
- DOI resolver or CrossRef
- Semantic Scholar
- OpenAlex
- author/project page
- the PDF first page, when locally available

Search preference:

- Use AnySearch first for web search, DOI/arXiv/title lookup, official page
  discovery, and URL extraction when it is available in the current environment.
- Treat AnySearch as a preferred capability, not a hard dependency of the vault
  or this skill.
- If AnySearch is unavailable, has quota/network errors, or is not supported by
  the current AI tool, use built-in web search, DOI/arXiv/CrossRef/OpenAlex
  lookup, publisher search, or other reliable search tools.
- Regardless of search provider, prefer primary sources over secondary
  summaries when finalizing metadata.

Verification guidance:

- Prefer DOI/arXiv/official pages over secondary summaries.
- Cross-check title, authors, year, and venue.
- If sources disagree, record the disagreement in `verification_notes`.
- If no reliable source is available, set `verification_status: unverified`.
- If only some fields are verified, set `verification_status: partially_verified`.

Suggested values:

```yaml
verification_status: verified | partially_verified | unverified
analysis_confidence: high | medium | low
source_acquired: true | false
source_verified_against_original: true | false
```

Only set `source_verified_against_original: true` when the actual source
artifact or official page was inspected.

### 3. Check For Existing Notes

Before creating a new note, search existing paper notes by:

- DOI
- arXiv ID
- normalized title
- citekey

If a matching note exists, update it only if the user wants ingestion to enrich
the existing note. Avoid creating duplicates.

### 4. Resolve Pending References To This Paper

Before finalizing the citekey, search existing vault notes for relation entries
that may already describe the paper being ingested:

- DOI
- arXiv ID
- exact or normalized title
- known aliases or title variants
- candidate citekeys
- `Status: not-ingested` relation blocks

If an existing `Status: not-ingested` relation clearly identifies the current
paper, use verified metadata to choose the canonical citekey. After creating the
note, update that relation entry by adding `Obsidian: [[{citekey}]]` and setting
`Status: ingested`.

If multiple existing relation entries describe the same paper, choose one
canonical citekey from verified metadata, then add the same Obsidian reference
to each confidently matched relation entry.

After creating the note, update all confidently matched pending relation blocks:

- add `Obsidian: [[{citekey}]]`
- change `Status: not-ingested` to `Status: ingested`
- preserve the title, authors, URL, work summary, relation role, limitation,
  comparison, and interpretation

Do not create stub files for pending references just to make links resolve.

### 5. Generate Citekey And Filename

Use a stable, readable citekey:

```text
firstauthorYYYYshorttitle
```

Examples:

```text
wang2025jenga
hu2022lora
vaswani2017attention
```

Filename should be stable and readable. Prefer:

```text
papers/{citekey}.md
```

If the vault already uses a different naming convention, follow the existing
convention.

### 6. Create The Paper Note

Use the template in `references/paper-note-template.md` and the strict format
contract in `references/format-contract.md`.

Write an initial note that is useful before deep human reading:

- concise summary
- research area and use scenario
- assumptions and applicability boundaries, separated from research positioning
- problem
- core idea
- method
- experiments/evidence
- key takeaways
- limitations
- relation blocks
- index file updates, without writing reverse index links into the paper note

Keep summaries factual and source-grounded. If the paper text is unavailable,
base the note on verified abstracts and official metadata, and mark analysis
confidence accordingly.

Do not create reading-question sections such as `Questions`, `Open Questions`,
or `Reading Questions` during ingestion. Those questions should be created later
by a reading or refinement workflow.

Do not create `My Understanding` during ingestion. User interpretation should be
added later by a reading or refinement workflow.

The `Method` section must not be only a component list. Start with one or two
paragraphs that explain the overall method, flow, or system design from a higher
level, including how major components cooperate. Component-level input/output
details should come after the reader has that overall map.

When describing key components, models, algorithms, modules, policies, dataset
construction steps, evaluation components, or pipelines, make the interface
explicit at the point of description. Describe what goes in, what comes out, and
how the component changes or transforms the input. Prefer a tiny concrete
example when the paper provides enough information to make one accurate. The
example should be simple enough to teach the mechanism, not a new result
invented by the ingesting agent.

Example of component/interface clarity:

```markdown
- Component: Contextual token selector
  - Input: token representations, task context, and a token budget.
  - Output: a subset or mask of tokens kept for fine-tuning.
  - Transformation: estimates which tokens are useful under the current context
    and drops low-utility tokens before the expensive training step.
  - Minimal example: Given a 32k-token document and a 25% token budget, the
    selector keeps tokens tied to the target answer and removes repeated boilerplate.
```

Keep `Research Area And Scenario` separate from `Assumptions And Scope`.
`Research Area And Scenario` should classify and position the paper: areas,
concrete target scenarios, and indexing rationale. Do not put boundary analysis,
failure cases, or `Key constraint` bullets there.

Use `Assumptions And Scope` for applicability analysis. Be especially specific
there. Do not write vague scope statements such as "runs in the cloud" or "uses
accelerators" without explaining which term matters and why. Identify the key
constraint, explain the mechanism behind the constraint, and state what cases
are excluded or weakened. Use bold sparingly to highlight only the critical
limiting word or short phrase, never the whole label or sentence.

Example of the expected reasoning style:

```markdown
- Claim: Requests are served by an accelerator cluster connected by heterogeneous links.
  - Key constraint: **heterogeneous links**, not merely "accelerator cluster".
  - Why it matters: The proposed policy depends on different movement costs
    across local device memory, peer-device links, host memory, or network paths.
  - Excludes: A single-GPU deployment or a uniform-topology cluster where
    topology-aware placement has little effect.
  - Portability: If the method depends on a vendor-specific primitive such as
    NVLink, CUDA, NCCL, XLA, or a particular NPU runtime, name that dependency;
    if it only needs measurable bandwidth/latency differences and migration
    controls, state that the assumption may generalize across hardware families.
```

### 7. Add Relation Blocks

Create relation links only when they help explain the paper.

Allowed relation types:

- `extends`
- `improves`
- `criticizes`
- `uses`
- `compares-with`
- `baseline`
- `dataset`
- `benchmark`
- `system`
- `survey`

For each important related work, prefer this shape:

For an ingested related paper:

```markdown
- Title: Full paper title.
  Authors: Author One; Author Two; Author Three.
  URL: https://...
  Obsidian: [[citekey]]
  - Type: baseline
  - Status: ingested
  - Work summary: What the related work does.
  - Role: What role the related work plays for this paper.
  - Limitation: What limitation this paper identifies, if any.
  - This paper: What this paper changes, adds, or reuses.
```

For a related paper that has not been ingested:

```markdown
- Title: Full paper title.
  Authors: Author One; Author Two; Author Three.
  URL: https://...
  - Type: baseline
  - Status: not-ingested
  - Work summary: What the related work does.
  - Role: What role the related work plays for this paper.
  - Limitation: What limitation this paper identifies, if any.
  - This paper: What this paper changes, adds, or reuses.
```

Only include `Obsidian: [[citekey]]` when the related paper already has a
canonical note. For a related paper that has not been ingested, do not include an
Obsidian link. Use the full title, authors, and a stable internet URL instead.
The entry should be centered on the related work's content and its role in the
current paper, not on DOI, arXiv, or other bibliographic bookkeeping fields.

### 8. Update Indexes

Suggest or update relevant indexes:

- research area/domain
- use scenario
- venue/conference/journal
- topic
- method
- dataset/benchmark
- course/project, when relevant

Consider multiple simultaneous memberships. A paper may belong to several
research areas at once, such as `LLM`, `AI Infrastructure`, `Cloud Computing`,
`Computer Networks`, `Databases`, `Systems`, `Security`, or `HCI`.

Prefer research-area names people commonly use in labs, reading groups, course
topics, and paper lists. Use scenario subgroups inside broader area indexes when
helpful. For example, an `LLM` index may contain scenarios such as
`Long-Context`, `Fine-Tuning`, `Inference Serving`, `Evaluation`, and
`Agent Systems`; an `AI Infrastructure` index may contain scenarios such as
`Training Systems`, `GPU Memory`, `Scheduling`, `Serving`, and `Observability`.

If areas have containment relationships, it is acceptable to add the same paper
to both broad and narrow indexes when both views are useful. Do not force a
single taxonomy path.

Do not create excessive index entries. Each index entry should add navigational
or analytical value.

Index files are the source of truth for navigation. Do not create or update a
paper-note section that lists reverse links back to indexes. The paper note may
keep semantic frontmatter fields such as `areas`, `scenarios`, `topics`, and
`methods`, but those fields describe the paper itself; they are not a mirror of
which index files currently link to it.

### 9. Report What Changed

End by reporting:

- created or updated paper note
- indexes updated
- verification status
- any uncertain metadata
- any relation targets that do not yet have notes

## Required References

Read before creating a note:

- `references/format-contract.md` for strict formatting rules.
- `references/paper-note-template.md` for the canonical note skeleton.

Do not rename canonical headings unless the vault already has a stronger local
convention and the user explicitly asks to adopt it.

## Final Self-Check

Before reporting completion, check:

- one canonical note exists for the paper
- all required frontmatter keys are present
- required headings are present in order
- unknown facts are marked as unknown rather than guessed
- relation types come from the allowed set
- not-ingested relation entries do not contain Obsidian wiki links
- pending references to the newly ingested paper were searched and normalized
  when confidently matched
- no paper-note reverse index section was created
- no local filesystem path, including local PDF paths, was written into
  `Source Notes` or other committed note content
- no PDF file was added to the public repository

## Failure Handling

If the paper cannot be identified:

- ask for a DOI, arXiv link, official URL, or PDF
- do not create a formal paper note

If metadata is incomplete but the user still wants a note:

- create a draft note only when there is enough information to identify the work
- set `status: draft`
- set `verification_status: unverified` or `partially_verified`
- include a short `verification_notes` item explaining what is missing

If the note already exists:

- do not duplicate it
- summarize the existing note path
- ask whether to enrich it when the requested action is ambiguous
