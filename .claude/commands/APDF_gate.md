# Gate Command

Run quality gate checks before phase transitions.

## Usage
`/gate` - Check the next applicable quality gate
`/gate <gateName>` - Check specific quality gate
`/gate --all` - Show all gates and their status

## Available Quality Gates

| Gate Name | Trigger Point | Phase Transition |
|-----------|---------------|------------------|
| requirements-complete | Before Design | 1 -> 2 |
| design-approved | Before Architecture | 2 -> 3 |
| architecture-ready | Before Backend | 3 -> 4 |
| implementation-complete | Before Testing | 5 -> 6 |
| release-ready | Before Deployment | 6 -> 7 |
| launch-approved | Before Production | 7 -> Production |

## Instructions

When the user runs this command:

1. **Determine Applicable Gate**
   - Based on current phase in state.json
   - Or use specified gate name

2. **Load Gate Definition**
   From methodology file, get gate checks:
   ```json
   {
     "gate": "requirements-complete",
     "checks": [
       "User stories defined",
       "MVP scope documented",
       "Success metrics set"
     ]
   }
   ```

3. **Evaluate Each Check**
   For each check:
   - Query state.json for relevant deliverable
   - Verify completeness
   - Check for approval if required

4. **Generate Report**
   - Show pass/fail for each check
   - Calculate overall gate status
   - Provide remediation for failures

5. **Gate Actions**
   If all checks pass:
   - Mark gate as passed in state.json
   - Allow phase transition

   If checks fail:
   - Block phase transition
   - Suggest steps to resolve

## Gate Check Logic

**requirements-complete:**
- User stories defined -> Check deliverable "user-stories" exists and approved
- MVP scope documented -> Check deliverable "mvp-scope" exists and approved
- Success metrics set -> Check step 1.1 complete with metrics defined

**design-approved:**
- Wireframes complete -> Check deliverable "wireframes" exists
- Design system defined -> Check deliverable "design-system" exists and approved
- Agent Principal approved -> Check approval record in decisions array

**architecture-ready:**
- Database schema defined -> Check deliverable "database-schema" exists
- API contracts documented -> Check deliverable "api-specification" exists
- Security reviewed -> Check step 1.9 complete and approved

**implementation-complete:**
- All features implemented -> All steps in phases 4-5 complete
- Unit tests passing -> Check test results recorded
- No critical bugs -> Check blockers array for severity

**release-ready:**
- All tests passing -> Check phase 6 completion
- Security scan clean -> Check security deliverables
- Performance acceptable -> Check performance test results

**launch-approved:**
- Staging validated -> Check step 7.4 complete
- Monitoring configured -> Check step 7.7 complete
- Rollback ready -> Check rollback configuration exists

## Output Format

```
## Quality Gate: architecture-ready

**Status:** PASSING (3/3 checks)

### Checks
- [x] Database schema defined
      Deliverable: database-schema (completed 2026-01-08)

- [x] API contracts documented
      Deliverable: api-specification (completed 2026-01-08)
      OpenAPI 3.0 spec with 24 endpoints defined

- [x] Security reviewed
      Step 1.9 complete, threat model approved
      8 threats identified, all mitigations planned

### Gate Status
All checks passing. Ready to proceed to Phase 4: Backend Development.

Run /phase 4 or /next to continue.
```

## Output Format (Failing)

```
## Quality Gate: release-ready

**Status:** FAILING (2/3 checks)

### Checks
- [x] All tests passing
      Unit: 342 passing, Integration: 89 passing, E2E: 23 passing

- [ ] Security scan clean
      FAILING: 2 high-severity issues found
      - SQL injection in /api/search (step 6.4)
      - XSS vulnerability in comment form (step 6.4)

- [x] Performance acceptable
      p95 latency: 180ms (target: <200ms)
      Load test: 1000 concurrent users handled

### Required Actions
1. Run /agent security to review and fix security issues
2. Re-run /step 6.4 to complete security testing
3. Run /gate release-ready to re-check

Cannot proceed to Phase 7 until gate passes.
```
