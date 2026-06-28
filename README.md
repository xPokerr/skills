# Skills For Real AI Engineers

My agent skills that I use every day to keep AI coding sessions structured, aligned, and synchronized.

Developing applications with AI agents is powerful, but prone to **drift**. Vague prompts lead to broken code, and a lack of project tracking leads to out-of-sync documentation.

These skills are designed to be small, easy to adapt, and composable. They solve the most common agent failure modes by introducing strict task spec compilation and automated project roadmap sync. Enjoy.

---

## Quickstart (30-second setup)

To install globally across all your workspaces and coding agents:

```bash
npx skills@latest add xPokerr/skills -g -a '*' -y
```

To install locally in a single project directory:

```bash
npx skills@latest add xPokerr/skills
```

To update your skills to the latest version:

```bash
npx skills@latest update
```

---

## Why These Skills Exist

I built these skills to fix the two most common failure modes I see when working with Claude Code, Cursor, Cline, and other coding agents.

### #1: The Agent Guessed the Spec (Vague Prompts)

> "No-one knows exactly what they want"
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**The Problem**: Handing a vague, rough request to a coding agent and hoping for the best. The agent will make silent, dangerous assumptions, invent requirements, and execute them incorrectly.

**The Fix** is to use:
- [**`prompt-enhancer`**](./skills/prompt-enhancer/SKILL.md)

**How it works**: Before writing code, the agent conducts a quick 3-question clarifying interview, reads the codebase, and outputs a complete, executable spec outlining objectives, task breakdowns, constraints, and labeled assumptions.

---

### #2: The Agent Has No Compass (Code Drift)

> "If you don't know where you are going, any road will get you there."
>
> Lewis Carroll, Alice in Wonderland

**The Problem**: AI agents are dropped into a codebase, write code, and finish their turn without updating the big picture. As a result, the next agent has no idea of the actual project goals, architectural constraints, or current status.

**The Fix** is to use:
- [**`project-roadmap`**](./skills/project-roadmap/SKILL.md)

**How it works**: The agent scans for or initializes a structured `ROADMAP.md` in the project root containing YAML metadata, a Mermaid system architecture diagram, and an exact code-level status checklist. The skill enforces updating the roadmap and logging the version changelog at the end of every feature addition.

---

## Compatibility

Works with any coding agent that supports the `skills` standard: Claude Code, Cursor, Cline, Codex, Continue, Gemini CLI, Roo Code, Windsurf, and many others.

---

## Repository Structure

```
skills/
  project-roadmap/
    SKILL.md    — the roadmap sync skill definition
  prompt-enhancer/
    SKILL.md    — the prompt enhancer skill definition
```
