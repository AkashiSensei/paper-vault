# International Computer-Science Source Routing

Use this reference to obtain broad coverage of mainstream international
computer-science journals and conferences. This is a routing guide, not a fixed
allowlist. Select sources by field, and verify current URLs and coverage at run
time.

## Contents

- Minimum Coverage
- Cross-Field Discovery And Metadata
- Publisher And Society Libraries
- Field-Specific Routes
- Venue Recognition Sources
- Full-Text Routing
- Coverage Self-Check

## Minimum Coverage

For a normal recommendation run, use multiple independent channels:

1. a broad scholarly discovery index;
2. a computer-science bibliography;
3. a domain-relevant official proceedings archive, digital library, or journal
   platform;
4. a citation index when influence is evaluated;
5. the primary page for final identity, publication type, and original links.

An exact-title lookup or a search explicitly limited to one venue may use fewer
discovery channels, but final verification still requires a primary record.

Record which channels were used and which were unavailable. Do not claim broad
coverage after searching only arXiv, one general web engine, or one publisher.

## Cross-Field Discovery And Metadata

Use these in combination:

| Source | Best use | Important limitation |
|---|---|---|
| AnySearch or built-in web search | Query expansion, current pages, broad recall | Search ranking is not paper quality |
| OpenAlex | Broad works, concepts, citations, related works, OA locations | Metadata and venue mapping can be incomplete |
| Semantic Scholar | Semantic search, citation graph, influential-citation signals | Coverage and citation counts vary by field |
| Crossref | DOI metadata and publisher resolution | Not a recommendation or quality database |
| DBLP | Curated CS publication and venue metadata | Major CS coverage, not every publication or full text |
| arXiv | Preprints, recent work, legal full text | A preprint is not evidence of peer review or final venue |
| Google Scholar, when accessible | Broad recall and citation cross-check | No stable open API; counts and versions can be noisy |

Prefer DOI, OpenAlex ID, Semantic Scholar ID, arXiv ID, and normalized
title/author/year combinations for identity and deduplication.

## Publisher And Society Libraries

Search the platforms relevant to the brief:

- ACM Digital Library: `https://dl.acm.org/`
- IEEE Xplore: `https://ieeexplore.ieee.org/`
- USENIX publications: `https://www.usenix.org/publications`
- SpringerLink: `https://link.springer.com/`
- ScienceDirect: `https://www.sciencedirect.com/`
- Wiley Online Library: `https://onlinelibrary.wiley.com/`

These cover a large share of mainstream international CS journals and
conference proceedings, but no single platform is comprehensive. Prefer the
paper's official landing page there for venue, track, DOI, and publication
status.

If the user has licensed access to Scopus, Web of Science, or Journal Citation
Reports, use them as additional indexing or journal-context signals. Do not make
the workflow depend on subscription access.

## Field-Specific Routes

### Systems, Architecture, Parallel Computing, And Storage

Search ACM DL, IEEE Xplore, USENIX, DBLP, official conference sites, and the
publisher pages of relevant journals. Include systems venues and journals across
operating systems, architecture, distributed systems, cloud, storage, and high
performance computing.

When systems are preferred, search design and evaluation terminology such as:

- system design, implementation, runtime, scheduler, storage, network;
- end-to-end, microbenchmark, scalability, overhead, deployment;
- production, cluster, datacenter, accelerator, operating system.

Do not restrict systems discovery to papers that mention LLMs or GPUs.

### Networks

Search ACM DL, IEEE Xplore, USENIX, DBLP, and official networking conference and
journal pages. Cover networked systems, measurement, protocols, mobile and
wireless networking, and Internet infrastructure.

### Security, Privacy, And Cryptography

Search IEEE Xplore, ACM DL, USENIX Security proceedings, NDSS proceedings,
DBLP, and official IACR publications or ePrint for cryptography when relevant.
Distinguish peer-reviewed proceedings from unreviewed preprints and technical
reports.

### Software Engineering, Systems Software, And Programming Languages

Search ACM DL, IEEE Xplore, DBLP, official proceedings, and publisher journal
pages. Include software engineering, testing, maintenance, formal methods,
programming languages, compilers, and runtime systems.

### Databases, Data Mining, And Information Retrieval

Search ACM DL, IEEE Xplore, DBLP, PVLDB and other official proceedings or
journal sites, plus OpenAlex and Semantic Scholar for citation neighborhoods.
Distinguish database systems contributions from model-only data-mining work.

### Artificial Intelligence And Machine Learning

Search official NeurIPS proceedings, PMLR, OpenReview where used by the venue,
AAAI and IJCAI proceedings, ACM/IEEE publisher pages, arXiv, DBLP, OpenAlex, and
Semantic Scholar.

Do not infer peer-review status from an OpenReview or arXiv page alone. Verify
the accepted venue and track independently.

### Natural Language Processing

Search ACL Anthology, official venue pages, DBLP, arXiv, OpenAlex, and Semantic
Scholar. Use publisher pages for journal articles.

ACL Anthology: `https://aclanthology.org/`

### Computer Vision And Graphics

Search CVF Open Access for CVPR/ICCV-family papers, official ECCV/Springer
proceedings, ACM DL for graphics venues, IEEE Xplore, DBLP, and arXiv.

CVF Open Access: `https://openaccess.thecvf.com/`

### Human-Computer Interaction And Ubiquitous Computing

Search ACM DL, IEEE Xplore, DBLP, official proceedings, and relevant journal
platforms. Evaluate qualitative, design, field-study, and deployment evidence
using HCI norms rather than systems or ML criteria.

### Theory And Algorithms

Search ACM DL, IEEE Xplore, DBLP, arXiv, official proceedings, and DROPS/LIPIcs
for venues it publishes. Evaluate proof contribution and correctness rather
than requiring empirical benchmarks.

DROPS: `https://drops.dagstuhl.de/`

### Interdisciplinary Computer Science

Search the CS routes above plus the official publisher and field index relevant
to the adjacent discipline. Do not apply CCF or ICORE mechanically outside
their intended CS venue context.

## Venue Recognition Sources

For computer-science conferences and journals, combine:

- current official CCF categories when Chinese academic recognition matters;
- current ICORE conference ranking as a complementary international signal;
- official ACM, IEEE, USENIX, or other field-society records;
- DBLP publication history and continuity;
- current journal indicators when licensed or openly verifiable;
- official awards, artifact badges, and community adoption.

CCF and ICORE are not discovery databases and do not measure the quality of an
individual paper. Use them after candidate generation to contextualize venues.

## Full-Text Routing

Prefer legal full text in this order:

1. official open-access PDF or HTML;
2. official preprint such as arXiv;
3. author or institutional repository manuscript;
4. project or artifact page linking the paper;
5. subscription landing page with full-text availability stated honestly.

Never use an unauthorized mirror. Provide both the official landing page and
the best verified legal full-text link.

## Coverage Self-Check

Before finalizing recommendations, ask:

- Did the search include a broad index and a CS-specific bibliography?
- Did it search at least one official source appropriate to the subfield?
- Were important publisher or society ecosystems omitted without explanation?
- Were both journals and conferences considered when the request allows both?
- Were preprints distinguished from accepted publications?
- Were citation and venue signals cross-checked rather than copied from search
  snippets?
- Are coverage gaps or inaccessible subscription sources disclosed?
