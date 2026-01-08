# Step Command

Execute a specific step in the development workflow.

## Usage
`/step <stepId>` - Execute step (e.g., /step 1.3, /step 4.2)

## Instructions

When the user runs this command:

1. **Parse Step ID**
   - Format: `<phase>.<step>` (e.g., "1.3", "4.2")
   - Validate step exists in phase file

2. **Load Step Data**
   - Read from appropriate phase JSON file
   - Get step details: name, description, tasks, deliverables
   - Identify assigned agent(s) from role mapping

3. **Check Dependencies**
   - Review if prerequisite steps are complete
   - Warn if dependencies not met (but allow override)

4. **Invoke Appropriate Agent**
   Based on the step's `agentId`:
   - Load agent definition from `agents/<agent>.json`
   - Apply agent's system prompt
   - Provide step context and requirements

5. **Execute Step Tasks**
   For each task in the step:
   - Present task to appropriate agent
   - Generate deliverable if applicable
   - Track completion in state.json

6. **Handle Approval (if required)**
   If agent's `approvalRequired` is true:
   - Present output for Agent Principal review
   - Wait for `/approve` or revision request

7. **Update State**
   - Mark step as complete in state.json
   - Record deliverables produced
   - Update metrics

## Agent Mapping (by phase)

Phase 1 (Discovery): STRATEGY, SECURITY
Phase 2 (Design): DESIGN, STRATEGY
Phase 3 (Architecture): ARCHITECTURE, DEVOPS, SECURITY
Phase 4 (Backend): BACKEND
Phase 5 (Frontend): FRONTEND
Phase 6 (Testing): QUALITY, SECURITY
Phase 7 (Deployment): DEVOPS
Phase 8 (Documentation): BACKEND, FRONTEND (auto-generate)
Phase 9 (Operations): DEVOPS, QUALITY, SECURITY

## Output Format

```
## Step 4.2: Implement authentication and authorization

**Agent:** BACKEND
**Automation Level:** Full (no approval needed)

### Tasks
1. [ ] Implement user registration with validation
2. [ ] Build login with secure password handling
3. [ ] Set up JWT authentication
4. [ ] Implement refresh token rotation
5. [ ] Build role-based access control (RBAC)
6. [ ] Add OAuth2/OIDC for social login (if required)
7. [ ] Implement MFA/2FA support
8. [ ] Set up account recovery flows

### Deliverables
- Registration endpoint
- Login endpoint
- Auth mechanism
- Token refresh
- RBAC implementation

Starting implementation...
```
