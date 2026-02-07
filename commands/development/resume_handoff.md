# Resume Handoff

You help resume work from handoff documents created in previous sessions.

## Purpose

Resume work that was paused by reading handoff documents, validating current state, and continuing from where it left off.

## Initial Response

**If handoff path provided**: Read it and proceed

**If no path**: List available handoffs
```
I'll help resume work from a handoff. Let me find available handoff documents...

[Search thoughts/handoffs/ for recent files]

Available handoffs:
1. thoughts/handoffs/2025-01-15-14-30-add-auth.md (2 hours ago)
   - Status: in-progress
   - Task: Add JWT authentication

2. thoughts/handoffs/2025-01-14-16-00-api-refactor.md (yesterday)
   - Status: blocked
   - Task: Refactor API endpoints

Which would you like to resume? Or provide a path to a specific handoff.
```

## Resume Process

### Step 1: Read Handoff Completely

Read the handoff document WITHOUT limits:
- Understand the task and context
- Note current status (done/remaining)
- Read key learnings and gotchas
- Identify next steps
- Check for blockers

Read any referenced documents:
- Related plans
- Research documents
- Original tickets/issues

### Step 2: Validate Current State

**CRITICAL**: Never assume the handoff state matches current reality. Always validate.

**Check Git State:**
```bash
# Compare current branch with handoff
git branch --show-current

# Check for new commits since handoff
git log --since="[handoff date]" --oneline

# Check current changes
git status
git diff --name-only
```

**Verify Files Still Exist:**
```bash
# Check files mentioned in handoff exist
ls [file paths from handoff]
```

**Run Tests:**
```bash
# Run test suite to see current state
npm test
# or pytest, go test, etc.
```

### Step 3: Analyze Discrepancies

Compare handoff state with current reality:

**Scenario A: Clean Continuation** ✅
- No new commits since handoff
- Files match handoff description
- Test status matches handoff
- → Can proceed directly with next steps

**Scenario B: Code Has Diverged** ⚠️
- New commits since handoff
- Files changed from handoff state
- → Need to analyze what changed and adjust plan

**Scenario C: Handoff is Stale** ⚠️
- Significant time has passed
- Major changes to codebase
- Context may be outdated
- → May need to re-research before continuing

**Scenario D: Blockers Resolved** ✅
- Handoff showed blockers
- Check if blockers are now unblocked
- → Can proceed if clear

### Step 4: Spawn Validation Agents (if needed)

If code has diverged or handoff is stale:

```markdown
codebase-analyzer:
"Analyze [component] and verify current state matches handoff description at thoughts/handoffs/[file]"

codebase-locator:
"Find files related to [task] and check if any new files were added since [handoff date]"

thoughts-locator:
"Find any new plans or research about [topic] created after [handoff date]"
```

### Step 5: Present Analysis

Show comprehensive analysis before starting work:

```markdown
# Handoff Analysis: [Task]

**Handoff Date**: YYYY-MM-DD HH:MM
**Time Since**: [X hours/days ago]

## Original Context

**Task**: [Task description from handoff]

**Status When Paused**: [status]
- ✅ Completed: [items]
- [ ] Remaining: [items]

**Key Learnings from Handoff**:
- [Learning 1]
- [Learning 2]
- ⚠️ [Gotcha 1]

## Current State Validation

### Git Status: [✅ Clean | ⚠️ Diverged | ❌ Significant Changes]

**Since handoff**:
- X new commits
- Y files changed
- Z files mentioned in handoff

**Relevant new commits**:
- `abc123`: "Description" - [RELATED/UNRELATED]

### Code Verification: [✅ Matches | ⚠️ Partially Matches | ❌ Diverged]

**Files from handoff**:
- ✅ `src/auth.ts` - Matches handoff description
- ⚠️ `src/routes.ts` - Modified since handoff (see commit abc123)
- ❌ `src/middleware.ts` - Significantly changed

**Issues found**:
- [Description of any issues]

### Test Status: [✅ | ⚠️ | ❌]

**Handoff said**:
- 15 tests passing
- 1 test failing (integration/auth.test.ts:45)

**Current state**:
- 16 tests passing (1 new test added)
- ❌ Still 1 test failing (same issue)

### Blockers: [✅ Resolved | ⚠️ Still Blocked | ❓ Unknown]

**Handoff blockers**:
- Waiting for API credentials

**Current status**:
- ✅ Credentials received (in .env file)
- Can proceed with implementation

## Artifacts Status

**From handoff**:
- ✅ `src/auth/middleware.ts:42-60` - Still exists, unchanged
- ⚠️ `src/routes/api.ts:100-120` - Modified by commit abc123
- ✅ `tests/auth.test.ts:10-50` - Still exists, one test added

## Recommended Next Actions

### Immediate Steps:
1. [Action 1] - [Reason]
2. [Action 2] - [Reason]

### Considerations:
- [Consideration 1]
- [Consideration 2]

### Risks:
- ⚠️ [Risk 1]

## Questions Before Proceeding

[Any clarifying questions needed before starting work]
```

### Step 6: Create Todo List

Convert handoff next steps into actionable todos:

```markdown
I'll create a todo list based on the handoff:

- [ ] Verify current state matches handoff expectations
- [ ] Review changes made since handoff
- [ ] [Next step 1 from handoff]
- [ ] [Next step 2 from handoff]
- [ ] Update handoff document when complete
```

Use TodoWrite to track these.

### Step 7: Execute (with confirmation)

**Don't automatically start work**. Present analysis first:

> **Ready to Resume**
>
> **Status**: [Clean/Needs Adjustment]
>
> **Summary**:
> - Original task: [description]
> - Time since handoff: [duration]
> - Current state: [matches/diverged]
> - Next action: [what to do]
>
> **Proposed approach**:
> 1. [Step 1]
> 2. [Step 2]
>
> Ready to proceed? Or would you like me to adjust the approach?

Wait for confirmation before starting.

### Step 8: Implement with Context

As you work:
- Reference learnings from handoff
- Avoid approaches that failed (documented in handoff)
- Apply gotchas/warnings from handoff
- Update the handoff or create a new one if pausing again

## Handling Different Scenarios

### Scenario: Clean Continuation

Handoff is recent, no changes since then.

**Action**:
1. Verify test status matches
2. Continue with next steps from handoff
3. Apply learnings from handoff

### Scenario: Code Has Diverged

New commits changed files mentioned in handoff.

**Action**:
1. Analyze new commits
2. Determine if they conflict with handoff plan
3. Adjust approach if needed
4. Document differences
5. Proceed with updated understanding

### Scenario: Handoff is Stale

Significant time passed, major codebase changes.

**Action**:
1. Research current state with agents
2. Compare with handoff expectations
3. Determine if handoff approach still valid
4. May need to create new plan
5. Archive old handoff if obsolete

### Scenario: Blocker Resolved

Handoff showed blockers, now resolved.

**Action**:
1. Verify blocker actually resolved
2. Check if resolution changes approach
3. Proceed with unblocked work
4. Update handoff status

### Scenario: Still Blocked

Handoff showed blockers, still present.

**Action**:
1. Confirm blocker still exists
2. Investigate workarounds
3. Document current blocker status
4. Determine if alternative approach possible
5. Either proceed with workaround or wait

## Critical Rules

### Always Validate First
Don't trust the handoff blindly:
- ❌ "Handoff says file X exists, so it does"
- ✅ "Handoff says file X exists, let me verify"

### Read Completely
Read handoff without truncation:
- ✅ Use Read tool without offset/limit
- ❌ Skim or partially read

### Check for Changes
Always check what happened since handoff:
- ✅ `git log --since="[date]"`
- ✅ Compare file states
- ❌ Assume nothing changed

### Present Before Acting
Show analysis before starting:
- ✅ Present findings, get confirmation
- ❌ Immediately start implementing

### Learn from Handoff
Apply documented learnings:
- ✅ Avoid failed approaches
- ✅ Heed warnings/gotchas
- ❌ Repeat mistakes

### Update or Create New Handoff
If pausing again:
- ✅ Update existing handoff with progress
- ✅ Or create new handoff
- ❌ Leave work without documentation

## Example Resume Flow

**User**: `/resume_handoff thoughts/handoffs/2025-01-15-14-30-add-auth.md`

**You**:
1. Read handoff completely
2. Check git log since 2025-01-15 14:30
3. Verify test status
4. Check if files mentioned still exist
5. Present analysis:
   > Handoff is from 2 hours ago. State is clean - no new commits.
   >
   > Original task: Add JWT authentication (Phase 2 of 3)
   > Status: 1 integration test failing
   > Next: Fix req.user mismatch, then Phase 3
   >
   > Handoff warns: Must set AUTH_SECRET env var
   >
   > Ready to continue?
6. Wait for confirmation
7. Fix the failing test
8. Continue with Phase 3
9. Update handoff or create new one

## Tips for Successful Resume

### Before Starting Work
- ✅ Read handoff completely
- ✅ Validate current state
- ✅ Identify any changes
- ✅ Present analysis
- ✅ Get confirmation

### During Work
- ✅ Reference handoff learnings
- ✅ Apply documented gotchas
- ✅ Avoid failed approaches
- ✅ Track progress with todos

### When Pausing Again
- ✅ Update existing handoff, or
- ✅ Create new handoff
- ✅ Document new learnings
- ✅ Note current progress

## Remember

Handoffs are snapshots in time:
- They capture state at a moment
- Reality may have moved on
- Always validate before trusting
- Adapt approach as needed
- Learn from documented experience

The goal is **continuity**, not **blind following**.
