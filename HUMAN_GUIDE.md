# Human Guide - Your Role in ATLAS3

**Purpose:** Complete operational manual for humans using ATLAS3
**Audience:** Founders, team leads, anyone directing AI execution
**Status:** v2.0

---

## Your Role

**You are the orchestrator and decision-maker.**

**You:**
- Set strategic direction (define or approve Steps via Mode 2)
- Invoke Usher modes (daily Mode 1, weekly Mode 5, monthly Mode 7)
- Review AI work (check START_HERE quality, approve guides, review code)
- Approve production (merge PRs after AI3 creates them)
- Capture strategic learnings (Mode 5 weekly)
- Maintain framework (Mode 7 monthly, Mode 8 quarterly)

**You don't:**
- Execute every checkpoint yourself (AI3 does)
- Micromanage (trust guides, spot-check quality)
- Track state manually (Usher auto-detects)

**Think:** CEO + Lead Engineer, delegating execution to AI team.

---

## Daily Operations

### Morning Routine (10-15 min)

```bash
# 1. Check email/notifications
# Any customer issues? Blocking decisions needed?

# 2. Invoke Usher
"Run ATLAS Mode 1" (Auto-Resume)

# Usher reports:
"Active Effort: STEP_1_2_SITE_CLONER
Phase: AI3 Execution
Current: CP3 of 5 (60% complete)
Next: Continue CP3 (Site Generation)"

# 3. Review yesterday's progress (if AI worked overnight)
cat efforts/STEP_1_2_SITE_CLONER/TODO_TRACKER.md
# Check: Which CPs done? Any issues?

# 4. Continue work
"Yes, continue CP3"

# Usher loads AI3 context, begins execution
# You monitor occasionally (every 1-2 hours check progress)
```

**Time:** 10-15 min orchestration, then AI works (you do other tasks)

---

### Code Review (15-30 min, when CP completes)

**After AI3 completes CP and merges to staging:**

```bash
# 1. Check Usher's completion report
# Should say: "CP2 complete. Merged to staging. Preview: [URL]"

# 2. Spot-check code quality
git checkout staging
git log --oneline -5
# Should see: Clear commits ([STEP_X_Y] CP2 - description)

# Pick 1-2 files to review:
cat src/lib/scraper/scraper.ts
# Look for:
# - TypeScript types present ✓
# - No hardcoded secrets ✓
# - Error handling exists ✓
# - Code is clear ✓

# 3. Test on staging
# Visit staging URL (Vercel deployment)
# Quick functional test (does CP's feature work?)

# 4. If good: "Looks good, continue to CP3"
# If issues: "Fix [specific issue] before next CP"
```

**Not reviewing every line** - spot-checking quality.

---

### End of Day (5 min)

```bash
# What got done today?
"Run ATLAS Mode 4" (Overview)

Usher shows:
"Today's progress:
- STEP_1_2: CP3 complete (60% → 80% done)
- Next: CP4 (Testing & Deployment)
- On track for completion: 2025-12-20"

# Note in your journal/log
"STEP_1_2: Completed CP3. On track."
```

**Stay oriented on progress.**

---

## Weekly Operations

### Friday Learning Capture (15-30 min)

**Critical weekly discipline:**

```
"Run ATLAS Mode 5" (Learning Capture)

Usher asks: "Which Effort completed this week?"
You: "STEP_1_2_SITE_CLONER"

Usher:
1. Reads COMPLETION_SUMMARY.md
2. Drafts 3-5 learning entries
3. Shows you for review

You:
- Review each (approve/edit/skip)
- Add strategic context ("This changes our pricing because...")
- Takes 10-15 minutes (vs 30-60 manually)

Usher:
- Adds to LEARNINGS_LOG.md
- Commits changes
- Reports complete

**DON'T SKIP THIS.**
No learning capture = no velocity improvement.
```

**Schedule:** Friday 4-5pm (non-negotiable calendar block)

---

## Monthly Operations

### Health Check (Last Friday, 30 min)

```
"Run ATLAS Mode 7" (Health Check)

Usher:
1. Scans all files (structure complete?)
2. Checks workflow compliance (AI1 → AI2 → AI3 happening?)
3. Validates progress tracking (TODO_TRACKERs updating?)
4. Analyzes velocity (improving or flat?)
5. Reports health (✅ healthy, ⚠️ issues, ❌ critical)

You:
- Review report
- Fix any issues flagged
- Confirm framework healthy

Time: 30 minutes
```

**Schedule:** Last Friday of month, 4pm

---

## Quarterly Operations

### Strategic Review (Half day, ~4 hours)

**Last week of quarter:**

**Morning (2 hours):**
```
"Run ATLAS Mode 2" (Refine Substeps)

Usher:
- Shows all Steps/Substeps status
- Shows learnings from quarter

You:
- Review what worked/didn't
- Refine future Steps (make more specific)
- Reorder if needed (priorities changed?)
- Add new Steps (opportunities discovered?)

Usher:
- Updates ATLAS_STEPS_PARTX.md
- Logs decisions in DECISION_LOG

Result: Strategy evolved based on execution reality
```

**Afternoon (2 hours):**
```
"Run ATLAS Mode 8" (Template Evolution)

Usher:
- Analyzes last 10-15 COMPLETION_SUMMARYs
- Identifies patterns (what's consistent?)
- Suggests template improvements

You:
- Approve improvements
- Prioritize (high impact first)

Usher:
- Updates templates
- Documents evolution

Result: Framework improved, future Efforts faster/better
```

**Schedule:** Last week of Mar, Jun, Sep, Dec

---

## Production Deployment (Your Responsibility)

**When AI3 completes final CP:**

**AI3 reports:**
```
"Final CP complete.
COMPLETION_SUMMARY created.
PR #47 created (staging → main).

Awaiting your approval to merge."
```

**Your workflow (30-60 min):**

**1. Review COMPLETION_SUMMARY (10 min)**
```bash
cat efforts/STEP_X_Y/COMPLETION_SUMMARY.md

Check:
- What was built? (deliverables clear?)
- Success criteria met? (all checked ✓)
- Quality validated? (testing passed?)
- Decisions documented? (rationale clear?)
```

**2. Review PR (10 min)**
```bash
# Visit GitHub PR #47
# Check: Files changed, commits, description

# Skim code changes (don't read every line):
# - No secrets committed (.env.local not in diff) ✓
# - Code looks clean ✓
# - Tests exist ✓
```

**3. Test staging (15 min)**
```bash
# Visit staging URL
# Full manual test:
# - All features work ✓
# - Mobile works (test on phone) ✓
# - No errors (check console) ✓
# - Performance good (feels fast) ✓

# Share with customer (if applicable):
# Get final approval before production
```

**4. Merge PR (2 min)**
```bash
# GitHub UI: Approve → Merge pull request

# Or CLI:
git checkout main
git pull origin main
git merge staging --no-ff
git push origin main

# Vercel deploys (~2 min)
```

**5. Monitor production (15 min)**
```bash
# First hour: Check every 15 min
# - Site loads ✓
# - No errors in Vercel logs ✓
# - Features work ✓

# Next 24 hours: Check 2-3 times
# - No error spikes
# - Customer happy (if applicable)
```

**You approve production. AI prepares, you decide.**

---

## Decision Making (Your Authority)

**You approve:**
- Production deployments (merge PRs)
- Strategic pivots (change Steps mid-flight)
- Major technical decisions (when AI2 presents options)
- Budget allocation (paid API tiers, hiring, tools)
- Customer scope changes (expand Effort or defer)

**AI executes within boundaries you set.**

---

## Weekly Time Budget

**ATLAS operations:**
- Daily invocation/review: 30-60 min/day = 3-6 hours/week
- Friday learning capture: 15 min/week
- Code reviews: 30 min/week (spot checks)
**Total: 4-7 hours/week on ATLAS**

**Leaves 35-40 hours/week for:**
- Customer communication
- Sales
- High-level strategy
- Deep work (when you want to code yourself)

**ATLAS manages execution complexity so you focus on leverage.**

---

## Usher Mode Usage Guide

**Mode 1 (85% usage):** "Continue work"
- Use: Every day, multiple times
- When: Starting work, resuming after break, checking progress

**Mode 2 (5% usage):** "Refine strategy"
- Use: Before starting new Step, mid-flight adjustments
- When: Substep is vague, learnings change direction, need to restructure

**Mode 3 (8% usage):** "Direct to substep"
- Use: When you know exactly what to work on
- When: Large Effort planned, skip scanning overhead

**Mode 4 (2% usage):** "Overview/AMA"
- Use: Status checks, onboarding teammates, learning framework
- When: "Where are we overall?" or "How does X work?"

**Mode 5 (Weekly):** "Learning capture"
- Use: Friday afternoon (after Effort completes)
- When: COMPLETION_SUMMARY exists, need to extract learnings

**Mode 6 (As needed):** "Document decision"
- Use: When making strategic choice
- When: Tech stack decision, market focus, pricing change

**Mode 7 (Monthly):** "Health check"
- Use: Last Friday of month
- When: Want to validate framework health

**Mode 8 (Quarterly):** "Template evolution"
- Use: Last week of quarter
- When: After 10-15 Efforts (enough patterns to analyze)

---

## Red Flags (You're Using ATLAS Wrong)

**🚩 Not capturing learnings:**
- Friday Mode 5 getting skipped
- LEARNINGS_LOG has 2 entries after 8 Efforts

**Fix:** Block Friday 4-5pm calendar, make non-negotiable

---

**🚩 Velocity not improving:**
- Effort 8 takes same time as Effort 2

**Fix:** Run Mode 8 (template evolution) - why aren't patterns being systematized?

---

**🚩 AI confused/making mistakes:**
- AI asking lots of questions
- Deliverables don't match requirements

**Fix:** Check guides (are they detailed enough? use Mode 2 to refine substep specificity)

---

**🚩 Can't find current state:**
- "Which CP are we on?" - you don't know

**Fix:** Run Mode 1 (auto-detection tells you) or Mode 4 (overview shows everything)

---

**🚩 Git is messy:**
- Merge conflicts, force pushes, unclear commits

**Fix:** Re-read GIT_WORKFLOW.md with team, enforce process

---

## When to Override ATLAS

**ATLAS is opinionated. Sometimes skip it:**

**Emergency hotfix:**
- Skip ATLAS, fix directly, document in LEARNINGS_LOG after

**Tiny task (<2 hours):**
- Don't create full Effort for "change phone number on contact page"
- Just do it, commit, move on

**Quick exploration:**
- Don't need AI1 research for "test if this API works"
- Test directly, document if valuable

**Return to ATLAS** for systematic work (>1 week Efforts).

---

## Success Indicators

**You're using ATLAS well if:**
- ✅ Know current state instantly (Mode 4 or check TODO_TRACKER)
- ✅ Velocity improving (Effort 10 is 50% faster than Effort 1)
- ✅ Quality consistent (all deliverables meet standards)
- ✅ Learnings captured (weekly Mode 5 discipline)
- ✅ Strategy evolving (quarterly Mode 2 updates based on learnings)
- ✅ Framework improving (quarterly Mode 8 template evolution)
- ✅ Confident deploying (trust process, quality gates work)

**If 5+ indicators:** ✅ You're using ATLAS correctly

---

## Team Scaling (When You Hire)

**Onboarding first teammate:**

**Week 1:**
- Read: README, OVERVIEW, role guide for their role (AI3 if developer)
- Shadow: Watch you use Mode 1 (see workflow)
- Execute: Have them invoke Mode 1, monitor first CP
- Review: Together, check their work

**Week 2:**
- Independent: They invoke Mode 1 themselves
- You review: Spot-check quality
- They learn: Capture learnings (Mode 5)

**By Week 3:** Teammate can execute Efforts independently

**ATLAS guides train teammates** - consistent quality across team.

---

## Related Documentation

**Your core docs:**
- ONBOARDING.md - Setup guide (read once)
- QUICK_START.md - Fast track (read once)
- HUMAN_GUIDE.md - This file (reference ongoing)
- ATLAS_ENTRY_POINT.md - 8 modes explained

**AI docs (understand their jobs):**
- roles/AI1_RESEARCHER_GUIDE.md
- roles/AI2_GUIDE_CREATOR_GUIDE.md
- roles/AI3_IMPLEMENTER_GUIDE.md

**Mode docs (detailed workflows):**
- modes/MODE1-8.md (reference when using that mode)

---

**You orchestrate. AIs execute. ATLAS maintains quality. Build to $1M+ ARR systematically.** 🎯
