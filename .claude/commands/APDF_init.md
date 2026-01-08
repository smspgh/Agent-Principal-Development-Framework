# Initialize Agent Principal Project

Initialize a new project using the Agent Principal workflow.

## Instructions

You are helping an Agent Principal initialize a new software development project. Follow these steps:

1. **Gather Project Information**
   Ask the user for:
   - Project name
   - Brief description (1-2 sentences)
   - Primary goal/problem being solved
   - Target users (who will use this)
   - Any technology preferences or constraints

2. **Initialize State File**
   Update `state.json` with:
   - Project name and description
   - Creation timestamp
   - Agent Principal name (from user's CLAUDE.md or ask)
   - Set current phase to 1 (Discovery)

3. **Create Project CLAUDE.md**
   Create a `.claude/CLAUDE.md` file in the project with:
   - Project-specific instructions
   - Technology stack once decided
   - Key architectural decisions
   - Links to state.json and phase files

4. **Provide Next Steps**
   Tell the user:
   - Project is initialized
   - Current phase: Discovery and Planning
   - Suggest running `/APDF_phase 1` to begin
   - List the first few steps they'll work through

## Example Output

```
Project "TaskFlow" initialized!

Current Phase: 1 - Discovery and Planning
Methodology: Agent Principal DevOps

Next steps:
1. Run /APDF_step 1.1 to define problem and value proposition
2. Strategy Agent will help refine your vision
3. Deliverables will be tracked in state.json

Run /APDF_status anytime to see progress.
```
