# Context Index - Smart Context Loading Rules

**Purpose:** Define exactly which files each AI loads for each phase
**Why:** Prevent context explosion (load 8-25 files, not 50+)
**Status:** v2.0 - Updated for three-phase workflow

---

## Core Principle

**Load minimum necessary, not maximum available.**

**Context budget per session:**
- AI1 Research: 8-12 files (~35K tokens)
- AI2 Planning: 12-18 files (~65K tokens)
- AI3 CP0: 12-18 files (~60K tokens first time)
- AI3 CP1+: 8-12 files (~35K tokens subsequent)

**Leaves:** 200K-250K tokens for thinking, research, generation

**Scales to:** 100+ Efforts without context explosion

---

## AI1 Research Phase (Substep-Level)

**When:** No START_HERE exists for STEP_X_Y

**Load these files (in order):**

```
1. ATLAS_OVERVIEW.md (~300 lines, ~3K tokens)
   Time: 2 min skim (10 min first time)

2. ATLAS_GLOSSARY.md (~200 lines, ~2K tokens)
   Time: 1 min (keep open for reference)

3. roles/AI1_RESEARCHER_GUIDE.md (~1,000 lines, ~11K tokens)
   Time: 3 min skim (10 min first time)

4. steps/STEP_X.md - RELEVANT STEP FILE
   Load: Individual step file (not entire tracker)
   Read: Substep X.Y definition specifically
   Lines: ~150-300 (single step file)
   Tokens: ~3K
   Time: 3 min

5. Previous COMPLETION_SUMMARY (if exists)
   File: efforts/STEP_X_{Y-1}_[NAME]/COMPLETION_SUMMARY.md
   Lines: ~500-1,000
   Tokens: ~7K
   Time: 8 min
   Skip if: First substep (X.1)

6. COMPANY_CONTEXT.md (outside ATLAS)
   Lines: ~400-600
   Tokens: ~5K
   Time: 8 min (3 min if refresher)

7. LEARNINGS_LOG.md - RECENT RELEVANT ONLY
   Load: Last 10-15 entries in relevant domain
   Lines: ~800-1,200 (not entire file)
   Tokens: ~10K
   Time: 5 min
   Filter: Customer sites vs tools vs strategic

8. ATLAS_ASSUMPTIONS.md (if filled)
   Lines: ~200-300
   Tokens: ~3K
   Time: 3 min
   Skip if: Template only (not filled)

9. Existing research (if any)
   Variable - ask human
   Optional

TOTAL FILES: 8-10
TOTAL TOKENS: ~33K-40K
TIME: 25-40 min
```

**What AI1 SKIPS:**
- ❌ AI2 guide (not your role)
- ❌ AI3 guides (not your role)
- ❌ GIT_WORKFLOW.md (you don't implement)
- ❌ Developer best practices (you don't code)
- ❌ Templates (you use START_HERE template only)
- ❌ Other Steps from ATLAS_STEPS.md (load relevant Step only)
- ❌ Old LEARNINGS (only recent relevant)
- ❌ Other Efforts (not relevant)

---

## AI2 Planning Phase (Effort-Level)

**When:** START_HERE exists, guides don't exist (or incomplete)

**Load these files (in order):**

```
1. ATLAS_OVERVIEW.md (~3K tokens, 2 min skim)
2. ATLAS_GLOSSARY.md (~2K tokens, 1 min)

3. roles/AI2_GUIDE_CREATOR_GUIDE.md (~1,500 lines, ~16K tokens)
   Time: 5 min skim (15 min first time)

4. START_HERE.md (PRIMARY INPUT - deep read)
   File: efforts/STEP_X_Y/START_HERE.md
   Lines: ~800-1,500
   Tokens: ~12K
   Time: 15 min

5. steps/STEP_X.md - RELEVANT STEP FILE
   Load: Individual step file
   Tokens: ~3K
   Time: 3 min

6. Previous COMPLETION_SUMMARY (if exists)
   Tokens: ~7K
   Time: 8 min

7. COMPANY_CONTEXT.md (~5K tokens, 3 min)

8. LEARNINGS_LOG.md - RECENT RELEVANT
   Last 15-20 entries
   Tokens: ~12K
   Time: 6 min

9. DECISION_LOG.md - RECENT
   Last 10 entries
   Tokens: ~8K
   Time: 4 min

10-14. Templates (reference)
   - OUTLINE_TEMPLATE.md (~3K tokens)
   - OVERVIEW_GUIDE_TEMPLATE.md (~4K tokens)
   - TODO_TRACKER_TEMPLATE.md (~3K tokens)
   - CP_GUIDE_TEMPLATE.md (~5K tokens)
   - EFFORT_TEMPLATE.md (~3K tokens)
   Total: ~18K tokens
   Time: 10 min (skim all)

15. Previous similar Effort (optional)
    Files: effort.md, OUTLINE.md, one CP guide example
    Tokens: ~8K
    Time: 8 min
    Skip if: First Effort of this type

TOTAL FILES: 12-18
TOTAL TOKENS: ~60-75K (first CP guide)
TIME: 60-80 min first time

For subsequent CP guides (CP1, CP2, ...):
   Don't reload all context
   Just: START_HERE, current guide template, research sources
   Tokens: ~35-45K
   Time: 30-40 min per additional CP
```

**What AI2 SKIPS:**
- ❌ AI1 guide (not your role - you don't do AI1's job)
- ❌ AI3 implementation guide (not executing - planning only)
- ❌ Full ATLAS_STEPS.md (load relevant Step only)
- ❌ All LEARNINGS (recent only)
- ❌ All DECISIONS (recent only)
- ❌ Unrelated Efforts
- ❌ CP artifacts from old Efforts (read COMPLETION_SUMMARY instead)

---

## AI3 Execution Phase - CP0 (First Checkpoint)

**When:** All guides exist, TODO_TRACKER shows CP0 pending

**Load these files (in order):**

```
1. ATLAS_OVERVIEW.md (~3K tokens, 1 min skim)

2. roles/AI3_IMPLEMENTER_GUIDE.md (~1,200 lines, ~13K tokens)
   Time: 3 min skim (10 min first time)

3. roles/AI3_DEVELOPER_BEST_PRACTICES.md (~1,200 lines, ~14K tokens)
   Time: Reference only (20 min first time, then lookup sections)

4. roles/GIT_WORKFLOW.md (~650 lines, ~7K tokens)
   Time: Reference only (10 min first time, then lookup)

5. OVERVIEW_GUIDE.md (CRITICAL - read first)
   File: efforts/STEP_X_Y/OVERVIEW_GUIDE.md
   Lines: ~300-600
   Tokens: ~5K
   Time: 5 min

6. TODO_TRACKER.md
   Lines: ~200-500
   Tokens: ~4K
   Time: 2 min

7. START_HERE.md (context)
   Lines: ~800-1,500
   Tokens: ~12K
   Time: 10 min (skim - focus on outcomes and technical recommendations)

8. effort.md
   Lines: ~200-400
   Tokens: ~3K
   Time: 3 min

9. CP0_GUIDE.md (your instructions)
   File: efforts/STEP_X_Y/guides/CP0_GUIDE.md
   Lines: ~600-1,200
   Tokens: ~10K
   Time: 8 min

TOTAL FILES: 9
TOTAL TOKENS: ~61K (first time), ~45K (if familiar with system)
TIME: ~35 min skim, ~60 min first time
```

**What AI3 SKIPS (CP0):**
- ❌ AI1 guide (not your role)
- ❌ AI2 guide (not your role)
- ❌ ATLAS_STEPS.md (goal already in effort.md)
- ❌ LEARNINGS_LOG (not needed for execution - guides already incorporate learnings)
- ❌ DECISION_LOG (not needed - decisions already in guides)
- ❌ OUTLINE.md (redundant with OVERVIEW_GUIDE)
- ❌ Other CP guides (not current)
- ❌ Previous CP artifacts (none yet - this is CP0)

---

## AI3 Execution Phase - CP1+ (Subsequent Checkpoints)

**When:** CP0 complete, executing CP1, CP2, ..., CPX

**Load these files (lighter - you know the system):**

```
1. OVERVIEW_GUIDE.md (refresher)
   Tokens: ~5K
   Time: 2 min

2. TODO_TRACKER.md (progress state)
   Tokens: ~4K
   Time: 2 min

3. CPX_GUIDE.md (current checkpoint instructions)
   File: guides/CPX_GUIDE.md
   Tokens: ~10K
   Time: 8 min

4. Previous CP implementation notes
   File: artifacts/CP{X-1}_implementation_notes.md
   Tokens: ~4K
   Time: 5 min

TOTAL FILES: 4
TOTAL TOKENS: ~23K
TIME: ~15-20 min
```

**Additional files if needed (on-demand):**
- START_HERE.md (if need to reference research - 5 min)
- effort.md (if need to check success criteria - 2 min)
- Previous earlier CP notes (if building on CP{X-2} - 5 min)

**What AI3 SKIPS (CP1+):**
- ❌ Role guides (already read in CP0, know your job)
- ❌ ATLAS_OVERVIEW (already understand system)
- ❌ START_HERE (already read, unless need to reference)
- ❌ effort.md (already know goals, unless double-checking)
- ❌ Other CP guides (not current - read when you get to them)
- ❌ OUTLINE (redundant - you're executing, not planning)

---

## Loading Optimization Strategies

### **Strategy 1: Partial File Loading**

**ATLAS_STEPS.md** (can be 1,000+ lines after 6 months):
```
DON'T load entire file

DO load relevant section:
  Extract Step number from context (STEP_X_Y → Step X)
  Find "## STEP X:" in file
  Read that section (includes all Substeps X.1, X.2, etc.)
  Stop at "## STEP [X+1]:"

Example:
  Working on STEP_2_3
  Load: "## STEP 2: ..." section (200 lines)
  Skip: STEP 1, STEP 3+ (800 lines saved)

Token savings: 80% (2K vs 10K)
```

---

### **Strategy 2: Recency Filtering**

**LEARNINGS_LOG.md** (can be 5,000+ lines after 30 Efforts):
```
DON'T load entire file

DO load recent relevant entries:
  Read file in reverse (newest first)
  Take last 10-20 entries
  Filter by domain tags (customer vs tool vs strategic)
  Stop when you have enough context

Example:
  Working on internal tool (STEP_2_1)
  Load: Last 15 entries tagged "internal tool" or "technical"
  Skip: Customer site entries (different domain)
  Skip: Entries >3 months old (already incorporated into templates)

Token savings: 90% (10K vs 100K)
```

---

### **Strategy 3: Completion Summary Over Artifacts**

**Previous Effort artifacts** (could be 20 files, 10K+ lines):
```
DON'T read all artifacts from previous Effort

DO read COMPLETION_SUMMARY:
  Previous Effort: STEP_1_1
  Instead of reading:
    - START_HERE.md (1,200 lines)
    - OUTLINE.md (300 lines)
    - 5 CP guides (5,000 lines)
    - 5 CP implementation notes (2,500 lines)
    Total: 9,000 lines, ~90K tokens

  Just read:
    - COMPLETION_SUMMARY.md (800 lines, ~8K tokens)

Token savings: 91% (8K vs 90K)
```

**This is why COMPLETION_SUMMARY is critical.**

---

## Context Validation (Before Starting Work)

**AI should validate context load:**

**✓ Loaded all required files**
- [ ] Core ATLAS files (for system understanding)
- [ ] Role guide (for your responsibilities)
- [ ] Effort context (OVERVIEW_GUIDE or START_HERE)
- [ ] Current work instructions (CP guide or substep definition)
- [ ] Previous work (COMPLETION_SUMMARY or CP notes)

**✓ Skipped unnecessary files**
- [ ] Not loading other roles' guides
- [ ] Not loading entire ATLAS_STEPS (just relevant section)
- [ ] Not loading all LEARNINGS (just recent relevant)
- [ ] Not loading unrelated Efforts

**✓ Context size reasonable**
- [ ] File count: 8-25 files (not 30+)
- [ ] Token estimate: 25K-75K (not 100K+)
- [ ] Load time: 15-80 minutes (not hours)

**If validation fails:**
- Too many files (>25): Be more selective
- Too many tokens (>100K): Load partial files, recent entries only
- Missing required files: Add to load list

---

## Context Loading Matrix (Quick Reference)

| Phase | Files | Tokens | Time | Key Docs |
|-------|-------|--------|------|----------|
| AI1 Research | 8-12 | 33-40K | 25-40min | ATLAS_STEPS, COMPLETION_SUMMARY, COMPANY_CONTEXT |
| AI2 Planning (first CP) | 12-18 | 60-75K | 60-80min | START_HERE (primary), templates, LEARNINGS |
| AI2 Planning (per CP) | 6-10 | 35-45K | 30-40min | START_HERE, CP template, research sources |
| AI3 CP0 | 9 | 61K | 35-60min | OVERVIEW_GUIDE, TODO, CP0_GUIDE |
| AI3 CP1+ | 4 | 23K | 15-20min | OVERVIEW, TODO, CPX_GUIDE, prev notes |

---

## File Type Reference

**Per-Effort Files:**
- START_HERE.md (AI1's comprehensive research)
- OUTLINE.md (AI2's CP map)
- OVERVIEW_GUIDE.md (AI2's quick-start for AI3)
- guides/*.md (AI2's per-CP instructions)
- TODO_TRACKER.md (progress tracking)
- COMPLETION_SUMMARY.md (AI3's handoff)
- effort.md (Effort overview)
- artifacts/*.md (per-CP implementation notes)

**Strategy Files:**
- ATLAS_STEPS_TRACKER.md (high-level status)
- steps/STEP_X.md (individual step definitions)
- STEP_DEFINITION_GUIDE.md (how to write steps)
- LEARNINGS_LOG.md (discoveries)
- DECISION_LOG.md (strategic decisions)
- ATLAS_ASSUMPTIONS.md (constraints)

---

## Related Documentation

- ATLAS_ENTRY_POINT.md (uses these rules for auto-loading)
- ATLAS_SPECIFICATION.md (defines what each phase needs)
- Role guides (reference context loading sections)

---

**Load smart. Skip unnecessary. Context efficiency enables long-term work.** 🎯
