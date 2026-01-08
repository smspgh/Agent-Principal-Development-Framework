# Agent Principal Workflow - Project Configuration

This project uses the **Agent Principal** methodology for solo-operator software development with AI agents.

## Quick Reference

### Slash Commands

**Greenfield Projects:**
| Command | Description |
|---------|-------------|
| `/APDF_init` | Initialize a new project |
| `/APDF_next` | Advance to next pending step |

**Existing Projects:**
| Command | Description |
|---------|-------------|
| `/APDF_onboard` | Onboard existing codebase |
| `/APDF_audit [category]` | Run codebase audit (security, quality, etc.) |
| `/APDF_improve [target] [scope]` | Run improvement cycle |

**Both Modes:**
| Command | Description |
|---------|-------------|
| `/APDF_phase <n>` | Start or view a phase (1-9) |
| `/APDF_step <id>` | Execute a specific step (e.g., 1.3) |
| `/APDF_status` | View current progress |
| `/APDF_agent <id>` | Invoke a specialized agent |
| `/APDF_deliver` | View or generate deliverables |
| `/APDF_approve` | Approve pending decisions |
| `/APDF_gate` | Run quality gate checks |

### Agent Team
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

### Project Modes
| Mode | Entry Command | Workflow |
|------|---------------|----------|
| **Greenfield** | `/APDF_init` | Linear phase progression |
| **Existing** | `/APDF_onboard` | Audit-driven improvement cycles |

### Workflow Phases
1. Discovery and Planning
2. Design and Prototyping
3. Architecture and Infrastructure
4. Backend Development
5. Frontend Development
6. Testing and Quality Assurance
7. Deployment and Launch
8. Documentation
9. Operations and Maintenance

### Existing Status Values (for onboarded projects)
| Status | Meaning |
|--------|---------|
| `existing` | Deliverables exist and are current |
| `partial` | Some deliverables exist, others missing |
| `legacy` | Exists but needs modernization |
| `missing` | Phase not addressed in codebase |
| `needs-update` | Exists but out of date |

## Project Files

- `state.json` - Current project state and progress
- `agents/*.json` - Agent definitions and capabilities
- `phases/*.json` - Phase step definitions
- `methodologies/agent-principal-devops.json` - Methodology configuration

## Conventions

### Deliverable Tracking
All deliverables are tracked in `state.json` with:
- Creation timestamp
- Generating agent
- Approval status
- Content or reference

### Quality Gates
Phase transitions require quality gate checks. Gates verify:
- Required deliverables exist
- Approvals obtained for assisted agents
- No blocking issues

### Approval Workflow
- **Assisted Agents** (Strategy, Design, Security): Propose outputs for Agent Principal review
- **Full Automation Agents** (Architecture, Backend, Frontend, Quality, DevOps): Execute autonomously

## Getting Started

### New Project (Greenfield)
1. Run `/APDF_init` to initialize your project
2. Run `/APDF_phase 1` to begin Discovery
3. Use `/APDF_next` to advance through steps
4. Run `/APDF_status` anytime to check progress

### Existing Project (Onboarding)
1. Run `/APDF_onboard` to analyze and onboard codebase
2. Run `/APDF_audit` to get detailed findings by category
3. Run `/APDF_improve [target] quick` to fix quick wins
4. Run `/APDF_status` to see audit scores and progress

## Notes for Claude

When working in this project:
- Always check `state.json` for current context
- Load appropriate agent definition before executing agent-specific tasks
- Update `state.json` after completing steps or generating deliverables
- Enforce quality gates before phase transitions
- Track all decisions in the decisions array
