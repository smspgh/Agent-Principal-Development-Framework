# Deliver Command

Generate, view, or update a project deliverable.

## Usage
`/deliver` - List all deliverables and their status
`/deliver <name>` - View or generate specific deliverable
`/deliver <name> --regenerate` - Regenerate existing deliverable

## Instructions

When the user runs this command:

1. **List Mode** (no arguments)
   - Read state.json for deliverables array
   - Group by phase
   - Show status (pending, complete, outdated)

2. **View/Generate Mode** (with name)
   - Search for deliverable in state.json
   - If exists and complete: display it
   - If pending: generate with appropriate agent
   - If not found: suggest similar deliverables

3. **Regenerate Mode** (--regenerate flag)
   - Mark existing deliverable as outdated
   - Generate fresh version
   - Track version history

4. **Deliverable Storage**
   Store in state.json under deliverables array:
   ```json
   {
     "name": "user-personas",
     "stepId": "1.3",
     "phase": 1,
     "status": "complete",
     "createdAt": "2026-01-08T10:30:00Z",
     "updatedAt": null,
     "agentId": "STRATEGY",
     "content": { ... },
     "approvedBy": "Agent Principal",
     "approvedAt": "2026-01-08T11:00:00Z"
   }
   ```

## Common Deliverables by Phase

**Phase 1 - Discovery:**
- problem-statement, value-proposition, user-personas, user-stories, mvp-scope, compliance-requirements, tech-stack, threat-model, slo-definitions

**Phase 2 - Design:**
- sitemap, user-flows, wireframes, design-system, ui-mockups, prototype

**Phase 3 - Architecture:**
- database-schema, api-specification, business-rules, branching-strategy, iac-templates, container-config

**Phase 4 - Backend:**
- auth-system, api-endpoints, integration-adapters, background-jobs, api-documentation

**Phase 5 - Frontend:**
- component-library, pages, state-management, forms, responsive-layouts

**Phase 6 - Testing:**
- unit-tests, integration-tests, e2e-tests, security-scan, performance-tests, accessibility-audit

**Phase 7 - Deployment:**
- infrastructure, ci-cd-pipeline, ssl-config, deployment-strategy, observability-stack

**Phase 8 - Documentation:**
- readme, api-docs, architecture-docs, runbooks

**Phase 9 - Operations:**
- monitoring-dashboards, alerting-rules, incident-procedures, backup-procedures

## Output Format (List)

```
## Project Deliverables

### Phase 1: Discovery (8/9 complete)
- [x] problem-statement
- [x] value-proposition
- [x] user-personas
- [x] user-stories
- [x] mvp-scope
- [x] compliance-requirements
- [x] tech-stack
- [x] threat-model
- [ ] slo-definitions <- pending

### Phase 2: Design (0/6 complete)
- [ ] sitemap
- [ ] user-flows
- [ ] wireframes
- [ ] design-system
- [ ] ui-mockups
- [ ] prototype

Run /deliver <name> to view or generate any deliverable.
```

## Output Format (View)

```
## Deliverable: user-personas

**Status:** Complete
**Created:** 2026-01-08
**Agent:** STRATEGY
**Step:** 1.3

---

### Persona 1: Project Manager Priya

**Demographics:**
- Age: 32-45
- Role: Mid-level project manager
- Company size: 50-500 employees

**Goals:**
- Track team progress efficiently
- Reduce status meeting overhead
- Get early warning on blockers

**Pain Points:**
- Too many tools to check
- Manual status collection
- Delayed visibility into issues

**Key Quote:**
"I spend 2 hours a day just collecting updates from my team."

---

[Additional personas...]
```
