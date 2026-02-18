# Mode 4: Overview & Framework AMA - Status + Answer Questions

**Purpose:** Show holistic progress + answer framework questions
**Usage:** ~2% (status checks, onboarding, understanding system)
**Trigger:** Human says "Show ATLAS overview" or "Explain how ATLAS works"

---

## What This Mode Does

**Two functions:**

**A) Overview (Status Reporting):**
- Scan all ATLAS_STEPS files (show progress)
- Show current work (active Efforts)
- Show completed work (with outcomes)
- Show what's next (planned substeps)
- Table of contents view (hierarchical)

**B) Framework AMA:**
- Answer "how does X work?" questions
- Explain mechanics (who creates TODO_TRACKER? who updates it?)
- Clarify ownership (which AI does what? when?)
- Reference documentation (point to relevant guides)

---

## Files Usher Loads

### For Overview (Status Display)

```
1. All ATLAS_STEPS files (~50K tokens, 20min)
   - ATLAS_STEPS_TRACKER.md
   - steps/STEP_1.md, STEP_2.md, STEP_3.md (relevant step files)

2. All Effort status (scan effort.md files - ~10K tokens, 10min)
   - Find all efforts/STEP_*/effort.md
   - Extract status (PLANNED, IN_PROGRESS, COMPLETE)

3. Active Effort details (if any IN_PROGRESS - ~15K tokens, 8min)
   - TODO_TRACKER.md (CP progress)
   - OUTLINE.md (CP structure)

Total: ~75K tokens, ~40min
```

### For AMA (Framework Questions)

```
Additional context for answering mechanics:

4. ATLAS_SPECIFICATION.md (~40K tokens, 20min)
   Purpose: Technical workflow details

5. Role guides (as needed - ~20K tokens, 10min per guide)
   - roles/AI1_RESEARCHER_GUIDE.md
   - roles/AI2_GUIDE_CREATOR_GUIDE.md
   - roles/AI3_IMPLEMENTER_GUIDE.md

6. Templates (as needed - ~15K tokens, 5min per template)
   - START_HERE_TEMPLATE.md
   - TODO_TRACKER_TEMPLATE.md
   - etc.

Loaded on-demand based on questions asked
```

---

## Workflow A: Overview Display

### Present Hierarchical Status

```markdown
# ATLAS Status Overview - your company

**Last updated:** 2025-12-20 14:30
**Overall progress:** 4 of 10 Steps complete (40%)

---

## PART 1: FOUNDATION (Steps -1 through 2)

### STEP -1: Platform Setup ✅ COMPLETE
**Completed:** 2025-12-10
**Duration:** 2 days
**Outcome:** Git monorepo, Vercel team, Supabase project initialized
**Details:** efforts/STEP_-1_PLATFORM_SETUP/COMPLETION_SUMMARY.md

---

### STEP 0: Build Core Tools (IN_PROGRESS - 2 of 3 complete)

#### STEP_0_1: Build Audit Engine ✅ COMPLETE
**Completed:** 2025-12-15
**Duration:** 7 days
**Outcome:** audit.10xbuild.com live, tested across 3 verticals
**Metrics:** 47 audits run in first week, 12 leads captured
**Learnings:** Multi-tenant architecture validated, PageSpeed rate limits hit (upgraded to paid)

#### STEP_0_2: Build Site Cloner 🔄 IN_PROGRESS
**Started:** 2025-12-16
**Progress:** CP3 of 5 (60% complete)
**Current:** AI3 executing CP3 (Site Generation)
**Est. completion:** 2025-12-20 (2 days remaining)
**Details:** efforts/STEP_0_2_SITE_CLONER/TODO_TRACKER.md

#### STEP_0_3: Build Rebuild Engine Core ⏸️ PLANNED
**Timeline:** 2 weeks (after STEP_0_2)
**Waiting on:** STEP_0_2 completion (needs Cloner output format)

---

### STEP 1: Validate on Contractors (PLANNED - 0 of 10 complete)

#### STEP_1_1: First Contractor ⏸️ PLANNED
**Timeline:** 1 week (after STEP_0_3)
**Deliverable:** First customer site using full Rebuild Engine

#### STEP_1_2 through STEP_1_10: Next 9 Contractors ⏸️ PLANNED
**Timeline:** 6-8 weeks total (faster with patterns)
**Purpose:** Validate contractor template at scale

---

### STEP 2: Build 10xbuild.com ⏸️ PLANNED
**Timeline:** 1 week
**Deliverable:** Company website showcasing first 3 customers

---

## PART 2: SCALE (Steps 3-5) - All PLANNED

### STEP 3: Scale Contractors (10 → 25) ⏸️
**Timeline:** 8-12 weeks
**Purpose:** Prove contractor vertical scales

### STEP 4: Add Law Firm Vertical ⏸️
**Timeline:** 4-6 weeks
**Purpose:** Prove engine generalizes (multi-vertical validation)

### STEP 5: Launch Inspector SaaS ⏸️
**Timeline:** 3-4 weeks
**Purpose:** Productize Audit Engine (first SaaS product)

---

## PART 3: PLATFORM (Steps 6-10) - Loosely Defined

Steps 6-10 will be defined after Part 2 learnings.

Likely areas:
- Add healthcare vertical
- Platform features (multi-site management, API, white-label)
- Scale to 50-100 customers across all verticals

---

## Summary

**Completed:**
- 1 Step fully complete (STEP -1)
- 2 substeps complete (Platform Setup, Audit Engine)
- ~4% of total substeps

**In Progress:**
- 1 Effort active (Site Cloner, 60% done)

**Next Up:**
- Complete Site Cloner (2 days)
- Start Rebuild Engine (2 weeks)
- First customer delivery (1 week after that)

**Trajectory:**
- On track for Part 1 completion by Month 3
- On track for first customers by Month 4
- Platform foundation solid (tools working, patterns proven)
```

---

## Workflow B: Framework AMA

**Human can ask questions, Usher answers with references.**

### Example Q&A:

**Q: "Who creates TODO_TRACKER?"**

**A:**
```
TODO_TRACKER.md ownership:

**Created by:** AI2 (during planning phase)
- When: After all CP guides are created
- Location: efforts/STEP_X_Y/TODO_TRACKER.md
- Initial state: All CPs marked ⏸️ PENDING
- Template: templates/TODO_TRACKER_TEMPLATE.md

**Updated by:** AI3 (after each checkpoint)
- When: After completing CP0, CP1, ..., CPX
- Updates: Mark CP ✅ COMPLETE, add date/duration/notes, update current CP pointer
- Commits: After each update

**Read by:**
- AI3 (every time resuming work - knows what's done)
- Framework (auto-detection - finds current CP)
- Human (status checking - detailed progress)

**Purpose:** Track CP-level progress, enable exact resume

**See:** templates/TODO_TRACKER_TEMPLATE.md (structure)
**See:** roles/AI2_GUIDE_CREATOR_GUIDE.md (creation process)
**See:** roles/AI3_IMPLEMENTER_GUIDE.md (update process)
```

---

**Q: "What's the difference between OUTLINE and OVERVIEW_GUIDE?"**

**A:**
```
Both created by AI2, different purposes:

**OUTLINE.md:**
- **When created:** Early in AI2 phase (before detailed guides)
- **Purpose:** High-level CP map (planning document)
- **Audience:** Human (review/approve plan before AI2 spends 12 hours on guides)
- **Contents:** CP list, rationale for count, dependencies, testing strategy
- **Length:** 200-400 lines
- **Used for:** Human approval checkpoint, AI2 reference during guide creation

**OVERVIEW_GUIDE.md:**
- **When created:** Late in AI2 phase (after all guides done)
- **Purpose:** Quick-start for AI3 (execution document)
- **Audience:** AI3 (get up to speed in 5 minutes before reading detailed guides)
- **Contents:** What we're building, CP sequence (1-2 sentences per CP), key watchouts, testing strategy
- **Length:** 300-600 lines
- **Used for:** AI3's first read when starting Effort

**Analogy:**
- OUTLINE = Blueprint review (architect shows plan to client before building)
- OVERVIEW_GUIDE = Construction site orientation (foreman shows builder the plan)

**See:** templates/OUTLINE_TEMPLATE.md
**See:** templates/OVERVIEW_GUIDE_TEMPLATE.md
```

---

**Q: "How does auto-detection work?"**

**A:**
```
Auto-detection determines state from file existence:

**Process:**
1. Find Effort directory (efforts/STEP_X_Y_[NAME]/)
2. Check files in sequence:
   - START_HERE.md exists? → AI1 done, else AI1 needed
   - OUTLINE.md exists? → AI2 started, else AI2 needed
   - All guides exist? (count vs OUTLINE) → AI2 done, else AI2 in progress
   - TODO_TRACKER exists? → AI2 complete, else AI2 final task
   - Read TODO_TRACKER → Find PENDING CP → AI3 phase, execute that CP

**Example:**
  Files found: START_HERE ✅, OUTLINE ✅, 5 guides ✅, TODO_TRACKER ✅
  TODO_TRACKER shows: CP0-2 ✅, CP3 ⏸️
  Detection: AI3 phase, current CP is CP3
  Action: Load AI3 context for CP3, begin execution

**Why file-based:**
- Files persist (survives session ends)
- Can't lose state (files are state)
- Easy to debug (examine files)
- Audit trail (files show history)

**See:** modes/MODE1_AUTO_RESUME.md (complete algorithm)
**See:** ATLAS_SPECIFICATION.md (state machine design)
```

---

**Q: "What files does AI1 read and in what order?"**

**A:**
```
AI1 research phase context loading:

**Order (important - load in this sequence):**
1. AI1_RESEARCHER_GUIDE.md (your role)
2. ATLAS_STEPS_PARTX.md (relevant Step section - substep definition)
3. Previous COMPLETION_SUMMARY.md (if exists - what was built)
4. COMPANY_CONTEXT.md (vision, constraints)
5. LEARNINGS_LOG.md (last 10-15 relevant entries)
6. ATLAS_ASSUMPTIONS.md (if filled - constraints)
7. Existing research (if any - ask human)

**Total:** 8-12 files, ~35K tokens, ~35 minutes

**Why this order:**
- Role first (understand your job)
- Substep definition (understand what to research)
- Previous work (build on, don't duplicate)
- Company context (constraints, vision)
- Learnings (patterns to apply)

**What AI1 does NOT load:**
- AI2 or AI3 guides (not your role)
- GIT_WORKFLOW.md (you don't implement)
- Templates (you use START_HERE template only)
- Other Steps (load relevant section only)
- All LEARNINGS (recent relevant only)

**See:** roles/AI1_RESEARCHER_GUIDE.md (section: Context You Load)
**See:** context/CONTEXT_INDEX.md (AI1 loading rules)
```

---

## Drill-Down Capability

**Human can drill into completed Efforts:**

```
"Show me details on STEP_0_1 (Audit Engine)"

Usher loads:
- efforts/STEP_0_1_AUDIT_ENGINE/COMPLETION_SUMMARY.md
- Presents: What was built, decisions, metrics, learnings

"What decisions were made in STEP_0_1?"

Usher shows:
- Decision section from COMPLETION_SUMMARY
- Plus any DECISION_LOG entries referencing STEP_0_1

"What did we learn from STEP_0_1?"

Usher shows:
- "What Worked" and "What Didn't Work" sections
- Tactical learnings (from COMPLETION_SUMMARY)
- Strategic learnings (from LEARNINGS_LOG entries tagged STEP_0_1)
```

**Conversational exploration of completed work.**

---

## When to Use Mode 4

**Use when:**
- Want holistic progress view (where are we overall?)
- Need to answer "what's next?" (show planned substeps)
- Learning ATLAS (understand how framework works)
- Onboarding teammate (explain mechanics)
- Reviewing completed work (show outcomes)

**Don't use when:**
- Want to continue work (use Mode 1)
- Want to refine strategy (use Mode 2)
- Need to execute (use Mode 1 or 3)

---

**This mode provides visibility and understanding. Low usage but high clarity.**
