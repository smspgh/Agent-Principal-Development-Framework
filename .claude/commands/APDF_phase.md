# Phase Command

Start, resume, or view details of a development phase.

## Usage
`/phase <number>` - Start or view phase by number (1-9)
`/phase` - Show current phase status

## Instructions

When the user runs this command:

1. **Parse the Phase Number**
   - If no number provided, show current phase from `state.json`
   - Valid phases: 1-9

2. **Load Phase Data**
   Read the corresponding phase file from `phases/`:
   - 1: `1-discovery.json`
   - 2: `2-design.json`
   - 3: `3-architecture.json`
   - 4: `4-backend.json`
   - 5: `5-frontend.json`
   - 6: `6-testing.json`
   - 7: `7-deployment.json`
   - 8: `8-documentation.json`
   - 9: `9-operations.json`

3. **Check Quality Gate** (if starting new phase)
   - Read methodology file for required quality gate
   - Verify previous phase completion if applicable
   - Warn if prerequisites not met

4. **Display Phase Overview**
   Show:
   - Phase name and description
   - Objectives
   - Steps with status (from state.json)
   - Primary agents involved
   - Estimated scope

5. **Update State**
   - Set `currentPhase` in state.json
   - Record phase start time if first time
   - Mark phase status as "in_progress"

## Output Format

```
## Phase 3: Architecture and Infrastructure

**Status:** In Progress (2/7 steps complete)
**Primary Agents:** ARCHITECTURE, DEVOPS, SECURITY

### Objectives
- Design database schema and data relationships
- Define API contracts and architecture
- Establish version control and branching strategy
- Set up Infrastructure as Code
- Configure development environments

### Steps
[x] 3.1 Design database schema and data model
[x] 3.2 Design API architecture
[ ] 3.3 Define data validation and business rules <- Current
[ ] 3.4 Set up version control and branching strategy
[ ] 3.5 Define Infrastructure as Code (IaC)
[ ] 3.6 Design containerization and orchestration
[ ] 3.7 Set up development environments

Run /step 3.3 to continue, or /next for the next pending step.
```
