# Paper Discovery Evaluation Rubric

Use this rubric after identity verification and hard-constraint filtering.
Scores support relative ordering within one discovery run; they are not
objective measures of scientific worth.

## Contents

- Source Hierarchy
- Stage 1: Hard Gates
- Stage 2: Default Weighted Evaluation
- Stage 3: Set-Level Assembly
- Dimension Guidance
- Systems-Paper Lens
- Classic And Frontier Calibration
- Confidence

## Source Hierarchy

Use `computer-science-sources.md` to route discovery across international
computer-science bibliographies, publishers, societies, proceedings, and
field-specific archives.

Prefer primary and authoritative sources:

1. official publisher, society, venue, journal, or proceedings page;
2. DOI record or official preprint record such as arXiv;
3. authors' or project page for legal manuscripts, artifacts, and corrections;
4. structured scholarly indexes such as Crossref, OpenAlex, Semantic Scholar,
   and DBLP;
5. secondary search and recommendation services for candidate generation only.

Cross-check important facts. Record unknown when verification fails.

For changeable signals, record both source and observation date:

```text
CCF rank: A, CCF seventh edition, checked YYYY-MM-DD
ICORE rank: A*, ICORE 2026, checked YYYY-MM-DD
Citations: 842, OpenAlex, checked YYYY-MM-DD
```

Use the current official CCF directory:
`https://www.ccf.org.cn/Academic_Evaluation/By_category/`

Use the current official ICORE portal for international computer-science
conference context:
`https://www.core.edu.au/icore-portal`

Do not use discontinued or stale journal rankings as if they were current.

## Stage 1: Hard Gates

A candidate must pass:

- identifiable real work;
- official page or resolvable primary record;
- no duplicate canonical work or duplicate version in the current result;
- no work explicitly excluded by the active requirements;
- all explicit hard requirements;
- no unresolved retraction or invalidation, unless requested for critical study;
- enough metadata and content evidence to justify the recommendation.

If only an abstract is available, the work may remain a candidate, but cap
paper-level assessment confidence at `medium`.

## Stage 2: Default Weighted Evaluation

Score every dimension from 0 to 5, then calculate:

```text
weighted contribution = dimension weight × score / 5
total = sum of weighted contributions
```

| Dimension | Weight | Central question |
|---|---:|---|
| Requirement fit | 25 | Does it directly satisfy the stated goal, role, and preferences? |
| Technical and empirical quality | 20 | Are the method, evidence, baselines, and claims credible? |
| Originality | 15 | What non-trivial idea, mechanism, dataset, analysis, or system design does it add? |
| Applicability | 15 | Do its assumptions, scale, hardware, data, and deployment conditions fit the intended use? |
| Vault value | 10 | Does it fill a gap, explain lineage, provide a prerequisite, or connect existing notes? |
| Venue and community recognition | 8 | What credible field-specific venue signals exist? |
| Scholarly or practical influence | 7 | What age-aware evidence of uptake, replication, citation, adoption, or awards exists? |

The default total is out of 100. Treat small score differences as ties. Explain
the evidence behind ordering; never present the number without the dimensions.

Explicit user requirements may change the effective emphasis, but do not reduce
paper-level quality to a negligible factor. A prestigious venue cannot rescue a
weak or inapplicable paper.

## Stage 3: Set-Level Assembly

Apply set-level requirements only after individual hard gates and quality
evaluation. When a coherent learning batch is requested:

- define one shared question or learning objective;
- for a multi-paper set, connect every selected candidate to at least one other
  candidate;
- require the complete set to form one connected graph;
- prefer complementary roles, assumptions, evidence, or trade-offs over
  near-duplicate papers;
- distinguish verified citation or lineage edges from analytical comparison
  edges;
- derive a useful reading sequence from prerequisites and contrasts.

Set coherence cannot rescue a weak paper. If no full-size connected set clears
the quality threshold, return a smaller connected set. Use a singleton only
when no qualified connected pair exists, and relate it to the shared question
or an ingested vault paper.

## Dimension Guidance

### Requirement Fit

Consider:

- direct match to the research question;
- requested paper role;
- contribution type;
- date, venue, access, language, and reading-budget preferences;
- requested balance, such as systems over model algorithms.

### Technical And Empirical Quality

Inspect the actual paper or official full description when possible:

- clear problem and claims;
- method appropriate to the question;
- fair and strong baselines;
- sufficient datasets, workloads, sample sizes, or proof obligations;
- ablations, sensitivity analysis, uncertainty, and threat discussion;
- conclusions proportional to evidence;
- reproducibility through code, data, artifacts, or detailed methods;
- corrections, retractions, conflicts, and known validity concerns.

Adapt evidence norms to paper type. A systems paper, theorem paper, benchmark,
survey, and empirical ML paper should not be graded by one experimental template.

### Originality

Distinguish:

- a new problem or framing;
- a new mechanism or system design;
- a meaningful synthesis;
- a new dataset, benchmark, or measurement;
- a strong application or transfer;
- a minor parameter, component, or scale change.

Do not equate recency with novelty.

### Applicability

Identify:

- required hardware, software stack, topology, data, model family, workload,
  trust model, or scale;
- excluded or weak cases;
- evidence at realistic scale;
- portability beyond the evaluated setting;
- operational complexity and resource cost.

Prefer a paper whose boundary matches the user's goal over a more famous but
misaligned paper.

### Vault Value

Compare with canonical notes, indexes, and relation blocks:

- prerequisite for an ingested paper;
- foundational ancestor or important descendant;
- competing approach or baseline;
- fills an uncovered method, venue, scenario, or dataset;
- strengthens a weakly represented area;
- redundant with an existing note.

Do not reward similarity alone. A near-duplicate may add less value than a
bridge or counterpoint.

### Venue And Community Recognition

For computer science:

- verify CCF rank from the current official edition when relevant to a Chinese
  academic preference;
- use ICORE as a complementary international conference signal when applicable;
- consider established ACM, IEEE, USENIX, or field-society venues;
- verify the exact track and paper type;
- consider best-paper or distinguished-paper awards only when officially listed.

For journals and non-CS fields, use field-appropriate norms and current official
sources. Do not compare conference and journal prestige mechanically.

CCF and ICORE rankings evaluate venues, not individual papers. An unranked venue
is not automatically poor, and a top-ranked venue does not make every paper
high quality.

### Scholarly Or Practical Influence

Use multiple signals when available:

- citation count with source and date;
- citations per year or field-normalized indicators;
- influential-citation or citation-context evidence;
- independent replications or follow-up work;
- adoption in widely used systems, libraries, benchmarks, standards, or courses;
- official awards or artifact badges.

Correct for age and field. Do not compare raw citations across unrelated fields
or use author affiliation as a quality proxy.

## Systems-Paper Lens

When systems work is preferred, additionally inspect:

- whether the system contribution is central rather than packaging;
- architecture and design trade-offs;
- implementation detail and engineering novelty;
- realistic workloads and deployment environment;
- end-to-end performance plus explanatory microbenchmarks;
- scalability, overhead, resource efficiency, and failure cases;
- fair comparison against production-relevant baselines;
- artifacts or deployment experience.

ML accuracy alone is insufficient evidence for a systems recommendation.

## Classic And Frontier Calibration

For foundational recommendations, emphasize:

- clear position in the intellectual lineage;
- lasting conceptual or practical influence;
- continued relevance to current work;
- independent uptake beyond the originating group.

For frontier recommendations, emphasize:

- credible novelty;
- current problem relevance;
- sufficient early evidence;
- artifact and metadata quality;
- explicit uncertainty due to limited follow-up.

Do not require a recent paper to have classic-level citations.

## Confidence

Assign:

- `high`: identity and evaluation checked against primary metadata and full text
  or a detailed official artifact;
- `medium`: identity is verified, but assessment relies mainly on abstract,
  official summary, and structured metadata;
- `low`: material identity or evaluation evidence remains incomplete.

Do not place a low-confidence work in the main recommendation list unless the
uncertainty itself is central to the user's request.
