# TODO Tracker - [Effort Name]

**Effort:** STEP_X_Y_[SHORTNAME]
**Status:** PLANNED / IN_PROGRESS / COMPLETE
**Total Checkpoints:** [X]
**Completed:** [Y]
**Current CP:** [CPZ] or None (not started)
**Last Updated:** [YYYY-MM-DD HH:MM] by [AI2 or AI3]

---

## Instructions

**For AI2 (creating this file):**
- Create after all CP guides are done
- List all CPs (CP0 through CPX from OUTLINE)
- Mark all as ⏸️ PENDING initially
- Set Status: PLANNED (awaiting AI3)

**For AI3 (updating this file):**
- Read before starting each CP (understand what's done)
- Update after completing each CP:
  - Change status: ⏸️ PENDING → ✅ COMPLETE
  - Add completion date and actual duration
  - Add notes (what went well, issues, learnings)
  - Update "Current CP" pointer
  - Update overall progress bar
- Commit after updating: `git commit -m "[STEP_X_Y] Update TODO - CPX complete"`

**For Framework (auto-detection):**
- Scans this file to determine current CP
- Finds first ⏸️ PENDING or 🔄 IN_PROGRESS
- Loads context for that CP

**For Human (status checking):**
- Quick status check (which CPs done? what's current? any blockers?)

---

## Overall Progress

**Progress bar:**
[░░░░░░░░░░] 0% ([Y] of [X] CPs complete)

**Status:**
- Planned: Awaiting AI3 execution
- OR In Progress: AI3 executing CPs
- OR Complete: All CPs done, awaiting PR merge

**Timeline:**
- Started: [Date] or Not yet
- Expected completion: [Date]
- Actual completion: [Date] or Ongoing

---

## Checkpoint Progress

### CP0: [Checkpoint Name] ⏸️ PENDING

**Goal:** [One sentence - what this CP accomplishes]

**Role:** AI3 (Implementer)

**Estimated duration:** [X hours]

**Status:** Not started

**Started:** N/A

**Completed:** N/A

**Actual duration:** N/A

**Tasks (high-level):**
- [Task 1]
- [Task 2]
- [Task 3]

**Dependencies:** None (first checkpoint)

**Blockers:** None

**Notes:**
[AI3 adds notes here when executing]

---

### CP1: [Checkpoint Name] ⏸️ PENDING

**Goal:** [One sentence]

**Role:** AI3

**Estimated duration:** [X days]

**Status:** Not started

**Dependencies:** CP0 must be complete

**Guide:** /guides/CP1_GUIDE.md

---

### CP2: [Checkpoint Name] ⏸️ PENDING

[Same structure]

**Dependencies:** CP1 must be complete

---

[Continue for all CPs through CPX]

---

### CPX: Testing & Deployment ⏸️ PENDING

**Goal:** Comprehensive validation and production launch

**Role:** AI3 + Human (AI3 prepares, Human approves)

**Estimated duration:** [X days]

**Status:** Not started

**Dependencies:** All previous CPs (CP0 through CPX-1) must be complete

**Critical tasks:**
- Comprehensive testing (E2E, performance, accessibility, security)
- Create PR to main
- Create COMPLETION_SUMMARY.md
- Update ATLAS_STEPS.md

**Guide:** /guides/CPX_GUIDE.md

---

## Example: How AI3 Updates After Completing CP0

**BEFORE (initial state):**
```
### CP0: Infrastructure Setup ⏸️ PENDING
**Status:** Not started
**Started:** N/A
**Completed:** N/A
```

**AFTER (AI3 updates):**
```
### CP0: Infrastructure Setup ✅ COMPLETE
**Status:** Complete
**Started:** 2025-12-16 09:00
**Completed:** 2025-12-16 14:30
**Actual duration:** 5.5 hours (estimated: 4h - took longer due to database migration complexity)

**Tasks completed:**
- Git branch created: effort/STEP_1_2_SITE_CLONER
- Vercel project: site-cloner (configured and deploying)
- Supabase: Reused [platform-name], added 3 tables (cloned_sites, assets, site_metadata)
- Environment: .env.local configured, Vercel env vars set
- Deployment: Validated (preview URL works)

**Notes:**
- Supabase table creation took longer than expected (complex schema with RLS policies)
- Puppeteer install smooth (1GB memory config applied from STEP_1_1 learnings)
- Deployment validated end-to-end (can push code → auto-deploy → site loads)

**Issues encountered:**
- None (setup went smoothly)

**For next CP:**
- Infrastructure ready
- Can start implementing scraper in CP1

**Updated:** 2025-12-16 14:35 by AI3

---

# Also update:
**Current CP:** CP1 (Site Scraping Engine)
**Progress:** [██░░░░░░░░] 20% (1 of 5 CPs complete)
```

---

## Status Markers

**Use these symbols:**
- ✅ COMPLETE - Checkpoint fully done, tested, validated
- 🔄 IN_PROGRESS - Currently executing (started but not finished)
- ⏸️ PENDING - Not started yet (awaiting previous CPs or ready to begin)
- ❌ BLOCKED - Cannot proceed (dependency missing, blocker encountered)

**Update status** after each CP completion (change symbol, add details)

---

## Notes Section

[AI3 adds general notes here during Effort execution]

**Example notes:**
- Reused component X from previous Effort (saved 3 hours)
- Customer provided content faster than expected (ahead of schedule)
- API rate limit hit on Day 3 (upgraded to paid tier $200/mo)

---

## Blockers Section

[AI3 documents any blockers encountered]

**Current blockers:** None

**Resolved blockers:**
- [Date]: [Blocker description]
  - Impact: [How it affected work]
  - Resolution: [How resolved]
  - Time cost: [Delay caused]

**If blocker encountered:**
1. Document immediately (don't wait)
2. Flag to human (if can't self-resolve)
3. Note in TODO_TRACKER (visibility)
4. Update when resolved

---

## Completion Checklist

**Effort is complete when:**

**All checkpoints:**
- [ ] CP0: ✅ COMPLETE
- [ ] CP1: ✅ COMPLETE
- [ ] CP2: ✅ COMPLETE
- [ ] ...
- [ ] CPX: ✅ COMPLETE

**Final deliverables:**
- [ ] COMPLETION_SUMMARY.md created
- [ ] ATLAS_STEPS.md updated (substep marked complete)
- [ ] PR created (staging → main)
- [ ] TODO_TRACKER shows 100% complete

**Quality validation:**
- [ ] All Effort success criteria met (from effort.md)
- [ ] All testing passed (comprehensive in final CP)
- [ ] Production ready (staging validated)

**When all checked:**
- Effort complete ✅
- Awaiting human PR approval
- After merge: Substep officially complete

---

## Progress Visualization

**Update progress bar after each CP:**

```
0%:   [░░░░░░░░░░] 0 of 5 complete
20%:  [██░░░░░░░░] 1 of 5 complete
40%:  [████░░░░░░] 2 of 5 complete
60%:  [██████░░░░] 3 of 5 complete
80%:  [████████░░] 4 of 5 complete
100%: [██████████] 5 of 5 complete
```

**Visual progress helps human quickly understand status.**

---

## Integration with Framework

**Framework uses TODO_TRACKER for:**

**Auto-detection:**
```
Find first CP marked ⏸️ PENDING or 🔄 IN_PROGRESS
→ This is current CP
→ Load context for this CP
→ Invoke AI3 for this CP
```

**Resume capability:**
```
Work pauses after CP2
Next day: "Continue ATLAS on STEP_X_Y"
Framework reads TODO_TRACKER: CP0-2 complete, CP3 pending
→ Automatically resumes at CP3
```

**Status reporting:**
```
"What's the status of STEP_X_Y?"
Framework reads TODO_TRACKER: 3 of 5 CPs complete (60%)
→ Reports exact progress
```

**This file is critical for state management. Keep it updated.**

---

## Related Documents

**Created by AI2:**
- OUTLINE.md (high-level CP map - created before this)
- CP guides (detailed instructions - created before this)
- OVERVIEW_GUIDE.md (quick-start - created before this)
- TODO_TRACKER.md (this file - created last in AI2 phase)

**Updated by AI3:**
- TODO_TRACKER.md (after each CP - mark complete, add notes)

**Read by:**
- AI3 (progress tracking, resume state)
- Framework (auto-detection)
- Human (status checking)

---

**Keep this file current. Update after EVERY checkpoint. This is how progress is tracked.**
