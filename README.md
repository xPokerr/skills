# xPokerr's AI Agent Skills

A collection of high-fidelity skills for AI coding agents to improve task specification and project documentation.

These skills are compatible with any coding agent that supports the `skills` standard (e.g., Claude Code, Cursor, Cline, Codex, Continue, Gemini CLI, Roo Code, Windsurf).

---

## Available Skills

### 1. 🚀 Prompt Enhancer (`prompt-enhancer`)
Turns a rough, vague user request into a structured, execution-ready task specification before any code is modified.
- **Trigger keywords:** `enhance`, `compile`, `ottimizza`, `compila`, `make this prompt executable`.
- **Functionality:** Conducts a quick 3-question clarifying interview, reads the codebase for grounding, and outputs a complete spec detailing objective, task breakdown, constraints, edge cases, and assumptions.

### 2. 🗺️ Project Roadmap (`project-roadmap`)
Creates and maintains a live `ROADMAP.md` at the root of a project to act as a machine-readable compass for developers and AI agents.
- **Trigger keywords:** `roadmap`, `vision`, `project plan`, `current status`, `changelog`.
- **Functionality:** Scans for or initializes a structured `ROADMAP.md` (complete with YAML metadata, Mermaid system architecture, exact code-level status checklists, and version changelogs). Enforces updating the roadmap and logging version history at the end of every feature addition.

---

## Installation

You can install all skills in this repository using the `skills` CLI:

### Global Installation (Recommended)
To make both skills active globally across all your workspaces:

```bash
npx skills@latest add xPokerr/skills -g -a '*' -y
```

### Local Project-Specific Installation
To install the skills only in the current project:

```bash
npx skills@latest add xPokerr/skills
```

### Updating
To update the skills after a new release/push:

```bash
npx skills@latest update
```
