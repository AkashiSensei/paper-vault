# Paper Note Template

Use this template when creating a canonical paper note. Keep the structure stable
enough for humans, Obsidian, and AI agents to read consistently.

```markdown
---
citekey: null
title: null
authors: []
year: null
venue: null
type: paper
status: ingested
tags: []
topics: []
areas: []
scenarios: []
methods: []
doi: null
arxiv: null
official_url: null
pdf_url: null
code_url: null
local_pdf: null
source_acquired: false
source_verified_against_original: false
verification_status: unverified
analysis_confidence: low
verification_notes: []
created: null
updated: null
---

# {{title}}

## Summary

One to three sentences explaining what the paper does and why it matters.

## Problem

What problem does the paper address? Why is the problem important?

## Research Area And Scenario

- Area(s): Which broad research directions does this paper belong to? Keep this
  as research positioning, not applicability analysis. Examples:
  LLM, AI Infrastructure, Cloud Computing, Computer Networks, Databases,
  Systems, Security, HCI.
- Scenario(s): What concrete use cases or settings does the paper target?
  Examples: long-context fine-tuning, GPU memory optimization, inference
  serving, distributed training, datacenter scheduling, retrieval-augmented
  generation.
- Why it matters here: Why is this paper relevant to those areas or scenarios?
- Indexing rationale: Why should this paper appear in these area/scenario
  indexes?

## Assumptions And Scope

- Stated assumptions:
  - Claim:
    - Key constraint: ... **specific limiter** ...
    - Why it matters:
    - Excludes or weakens:
- Implied assumptions:
  - Claim:
    - Key constraint: ... **specific limiter** ...
    - Why it matters:
    - Excludes or weakens:
- What is ignored or abstracted away:
  - Claim:
    - Key constraint: ... **specific limiter** ...
    - Why it matters:
    - Excludes or weakens:
- Applies when:
  - Claim:
    - Key constraint: ... **specific limiter** ...
    - Why it matters:
- May not apply when:
  - Claim:
    - Key constraint: ... **specific limiter** ...
    - Why it matters:

## Core Idea

What is the central insight or mechanism?

## Method

Start with one or two paragraphs explaining the overall method, pipeline, or
system design. Describe the high-level flow and how the major components
cooperate before listing component details.

Then describe the main model, system, algorithm, theory, dataset, or
experimental design as appropriate. When describing an important component,
model, procedure, scheduler, policy, dataset construction step, or evaluation
component, explain its interface close to the description:

- Component:
  - Role:
  - Input:
  - Output:
  - Transformation:
  - Minimal example:

## Experiments And Evidence

- What does the paper evaluate?
- What baselines, datasets, workloads, or metrics are used?
- What are the most important results?

## Contributions

- Contribution 1.
- Contribution 2.
- Contribution 3.

## Limitations

- Limitation 1.
- Limitation 2.

## Key Takeaways

- Takeaway 1.
- Takeaway 2.

## Relation: Previous Work

- Title:
  Authors:
  URL:
  - Type: baseline
  - Status: not-ingested
  - Work summary:
  - Role:
  - Limitation:
  - This paper:

## Relation: Compared With

- Title:
  Authors:
  URL:
  - Type: compares-with
  - Status: not-ingested
  - Work summary:
  - Similarity:
  - Difference:
  - When to use which:

## Source Notes

- Metadata sources:
- Source verification:
- PDF policy: Do not store PDFs in the public repository. If a local PDF was
  inspected, describe that generically without recording its local path.
```

## Field Notes

- `citekey`: stable identifier, usually `firstauthorYYYYshorttitle`.
- `authors`: use a YAML list of display names, one author per item.
- `status`: suggested values are `draft`, `ingested`, `reading`, `refined`, and
  `archived`.
- `verification_status`: suggested values are `verified`,
  `partially_verified`, and `unverified`.
- `analysis_confidence`: suggested values are `high`, `medium`, and `low`.
- `local_pdf`: keep `null` for public vault notes unless the user explicitly
  wants a private-only vault. Do not write absolute local paths into committed
  notes.
- For strict formatting rules, see `format-contract.md`.
