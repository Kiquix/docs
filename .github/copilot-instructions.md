# Copilot Documentation Instructions

for the docs codebase

## Review Philosophy

- Only comment when you have high confidence that an issue exists.
- Prefer factual inaccuracies, misleading workflow descriptions, broken IA, broken links, or unclear writing over style nitpicks.
- Do not invent product behavior or API details.

## Agent Roles and Orchestration

- Default to a single Codex agent working end-to-end.
- Use additional agents only when a docs task genuinely benefits from parallel source-review or IA work.
- Treat this repo as documentation-first: writing, structure, and source accuracy are the primary concerns.

## Retentia Memory Discipline

- Treat Retentia MCP as the durable memory system for run logs, decisions, and repo recall.
- For non-trivial tasks, retrieve memory programmatically using `mem_search`, `mem_context_pack`, `mem_timeline`, and `mem_get_entries`.
- Use `project = "docs"` for this repo.

## Core Architecture Overview

This repo is a Mintlify documentation site.

### Key patterns in this codebase

- Content is written in MDX pages.
- Navigation and global doc structure live in `docs.json`.
- Topic areas are grouped in directories such as `api-reference/`, `essentials/`, `billing/`, and `getting-started/`.
- Reusable content may live in `snippets/` or shared assets folders.
- The repo is documentation-first, so source accuracy matters more than ornamental prose.

## Priority Areas the Review Must Cover

### Accuracy and source fidelity

Flag issues such as:

- instructions that do not match actual product behavior
- mixed-up repo or product names
- undocumented prerequisites or missing caveats
- invented API behavior, flags, or UI states

### IA and readability

Focus on defects such as:

- missing next steps or broken task flow
- headings that do not match user intent
- duplicate or contradictory guidance across pages
- content that is too internal, too vague, or too jargon-heavy

### Formatting and Mintlify constraints

Only comment when there is a real issue.

- broken frontmatter or MDX structure
- broken links or malformed code fences
- poor code/path formatting that obscures instructions

## Project-Specific Conventions

- Use active voice and second person.
- Prefer concise, user-facing wording.
- Use bold for UI labels and backticks for commands, paths, env vars, and code references.
- Keep internal/admin-only features out of end-user docs unless the page is explicitly internal.

## Response Format for Copilot

When providing feedback:

1. State the issue in one sentence.
2. Briefly explain why it matters if needed.
3. Provide a concrete fix direction or replacement wording.
