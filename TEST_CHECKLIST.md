# ATLAS3 Test Checklist - Validation Before Use

**Purpose:** Systematic validation of ATLAS3 build
**How:** Spin up fresh Claude, test each critical path
**Time:** 30-60 minutes total testing

---

## Pre-Test: File Structure Validation

**Run these commands:**

```bash
# 1. Count total files
find /Users/rsmith/Projects/ATLAS3 -type f -name "*.md" | wc -l
# Expected: 37 files

# 2. Verify all 8 modes exist
ls /Users/rsmith/Projects/ATLAS3/modes/
# Expected: MODE1-MODE8.md (8 files)

# 3. Verify all templates exist
ls /Users/rsmith/Projects/ATLAS3/templates/
# Expected: 7 template files

# 4. Verify all role guides exist
ls /Users/rsmith/Projects/ATLAS3/roles/
# Expected: 5 role guides

# 5. Check partitioned STEPS pattern documented
grep -l "ATLAS_STEPS_PART" /Users/rsmith/Projects/ATLAS3/ATLAS_ENTRY_POINT.md
# Expected: File path returned (pattern is documented)
```

**✅ If all pass:** File structure is correct, proceed to functional tests

---

## Test 1: Entry Point Menu Works

**Spin up fresh Claude:**
```
Point Claude to: /Users/rsmith/Projects/ATLAS3/ATLAS_ENTRY_POINT.md

Say: "Read this file and present the Usher menu"
```

**Expected behavior:**
- Claude reads entry point
- Presents 8-mode menu (Mode 1-8 with descriptions)
- Asks: "Enter number (1-8):"

**✅ Pass if:** Menu is clear, 8 modes listed, asks for selection

**❌ Fail if:** No menu presented, wrong number of modes, confusing presentation

---

## Test 2: Mode 1 (Auto-Resume) - File Loading

**Say to Claude:**
```
"Select Mode 1 (Auto-Resume)

Pretend we're working on STEP_0_2_PAYMENT_SYSTEM which is IN_PROGRESS.

What files would you load for AI3 executing CP3?"
```

**Expected behavior:**
- Claude loads MODE1_AUTO_RESUME.md
- Follows Workflow E (AI3 Execution)
- Lists files for CP3 (not CP0):
  1. OVERVIEW_GUIDE.md
  2. TODO_TRACKER.md
  3. CP3_GUIDE.md
  4. CP2_implementation_notes.md

**✅ Pass if:** Lists 4 files, correct files, explains why each

**❌ Fail if:** Lists 20 files, wrong files, or can't determine what to load

---

## Test 3: Mode 2 (Refine Substeps) - Collaborative Flow

**Say to Claude:**
```
"Select Mode 2 (Refine Substeps)

We need to make STEP_0_3 (Notification Service) more specific.

Walk me through the refinement process."
```

**Expected behavior:**
- Claude loads MODE2_REFINE_SUBSTEPS.md
- Loads context (ATLAS_STEPS files, LEARNINGS, DECISIONS)
- Asks questions to make substep specific:
  - What exactly is Notification Service?
  - What are deliverables?
  - What are success criteria?
  - How should it be broken into substeps?
- Drafts updated substep definition
- Asks for approval

**✅ Pass if:** Collaborative Q&A, helps structure thinking, produces specific output

**❌ Fail if:** Just asks what to write (not collaborative), or produces vague output

---

## Test 4: Mode 5 (Learning Capture) - Extraction

**Say to Claude:**
```
"Select Mode 5 (Learning Capture)

Extract learnings from a hypothetical COMPLETION_SUMMARY that says:
- Async webhook processing was 8x faster than synchronous
- Diverse scenario testing caught 3D Secure edge cases
- Reusing Supabase saved 2 hours

Draft learning entries."
```

**Expected behavior:**
- Claude loads MODE5_LEARNING_CAPTURE.md
- Drafts 3 learning entries in proper format:
  - Context, Discovery, Evidence, Implications, Actions
- Each entry is specific (not vague)
- Asks for review/approval

**✅ Pass if:** Drafts 3 entries, proper format, extracts strategic implications

**❌ Fail if:** Vague entries, wrong format, doesn't extract implications

---

## Test 5: Auto-Detection Logic

**Say to Claude:**
```
"We have an Effort at /efforts/STEP_0_2_PAYMENT_SYSTEM/ with:
- START_HERE.md exists
- OUTLINE.md exists
- 5 guides exist (CP0-CP4)
- TODO_TRACKER.md exists
- TODO_TRACKER shows: CP0-2 complete ✅, CP3 pending ⏸️

What phase are we in? What's next?"
```

**Expected behavior:**
- Claude analyzes file existence
- Detects: AI3 phase (all guides exist)
- Reads TODO_TRACKER: CP3 is next
- States: "AI3 execution phase, execute CP3 (Webhook Processing)"
- Lists files to load for CP3

**✅ Pass if:** Correct detection, identifies CP3, knows what to load

**❌ Fail if:** Wrong phase detected, can't determine current CP, unclear what to load

---

## Test 6: Progress Tracking Clarity

**Say to Claude:**
```
"Explain where progress is tracked in ATLAS3.

Where does Step/Substep status live?
Where does CP progress live?
How is AI phase detected?
Who updates what and when?"
```

**Expected behavior:**
- Claude explains three-level tracking:
  1. ATLAS_STEPS_PARTX.md (Step/Substep status)
  2. File existence (AI phase - algorithmic)
  3. TODO_TRACKER.md (CP progress)
- Explains who updates:
  - AI3 updates TODO_TRACKER (after each CP)
  - AI3 updates ATLAS_STEPS (when substep complete)
  - File creation IS the update for AI phase

**✅ Pass if:** Clear explanation, all three levels covered, ownership clear

**❌ Fail if:** Confused about where status lives, can't explain who updates what

---

## Test 7: Handoff Documents

**Say to Claude:**
```
"What's the handoff document from AI1 to AI2?
What's the handoff from AI2 to AI3?
What's the handoff from AI3 to next substep?"
```

**Expected behavior:**
- AI1 → AI2: START_HERE.md
- AI2 → AI3: OVERVIEW_GUIDE.md + TODO_TRACKER.md + guides/
- AI3 → Next AI1: COMPLETION_SUMMARY.md

**✅ Pass if:** Identifies all three handoffs, explains purpose of each

**❌ Fail if:** Confused about handoffs, missing documents, unclear flow

---

## Test 8: File Ownership

**Say to Claude:**
```
"Who creates TODO_TRACKER.md?
Who updates it?
Who reads it?
When is it created?
When is it updated?"
```

**Expected behavior:**
- Created by: AI2 (during planning phase, after guides)
- Updated by: AI3 (after each CP completion)
- Read by: AI3 (resume state), Framework (auto-detection), Human (status)
- Created: During AI2 phase (last task)
- Updated: After each CP (AI3 marks complete, adds notes)

**✅ Pass if:** All ownership clear, timing clear, purpose clear

**❌ Fail if:** Ambiguous about who does what, unclear when updates happen

---

## Test 9: Mode Router Efficiency

**Check context loading:**
```
Ask Claude:
"If I run Mode 1, how many lines of documentation do you load?
If I run Mode 5, how many lines?"
```

**Expected:**
- Mode 1: Entry point (390 lines) + MODE1 (209 lines) = ~600 lines
- Mode 5: Entry point (390 lines) + MODE5 (205 lines) = ~595 lines

**✅ Pass if:** Under 700 lines per mode (efficient)

**❌ Fail if:** Loading 2,000+ lines (modes are leaking into each other)

---

## Test 10: Workflow Correctness

**Say to Claude:**
```
"Describe the complete workflow for a substep:
- What does AI1 do?
- What does AI2 do?
- What does AI3 do?
- How do they hand off?"
```

**Expected (correct workflow):**
```
AI1 Phase:
- Researches entire substep
- Produces START_HERE.md
- Completion marker: START_HERE exists

AI2 Phase:
- Reads START_HERE, validates
- Creates OUTLINE (decides CP count 3-10)
- Researches each CP individually
- Creates CP guides (one per CP)
- Creates OVERVIEW_GUIDE, TODO_TRACKER, effort.md
- Completion marker: All guides + TODO_TRACKER exist

AI3 Phase:
- Executes CP0 (setup) → updates TODO_TRACKER
- Executes CP1 (implementation) → updates TODO
- Continues for all CPs
- Final CP: Testing, COMPLETION_SUMMARY, update ATLAS_STEPS
- Completion marker: COMPLETION_SUMMARY exists, PR created

Handoffs:
- AI1 → AI2: START_HERE.md
- AI2 → AI3: Guides + TODO_TRACKER
- AI3 → Next AI1: COMPLETION_SUMMARY.md
```

**✅ Pass if:** Matches this workflow exactly

**❌ Fail if:** Says "AI1 executes CP0" or "AI2 doesn't research" or missing steps

---

## Validation Summary

**Run all 10 tests with fresh Claude.**

**Results:**
- [ ] Test 1: Entry point menu ✅/❌
- [ ] Test 2: Mode 1 file loading ✅/❌
- [ ] Test 3: Mode 2 collaboration ✅/❌
- [ ] Test 4: Mode 5 extraction ✅/❌
- [ ] Test 5: Auto-detection ✅/❌
- [ ] Test 6: Progress tracking ✅/❌
- [ ] Test 7: Handoffs ✅/❌
- [ ] Test 8: File ownership ✅/❌
- [ ] Test 9: Context efficiency ✅/❌
- [ ] Test 10: Workflow correctness ✅/❌

**If 10/10 pass:** ✅ ATLAS3 is correct and ready for production

**If 8-9/10 pass:** ⚠️ Minor issues, fix and retest

**If <8/10 pass:** ❌ Major issues, review failed tests, fix root causes

---

## Quick Automated Checks

**Before spinning up Claude, run these:**

```bash
# All modes have workflows
for i in 1 2 3 4 5 6 7 8; do
  echo "MODE$i workflow sections:"
  grep -c "^##.*Workflow\|^##.*Step\|^##.*Process" /Users/rsmith/Projects/ATLAS3/modes/MODE${i}*.md
done
# Each should have workflow sections (>2)

# All templates have instructions
for t in START_HERE OUTLINE OVERVIEW_GUIDE TODO_TRACKER COMPLETION_SUMMARY CP_GUIDE EFFORT; do
  echo "$t template has instructions:"
  grep -c "Instructions" /Users/rsmith/Projects/ATLAS3/templates/${t}*.md
done
# Each should have 1 (instructions section)

# Role guides reference correct files
grep -c "START_HERE\|OUTLINE\|TODO_TRACKER" /Users/rsmith/Projects/ATLAS3/roles/AI*.md
# Should be high (guides reference new file types)

# Specification is comprehensive
wc -l /Users/rsmith/Projects/ATLAS3/ATLAS_SPECIFICATION.md
# Should be ~1,000+ lines (comprehensive spec)
```

**If automated checks pass:** Structure is solid, proceed to Claude tests

---

## Next Steps After Validation

**If tests pass:**
1. Mark ATLAS3 as validated (update BUILD_COMPLETE.md)
2. Create your company strategy files (ATLAS_STEPS_TRACKER.md + steps/STEP_X.md)
3. Run Mode 1 (start first substep for your company)

**If tests fail:**
1. Document failures (which tests, what went wrong)
2. Fix issues (update files)
3. Retest (verify fixes work)
4. Repeat until 10/10 pass

---

**Test systematically. Validate before using for real company. Measure thrice.**
