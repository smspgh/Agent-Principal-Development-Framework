# Improvement Cycle

Run a targeted improvement cycle on a specific area. Designed for existing codebases.

## Usage

```
/APDF_improve [target] [scope]
```

Targets:
- `security` - Fix security findings
- `quality` - Improve code quality and tests
- `performance` - Optimize performance
- `techdebt` - Reduce technical debt
- `documentation` - Improve docs
- `dependencies` - Update and clean dependencies
- `[finding-id]` - Fix a specific audit finding (e.g., `SEC-001`)

Scope:
- `quick` - Quick wins only (small effort)
- `sprint` - Sprint-sized batch of improvements
- `full` - Comprehensive improvement cycle

## Instructions

### 1. Load Current State

Read from `state.json`:
- Audit findings for the target area
- Previous improvement attempts
- Current scores

### 2. Plan Improvement Cycle

Based on target and scope, create improvement plan:

```json
{
  "improvementCycle": {
    "id": "IMP-001",
    "target": "security",
    "scope": "quick",
    "startedAt": "<timestamp>",
    "status": "planning|in-progress|completed|blocked",
    "items": [
      {
        "findingId": "SEC-001",
        "title": "Fix SQL Injection",
        "agent": "BACKEND",
        "effort": "small",
        "priority": 1,
        "status": "pending|in-progress|completed|skipped"
      }
    ],
    "metrics": {
      "planned": 0,
      "completed": 0,
      "skipped": 0,
      "scoreImprovement": 0
    }
  }
}
```

### 3. Execute Improvements

For each item in the plan:

1. **Invoke appropriate agent** based on finding category
2. **Make the fix** following best practices
3. **Verify the fix** with tests or manual check
4. **Update state** marking item complete
5. **Move to next item** or report blocker

### Agent Routing

| Target | Primary Agent | Supporting Agents |
|--------|---------------|-------------------|
| security | SECURITY | BACKEND, FRONTEND |
| quality | QUALITY | BACKEND, FRONTEND |
| performance | QUALITY | BACKEND, ARCHITECTURE |
| techdebt | ARCHITECTURE | BACKEND, FRONTEND |
| documentation | ARCHITECTURE | All agents |
| dependencies | DEVOPS | SECURITY |

### 4. Quick Wins (scope: quick)

Filter for:
- Effort: `small` only
- Impact: High or medium severity
- Dependencies: None or minimal

Typical quick wins:
- Add missing input validation
- Fix linting errors
- Update a single deprecated API
- Add missing error handling
- Write missing tests for critical path
- Fix security header configuration

### 5. Sprint Scope (scope: sprint)

Batch improvements targeting:
- 5-10 items per sprint
- Mix of efforts (mostly small/medium)
- Coherent theme (e.g., all security, all in one module)
- Achievable in 2-4 hours of agent work

### 6. Full Cycle (scope: full)

Comprehensive improvement:
- All findings in category
- Includes large effort items
- May span multiple sessions
- Creates sub-cycles for tracking

### 7. Report Results

After cycle completion:

```
Improvement Cycle Complete!

Target: Security
Scope: Quick Wins
Duration: 45 minutes

Results:
- Completed: 4/5 items
- Skipped: 1 (needs architectural change)

Fixes Applied:
[x] SEC-001: SQL Injection fixed (parameterized queries)
[x] SEC-003: Session expiry implemented
[x] SEC-004: Security headers added
[x] SEC-005: Debug mode disabled
[ ] SEC-002: Rate limiting (skipped - needs infrastructure)

Score Change: 65 -> 82 (+17 points)

Remaining Items:
- SEC-002: Rate limiting (large effort)

Run /APDF_audit security to verify improvements.
Run /APDF_improve security sprint to continue.
```

## State Tracking

Update `state.json` after each cycle:

```json
{
  "improvementHistory": [
    {
      "cycleId": "IMP-001",
      "target": "security",
      "scope": "quick",
      "completedAt": "<timestamp>",
      "itemsCompleted": 4,
      "itemsSkipped": 1,
      "scoreBefore": 65,
      "scoreAfter": 82
    }
  ]
}
```

## Improvement Patterns by Target

### Security Improvements
1. Input validation and sanitization
2. Authentication/authorization fixes
3. Secrets rotation and management
4. Dependency vulnerability patches
5. Security header configuration
6. CORS policy updates
7. Rate limiting implementation

### Quality Improvements
1. Add missing tests
2. Fix linting violations
3. Reduce code duplication
4. Improve error handling
5. Add type annotations
6. Remove dead code
7. Refactor complex functions

### Performance Improvements
1. Add database indexes
2. Implement caching
3. Fix N+1 queries
4. Optimize bundle size
5. Add lazy loading
6. Implement pagination
7. Optimize images/assets

### Tech Debt Reduction
1. Resolve TODO/FIXME comments
2. Update deprecated APIs
3. Remove unused dependencies
4. Consolidate duplicate logic
5. Extract reusable components
6. Improve naming conventions
7. Add missing abstractions

## Example Session

```
> /APDF_improve security quick

Starting Security Improvement Cycle (Quick Wins)...

Loading audit findings...
Found 5 security issues (1 high, 2 medium, 2 low)

Quick wins available: 4 items

Plan:
1. [HIGH] SEC-001: Fix SQL injection (small effort)
2. [MED]  SEC-003: Add session expiry (small effort)
3. [LOW]  SEC-004: Add security headers (small effort)
4. [LOW]  SEC-005: Disable debug mode (small effort)

Skipping:
- SEC-002: Rate limiting (medium effort, needs infra)

Proceeding with 4 items...

[1/4] Fixing SEC-001: SQL Injection
Invoking BACKEND agent...
- Located: src/api/users.ts:45
- Fix: Converting to parameterized query
- Verified: Tests passing

[2/4] Fixing SEC-003: Session Expiry
...

Cycle Complete!
Run /APDF_status to see updated scores.
```
