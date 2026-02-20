# ATLAS v3.0 - Complete System Overview

**Purpose:** Comprehensive explanation of ATLAS orchestration system
**Audience:** Everyone using ATLAS (founders, AIs, team members)
**Status:** Master documentation - read this first
**Version:** 3.0

---

## What ATLAS Is

ATLAS is a **state-driven orchestration framework** that turns company vision into systematic execution through three sequential AI phases.

**ATLAS is NOT:**
- A project management tool (Jira, Linear)
- An AI agent that "thinks" and decides
- Specific to any one company or technology

**ATLAS IS:**
- A routing and workflow system for AI cognition
- A state machine encoded in markdown files
- A systematic approach to company building (execution determines outcomes)
- A knowledge compounding engine (with the potential for 2-4x efficiency gains over 20+ efforts)

---

## The Core Problem ATLAS Solves

**Building a company requires:**
1. Research (understand market, validate assumptions, evaluate options)
2. Planning (break work into executable phases, create detailed guides)
3. Execution (build things precisely, maintain quality, track progress)
4. Learning (capture discoveries, feed back to strategy, compound knowledge)

**Most approaches fail because:**
- Research and execution blur (start coding before understanding problem)
- Planning is vague (no detailed guides, AIs guess and make mistakes)
- Progress is lost (work pauses, can't resume precisely)
- Learning disappears (discoveries lost in chat history, same mistakes repeated)
- Context explodes (trying to load everything, hit AI context limits)

**ATLAS solves this through:**
- **Clear phase separation** (AI1 researches, AI2 plans, AI3 implements - no blur)
- **Detailed guides** (AI2 creates step-by-step instructions, AI3 executes mechanically)
- **Exact progress tracking** (TODO_TRACKER shows which CP is done, can resume anywhere)
- **Explicit learning capture** (COMPLETION_SUMMARY → next Effort, LEARNINGS_LOG → strategy)
- **Smart context loading** (load only relevant files, 8-25 per session, scales to 100+ Efforts)

---

## The Three-Phase Workflow (CRITICAL TO UNDERSTAND)

ATLAS operates in **three sequential phases**, NOT role-per-checkpoint.

### **INCORRECT mental model** (what ATLAS is NOT):
```
❌ AI1 executes CP0 (research checkpoint)
   AI3 executes CP1 (design checkpoint)
   AI3 executes CP2 (implementation checkpoint)
   AI3 executes CP3 (launch checkpoint)
```
This is WRONG. Don't think this way.

### **CORRECT mental model** (what ATLAS actually is):
```
✅ AI1 Phase: Research ENTIRE substep (before Effort exists)
     ↓ Produces: START_HERE.md
   AI2 Phase: Plan execution (create guides for ALL checkpoints)
     ↓ Produces: OUTLINE, guides, TODO_TRACKER
   AI3 Phase: Execute ALL checkpoints (CP0 through CPX)
     ↓ Produces: Working implementation, COMPLETION_SUMMARY
```

**Key insight:** Roles are **phases of work**, not **checkpoint assignments**.

---

## Phase 1: AI1 Research (Substep-Level Investigation)

### **When AI1 Runs**

**Trigger:** Substep is defined in ATLAS_STEPS.md, no research exists yet

**Example:**
```
ATLAS_STEPS.md contains:
  STEP_1_2: Build [Feature Name] (e.g., Payment System, User Dashboard, Notification Service)

No START_HERE.md exists yet for STEP_1_2
→ AI1 research phase needed
```

---

### **What AI1 Does**

**Job:** Research the ENTIRE substep (not just one checkpoint).

**Process:**
1. **Read substep definition** from ATLAS_STEPS.md
   - Understand: What must this substep accomplish?
   - How specific is it? (vague vs detailed)

2. **Read previous context** (if exists)
   - Previous substep's COMPLETION_SUMMARY
   - What was built? What was learned? What patterns emerged?

3. **Deep research** (varies by substep specificity)
   - If vague: 80% research (investigate everything - competitors, technical options, patterns)
   - If specific: 20% validation (is this approach sound? any gotchas?)

4. **Make implementation outcomes MORE specific**
   - Substep says: "Build user dashboard"
   - AI1 specifies: "Multi-tenant dashboard with real-time data integration, database backend, export capabilities, works across multiple customer segments, <2sec load time, responsive design"

5. **Rough CP breakdown** (3-10 CPs estimated)
   - AI1 guesses phases: Setup, core features, additional features, testing
   - AI2 will refine (might be different)

6. **Identify what AI2 needs to research**
   - "For CP0 setup, AI2 should research: Vercel monorepo patterns, Supabase multi-tenant setup"
   - "For CP1 analysis engine, AI2 should research: PageSpeed API integration, scoring algorithms"

---

### **What AI1 Produces**

**Primary output:**
```
/efforts/STEP_1_2_[NAME]/START_HERE.md
```

**Structure:**
- **Context:** What this substep builds, why, for whom
- **Research Findings:** Competitive analysis, technical options, design patterns
- **Implementation Outcomes:** VERY specific (more than substep definition)
- **Rough CP Breakdown:** Estimated 3-10 phases
- **For AI2:** What to research when creating each CP guide

**Length:** 800-1,500 lines (comprehensive)

**Purpose:** Give AI2 everything needed to create perfect execution guides

---

### **Completion Marker**

**AI1 complete when:**
- START_HERE.md exists in `/efforts/STEP_X_Y/`

**Framework detects:**
- "START_HERE.md exists → AI1 phase done → Time for AI2 planning"

---

### **Research Distribution: 80%**

AI1 is **80% research, 20% synthesis**:
- Most time spent investigating (competitors, technical options, patterns, examples)
- Some time synthesizing findings into START_HERE document
- No implementation (that's AI3's job)
- No detailed guide creation (that's AI2's job)

---

## Phase 2: AI2 Planning (Guide Creation with Research)

### **When AI2 Runs**

**Trigger:** START_HERE.md exists, no OUTLINE.md or guides exist yet

**Example:**
```
/efforts/STEP_1_2_SITE_CLONER/START_HERE.md exists
No OUTLINE.md exists yet
→ AI2 planning phase needed
```

---

### **What AI2 Does**

**Job:** Transform AI1's research into actionable execution guides for AI3.

**Process:**

**Step 1: Validate AI1's Research (30-60 min)**
- Read START_HERE.md thoroughly
- Spot-check findings (do recommendations make sense?)
- Confirm technical approach is sound
- Identify gaps (what did AI1 miss?)

**Step 2: Create OUTLINE (1 hour)**
- **Decide CP count:** 3-10 checkpoints (based on complexity)
  - Simple Effort: 3 CPs (setup, implement, deploy)
  - Medium: 5 CPs (setup, core, features, polish, deploy)
  - Complex: 8 CPs (setup, multiple implementation phases, testing, deploy)
- **First CP is ALWAYS:** CP0 (infrastructure setup)
- **Last CP is ALWAYS:** CPX (comprehensive testing + deployment)
- **Middle CPs are:** Implementation phases (AI2 decides split)
- **Document rationale:** Why this many CPs? Why this order?

**Step 3: Research CP0 Deeply (1-2 hours)**
- What does setup entail for THIS specific Effort?
- Git structure (monorepo? standalone? copy from where?)
- Infrastructure (Vercel project? Supabase? Environment vars?)
- Initial file structure
- Dependencies to install
- Validation (how to test setup worked?)
- **Find examples:** Look at previous Efforts, existing repos, documentation
- **Document exact steps:** Not "set up Vercel" but "1. Visit vercel.com, 2. Click New Project, 3. Name: [exact name], 4. Configure: [exact settings]"

**Step 4: Create CP0_GUIDE.md (1 hour)**
- Transform research into guide
- Include: Pre-flight (what to check first), Tasks (exact steps), Outputs (what should exist), Success criteria, Update TODO_TRACKER
- Reference sources (based on previous projects, platform documentation)
- Make it so detailed AI3 executes mechanically

**Step 5: Research CP1 Deeply (2-4 hours)**
- What does this implementation phase need?
- Technical patterns (how to integrate PageSpeed API? error handling? rate limiting?)
- Code examples (find similar implementations on GitHub, in docs)
- Best practices (what's the right approach?)
- Gotchas (what goes wrong? how to avoid?)

**Step 6: Create CP1_GUIDE.md (1 hour)**
- Same structure as CP0
- Informed by research (not generic)
- Include code examples, reference patterns found

**Step 7-X: Repeat for All CPs**
- Research CP deeply → Create guide
- Every CP gets same treatment (research → guide)

**Step X+1: Create OVERVIEW_GUIDE.md (30-45 min)**
- Synthesize all CPs into quick-start
- What we're building (1 paragraph)
- CP sequence (1-2 sentences per CP)
- Key watchouts (performance targets, integration gotchas)
- Testing strategy (when to test, what to validate)
- Quick reference (links to detailed guides)

**Step X+2: Create TODO_TRACKER.md (15-30 min)**
- List all CPs (CP0 through CPX)
- Mark all PENDING initially
- Add structure for AI3 to update (date completed, duration, notes)

**Step X+3: Create effort.md (15-30 min)**
- High-level overview
- Goals and success criteria
- Links to guides (OVERVIEW_GUIDE, START_HERE, CP guides)

---

### **What AI2 Produces**

**Files created:**
```
/efforts/STEP_1_2_[NAME]/
├── OUTLINE.md                      # AI2 creates
├── OVERVIEW_GUIDE.md               # AI2 creates
├── TODO_TRACKER.md                 # AI2 creates
├── effort.md                       # AI2 creates
└── guides/                         # AI2 creates all
    ├── CP0_GUIDE.md
    ├── CP1_GUIDE.md
    ├── CP2_GUIDE.md
    ├── ...
    └── CPX_GUIDE.md
```

**Length per guide:** 600-1,200 lines (detailed, not summary)

**Total AI2 output:** 4,000-8,000 lines of planning docs

**Purpose:** Enable AI3 to execute without questions

---

### **Completion Marker**

**AI2 complete when:**
- OUTLINE.md exists
- All CP guides exist (CP0 through CPX per OUTLINE)
- OVERVIEW_GUIDE.md exists
- TODO_TRACKER.md exists

**Framework detects:**
- "All guides + TODO_TRACKER exist → AI2 phase done → Time for AI3 execution"

---

### **Research Distribution: 50%**

AI2 is **50% research, 50% guide creation**:
- Research each CP individually (what does CP0 need? research. CP1? research.)
- Create guides informed by research (not generic templates)
- Guides reference sources ("Based on platform docs, reference implementations")

**AI2 is a research role** (not just templating). Research makes guides precise.

---

## Phase 3: AI3 Execution (All Checkpoints)

### **When AI3 Runs**

**Trigger:** All guides exist, TODO_TRACKER shows pending CPs

**Example:**
```
/efforts/STEP_1_2_SITE_CLONER/ has:
  - All guides (CP0-CP4)
  - TODO_TRACKER (shows all PENDING)
→ AI3 execution phase, starting at CP0
```

---

### **What AI3 Does**

**Job:** Execute ALL checkpoints precisely, track progress, produce working deliverables.

**Process:**

**Pre-Flight (Before CP0, first checkpoint):**
```bash
# 1. Git sync validation (ensure clean state)
git fetch origin
git checkout main && git pull
git checkout staging && git pull
git diff main staging  # Document any divergence

# 2. Read progress tracking
cat TODO_TRACKER.md
# Understand what's done (if resuming mid-Effort)

# 3. Load context
# Read OVERVIEW_GUIDE (5 min - get mental model)
# Read START_HERE (10 min - understand research)
# Read effort.md (3 min - understand goals)
```

**Execute CP0 (Setup/Infrastructure):**
```
# 1. Read CP0_GUIDE.md (8 min)
# Understand exact tasks

# 2. Spot-check sanity (5 min)
# - Will this setup achieve outcome?
# - Any security concerns? (API keys handled properly?)
# - Any red flags? (missing steps? vulnerability?)
# - Does approach make sense?

# 3. Execute tasks (per guide - 2-6 hours)
# Follow CP0_GUIDE.md exactly
# Git init, Vercel setup, Supabase, dependencies, etc.

# 4. Test after CP0 (15 min)
npm run build  # Must succeed
vercel deploy --preview  # Test deployment works
# Validate all success criteria from CP0_GUIDE

# 5. Update TODO_TRACKER (5 min)
# Mark CP0: ✅ COMPLETE
# Add completion date, duration, notes

# 6. Commit (5 min)
git add .
git commit -m "[STEP_1_2] CP0 complete - infrastructure initialized"
git push origin effort/STEP_1_2_SITE_CLONER

# 7. Report completion
"CP0 complete. Duration: 4.2h. Ready for CP1."
```

**Execute CP1-CPX (repeat for each):**
```
# 1. Read CPX_GUIDE.md (8 min)
# 2. Spot-check sanity (5 min)
#    - Security concerns?
#    - Scaling issues?
#    - Vulnerabilities?
#    - Will this achieve intended outcome?
# 3. Execute tasks (per guide - hours to days)
# 4. Test after CP (build + unit tests + manual)
# 5. Update TODO_TRACKER (mark complete)
# 6. Commit frequently during CP
# 7. Final commit: "[STEP_X_Y] CPX complete - [summary]"
# 8. Merge to staging (if appropriate)
# 9. Report completion, move to next CP
```

**Execute Final CP (Last checkpoint - CPX):**
```
# Standard tasks:
# - Complete remaining features
# - Comprehensive testing (E2E, performance, accessibility, cross-vertical if applicable)
# - Merge to staging
# - Full staging validation
# - Create PR staging → main (human approves, don't merge yourself)

# Additional final CP responsibilities:

# 1. Create COMPLETION_SUMMARY.md (30-60 min)
# Document:
# - What was built
# - Key decisions made
# - What worked (repeat in future)
# - What didn't work (avoid in future)
# - Recommendations for next substep
# - Technical foundation established (reusable for future)

# 2. Update ATLAS_STEPS.md (5 min)
# Mark substep complete:
# STEP_1_2: Build Payment System
# **Status:** ✅ COMPLETE
# **Completed:** 2025-12-20
# **Outcome:** Feature deployed and operational

# 3. Update TODO_TRACKER (final update)
# Mark all CPs complete
# Add final notes

# 4. Report Effort complete
"Effort STEP_1_2_SITE_CLONER complete.
COMPLETION_SUMMARY created.
ATLAS_STEPS.md updated.
PR #47 created (awaiting human approval).

Next: Human approves PR → Substep officially complete"
```

**Human approves PR:**
- Reviews code, testing, COMPLETION_SUMMARY
- Merges to main
- Substep is officially complete

---

### **What AI3 Produces**

**Outputs per CP:**
- Working code/implementation
- artifacts/CPX_implementation_notes.md (decisions, issues, learnings)
- Updated TODO_TRACKER.md (after each CP)
- Git commits (frequent, clear messages)

**Final outputs:**
- COMPLETION_SUMMARY.md (handoff to next substep)
- Updated ATLAS_STEPS.md (substep status)
- PR to main (awaiting human)

**Purpose:** Deliver working implementation + context for future work

---

### **Completion Marker**

**AI3 complete when:**
- All CPs executed (TODO_TRACKER shows all ✅)
- COMPLETION_SUMMARY.md created
- ATLAS_STEPS.md updated (substep marked complete)
- PR created (awaiting human approval)

**Human merges PR:**
- Substep officially complete
- Ready for next substep (framework detects, starts AI1 for STEP_1_3)

---

### **Research Distribution: 20%**

AI3 is **20% research, 80% execution**:
- Spot-check guides (sanity validation before executing)
- Quick technical checks (can this API do X? check docs)
- Security validation (any vulnerabilities in this approach?)
- Mostly executes (follows guides precisely)

---

## Core Concepts (The ATLAS Vocabulary)

### **Step**
Strategic milestone (months). What must become true for company to advance.

**Example:** "Build Platform Foundation" (3 months, 3 substeps)

**Defined in:** ATLAS_STEPS.md

---

### **Substep**
Execution unit within Step (weeks). One substep = one Effort.

**Example:** "STEP_1_2: Build Payment System" (2 weeks)

**Named:** STEP_X_Y (e.g., STEP_1_2, STEP_3_5)

**Becomes:** One Effort (STEP_1_2_SITE_CLONER)

---

### **Effort**
The work package AI1/AI2/AI3 execute to accomplish a substep.

**Contains:**
- START_HERE.md (AI1's research)
- OUTLINE.md (AI2's CP map)
- OVERVIEW_GUIDE.md (AI2's quick-start)
- guides/ (AI2's detailed CP instructions)
- TODO_TRACKER.md (progress tracking)
- artifacts/ (outputs during execution)
- COMPLETION_SUMMARY.md (AI3's final handoff)

**Duration:** 1-4 weeks typically

**Maps to:** One substep (STEP_X_Y → STEP_X_Y_SHORTNAME Effort)

---

### **Checkpoint (CP)**
Phase within Effort execution. AI3 executes these sequentially.

**Types:**
- **CP0:** ALWAYS setup/infrastructure (git, Vercel, Supabase, environment)
- **CP1-CPX-1:** Implementation phases (features, integrations, polish)
- **CPX (last):** ALWAYS comprehensive testing + deployment + completion

**Count:** Variable (3-10, AI2 decides based on complexity)

**Executed by:** AI3 only (AI1 and AI2 don't execute CPs)

**Progress tracked:** TODO_TRACKER.md (updated by AI3 after each CP)

---

### **START_HERE.md**
AI1's comprehensive research document.

**Created by:** AI1 (research phase)
**Read by:** AI2 (planning input), AI3 (context)
**Updated:** Never (static after AI1 completes)
**Purpose:** Enable AI2 to create perfect guides without guessing

**Key sections:**
- Research findings (competitive, technical, design)
- Implementation outcomes (very specific)
- Rough CP breakdown (AI2 refines)
- For AI2 (what to research per CP)

---

### **OUTLINE.md**
AI2's high-level checkpoint map.

**Created by:** AI2 (after reading START_HERE)
**Read by:** AI3 (understand CP sequence), Human (approve plan)
**Updated:** Rarely (only if CP count changes during planning)
**Purpose:** Show all CPs at a glance before detailed guides

**Contents:**
- Effort summary (1 paragraph)
- CP breakdown (CP0 through CPX with 1-2 sentences each)
- Rationale for CP count (why 5 and not 3 or 7?)
- Dependencies (what needs what)
- Testing strategy

---

### **OVERVIEW_GUIDE.md**
AI2's quick-start guide for the Effort.

**Created by:** AI2 (after creating all CP guides)
**Read by:** AI3 (first thing when starting Effort)
**Purpose:** Get AI3 up to speed in 5 minutes (before diving into detailed guides)

**Contents:**
- What we're building (1 paragraph)
- CP sequence (paragraph per CP - goal, duration, output)
- Key watchouts (performance targets, integration gotchas, multi-vertical testing)
- Testing strategy (when, what, how)
- Quick reference (links to START_HERE, CP guides, TODO_TRACKER)

---

### **CPX_GUIDE.md**
AI2's detailed instructions for one checkpoint.

**Created by:** AI2 (after researching that specific CP)
**Read by:** AI3 (when executing that CP)
**Updated:** Rarely (only if approach changes mid-Effort)
**Purpose:** Exact instructions AI3 executes mechanically

**Structure:**
- Overview (what this CP accomplishes)
- Pre-flight (what to check before starting)
- Tasks (detailed steps with commands, code examples)
- Outputs (what must exist after CP)
- Success criteria (how to know CP is complete)
- Update TODO_TRACKER (mark CP complete, add notes)
- Next CP (what comes after)

**Length:** 600-1,200 lines per guide

**Tone:** Precise, detailed, actionable (line numbers, commands, examples)

---

### **TODO_TRACKER.md**
Progress tracking document (CP-level granularity).

**Created by:** AI2 (initial template, all CPs marked PENDING)
**Updated by:** AI3 (after completing each CP)
**Read by:** AI3 (every time resuming work), Framework (for auto-detection), Human (status check)
**Purpose:** Track which CPs done, which current, enable resume

**Structure:**
- Overall status (Effort status, total CPs, completed count, current CP)
- CP0: [Goal] ✅ COMPLETE / 🔄 IN_PROGRESS / ⏸️ PENDING
  - Completed: [Date]
  - Duration: [Actual hours]
  - Notes: [Any issues or discoveries]
- CP1: [Goal] [Status]
  [Same structure]
- ... for all CPs
- Blockers: [Any blockers encountered]
- Notes: [General notes]

---

### **COMPLETION_SUMMARY.md**
AI3's handoff document to next substep.

**Created by:** AI3 (final task in last CP)
**Read by:** Next substep's AI1 (efficient context), AI2 (learnings), Human (review)
**Updated:** Never (static after Effort complete)
**Purpose:** Feed forward to next Effort (don't re-read all artifacts)

**Structure:**
- What was built (deliverables, metrics, tech)
- Key decisions (what we chose, why, trade-offs, outcomes)
- What worked (patterns to repeat)
- What didn't work (issues encountered, how resolved, avoid next time)
- Recommendations for next substep (what to reuse, what to avoid)
- Technical foundation (infrastructure established, reusable for future)

**Length:** 500-1,000 lines

**Purpose:** Next AI1 reads THIS (not 20 artifact files) - context efficiency

---

## Progress Tracking (Three Levels)

### **Level 1: Step/Substep Status (ATLAS_STEPS.md)**

```markdown
## STEP 1: Build Platform Foundation

**Status:** IN_PROGRESS (2 of 3 substeps complete)
**Started:** 2025-12-10
**Expected completion:** 2026-01-15

### Substeps

#### STEP_1_1: Build User Dashboard
**Status:** ✅ COMPLETE
**Completed:** 2025-12-15
**Outcome:** Feature deployed and validated with initial users
**Summary:** efforts/STEP_1_1_USER_DASHBOARD/COMPLETION_SUMMARY.md

#### STEP_1_2: Build Payment System
**Status:** 🔄 IN_PROGRESS (AI3 on CP3 of 5)
**Started:** 2025-12-16
**Expected:** 2025-12-20

#### STEP_1_3: Build Notification Service
**Status:** ⏸️ PLANNED
```

**Who updates:** AI3 when substep completes, or human/AI2 when Step completes

**Who reads:** Everyone (shows strategic progress)

---

### **Level 2: AI Phase Detection (File Existence)**

```
Framework checks /efforts/STEP_1_2_SITE_CLONER/:

START_HERE.md exists?
  NO → AI1 research phase needed
  YES → AI1 complete, continue to AI2 check

OUTLINE.md exists?
  NO → AI2 planning phase needed (hasn't started)
  YES → AI2 started, check completeness

Count guides/*.md files, compare to OUTLINE.md CP count
  Mismatch → AI2 planning phase (incomplete - creating guides)
  Match → AI2 complete, continue to AI3 check

TODO_TRACKER.md exists?
  NO → AI2 incomplete (final step)
  YES → AI2 complete, AI3 can execute

Read TODO_TRACKER.md, find first PENDING CP
  → AI3 execution phase, current CP is [X]
```

**Who updates:** File creation IS the update (no manual status file)

**Who reads:** Framework (for auto-detection), Human (understand phase)

---

### **Level 3: CP Progress (TODO_TRACKER.md)**

```markdown
## Checkpoint Progress

### CP0: Infrastructure Setup ✅ COMPLETE
**Completed:** 2025-12-16 14:30
**Duration:** 4.2 hours (estimated: 4h)
**Notes:** Platform + database setup smooth, copied from previous project patterns

### CP1: Core Cloning Logic ✅ COMPLETE
**Completed:** 2025-12-17 16:00
**Duration:** 1.8 days (estimated: 2d)
**Notes:** Puppeteer scraping faster than expected

### CP2: Content Extraction 🔄 IN_PROGRESS
**Started:** 2025-12-18 09:00
**Progress:** HTML/CSS extraction done, JS bundle handling remaining
**Blocker:** None
**Est. completion:** 2025-12-19

### CP3: Site Generation ⏸️ PENDING
**Est. duration:** 2 days
**Dependencies:** CP2 complete

### CP4: Testing & Deployment ⏸️ PENDING
**Est. duration:** 1 day
**Dependencies:** CP0-3 complete
```

**Who updates:** AI3 (after completing each CP - marks ✅, adds date/duration/notes)

**Who reads:** AI3 (knows what's done), Framework (auto-detection), Human (detailed status)

---

## File Types & Ownership

### **Who Creates What**

**AI1 creates:**
- START_HERE.md (research document)
- efforts/STEP_X_Y/ directory (initial)

**AI2 creates:**
- OUTLINE.md (CP map)
- OVERVIEW_GUIDE.md (quick-start)
- guides/CPX_GUIDE.md (all guides)
- TODO_TRACKER.md (progress template)
- effort.md (overview)

**AI3 creates:**
- Code/implementation (in repo)
- artifacts/CPX_implementation_notes.md (per CP)
- COMPLETION_SUMMARY.md (final handoff)

**AI3 updates:**
- TODO_TRACKER.md (after each CP)
- ATLAS_STEPS.md (when substep complete)

**Human creates:**
- Company CONTEXT.md (vision)
- ATLAS_STEPS.md (initial strategy, or approves AI2's draft)

**Human updates:**
- LEARNINGS_LOG.md (strategic learnings from COMPLETION_SUMMARY)
- DECISION_LOG.md (strategic decisions)
- ATLAS_STEPS.md (quarterly strategy evolution)

---

### **Who Reads What**

**AI1 reads:**
- ATLAS_STEPS.md (substep definition)
- Previous COMPLETION_SUMMARY.md (if exists)
- Company CONTEXT.md
- LEARNINGS_LOG.md (recent)
- Any existing research (if human/META did pre-work)

**AI2 reads:**
- START_HERE.md (AI1's research - primary input)
- ATLAS_STEPS.md (substep context)
- Previous COMPLETION_SUMMARY (if exists)
- Company CONTEXT.md
- LEARNINGS_LOG.md (recent)
- DECISION_LOG.md (recent)
- Templates (for structure)
- Previous similar Effort (if exists)

**AI3 reads:**
- OVERVIEW_GUIDE.md (quick context)
- TODO_TRACKER.md (progress state)
- CPX_GUIDE.md (current CP instructions)
- START_HERE.md (AI1's research - for context)
- effort.md (goals/criteria)
- Previous CP implementation notes
- Role guides (AI3_IMPLEMENTER, DEVELOPER_BEST_PRACTICES, GIT_WORKFLOW)

**Human reads:**
- ATLAS_STEPS.md (strategy status)
- OUTLINE.md (approve AI2's plan)
- COMPLETION_SUMMARY.md (Effort outcomes)
- TODO_TRACKER.md (detailed progress)
- PR diffs (code review before merging)

---

## Checkpoint Structure (The Pattern)

### **CP0: ALWAYS Infrastructure Setup (AI3)**

**Purpose:** Prepare technical foundation

**Common tasks:**
- Create git repository (if new project)
- Create Vercel project, configure deployment
- Create Supabase project, deploy database schema
- Configure environment variables (.env files, Vercel env vars)
- Install dependencies (npm install packages)
- Create initial file/folder structure
- Create feature branch (effort/STEP_X_Y_NAME)
- Validate deployment works (can push code → auto-deploy)

**Duration:** 2-6 hours

**Role:** AI3 (implementer) - NOT AI1 (research already done by AI1 in START_HERE)

**Output:**
- Infrastructure operational
- Can build features in CP1+
- Git branch created
- Deployment pipeline verified

---

### **CP1-CPX-1: Implementation Phases (AI3, Variable Count)**

**Purpose:** Build features, integrate services, create functionality

**Number of CPs:** AI2 decides (1-8 implementation CPs)

**Decision factors:**
- **Effort size:**
  - Small (2-3 days total): 1-2 implementation CPs
  - Medium (1 week): 2-4 implementation CPs
  - Large (2-3 weeks): 4-8 implementation CPs

- **Natural phases:**
  - Does work have clear phases? (design → build → integrate → polish)
  - Each phase could be a CP

- **Testing checkpoints:**
  - Good to validate incrementally (build core → test → build features → test)

- **Scope per CP:**
  - If CP would be <4 hours: Combine with another
  - If CP would be >1 week: Split into multiple

**Each implementation CP:**
- Executes tasks from guide
- Tests after completion (build + unit + manual)
- Updates TODO_TRACKER
- Merges to staging (for preview/validation)
- Produces implementation notes

**Examples:**

**Simple Effort (3 total CPs):**
```
CP0: Setup (4h)
CP1: Implementation (2 days)
CP2: Testing & Deploy (1 day)
```

**Medium Effort (5 total CPs):**
```
CP0: Setup (4h)
CP1: Core Functionality (2 days)
CP2: Additional Features (2 days)
CP3: Polish & UX (1 day)
CP4: Testing & Deploy (1 day)
```

**Complex Effort (8 total CPs):**
```
CP0: Setup (4h)
CP1: Component Library (2 days)
CP2: Variant A Implementation (2 days) [e.g., customer segment, feature tier, or use case]
CP3: Variant B Implementation (2 days)
CP4: Variant C Implementation (2 days)
CP5: Variant Config System (1 day)
CP6: Cross-Scenario Testing (1 day) [e.g., test all variants, user types, edge cases]
CP7: Deployment & Docs (1 day)
```

**AI2 decides split. AI3 executes whatever AI2 planned.**

---

### **CPX: ALWAYS Final Validation & Deployment (AI3)**

**Purpose:** Comprehensive quality gate and production launch

**Tasks:**
- Complete any remaining implementation
- **Comprehensive testing:**
  - E2E tests (full user flows)
  - Performance (Lighthouse, PageSpeed - validate <2s mobile)
  - Accessibility (WCAG AA, axe DevTools - zero critical errors)
  - Cross-segment (if multi-segment tool - test across customer types)
  - Security (no secrets, no vulnerabilities, input validation)
  - Multi-tenant (if applicable - isolation works?)
- Full staging validation (test deployed version)
- Create PR staging → main (human approves)
- Post-launch monitoring plan
- **Create COMPLETION_SUMMARY.md** (handoff doc)
- **Update ATLAS_STEPS.md** (mark substep complete)
- **Update TODO_TRACKER** (mark all CPs ✅)

**Duration:** 1-2 days

**Critical:** This is the quality gate. No shortcuts. Everything validated before production.

**Role:** AI3 with human approval (human merges PR)

**Output:**
- Production deployment (via PR)
- COMPLETION_SUMMARY.md
- Updated ATLAS_STEPS.md
- All quality checks passed

---

## The Learning Loop (Knowledge Compounds)

```
Execution → Discovery → Documentation → Application → Better Execution

Detailed:

AI3 executes Effort
  ↓ Discovers patterns, issues, solutions
AI3 documents in COMPLETION_SUMMARY
  ↓ "Database security patterns from previous project work great - copy for all future"
Human reads COMPLETION_SUMMARY
  ↓ Extracts strategic learnings
Human updates LEARNINGS_LOG
  ↓ "Multi-tenant architecture from day 1 pays off - make standard"
AI1 researching STEP_1_3
  ↓ Reads LEARNINGS_LOG + STEP_1_2 COMPLETION_SUMMARY
AI1's START_HERE for STEP_1_3
  ↓ "Reuse Supabase instance from STEP_1_2, copy RLS patterns (proven)"
AI2 planning STEP_1_3
  ↓ Reads learnings, applies patterns
AI2 creates guides with patterns
  ↓ "CP0: Reuse existing Supabase (don't create new project)"
AI3 executes STEP_1_3
  ↓ Faster (infrastructure exists), better (patterns proven)
Effort STEP_1_3 completes in 60% of STEP_1_2 time
  ↓ Velocity compounds
Next Efforts even faster...
```

**This is how ATLAS can enable improvement:** Effort 1 takes 2 weeks → Effort 10 may take 7-10 days (with consistent application and compounded knowledge)

---

## Auto-Detection Logic (Framework Intelligence)

### **User says: "Continue ATLAS on STEP_1_2"**

**Framework determines everything automatically:**

```
Step 1: Identify Effort directory
  find efforts/ -name "STEP_1_2*"
  Found: efforts/STEP_1_2_SITE_CLONER/

Step 2: Detect AI phase
  Check START_HERE.md exists?
    NO → "Starting AI1 research phase for STEP_1_2"
          Load AI1 context, begin research
    YES → Continue to Step 3

  Check OUTLINE.md exists?
    NO → "Starting AI2 planning phase (START_HERE exists)"
          Load AI2 context, begin planning
    YES → Continue to Step 4

  Count guides in /guides/ directory
  Compare to CP count in OUTLINE.md
  Mismatch → "Continuing AI2 (creating CP4 of 7 guides)"
              Load AI2 context, continue guide creation
  Match → Continue to Step 5

  Check TODO_TRACKER.md exists?
    NO → "AI2 incomplete (final task)"
          Continue AI2, create TODO_TRACKER
    YES → "AI2 complete, starting AI3"
          Continue to Step 6

Step 3: Determine current CP (AI3 phase)
  Read TODO_TRACKER.md
  Find first CP marked PENDING (⏸️)
  Found: CP3 (Site Generation)

Step 4: Load context automatically
  Load AI3 context for CP3:
    - OVERVIEW_GUIDE.md
    - TODO_TRACKER.md
    - guides/CP3_GUIDE.md
    - artifacts/CP2_implementation_notes.md
    - [other required files per CONTEXT_INDEX]

Step 5: Report and begin
  "Resuming AI3 execution on CP3 (Site Generation) of Effort STEP_1_2_SITE_CLONER"
  [AI3 begins CP3 execution]

User input: "Continue ATLAS on STEP_1_2"
Framework determined: AI3 phase, CP3, exact context loaded
```

**This is "state-driven" - framework knows state from files, not manual tracking.**

---

## File Structure (Complete)

```
/efforts/STEP_X_Y_[NAME]/
├── START_HERE.md                    # AI1 (research)
├── OUTLINE.md                       # AI2 (CP map)
├── OVERVIEW_GUIDE.md                # AI2 (quick-start)
├── TODO_TRACKER.md                  # AI2 creates, AI3 updates
├── COMPLETION_SUMMARY.md            # AI3 (handoff)
├── effort.md                        # AI2 (overview)
│
├── guides/                          # AI2 creates all (variable count)
│   ├── CP0_GUIDE.md                # Setup (always exists)
│   ├── CP1_GUIDE.md                # Implementation
│   ├── CP2_GUIDE.md                # Implementation
│   ├── ...                         # Variable (3-10 total)
│   └── CPX_GUIDE.md                # Final (testing/deploy, always last)
│
└── artifacts/                       # AI3 creates during execution
    ├── CP0_setup_notes.md
    ├── CP1_implementation_notes.md
    ├── CP2_implementation_notes.md
    └── ...
```

---

## Context Management (Smart Loading)

**Core principle:** Load minimum necessary, not maximum available.

**Typical loads:**
- **AI1 research:** 8-12 files (~35K tokens)
- **AI2 planning:** 12-18 files (~65K tokens first CP, ~45K tokens per additional CP)
- **AI3 CP0:** 12-18 files (~60K tokens first time)
- **AI3 CP1+:** 8-12 files (~35K tokens, lighter after first)

**Scales to 100+ Efforts:** Because we load selectively (relevant Step section only, recent learnings only, current Effort only)

**See CONTEXT_INDEX.md for exact loading rules per role and checkpoint.**

---

## Framework Limitations

**ATLAS optimizes for:**
- Systematic execution over ad-hoc work
- Learning capture over repeated mistakes
- Clear progress tracking over uncertainty

**ATLAS cannot fix:**
- Wrong market or product choice
- Insufficient customer research
- Poor product-market fit
- Inadequate funding or team
- Weak execution discipline

**Realistic expectations:**
- Velocity improvements: 2-4x over 20+ efforts (not 10x)
- Learning compounds IF you consistently apply the framework
- Quality improves IF you maintain discipline
- Success still requires market validation, strong execution, and often luck

---

## Integration Points

### **ATLAS (generic framework) + Company (specific context)**

**ATLAS provides:**
- Workflow system (AI1 → AI2 → AI3)
- File templates (START_HERE, OUTLINE, guides)
- Role definitions (what each AI does)
- Progress tracking (TODO_TRACKER, status markers)

**Company provides:**
- Vision document (COMPANY_CONTEXT.md - outside ATLAS)
- Strategic Steps (ATLAS_STEPS.md - inside ATLAS strategy/)
- Learnings (captured during execution)
- Decisions (strategic choices made)

**Separation maintained:**
- ATLAS is reusable (works for any company, project, or product)
- Company context is external (specific to your implementation)

---

## Why This Design Works

### **1. Separation of Concerns**

**AI1:** Figure out WHAT to build (research)
**AI2:** Figure out HOW to build it (detailed planning)
**AI3:** BUILD it (execution)

**No blur:** Each AI has one job. Prevents confusion and scope creep.

---

### **2. Research Tapers Appropriately**

**Early (AI1):** Heavy research needed (understand problem space)
**Middle (AI2):** Moderate research (validate + find implementation patterns)
**Late (AI3):** Light research (spot-checks only, mostly execute)

**Efficiency:** Don't research during implementation (wastes time). Research upfront (saves time).

---

### **3. Progress is State, Not Documentation**

**State is encoded in files:**
- START_HERE exists → AI1 done
- Guides exist → AI2 done
- TODO_TRACKER shows ✅ → CPs done

**Not separate status tracker.** File existence IS the status.

**Benefits:**
- Can't lose state (files are state)
- Can resume anywhere (read files, determine next)
- Can validate (scan files, check completeness)

---

### **4. Handoffs Are Artifacts**

**AI1 → AI2:** START_HERE.md is the handoff
**AI2 → AI3:** OVERVIEW_GUIDE + TODO_TRACKER + guides are the handoff
**AI3 → Next AI1:** COMPLETION_SUMMARY.md is the handoff

**Not chat messages.** Artifacts enable clean phase transitions.

---

### **5. Learning is Structural**

**Not aspirational:** "We should capture insights"

**But structural:**
- AI3 MUST create COMPLETION_SUMMARY (can't mark Effort complete without it)
- Human reads COMPLETION_SUMMARY (part of weekly workflow)
- AI1 MUST read previous COMPLETION_SUMMARY (required context)
- AI2 MUST read LEARNINGS_LOG (required planning input)

**Learning is built into workflow, not optional.**

---

## Success Metrics (Is ATLAS Working?)

**After 1 Effort:**
- ✅ Effort completed (all CPs done)
- ✅ COMPLETION_SUMMARY exists (learnings captured)
- ✅ Process understood (know how workflow works)

**After 3 Efforts:**
- ✅ Velocity improving (Effort 3 faster than Effort 1)
- ✅ Learnings applied (patterns repeated, mistakes avoided)
- ✅ Templates refined (guides better based on experience)

**After 10 Efforts:**
- ✅ Potential velocity gain (30-50% improvement with consistent application)
- ✅ Knowledge compounding (templates evolved, tools built)
- ✅ Strategic evolution (steps refined based on learnings)

**After 30 Efforts:**
- ✅ Systematic execution (quality maintained, efficiency improved)
- ✅ Scalable process (team can follow guides)
- ✅ Company operating system (systematic approach embedded)

---

## What ATLAS Enables

- Research → Plan → Execute → Learn → Evolve strategy → Repeat
- Each cycle: Faster, better, more informed
- Knowledge compounds, velocity increases, quality maintains
- Systematic approach to building complex products with evolving requirements
- Clear progress tracking and knowledge capture across all execution phases

---

## Version History

**v2.0 (2025-12-11):**
- Complete workflow redesign
- Three-phase model (AI1 → AI2 → AI3 linear handoff)
- Auto-detection (framework finds state)
- Progress tracking (TODO_TRACKER, three levels)
- Correct checkpoint structure (CP0 = setup, last = testing/deploy)
- File ownership explicit (who creates/updates/reads)
- Research distribution clear (80/50/20)

**v1.0 (2025-12-10):**
- Initial release (deprecated)
- Workflow was incorrect (role-per-checkpoint model)
- Missing progress tracking
- Manual state specification
- Rebuilt as v2.0

---

## Reading Order

**Quick path (1 hour):**
1. README.md (this file) - 5min
2. QUICK_START.md - 15min
3. ONBOARDING.md - 30min
4. **Start using** - Create vision doc, create Steps, execute

**Comprehensive path (4 hours):**
1. README.md - 5min
2. ATLAS_OVERVIEW.md (this file) - 30min
3. ATLAS_SPECIFICATION.md - 45min
4. Role guides (AI1, AI2, AI3) - 45min each = 135min
5. ONBOARDING.md - 30min
6. Templates (skim) - 15min
7. **Start using** - Fully informed

**Reference as needed:**
- ATLAS_GLOSSARY.md - Quick terminology lookup
- CONTEXT_INDEX.md - What files to load
- ATLAS_VALIDATION.md - Verify setup
- Templates - When creating files
- Examples - See correct workflow

---

## Philosophy

ATLAS v2.0 is built on these beliefs:

**Measure thrice, cut once:**
- AI1 measures (deep research)
- AI2 measures again (validation + planning)
- AI3 cuts (precise execution)

**State is files, not memory:**
- Progress tracked in files (TODO_TRACKER)
- Can always resume (read files, determine next)
- Never lose state (files persist)

**Learning compounds:**
- Every Effort teaches next
- Knowledge captured explicitly
- Velocity improves systematically

**Quality is systematic:**
- Security checks (AI3 validates)
- Testing after each CP (not deferred)
- Human approval for production (final gate)

**Roles prevent chaos:**
- AI1 researches (doesn't implement)
- AI2 plans (doesn't execute)
- AI3 implements (doesn't strategize)
- Boundaries enable parallelism

---

## Built For

**Reusable for:** Companies that prioritize systematic planning and value disciplined execution

---

## Support

**Understanding ATLAS:**
- ATLAS_OVERVIEW.md - System explanation
- ATLAS_SPECIFICATION.md - Technical details
- QUICK_START.md - Fast track

**Using ATLAS:**
- ATLAS_ENTRY_POINT.md - Auto-detection and invocation
- Role guides - How each AI works
- Templates - File structures

**Maintaining ATLAS:**
- HUMAN_GUIDE.md - Your operational manual
- ATLAS_VALIDATION.md - Health checks
- ONBOARDING.md - Setup procedures

---

## Next Steps

**If new to ATLAS:**
1. Read ATLAS_OVERVIEW.md (understand system)
2. Read ONBOARDING.md (learn configuration)
3. Create company vision + strategy
4. Start first Effort

**If ready to use:**
```
"Continue ATLAS on STEP_X_Y"
```

**Framework handles the rest.**

---

**ATLAS v3.0 is ready for systematic company building.** Built for ambitious, systematic company building.
