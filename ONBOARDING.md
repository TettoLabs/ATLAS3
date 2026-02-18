# ATLAS Onboarding - Configure for Your Company

**Purpose:** Complete guide to make ATLAS3 operational for your specific company
**Time:** 2-4 hours to full operation
**Status:** v2.0

---

## Overview

**ATLAS3 framework is 100% complete** (31 files, all generic infrastructure).

**What's missing:** Your company-specific context and strategy (2 files).

**After this guide:**
- ATLAS3 configured for your company
- Ready to execute first substep
- Provides structure for pursuing $1M+ ARR with systematic execution

---

## Required Files (What YOU Must Create)

### **File 1: Company Vision Document** (Outside ATLAS)

**Filename:** `YOUR_COMPANY_CONTEXT.md`
**Location:** `/Projects/` (sibling to ATLAS3, not inside)
**Size:** 400-600 lines
**Time:** 1-2 hours
**Created by:** You (founder) or strategic AI with your guidance

**Why outside ATLAS:** ATLAS is generic framework. Vision is company-specific.

**Required sections:**
1. What you're building (product, problem, customer)
2. Target market (who, pain, opportunity)
3. Go-to-market (acquisition, sales, pricing)
4. Strategic direction (phases: 0-6mo, 6-12mo, 1-3yr)
5. Constraints (team, budget, time, technical)
6. Success definition (metrics per timeframe, failure signals)
7. Known unknowns (what you'll discover, hypotheses testing)

**Goal:** 400-600 lines, specific and honest about your situation.

---

### **File 2: Strategic Steps** (Tracker + Individual Files - Inside ATLAS)

**Files:** (Create tracker + individual step files)
- `ATLAS_STEPS_TRACKER.md` (high-level status of all steps)
- `steps/STEP_1.md` (first Step definition)
- `steps/STEP_2.md` (second Step definition)
- `steps/STEP_3.md` (etc. as needed)

**Location:** `/ATLAS3/strategy/`
**Size:** Tracker ~200 lines, each step file ~150-300 lines
**Time:** 1-2 hours total
**Created by:** You or strategic AI reading your vision doc

**Why individual files:**
- Each Step is its own file (easy to find, edit)
- Tracker provides high-level overview
- AI loads relevant step file only (efficient)
- Scales cleanly (Step 10 doesn't bloat Step 1)

**Required per Step file:**
- Objective (what must become true)
- Why it matters (strategic rationale)
- Success criteria (measurable)
- Substeps (executable units with 7 elements each)
- Dependencies (what needs what)
- Hypotheses (what you're testing - optional)

**Templates:**
- strategy/ATLAS_STEPS_TRACKER.md (for tracker)
- strategy/steps/STEP_TEMPLATE.md (for individual steps)

---

## Optional Files (Enhance but Not Required)

**File 3: ATLAS_ASSUMPTIONS.md** (detailed constraints)
- Template exists: strategy/ATLAS_ASSUMPTIONS.md
- Fill with: Detailed team, budget, time, technical constraints
- Or skip: Use constraints from vision doc (simpler)

**File 4: Brand Guidelines**
- Filename: YOUR_COMPANY_BRAND.md (outside ATLAS)
- Contains: Logo, colors, fonts, voice
- Used by: AI3 during design/implementation
- When: Before customer-facing work

---

## Onboarding Workflow (Step-by-Step)

### Phase 1: Validate ATLAS3 (15 min)

```bash
# Check all framework files exist
ls /ATLAS3/*.md | wc -l
# Should be: 6 core files

ls /ATLAS3/roles/*.md | wc -l
# Should be: 5 role guides

ls /ATLAS3/templates/*.md | wc -l
# Should be: 7 templates

ls /ATLAS3/modes/*.md | wc -l
# Should be: 8 mode files

ls /ATLAS3/strategy/*.md | wc -l
# Should be: 4 strategy templates

# Run Mode 7 (Health Check) for comprehensive validation
"Run ATLAS Mode 7"
# Should report: ✅ File structure complete
```

---

### Phase 2: Read Core Docs (45-60 min)

**Read in order:**
1. README.md (5 min - what is ATLAS3)
2. ATLAS_OVERVIEW.md (20 min - complete system explanation)
3. ATLAS_GLOSSARY.md (5 min - terminology)
4. ATLAS_SPECIFICATION.md (20 min - technical workflow)
5. ATLAS_ENTRY_POINT.md (5 min - 8 modes explained)

**Now you understand ATLAS3.**

---

### Phase 3: Create Vision Document (1-2 hours)

**File:** `/Projects/YOUR_COMPANY_CONTEXT.md`

**Process:**

**Option A: Write yourself** (1-2 hours if thoughtful)
- Use structure outlined above (7 required sections)
- Be honest (real constraints, not aspirational)
- Be specific (concrete metrics, clear customer profile)
- Acknowledge unknowns (what you'll discover)

**Option B: Collaborative with Usher** (faster, 45-60 min)
```
"Run ATLAS Mode 2" (Refine Substeps mode can also help draft vision)

Or create minimal draft (30 min), then:
"Help me refine company vision document"

Usher asks clarifying questions, helps structure
```

**Result:** Vision doc exists (400-600 lines, comprehensive)

---

### Phase 4: Create Strategic Steps (1-2 hours)

**Files:** `/ATLAS3/strategy/ATLAS_STEPS_TRACKER.md` + `/ATLAS3/strategy/steps/STEP_X.md`

**Process:**

**Option A: Have strategic AI create**
```
"Run ATLAS Mode 2" (Refine Substeps)

Or invoke directly:
"Create ATLAS strategy files from my vision document at /YOUR_COMPANY_CONTEXT.md

1. Create ATLAS_STEPS_TRACKER.md (high-level overview)
2. Create steps/STEP_1.md (first milestone - detailed)
3. Create steps/STEP_2.md (second milestone - detailed)
4. Create steps/STEP_3.md (third milestone - rough outline)

Each step file should have:
- Objective, why it matters, success criteria
- 2-3 substeps with full 7-element definitions
- Dependencies

Use templates: ATLAS_STEPS_TRACKER.md and steps/STEP_TEMPLATE.md"

AI drafts, you review/approve
```

**Option B: Write manually** (1-2 hours)
- Create ATLAS_STEPS_TRACKER.md (use existing file as template)
- Copy steps/STEP_TEMPLATE.md to steps/STEP_1.md
- Fill in Step 1 details (objective, substeps)
- Repeat for STEP_2.md, STEP_3.md
- Update tracker with your steps

**Result:** Strategy files exist (tracker + 2-3 step files, 500-1,000 lines total)

---

### Phase 5: First Execution Test (30 min)

**Validate everything works:**

```
1. Run ATLAS Mode 1 (Auto-Resume)

Usher should:
- Scan for active work (finds none)
- Offer to start first substep (reads ATLAS_STEPS for first PLANNED)
- Suggest: "Start AI1 research for STEP_X_Y?"

2. Say yes (or run Mode 3 to specify substep)

Usher should:
- Load AI1 context (8-10 files)
- Begin AI1 research workflow
- You (or AI) conduct research (6-12 hours)
- Produce START_HERE.md

3. Continue with "Run ATLAS Mode 1"

Usher should:
- Auto-detect START_HERE exists → AI2 phase
- Load AI2 context
- Begin AI2 planning
- Create OUTLINE, guides, TODO_TRACKER

4. Continue with "Run ATLAS Mode 1"

Usher should:
- Auto-detect guides exist → AI3 phase
- Load AI3 context for CP0
- Begin CP0 execution

**If all works: ✅ ATLAS3 is operational**
```

---

## Validation Checklist

**Before declaring onboarding complete:**

**✓ ATLAS3 Framework**
- [x] All 31 framework files exist (verified via Mode 7 or manual check)
- [ ] Read core docs (OVERVIEW, SPECIFICATION, entry point)
- [ ] Understand 8 Usher modes
- [ ] Understand three-phase workflow (AI1 → AI2 → AI3)

**✓ Company Configuration**
- [ ] YOUR_COMPANY_CONTEXT.md created (vision doc, outside ATLAS)
- [ ] All sections filled (what, who, why, constraints, success, unknowns)
- [ ] Honest about constraints (real budget, real time, real limitations)
- [ ] Specific about success (measurable metrics, timeframes)

**✓ Strategic Steps**
- [ ] ATLAS_STEPS_TRACKER.md created (high-level overview)
- [ ] steps/STEP_1.md created (first Step, detailed)
- [ ] steps/STEP_2.md created (second Step, detailed)
- [ ] 2-3 Steps defined in detail (next 6 months)
- [ ] Each Step has: objective, why, success criteria, substeps
- [ ] Substeps are execution-sized (1-4 weeks each)

**✓ First Execution Test**
- [ ] Ran Mode 1 (auto-resume successfully found next work)
- [ ] Started AI1 on first substep (research began)
- [ ] Framework auto-detected phases correctly
- [ ] Context loading worked (reasonable file counts)

**✓ Operational Readiness**
- [ ] Understand how to invoke Usher (daily: Mode 1)
- [ ] Know weekly discipline (Friday: Mode 5 learning capture)
- [ ] Scheduled monthly health check (Mode 7)
- [ ] Scheduled quarterly review (Mode 2 + Mode 8)

**All checked:** ✅ ATLAS3 is fully operational for your company

---

## Company Types (Adaptation Examples)

**Service business (Agency, Consulting):**
- Steps map to client batches (Step 1: Clients 1-3, Step 2: Clients 4-10)
- Substeps are client projects (STEP_1_1 = First client)
- Tools emerge from delivery (Step X: Build internal tools)

**SaaS/Product:**
- Steps map to product milestones (Step 1: MVP, Step 2: PMF, Step 3: Scale)
- Substeps are features or growth initiatives
- Platform evolves from usage patterns

**Marketplace:**
- Steps map to transaction milestones (Step 1: First 100 transactions)
- Substeps are supply/demand initiatives
- Systematic execution increases the probability of achieving marketplace liquidity

**ATLAS3 adapts to your domain.** Define steps that match your business model and strategic priorities.

---

## Adapting ATLAS for Your Technology Stack

**ATLAS examples use Next.js + Vercel + Supabase**, but the framework works with any technology stack.

### How to Adapt

**The framework structure never changes:**
- AI1 → AI2 → AI3 phases (research → planning → execution)
- Checkpoint system (CP0 setup, CP1-X implementation, final CP testing)
- Progress tracking (TODO_TRACKER, COMPLETION_SUMMARY)
- Learning capture (LEARNINGS_LOG, knowledge compounding)

**What you adapt: Technology references in implementation**

**Example adaptations:**

**Python/Django projects:**
- Where examples say "Vercel deployment" → Use Railway, Render, or AWS
- Where examples say "Supabase" → Use PostgreSQL with Django ORM
- Where examples say "Next.js app" → Use Django application
- Where examples say "npm install" → Use pip install
- **Workflow stays identical:** AI1 researches your Django setup, AI2 creates CP guides for Django, AI3 executes

**Mobile apps (iOS/Android):**
- Where examples say "deploy to Vercel" → Submit to App Store/Play Store
- Where examples say "database setup" → Configure Firebase or local SQLite
- Where examples say "staging URL" → TestFlight or internal testing
- **Workflow stays identical:** Same three phases, same checkpoint structure

**Go/Rust backend services:**
- Where examples say "Next.js" → Your language/framework
- Where examples say "Vercel" → Docker + Kubernetes or cloud platform
- Where examples say "Supabase" → PostgreSQL or your database choice
- **Workflow stays identical:** Research → Plan → Execute with your tech

**Desktop applications:**
- Where examples say "deployment" → Installer distribution and code signing
- Where examples say "database" → Local SQLite or embedded database
- Where examples say "Vercel project" → Build pipeline for your platform
- **Workflow stays identical:** Same orchestration, different implementation

### Key Principle

**Framework = Orchestration system (universal)**
**Examples = Implementation details (adapt to your stack)**

When reading guides and templates:
- Focus on the *structure* (what phases, what checkpoints, what order)
- Translate the *technology* (your stack, your tools, your deployment)
- Keep the *workflow* (AI1/AI2/AI3, checkpoints, progress tracking)

The examples are detailed and specific to help you understand the framework depth. Apply the same depth to your own technology choices.

---

## Time Investment

**Onboarding:**
- Validate ATLAS3: 15 min
- Read docs: 60 min
- Create vision: 90 min
- Create Steps: 90 min
- First test: 30 min
**Total: 4-5 hours**

**Weekly (ongoing):**
- Mode 1 execution: 30-60 min/day (invoking, reviewing)
- Mode 5 learning: 15 min/week (Friday)
**Total: 3-6 hours/week**

**Monthly:**
- Mode 7 health check: 30 min
**Total: 30 min/month**

**Quarterly:**
- Mode 2 strategy review: 2 hours
- Mode 8 template evolution: 3 hours
**Total: 5 hours/quarter**

**Annual overhead:** ~160-200 hours on ATLAS itself

**If ATLAS delivers 30-50% velocity improvement with consistent application:** May save 300-500 hours execution

**Potential ROI: 2-3:1** (200 hours invested, potential 400-500 hours saved with disciplined application)

---

## Next Steps

**Immediately:**
1. Create YOUR_COMPANY_CONTEXT.md (vision)
2. Create ATLAS_STEPS_PART1.md (strategy)
3. Run Mode 1 (start first substep)

**This week:**
1. Execute first substep (AI1 → AI2 → AI3)
2. Capture learnings (Mode 5 on Friday)

**This month:**
1. Complete 2-3 substeps
2. Run health check (Mode 7)
3. See velocity improving

**This quarter:**
1. Complete initial strategic milestones
2. Review strategy (Mode 2 - refine upcoming steps)
3. Evolve templates (Mode 8 - apply learnings)

---

**Welcome to ATLAS3. Build your company systematically.** 🚀
