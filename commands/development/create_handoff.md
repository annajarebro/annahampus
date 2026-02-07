# Create Handoff

You help create handoff documents when pausing work or transferring context to another session.

## Purpose

Handoffs capture the current state of work so you (or someone else) can pick it up later without losing context.

## When to Use

- Pausing work on a task for an extended time
- Need to switch context but want to preserve learnings
- Completing research that someone else will implement
- End of day/session with work in progress

## Initial Response

**If no context**: Ask what work to hand off
```
I'll help create a handoff document. What work are you handing off?
- In-progress implementation?
- Completed research?
- Debugging session?
- Planning work?
```

**If context provided**: Proceed to create handoff

## Handoff Creation Process

### Step 1: Gather Information

Ask clarifying questions:
- What's the current status? (in-progress, blocked, needs-review)
- What plan/research are you working from?
- What's been completed so far?
- What are the next steps?
- Any important learnings or gotchas discovered?

### Step 2: Collect Context

**Git State:**
```bash
git status
git log -5 --oneline
git diff --name-only
```

**Recent Changes:**
```bash
git diff HEAD~1 --name-only
# or for uncommitted:
git diff --name-only
```

### Step 3: Identify Artifacts

List what's been created/modified:
- Code files changed
- Tests added/modified
- Documentation updated
- Plans/research created

### Step 4: Document Learnings

Capture important insights:
- Patterns discovered in the codebase
- Approaches that didn't work and why
- Important constraints or gotchas
- Dependencies or integration points

### Step 5: Write Handoff Document

**Ensure directory exists:**
```bash
mkdir -p thoughts/handoffs
```

**Filename format:** `thoughts/handoffs/YYYY-MM-DD-HH-MM-description.md`

**Template:**

```markdown
---
title: [Task/Feature Description]
date: YYYY-MM-DD HH:MM
status: in-progress | blocked | needs-review | complete
related_plan: thoughts/plans/YYYY-MM-DD-plan.md (if applicable)
---

# Handoff: [Task Description]

## Current Status

**Overall**: [in-progress | blocked | needs-review | complete]

**What's Done**:
- ✅ Item 1
- ✅ Item 2

**What's Remaining**:
- [ ] Item 1
- [ ] Item 2

**Blockers** (if any):
- Description of what's blocking progress

## Context

### What This Is About
Brief description of the task/feature being worked on.

### Related Documents
- Plan: `thoughts/plans/YYYY-MM-DD-description.md`
- Research: `thoughts/research/YYYY-MM-DD-topic.md`
- Original issue/ticket reference (if applicable)

## Recent Changes

### Files Modified
- `src/auth/middleware.ts:42-60` - Added JWT validation
  - Status: Complete, tests passing
- `src/routes/api.ts:100-120` - Updated auth routes
  - Status: In progress, needs error handling

### Commits
- `abc123`: "Add JWT validation logic"
- `def456`: "Update auth routes"

### Uncommitted Changes
- Modified: `src/auth/middleware.ts`
- Modified: `src/routes/api.ts`
- Added: `tests/auth.test.ts`

## Key Learnings

### Patterns Discovered
- Auth middleware uses pattern X (found in `src/middleware/`)
- Error handling follows convention Y (see `src/errors/`)

### What Worked
- Approach A worked well for [reason]
- Library X was better than Y because [reason]

### What Didn't Work
- Tried approach B but had issues: [description]
- Library Z doesn't support [feature we need]

### Important Gotchas
- ⚠️ Must call middleware before routes or it fails silently
- ⚠️ Config requires environment variable AUTH_SECRET
- ⚠️ Tests need specific setup (see test file comments)

## Implementation Details

### Current Approach
Brief description of the technical approach being taken.

### Key Code Locations
- Entry point: `src/server.ts:50`
- Main logic: `src/auth/middleware.ts:42-80`
- Tests: `tests/auth.test.ts:10-50`
- Config: `config/auth.json`

### Dependencies
- Added: `jsonwebtoken@9.0.0`
- Uses existing: `express`, `bcrypt`

## Testing Status

### Tests Passing
- ✅ Unit tests for JWT validation (15 tests)
- ✅ Auth middleware tests (8 tests)

### Tests Failing
- ❌ Integration test for login flow
  - Error: "Cannot read property 'user' of undefined"
  - Location: `tests/integration/auth.test.ts:45`

### Tests Missing
- [ ] Error handling edge cases
- [ ] Token expiration scenarios
- [ ] Refresh token flow

## Next Steps

### Immediate Actions
1. [ ] Fix failing integration test
   - Issue: req.user vs req.session.user mismatch
   - Fix: Update route handlers or middleware
2. [ ] Add error handling to auth routes
   - Location: `src/routes/api.ts:100-120`
   - Pattern: Use existing error middleware

### Follow-up Tasks
1. [ ] Add rate limiting to auth endpoints
2. [ ] Implement token refresh flow
3. [ ] Add logging for auth failures
4. [ ] Update documentation

## Questions/Decisions Needed

- Should we use req.user or req.session.user? (needs decision)
- Token expiration: 15min or 1hour? (needs product input)
- Refresh token storage: Redis or database? (needs architecture review)

## Other Notes

- Working branch: `feature/auth-jwt`
- PR draft created: #123 (not ready for review)
- Discussed with [person] on [date] about approach
- See also: `thoughts/research/YYYY-MM-DD-jwt-comparison.md`

## How to Resume

1. Read this handoff completely
2. Check git status and verify no conflicts
3. Run tests: `npm test`
4. Review failing integration test at `tests/integration/auth.test.ts:45`
5. Start with fixing req.user vs req.session.user issue
6. See "Next Steps" section for prioritized actions
```

### Step 6: Present Handoff

Show the handoff location and summary:

> **Handoff Created** 📋
>
> **Location**: `thoughts/handoffs/YYYY-MM-DD-HH-MM-description.md`
>
> **Status**: [status]
>
> **Summary**:
> - X items completed
> - Y items remaining
> - Z key learnings documented
>
> **Next session should**:
> 1. [First action]
> 2. [Second action]
>
> The handoff is ready. You can resume this work later with:
> `/resume_handoff thoughts/handoffs/YYYY-MM-DD-HH-MM-description.md`

## What to Include

### Essential Information
- ✅ Current status (what's done, what's not)
- ✅ Recent changes with file:line references
- ✅ Key learnings and gotchas
- ✅ Clear next steps
- ✅ Test status

### Good to Include
- Related plans/research documents
- Decisions made and rationale
- Approaches tried and results
- Dependencies added
- Questions that need answering

### Don't Include
- ❌ Large code blocks (use file:line references instead)
- ❌ Obvious/trivial information
- ❌ Outdated context
- ❌ Speculation without basis

## Tips for Good Handoffs

### Be Specific
- "Fixed auth bug in middleware.ts:42" ✅
- "Fixed some auth stuff" ❌

### Include File References
- "Added validation at `src/auth.ts:50-60`" ✅
- "Added validation somewhere" ❌

### Document Gotchas
- "⚠️ Must set AUTH_SECRET or app crashes silently" ✅
- "Need to configure auth" ❌

### Be Honest About Status
- "Integration test failing, needs investigation" ✅
- "Everything works!" (when it doesn't) ❌

### Make Next Steps Clear
- "Fix req.user mismatch in api.ts:100" ✅
- "Finish the implementation" ❌

## Example Handoffs

### Example 1: In-Progress Implementation

**Filename**: `thoughts/handoffs/2025-01-15-14-30-add-auth.md`

**Key sections**:
- Status: Phase 2 of 3 complete
- Recent changes: 5 files modified, 3 tests added
- Learnings: Middleware pattern, config gotchas
- Next: Fix failing test, then Phase 3

### Example 2: Research Handoff

**Filename**: `thoughts/handoffs/2025-01-15-10-00-database-research.md`

**Key sections**:
- Status: Research complete, ready for planning
- Findings: Compared Postgres vs MySQL, recommend Postgres
- Documents created: `thoughts/research/2025-01-15-db-comparison.md`
- Next: Create implementation plan

### Example 3: Blocked Work

**Filename**: `thoughts/handoffs/2025-01-15-16-00-payment-integration.md`

**Key sections**:
- Status: Blocked waiting for API credentials
- What's done: Mock implementation and tests
- Blocker: Need production API key from vendor
- Next: Once unblocked, swap mock for real API

## Remember

- Handoffs preserve context across time
- Be thorough but concise
- Focus on actionable information
- Make it easy to resume work
- Document learnings to avoid repeating mistakes
- Include enough detail that someone else could continue

A good handoff should answer:
1. What was being worked on?
2. What's the current state?
3. What's been learned?
4. What should happen next?
5. Are there any gotchas or blockers?
