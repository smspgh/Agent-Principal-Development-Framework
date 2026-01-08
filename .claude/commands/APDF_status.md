# Status Command

Display current project progress and next recommended actions.

## Usage
`/APDF_status` - Show full project status
`/APDF_status brief` - Show condensed status
`/APDF_status audit` - Show audit results summary (existing projects)

## Instructions

When the user runs this command:

1. **Load State**
   Read `state.json` for current project state
   Check `projectMode` to determine display format

2. **For Greenfield Projects (projectMode: "greenfield")**
   - Calculate step completion metrics
   - Current phase progress percentage
   - Overall project progress percentage
   - Time since project start (if tracked)
   - Identify current phase and step
   - Check quality gates
   - Show pending deliverables

3. **For Existing Projects (projectMode: "existing")**
   - Show codebase profile summary
   - Display audit scores by category
   - List tech debt count and priorities
   - Show improvement cycle status
   - Display phase existing status mapping
   - Count findings by severity
   - Recommend next actions based on findings

4. **Generate Recommendations**
   - Suggest next action (greenfield: next step, existing: next improvement)
   - Flag any overdue items
   - Highlight decisions awaiting approval

## Output Format (Full)

```
# Project Status: TaskFlow

## Overview
**Phase:** 4 of 9 - Backend Development
**Progress:** 42% complete (26/62 steps)
**Started:** 2026-01-05

## Current Phase: Backend Development
[==========----------] 50% (4/7 steps)

Completed:
- [x] 4.1 Initialize server and database connection
- [x] 4.2 Implement authentication and authorization
- [x] 4.3 Develop core API endpoints
- [x] 4.4 Integrate third-party services

In Progress:
- [ ] 4.5 Implement background jobs <- Current

Remaining:
- [ ] 4.6 Build real-time features
- [ ] 4.7 Write API documentation

## Next Quality Gate
**Gate:** implementation-complete
**Trigger:** Before Phase 6 (Testing)
**Status:** 2/3 checks passing
- [x] All features implemented
- [x] Unit tests passing
- [ ] No critical bugs (pending QA review)

## Deliverables This Phase
- [x] Project scaffold
- [x] Database connection
- [x] Authentication system
- [x] Core API endpoints
- [ ] Background job system
- [ ] Real-time communication
- [ ] API documentation

## Recommended Next Action
Run `/APDF_step 4.5` to implement background jobs and async processing.

## Pending Decisions
None awaiting approval.
```

## Output Format (Brief)

```
TaskFlow | Phase 4/9 | 42% complete
Current: 4.5 Implement background jobs
Next: /APDF_step 4.5 or /APDF_next
```

## Output Format (Existing Project)

```
# Project Status: E-commerce Platform

## Overview
**Mode:** Existing Codebase
**Onboarded:** 2026-01-05
**Last Audit:** 2026-01-08

## Codebase Profile
**Stack:** TypeScript, React, Node.js, PostgreSQL
**Tests:** 70% coverage (Jest, Playwright)
**CI/CD:** GitHub Actions
**Hosting:** AWS

## Audit Scores
| Category | Score | Trend |
|----------|-------|-------|
| Security | 72/100 | +12 |
| Quality | 68/100 | +8 |
| Architecture | 85/100 | -- |
| Documentation | 45/100 | +5 |
| DevOps | 78/100 | -- |
| **Overall** | **70/100** | **+6** |

## Findings Summary
| Severity | Open | Resolved |
|----------|------|----------|
| High | 2 | 3 |
| Medium | 8 | 12 |
| Low | 15 | 20 |

## Tech Debt
**Total Items:** 24
- Critical: 1
- High: 5
- Medium: 12
- Low: 6

## Phase Status
| Phase | Status |
|-------|--------|
| 1. Discovery | existing |
| 2. Design | partial |
| 3. Architecture | existing |
| 4. Backend | existing |
| 5. Frontend | existing |
| 6. Testing | partial |
| 7. Deployment | existing |
| 8. Documentation | needs-update |
| 9. Operations | partial |

## Current Improvement Cycle
**Target:** Security (Quick Wins)
**Progress:** 3/5 items completed

## Recommended Actions
1. Run `/APDF_improve security` to finish current cycle
2. Run `/APDF_audit documentation` for detailed doc review
3. Address DEBT-001: Critical legacy auth code

## High Priority Findings
- SEC-001: Session tokens never expire
- SEC-003: Rate limiting missing on login
```

## Output Format (Existing - Brief)

```
E-commerce | Existing | Score: 70/100
Open: 25 findings (2 high)
Tech Debt: 24 items (1 critical)
Run /APDF_improve security or /APDF_audit
```
