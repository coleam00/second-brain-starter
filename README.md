# Build Your AI Second Brain with Claude Code

A skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that generates a personalized Product Requirements Document (PRD) for building your own AI second brain - a proactive, persistent AI assistant that knows your context, remembers across sessions, and keeps you informed.

**Watch the overview:** [How I Built My AI Second Brain with Claude Code](https://youtube.com/@ColeMedin) (YouTube)

## What This Does

You fill out a simple requirements template describing your tools, workflow, and preferences. Then Claude Code generates a phased build plan tailored to your setup - covering memory, integrations, skills, a proactive heartbeat, chat interface, and security hardening.

The generated PRD gives you (or your coding agent) a step-by-step blueprint for building a second brain that:

- **Remembers** across sessions - decisions, preferences, context, all in markdown files
- **Connects** to your platforms - Gmail, Slack, Calendar, Asana, Linear, GitHub, and more
- **Proactively monitors** your email, calendar, and tasks every 30 minutes
- **Chats** with you through Slack (or Discord, or any messaging platform)
- **Searches** months of memory with hybrid keyword + semantic search
- **Drafts** replies in your voice using RAG on your past messages
- **Tracks habits** with daily nudges inspired by Atomic Habits

## Quick Start

### 1. Install the Skill

Copy the `.claude/skills/create-second-brain-prd/` directory into your project:

```bash
# Clone this repo
git clone https://github.com/coleam00/second-brain-starter.git

# Copy the skill into your project
cp -r second-brain-starter/.claude/skills/create-second-brain-prd \
      your-project/.claude/skills/create-second-brain-prd
```

Or just copy the `.claude/` folder from this repo into an existing project.

### 2. Fill Out the Requirements Template

Copy the template to your workspace and fill it out:

```bash
cp .claude/skills/create-second-brain-prd/my-second-brain-requirements.md \
   ./my-second-brain-requirements.md
```

The template has 8 sections:

1. **About You** - Name, role, timezone
2. **Your Platforms** - Which tools you use (Gmail, Slack, Linear, etc.)
3. **Top Tasks** - 3-5 things you want AI to handle proactively
4. **Proactivity Level** - Observer, Advisor, Assistant, or Partner
5. **Security Boundaries** - What the agent should never do without permission
6. **Memory Categories** - What types of knowledge matter to you
7. **Infrastructure** - OS, local vs. VPS deployment
8. **Integration Priority** - Which 3 integrations to build first

See `example-my-second-brain-requirements.md` in the skill directory for a completed example.

### 3. Generate Your PRD

Open Claude Code in your project and run:

```
/create-second-brain-prd ./my-second-brain-requirements.md
```

Claude will:
1. Read your requirements
2. Load the architecture reference blueprint
3. Research every tool and API in your stack via web search
4. Generate a personalized 9-phase PRD at `.agent/plans/second-brain-prd.md`

### 4. Build It

Follow the phases in your PRD. Each phase includes:
- What to build and why
- Key files to create (with paths)
- Dependencies on previous phases
- Complexity estimate
- Personalization notes based on your answers

The recommended build order:

| Phase | What | Complexity |
|-------|------|------------|
| 1 | Memory Layer (SOUL.md, USER.md, MEMORY.md, daily logs) | Low |
| 2 | Hooks (SessionStart, PreCompact, SessionEnd) | Medium |
| 3 | Memory Search (hybrid keyword + semantic) | Medium |
| 4 | Integrations (your top 3 platforms) | Medium each |
| 5 | Skills (vault structure + custom skills) | Low-Medium |
| 6 | Proactive Systems (heartbeat + daily reflection) | High |
| 7 | Chat Interface (Slack/Discord bot) | High |
| 8 | Security Hardening (sanitization, guardrails) | Medium |
| 9 | Deployment (local scheduler or VPS) | Medium |

## Architecture Overview

The second brain is built on Claude Code and the Claude Agent SDK. No massive framework - just markdown files, Python scripts, and an Obsidian vault.

```
Memory Layer (center of everything)
    SOUL.md - Agent personality, values, boundaries
    USER.md - Your profile, accounts, preferences
    MEMORY.md - Key decisions, lessons, active projects
    daily/YYYY-MM-DD.md - Timestamped session logs

Hooks (context persistence)
    SessionStart - Loads memory into every conversation
    PreCompact - Saves context before auto-compaction
    SessionEnd - Captures decisions on exit

Integrations (platform connections)
    Python CLI wrapper pattern - LLM never sees API keys
    query.py gmail list / query.py asana overdue / etc.

Skills (extensible capabilities)
    Progressive disclosure - metadata always loaded, full instructions on demand

Heartbeat (proactive monitoring)
    Python gathers data -> Claude reasons -> notifications sent
    ~$0.05/run vs $0.38 with MCP tool calls

Memory Search (hybrid RAG)
    FastEmbed (local ONNX) + SQLite/Postgres
    70% vector + 30% keyword = best of both worlds
```

## Proactivity Levels

Your choice in the requirements template shapes the entire system:

| Level | What It Does |
|-------|-------------|
| **Observer** | Notifications only. Never takes action. |
| **Advisor** | Drafts emails/messages for your review. Tracks habits with suggestions. |
| **Assistant** | Auto-organizes files, auto-logs decisions. Asks for anything external. |
| **Partner** | Sends low-risk messages, completes routine tasks. Asks only for irreversible actions. |

## Learn More

- **Full workshop:** Join the [Dynamous community](https://dynamous.ai) for a 4-hour hands-on workshop covering every module
- **Claude Agent SDK:** [Documentation](https://code.claude.com/docs/en/agent-sdk/overview)
- **Obsidian:** [obsidian.md](https://obsidian.md)
