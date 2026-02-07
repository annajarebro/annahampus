---
description: Research and document how the codebase works
---

# Research Codebase Command

You are conducting research to document and understand the codebase. Your goal is to create comprehensive documentation about HOW things work, WHERE they are located, and WHAT patterns exist.

## CRITICAL: You Are a Documentarian, NOT an Evaluator

- **DO**: Document and explain the codebase as it exists today
- **DO**: Describe where components are, how they work, how they interact
- **DO**: Create a technical map of the existing system
- **DON'T**: Suggest improvements or changes (unless explicitly asked)
- **DON'T**: Perform root cause analysis (unless explicitly asked)
- **DON'T**: Propose future enhancements (unless explicitly asked)

## Initial Response

Acknowledge the research request and outline what you'll investigate:
- What specific areas or questions you'll explore
- Which agents you'll spawn to help with research
- Where you'll document findings

## Step-by-Step Process

### Step 1: Understand the Research Question
1. Read any mentioned files COMPLETELY (no limit/offset parameters)
2. Clarify the scope: What exactly needs to be documented?
3. Identify key areas to investigate

### Step 2: Spawn Parallel Research Tasks
Create multiple specialized research sub-tasks using the Task tool with these agents:
- **codebase-locator**: Find WHERE relevant files and components are
- **codebase-analyzer**: Investigate HOW specific parts work
- **codebase-pattern-finder**: Discover existing patterns and conventions
- **thoughts-locator**: Find any existing research documents
- **thoughts-analyzer**: Extract insights from previous research
- **web-search-researcher**: Gather external context if needed

**IMPORTANT**: Spawn all research tasks IN PARALLEL using multiple Task tool calls in a single message. Wait for ALL tasks to complete before proceeding.

### Step 3: Gather Context
1. Read ALL files identified by the research agents COMPLETELY
2. Do NOT use limit/offset parameters
3. Build full context before analyzing

### Step 4: Create Research Document
Write findings to: `thoughts/shared/research/YYYY-MM-DD-topic-name.md`

Use the metadata script to generate YAML frontmatter:
```bash
./scripts/spec_metadata.sh
```

Then structure the document:

```markdown
---
date: [ISO format with timezone]
researcher: [Your name]
git_commit: [Current commit]
branch: [Current branch]
repository: [Repo name]
topic: [Research question]
tags: [relevant, tags]
status: complete
last_updated: YYYY-MM-DD
last_updated_by: [Name]
---

# Research: [Topic]

## Research Question
[Clear statement of what was investigated]

## Summary
[2-3 paragraphs summarizing key findings]

## Detailed Findings

### Finding 1: [Title]
[Detailed explanation with file:line references]

### Finding 2: [Title]
[Detailed explanation with file:line references]

## Code References
[Key files and their roles]
- `path/to/file.ext:line` - [What's here and why it matters]

## Architecture Documentation
[How components fit together, with diagrams if helpful]

## Historical Context
[Insights from previous research documents if applicable]

## Related Research
[Links to other relevant thoughts documents]

## Open Questions
[Questions that remain unanswered]
```

## Important Guidelines

1. **Be Thorough**: Read files completely, don't skip sections
2. **Be Precise**: Every claim needs a file:line reference
3. **Be Neutral**: Document what exists, not what should exist
4. **Be Complete**: Cover the full scope of the research question
5. **Be Organized**: Structure findings logically with clear headings

## What Good Research Looks Like

Good research documentation:
- Answers the research question completely
- Provides specific file:line references for all claims
- Explains both WHAT exists and HOW it works
- Identifies patterns and conventions
- Connects related components
- Is readable by someone unfamiliar with the codebase

## Common Research Topics

- "How does [feature] work?"
- "Where is [functionality] implemented?"
- "What patterns exist for [task]?"
- "How do [component A] and [component B] interact?"
- "What's the architecture of [system]?"

## Success Criteria

- [ ] Research question clearly stated
- [ ] All relevant code located and read
- [ ] Comprehensive findings documented with file:line references
- [ ] Document saved to thoughts/shared/research/
- [ ] Open questions identified if any remain
- [ ] User understands how the codebase works

Remember: You're creating a knowledge base, not judging the code. Future you (or future team members) should be able to understand the codebase from your documentation.
