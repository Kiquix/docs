# Agent Operating Guide

Follow `.github/copilot-instructions.md` first.
This file adds repository-specific orchestration and memory rules for `docs`.

## Core operating model

- Default to one Codex agent working end-to-end in the current workspace. Use subagents only when the task is large, clearly parallelizable, approval-heavy, or the human explicitly asks for delegation.
- Treat planning, architecture, QA, and IA work as responsibility buckets, not mandatory always-on spawned agents.
- Prefer direct implementation once scope is clear. Do not stop at planning when the human asked for doc changes.
- This repo is documentation-first, so most work should stay local and focus on writing quality, factual accuracy, IA, and source-of-truth alignment.

## Retentia is the durable memory layer

Use Retentia MCP as the source of durable context.

Required Retentia project scope:

- `project = "docs"`

Use:

- `mem_add_observation` for live checklist items, blockers, phase updates, and run logs
- `mem_add_summary` for durable compressed memory, decisions, repo mapping, and contract summaries

If Retentia is unavailable:

- queue notes locally
- backfill them into Retentia when MCP is restored

## Start-of-run checklist

At the beginning of every non-trivial run:

1. Confirm Retentia is reachable.
2. Add a Run Header observation with:
   - date/time
   - request summary
   - repos involved and local paths
   - constraints
   - definition of done
3. Query Retentia first before planning:
   - `mem_search` for task and repo keywords
   - `mem_timeline` or `mem_get_entries` for prior decisions
   - `mem_context_pack` when broader compact recall is needed
4. Update or add a compressed repo-map summary if new structure is discovered.

## Phase discipline

Work in phases:

- Discovery
- Design
- Implementation
- Validation
- Wrap-up

For non-trivial runs, persist a concise Retentia observation or summary after each phase. At wrap-up, write a compressed summary with:

- key findings
- decisions
- invariants
- remaining work

## Decision recording

Every meaningful decision must be persisted with:

- date
- decision
- reason
- alternatives considered
- risks or follow-ups, if any

## Cross-repo and contract discipline

If work spans multiple repos or services:

- identify the documentation source of truth before editing
- record exact terms, product names, and contract shapes in Retentia
- keep Retentia entries separated by repo project value
- do not blend `Fred-Client`, `meet-fred-public-website`, `ai-emotion-analyzer`, or `usersphere-m` behavior unless the page explicitly compares them
- never invent features, endpoints, or admin workflows that are not grounded in source material

## Quality bar

- prefer small, reviewable diffs
- preserve factual accuracy, information scent, and link integrity
- keep writing concise, user-facing, and product-correct
- update navigation or cross-links when content moves
- never guess when something cannot be located
- say where you looked and what is missing
