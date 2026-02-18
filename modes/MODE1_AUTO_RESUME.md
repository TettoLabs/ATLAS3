# Mode 1: Auto-Resume - Find State & Continue Work

**Purpose:** Automatically detect where work stopped and continue from exact point
**Usage:** 85% of time (most common workflow)
**Trigger:** Human says "Continue ATLAS on STEP_X_Y" or "Resume ATLAS work"

---

## What This Mode Does

**Scans files to determine:**
1. Which Effort directory (STEP_X_Y_[NAME])
2. Which AI phase (AI1 research, AI2 planning, or AI3 execution)
3. Which checkpoint (if AI3 phase)
4. What context to load
5. What to do next

**Executes:** The appropriate workflow (AI1 research, AI2 planning, or AI3 execution)

**No manual state tracking needed.** File existence reveals everything.

---

## Auto-Detection Algorithm

### Step 1: Locate Effort

```bash
find /ATLAS3/efforts/ -type d -name "STEP_X_Y*"
```

**Outcomes:**
- **Not found:** Substep hasn't started → Offer to start AI1
- **One match:** Proceed to step 2
- **Multiple matches:** Ask human which one

---

### Step 2: Detect AI Phase

**Check START_HERE.md exists?**
```bash
ls efforts/STEP_X_Y_[NAME]/START_HERE.md 2>/dev/null
```
- NO → AI1 phase needed (go to Workflow A)
- YES → Continue

**Check OUTLINE.md exists?**
```bash
ls efforts/STEP_X_Y_[NAME]/OUTLINE.md 2>/dev/null
```
- NO → AI2 phase starting (go to Workflow B)
- YES → Continue

**Check all guides exist?**
```bash
CP_COUNT=$(grep -c "^### CP" efforts/STEP_X_Y/OUTLINE.md)
GUIDE_COUNT=$(ls efforts/STEP_X_Y/guides/*.md 2>/dev/null | wc -l)
```
- Mismatch → AI2 phase incomplete (go to Workflow C)
- Match → Continue

**Check TODO_TRACKER exists?**
```bash
ls efforts/STEP_X_Y/TODO_TRACKER.md 2>/dev/null
```
- NO → AI2 phase final task (go to Workflow D)
- YES → AI2 complete, continue

**Find current CP:**
```bash
grep -E "⏸️ PENDING|🔄 IN_PROGRESS" efforts/STEP_X_Y/TODO_TRACKER.md | head -1
```
- Extract CP number → AI3 phase (go to Workflow E)

---

## Workflow A: AI1 Research

**Files to load:**
```
1. roles/AI1_RESEARCHER_GUIDE.md (~10min)
2. strategy/steps/STEP_X.md (relevant step file - ~3min)
3. Previous COMPLETION_SUMMARY (if exists - ~8min)
4. /COMPANY_CONTEXT.md (~8min)
5. strategy/LEARNINGS_LOG.md (last 10-15 entries - ~5min)

Total: ~35min, ~35K tokens
```

**Process:**
- Create efforts/STEP_X_Y_[NAME]/ directory
- Research substep deeply (6-12 hours)
- Create START_HERE.md
- Report complete

**Next:** Framework auto-detects AI2 phase on next "Continue ATLAS on STEP_X_Y"

---

## Workflow B: AI2 Planning Start

**Files to load:**
```
1. roles/AI2_GUIDE_CREATOR_GUIDE.md (~5min)
2. START_HERE.md (deep read - ~15min)
3. strategy/steps/STEP_X.md (relevant step file - ~3min)
4. Previous COMPLETION_SUMMARY (if exists - ~8min)
5. /COMPANY_CONTEXT.md (~3min)
6. strategy/LEARNINGS_LOG.md (last 15-20 entries - ~6min)
7. strategy/DECISION_LOG.md (last 10 entries - ~4min)
8. templates/ (OUTLINE, CP_GUIDE - ~5min)

Total: ~50min, ~50K tokens
```

**Process:**
- Validate AI1's research
- Create OUTLINE.md (decide CP count 3-10)
- Report outline complete

**Next:** Framework detects guide creation phase

---

## Workflow C: AI2 Planning Continue

**Files to load:**
```
Same as Workflow B, plus:
- Already-created guides (maintain consistency)
```

**Process:**
- Research next CP deeply (2-4 hours)
- Create CPX_GUIDE.md
- Repeat for all remaining CPs
- Create OVERVIEW_GUIDE.md
- Create TODO_TRACKER.md
- Create effort.md
- Report AI2 complete

**Next:** Framework detects AI3 phase

---

## Workflow D: AI2 Final Tasks

**Just create TODO_TRACKER.md and report complete.**

---

## Workflow E: AI3 Execution

**Files to load (CP0):**
```
1. roles/AI3_IMPLEMENTER_GUIDE.md (~3min)
2. roles/AI3_DEVELOPER_BEST_PRACTICES.md (reference)
3. roles/GIT_WORKFLOW.md (reference)
4. OVERVIEW_GUIDE.md (~5min)
5. TODO_TRACKER.md (~2min)
6. START_HERE.md (~10min)
7. effort.md (~3min)
8. guides/CP0_GUIDE.md (~8min)

Total: ~35min, ~60K tokens
```

**Files to load (CP1+):**
```
1. OVERVIEW_GUIDE.md (~2min)
2. TODO_TRACKER.md (~2min)
3. CPX_GUIDE.md (~8min)
4. Previous CP notes (~5min)

Total: ~17min, ~25K tokens
```

**Process:**
- Pre-flight (CP0 only - git sync)
- Read CP guide
- Spot-check sanity/security
- Execute tasks
- Test after CP
- Update TODO_TRACKER
- Merge to staging
- Report complete
- Continue to next CP or final tasks

**If final CP:**
- Comprehensive testing
- Create PR (don't merge)
- Create COMPLETION_SUMMARY.md
- Update ATLAS_STEPS.md
- Update TODO_TRACKER
- Report Effort complete

---

## Key Features

**✅ No manual state tracking** - Files reveal everything
**✅ Resume anywhere** - CP2 of 5? Start there.
**✅ Context optimized** - Loads only what's needed
**✅ Error handling** - Catches inconsistent states

---

**This mode handles standard execution flow. 85% of usage.**
