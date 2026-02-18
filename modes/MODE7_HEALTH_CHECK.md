# Mode 7: Health Check - Validate Framework Setup & Usage

**Purpose:** Run diagnostics on ATLAS3 setup and usage patterns
**Usage:** Monthly or when something feels wrong
**Trigger:** Human says "Run ATLAS health check" or "Validate ATLAS setup"

---

## What This Mode Does

**Runs ATLAS_VALIDATION.md checklist programmatically:**
1. File structure (all required files exist?)
2. Workflow compliance (AI1 → AI2 → AI3 happening correctly?)
3. Progress tracking (TODO_TRACKERs updating? ATLAS_STEPS current?)
4. Context management (AIs loading correct files? Not overloading?)
5. File ownership (updates happening by right roles?)
6. Git health (clean history? no force pushes to main?)
7. Learning loops (learnings captured? applied in future Efforts?)

**Reports:**
- ✅ Healthy (all checks pass)
- ⚠️ Issues found (specific problems with fixes)
- ❌ Critical (framework broken, needs attention)

---

## Files Usher Loads

```
1. ATLAS_VALIDATION.md (checklist to execute)
   Lines: ~1,500
   Tokens: ~15K
   Time: 10 min

2. All ATLAS3 framework files (scan for existence)
   Purpose: Verify file structure
   Time: 2 min (just ls commands)

3. All Effort files (check workflow compliance)
   Scan: efforts/*/effort.md, TODO_TRACKER.md, COMPLETION_SUMMARY.md
   Tokens: ~20K
   Time: 8 min

4. ATLAS_STEPS files (check progress tracking)
   Tokens: ~12K
   Time: 5 min

5. Git repository (check health)
   Commands: git log, git branch, git diff
   Time: 3 min

6. Recent COMPLETION_SUMMARYs (check if learnings extracted)
   Last 3-5 Efforts
   Tokens: ~24K
   Time: 10 min

Total: ~71K tokens, ~40 min
```

---

## Diagnostic Checks

### Check 1: File Structure

```bash
# Core files exist?
ls ATLAS3/README.md ATLAS3/ATLAS_OVERVIEW.md ATLAS3/ATLAS_SPECIFICATION.md
# Should all exist

# Role guides exist?
ls ATLAS3/roles/AI1*.md ATLAS3/roles/AI2*.md ATLAS3/roles/AI3*.md
# Should have all 5 guides

# Templates exist?
ls ATLAS3/templates/*.md | wc -l
# Should be: 7 templates

# Strategy files exist?
ls ATLAS3/strategy/*.md
ls ATLAS3/strategy/steps/*.md  # Individual step files
# Should have STEPS_TEMPLATE, ASSUMPTIONS, LEARNINGS, DECISIONS
```

**Result:** ✅ All required files exist

---

### Check 2: Workflow Compliance

**Scan recent Efforts:**
```bash
# Find last 3 completed Efforts
find efforts/ -name "COMPLETION_SUMMARY.md" | head -3

# For each, check workflow:
# - Does START_HERE.md exist? (AI1 researched)
# - Does OUTLINE.md exist? (AI2 planned)
# - Do all guides exist per OUTLINE? (AI2 completed)
# - Does TODO_TRACKER exist? (AI2 created)
# - Are all CPs marked ✅ in TODO_TRACKER? (AI3 completed)
# - Does COMPLETION_SUMMARY exist? (AI3 handed off)
```

**Issues to catch:**
- START_HERE missing (AI1 skipped - bad)
- Guides incomplete (AI2 didn't finish - bad)
- TODO_TRACKER not updated (AI3 not tracking - bad)
- COMPLETION_SUMMARY missing (AI3 didn't create handoff - bad)

**Result:** ✅ Workflow followed correctly / ⚠️ Issues found

---

### Check 3: Progress Tracking

**Check ATLAS_STEPS files:**
```bash
# Are completed substeps marked ✅?
grep "Status: ✅ COMPLETE" strategy/ATLAS_STEPS_PART*.md

# Are in-progress substeps marked 🔄?
grep "Status: 🔄 IN_PROGRESS" strategy/ATLAS_STEPS_PART*.md

# Are completed substeps linked to COMPLETION_SUMMARY?
grep "Details: efforts/" strategy/ATLAS_STEPS_PART*.md
```

**Issues to catch:**
- Substep complete but not marked in ATLAS_STEPS (AI3 forgot)
- COMPLETION_SUMMARY exists but no link (tracking broken)
- Multiple IN_PROGRESS (should be one at a time usually)

**Result:** ✅ Progress tracking current / ⚠️ Out of sync

---

### Check 4: Context Management

**Check recent AI sessions (if accessible):**
```
How many files did AI1 load? (should be 8-12)
How many files did AI2 load? (should be 12-18)
How many files did AI3 load? (should be 9 first, 4 subsequent)

Are AIs loading:
- Full ATLAS_STEPS? (should load relevant section only)
- All LEARNINGS? (should load recent only)
- Unrelated Efforts? (should skip)

Token counts reasonable? (should be 25K-75K per session)
```

**Issues to catch:**
- AI loading 30+ files (context explosion)
- AI loading full ATLAS_STEPS (inefficient)
- AI loading all LEARNINGS (not selective)

**Result:** ✅ Context efficient / ⚠️ Overloading detected

---

### Check 5: Learning Loops

**Check if learnings are captured:**
```bash
# Count COMPLETION_SUMMARYs
COMPLETE=$(find efforts/ -name "COMPLETION_SUMMARY.md" | wc -l)

# Count LEARNINGS_LOG entries
LEARNINGS=$(grep -c "^## 2025" strategy/LEARNINGS_LOG.md)

# Compare
# Should be: ~3-5 learnings per Effort
# If COMPLETE=5 and LEARNINGS=2: ⚠️ Not capturing enough
```

**Check if learnings are applied:**
```bash
# Do recent Efforts reference past learnings?
# Check START_HERE files: Do they mention "from LEARNINGS_LOG: ..."
# Check guides: Do they say "based on STEP_X_Y pattern: ..."

# If no references: ⚠️ Learnings not being applied
```

**Result:** ✅ Learning loops working / ⚠️ Learnings not captured or not applied

---

### Check 6: Git Health

```bash
# Check for force pushes to main (should be ZERO)
git log main --all --source --pretty=format:"%h %s" | grep -i "force"
# Should find nothing

# Check commit message quality
git log main --oneline -20
# Should see: [STEP_X_Y] CPX - description format

# Check for stale branches
git branch -a --merged main | grep effort/
# Should be minimal (merged efforts should be deleted)

# Check staging vs main divergence
git log main..staging --oneline | wc -l
# Should be reasonable (<20 commits ahead)
```

**Issues to catch:**
- Force pushes to main (violation of workflow)
- Vague commit messages (no [STEP_X_Y] prefix)
- 50 stale effort branches (cleanup needed)
- Staging 200 commits ahead of main (something's wrong)

**Result:** ✅ Git healthy / ⚠️ Issues found

---

### Check 7: Velocity Trends

**Analyze completed Efforts:**
```
First 3 Efforts:
- STEP_-1: 2 days
- STEP_0_1: 7 days
- STEP_0_2: 10 days (current estimate)

Average: ~6 days

Expected for Effort 4-6: 4-5 days (30% faster - learning curve)

If not improving: ⚠️ Learnings not being applied, or Efforts getting more complex
```

---

## Health Report Template

```markdown
# ATLAS Health Check Report

**Date:** 2025-12-20
**Efforts analyzed:** 3 complete, 1 in progress
**Time period:** Months 1-2

---

## Overall Health: ✅ HEALTHY

**Summary:** All checks passed. Framework is being used correctly. Minor optimizations possible.

---

## Check Results

### 1. File Structure: ✅ PASS
- All 27 core files exist
- All templates present
- Strategy files configured

### 2. Workflow Compliance: ✅ PASS
- All 3 Efforts followed AI1 → AI2 → AI3 sequence
- All have START_HERE (AI1 researched)
- All have guides (AI2 planned)
- All have COMPLETION_SUMMARY (AI3 handed off)

### 3. Progress Tracking: ⚠️ MINOR ISSUE
- ATLAS_STEPS tracking: ✅ Current
- TODO_TRACKER updates: ✅ AI3 updating after each CP
- Issue: STEP_0_1 marked complete but no link to COMPLETION_SUMMARY
  - Fix: Add link to steps/STEP_X.md file

### 4. Context Management: ✅ PASS
- AI1 loading: 8-10 files (~35K tokens) ✅
- AI2 loading: 14-16 files (~65K tokens) ✅
- AI3 loading: 9 files CP0, 4 files CP1+ ✅
- No context explosion detected

### 5. Learning Loops: ✅ PASS
- 3 Efforts complete → 8 learnings captured (2.7 per Effort) ✅
- Recent Efforts reference past learnings ✅
- Patterns being applied (e.g., multi-tenant architecture reused)

### 6. Git Health: ✅ PASS
- Zero force pushes to main ✅
- Commit messages follow convention ✅
- 2 stale branches (minor cleanup needed)
- Staging 3 commits ahead of main (normal)

### 7. Velocity Trends: ✅ IMPROVING
- STEP_0_1: 7 days
- STEP_0_2: ~10 days (in progress, on track)
- Expected STEP_0_3: ~7 days (reusing patterns)
- Trend: ⚠️ Not yet improving (too early, only 2 complete)
  - Check again after 5 Efforts (Month 3)

---

## Recommendations

**High priority:**
1. Add COMPLETION_SUMMARY link to STEP_0_1 in ATLAS_STEPS (5 min fix)
2. Delete 2 merged effort branches (git branch -d cleanup)

**Medium priority:**
3. After 5 Efforts: Review velocity (should be 30-40% faster by then)

**Low priority:**
4. Archive old LEARNINGS entries after 30 (quarterly task)

---

## Next Health Check

**Schedule:** 2026-01-20 (monthly)
**or:** After 5 more Efforts complete (whichever first)

---

**Framework is healthy. Continue using as-is.**
```

---

## When to Use Mode 7

**Use:**
- After initial setup (validate everything configured)
- Monthly (routine health check)
- Quarterly (comprehensive review)
- When something feels wrong (diagnose issues)
- Before major milestone (ensure foundation solid)

**Time:** 30-45 minutes (automated checks + report)

---

**This mode catches issues early. Use monthly for peace of mind.**
