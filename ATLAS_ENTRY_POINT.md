# ATLAS Entry Point - The Usher System

**Purpose:** Route to correct mode based on human intent
**The Usher:** Intelligent orchestrator that finds state, refines strategy, answers questions
**Status:** v2.0 - 8-mode system

---

## What Is the Usher?

**The Usher is your ATLAS orchestrator.**

**Not just routing** - The Usher helps you:
- Find exactly where work stopped (auto-detection)
- Refine vague substeps (collaborative improvement)
- Extract learnings (weekly friction reducer)
- Document decisions (strategic capture)
- Check framework health (monthly diagnostics)
- Evolve templates (quarterly improvement)
- Understand ATLAS (framework AMA)

**8 modes. Each mode is a self-contained workflow in `/modes/` directory.**

---

## How to Invoke

**Simple (recommended):**
```
"Run ATLAS" or "Open ATLAS Usher"
```

**Usher presents 8-mode menu** (see below).

**You select mode** (1-8).

**Usher routes to that mode** (loads mode file, executes workflow).

---

**Direct (if you know mode):**
```
"Run ATLAS Mode 1" (auto-resume)
"Run ATLAS Mode 2" (refine substeps)
"Run ATLAS Mode 5" (capture learnings)
```

Usher goes directly to that mode.

---

## The 8 Modes

When you invoke ATLAS, Usher asks:

```
ATLAS Usher - Select Mode

What do you need?

1. Continue Work (Auto-Resume)
   → Find where we left off, continue from exact point
   → Usage: 85% (most common - daily execution)
   → Goes to: modes/MODE1_AUTO_RESUME.md

2. Refine Strategy (Collaborative Substep Improvement)
   → Work together to perfect substeps before AI1/AI2/AI3 execute
   → Usage: 5% (strategic refinement, mid-flight adjustments)
   → Goes to: modes/MODE2_REFINE_SUBSTEPS.md

3. Work on Specific Substep (Direct)
   → Skip scanning, go directly to STEP you specify
   → Usage: 8% (when you know exactly what to work on)
   → Goes to: modes/MODE3_DIRECT.md

4. Show Overview & Answer Questions (Status + AMA)
   → Display progress, explain framework, answer "how does X work?"
   → Usage: 2% (status checks, learning system, onboarding)
   → Goes to: modes/MODE4_OVERVIEW_AMA.md

5. Capture Learnings (Weekly Extract)
   → Extract strategic learnings from COMPLETION_SUMMARY → LEARNINGS_LOG
   → Usage: Weekly (Friday afternoon discipline)
   → Goes to: modes/MODE5_LEARNING_CAPTURE.md

6. Document Decision (Strategic Choice)
   → Format strategic decision for DECISION_LOG (alternatives, rationale)
   → Usage: As needed (1-3 times per month)
   → Goes to: modes/MODE6_DOCUMENT_DECISION.md

7. Health Check (Framework Diagnostics)
   → Run ATLAS_VALIDATION.md checklist, check framework health
   → Usage: Monthly or when something feels wrong
   → Goes to: modes/MODE7_HEALTH_CHECK.md

8. Evolve Templates (Quarterly Improvement)
   → Analyze patterns, improve framework based on learnings
   → Usage: Quarterly (after 10-15 Efforts)
   → Goes to: modes/MODE8_TEMPLATE_EVOLUTION.md

Enter number (1-8):
```

**Human selects mode → Usher loads that mode file → Workflow begins.**

---

## Mode Summaries (Quick Reference)

**Execution modes (daily/weekly):**
- **Mode 1:** Auto-resume (85% usage) - Continue work
- **Mode 3:** Direct (8% usage) - Go to specific substep

**Strategic modes (weekly/monthly):**
- **Mode 2:** Refine substeps (5% usage) - Collaborative improvement
- **Mode 5:** Learning capture (weekly) - Extract learnings
- **Mode 6:** Document decision (as needed) - Strategic choices

**Meta modes (monthly/quarterly):**
- **Mode 4:** Overview/AMA (2% usage) - Status + questions
- **Mode 7:** Health check (monthly) - Validate framework
- **Mode 8:** Template evolution (quarterly) - Improve framework

---

## Routing Logic

**After human selects mode:**

```
If mode = 1:
  Load: modes/MODE1_AUTO_RESUME.md
  Execute: Auto-detection algorithm
  Result: Continue work from exact point

If mode = 2:
  Load: modes/MODE2_REFINE_SUBSTEPS.md
  Execute: Collaborative refinement
  Result: Updated ATLAS_STEPS with refined substep

If mode = 3:
  Ask: "Which substep?" (STEP_X_Y)
  Load: modes/MODE3_DIRECT.md
  Reference: MODE1 (same workflow, skip scanning)
  Result: Continue specified substep

If mode = 4:
  Load: modes/MODE4_OVERVIEW_AMA.md
  Execute: Status display + Q&A
  Result: Overview shown, questions answered

If mode = 5:
  Ask: "Which Effort to extract learnings from?" (recently completed)
  Load: modes/MODE5_LEARNING_CAPTURE.md
  Execute: Extract + format learnings
  Result: LEARNINGS_LOG.md updated

If mode = 6:
  Ask: "What decision to document?"
  Load: modes/MODE6_DOCUMENT_DECISION.md
  Execute: Interview + format decision
  Result: DECISION_LOG.md updated

If mode = 7:
  Load: modes/MODE7_HEALTH_CHECK.md
  Execute: Run ATLAS_VALIDATION.md checks
  Result: Health report (✅ healthy, ⚠️ issues, ❌ critical)

If mode = 8:
  Load: modes/MODE8_TEMPLATE_EVOLUTION.md
  Load: guides/TEMPLATE_EVOLUTION_GUIDE.md (meta-guide)
  Execute: Pattern analysis + template updates
  Result: Templates evolved, framework improved
```

**Each mode file is self-contained** (includes workflow, file loading, outputs).

---

## Shared Utilities (Used by Multiple Modes)

### File Scanning Functions

**Function: Find Active Efforts**
```bash
find /ATLAS3/efforts/ -name "effort.md" -exec grep -l "Status: IN_PROGRESS\|Status: 🔄" {} \;
```

**Function: Check File Exists**
```bash
file_exists() {
  ls "$1" 2>/dev/null && echo "exists" || echo "missing"
}
```

**Function: Extract Status**
```bash
get_status() {
  grep "Status:" "$1" | head -1 | awk '{print $2}'
}
```

**These utilities are called by mode workflows.**

---

## Error Handling (Shared)

### Error: Mode Not Found
```
Invalid mode: X

Valid modes: 1-8
Please enter a number between 1 and 8.
```

### Error: Required Files Missing
```
Error: ATLAS3 not properly configured

Missing files:
- strategy/ATLAS_STEPS_PART1.md (required)
- templates/START_HERE_TEMPLATE.md (required)

Run ATLAS Mode 7 (Health Check) to diagnose.

Or see: ONBOARDING.md for setup instructions.
```

### Error: No Active Work (Mode 1)
```
No active Efforts found.

Checked:
- All effort.md files
- None have Status: IN_PROGRESS

Options:
1. Check ATLAS_STEPS (what's next to start?)
2. Review completed work (Mode 4 - Overview)
3. Start new substep (specify STEP_X_Y)

What would you like?
```

---

## Context Loading Per Mode (Summary)

**Mode 1:** 8-12 files (~35K tokens) - Execution context
**Mode 2:** 12-18 files (~77K tokens) - Strategy context
**Mode 3:** Same as Mode 1 (references it)
**Mode 4:** 15-25 files (~75K tokens) - All strategy + Effort status
**Mode 5:** 4 files (~29K tokens) - COMPLETION_SUMMARY + LEARNINGS_LOG
**Mode 6:** 2-4 files (~20K tokens) - DECISION_LOG + context
**Mode 7:** 10-15 files (~71K tokens) - Validation + scans
**Mode 8:** 20-30 files (~222K tokens, heavy - batch if needed)

**All modes manageable except Mode 8** (quarterly, can batch analysis).

---

## Strategy Structure

**Framework uses individual step files:**

```
/ATLAS3/strategy/
├── ATLAS_STEPS_TRACKER.md     # High-level status of all steps
├── STEP_DEFINITION_GUIDE.md   # How to write step definitions
├── steps/                     # Individual step files
│   ├── STEP_TEMPLATE.md       # Template for new steps
│   ├── STEP_1.md              # Step 1 definition (HOD creates)
│   ├── STEP_2.md              # Step 2 definition
│   └── ...
├── DECISION_LOG.md
├── LEARNINGS_LOG.md
└── ATLAS_ASSUMPTIONS.md
```

**Why individual files:**
- Each Step is its own file (easy to find, edit, load)
- Tracker provides high-level overview
- AI loads relevant step file only (STEP_1.md for STEP_1_X)
- Scales cleanly (Step 10 doesn't bloat Step 1)

**Status tracking:**
- ATLAS_STEPS_TRACKER.md shows overall progress
- Each STEP_X.md contains substep status
- Usher scans tracker + relevant step file

**Dependencies maintained:**
- Step files can reference each other
- Tracker shows dependency chain

---

## Progress Tracking (Where Status Lives)

**Step/Substep status:**
- Lives in: steps/STEP_X.md files + ATLAS_STEPS_TRACKER.md
- Updated by: AI3 (when substep completes), Mode 2 (when refining), human (strategic changes)
- Format: ✅ COMPLETE, 🔄 IN_PROGRESS, ⏸️ PLANNED

**AI phase status:**
- Detected from: File existence (START_HERE, OUTLINE, guides, TODO_TRACKER)
- Not stored: Detection is algorithmic (scan files, determine phase)
- Why: Files ARE the state (can't get out of sync)

**CP progress status:**
- Lives in: TODO_TRACKER.md (per Effort)
- Updated by: AI3 (after each CP)
- Format: ✅ COMPLETE, 🔄 IN_PROGRESS, ⏸️ PENDING

**Three-level tracking (all tied together):**
1. steps/STEP_X.md + ATLAS_STEPS_TRACKER.md → Which substeps done
2. File existence → Which AI phase
3. TODO_TRACKER.md → Which CPs done

**Usher scans all three → Knows exact state.**

---

## Philosophy

**The Usher is your intelligent partner:**

**Not just:** "Run this command" (dumb router)

**But:** "Find state, refine strategy, capture learnings, improve framework, answer questions"

**Modes enable:**
- **Execution** (Mode 1, 3) - Get work done
- **Strategy** (Mode 2) - Keep aligned with reality
- **Learning** (Mode 5, 6) - Capture knowledge
- **Quality** (Mode 7, 8) - Maintain and improve system
- **Understanding** (Mode 4) - Know where you are, how system works

**Usher makes ATLAS3 usable for building billion-dollar companies.**

---

## Related Documentation

**Mode files:**
- modes/MODE1_AUTO_RESUME.md - Continue work (most used)
- modes/MODE2_REFINE_SUBSTEPS.md - Strategy improvement
- modes/MODE3_DIRECT.md - Direct to substep
- modes/MODE4_OVERVIEW_AMA.md - Status + framework questions
- modes/MODE5_LEARNING_CAPTURE.md - Weekly extract
- modes/MODE6_DOCUMENT_DECISION.md - Strategic choices
- modes/MODE7_HEALTH_CHECK.md - Monthly diagnostics
- modes/MODE8_TEMPLATE_EVOLUTION.md - Quarterly improvement

**Supporting docs:**
- ATLAS_OVERVIEW.md - System explanation
- ATLAS_SPECIFICATION.md - Technical details
- ATLAS_VALIDATION.md - Health check reference
- context/CONTEXT_INDEX.md - File loading rules

---

## Quick Start

**First time using ATLAS:**
```
"Run ATLAS"
Select: Mode 4 (Overview) - Understand system
Then: Mode 1 (Auto-Resume) - Start working
```

**Daily usage:**
```
"Run ATLAS"
Select: Mode 1 (Auto-Resume)
[Usher finds state, continues work]
```

**Weekly:**
```
Friday: Mode 5 (Learning Capture) - Extract from completed Effort
```

**Monthly:**
```
Mode 7 (Health Check) - Validate framework
```

**Quarterly:**
```
Mode 2 (Refine Strategy) - Update Steps based on learnings
Mode 8 (Template Evolution) - Improve framework
```

---

**The Usher orchestrates everything. Trust the modes. Build systematically.** 🎯
