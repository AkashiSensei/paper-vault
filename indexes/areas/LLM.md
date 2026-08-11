# LLM

## Scope And Boundary

This area is defined by the **subject of the research contribution**, not by the mere presence of an LLM in the workload. It indexes work whose primary contribution concerns LLM architectures, learning or adaptation algorithms, capabilities and behavior, reasoning and agent methods, evaluation, or ways of organizing and using LLMs.

Include a paper here when answering its main research question requires understanding or changing the model, its behavior, or how people and systems organize its use. Do not include a paper merely because its experiments train, fine-tune, or serve an LLM. If the main contribution is a kernel, compiler, memory manager, distributed runtime, scheduler, serving engine, or cluster control plane, classify it under AI Infrastructure and Systems; retain `llm` as a tag and use LLM-specific topics and scenarios for workload-level discovery.

This boundary is especially important now that LLMs are the dominant workload in much of AI Infrastructure research. If every paper that merely involved an LLM were added here, most contemporary work on training systems, inference serving, operator optimization, and AI platforms would also enter the LLM area. The area would then collapse into a broad workload label, duplicate much of AI Infrastructure, and stop distinguishing research on LLMs from research on the systems that run them.

Use the following decision rule:

- **Model, behavior, or use is the object of study:** include the paper in LLM. ReAct and research on autonomous-agent organization are examples.
- **Compute, memory, communication, scheduling, or platform operation is the object of study:** do not include the paper in LLM solely because the workload is an LLM. Orca, vLLM/PagedAttention, and JENGA are examples.
- **Both are substantive research contributions:** cross-list only when the paper makes independent contributions on both sides, not when the LLM merely supplies the benchmark or workload.

## 2026-07

- [[papers/wang2024autonomousagents]]
  - Title: A survey on large language model based autonomous agents
  - Subarea: LLM agents; architecture, capability acquisition, applications, and evaluation.
  - Why listed here: Studies how LLMs function as persistent agent controllers and organizes the surrounding profile, memory, planning, action, and evaluation mechanisms.
- [[papers/yao2023react]]
  - Title: ReAct: Synergizing Reasoning and Acting in Language Models
  - Subarea: LLM reasoning, tool use, and interactive agents.
  - Why listed here: Expands an LLM policy with natural-language thoughts and environment actions so external observations can ground and revise later reasoning.
