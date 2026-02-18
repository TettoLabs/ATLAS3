# CP[X] Guide - [Checkpoint Name]

**Checkpoint:** CP[X]
**Role:** AI3 (Implementer)
**Goal:** [One sentence - what this checkpoint accomplishes]
**Duration:** [X hours/days estimated]
**Type:** Setup / Implementation / Testing / Deployment

---

## Instructions for AI2

This template defines the structure for any checkpoint guide (CP0, CP1, CP2, ..., CPX).

**Create one guide per checkpoint** (number varies: 3-10 guides per Effort).

**Before creating this guide:**
- Research this checkpoint deeply (1-4 hours depending on complexity)
- Find examples, patterns, best practices
- Document exact steps, not vague directions

**Guide quality determines AI3's execution quality.**

**Length per guide:** 600-1,200 lines (detailed, precise, actionable)

---

## Overview

[2-3 paragraphs explaining what happens in this checkpoint]

**What this checkpoint builds:**
[Specific deliverables]

**Why this is a separate checkpoint:**
[Rationale for why this isn't combined with previous/next CP]

**Fits in Effort sequence:**
- Previous CP delivered: [What CP{X-1} produced]
- This CP delivers: [What this produces]
- Next CP needs: [What CP{X+1} requires from this]

---

## Checkpoint Type Guidance

**If CP0 (Setup):**
- This is ALWAYS infrastructure initialization
- NOT research (AI1 already researched)
- Tasks: Git, Vercel, Supabase, environment, dependencies, validation
- Output: Foundation ready for implementation CPs

**If CP1-CPX-1 (Implementation):**
- This is feature building, integration, functionality creation
- Tasks: Code implementation, testing, merging to staging
- Output: Working features, tested and deployed to staging

**If CPX (Final - Testing/Deployment):**
- This is ALWAYS comprehensive validation and production launch
- Tasks: Full testing, PR creation, COMPLETION_SUMMARY, progress updates
- Output: Production deployment, handoff documents

---

## Pre-Flight Checks (AI3 reads before starting)

**Required reading (in order):**

**If CP0 (first checkpoint):**
1. /ATLAS3/efforts/STEP_X_Y/OVERVIEW_GUIDE.md (5 min - mental model)
2. /ATLAS3/efforts/STEP_X_Y/TODO_TRACKER.md (2 min - progress state)
3. /ATLAS3/efforts/STEP_X_Y/START_HERE.md (10 min - research context)
4. /ATLAS3/efforts/STEP_X_Y/effort.md (3 min - goals)
5. /ATLAS3/efforts/STEP_X_Y/guides/CP0_GUIDE.md (8 min - this file)
6. /ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md (3 min - role refresher if needed)
7. /ATLAS3/roles/GIT_WORKFLOW.md (3 min - git procedures if needed)

**If CP1+ (subsequent checkpoints):**
1. /ATLAS3/efforts/STEP_X_Y/OVERVIEW_GUIDE.md (2 min - refresher)
2. /ATLAS3/efforts/STEP_X_Y/TODO_TRACKER.md (2 min - what's done)
3. /ATLAS3/efforts/STEP_X_Y/guides/CPX_GUIDE.md (8 min - this file)
4. Previous CP implementation notes (5 min - what was built)

**Total:** ~30-35 min first CP, ~15-20 min subsequent

---

**Git sync validation (CP0 only):**

**If first checkpoint in Effort:**
```bash
# Validate git is synced before starting
git fetch origin
git checkout main && git pull origin main
git checkout staging && git pull origin staging

# Verify both match remote
git log main -1
git log origin/main -1
# Hashes should match

git log staging -1
git log origin/staging -1
# Hashes should match

# Document any divergence
git diff main staging
# Note if significant diff (staging has unreleased work)
```

**Skip if:** Resuming mid-Effort (git already synced in CP0)

---

**Progress check:**
```bash
# Read TODO_TRACKER
cat TODO_TRACKER.md

# Understand:
# - Which CPs are complete? (marked ✅)
# - Which is current? (first ⏸️ or 🔄)
# - Any blockers? (documented issues)

# If resuming (some CPs complete):
# - Don't redo completed work
# - Read previous CP implementation notes
# - Understand current state
```

---

## Spot-Check Sanity (AI3's 20% research - 5-10 min)

**Before executing tasks, AI3 validates:**

**Security:**
- [ ] No hardcoded secrets? (API keys should be in .env)
- [ ] No SQL injection? (use parameterized queries, not string concat)
- [ ] No XSS? (sanitize user input, escape output)
- [ ] Input validated? (never trust user input)
- [ ] Authentication proper? (if this CP adds auth endpoints)

**Vulnerabilities:**
- [ ] Dependencies safe? (npm audit - check for HIGH/CRITICAL)
- [ ] OWASP Top 10? (common web vulnerabilities)
- [ ] Secrets exposed? (check .gitignore, no secrets in code)
- [ ] Rate limiting? (prevent abuse on API endpoints)

**Scaling concerns:**
- [ ] N+1 queries? (fetch in loop = slow, use JOIN or batch)
- [ ] Memory leaks? (connections closed, resources freed)
- [ ] Unbounded growth? (pagination on lists, limits on uploads)
- [ ] Caching? (repeated operations cached)

**Approach sanity:**
- [ ] Will this achieve intended outcome? (check against success criteria)
- [ ] Missing anything? (error handling, edge cases, validation)
- [ ] Overcomplicated? (simpler approach exists?)
- [ ] Red flags? (TODOs in guide, assumptions not validated, vague steps)

**If issues found:**
- Critical (security): Flag to human immediately (don't proceed with vulnerable approach)
- Medium (scaling): Document in implementation notes (fix if time permits, or note for future)
- Minor (code style): Fix during implementation

**If major concerns:** Stop, get clarification. Don't implement flawed approach.

**Time:** 5-10 minutes (quick scan, not deep audit - AI1/AI2 already researched)

---

## Tasks

**List all tasks for this checkpoint with exact steps.**

### Task 1: [Task Title] ([time estimate])

**What:**
[Description of what this task accomplishes]

**Why:**
[Why this task is needed - ties to checkpoint goal]

**How:**

**Step-by-step instructions:**

1. [First step - be specific]
   ```bash
   # Exact command if applicable
   [command]
   ```

2. [Second step]
   ```typescript
   // Code example if applicable
   [code snippet showing exact pattern]
   ```

3. [Third step]
   [Continue with all steps]

**Code examples:**

```typescript
// File: [exact file path]
// Purpose: [what this code does]

[Complete code example showing the pattern, not pseudocode]

// Example with real types, real imports, real logic
import { createClient } from '@supabase/supabase-js';

export async function exampleFunction(param: string): Promise<Result> {
  // Implementation showing exact pattern
  const supabase = createClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.SUPABASE_SERVICE_KEY!
  );

  const { data, error } = await supabase
    .from('table_name')
    .select('*')
    .eq('column', param);

  if (error) {
    console.error('Error:', error);
    throw new Error(`Database query failed: ${error.message}`);
  }

  return data;
}
```

**Based on:**
[Reference to where this pattern came from]
- Documentation: [Link to docs section]
- Example: [Link to repo, previous Effort file]
- Pattern: [Previous successful implementation]

**Gotchas:**
- [Gotcha 1: Common mistake and how to avoid]
- [Gotcha 2: Edge case to handle]

**Output from this task:**
- [File created or modified]
- [Feature implemented]
- [What should exist after task]

**Validation:**
```bash
# How to verify this task is complete
[exact validation command or test]

# Expected result:
[what success looks like]
```

---

### Task 2: [Task Title] ([time estimate])

[Same complete structure]

---

### Task 3: [Continue for all tasks in this CP]

[Each task gets full treatment - What, Why, How, Examples, Gotchas, Output, Validation]

**Typical CP has: 3-8 tasks**

---

## Outputs (What This CP Produces)

**Artifacts:**

**Artifact 1:** `artifacts/CPX_[name].md`
- **Purpose:** [What this artifact documents]
- **Created by:** AI3 (during or after task execution)
- **Format:** [Structure - see example below]
- **Used by:** [Next CP, human review, future reference]

**Artifact 2:** Working code/implementation
- **Location:** [File path or directory]
- **What:** [Code that was written]
- **Purpose:** [What this code does]

**Artifact 3:** [If applicable - tests, documentation, assets]

**Example artifact structure:**

```markdown
# CPX Implementation Notes

## What Was Built
[List of deliverables]

## Technical Decisions
[Decisions made during implementation]

## Issues Encountered
[Problems and solutions]

## For Next CP
[What next CP should know]
```

---

## Success Criteria

**This checkpoint is complete when:**

**Implementation complete:**
- [ ] All tasks from this guide executed
- [ ] All deliverables produced
- [ ] Code follows best practices (see AI3_DEVELOPER_BEST_PRACTICES.md)
- [ ] No TODOs or FIXMEs left (or documented as intentional)

**Testing passed:**
- [ ] Build succeeds: `npm run build`
- [ ] All tests pass: `npm test`
- [ ] Lint clean: `npm run lint`
- [ ] Manual testing done (features work as expected)
- [ ] Performance validated (if applicable - <2s load, Lighthouse 90+)
- [ ] Accessibility validated (if applicable - WCAG AA, zero critical errors)

**Git workflow followed:**
- [ ] Frequent commits (after each logical change, not one giant commit)
- [ ] Clear commit messages ([STEP_X_Y] CPX - description)
- [ ] All commits pushed to effort branch
- [ ] Merged to staging (if appropriate - usually yes)
- [ ] Staging deployment verified (preview works)

**Documentation created:**
- [ ] Implementation notes (artifacts/CPX_implementation_notes.md)
- [ ] Decisions documented (what/why in notes)
- [ ] Issues documented (problems encountered and solutions)
- [ ] README updated (if applicable)

**Progress updated:**
- [ ] TODO_TRACKER.md updated (this CP marked ✅ COMPLETE)
- [ ] Completion date added
- [ ] Actual duration noted
- [ ] Notes added (what went well, issues, learnings)
- [ ] Current CP pointer updated (to next CP or "All complete")
- [ ] TODO update committed and pushed

**All criteria must be checked before moving to next CP.**

---

## Testing Checklist (Execute After CP Tasks)

**Standard tests (every CP):**

```bash
# 1. Build validation
npm run build
# Expected: ✓ Compiled successfully
# If fails: Fix errors before proceeding

# 2. Type check
npx tsc --noEmit
# Expected: No type errors
# If fails: Fix TypeScript issues

# 3. Lint check
npm run lint
# Expected: Zero errors (warnings ok if justified)
# If fails: Fix linting issues or justify warnings

# 4. Test suite
npm test
# Expected: All tests pass
# If fails: Fix failing tests or implementation

# 5. Dev server
npm run dev
# Expected: Starts without errors
# Visit localhost:3000, test new features

# 6. Manual feature testing
# Test what was built in this CP
# Verify: Works as expected, no console errors, mobile responsive

# 7. Git status check
git status
# Expected: No uncommitted changes (all work committed)
```

**CP-specific tests:**

**If user-facing functionality (CP1+ implementation):**
```bash
# Performance test
npm run lighthouse  # or manual PageSpeed Insights
# Target: Performance 90+, mobile <2s

# Accessibility scan
# Use axe DevTools or WAVE extension
# Target: Zero critical errors, WCAG AA compliant
```

**If database changes (any CP):**
```bash
# Verify migrations applied
psql $DATABASE_URL -c "\dt"  # List tables
# Expected: New tables exist

psql $DATABASE_URL -c "SELECT COUNT(*) FROM [new_table];"
# Expected: 0 rows (empty, ready for data) or test data if seeded
```

**If API endpoints (CP1+ implementation):**
```bash
# Test endpoints
curl -X POST http://localhost:3000/api/[endpoint] \
  -H "Content-Type: application/json" \
  -d '{"test":"data"}'

# Expected: 200 OK with expected response
# Test error cases too (400, 401, 500)
```

**All tests must pass before marking CP complete.**

---

## Update TODO_TRACKER (Required After CP)

**Template for TODO update:**

```bash
# Edit /TODO_TRACKER.md

# Change this CP's section:

FROM:
### CPX: [Checkpoint Name] ⏸️ PENDING
**Status:** Not started

TO:
### CPX: [Checkpoint Name] ✅ COMPLETE
**Completed:** 2025-12-[DD] [HH:MM]
**Actual duration:** [X.Y] hours/days (estimated: [Z] hours/days)
**Status:** Complete

**Tasks completed:**
- [Task 1 summary]
- [Task 2 summary]
- [Task 3 summary]

**Output:**
- [Deliverable 1]
- [Deliverable 2]

**Notes:**
- [What went well]
- [Issues encountered and how resolved]
- [Any learnings or discoveries]

**Blockers encountered:** None / [Description if any]

**For next CP:**
- [What CP{X+1} can assume is ready]
- [What to watch out for]

**Updated:** [Date Time] by AI3

---

# Also update these sections:

**Current CP:** CP{X+1} or "All complete" if this was last

**Progress bar:**
[████████░░] 80% (4 of 5 CPs complete)

# Commit update
git add TODO_TRACKER.md
git commit -m "[STEP_X_Y] Update TODO - CPX complete"
git push origin effort/STEP_X_Y_[NAME]
```

**AI3: You MUST do this after every CP. Non-negotiable.**

---

## Next Checkpoint

**What comes after this CP:**

**If not final CP:**
```
Next: CP{X+1} - [Next checkpoint name]

AI3 should:
1. Read TODO_TRACKER (verify this CP marked ✅)
2. Read guides/CP{X+1}_GUIDE.md (next instructions)
3. Read artifacts/CPX_implementation_notes.md (context from this CP)
4. Execute CP{X+1}

Continue: "Continue ATLAS on STEP_X_Y" (framework will auto-load CP{X+1})
```

**If final CP:**
```
This is the FINAL checkpoint.

After tasks above, complete these final responsibilities:

1. Comprehensive testing (beyond normal CP testing)
2. Create PR to main (staging → main, don't merge)
3. Create COMPLETION_SUMMARY.md (handoff document)
4. Update ATLAS_STEPS.md (mark substep complete)
5. Final TODO_TRACKER update (all CPs ✅)
6. Report Effort complete (awaiting human PR approval)

See "Final CP Additional Tasks" section below if this is final CP.
```

---

## Final CP Additional Tasks (Only if CPX - Last Checkpoint)

**If this is the last checkpoint, include these additional responsibilities:**

### Task X+1: Comprehensive Testing (1-2 hours)

**Beyond standard CP testing, run full test suite:**

```bash
# 1. E2E tests (if exist)
npm run test:e2e

# 2. Performance validation
npm run build && npm start
# Use Lighthouse or PageSpeed Insights on http://localhost:3000
# Targets: Performance 90+, <2s mobile load

# 3. Accessibility audit
# Use axe DevTools, scan all pages
# Target: Zero critical errors, WCAG AA compliant

# 4. Cross-vertical testing (if multi-vertical tool)
# Test on contractor site: [URL]
# Test on law firm site: [URL]
# Test on healthcare site: [URL]
# Validate: Works for all, not just one type

# 5. Security scan
npm audit  # Check dependency vulnerabilities
grep -r "console.log" src/  # Should find zero (or only in utils)
grep -r "api.*key.*=" src/  # Should find zero (no hardcoded secrets)

# 6. Load testing (if applicable)
# Test concurrent users, requests/sec
# Validate: Handles expected load

# 7. Full staging validation
# Deploy to staging (should already be there)
# Visit staging URL
# Full manual walkthrough (every feature, every page)
# Share with customer (if applicable - get approval)
```

**All tests must pass before production.**

---

### Task X+2: Create PR to Main (Don't Merge)

```bash
# 1. Ensure staging has all work
git checkout staging
git pull origin staging
# Should include all Effort commits

# 2. Verify staging deployment
# Visit staging URL, full manual test

# 3. Create PR
gh pr create \
  --base main \
  --head staging \
  --title "[STEP_X_Y] Complete - [Brief description]" \
  --body "See COMPLETION_SUMMARY.md for details"

# 4. Note PR number
# Example: PR #47

# DO NOT MERGE
# Human will review code, testing, COMPLETION_SUMMARY
# Human merges after approval
```

---

### Task X+3: Create COMPLETION_SUMMARY.md (30-60 min)

**Template:** /ATLAS3/templates/COMPLETION_SUMMARY_TEMPLATE.md

**Document:**
- What was built (deliverables, metrics, tech)
- Key decisions (what you chose, why, outcomes)
- What worked (patterns to repeat)
- What didn't work (issues and solutions)
- Recommendations for next substep (what to reuse, what to avoid)
- Technical foundation (infrastructure, patterns, costs)

**Save to:** /efforts/STEP_X_Y/COMPLETION_SUMMARY.md

**This is critical handoff** - next substep's AI1 reads THIS (not all artifacts)

---

### Task X+4: Update ATLAS_STEPS.md (5 min)

```bash
# Edit /ATLAS3/strategy/ATLAS_STEPS.md

# Find STEP_X_Y, mark complete:

#### STEP_X_Y: [Substep Name]
**Status:** ✅ COMPLETE
**Completed:** [Date]
**Duration:** [Actual] days (estimated: [Est])
**Outcome:** [Brief summary - URL deployed, metrics achieved]
**Details:** efforts/STEP_X_Y_[NAME]/COMPLETION_SUMMARY.md

# If all substeps in Step X complete, update Step status:
## STEP X: [Step Name]
**Status:** ✅ COMPLETE (all substeps done)
**Completed:** [Date]

# Commit update
git add strategy/ATLAS_STEPS.md
git commit -m "Strategy: Mark STEP_X_Y complete"
git push
```

---

### Task X+5: Final TODO Update (5 min)

```bash
# Edit TODO_TRACKER.md

# Mark final CP complete (same as other CPs)

# Update overall status:
**Status:** ✅ COMPLETE (all CPs done)
**Completed:** [Date]

# Update progress bar:
Progress: [██████████] 100% ([X] of [X] CPs complete)

# Add final note:
## Final Status

All checkpoints complete.
COMPLETION_SUMMARY created.
ATLAS_STEPS.md updated.
PR #[X] created (awaiting human approval).

Effort STEP_X_Y complete. ✅

# Commit
git add TODO_TRACKER.md
git commit -m "[STEP_X_Y] Final TODO update - all CPs complete"
git push
```

---

## Rollback Plan

**If this checkpoint needs to be undone:**

**Within effort branch (before staging merge):**
```bash
# Option A: Revert specific commits
git log --oneline  # Find problematic commits
git revert <commit-hash>  # Revert each

# Option B: Reset to previous CP (destructive)
git log --oneline  # Find CP{X-1} complete commit
git reset --hard <previous-cp-commit>
git push --force origin effort/STEP_X_Y  # OK for effort branch (not staging/main)
```

**After staging merge:**
```bash
# Revert merge on staging
git checkout staging
git log --oneline  # Find merge commit
git revert -m 1 <merge-commit>  # Keep staging history
git push origin staging

# Fix issues on effort branch
git checkout effort/STEP_X_Y
# Fix problems
# Re-merge when ready
```

**Production rollback:**
- Human handles (not AI3)
- Via git revert or Vercel instant rollback
- See GIT_WORKFLOW.md for procedures

---

## Completion Report (AI3 Provides After CP)

```
Checkpoint CPX of Effort STEP_X_Y_[NAME] complete.

Duration: [Actual time] (estimated: [Est])

Implemented:
- [Feature/component 1]
- [Feature/component 2]
- [Feature/component 3]

Artifacts produced:
- Code: [Location] ([X,XXX] lines)
- Tests: [Location] ([XX] tests, all passing)
- Implementation notes: artifacts/CPX_implementation_notes.md

Testing:
- Build: ✅ Success
- Tests: ✅ [XX]/[XX] passing
- Lint: ✅ Clean
- Manual: ✅ [Features tested]
- Performance: ✅ [Metrics] (if applicable)
- Accessibility: ✅ [Compliance] (if applicable)

Git:
- Commits: [XX] commits in this CP
- Staging: Merged and deployed ✅
- Preview: [Vercel URL]

TODO_TRACKER:
- Updated: CPX marked ✅
- Current CP: CP{X+1} or "All complete"
- Progress: [XX]%

Issues:
- [Any issues encountered]
- [Resolutions]

Next:
- [If not final: Next CP name and brief description]
- [If final: PR created, awaiting human approval]

Continue: "Continue ATLAS on STEP_X_Y"
[Framework will auto-load next CP or recognize completion]

[If final CP: See full Effort completion report in AI3_IMPLEMENTER_GUIDE.md]
```

---

## Notes for AI2 (Creating This Guide)

**When creating this guide:**

**Research phase (1-4 hours):**
- What does this CP specifically need? (not general - specific to this CP's goal)
- Find examples (code repos, docs, previous Efforts)
- Identify patterns (what's the best approach?)
- Document gotchas (what goes wrong? how to avoid?)

**Guide creation (1 hour):**
- Transform research into actionable steps
- Include exact commands, code examples
- Reference sources (where patterns came from)
- Add validation steps (how to test)

**Quality check:**
- Could AI3 execute this without asking questions? (if no, add more detail)
- Are commands exact? (not "set up Vercel" but exact steps)
- Are examples complete? (not pseudocode, real code)
- Are gotchas documented? (things that go wrong)

**Your guide quality determines AI3's execution quality.**

**Detailed guides → confident AI3 → fast, correct implementation.**

---

## Related Documents

**For context:**
- START_HERE.md (AI1's research - why this approach)
- OUTLINE.md (CP sequence and rationale)
- OVERVIEW_GUIDE.md (quick-start for Effort)
- effort.md (goals and success criteria)

**For execution:**
- AI3_IMPLEMENTER_GUIDE.md (role responsibilities)
- AI3_DEVELOPER_BEST_PRACTICES.md (code quality standards)
- GIT_WORKFLOW.md (git procedures)

**For progress:**
- TODO_TRACKER.md (mark this CP complete after execution)

---

**This guide is executed by AI3. Make it precise, detailed, and actionable.**
