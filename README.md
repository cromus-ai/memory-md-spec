# MEMORY.md

**The open specification for portable AI agent memory.**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Spec Version](https://img.shields.io/badge/spec-v1.0.0-blue.svg)](MEMORY.md)
[![Validator](https://img.shields.io/badge/validator-cromus.ai%2Fvalidator%2Fmemory-black.svg)](https://cromus.ai/validator/memory)
[![Part of the Cromus open spec stack](https://img.shields.io/badge/ecosystem-SKILL.md%20%C2%B7%20ETHOS.md%20%C2%B7%20MEMORY.md-purple.svg)](https://cromus.ai)

---

## What is MEMORY.md?

MEMORY.md is an open standard for describing what an AI agent remembers — across sessions, across agents, and across platforms.

It is the portable, human-readable, agent-executable memory layer for AI workflows. A single markdown file that any model can read, any orchestration framework can pass, and any team can version-control.

```
SKILL.md   →  what the agent does
ETHOS.md   →  how the agent behaves
MEMORY.md  →  what the agent remembers
```

---

## The Problem

Every AI agent faces the same three memory problems:

**Context window exhaustion** — As conversations grow, agents lose early context. Critical decisions and project state disappear — not because the agent forgot, but because the window ran out of room.

**Session discontinuity** — When a session ends, memory resets. The next session starts blind. Users re-explain context. Workflows restart from zero.

**Agent handoff failure** — In multi-agent systems, memory does not travel between agents. There is no standard for what should be passed forward.

MEMORY.md solves all three — at the model, infrastructure, and application level — with a single portable file.

---

## How It Works

A MEMORY.md file has five required sections:

| Section | Purpose | Compressible |
|---------|---------|--------------|
| **Identity** | What the agent always knows — role, purpose, hard constraints | Never |
| **Persistent Context** | Facts and decisions that survive across sessions | Summarize only |
| **Session Context** | What's active right now | Yes |
| **Compression Rules** | How the agent manages context when limits approach | Never |
| **Handoff Protocol** | How memory transfers between agents or sessions | Never |

---

## Quick Start

Create a `MEMORY.md` file in your project root:

```markdown
---
memory_id: my-agent-memory
version: 1.0.0
scope: persistent
agent_compatibility: any
compression_strategy: summarize
last_updated: 2026-04-02
owner: my-agent
---

## Identity
- **Role:** [Agent role]
- **Project:** [Project name]
- **Owner:** [Your name]
- **Purpose:** [One sentence]
- **Hard constraints:** [What this agent must never do]
- **Always true:** [Facts that never change]

## Persistent Context
### Decisions made
- [Decision] — [Date] — [Rationale]

### Project state
- **Current phase:** [Phase]
- **Last completed:** [Task]
- **Active blockers:** [Blockers or "none"]
- **Next action:** [What happens next]

## Session Context
- **Session started:** [ISO 8601 datetime]
- **Current task:** [Current task]
- **Recent summary:** [2-3 sentence summary]

## Compression Rules
### Trigger threshold
Compress at 80% context usage

### Priority order
1. Identity — never compress
2. Decisions made — never compress
3. Project state — summarize only
4. Session Context — re-summarize then discard

### Summarization style
Bullet. Target 20% of original length.

### What to discard first
- Conversation acknowledgements
- Completed step explanations

## Handoff Protocol
### Pass forward
- Full Identity section
- Full Persistent Context section
- Current task and recent summary

### Discard on handoff
- Active documents (reference by name only)
- Temporary constraints

### Outgoing summary format
```
MEMORY HANDOFF — [memory_id] — [datetime]
Current phase: [value]
Last completed: [value]
Next action: [value]
Active blockers: [value]
Key context: [2-3 sentences]
```
```

---

## Scope

| Scope | Lifetime | Shared | Use case |
|-------|----------|--------|----------|
| `session` | Single run | No | Stateless tasks, one-shot agents |
| `persistent` | Indefinite | No | Long-running solo agent workflows |
| `shared` | Indefinite | Yes | Multi-agent systems, team workflows |

---

## Compression Strategies

| Strategy | Description | Best for |
|----------|-------------|----------|
| `summarize` | Agent rewrites verbose sections into concise summaries | General purpose |
| `chunk` | Agent segments memory into discrete retrievable blocks | Long-running projects |
| `embed` | Memory is externalized to a vector store | High-volume persistent memory |
| `prune` | Agent drops low-priority sections per priority order | Token-constrained environments |

---

## Compatibility

MEMORY.md works with any model that can read markdown and follow instructions.

| Layer | How MEMORY.md works |
|-------|---------------------|
| **Model** | Loaded into system prompt or first user turn |
| **Infrastructure** | Passed as a file between agents in orchestration frameworks |
| **Application** | Stored alongside SKILL.md in workflow repos |

Works with: Claude, GPT-4, Gemini, Mistral, LLaMA, and any instruction-following model.

Works in: LangGraph, CrewAI, AutoGen, n8n, Make, Claude Projects, custom agents.

---

## Relationship to SKILL.md and ETHOS.md

MEMORY.md is the third spec in the Cromus open agent specification stack:

| Spec | Defines | GitHub |
|------|---------|--------|
| SKILL.md | What the agent does | [cromus-ai/skill-md-spec](https://github.com/cromus-ai/skill-md-spec) |
| ETHOS.md | How the agent behaves | [cromus-ai/ethos-md-spec](https://github.com/cromus-ai/ethos-md-spec) |
| MEMORY.md | What the agent remembers | [cromus-ai/memory-md-spec](https://github.com/cromus-ai/memory-md-spec) |

All three files travel with the workflow. None are platform-dependent.

---

## Validation

Validate your MEMORY.md file at:

**[cromus.ai/validator/memory](https://cromus.ai/validator/memory)**

The validator checks:
- All required sections present
- Valid frontmatter field values
- Compression Rules include trigger threshold and priority order
- Handoff Protocol includes pass-forward and discard lists

---

## Full Specification

Read the complete specification: **[MEMORY.md](MEMORY.md)**

---

## Contributing

Issues, feedback, and pull requests welcome.

- Open an issue to propose changes to the spec
- Fork and submit a PR for corrections or additions
- Share your MEMORY.md implementations in Discussions

---

## License

MIT License — free to use, fork, and build on.

---

## Community

- Validator: [cromus.ai/validator/memory](https://cromus.ai/validator/memory)
- Platform: [cromus.ai](https://cromus.ai)
- SKILL.md: [github.com/cromus-ai/skill-md-spec](https://github.com/cromus-ai/skill-md-spec)
- ETHOS.md: [github.com/cromus-ai/ethos-md-spec](https://github.com/cromus-ai/ethos-md-spec)

---

*MEMORY.md is an open specification maintained by Cromus.ai. Not affiliated with Anthropic, OpenAI, Google, or any model provider.*
