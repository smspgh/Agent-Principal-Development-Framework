# Onboard Existing Codebase

Onboard an existing application to the Agent Principal workflow.

## Instructions

You are helping an Agent Principal onboard an **existing** codebase (not a new project). This differs from `/APDF_init` which is for greenfield projects.

### 1. Gather Context

Ask the user for:
- Project name
- Repository location (if not current directory)
- Brief description of what the application does
- Current state: production, staging, development, abandoned?
- Primary goal for onboarding: maintenance, enhancement, refactoring, tech debt reduction?
- Any known issues or pain points

### 2. Run Codebase Discovery

Use the Explore agent to analyze:
```
- Project structure (directories, key files)
- Technology stack (languages, frameworks, libraries)
- Build system (package managers, build tools)
- Test coverage (test files, testing frameworks)
- Documentation (README, docs folder, inline docs)
- Configuration (env files, config files)
- Infrastructure (Docker, CI/CD, deployment)
```

### 3. Generate Codebase Audit

Create an initial audit by scanning for:

| Category | What to Find |
|----------|--------------|
| **Architecture** | Entry points, core modules, data flow |
| **Dependencies** | Package versions, outdated deps, security vulnerabilities |
| **Quality** | Test coverage, linting config, type coverage |
| **Security** | Auth mechanisms, secrets handling, input validation |
| **Documentation** | README completeness, API docs, code comments |
| **DevOps** | CI/CD pipelines, deployment scripts, monitoring |

### 4. Initialize State File

Update `state.json` with:
```json
{
  "projectMode": "existing",
  "onboardedAt": "<timestamp>",
  "codebaseProfile": {
    "languages": [],
    "frameworks": [],
    "buildTools": [],
    "testingFrameworks": [],
    "cicd": null,
    "hosting": null
  },
  "auditResults": {
    "completedAt": null,
    "findings": [],
    "techDebt": [],
    "securityIssues": [],
    "qualityScore": null
  },
  "existingAssets": {
    "hasTests": false,
    "hasDocs": false,
    "hasCI": false,
    "hasDocker": false
  }
}
```

### 5. Map Existing State to Phases

For each phase (1-9), assess current state:

| Status | Meaning |
|--------|---------|
| `existing` | Phase deliverables exist and are current |
| `partial` | Some deliverables exist, others missing |
| `legacy` | Exists but needs modernization |
| `missing` | Phase not addressed in codebase |
| `needs-update` | Exists but out of date |

### 6. Generate Improvement Roadmap

Based on audit, recommend:
1. **Critical fixes** (security, broken functionality)
2. **Quick wins** (easy improvements with high impact)
3. **Tech debt reduction** (refactoring priorities)
4. **Feature readiness** (what's needed for new features)

### 7. Provide Next Steps

Tell the user:
```
Codebase onboarded: {projectName}

Profile:
- Stack: {languages/frameworks}
- Tests: {coverage status}
- Docs: {documentation status}
- CI/CD: {pipeline status}

Audit Summary:
- Tech Debt Items: {count}
- Security Findings: {count}
- Quality Score: {score}/100

Recommended Actions:
1. Run /APDF_audit for detailed findings
2. Run /APDF_improve to start improvement cycle
3. Run /APDF_phase {n} to focus on a specific area

Run /APDF_status to see full breakdown.
```

## Example Session

```
> /APDF_onboard

Onboarding existing codebase...

Project: E-commerce Platform
Mode: Existing Application
Goal: Maintenance and Enhancement

Scanning codebase...

Stack Detected:
- TypeScript, React, Node.js
- PostgreSQL, Redis
- Jest, Playwright
- GitHub Actions, Docker

Phase Assessment:
1. Discovery: existing (requirements in README)
2. Design: partial (no design system)
3. Architecture: existing (well-structured)
4. Backend: existing (API complete)
5. Frontend: existing (React app)
6. Testing: partial (70% coverage)
7. Deployment: existing (CI/CD active)
8. Documentation: needs-update (outdated)
9. Operations: partial (monitoring gaps)

Tech Debt Identified: 12 items
Security Findings: 2 items (medium)
Quality Score: 72/100

Ready for improvement cycle!
Run /APDF_audit security for detailed security review.
Run /APDF_improve quality to boost test coverage.
```
