# Next Command

Automatically advance to and execute the next pending step.

## Usage
`/next` - Execute the next pending step
`/next --preview` - Show what the next step would be without executing

## Instructions

When the user runs this command:

1. **Load Current State**
   Read `state.json` to find:
   - Current phase
   - Completed steps
   - Next pending step

2. **Determine Next Step**
   Logic:
   - Find first incomplete step in current phase
   - If current phase complete, check quality gate
   - If gate passes, move to next phase's first step
   - Skip steps marked as excluded in methodology

3. **Check Dependencies**
   - Verify all prerequisite steps complete
   - Check quality gate if transitioning phases

4. **Execute or Preview**
   If `--preview`:
   - Show what would happen
   - Don't update state

   Otherwise:
   - Invoke `/step <nextStepId>` logic
   - Execute the step with appropriate agent

5. **Handle Phase Transitions**
   If moving to new phase:
   - Run quality gate check
   - Show phase transition message
   - Update currentPhase in state.json

## Output Format

```
## Advancing to Next Step

Previous: 3.4 Set up version control (completed)
Next: 3.5 Define Infrastructure as Code

---

[Executes step 3.5 with DevOps Agent]
```

## Phase Transition Output

```
## Phase 3 Complete!

Quality Gate: architecture-ready
- [x] Database schema defined
- [x] API contracts documented
- [x] Security reviewed

Transitioning to Phase 4: Backend Development

---

## Step 4.1: Initialize server and database connection

[Continues with step execution]
```
