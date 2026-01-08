# Audit Codebase

Run a focused audit on the codebase. Use after `/APDF_onboard` or anytime for existing projects.

## Usage

```
/APDF_audit [category]
```

Categories:
- `all` - Full audit across all categories (default)
- `security` - Security vulnerabilities and risks
- `quality` - Code quality and test coverage
- `architecture` - Structure and design patterns
- `dependencies` - Package health and updates
- `performance` - Performance issues and bottlenecks
- `documentation` - Documentation completeness
- `devops` - CI/CD and infrastructure
- `techdebt` - Technical debt inventory

## Instructions

### Security Audit

Invoke **SECURITY** agent to scan for:
- [ ] Authentication/authorization weaknesses
- [ ] Input validation gaps
- [ ] SQL injection vulnerabilities
- [ ] XSS vulnerabilities
- [ ] Secrets in code or config
- [ ] Outdated dependencies with CVEs
- [ ] CORS misconfigurations
- [ ] Missing security headers
- [ ] Insecure data storage
- [ ] Logging sensitive data

### Quality Audit

Invoke **QUALITY** agent to assess:
- [ ] Test coverage percentage
- [ ] Test quality (assertions, edge cases)
- [ ] Linting violations
- [ ] Type coverage (TypeScript/Flow)
- [ ] Code duplication
- [ ] Cyclomatic complexity
- [ ] Dead code
- [ ] Console.log/debug statements
- [ ] Error handling patterns
- [ ] Code comment quality

### Architecture Audit

Invoke **ARCHITECTURE** agent to evaluate:
- [ ] Module boundaries and coupling
- [ ] Dependency injection patterns
- [ ] API design consistency
- [ ] Database schema design
- [ ] State management approach
- [ ] Error handling strategy
- [ ] Logging and observability
- [ ] Configuration management
- [ ] Feature flag usage
- [ ] Scalability concerns

### Dependencies Audit

Invoke **DEVOPS** agent to check:
- [ ] Outdated packages (major, minor, patch)
- [ ] Deprecated packages
- [ ] Security vulnerabilities (npm audit)
- [ ] License compliance
- [ ] Unused dependencies
- [ ] Missing peer dependencies
- [ ] Lock file consistency
- [ ] Bundle size impact

### Performance Audit

Invoke **QUALITY** agent to analyze:
- [ ] N+1 query patterns
- [ ] Missing database indexes
- [ ] Memory leaks
- [ ] Unnecessary re-renders (React)
- [ ] Bundle size
- [ ] Lazy loading opportunities
- [ ] Caching usage
- [ ] API response times
- [ ] Asset optimization

### Documentation Audit

Invoke **ARCHITECTURE** agent to review:
- [ ] README completeness
- [ ] API documentation
- [ ] Inline code comments
- [ ] Architecture decision records
- [ ] Setup/installation guide
- [ ] Contributing guide
- [ ] Changelog maintenance
- [ ] Environment documentation

### DevOps Audit

Invoke **DEVOPS** agent to verify:
- [ ] CI/CD pipeline health
- [ ] Build time optimization
- [ ] Test automation in pipeline
- [ ] Deployment strategy
- [ ] Environment parity
- [ ] Secret management
- [ ] Monitoring coverage
- [ ] Alerting configuration
- [ ] Backup procedures
- [ ] Rollback capability

### Tech Debt Audit

Invoke **ARCHITECTURE** agent to inventory:
- [ ] TODO/FIXME/HACK comments
- [ ] Temporary workarounds
- [ ] Deprecated patterns in use
- [ ] Missing abstractions
- [ ] Over-engineering
- [ ] Copy-paste code
- [ ] Outdated patterns
- [ ] Migration remnants
- [ ] Incomplete features
- [ ] Known limitations

## Output Format

Update `state.json` with findings:

```json
{
  "auditResults": {
    "lastAuditAt": "<timestamp>",
    "category": "<category>",
    "findings": [
      {
        "id": "SEC-001",
        "category": "security",
        "severity": "high|medium|low|info",
        "title": "SQL Injection in User Query",
        "location": "src/api/users.ts:45",
        "description": "User input directly concatenated into SQL query",
        "recommendation": "Use parameterized queries",
        "effort": "small|medium|large",
        "status": "open|in-progress|resolved|wont-fix"
      }
    ],
    "summary": {
      "total": 0,
      "bySeverity": { "high": 0, "medium": 0, "low": 0, "info": 0 },
      "byCategory": {},
      "byStatus": {}
    },
    "scores": {
      "security": 0,
      "quality": 0,
      "architecture": 0,
      "documentation": 0,
      "devops": 0,
      "overall": 0
    }
  }
}
```

## Example Output

```
Audit Complete: Security

Findings: 5 issues

HIGH (1):
- SEC-001: SQL Injection in user search
  Location: src/api/users.ts:45
  Effort: Small

MEDIUM (2):
- SEC-002: Missing rate limiting on auth endpoints
- SEC-003: Session tokens don't expire

LOW (2):
- SEC-004: Security headers could be strengthened
- SEC-005: Debug mode enabled in production config

Security Score: 65/100

Recommendations:
1. Fix SEC-001 immediately (critical vulnerability)
2. Run /APDF_improve security to address all findings
3. Schedule regular security audits

Run /APDF_audit all for complete codebase audit.
```

## Severity Definitions

| Severity | Description | Action |
|----------|-------------|--------|
| **High** | Critical issue, security risk, or major bug | Fix immediately |
| **Medium** | Significant issue affecting quality or maintainability | Fix soon |
| **Low** | Minor issue or improvement opportunity | Fix when convenient |
| **Info** | Observation or suggestion | Consider for future |

## Effort Estimates

| Effort | Description |
|--------|-------------|
| **Small** | < 1 hour, single file change |
| **Medium** | 1-4 hours, multiple files |
| **Large** | > 4 hours, significant refactoring |
