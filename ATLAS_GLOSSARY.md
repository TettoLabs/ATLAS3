# ATLAS Glossary - Quick Terminology Reference

**Purpose:** Single source of truth for ATLAS terminology
**Audience:** All users (quick lookup during work)
**Status:** v2.0
**Use:** Keep open for reference while working

---

## Core Concepts (Hierarchical)

### **Step**
Strategic milestone. What must become true for company to advance.

- **Size:** Months typically
- **Example:** "Build Platform Foundation" (3 months, contains 3 substeps)
- **Defined in:** ATLAS_STEPS.md
- **Contains:** Substeps (if large)

---

### **Substep**
Execution unit within Step. One substep = one Effort.

- **Naming:** STEP_X_Y (e.g., STEP_1_2)
- **Size:** 1-4 weeks typically
- **Example:** STEP_1_2: Build Site Cloner (2 weeks)
- **Becomes:** One Effort (STEP_1_2_SITE_CLONER)

---

### **Effort**
The work package that AI1/AI2/AI3 execute to accomplish a substep.

- **Size:** 1-4 weeks (same as substep)
- **Maps to:** One substep (1:1 relationship)
- **Contains:** START_HERE, OUTLINE, guides, TODO_TRACKER, artifacts, COMPLETION_SUMMARY
- **Naming:** STEP_X_Y_SHORTNAME (e.g., STEP_1_2_SITE_CLONER)

---

### **Checkpoint (CP)**
Phase within Effort execution. AI3 executes these sequentially.

- **Naming:** CP0, CP1, CP2, ..., CPX
- **Count:** Variable (3-10, AI2 decides)
- **Types:**
  - CP0: Always setup/infrastructure
  - CP1-CPX-1: Implementation phases
  - CPX (last): Always testing/deployment
- **Executed by:** AI3 only

---

## AI Phases (NOT Checkpoint Roles)

### **AI1 Phase**
Research entire substep, produce START_HERE.md.

- **When:** Before Effort exists
- **Input:** Substep from ATLAS_STEPS.md
- **Output:** START_HERE.md (comprehensive research)
- **Duration:** 6-12 hours (varies by substep specificity)
- **Research:** 80%
- **Completion marker:** START_HERE.md exists

---

### **AI2 Phase**
Validate research, create execution guides.

- **When:** After START_HERE exists, before AI3 execution
- **Input:** START_HERE.md from AI1
- **Output:** OUTLINE, all CP guides, OVERVIEW_GUIDE, TODO_TRACKER
- **Duration:** 8-15 hours (varies by CP count)
- **Research:** 50% (validates AI1, researches each CP)
- **Completion marker:** All guides + TODO_TRACKER exist

---

### **AI3 Phase**
Execute all checkpoints, produce working deliverables.

- **When:** After all guides exist
- **Input:** Guides from AI2, TODO_TRACKER
- **Output:** Working code, COMPLETION_SUMMARY, updated progress
- **Duration:** 1-4 weeks (varies by Effort scope)
- **Research:** 20% (spot-checks, sanity validation)
- **Completion marker:** COMPLETION_SUMMARY exists, PR created

---

## Key Documents (File Types)

### **START_HERE.md**
AI1's comprehensive research document.

- **Created by:** AI1 (research phase)
- **Updated by:** Never (static)
- **Read by:** AI2 (primary input), AI3 (context)
- **Purpose:** Give AI2 everything needed for perfect planning
- **Location:** `/efforts/STEP_X_Y_[NAME]/START_HERE.md`
- **Length:** 800-1,500 lines

---

### **OUTLINE.md**
AI2's high-level checkpoint map.

- **Created by:** AI2 (after reading START_HERE)
- **Updated by:** AI2 (rarely, if CP count changes)
- **Read by:** AI3 (understand sequence), Human (approve plan)
- **Purpose:** Show all CPs at a glance before detailed guides
- **Location:** `/efforts/STEP_X_Y_[NAME]/OUTLINE.md`
- **Length:** 200-400 lines

---

### **OVERVIEW_GUIDE.md**
AI2's quick-start guide for Effort.

- **Created by:** AI2 (after creating all guides)
- **Updated by:** Rarely
- **Read by:** AI3 (first thing when starting Effort)
- **Purpose:** Get AI3 up to speed in 5 minutes
- **Location:** `/efforts/STEP_X_Y_[NAME]/OVERVIEW_GUIDE.md`
- **Length:** 300-600 lines

---

### **CPX_GUIDE.md**
AI2's detailed instructions for one checkpoint.

- **Created by:** AI2 (one per CP, after researching that CP)
- **Updated by:** Rarely
- **Read by:** AI3 (when executing that CP)
- **Purpose:** Exact step-by-step instructions
- **Location:** `/efforts/STEP_X_Y_[NAME]/guides/CPX_GUIDE.md`
- **Length:** 600-1,200 lines per guide
- **Count:** Variable (3-10 guides per Effort)

---

### **TODO_TRACKER.md**
CP-level progress tracking document.

- **Created by:** AI2 (initial template, all PENDING)
- **Updated by:** AI3 (after each CP completion)
- **Read by:** AI3 (resume state), Framework (auto-detection), Human (status)
- **Purpose:** Track which CPs done, enable resume
- **Location:** `/efforts/STEP_X_Y_[NAME]/TODO_TRACKER.md`
- **Length:** 200-500 lines
- **Format:** Markdown checklist with status markers (✅🔄⏸️)

---

### **COMPLETION_SUMMARY.md**
AI3's final handoff document.

- **Created by:** AI3 (last task in final CP)
- **Updated by:** Never
- **Read by:** Next substep's AI1, AI2, Human
- **Purpose:** Efficient handoff (don't re-read all artifacts)
- **Location:** `/efforts/STEP_X_Y_[NAME]/COMPLETION_SUMMARY.md`
- **Length:** 500-1,000 lines

---

### **ATLAS_STEPS.md**
Master strategy document with all Steps and Substeps.

- **Created by:** Human or AI2 (strategic mode)
- **Updated by:** AI3 (substep completion status), AI2 (strategy evolution quarterly)
- **Read by:** AI1 (substep definition), AI2 (planning context), AI3 (strategic context)
- **Purpose:** Strategic roadmap
- **Location:** `/ATLAS3/strategy/ATLAS_STEPS.md`
- **Length:** 500-2,000 lines (grows over time)

---

### **LEARNINGS_LOG.md**
Strategic learnings from execution.

- **Created by:** Framework (empty template)
- **Updated by:** Human (extracts from COMPLETION_SUMMARY), AI2 (strategic mode)
- **Read by:** AI1 (before research), AI2 (before planning), AI2 strategic (quarterly review)
- **Purpose:** Capture discoveries for future application
- **Location:** `/ATLAS3/strategy/LEARNINGS_LOG.md`
- **Format:** Dated entries with context, discovery, evidence, implications

---

### **DECISION_LOG.md**
Strategic decisions with rationale.

- **Created by:** Framework (empty template)
- **Updated by:** Human (strategic choices), AI2 (if AI makes strategic decision)
- **Read by:** AI1 (understand past), AI2 (planning/strategic mode)
- **Purpose:** Document strategic decisions (don't re-litigate)
- **Location:** `/ATLAS3/strategy/DECISION_LOG.md`
- **Format:** Dated entries with decision, alternatives, rationale, trade-offs

---

## Checkpoint Types

### **CP0**
Setup/infrastructure checkpoint. Always first.

- **Purpose:** Prepare technical foundation
- **Tasks:** Git init, Vercel project, database setup, environment config, dependencies
- **Role:** AI3 (implementer, not AI1)
- **Duration:** 2-6 hours
- **Output:** Infrastructure ready for CP1+ to build on

---

### **CP1-CPX-1**
Implementation checkpoints. Variable count.

- **Purpose:** Build features, integrate services, create functionality
- **Count:** 1-8 CPs (AI2 decides based on Effort complexity)
- **Role:** AI3 (implementer)
- **Each CP:**
  - Builds subset of features
  - Tests after completion
  - Updates TODO_TRACKER
  - Merges to staging

---

### **CPX (Final)**
Testing and deployment checkpoint. Always last.

- **Purpose:** Comprehensive quality gate and production launch
- **Tasks:** Full testing, staging validation, PR creation, COMPLETION_SUMMARY, status updates
- **Role:** AI3 + Human (AI3 prepares, Human approves PR)
- **Duration:** 1-2 days
- **Output:** Production deployment, COMPLETION_SUMMARY, updated ATLAS_STEPS.md

---

## Progress States

### **Step Status**
- **PLANNED:** Defined, not started
- **IN_PROGRESS:** One or more substeps executing
- **COMPLETE:** All substeps done
- **ON_HOLD:** Temporarily paused

---

### **Substep/Effort Status**
- **PLANNED:** AI1 hasn't started research yet
- **AI1_RESEARCH:** AI1 creating START_HERE
- **AI2_PLANNING:** AI2 creating guides
- **IN_PROGRESS:** AI3 executing CPs
- **COMPLETE:** All CPs done, PR merged

---

### **CP Status** (in TODO_TRACKER.md)
- **⏸️ PENDING:** Not started
- **🔄 IN_PROGRESS:** Currently executing
- **✅ COMPLETE:** Finished and validated

---

## File Locations

```
/ATLAS3/                             # Framework (generic)
├── [core files]                     # README, OVERVIEW, etc.
├── roles/                           # AI guides
├── templates/                       # File templates
├── strategy/                        # Strategy templates
└── context/                         # Context loading rules

/COMPANY_CONTEXT.md                  # Vision (outside ATLAS)

/ATLAS3/strategy/
├── ATLAS_STEPS.md                   # Your strategy (you fill)
├── ATLAS_ASSUMPTIONS.md             # Your constraints (optional)
├── LEARNINGS_LOG.md                 # Discoveries (fills during execution)
└── DECISION_LOG.md                  # Decisions (fills during execution)

/efforts/STEP_X_Y_[NAME]/            # Effort directory
├── START_HERE.md                    # AI1 creates
├── OUTLINE.md                       # AI2 creates
├── OVERVIEW_GUIDE.md                # AI2 creates
├── TODO_TRACKER.md                  # AI2 creates, AI3 updates
├── COMPLETION_SUMMARY.md            # AI3 creates
├── effort.md                        # AI2 creates
├── guides/                          # AI2 creates all
│   ├── CP0_GUIDE.md
│   └── ...
└── artifacts/                       # AI3 creates during execution
    ├── CP0_setup_notes.md
    └── ...
```

---

## Common Terms

**Artifact:** Output file (research summary, code, notes, documentation)

**Context loading:** Process of determining which files to read (smart loading = only relevant files)

**Handoff:** Transition between AI phases (via artifact documents)

**Completion marker:** File whose existence indicates phase is done (START_HERE → AI1 done)

**Auto-detection:** Framework determines current phase/CP from file existence (no manual tracking)

**Research distribution:** 80% AI1, 50% AI2, 20% AI3 (tapers as work progresses)

---

## Abbreviations

- **CP:** Checkpoint
- **CPX:** Last checkpoint (variable number, X represents final)
- **AI1:** Researcher role
- **AI2:** Guide Creator / Planner role
- **AI3:** Implementer / Developer role

---

## Key Relationships

```
Strategy Layer:
  Step → contains Substeps
  Substep → becomes one Effort

Execution Layer:
  Effort → has Checkpoints (3-10)
  Checkpoint → executed by AI3
  Checkpoint → produces Artifacts

AI Workflow:
  AI1 Phase → produces START_HERE
  AI2 Phase → produces Guides + TODO_TRACKER
  AI3 Phase → executes all Checkpoints
  COMPLETION_SUMMARY → feeds next Effort

Progress Tracking:
  ATLAS_STEPS.md → Step/Substep status
  File existence → AI phase status
  TODO_TRACKER.md → CP status
```

---

## Important Distinctions

### **Step vs. Substep**
- **Step:** Strategic (months) - "Build platform tools"
- **Substep:** Tactical (weeks) - "Build audit engine"
- **Relationship:** Step contains multiple Substeps

### **Substep vs. Effort**
- **Substep:** Definition in ATLAS_STEPS.md (what to build)
- **Effort:** Execution package (how it gets built)
- **Relationship:** One substep → one Effort directory

### **AI Phase vs. Checkpoint**
- **AI Phase:** Research (AI1) / Planning (AI2) / Execution (AI3)
- **Checkpoint:** CP0, CP1, ... (only during AI3 phase)
- **Relationship:** AI phases are sequential, CPs are within AI3 phase

### **OUTLINE vs. OVERVIEW_GUIDE**
- **OUTLINE:** High-level CP map (before detailed guides)
- **OVERVIEW_GUIDE:** Quick-start for execution (after guides created)
- **Both created by:** AI2
- **Difference:** OUTLINE is planning doc, OVERVIEW_GUIDE is execution doc

### **Artifact vs. Deliverable**
- **Artifact:** Any file output (docs, notes, summaries)
- **Deliverable:** Final working product (code, site, tool)
- **Relationship:** Artifacts include deliverables + documentation

---

## Usage Examples

**Referring to a Step:**
> "Working on Step 1: Build Platform Foundation"

**Referring to a Substep:**
> "Currently executing Substep 1.2 (STEP_1_2)"

**Referring to an Effort:**
> "Effort STEP_1_2_SITE_CLONER is in progress"

**Referring to AI phase:**
> "AI1 has completed research for STEP_1_2"
> "AI2 is creating guides"
> "AI3 is executing CP3"

**Referring to a Checkpoint:**
> "AI3 completed CP2, starting CP3"

**Referring to progress:**
> "TODO_TRACKER shows CP0-2 complete, CP3 in progress"

---

## Quick Reference Card

| Term | Duration | Who Creates | Example |
|------|----------|-------------|---------|
| Step | Months | Human/AI2 | "Build Platform Foundation" |
| Substep | Weeks | Human/AI2 | STEP_1_2 |
| Effort | Weeks | AI1/AI2/AI3 | STEP_1_2_SITE_CLONER |
| Checkpoint | Hours-Days | AI2 plans, AI3 executes | CP0, CP1, CP2 |
| START_HERE | N/A | AI1 | START_HERE.md |
| Guide | N/A | AI2 | CP1_GUIDE.md |
| TODO_TRACKER | N/A | AI2/AI3 | TODO_TRACKER.md |

---

## Related Documentation

- **ATLAS_OVERVIEW.md** - Complete system explanation
- **ATLAS_SPECIFICATION.md** - Technical workflow details
- **Role guides** - What each AI does
- **Templates** - File structures and formats

---

**Keep this open for quick reference while working with ATLAS.** 📖
