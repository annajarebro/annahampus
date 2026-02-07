---
description: Create a detailed implementation plan interactively
---

# Create Plan Command

You are creating a detailed implementation plan for a feature or change. This is an INTERACTIVE process - you'll gather information, present options, get feedback, and iterate before finalizing the plan.

## Initial Response

Acknowledge the planning request and outline your approach:
- What you understand needs to be built
- What research you'll conduct first
- How you'll structure the planning process

## Step-by-Step Process

### Step 1: Gather Context
1. Read any mentioned files, tickets, or requirements COMPLETELY (no limit/offset)
2. Read existing research documents from thoughts/ if they exist
3. Understand the current state of the codebase

### Step 2: Conduct Research
Spawn parallel research tasks using the Task tool:
- **codebase-locator**: Find related code and similar features
- **codebase-analyzer**: Understand current implementation patterns
- **codebase-pattern-finder**: Find examples of similar work
- **thoughts-locator**: Check for previous plans or research
- **thoughts-analyzer**: Extract insights from existing documentation
- **web-search-researcher**: Research external best practices if needed

**IMPORTANT**: Spawn ALL research tasks in PARALLEL. Wait for all to complete before proceeding.

### Step 3: Analyze Findings and Present Options
1. **Present what you learned** from research
2. **Identify key decisions** that need to be made
3. **Present design options** with pros/cons
4. **Ask questions** about unclear requirements
5. **Get user feedback** before writing the plan

**DON'T skip this step!** The plan will be better with user input.

### Step 4: Get Phasing Agreement
Before writing the full plan:
1. Propose how to break the work into phases
2. Explain the rationale for each phase
3. Get user agreement on the phasing approach
4. Adjust based on feedback

### Step 5: Write the Plan
Save to: `thoughts/shared/plans/YYYY-MM-DD-brief-description.md`

Generate metadata using:
```bash
./scripts/spec_metadata.sh
```

Structure the plan:

```markdown
---
date: [ISO with timezone]
researcher: [Your name]
git_commit: [Hash]
branch: [Branch]
repository: [Repo]
topic: [Feature name]
tags: [relevant, tags]
status: in-progress
last_updated: YYYY-MM-DD
last_updated_by: [Name]
type: implementation_plan
---

# [Feature Name] Implementation Plan

## Overview
[2-3 paragraphs explaining what we're building and why]

## Current State Analysis
[What exists today with file:line references]

### Key Discoveries
- **Discovery 1** (file.ext:line): [What you found and why it matters]
- **Discovery 2** (file.ext:line): [What you found and why it matters]

## Desired End State
[What the system will look like when done]

## What We're NOT Doing
[Explicitly call out what's out of scope]

## Implementation Approach
[High-level strategy and rationale]

---

## Phase 1: [Phase Name]

### Overview
[What this phase accomplishes]

### Changes Required

#### Change 1: [Description]
**File**: `path/to/file.ext`

**Current**:
```language
[Relevant current code if modifying existing]
```

**New**:
```language
[Pseudocode or description of new code]
```

**Rationale**: [Why this change is needed]

#### Change 2: [Description]
[Same structure]

### Success Criteria

#### Automated Verification
- [ ] All existing tests pass
- [ ] New unit tests pass
- [ ] Integration tests pass
- [ ] Linter passes
- [ ] Build succeeds

**Command to verify**: `[exact command to run]`

#### Manual Verification
- [ ] [Specific thing to test manually]
- [ ] [Another specific thing to test]
- [ ] [Edge case to verify]

**How to test**: [Step-by-step instructions]

---

## Phase 2: [Phase Name]
[Same structure as Phase 1]

---

## Testing Strategy
[Overall approach to testing this feature]

## Performance Considerations
[Any performance implications or optimizations needed]

## Migration Notes
[If applicable: how to migrate existing data/users]

## References
- Research: thoughts/shared/research/YYYY-MM-DD-topic.md
- Related Plans: thoughts/shared/plans/YYYY-MM-DD-other-feature.md
- External Docs: [URLs]
```

## Important Guidelines

1. **Be Interactive**: Get feedback at major decision points, don't write the full plan in one shot
2. **Be Skeptical**: Question vague requirements, identify potential issues early
3. **Be Thorough**: Include specific file paths, code references, and clear success criteria
4. **Be Practical**: Break work into testable, incremental phases
5. **Be Clear**: Write so anyone can implement the plan, not just you

## Success Criteria Split

ALWAYS split success criteria into two categories:
- **Automated Verification**: Things that can be checked by running commands
- **Manual Verification**: Things that require human testing

This ensures both code quality AND user experience are validated.

## Phases Should Be:
- **Incremental**: Each phase adds value
- **Testable**: Clear success criteria for each phase
- **Independent**: Later phases build on earlier ones but each stands alone
- **Manageable**: Not too large to complete in one session

## What Makes a Good Plan

A good implementation plan:
- Can be followed by someone who wasn't involved in planning
- Has no open questions or ambiguities
- Includes specific file paths and code locations
- Has measurable success criteria
- Balances thoroughness with practicality
- Anticipates edge cases and challenges

## Common Planning Scenarios

- **New Feature**: Research patterns, plan implementation, define testing
- **Refactoring**: Document current state, plan incremental changes, ensure no regression
- **Bug Fix**: Understand root cause, plan fix, add tests to prevent recurrence
- **Integration**: Research external system, plan connection points, handle errors

## Success Criteria

- [ ] Research completed and findings incorporated
- [ ] User feedback gathered on approach
- [ ] Phasing agreed upon
- [ ] Plan document written with all sections complete
- [ ] All phases have clear success criteria (automated + manual)
- [ ] No open questions remain
- [ ] User approves plan

Remember: The plan is the foundation for implementation. Take time to get it right!
