# Approve Command

Approve pending decisions, deliverables, or agent recommendations.

## Usage
`/approve` - Approve the most recent pending item
`/approve <item>` - Approve specific pending item
`/approve --list` - List all items awaiting approval
`/approve --reject <item> "<reason>"` - Reject with feedback

## Instructions

When the user runs this command:

1. **List Mode** (--list)
   - Scan state.json for items with `approvalRequired: true` and `status: pending`
   - Show categorized list

2. **Approve Mode** (default or with item name)
   - Find the pending item
   - Update status to "approved"
   - Record approval timestamp
   - Record approver as "Agent Principal"
   - Trigger any post-approval actions

3. **Reject Mode** (--reject)
   - Mark item as "revision_requested"
   - Store rejection reason
   - Notify appropriate agent for revision

4. **Items Requiring Approval**
   These agent outputs require explicit approval:
   - STRATEGY: Requirements, MVP scope, prioritization decisions
   - DESIGN: Wireframes, design system, UI mockups
   - SECURITY: Threat models, security findings, compliance status

## Approval Tracking

Store in state.json:
```json
{
  "decisions": [
    {
      "id": "dec-001",
      "type": "deliverable",
      "name": "mvp-scope",
      "stepId": "1.5",
      "agentId": "STRATEGY",
      "status": "approved",
      "createdAt": "2026-01-08T10:00:00Z",
      "approvedAt": "2026-01-08T10:30:00Z",
      "approvedBy": "Agent Principal"
    }
  ]
}
```

## Output Format (List)

```
## Pending Approvals

### Deliverables
1. **design-system** (Step 2.3)
   Agent: DESIGN
   Created: 10 minutes ago
   Preview: Color palette, typography, spacing scale defined

2. **threat-model** (Step 1.9)
   Agent: SECURITY
   Created: 2 hours ago
   Preview: 8 threats identified, 3 high severity

### Decisions
3. **tech-stack** (Step 1.8)
   Agent: ARCHITECTURE
   Created: 1 hour ago
   Preview: React + Node.js + PostgreSQL recommended

Run /approve <number or name> to approve, or /approve --reject <name> "reason"
```

## Output Format (Approve)

```
## Approved: design-system

**Status:** Approved
**Approved at:** 2026-01-08 14:32:00

The design system has been recorded and will be used as reference for:
- Frontend implementation (Phase 5)
- Component development
- UI consistency checks

Next pending approval: threat-model
Run /approve to continue, or /status to see progress.
```

## Output Format (Reject)

```
## Revision Requested: threat-model

**Reason:** Need more detail on mitigation strategies for high-severity threats.

The Security Agent will revise the threat model with:
- Detailed mitigation steps for each high-severity threat
- Estimated effort for each mitigation
- Priority recommendations

Run /agent security to work on revisions, or /step 1.9 to regenerate.
```
