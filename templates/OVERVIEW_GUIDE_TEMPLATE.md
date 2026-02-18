# Overview Guide - [Effort Name]

**Effort:** STEP_X_Y_[SHORTNAME]
**For:** AI3 (Quick-start before diving into detailed guides)
**Created by:** AI2
**Date:** [YYYY-MM-DD]

---

## Instructions for AI2

This template defines OVERVIEW_GUIDE.md (your quick-start guide for AI3).

**Create this AFTER** all CP guides are done (synthesizes them).

**Purpose:** Get AI3 up to speed in 5 minutes (before reading detailed CP guides).

**Length:** 300-600 lines (concise overview, not detailed instructions)

---

## What We're Building

[1 paragraph - clear, specific description]

**Deliverable:**
[What gets built - product name, purpose]

**Tech stack:**
[Technologies used - Next.js, Supabase, Puppeteer, etc.]

**Deployment:**
[Where deployed - URL, platform]

**Duration:**
[Total Effort timeline - X days/weeks]

**Strategic impact:**
[Why this matters - how it advances company goals]

---

## Checkpoint Sequence

**Total:** [X] checkpoints (CP0 through CPX)

---

### CP0: Infrastructure Setup (AI3, [X] hours)

**Goal:**
[One sentence - what setup accomplishes]

**Key tasks:**
- [Task 1]
- [Task 2]
- [Task 3]

**Output:**
[What exists after CP0]

**Gotchas:**
- [Gotcha 1 to watch for]
- [Gotcha 2]

---

### CP1: [Phase Name] (AI3, [X] days)

**Goal:**
[One sentence goal]

**Key tasks:**
[High-level task list]

**Output:**
[What's delivered]

**Gotchas:**
[Things to watch for - API rate limits, memory issues, etc.]

---

### CP2: [Phase Name] (AI3, [X] days)

[Same structure for all middle CPs]

---

### CPX: Testing & Deployment (AI3, [X] days)

**Goal:**
Comprehensive validation and production launch

**Key tasks:**
- Full testing (E2E, performance, accessibility, cross-vertical)
- Staging validation
- PR creation (staging → main)
- COMPLETION_SUMMARY creation
- Progress updates (TODO_TRACKER, ATLAS_STEPS.md)

**Output:**
- Production deployment
- COMPLETION_SUMMARY.md
- Substep marked complete

**Critical:**
This is the quality gate. All success criteria must be met.

---

## Key Things to Watch For

**Performance targets:**
- [Specific target: <2s mobile load, Lighthouse 90+, etc.]
- [How to measure: PageSpeed Insights, Lighthouse]
- [When to optimize: If below target in CP[X]]

**Security concerns:**
- [Concern 1: API keys in .env, not code]
- [Concern 2: Input validation on all user input]
- [Concern 3: OWASP Top 10 vulnerabilities]
- [Spot-check: Before executing each CP (20% research)]

**Integration gotchas:**
- [Integration 1: Rate limits for API X (100/day free)]
- [Integration 2: Memory config for Puppeteer (1GB needed)]
- [Integration 3: Multi-tenant isolation (test user separation)]

**Multi-vertical compatibility (if applicable):**
- [Must test on: Contractor, law, healthcare sites]
- [Validate: Works universally, not just one vertical]
- [Watch for: Scoring calibration (different per vertical?)]

**Cost monitoring:**
- [Service X: Free tier limits, when to upgrade]
- [Infrastructure: Current cost, projected cost at scale]

---

## Testing Strategy

**Incremental (after each CP):**
- npm run build (must succeed)
- npm test (all pass)
- npm run lint (zero errors)
- Manual testing (feature works)
- Staging deployment (validate in preview)

**Comprehensive (final CP):**
- **E2E:** [Specific user flows to test]
- **Performance:** [Targets and validation method]
- **Accessibility:** [WCAG AA, axe scan]
- **Cross-vertical:** [Test on X site types]
- **Security:** [Scan for vulnerabilities]
- **Load:** [If applicable - concurrent users, requests/sec]

**Quality gates (all must pass before production):**
1. All Effort success criteria met (check effort.md)
2. Comprehensive testing passed (zero critical errors)
3. Staging validation complete (full manual test)
4. Human approval (reviewed and approved)

---

## Progress Tracking

**Use TODO_TRACKER.md:**
- Read before starting each CP (understand what's done)
- Update after completing each CP (mark ✅, add notes)
- Commit updates (git commit "[STEP_X_Y] Update TODO - CPX complete")

**Current CP indicator:**
- TODO_TRACKER shows which CP is next
- Framework uses this for auto-resume

---

## Git Workflow Summary

**Branch strategy:**
```
staging (working branch)
  ↓ create effort branch
effort/STEP_X_Y_[NAME] (feature branch)
  ↓ merge after each CP
staging (validation environment)
  ↓ PR after final CP (human approves)
main (production)
```

**Commit frequency:**
- After each logical change (component, feature, fix)
- Every 30-90 minutes of work
- Before taking breaks
- Don't batch days into one commit

**Testing before commit (always):**
```bash
npm run build && npm test && npm run lint
# All must pass before committing
```

**Merge to staging:**
- After each CP (for validation)
- Never force push to staging
- Test on staging before next CP

**PR to main:**
- Final CP only (comprehensive)
- Human approves and merges
- Don't merge yourself

**See GIT_WORKFLOW.md for detailed procedures.**

---

## Quick Reference

**Your execution checklist (AI3):**

**Starting Effort (CP0):**
1. Read OVERVIEW_GUIDE.md (this file - 5 min)
2. Read TODO_TRACKER.md (progress - 2 min)
3. Read START_HERE.md (AI1 research - 10 min)
4. Read effort.md (goals - 3 min)
5. Pre-flight checks (git sync - 2 min)
6. Read CP0_GUIDE.md (instructions - 8 min)
7. Execute CP0
8. Update TODO_TRACKER
9. Report complete

**Continuing (CP1+):**
1. Read OVERVIEW_GUIDE.md (refresher - 2 min)
2. Read TODO_TRACKER.md (what's done - 2 min)
3. Read CPX_GUIDE.md (instructions - 8 min)
4. Read previous CP notes (context - 5 min)
5. Execute CPX
6. Update TODO_TRACKER
7. Report complete

**Final CP (CPX):**
[Same as continuing, plus:]
8. Comprehensive testing
9. Create PR to main
10. Create COMPLETION_SUMMARY.md
11. Update ATLAS_STEPS.md
12. Report Effort complete

---

## Critical Links

**Planning documents:**
- Research: /START_HERE.md (AI1's comprehensive investigation)
- Checkpoint map: /OUTLINE.md (this doc without detail)
- Goals: /effort.md (success criteria, strategic context)

**Execution documents:**
- Quick-start: /OVERVIEW_GUIDE.md (this file)
- Detailed guides: /guides/CP0_GUIDE.md through CPX_GUIDE.md
- Progress: /TODO_TRACKER.md (update after each CP)

**Reference documents:**
- Coding standards: /ATLAS3/roles/AI3_DEVELOPER_BEST_PRACTICES.md
- Git procedures: /ATLAS3/roles/GIT_WORKFLOW.md
- Your role: /ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md

---

## For AI3: Start Here

**Read this file FIRST** when starting Effort.

**Then read:**
1. TODO_TRACKER.md (2 min - understand state)
2. CP0_GUIDE.md (8 min - detailed instructions)
3. START_HERE.md (10 min - research context, optional but helpful)

**Then execute CP0.**

**This OVERVIEW gives you the mental model. CP guides give you the steps.**

---

**Created by AI2. Enables AI3 to execute with confidence.**
