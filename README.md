# Agent Principal Development Framework

A comprehensive, modular framework for solo operators to develop web applications using AI agents. Optimized for DevOps/CD methodology with Claude Code.

## What is an Agent Principal?

An **Agent Principal** is a solo operator who orchestrates specialized AI agents to execute the full software development lifecycle. Instead of managing human teams, the Agent Principal directs AI agents that handle domain-specific tasks while retaining strategic control and approval authority.

## Quick Start

### New Project (Greenfield)
```
/APDF_init              # Initialize project
/APDF_phase 1           # Start Discovery phase
/APDF_next              # Advance to next step
/APDF_status            # Check progress
```

### Existing Project
```
/APDF_onboard           # Analyze and onboard codebase
/APDF_audit [category]  # Run security, quality, or full audit
/APDF_improve [target]  # Fix findings iteratively
/APDF_status            # View scores and findings
```

## Agent Team

| Agent | Domain | Automation |
|-------|--------|------------|
| STRATEGY | Product, requirements, prioritization | Assisted |
| DESIGN | UX/UI, wireframes, design systems | Assisted |
| ARCHITECTURE | System design, schemas, APIs | Full |
| BACKEND | Server-side implementation | Full |
| FRONTEND | Client-side implementation | Full |
| QUALITY | Testing, QA, performance | Full |
| DEVOPS | Infrastructure, CI/CD, deployment | Full |
| SECURITY | Security review, compliance | Assisted |

**Assisted** = Agent proposes, Agent Principal approves
**Full** = Agent executes autonomously

## Workflow Phases

1. **Discovery** - Define problem, users, requirements
2. **Design** - Wireframes, UX flows, design system
3. **Architecture** - Database, APIs, infrastructure
4. **Backend** - Server implementation
5. **Frontend** - Client implementation
6. **Testing** - Quality assurance
7. **Deployment** - CI/CD, launch
8. **Documentation** - User and developer docs
9. **Operations** - Monitoring, maintenance

## Project Structure

```
├── agents/              # Agent definitions (8 agents)
├── phases/              # Phase step definitions (9 phases)
├── methodologies/       # Workflow configurations
├── .claude/
│   ├── commands/        # Slash command definitions (APDF_*.md)
│   ├── settings.json    # Hooks and permissions
│   └── CLAUDE.md        # Project instructions
├── state.json           # Progress and audit tracking (template)
├── state.example.json   # Example of populated state
└── meta.json            # Schema metadata
```

## State Management

The `state.json` file tracks all project progress, audit findings, and deliverables.

### How It Works

1. **Template State**: The framework ships with an empty `state.json` template
2. **Initialization**: Running `/APDF_init` or `/APDF_onboard` populates it with your project data
3. **Tracking**: Commands update state as you progress through phases
4. **Persistence**: Commit `state.json` to your repo to preserve progress across sessions

### Files

| File | Purpose |
|------|---------|
| `state.json` | Your project's live state (starts empty, gets populated) |
| `state.example.json` | Reference showing what a populated state looks like |

### Example Workflow

```
# Fresh copy of framework
state.json → empty template

# After running /APDF_onboard
state.json → populated with:
  - Project name and description
  - Codebase profile (languages, frameworks)
  - Phase assessments
  - Audit findings and scores
```

## Commands Reference

| Command | Description |
|---------|-------------|
| `/APDF_init` | Initialize new project |
| `/APDF_onboard` | Onboard existing codebase |
| `/APDF_audit [category]` | Run codebase audit |
| `/APDF_improve [target] [scope]` | Run improvement cycle |
| `/APDF_phase <n>` | Start/view phase |
| `/APDF_step <id>` | Execute specific step |
| `/APDF_status` | View progress |
| `/APDF_next` | Advance to next step |
| `/APDF_agent <id>` | Invoke agent directly |
| `/APDF_deliver` | Manage deliverables |
| `/APDF_approve` | Approve pending items |
| `/APDF_gate` | Run quality gate checks |

## Usage with Claude Code

1. Copy this framework to your project root
2. Open Claude Code in the project directory
3. Run `/APDF_init` for new projects or `/APDF_onboard` for existing
4. Follow the guided workflow

## Customization

- Add custom agents in `agents/`
- Modify phase steps in `phases/`
- Create custom slash commands in `.claude/commands/`
- Extend quality gates in methodology files

## License

MIT
