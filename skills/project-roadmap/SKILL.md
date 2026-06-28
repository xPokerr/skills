---
name: project-roadmap
description: Create, maintain, and synchronize the project's ROADMAP.md file to serve as a high-fidelity guide/compass for human developers and AI agents. Use when initializing a project, adding features, or auditing project status.
---

# Project Roadmap & Vision Sync Skill

This skill enforces the creation and continuous maintenance of a `ROADMAP.md` file in the root of the project. This file serves as a machine-readable compass and status tracker for incoming AI agents and human developers.

## Instructions

Whenever you are asked to initialize a new project, add features, or troubleshoot a system, follow these steps:

### 1. Verification & Initialization
At the start of your session, check if `ROADMAP.md` exists in the root of the workspace:
- **If missing:** Ask the user if they want to initialize it. If approved, create a `ROADMAP.md` in the root using the template below.
- **If present:** Read `ROADMAP.md` immediately to understand the project vision, stack constraints, remote access setup, and current status checklist.

### 2. Standardized Roadmap Template
The `ROADMAP.md` file MUST follow this structure:

```markdown
---
status: [active | maintenance | paused]
last_updated: YYYY-MM-DD
primary_stack:
  backend: [e.g. Node.js (TypeScript)]
  frontend: [e.g. React / TailwindCSS]
  database: [e.g. PostgreSQL]
  integrations: [e.g. Stripe, OpenAI]
remote_access: [e.g. Tailscale, Cloudflare Tunnels, None]
---

# [Project Name] Roadmap & Project Vision

This document tracks the ultimate goals, current state, and future milestones of the project. It serves as the single source of truth for understanding the project's direction and current status, and **must be updated continuously whenever a new feature or function is added to the codebase**.

---

## 1. Project Vision

Describe the ultimate objective of the project. Explain what the final product does, who it is for, its key architectural choices, and the long-term goal.

---

## 2. System Architecture

Include a Mermaid diagram representing the flow of data, components, services, and communication layers (e.g. databases, client apps, cloud APIs).

---

## 3. Current Status & Feature Implementation

Provide a categorized, checklist-style view of all modules. Every status entry must have:
- A status badge (`[Complete]`, `[In Progress]`, `[Planned]`).
- A link to the main code files using absolute `file://` URIs.

### Legend:
- `[Complete]` - Feature is fully implemented, verified, and in production.
- `[In Progress]` - Feature is currently being actively developed or tested.
- `[Planned]` - Feature is scheduled for development in future milestones.

### [Component/Layer Name]
- `[Status]` **Feature Name:** Description. Links to [filename](file:///absolute/path/to/file) or [className](file:///absolute/path/to/file#L12).
```

### 3. Continuous Synchronization Rule
Every time you complete a task, implement a feature, or resolve a bug:
1. Locate `ROADMAP.md`.
2. Update the status legends of modified features (e.g., move from `[Planned]` or `[In Progress]` to `[Complete]`).
3. If new files were created, add them with absolute `file://` scheme links under the corresponding status category.
4. Update the `last_updated` field in the YAML frontmatter.
5. Append a descriptive version/changelog note in the **Changelog** section.
