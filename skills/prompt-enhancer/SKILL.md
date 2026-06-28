---
name: Prompt Enhancer
description: Turns a rough request into a structured, agent-ready execution spec for any coding agent. Use when the user wants to enhance, compile, refine, or sharpen a prompt; turn a request into a task brief or spec; or "make this prompt agent-ready / eseguibile". Triggers on enhance, compile, ottimizza, compila, "make this a proper prompt/spec/brief".
version: 2.0.0
---

# Prompt Enhancer

Compile a rough request into an execution spec any coding agent can run with no further questions. The output is the spec **only** — never execute the task itself.

## Workflow (follow in order)

### 1. Ground yourself in context
Before writing anything, understand the codebase the request targets. Use whatever tools are available to you:

- Read every file, path, or symbol the user references explicitly.
- Detect stack and conventions from package manifests, lint config, and existing patterns — never guess.
- If a structural index exists, prefer it over scanning raw files. Examples:
  - **Graphify**: check for `graphify-out/` — if present, query the graph for architecture and scope.
  - **Other indexing tools**: if your agent has a similar repo-exploration plugin or skill, use it.
  - **No index available**: browse the directory tree and read key entry points to build context manually.

Skip this step only if the request has no codebase context at all.

### 2. Interview — resolve the gaps that matter (max 3 questions)
Ask up front for missing information that would change the spec, then proceed. Rules:
- **Only ask high-leverage questions** — ones where different answers produce materially different specs (scope boundaries, target files, acceptance criteria, tech choices). Never ask what you can determine by reading the code (step 1).
- **Batch them**: one round, up to 3 questions, then stop.
- If the user says "just proceed" / "no time" / ignores the questions → fall back to **labeled assumptions** (step 3) and produce the spec anyway. Never block.

### 3. Compile the spec
Fill gaps in this order: (a) what the user stated, (b) what you learned from the code, (c) answers from the interview, (d) sensible defaults — **every (d) item tagged `[ASSUMPTION]`** so nothing is silently invented.

Preserve all explicit technical detail, constraints, and edge cases verbatim. Do not narrow scope or summarize intent.

## Output Format
Emit the spec inside a single fenced ```markdown block so the user can copy it. Omit a section only if it has genuinely no content.

```markdown
## Objective
One sentence: what "done" looks like.

## Task Breakdown
Numbered, atomic, ordered steps a coding agent can execute directly.

## Scope
- Files / directories to create or modify
- Files / directories that must NOT be touched
- Stack, frameworks, conventions to follow (cite what you detected)

## Constraints & Requirements
- Hard constraints (no exceptions)
- Soft constraints (flex only if technically necessary)
- Explicit style / convention rules

## Edge Cases to Handle
Edge cases the user named, plus standard ones for this task tagged [ASSUMPTION].

## Acceptance Criteria
Concrete, checkable conditions. Include the exact commands to verify (build/test/lint/run).

## Assumptions & Open Questions
Every [ASSUMPTION] made, and anything still unresolved. Empty if none.
```

## Worked Example

**User:** "enhance this: add rate limiting to the login endpoint"

**Interview (asked once, then proceed):**
1. Limit per IP, per account, or both?
2. Target: in-memory or shared store (Redis)? Single instance or multiple?
3. Response on limit hit — 429 with Retry-After, or silent lockout?

**Resulting spec (excerpt):**
```markdown
## Objective
Throttle repeated POST /auth/login attempts to mitigate credential-stuffing.

## Task Breakdown
1. Add a per-IP + per-account rate limiter to the /auth/login handler.
2. On breach, return 429 with a Retry-After header. [ASSUMPTION: 429 chosen; user didn't specify]
3. Back the counter with Redis (detected ioredis in package.json) keyed `rl:login:{ip}:{account}`.
...
## Acceptance Criteria
- 6th attempt within 60s → HTTP 429; verified by `npm test -- auth.rate-limit`.
- Limiter fails CLOSED (denies) if Redis is unreachable.

## Assumptions & Open Questions
- [ASSUMPTION] Window = 5 attempts / 60s (no value given).
```

## Quality Check (before outputting)
- [ ] Read all referenced context before writing the spec
- [ ] Interview covered only spec-changing gaps; no code-discoverable questions asked
- [ ] Every non-stated decision tagged [ASSUMPTION]
- [ ] No silent invention, no compressed intent, all stated constraints present
- [ ] Task breakdown directly executable by a coding agent
- [ ] Acceptance criteria include exact verification commands
- [ ] Produced the spec only — executed nothing
