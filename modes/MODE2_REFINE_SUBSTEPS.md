# Mode 2: Refine Substeps - Collaborative Strategy Improvement

**Purpose:** Work with human to refine/perfect substeps before AI1/AI2/AI3 execute
**Usage:** ~5% (strategic refinement, mid-flight adjustments)
**Trigger:** Human needs to update strategy, refine vague substep, or adjust after learnings

---

## What This Mode Does

**Usher becomes collaborative partner:**
1. Read current ATLAS_STEPS (partitioned files)
2. Show status (what's complete, what's in progress, what's planned)
3. Human selects substep to refine (or Step to restructure)
4. Usher loads context for that substep/Step
5. Collaborative refinement (Usher asks questions, helps structure)
6. Usher updates ATLAS_STEPS_PARTX.md files
7. Logs changes in DECISION_LOG.md

**This enables:**
- Mid-flight strategy adjustments (learnings change approach)
- Vague substeps become specific (before AI1 wastes time researching unknowns)
- Step restructuring (split substeps differently, reorder, add/remove)

---

## Files Usher Loads (In Order)

### Initial Context (What's Current State?)

```
1. strategy/ATLAS_STEPS_TRACKER.md (~200 lines, ~2K tokens, 2min)
2. strategy/steps/STEP_X.md (relevant step file ~200 lines, ~2K tokens, 2min)

Total STEPS files: ~1,200 lines, ~12K tokens, 12min

4. COMPANY_CONTEXT.md (~400 lines, ~4K tokens, 5min)

5. LEARNINGS_LOG.md (last 20-30 entries - ~1,500 lines, ~15K tokens, 8min)

6. DECISION_LOG.md (last 15 entries - ~1,200 lines, ~12K tokens, 6min)

7. Recent COMPLETION_SUMMARYs (last 3-5 Efforts - ~3,000 lines, ~30K tokens, 15min)
   Purpose: Understand recent execution outcomes

Total: ~7,100 lines, ~77K tokens, ~50min context load
```

**This is heavier context** (reviewing strategy requires broad view), but still under 100K.

---

## Workflow: Collaborative Refinement

### Step 1: Present Current Strategy Status

**Usher analyzes and reports:**

```markdown
Current Strategy Status (from ATLAS_STEPS files):

**PART 1: Foundation (Steps -1 through 2)**
- STEP -1: Platform Setup ✅ COMPLETE (2025-12-10)
- STEP 0: Build Core Tools
  - STEP_0_1: Audit Engine ✅ COMPLETE (2025-12-15)
  - STEP_0_2: Site Cloner 🔄 IN_PROGRESS (AI3 on CP3 of 5)
  - STEP_0_3: Rebuild Engine Core ⏸️ PLANNED
- STEP 1: Validate on Contractors
  - STEP_1_1: First Contractor ⏸️ PLANNED
  - STEP_1_2-1_10: Next 9 contractors ⏸️ PLANNED
- STEP 2: Build 10xbuild.com ⏸️ PLANNED

**PART 2: Scale (Steps 3-5)**
- STEP 3: Scale Contractors (10 → 25) ⏸️ PLANNED
- STEP 4: Add Law Firm Vertical ⏸️ PLANNED
- STEP 5: Launch Inspector SaaS ⏸️ PLANNED

**PART 3: Platform (Steps 6-10)**
- All PLANNED (will be defined after Part 2 learnings)

**Overall progress:**
- Steps complete: 2 of 10 (20%)
- Substeps complete: 2 of 50+ (4%)
- Current work: STEP_0_2 (Site Cloner, 60% done)
- Next planned: STEP_0_3 (Rebuild Engine)

**Recent learnings (last 5):**
1. Multi-tenant architecture pays off (STEP_0_1, STEP_0_2)
2. Cross-vertical testing critical (caught contractor assumptions)
3. Reusing infrastructure saves 30-40% setup time
4. PageSpeed rate limits hit faster than expected
5. Puppeteer patterns proven (use across tools)
```

---

### Step 2: Ask What to Refine

```
What would you like to refine?

1. Specific substep (drill into details, make more specific)
2. Entire Step (restructure substeps, reorder, adjust scope)
3. Add new Step/Substep (based on learnings)
4. Reorder Steps (change priorities)
5. Update success criteria (adjust targets based on execution)
6. Review and adjust (general refinement session)

Enter number (1-6):
```

---

### Step 3: Load Substep-Specific Context (If Option 1)

**Human selects: "Refine STEP_0_3 (Rebuild Engine Core)"**

**Usher loads additional context:**

```
8. STEP_0_1 COMPLETION_SUMMARY (~800 lines, ~8K tokens, 8min)
   Why: Audit Engine is related (both tools, might share patterns)

9. STEP_0_2 START_HERE.md (if exists - ~1,200 lines, ~12K tokens, 10min)
   Why: Site Cloner is directly related (Rebuild Engine uses Cloner output)

10. STEP_0_3 current definition from steps/STEP_0.md (or relevant step file)
    Already loaded, re-read specific section (2min)

Total additional: ~2,000 lines, ~20K tokens, 20min

Running total: ~97K tokens (still under 100K)
```

---

### Step 4: Collaborative Refinement Session

**Usher asks questions to improve specificity:**

```
Current STEP_0_3 definition:

#### STEP_0_3: Build Rebuild Engine Core
**Target:** Vertical-agnostic engine + contractor template
**Timeline:** 2 weeks
**Focus:** Foundation for multi-vertical platform

Let's make this more specific. I'll ask questions to refine.

---

Q1: What exactly is "Rebuild Engine Core"?

Based on research:
- Site Cloner (STEP_0_2) extracts content from sites
- Rebuild Engine transforms extracted content into modern Next.js sites
- "Core" means: Template system, component library, generation logic

Should substep be:
A) "Build template system (vertical-agnostic core + contractor template)"
B) "Build generation engine (content → Next.js) + contractor template"
C) "Build component library (universal) + template config system + contractor template"

[Human chooses or refines]

---

Q2: What are the specific deliverables?

Current says: "Vertical-agnostic engine + contractor template"

More specific would be:
"Deliverables:
1. Universal component library (Button, Hero, Services, Contact, Footer - works for any vertical)
2. Template configuration system (CLI tool: select vertical → applies vertical template)
3. Contractor template (blue/orange colors, trust-focused copy, lead-gen CTAs)
4. Generation engine (takes Site Cloner output + template → generates Next.js project)
5. Validation: Generated site builds without errors, matches design intent"

Is this correct? What would you add/change?

[Human refines]

---

Q3: What are the success criteria?

Current: Generic

More specific:
"Success criteria:
- Component library: 15-20 universal components (proven on Audit Engine, Site Cloner)
- Template system: Can switch contractor ↔ law ↔ healthcare via config file
- Contractor template: Tested on 3 contractor sites (HVAC, plumbing, electrical)
- Generation engine: Takes Cloner JSON → produces Next.js project in <30 seconds
- Output quality: Generated site Lighthouse 90+, WCAG AA, builds without errors
- Multi-vertical proof: Same component library works for all 3 verticals"

Does this capture requirements? Anything missing?

[Human confirms or adds]

---

Q4: How should this be broken into substeps?

Current: One substep (STEP_0_3)

Could be split:
- STEP_0_3_1: Build universal component library
- STEP_0_3_2: Build template config system
- STEP_0_3_3: Build contractor template + validate

Or stay as one:
- STEP_0_3: All in one (component library + template system + contractor template)

Given 2 week estimate, is one substep manageable or should we split?

[Human decides]

---

Q5: What risks should we call out?

From STEP_0_1, STEP_0_2 learnings:
- Template system complexity (could over-engineer - keep simple)
- Contractor-specific assumptions (test universality early)
- Component library scope creep (limit to 15-20, not 50)

Should document:
"Risks:
- Over-engineering template system (mitigation: start with 2 verticals, not 5)
- Contractor bias in 'universal' components (mitigation: test on law firm mock in CP3)
- Scope creep on components (mitigation: hard cap at 20 components, defer extras)"

Anything else?

[Human adds risks]
```

**Usher helps structure thinking, not just transcribe.**

---

### Step 5: Update ATLAS_STEPS_PARTX.md

**Usher drafts update:**

```markdown
#### STEP_0_3: Build Rebuild Engine Core

**Status:** ⏸️ PLANNED
**Timeline:** 2 weeks (estimated)
**Focus:** Multi-vertical foundation (universal components + template system + contractor template)

**Objective:**
Build the core Rebuild Engine: universal component library (works for any vertical), template configuration system (select vertical → apply template), and contractor template (first vertical validation).

**Deliverables:**
1. **Universal Component Library** (15-20 components)
   - Button, Hero, Services, About, Contact, Footer, Card, Form, etc.
   - Works for contractor, law, healthcare (vertical-agnostic)
   - Accessible (WCAG AA), performant (<2s), responsive

2. **Template Configuration System** (CLI tool or config file)
   - Input: Vertical selection (contractor / law / healthcare)
   - Output: Applies vertical-specific colors, copy, CTAs
   - Easily extensible (add new vertical = add config file)

3. **Contractor Template** (first vertical)
   - Colors: Blue/orange (trust-focused)
   - Copy: Lead generation emphasis ("Get more calls, more jobs")
   - CTAs: Phone click-to-call, contact forms
   - Tested on: 3 contractor sites (HVAC, plumbing, electrical)

4. **Generation Engine** (content → Next.js)
   - Input: Site Cloner output JSON (from STEP_0_2)
   - Process: Component library + template config → Next.js project
   - Output: Deployable Next.js site (builds without errors)
   - Performance: <30 second generation time

**Success Criteria:**
- [ ] 15-20 universal components built and tested
- [ ] Template config system works (switch contractor ↔ law ↔ healthcare)
- [ ] Contractor template validated (tested on 3 contractor sites)
- [ ] Generation engine works (Cloner output → Next.js project)
- [ ] Output quality: Lighthouse 90+, WCAG AA, builds clean
- [ ] Multi-vertical proof: Components work for all 3 verticals (tested with mock law/healthcare)

**Could split into sub-substeps if needed:**
- STEP_0_3_1: Component library
- STEP_0_3_2: Template system + contractor template
- STEP_0_3_3: Generation engine + validation

**Decision:** Keep as one substep (2 weeks manageable, logical unit)

**Risks:**
- Template system over-engineering (mitigation: start simple, 2 verticals only)
- Contractor assumptions in "universal" components (mitigation: test on law mock early)
- Scope creep (mitigation: hard cap 20 components, defer extras to future)

**Dependencies:**
- Requires: STEP_0_2 complete (Site Cloner provides input data format)
- Enables: STEP_1_X (customer delivery uses Rebuild Engine)

**Hypotheses:**
- H1: Universal components can serve contractor, law, healthcare (test in CP validation)
- H2: Template config approach is flexible enough (vs hardcoded per vertical)

**Updated:** 2025-12-11 (refined with Usher Mode 2)
**Reason:** Made outcomes very specific (was vague), added risks, clarified success criteria
```

**Usher asks: "Review this update. Approve? (yes/no/edit)"**

**If yes:**
- Usher saves update to steps/STEP_0.md (or relevant step file)
- Commits change
- Logs decision in DECISION_LOG.md (refinement rationale)

**If edit:**
- Human provides feedback
- Usher refines
- Iterate until approved

---

### Step 6: Document Decision (Auto)

**Usher adds to DECISION_LOG.md:**

```markdown
## 2025-12-11: Refined STEP_0_3 Definition (Rebuild Engine)

**Context:** STEP_0_3 was vague ("Build rebuild engine core"). Before AI1 starts research, refined with human to make very specific.

**Changes made:**
- Added specific deliverables (4 distinct outputs: components, template system, contractor template, generation engine)
- Added measurable success criteria (15-20 components, Lighthouse 90+, multi-vertical validated)
- Added risks (over-engineering, contractor bias, scope creep) with mitigations
- Clarified dependencies (needs STEP_0_2 Cloner output format)

**Rationale:**
- Vague substeps waste AI1 time (research what's already decided)
- Specific substeps enable focused research (AI1 validates approach, doesn't define scope)
- Early risk identification prevents issues during execution

**Impact:**
- STEP_0_3 now ready for AI1 (can research patterns, not define scope)
- AI2 will have clearer planning inputs
- AI3 will have precise targets

**Approved by:** Ryan (human)
**Updated by:** Usher (Mode 2)
```

---

## Workflow Summary

**Mode 2 process:**
1. Load strategy context (~50min, ~77K tokens)
2. Present current state (Steps, substeps, progress)
3. Ask what to refine (substep, Step, criteria, etc.)
4. Load specific context for selected item
5. Collaborative Q&A (Usher asks, human answers, refine together)
6. Draft update to ATLAS_STEPS_PARTX.md
7. Human approves/edits
8. Usher saves update, commits
9. Usher logs decision in DECISION_LOG.md
10. Report refinement complete

**Key value:**
- Prevents vague substeps from wasting AI time
- Enables mid-flight strategy adjustment (learnings inform changes)
- Collaborative (Usher helps structure, doesn't dictate)
- Documented (updates logged, rationale captured)

---

## When to Use Mode 2

**Use when:**
- Substep is vague (before AI1 starts - make specific)
- Learnings invalidate current plan (mid-flight pivot)
- Success criteria need adjustment (targets were wrong)
- Step needs restructuring (split differently, reorder)
- Adding new Step/Substep (based on discoveries)

**Don't use when:**
- Just want status (use Mode 4 - Overview)
- Continuing execution (use Mode 1 - Auto-Resume)
- Strategy is clear (no refinement needed)

---

**This mode keeps strategy aligned with reality. 5% usage but high impact.**
