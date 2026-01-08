# Agent Command

Directly invoke a specialized agent for a specific task.

## Usage
`/agent <agentId>` - Start interactive session with agent
`/agent <agentId> <task description>` - Execute specific task with agent

## Available Agents

| Agent ID | Name | Primary Use |
|----------|------|-------------|
| strategy | Strategy Agent | Product thinking, requirements, prioritization |
| design | Design Agent | UX/UI specifications, wireframes, design systems |
| architecture | Architecture Agent | System design, schemas, API contracts |
| backend | Backend Agent | Server-side implementation |
| frontend | Frontend Agent | Client-side implementation |
| quality | Quality Agent | Testing, QA, performance |
| devops | DevOps Agent | Infrastructure, CI/CD, deployment |
| security | Security Agent | Security review, compliance, threat modeling |

## Instructions

When the user runs this command:

1. **Parse Agent ID**
   - Validate agent exists in `agents/` directory
   - Load agent definition JSON

2. **Load Agent Context**
   - Apply agent's `systemPrompt`
   - Load relevant project context from state.json
   - Include any completed deliverables the agent needs

3. **Execute Task**
   If task description provided:
   - Execute the specific task
   - Generate appropriate output
   - Track in state.json if produces deliverable

   If no task (interactive mode):
   - Introduce agent capabilities
   - Ask what the user wants to accomplish
   - Guide through agent's domain

4. **Handle Approval**
   If agent has `approvalRequired: true`:
   - Present output for review
   - Wait for approval before recording as complete

## Output Format (Task Mode)

```
## Security Agent

**Task:** Review authentication implementation for vulnerabilities

### Analysis

Reviewing code in `src/auth/`...

**Findings:**

1. **HIGH** - Password hashing uses MD5 (src/auth/password.ts:23)
   - Recommendation: Switch to bcrypt or Argon2

2. **MEDIUM** - No rate limiting on login endpoint (src/auth/login.ts:45)
   - Recommendation: Add rate limiting middleware

3. **LOW** - Session tokens don't expire (src/auth/session.ts:12)
   - Recommendation: Add 24h expiration

### Summary
- Critical issues: 1
- Medium issues: 1
- Low issues: 1

**Approval Required:** Please review findings and run `/approve` to acknowledge.
```

## Output Format (Interactive Mode)

```
## Architecture Agent

I'm the Architecture Agent, specialized in system design and technical planning.

I can help you with:
- Database schema design
- API architecture and contracts
- System component design
- Technology selection
- Infrastructure planning
- Architecture Decision Records

What would you like to work on?
```
