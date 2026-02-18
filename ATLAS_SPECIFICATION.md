# ATLAS v2.0 - Complete Workflow Specification

**Purpose:** Definitive specification of correct ATLAS workflow
**Status:** Master specification - all files built from this
**Created:** 2025-12-11
**For:** ATLAS framework developers

---

## Critical Principle

**ATLAS orchestrates three sequential AI phases (not checkpoint-based roles):**

```
AI1 Phase (Research entire substep) →
AI2 Phase (Plan execution with guides) →
AI3 Phase (Execute all checkpoints)
```

**Not:** AI1 executes CP0, AI3 executes CP1-3
**But:** AI1 researches before Effort, AI2 plans Effort, AI3 executes all CPs

---

## The Correct Three-Phase Workflow

### **Phase 1: AI1 Research (Substep-Level, Pre-Effort)**

**Trigger:** Substep defined in ATLAS_STEPS.md, no START_HERE.md exists yet

**Invocation:**
```
Human: "Run ATLAS to research STEP_1_2"
OR
Human: "Continue ATLAS on STEP_1_2" (framework auto-detects no START_HERE → AI1 phase)
```

**Context AI1 Loads (in order):**
1. ATLAS_OVERVIEW.md (skim - 2min)
2. ATLAS_GLOSSARY.md (reference - 1min)
3. AI1_RESEARCHER_GUIDE.md (role guide - 10min first time, 3min after)
4. ATLAS_STEPS.md (STEP_1 section only, read Substep 1.2 specifically - 3min)
5. Previous substep COMPLETION_SUMMARY.md (if exists - STEP_1_1_COMPLETE.md - 5min)
6. Company CONTEXT.md (your company_CONTEXT.md - 8min)
7. LEARNINGS_LOG.md (last 10-15 entries relevant to domain - 5min)
8. Any research already done by human/META (if exists - variable)

**Total: ~35-45 minutes context loading, 3-8 hours research**

**AI1 Process:**

**Step 1: Understand Scope (30-60 min)**
- What is this substep trying to accomplish? (read from ATLAS_STEPS.md)
- How specific is the substep definition? (vague "build engine" vs specific "build with these exact features")
- What did previous substep accomplish? (read COMPLETION_SUMMARY if exists)
- What constraints apply? (from company CONTEXT and ATLAS_ASSUMPTIONS)

**Step 2: Deep Research (2-6 hours, varies by specificity)**

**If substep is vague** (e.g., "Build Audit Engine"):
- 80% research: Competitive analysis, technical options, architecture patterns
- What exists? (inspect.dev, GTMetrix, PageSpeed, other audit tools)
- How do they work? (APIs, scoring, reporting)
- What can we learn/copy? (patterns, approaches, gotchas)
- What should we build? (make MORE specific than substep definition)

**If substep is specific** (e.g., "Build Audit Engine with PageSpeed API, Supabase multi-tenant, generates PDF reports"):
- 20% validation research: Is this approach sound? Any gotchas?
- Validate assumptions (PageSpeed rate limits? Supabase RLS patterns?)
- Find examples (who else has done this? what patterns work?)
- Identify risks (what could go wrong?)

**Step 3: Rough CP Breakdown (30-60 min)**
- How many phases does this work have? (3-10 typically)
- What's always first? (CP0: setup/infrastructure)
- What's always last? (CPX: testing/deployment/completion)
- What's in between? (implementation phases)
- Rough guess at order (AI2 will refine)

**Step 4: Create START_HERE.md (1-2 hours)**

**AI1 Outputs:**

**Primary deliverable:**
- `/efforts/STEP_1_2_[NAME]/START_HERE.md`

**Structure:**
```markdown
# Start Here - STEP_1_2 [Substep Name]

**Substep:** STEP_1_2 from ATLAS_STEPS.md
**Researched by:** AI1
**Date:** [Date]
**Research Duration:** [X hours]

---

## Context

**What this substep builds:**
[2-3 paragraphs: What we're building, why, who for]

**Specificity level:**
[How specific was the substep definition? Did we need heavy research or just validation?]

**Previous substep context:**
[If STEP_1_1 happened, what did it build? What can we reuse? What did we learn?]

---

## Implementation Outcomes (Very Specific)

**Must deliver:**
1. [Specific outcome 1 - more detailed than substep definition]
   - Feature: [Exact feature]
   - Quality bar: [Performance target, accessibility requirement]
   - Integration: [What it connects to]

2. [Specific outcome 2]
   [Same specificity]

3. [Specific outcome 3]

**Example:**
NOT: "Build audit tool"
BUT: "Multi-tenant audit tool with API integration, scoring A-F, PDF export, email delivery, works across customer segments, <2min analysis time"

---

## Research Findings

### Competitive Analysis
[What exists, strengths/weaknesses, gaps we can fill]

### Technical Approach
**Recommended stack:**
[Specific technologies with rationale]

**Architecture:**
[High-level system design]

**Alternatives considered:**
[What else we could do, why not recommended]

### Design Patterns
[UI/UX patterns researched, what works for this domain]

### Integration Requirements
[What needs to connect to what, APIs, services]

---

## Rough Checkpoint Breakdown (AI2 will refine)

**Estimated 4-6 checkpoints for this Effort:**

**CP0: Infrastructure Setup** (~4 hours)
- Git repo init (if new), Vercel project, Supabase project
- Database schema (3 tables: audits, customers, reports)
- Environment vars, deployment validation

**CP1: Core Analysis Engine** (~2 days)
- PageSpeed API integration
- Scoring algorithm (metrics → A-F grade)
- Multi-segment support (test across customer types)

**CP2: Report Generation** (~2 days)
- Puppeteer PDF rendering
- Professional report template design
- Email delivery integration

**CP3: Testing & Deployment** (~1 day)
- Test across 10 diverse sites
- Performance validation
- Deploy to tool.yourdomain.com
- Documentation

**NOTE:** AI2 may adjust to 3 CPs (combine CP1-2) or 7 CPs (split further). This is guidance.

---

## For AI2 (What to research when creating guides)

**CP0 (Setup) guide needs:**
- Vercel monorepo setup patterns (research docs, examples)
- Database multi-tenant patterns (check previous projects or documentation for examples)
- Database schema (audits table structure, indexes)

**CP1 (Analysis) guide needs:**
- PageSpeed API integration (rate limits: 100/day free, pagination, error handling)
- Scoring algorithm design (how to combine 6 metrics into A-F grade?)
- Multi-vertical testing approach (ensure works for contractor, law, healthcare)

**CP2 (Reports) guide needs:**
- Puppeteer on Vercel (memory config: 1GB, cold start issues)
- PDF template design (professional layout, branding)
- Email delivery (Resend integration, template rendering)

**CP3 (Testing) guide needs:**
- Cross-vertical validation (test on 3+ different business types)
- Performance benchmarks (can handle 50 audits/hour?)
- Monitoring setup (error tracking, usage analytics)

---

## Risks & Gotchas

**Risk 1:** PageSpeed API rate limits
- Free tier: 100/day (might hit during testing)
- Mitigation: Caching OR paid tier ($200/mo for 25K)

**Risk 2:** Puppeteer memory on Vercel
- Default 1024MB might not be enough for complex PDFs
- Solution: Configure function memory to 1024MB in vercel.json

**Risk 3:** Multi-vertical scoring calibration
- What's "good" for contractor might differ from law firm
- Solution: Vertical-specific score adjustments

---

## Next Steps

**For AI2:**
1. Read this START_HERE thoroughly
2. Validate research (spot-check findings)
3. Create OUTLINE (decide if 4-6 CPs is right)
4. Research each CP deeply
5. Create detailed guides
6. Create OVERVIEW_GUIDE
7. Create TODO_TRACKER

**Timeline:** AI2 should spend 8-12 hours planning this Effort (complex substep)

---

**End of START_HERE.md**
```

**Completion markers:**
- START_HERE.md exists → AI1 phase complete
- Framework detects: Time for AI2 planning phase

---

### **Phase 2: AI2 Planning (Effort-Level Guide Creation)**

**Trigger:** START_HERE.md exists, no OUTLINE.md or guides exist yet

**Invocation:**
```
Human: "Continue ATLAS on STEP_1_2" (framework detects START_HERE exists → AI2 phase)
OR
Human: "Run ATLAS to plan Effort for STEP_1_2"
```

**Context AI2 Loads (in order):**
1. ATLAS_OVERVIEW.md (skim - 2min)
2. ATLAS_GLOSSARY.md (reference - 1min)
3. AI2_GUIDE_CREATOR_GUIDE.md (role guide - 15min first time, 5min after)
4. START_HERE.md from AI1 (deep read - 10-15min)
5. ATLAS_STEPS.md (relevant Step section - 3min)
6. Previous substep COMPLETION_SUMMARY (if exists - 5min)
7. Company CONTEXT.md (8min)
8. LEARNINGS_LOG.md (last 10-15 entries - 5min)
9. DECISION_LOG.md (last 5-10 entries - 3min)
10. Previous similar Effort structure (if exists - 5min)
11. Checkpoint guide templates (reference - 10min)

**Total: ~60-80 minutes context loading, 8-12 hours planning/guide creation**

**AI2 Process:**

**Step 1: Validate AI1's Research (30-60 min)**
- Read START_HERE.md thoroughly
- Spot-check key findings (is recommended stack sound?)
- Confirm outcomes are specific enough (or make more specific)
- Identify gaps (what did AI1 miss?)

**Step 2: Create OUTLINE (1 hour)**

**File:** `/efforts/STEP_1_2_[NAME]/OUTLINE.md`

**Contents:**
```markdown
# Outline - STEP_1_2 [Name]

**Effort:** Build [what]
**Total Checkpoints:** 5 (AI2 decision)
**Estimated Duration:** 1 week

---

## Checkpoint Breakdown

**CP0: Infrastructure Setup** (AI3, 4 hours)
- Git/Vercel/Supabase initialization
- Database schema deployment
- Environment configuration

**CP1: Core Functionality** (AI3, 2 days)
- [Main feature implementation]

**CP2: Secondary Features** (AI3, 2 days)
- [Supporting features]

**CP3: Polish & Optimization** (AI3, 1 day)
- Performance tuning, UI polish

**CP4: Testing & Deployment** (AI3, 1 day)
- Comprehensive testing, staging, production

---

## Rationale for 5 CPs

[Why 5 and not 3 or 7? What's the logic for splitting work this way?]

---

## Testing Strategy

- After each CP: Unit tests, build validation
- CP4: Comprehensive E2E, performance, accessibility, cross-vertical

---

## Key Dependencies

- CP1 needs CP0 (can't build features without infrastructure)
- CP3 needs CP1-2 (optimization requires features to exist)
- CP4 is final gate (all must be done before this)
```

**Step 3: Research CP0 Deeply (1-2 hours)**
- What does setup entail for THIS specific Effort?
- Git structure (monorepo? standalone? copy from where?)
- Vercel config (team account, project settings, environment vars)
- Supabase (tables needed, RLS policies, initial data)
- Reference examples (previous projects, documentation)
- Document exact commands, exact steps

**Step 4: Create CP0_GUIDE.md (1 hour)**

**File:** `/efforts/STEP_1_2_[NAME]/guides/CP0_GUIDE.md`

**Contents:**
```markdown
# CP0 Guide - Infrastructure Setup

**Role:** AI3 (Implementer)
**Goal:** Initialize all technical infrastructure for Audit Engine
**Duration:** 4 hours
**Type:** Setup/Initialization (not research)

---

## What This Is

CP0 is ALWAYS infrastructure and environment setup.
NOT research (that was AI1's job, documented in START_HERE.md).

This checkpoint prepares the technical foundation so CP1-4 can build features.

---

## Pre-Flight (AI3 reads before starting)

**Required reading:**
1. START_HERE.md (AI1's research - 10 min)
2. OVERVIEW_GUIDE.md (effort summary - 3 min)
3. THIS file (CP0_GUIDE.md - 5 min)
4. AI3_IMPLEMENTER_GUIDE.md (role refresher - 3 min if needed)
5. GIT_WORKFLOW.md (git procedures - 3 min if needed)

**Git sync validation:**
```bash
git fetch origin
git checkout main && git pull origin main
git checkout staging && git pull origin staging
git diff main staging  # Should match or document divergence
```

---

## Tasks

### Task 1: Create Effort Git Branch (10 min)
```bash
git checkout staging
git checkout -b effort/STEP_1_2_AUDIT_ENGINE
git push -u origin effort/STEP_1_2_AUDIT_ENGINE
```

### Task 2: Initialize Vercel Project (30 min)
[Exact steps based on research]

### Task 3: Create Supabase Project (30 min)
[Exact steps with schema]

### Task 4: Configure Environment (20 min)
[Exact .env setup]

### Task 5: Validate Deployment (30 min)
[Test build/deploy works]

---

## Outputs

- Git branch created: effort/STEP_1_2_AUDIT_ENGINE
- Vercel project: audit-engine
- Supabase project: [platform-name]
- Database schema deployed
- .env.local configured
- Initial deployment successful (test URL works)
- README.md with setup notes

---

## Success Criteria

- [ ] Git branch exists and pushed
- [ ] Vercel project deploying successfully
- [ ] Supabase tables created (run: \dt in psql)
- [ ] Build succeeds: npm run build
- [ ] Dev server runs: npm run dev
- [ ] Can access deployed URL

---

## Update TODO_TRACKER

After completing CP0:
```markdown
## CP0: Infrastructure Setup ✅ COMPLETE
**Completed:** [Date]
**Duration:** [Actual hours]

- [x] Git branch created
- [x] Vercel project initialized
- [x] Supabase database ready
- [x] Environment configured
- [x] Deployment validated

**Next:** CP1 (Core Analysis Engine)
```

---

## Next Checkpoint

Read CP1_GUIDE.md (Core Analysis Engine)
Estimated: 2 days implementation
```

**Step 5: Research CP1 Deeply (2-3 hours)**
[Repeat research process for CP1 specifics]

**Step 6: Create CP1_GUIDE.md (1 hour)**
[Same structure as CP0, tailored to CP1 implementation]

**Step 7-X: Repeat for all CPs**
[Research → Create guide, for each checkpoint]

**Final Steps: Create Supporting Docs**

**Step X+1: Create OVERVIEW_GUIDE.md (30-45 min)**

**File:** `/efforts/STEP_1_2_[NAME]/OVERVIEW_GUIDE.md`

```markdown
# Overview Guide - STEP_1_2 Audit Engine

**Quick-Start Guide for AI3**

**What:** Multi-tenant website audit tool (works for any SMB vertical)
**Duration:** 1 week (5 checkpoints)
**Tech:** Next.js + Supabase + PageSpeed API + Puppeteer

---

## Checkpoint Sequence

1. **CP0:** Setup (4h) - Infrastructure initialization
2. **CP1:** Core Analysis (2d) - PageSpeed integration, scoring
3. **CP2:** Reports (2d) - PDF generation, email delivery
4. **CP3:** Polish (1d) - UI/UX, multi-vertical testing
5. **CP4:** Deploy (1d) - Testing, staging, production

---

## Key Things to Watch

- PageSpeed API: 100/day free tier (might hit limit)
- Puppeteer: Needs 1GB memory on Vercel
- Multi-vertical: Test on contractor, law, healthcare sites

---

## Testing Strategy

After each CP: Build + unit tests
CP4: Comprehensive (10+ site types, performance, accessibility)

---

## Quick Reference

- Research: /START_HERE.md
- CP Guides: /guides/CP0_GUIDE.md through CP4_GUIDE.md
- Progress: /TODO_TRACKER.md
```

**Step X+2: Create TODO_TRACKER.md (15-30 min)**

**File:** `/efforts/STEP_1_2_[NAME]/TODO_TRACKER.md`

```markdown
# TODO Tracker - STEP_1_2 Audit Engine

**Effort:** STEP_1_2_AUDIT_ENGINE
**Status:** PLANNED (not started)
**Total CPs:** 5
**Completed:** 0
**Current:** None (awaiting AI3)
**Last Updated:** [Date by AI2]

---

## Checkpoint Progress

### CP0: Infrastructure Setup ⏸️ PENDING
**Goal:** Initialize Vercel + Supabase + git
**Estimated:** 4 hours
**Status:** Not started
**Started:** N/A
**Completed:** N/A

### CP1: Core Analysis Engine ⏸️ PENDING
**Goal:** PageSpeed integration, scoring algorithm
**Estimated:** 2 days
**Dependencies:** CP0 complete

### CP2: Report Generation ⏸️ PENDING
**Goal:** PDF rendering, email delivery
**Estimated:** 2 days
**Dependencies:** CP1 complete

### CP3: Polish & Multi-Vertical ⏸️ PENDING
**Goal:** UI polish, test on 3 verticals
**Estimated:** 1 day
**Dependencies:** CP2 complete

### CP4: Testing & Deployment ⏸️ PENDING
**Goal:** Comprehensive testing, production launch
**Estimated:** 1 day
**Dependencies:** CP0-3 complete

---

## Notes

[AI3 adds notes here as work progresses]

---

## Blockers

[AI3 documents any blockers here]

---

**AI3: Update this file after completing each CP. Mark with ✅ COMPLETE and date.**
```

**Step X+3: Create effort.md (if not exists) (15 min)**
[High-level overview, links to guides]

**AI2 Completion:**

**Outputs produced:**
- `/efforts/STEP_1_2_[NAME]/START_HERE.md` (exists from AI1)
- `/efforts/STEP_1_2_[NAME]/OUTLINE.md` (created by AI2)
- `/efforts/STEP_1_2_[NAME]/OVERVIEW_GUIDE.md` (created by AI2)
- `/efforts/STEP_1_2_[NAME]/guides/CP0_GUIDE.md` (created by AI2)
- `/efforts/STEP_1_2_[NAME]/guides/CP1_GUIDE.md` (created by AI2)
- `/efforts/STEP_1_2_[NAME]/guides/CP2_GUIDE.md` (created by AI2)
- `/efforts/STEP_1_2_[NAME]/guides/CP3_GUIDE.md` (created by AI2)
- `/efforts/STEP_1_2_[NAME]/guides/CP4_GUIDE.md` (created by AI2)
- `/efforts/STEP_1_2_[NAME]/TODO_TRACKER.md` (created by AI2)
- `/efforts/STEP_1_2_[NAME]/effort.md` (created by AI2)

**Completion marker:**
- All guides exist (CP0 through CPX)
- TODO_TRACKER exists
- OVERVIEW_GUIDE exists
- Framework detects: Time for AI3 execution phase

**AI2 reports:**
```
AI2 planning complete for STEP_1_2_AUDIT_ENGINE.

Structure created:
- 5 checkpoints defined (CP0 setup, CP1-3 implementation, CP4 testing)
- 5 detailed guides created (8-12 pages each)
- OVERVIEW_GUIDE created (quick-start for AI3)
- TODO_TRACKER created (progress tracking)

Ready for AI3 execution.
Next: Run ATLAS to continue STEP_1_2 (framework will auto-detect AI3 phase)
```

---

### **Phase 3: AI3 Execution (Checkpoint-by-Checkpoint Implementation)**

**Trigger:** All guides exist, TODO_TRACKER shows pending CPs

**Invocation:**
```
Human: "Continue ATLAS on STEP_1_2" (framework detects guides exist → AI3 phase, reads TODO_TRACKER for current CP)
OR
Human: "Run ATLAS as AI3 for STEP_1_2" (manual specification)
```

**Context AI3 Loads (in order):**

**First time starting Effort (CP0):**
1. ATLAS_OVERVIEW.md (skim - 1min)
2. AI3_IMPLEMENTER_GUIDE.md (role guide - 10min first time, 3min after)
3. AI3_DEVELOPER_BEST_PRACTICES.md (coding standards - 20min first time, reference after)
4. GIT_WORKFLOW.md (git procedures - 10min first time, reference after)
5. OVERVIEW_GUIDE.md (effort quick-start - 5min)
6. TODO_TRACKER.md (progress tracking - 2min)
7. START_HERE.md (AI1's research - 10min)
8. effort.md (goals/criteria - 3min)
9. CP0_GUIDE.md (current checkpoint instructions - 8min)

**Total first CP: ~60-75 min context loading**

**Continuing from CP1+:**
1. OVERVIEW_GUIDE.md (quick refresher - 2min)
2. TODO_TRACKER.md (what's done, what's next - 2min)
3. CPX_GUIDE.md (current checkpoint - 8min)
4. Previous CP implementation notes (5min)

**Total subsequent CPs: ~15-20 min context loading**

**AI3 Process:**

**Pre-Flight (CP0 only, first checkpoint):**

```bash
# 1. Validate git sync (2 min)
git fetch origin
git checkout main
git pull origin main
git log -1  # Note commit hash

git checkout staging
git pull origin staging
git log -1  # Note commit hash

git diff main staging
# Document any divergence

# 2. Read TODO_TRACKER (1 min)
cat efforts/STEP_1_2/TODO_TRACKER.md
# Understand: What's complete? What's current? Any blockers?

# 3. Read OVERVIEW_GUIDE (3 min)
cat efforts/STEP_1_2/OVERVIEW_GUIDE.md
# Get mental model of entire Effort

# 4. Read START_HERE brief (2 min)
head -100 efforts/STEP_1_2/START_HERE.md
# Understand research context
```

**Execute CP0 (Setup):**

```bash
# 1. Read CP0_GUIDE.md deeply (8 min)
cat efforts/STEP_1_2/guides/CP0_GUIDE.md
# Understand exact tasks

# 2. Spot-check sanity (5 min)
# - Will this setup achieve the outcome?
# - Any security concerns? (API keys, permissions)
# - Any missing steps?
# - Any red flags?

# 3. Execute tasks per guide (4 hours)
[Follow CP0_GUIDE.md exactly]
[Git init, Vercel setup, Supabase, etc.]

# 4. Test after CP0 (15 min)
npm run build  # Must succeed
vercel deploy --prod  # Test deployment
psql $DATABASE_URL -c "\dt"  # Verify tables exist

# 5. Update TODO_TRACKER (5 min)
# Mark CP0 complete, add completion date, note any issues

# 6. Commit (5 min)
git add .
git commit -m "[STEP_1_2] CP0 complete - infrastructure initialized"
git push origin effort/STEP_1_2_AUDIT_ENGINE
```

**Report CP0 Complete:**
```
CP0 (Infrastructure Setup) of STEP_1_2_AUDIT_ENGINE complete.

Completed:
- Git branch: effort/STEP_1_2_AUDIT_ENGINE created
- Vercel project: audit-engine initialized
- Supabase: [platform-name] with 3 tables
- Environment configured (.env.local + Vercel vars)
- Deployment validated (test URL works)

Testing:
- Build: ✅ Success
- Deploy: ✅ audit-engine-git-abc123.vercel.app live
- Database: ✅ Tables exist

TODO_TRACKER updated: CP0 marked complete, CP1 next

Duration: 4.2 hours (estimated 4h)

Next: CP1 (Core Analysis Engine)
Continue: "Run ATLAS to continue STEP_1_2" (framework will load CP1)
```

**Execute CP1-CPX (repeat process):**
1. Read CPX_GUIDE.md
2. Spot-check sanity (will this work? security concerns?)
3. Execute tasks
4. Test after CP
5. Update TODO_TRACKER
6. Commit and push
7. Report complete, move to next

**Execute Final CP (CP4 in this example):**

**Additional responsibilities in final CP:**
- Comprehensive testing (cross-vertical, performance, accessibility)
- Merge to staging
- Full staging validation
- Create PR staging → main (human approves)
- Create COMPLETION_SUMMARY.md (for next substep)
- Update ATLAS_STEPS.md (mark substep complete)

**Final CP Tasks:**
```bash
# ... [testing tasks from CP4_GUIDE.md]

# After all testing passes:

# 1. Merge to staging
git checkout staging
git merge effort/STEP_1_2_AUDIT_ENGINE --no-ff
git push origin staging

# 2. Test on staging thoroughly
[Full validation]

# 3. Create PR to main (don't merge - human approves)
gh pr create --base main --head staging \
  --title "[STEP_1_2] Launch Audit Engine V0.5" \
  --body "..."

# 4. Create COMPLETION_SUMMARY.md
```

**COMPLETION_SUMMARY.md:**

**File:** `/efforts/STEP_1_2_[NAME]/COMPLETION_SUMMARY.md`

```markdown
# Completion Summary - STEP_1_2 Audit Engine

**Substep:** STEP_1_2 from ATLAS_STEPS.md
**Completed:** 2025-12-20
**Duration:** 7 days (estimated: 7 days)
**Outcome:** ✅ SUCCESS

---

## What Was Built

**Deliverable:** Audit Engine V0.5
- Multi-tenant website analysis tool
- URL: tool.yourdomain.com
- Analyzes: Performance, SEO, mobile, accessibility, security
- Output: Professional PDF report via email
- Verticals tested: Contractors, law firms, healthcare (universal)

**Tech:**
- Next.js 15 + Supabase + PageSpeed API + Puppeteer
- Deployment: Vercel (auto-deploy on push)
- Database: 3 tables (audits, customers, reports)

**Metrics:**
- Build time: 7 days (on estimate)
- Performance: 95 Lighthouse score (tool itself)
- Analysis speed: <2 min per site
- Multi-vertical: Tested on 12 diverse sites across 3 verticals

---

## Key Decisions

**Decision 1: Multi-tenant from day 1**
- Built with Supabase RLS (row-level security)
- Why: Will become Inspector SaaS, needs architecture now
- Trade-off: 2x build time vs simple script
- Outcome: CORRECT (architecture is solid, can scale to SaaS easily)

**Decision 2: PageSpeed API over Lighthouse CLI**
- Used Google's hosted API
- Why: Simpler (no headless Chrome), faster
- Trade-off: Rate limits (100/day free)
- Outcome: ACCEPTABLE (hit limits during testing, upgraded to paid $200/mo)

**Decision 3: PDF via Puppeteer (not react-pdf)**
- Puppeteer renders HTML to PDF
- Why: More flexible, better quality
- Trade-off: Memory usage (needed 1GB config)
- Outcome: CORRECT (PDFs are professional quality)

---

## What Worked (Repeat in Future)

✅ **Copied database patterns from previous project:** Saved 8 hours (auth, security, client setup)
✅ **Multi-tenant architecture:** No regrets, enables SaaS path
✅ **Testing across verticals in CP3:** Caught scoring calibration issues early
✅ **Puppeteer memory config 1GB:** Solved crashes immediately

---

## What Didn't Work (Avoid Next Time)

⚠️ **Over-engineered initial schema:** Predicted 8 tables, only needed 3
- Learning: Start minimal (3 tables), add as needed
- For next: Don't predict future schema, build what's needed now

⚠️ **Hit PageSpeed rate limits during testing:** Free tier 100/day insufficient
- Learning: Budget for paid API tiers upfront ($200/mo for 25K requests)
- For next: Check rate limits BEFORE starting CP0

---

## Recommendations for Next Substep

**For STEP_1_3 (Site Cloner):**
1. Reuse Audit Engine's Supabase instance (don't create new project)
2. Copy Puppeteer patterns (scraping + rendering proven)
3. Start with 3 tables max (don't over-architect)
4. Budget PageSpeed paid tier from start (avoid rate limit surprise)

**For AI1 researching STEP_1_3:**
- Audit Engine codebase exists (reference /apps/audit-engine/)
- Supabase patterns are proven (check /lib/supabase/ for RLS examples)
- Multi-tenant works (no architecture changes needed)

**For AI2 planning STEP_1_3:**
- CP0 can be lighter (shared infrastructure already exists)
- Consider: Can Site Cloner and Audit Engine share components? (both analyze sites)

---

## Technical Foundation Established

**Reusable for future Efforts:**
- Vercel team account: "your company"
- Supabase project: "[platform-name]" (can add tables for new tools)
- Multi-tenant patterns: RLS policies, customer isolation
- PDF generation: Puppeteer setup, memory config, templates
- Email delivery: Resend integration, template system

**Cost:**
- Vercel: $0/mo (Pro features not needed yet)
- Supabase: $0/mo (free tier, <500MB database)
- PageSpeed API: $200/mo (25K requests)
- Resend: $0/mo (3K emails/mo free)
**Total: $200/mo**

---

**This summary feeds forward to STEP_1_3, STEP_1_4, and all future work.**
```

**Step X+3: Update ATLAS_STEPS.md (10 min)**

Mark substep complete:
```markdown
#### STEP_1_2: Build Audit Engine
**Status:** ✅ COMPLETE
**Completed:** 2025-12-20
**Outcome:** tool.yourdomain.com live, tested across 3 verticals
**Learnings:** See efforts/STEP_1_2_AUDIT_ENGINE/COMPLETION_SUMMARY.md
```

**AI2 Completion Report:**
```
AI2 planning phase complete for STEP_1_2_AUDIT_ENGINE.

Created:
- OUTLINE.md (5 checkpoints defined)
- 5 detailed CP guides (CP0-CP4, 8-12 pages each)
- OVERVIEW_GUIDE.md (quick-start for AI3)
- TODO_TRACKER.md (progress tracking template)
- effort.md (goals and success criteria)

Total planning time: 10 hours (researched each CP deeply)

Ready for AI3 execution.

Framework status: All guides exist → AI3 phase can begin
Next: "Continue ATLAS on STEP_1_2" (will auto-load CP0 for AI3)
```

---

## Checkpoint Types & Patterns

### **CP0: ALWAYS Setup/Initialization (AI3)**

**Purpose:** Prepare technical foundation

**Common tasks:**
- Git repository initialization (if new)
- Create Vercel/deployment project
- Create database/Supabase project
- Configure environment variables
- Set up initial file structure
- Validate deployment works
- Create feature branch for Effort

**Duration:** 2-6 hours typically

**Role:** AI3 (Implementer) - NOT AI1

**Output:**
- Infrastructure ready
- Can build features in CP1+

---

### **CP1-CPX-1: Implementation Phases (AI3)**

**Purpose:** Build features, integrate services, create functionality

**Number:** Variable (1-8 CPs depending on complexity)
- Simple Effort: 1-2 implementation CPs
- Medium Effort: 2-4 implementation CPs
- Complex Effort: 4-8 implementation CPs

**AI2 decides split based on:**
- Natural phases (design → build → integrate → polish)
- Complexity (too much for one CP? split)
- Testing checkpoints (good to validate incrementally)

**Each implementation CP:**
- Tests after completion (build + unit tests + manual validation)
- Merges to staging (for preview/testing)
- Updates TODO_TRACKER
- Produces implementation notes artifact

---

### **CPX (Last): ALWAYS Testing & Deployment (AI3)**

**Purpose:** Comprehensive validation and production launch

**Tasks:**
- Full E2E testing
- Performance validation (Lighthouse, PageSpeed)
- Accessibility validation (WCAG, axe)
- Cross-vertical testing (if multi-vertical tool)
- Security check (no secrets committed, APIs secured)
- Staging validation (full manual test)
- Production deployment (merge to staging, create PR to main)
- Post-launch monitoring plan
- Create COMPLETION_SUMMARY.md
- Update ATLAS_STEPS.md (mark substep complete)
- Update TODO_TRACKER (mark all CPs complete)

**Duration:** 1-2 days typically

**Critical:** This is the quality gate. Comprehensive testing, no shortcuts.

**Output:**
- Production deployment (via PR, human merges)
- COMPLETION_SUMMARY.md (feeds next substep)
- Updated ATLAS_STEPS.md (progress tracking)

---

## Progress Tracking System

### **Three Levels of Tracking:**

**Level 1: Step/Substep Status (in ATLAS_STEPS.md)**

```markdown
## STEP 1: Build Platform Foundation

**Status:** IN_PROGRESS (2 of 3 substeps complete)
**Started:** 2025-12-10

### Substeps

#### STEP_1_1: Audit Engine
**Status:** ✅ COMPLETE
**Completed:** 2025-12-15
**Outcome:** tool.yourdomain.com live

#### STEP_1_2: Site Cloner
**Status:** 🔄 IN_PROGRESS (AI3 on CP3 of 5)
**Started:** 2025-12-16

#### STEP_1_3: Rebuild Engine Core
**Status:** ⏸️ PLANNED
```

**Who updates:** AI3 when substep completes (in final CP), or AI when Step completes

---

**Level 2: AI Phase Detection (file existence)**

```
Check for IN_PROGRESS Effort: efforts/STEP_1_2/effort.md has "Status: IN_PROGRESS"

Then check files:
- START_HERE.md exists? → AI1 complete ✅
- OUTLINE.md + guides exist? → AI2 complete ✅
- TODO_TRACKER shows CPs? → AI3 phase, check which CP

Auto-detect: "AI3 should execute CP3 of STEP_1_2"
```

**Who updates:** File creation IS the update (no manual tracking)

---

**Level 3: CP Progress (in TODO_TRACKER.md)**

```markdown
## CP0: Infrastructure Setup ✅ COMPLETE
**Completed:** 2025-12-16 14:30
**Duration:** 4.2 hours

## CP1: Core Analysis ✅ COMPLETE
**Completed:** 2025-12-18 16:00
**Duration:** 1.8 days

## CP2: Report Generation 🔄 IN_PROGRESS
**Started:** 2025-12-19 09:00
**Progress:** PDF template done, email integration remaining
**Est. completion:** 2025-12-20

## CP3: Polish ⏸️ PENDING
## CP4: Testing & Deploy ⏸️ PENDING
```

**Who updates:** AI3 after completing each CP (marks ✅, adds date/notes)

---

## File Ownership & Update Responsibility

### **START_HERE.md**
- **Created by:** AI1 (research phase)
- **Updated by:** Never (static after creation)
- **Read by:** AI2 (when planning), AI3 (for context)
- **Purpose:** AI1's comprehensive research on substep

### **OUTLINE.md**
- **Created by:** AI2 (after reading START_HERE)
- **Updated by:** AI2 (if CP count changes during planning)
- **Read by:** AI3 (understand CP sequence), Human (review plan)
- **Purpose:** High-level map of all CPs

### **OVERVIEW_GUIDE.md**
- **Created by:** AI2 (after creating all CP guides)
- **Updated by:** Rarely (only if Effort scope changes)
- **Read by:** AI3 (first thing when starting Effort)
- **Purpose:** Quick-start guide for Effort execution

### **CPX_GUIDE.md files**
- **Created by:** AI2 (one per CP, after researching that CP)
- **Updated by:** Rarely (only if approach changes mid-Effort)
- **Read by:** AI3 (when executing that specific CP)
- **Purpose:** Exact instructions for CP execution

### **TODO_TRACKER.md**
- **Created by:** AI2 (initial template with all CPs pending)
- **Updated by:** AI3 (after completing each CP)
- **Read by:** AI3 (every time resuming work), Framework (for auto-detection)
- **Purpose:** Track which CPs are done, which is current, resume state

### **COMPLETION_SUMMARY.md**
- **Created by:** AI3 (final task in last CP)
- **Updated by:** Never (static after Effort complete)
- **Read by:** Next substep's AI1 (context), AI2 (learnings), Human (review)
- **Purpose:** Handoff document to next Effort

### **effort.md**
- **Created by:** AI2 (during planning)
- **Updated by:** AI2 (if scope changes), AI3 (status updates)
- **Read by:** All AIs (high-level context)
- **Purpose:** Effort overview, goals, success criteria

### **ATLAS_STEPS.md**
- **Created by:** Human or AI2 in strategic mode (initial)
- **Updated by:** AI3 (mark substeps complete), AI2 (refine strategy quarterly)
- **Read by:** AI1 (understand substep), AI2 (plan Efforts), AI3 (strategic context)
- **Purpose:** Master strategy document

### **LEARNINGS_LOG.md**
- **Created by:** Framework (empty template)
- **Updated by:** Human (after reviewing COMPLETION_SUMMARY), AI2 in strategic mode
- **Read by:** AI1 (before research), AI2 (when planning), AI2 strategic (quarterly)
- **Purpose:** Capture discoveries for future application

### **DECISION_LOG.md**
- **Created by:** Framework (empty template)
- **Updated by:** Human (strategic choices), AI2 (if AI makes strategic decision)
- **Read by:** AI1 (understand past choices), AI2 (when planning or strategic mode)
- **Purpose:** Document strategic decisions with rationale

### **ATLAS_ASSUMPTIONS.md**
- **Created by:** Human or strategic AI (after company vision)
- **Updated by:** Human (when constraints change)
- **Read by:** All AIs (understand boundaries)
- **Purpose:** Global constraints and principles

---

## Entry Point Auto-Detection Logic

### **User says: "Continue ATLAS on STEP_1_2"**

**Framework does:**

```
Step 1: Determine Effort directory
- Check: /efforts/STEP_1_2_[MATCH]/
- If multiple matches: Ask "Which: STEP_1_2_AUDIT or STEP_1_2_OTHER?"
- If no match: "STEP_1_2 hasn't been started. Create START_HERE first? (AI1 research)"

Step 2: Detect AI phase
- Check START_HERE.md exists?
  NO → "Starting AI1 research phase for STEP_1_2"
  YES → Continue to Step 3

- Check OUTLINE.md + guides/ directory exists?
  NO → "Starting AI2 planning phase (START_HERE exists, need guides)"
  YES → Continue to Step 4

Step 3: AI2 Phase - Check guide completeness
- Count guides in /guides/ directory
- Check OUTLINE.md for CP count
- Match?
  NO → "Continuing AI2 guide creation (CP4 of 7 remaining)"
  YES → "AI2 complete, starting AI3 execution"

Step 4: AI3 Phase - Determine current CP
- Read TODO_TRACKER.md
- Find first unchecked CP
- "Resuming AI3 execution on CP3 (Report Generation)"

Step 5: Load context automatically
- Based on phase + CP, load exact files (per CONTEXT_INDEX)
- Report what was loaded (transparency)
- Begin work

User specified: STEP_1_2
Framework determined: AI3 phase, CP3, exact context to load
Auto-magic. ✨
```

---

## State Detection (Where Are We?)

Framework can answer these questions by scanning files:

### **Which Step is active?**
```bash
grep "Status: IN_PROGRESS\|ACTIVE" /ATLAS/strategy/ATLAS_STEPS.md
# Output: "## STEP 2: Build Internal Tools" has "Status: IN_PROGRESS"
```

### **Which Substep is active?**
```bash
find /ATLAS/efforts/ -name "effort.md" -exec grep -l "Status: IN_PROGRESS" {} \;
# Output: efforts/STEP_2_1_AUDIT_ENGINE/effort.md
# Substep STEP_2_1 is active
```

### **Which AI phase?**
```bash
cd efforts/STEP_2_1_AUDIT_ENGINE

# Check phase markers:
ls START_HERE.md 2>/dev/null && echo "AI1 done" || echo "AI1 needed"
ls OUTLINE.md 2>/dev/null && echo "AI2 started" || echo "AI2 needed"
ls guides/*.md 2>/dev/null | wc -l  # If >0, AI2 in progress or done
ls TODO_TRACKER.md 2>/dev/null && echo "AI2 done, AI3 can start" || echo "AI2 incomplete"

# If TODO_TRACKER exists:
grep "Current CP:" TODO_TRACKER.md
# Output: "Current CP: CP3"
```

### **Which CP is current?**
```bash
cat efforts/STEP_2_1/TODO_TRACKER.md | grep -A1 "🔄 IN_PROGRESS"
# Output: "CP3: Report Generation 🔄 IN_PROGRESS"
```

**Framework scans these files, determines state, loads appropriate context.**

---

## Research Distribution (80/50/20 Rule)

**AI1: 80% research, 20% synthesis**
- Deep investigation of entire substep
- Competitive analysis, technical options, patterns
- Produces START_HERE.md (comprehensive document)

**AI2: 50% research, 50% planning**
- Validate AI1's research (spot-checks)
- Deep research on each CP individually (what does CP0 setup need? research. CP1 implementation? research.)
- Produces guides informed by research (not generic templates)

**AI3: 20% research, 80% implementation**
- Spot-check guide sanity (will this work? any red flags?)
- Quick technical validation (can this API do X? check docs)
- Mostly executes (follows guides precisely)

**Research tapers off as work progresses:**
- AI1: Figure out WHAT to build (heavy research)
- AI2: Figure out HOW to build it (moderate research per CP)
- AI3: BUILD it (light research, mostly execution)

---

## Security & Quality Gates (AI3 Responsibilities)

**AI3 is final gateway before code ships. Must check:**

### **Security (Every CP):**
- No hardcoded secrets (API keys, passwords, tokens)
- No SQL injection vulnerabilities (use parameterized queries)
- No XSS vulnerabilities (sanitize user input)
- Authentication/authorization proper (if applicable)
- Environment vars in .env.local (not in code)
- Secrets not committed to git (check .gitignore)

### **Vulnerabilities (Every CP):**
- Dependency vulnerabilities (npm audit, check for critical)
- OWASP Top 10 (especially for web apps)
- Rate limiting (prevent abuse)
- Input validation (never trust user input)

### **Red Flags (Every CP):**
- TODO/FIXME comments (address before marking CP complete)
- console.log in production code (remove or use proper logging)
- Commented-out code (delete, git tracks history)
- Overly complex logic (refactor if can't explain)
- Missing error handling (all async operations need try/catch)

### **Scaling Concerns (CP2+ implementation):**
- Database queries (indexes needed? N+1 queries?)
- API rate limits (will this scale to 100 users?)
- Memory usage (will this crash at scale?)
- Caching (what should be cached?)

**AI3 spot-checks these in "sanity check" phase before executing CP.**

**If red flag found:**
- Flag to human immediately (don't proceed with vulnerable code)
- Or fix if obvious (remove console.log, add error handling)
- Document in implementation notes

---

## Example Files (What They Look Like)

### **START_HERE.md** (AI1 Output)
- Length: 800-1,500 lines
- Sections: Context, Research Findings (competitive/technical/design), Implementation Outcomes (very specific), Rough CP Breakdown, For AI2
- Tone: Comprehensive research document
- Purpose: Give AI2 everything needed to create perfect guides

### **OUTLINE.md** (AI2 Output)
- Length: 200-400 lines
- Sections: Effort summary, CP breakdown (CP0-CPX with 1-2 sentences each), Rationale for CP count, Dependencies, Testing strategy
- Tone: High-level roadmap
- Purpose: Quick overview before diving into detailed guides

### **OVERVIEW_GUIDE.md** (AI2 Output)
- Length: 300-600 lines
- Sections: What we're building, CP sequence (paragraph per CP), Key watchouts, Testing strategy, Quick reference links
- Tone: Quick-start guide for AI3
- Purpose: Get AI3 up to speed in 5 minutes

### **CPX_GUIDE.md** (AI2 Output, one per CP)
- Length: 600-1,200 lines per guide
- Sections: Overview, Pre-flight, Tasks (detailed steps), Outputs, Success criteria, Update TODO, Next CP
- Tone: Exact instructions (line numbers, commands, examples)
- Purpose: AI3 executes this mechanically

### **TODO_TRACKER.md** (AI2 creates, AI3 updates)
- Length: 200-500 lines
- Sections: Overall status, CP0 checklist, CP1 checklist, ..., Notes, Blockers
- Tone: Progress checklist
- Purpose: Track which CPs done, resume state, identify blockers

### **COMPLETION_SUMMARY.md** (AI3 Output)
- Length: 500-1,000 lines
- Sections: What was built, Key decisions, What worked, What didn't, Recommendations for next, Technical foundation
- Tone: Handoff document
- Purpose: Feed context to next substep (efficiency)

---

## File Structure (Complete)

```
/efforts/STEP_X_Y_[NAME]/
├── START_HERE.md                    # AI1 creates (research)
├── OUTLINE.md                       # AI2 creates (CP map)
├── OVERVIEW_GUIDE.md                # AI2 creates (quick-start)
├── TODO_TRACKER.md                  # AI2 creates, AI3 updates
├── COMPLETION_SUMMARY.md            # AI3 creates (final)
├── effort.md                        # AI2 creates (overview)
│
├── guides/                          # AI2 creates all
│   ├── CP0_GUIDE.md                # Setup (AI3 executes)
│   ├── CP1_GUIDE.md                # Implementation (AI3)
│   ├── CP2_GUIDE.md                # Implementation (AI3)
│   ├── ...                         # Variable count
│   └── CPX_GUIDE.md                # Testing/Deploy (AI3)
│
└── artifacts/                       # AI3 creates during execution
    ├── CP0_setup_notes.md
    ├── CP1_implementation_notes.md
    ├── CP2_implementation_notes.md
    └── ...
```

---

## What From ATLAS1 to Keep/Discard

### **KEEP (Good as-is or minor updates):**
- ✅ ATLAS_GLOSSARY.md (terminology reference - still valid)
- ✅ AI3_DEVELOPER_BEST_PRACTICES.md (coding standards - still valid)
- ✅ GIT_WORKFLOW.md (git procedures - still valid)
- ✅ ATLAS_STEPS_TEMPLATE.md (how to write Steps - still valid)
- ✅ ATLAS_ASSUMPTIONS.md template (constraints template - still valid)
- ✅ DECISION_LOG.md template (decision format - still valid)
- ✅ LEARNINGS_LOG.md template (learning format - still valid)
- ✅ migrations/MIGRATIONS_LOG.md (database tracking - still valid)
- ✅ Context loading CONCEPT (still valid, needs file list updates)

### **REWRITE (Core workflow wrong):**
- ❌ AI1_RESEARCHER_GUIDE.md (says "execute CP0" - wrong)
- ❌ AI2_GUIDE_CREATOR_GUIDE.md (missing research phase - incomplete)
- ❌ AI3_IMPLEMENTER_GUIDE.md (missing pre-flight, TODO updates, completion summary - incomplete)
- ❌ ATLAS_ENTRY_POINT.md (manual specification, not auto-detection - wrong)
- ❌ ATLAS_OVERVIEW.md (workflow section - wrong)
- ❌ ATLAS_ONBOARDING.md (entire workflow - wrong)
- ❌ QUICK_START.md (workflow examples - wrong)
- ❌ HUMAN_BEST_PRACTICES.md (invocation examples - wrong)
- ❌ examples/10XBUILD_EXAMPLE.md (entire example - wrong)
- ❌ efforts/README.md (structure description - incomplete)

### **REPLACE (Templates are wrong structure):**
- ❌ CP0_GUIDE.md template (says research, should say setup)
- ❌ CP1_GUIDE.md template (needs context updates)
- ❌ CP2_GUIDE.md template (needs context updates)
- ❌ CP3_GUIDE.md template (make generic "final CP" template)
- ❌ efforts/STEP_TEMPLATE_EFFORT/ structure (missing START_HERE, OUTLINE, OVERVIEW, TODO, COMPLETION)

### **CREATE (Missing from ATLAS1):**
- 🆕 START_HERE_TEMPLATE.md
- 🆕 OUTLINE_TEMPLATE.md
- 🆕 OVERVIEW_GUIDE_TEMPLATE.md
- 🆕 TODO_TRACKER_TEMPLATE.md
- 🆕 COMPLETION_SUMMARY_TEMPLATE.md
- 🆕 CP_GUIDE_GENERIC_TEMPLATE.md (AI2 uses for any CP, not just 0-3)

---

## Build Order for ATLAS3 (After This Spec Approved)

### **Phase 1: Foundation (Create first)**
1. README.md (what is ATLAS3)
2. ATLAS_OVERVIEW.md (system explanation with CORRECT workflow)
3. ATLAS_GLOSSARY.md (copy from ATLAS1, update refs)

### **Phase 2: Core Workflow (Create second)**
4. AI1_RESEARCHER_GUIDE.md (complete rewrite)
5. AI2_GUIDE_CREATOR_GUIDE.md (complete rewrite)
6. AI3_IMPLEMENTER_GUIDE.md (major updates)
7. ATLAS_ENTRY_POINT.md (complete rewrite with auto-detection)

### **Phase 3: Templates (Create third)**
8. START_HERE_TEMPLATE.md (new)
9. OUTLINE_TEMPLATE.md (new)
10. OVERVIEW_GUIDE_TEMPLATE.md (new)
11. TODO_TRACKER_TEMPLATE.md (new)
12. COMPLETION_SUMMARY_TEMPLATE.md (new)
13. CP_GUIDE_TEMPLATE.md (generic, replaces CP0-3)

### **Phase 4: Supporting Files (Create fourth)**
14. AI3_DEVELOPER_BEST_PRACTICES.md (copy from ATLAS1)
15. GIT_WORKFLOW.md (copy from ATLAS1)
16. CONTEXT_INDEX.md (update with new file types)
17. ATLAS_STEPS_TEMPLATE.md (copy from ATLAS1)
18. Strategy templates (ASSUMPTIONS, DECISION, LEARNINGS - copy templates)

### **Phase 5: Human & Documentation (Create fifth)**
19. HUMAN_BEST_PRACTICES.md (rewrite with correct workflow)
20. ATLAS_ONBOARDING.md (rewrite)
21. QUICK_START.md (rewrite)
22. ATLAS_VALIDATION.md (new - verify everything works)
23. examples/EXAMPLE_WALKTHROUGH.md (rewrite with correct flow)

---

## This Specification Defines

✅ **Correct AI1 workflow** (research entire substep, produce START_HERE)
✅ **Correct AI2 workflow** (validate, outline, research each CP, create guides + tracking)
✅ **Correct AI3 workflow** (pre-flight, execute CPs, update TODO, create COMPLETION)
✅ **Auto-detection logic** (framework finds state from files)
✅ **Progress tracking** (3 levels: Step/Substep, AI phase, CP progress)
✅ **File ownership** (who creates, updates, reads each file)
✅ **CP structure** (CP0 setup, CP1-X implementation, last testing/deploy)
✅ **Research distribution** (80% AI1, 50% AI2, 20% AI3)
✅ **Context loading** (what each AI reads, in what order)
✅ **Completion markers** (how we know phase is done)
✅ **Build order** (what to create first, second, third)

---

**This is the master specification. Build ATLAS3 from this. Measure thrice. Cut once.** 📐
