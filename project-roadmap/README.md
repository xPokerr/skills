# Project Roadmap Skill (project-roadmap)

This skill enables AI agents and developers to systematically create, maintain, and synchronize a `ROADMAP.md` file at the root of a project.

It serves as a **live compass** that aligns incoming agents and teams on the project's vision, system architecture, exact code-level status checklists, and changelogs.

## Why use this skill?

When working with LLM-based coding agents:
1. **Instant Context Alignment:** Agents read the `ROADMAP.md` at the start of a session to understand what the project is, the primary stack, and which components are completed or planned.
2. **Context File Mapping:** By requiring agents to write absolute `file://` scheme URIs to the source files, agents can jump directly to the right files without scanning the entire workspace.
3. **Continuous Tracking:** The agent is forced to update the roadmap and changelog at the end of every feature addition, ensuring the documentation never falls out of sync.

## Installation

### 1. Global Installation (Antigravity/Gemini)
To make this skill globally active across all your workspaces:

1. Copy the `SKILL.md` file to your global customizations root:
   ```bash
   mkdir -p ~/.gemini/config/skills/project-roadmap
   cp SKILL.md ~/.gemini/config/skills/project-roadmap/SKILL.md
   ```
2. The agent will automatically discover and load the skill.

### 2. Project-Specific Installation
To enable this skill for a single project:
1. Create a `.agents/skills/project-roadmap` folder in your project root.
2. Copy `SKILL.md` into it.

## How it works

Once loaded, the agent will trigger on terms like `roadmap`, `vision`, `project plan`, `current status`, or `changelog`. It will:
1. Scan for the root `ROADMAP.md`.
2. Initialize it using the standardized template if it doesn't exist.
3. Maintain it continuously, updating status badges (`[Complete]`, `[In Progress]`, `[Planned]`) and tracking modifications in the Changelog.
