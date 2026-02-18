# Mode 8: Template Evolution - Improve Framework from Learnings

**Purpose:** Systematically improve ATLAS3 framework based on execution patterns
**Usage:** Quarterly (after 10-15 Efforts) or when friction is felt
**Trigger:** Human says "Evolve ATLAS templates" or quarterly review
**Complexity:** HIGH - Meta-level framework improvement

---

## What This Mode Does

**Framework improvement through pattern analysis:**
1. Read all COMPLETION_SUMMARYs (last 10-15 Efforts)
2. Identify patterns ("AI3 always does X in CP0 - should be in template")
3. Spot gaps ("Guides never mention Y - should be added")
4. Find repetition ("Every Effort has same issue - fix in framework")
5. Suggest template updates (specific improvements)
6. Human approves, Usher updates templates/guides
7. Document evolution in TEMPLATE_EVOLUTION_LOG.md

**This enables:**
- Framework improves with use (templates get better over time)
- Common patterns systematized (don't repeat manual work)
- Friction reduced (add what's consistently needed)
- Quality increased (incorporate lessons learned)

---

## Prerequisite: TEMPLATE_EVOLUTION_GUIDE.md

**This mode requires companion document:**

**File:** `/ATLAS3/guides/TEMPLATE_EVOLUTION_GUIDE.md`

**Contains:**
- How to analyze COMPLETION_SUMMARYs for patterns
- What makes a good template improvement (vs framework bloat)
- How to update templates safely (don't break existing Efforts)
- How to test template changes (validation approach)
- Examples of good vs bad template updates

**Usher loads this guide** (provides meta-framework for framework improvement).

**Create this file separately** (not in this mode file - too complex for inline).

---

## Files Usher Loads

```
1. TEMPLATE_EVOLUTION_GUIDE.md (meta-framework)
   Lines: ~800-1,200
   Tokens: ~12K
   Time: 12 min

2. Last 10-15 COMPLETION_SUMMARYs
   Files: efforts/STEP_*/COMPLETION_SUMMARY.md (sorted by date, recent first)
   Lines: ~7,500-15,000 total
   Tokens: ~90K
   Time: 40 min (skim for patterns, not deep read)

3. Current templates (to analyze for improvement)
   Files: templates/*.md
   Lines: ~5,000
   Tokens: ~50K
   Time: 20 min

4. Current role guides (might need updates)
   Files: roles/*.md
   Lines: ~5,000
   Tokens: ~50K
   Time: 15 min (skim, focus on instructions that might need refinement)

5. LEARNINGS_LOG.md (last 30 entries)
   Tokens: ~20K
   Time: 10 min (look for process-related learnings)

Total: ~17,500-25,000 lines, ~222K tokens, ~100 min

NOTE: This is HEAVY context (framework improvement requires broad view)
Might hit limits. Solution: Analyze in batches (5 Efforts at a time)
```

---

## Workflow: Pattern Analysis & Template Updates

### Step 1: Analyze Patterns from Execution

**Usher reads COMPLETION_SUMMARYs and identifies:**

**Pattern Type 1: Consistent Successes** (always works - systematize)
```
From 10 COMPLETION_SUMMARYs:

Pattern found (8 of 10 Efforts):
"Reusing Supabase instance saves 2-3 hours setup time"

Current template state:
- CP0_GUIDE_TEMPLATE says: "Create Vercel project, create Supabase project"
- Doesn't mention checking for existing infrastructure first

Suggested improvement:
- Add to CP0_GUIDE_TEMPLATE, Task 1: "Check if Supabase project exists (from previous Effort). If yes, reuse. If no, create new. Default: Reuse."

Impact: Saves 2-3h × 30 future Efforts = 60-90 hours
```

---

**Pattern Type 2: Consistent Failures** (always breaks - prevent)
```
From 10 COMPLETION_SUMMARYs:

Pattern found (6 of 10 Efforts):
"Hit API rate limits during testing (didn't budget for paid tier)"

Current template state:
- CP_GUIDE_TEMPLATE doesn't mention checking rate limits

Suggested improvement:
- Add to CP_GUIDE_TEMPLATE, Spot-Check Sanity section: "Check API rate limits (free tier sufficient? budget for paid if usage high?)"
- Add to START_HERE_TEMPLATE, Integration Requirements: "Rate limits: [X/day free, $Y/mo for Z requests]"

Impact: Prevents 18-hour delays × future Efforts
```

---

**Pattern Type 3: Missing Guidance** (gap in templates - add)
```
From 10 COMPLETION_SUMMARYs:

Found (7 of 10 Efforts):
"Cross-vertical testing revealed assumptions"

Current template state:
- CP_GUIDE_TEMPLATE final CP has "comprehensive testing" but doesn't specify cross-vertical

Suggested improvement:
- Add to final CP template: "If multi-vertical tool: Test on contractor, law, healthcare sites (minimum 3 per vertical). Validate universal (not vertical-specific assumptions)."

Impact: Catches contractor bias early (before production)
```

---

**Pattern Type 4: Framework Friction** (manual work that could be automated)
```
From 10 COMPLETION_SUMMARYs:

Found (9 of 10 Efforts):
"Updating TODO_TRACKER after each CP is manual (sometimes forgotten)"

Current state:
- AI3 manually edits TODO_TRACKER.md
- Error-prone (forget to update, wrong format)

Suggested improvement:
- Could add: TODO_TRACKER_UPDATE_SCRIPT.md (guide for creating script that updates TODO)
- Or: Improve AI3 guide with exact update template (copy-paste, fill in, commit)

Impact: Reduces errors in progress tracking
```

---

### Step 2: Prioritize Improvements

**Usher categorizes:**

**High impact, low effort (do now):**
- Add "check for existing infrastructure" to CP0 template
- Add "API rate limit check" to guides

**High impact, high effort (plan for next quarter):**
- Create TODO update script
- Add cross-vertical testing checklist

**Low impact (skip or defer):**
- Minor wording changes
- Formatting improvements

---

### Step 3: Draft Template Updates

**For each high-priority improvement:**

**Usher shows diff:**
```markdown
File: templates/CP_GUIDE_TEMPLATE.md

BEFORE (line 45-50):
```markdown
## Spot-Check Sanity

**Security:**
- [ ] No hardcoded secrets?
- [ ] Input validated?
```

AFTER (adding rate limit check):
```markdown
## Spot-Check Sanity

**Security:**
- [ ] No hardcoded secrets?
- [ ] Input validated?

**Integration concerns:**
- [ ] API rate limits checked? (free tier sufficient or need paid?)
- [ ] Budget allocated if paid tier needed?
```

**Rationale:**
From STEP_0_1, STEP_0_2, STEP_2_1: All hit rate limits unexpectedly.
Adding check prevents future 18-hour delays.

**Approve this change? (yes/no/edit)**
```

---

### Step 4: Human Approves & Usher Updates

**If approved:**
```bash
# Update template file
[Apply changes]

# Commit
git add templates/CP_GUIDE_TEMPLATE.md
git commit -m "Templates: Add API rate limit check to CP guide (from Efforts 0_1, 0_2, 2_1 pattern)"
git push

# Document in TEMPLATE_EVOLUTION_LOG.md
cat >> TEMPLATE_EVOLUTION_LOG.md << 'EOF'
## 2025-12-20: Added API Rate Limit Check

**Pattern:** 6 of 10 Efforts hit API rate limits during testing
**Template updated:** CP_GUIDE_TEMPLATE.md (Spot-Check Sanity section)
**Change:** Added rate limit validation before implementation
**Impact:** Prevents 18-hour delays in future Efforts
**Efforts analyzed:** STEP_0_1, STEP_0_2, STEP_2_1, STEP_2_2, STEP_4_1, STEP_4_2
EOF
```

---

### Step 5: Repeat for All Improvements

**Systematic evolution:**
- Improvement 1: Check exists → Draft → Approve → Update
- Improvement 2: Same process
- Continue until all high-priority improvements applied

---

### Step 6: Report Evolution Complete

```
Template evolution session complete.

Templates updated: 4
- CP_GUIDE_TEMPLATE.md (added rate limit check, cross-vertical testing)
- START_HERE_TEMPLATE.md (added integration requirements detail)
- TODO_TRACKER_TEMPLATE.md (clarified update instructions)

Patterns systematized: 8
- Infrastructure reuse (saves 2-3h per Effort)
- Parallel I/O (5x performance)
- Cross-vertical testing (catches assumptions)
- Multi-tenant architecture (proven pattern)
- [4 more]

Efforts analyzed: 10 (STEP_-1 through STEP_2_1)

Next template evolution: After 10 more Efforts (Month 6)

ATLAS3 is now smarter. Future Efforts will be faster and better.
```

---

## When to Use Mode 8

**Timing:**
- After 10-15 Efforts (enough patterns to analyze)
- Quarterly (routine improvement)
- When friction is felt ("AI keeps making same mistake - fix in template")

**Don't use:**
- After 1-2 Efforts (too early, patterns unclear)
- During active Effort (focus on execution first)
- If no issues (don't fix what isn't broken)

**Frequency:** Quarterly or after 10-15 Efforts

---

## Value Proposition

**Template evolution enables:**
- Compound improvement (framework gets better, not just your knowledge)
- Systematic excellence (good patterns become defaults)
- Reduced friction (common tasks are templated)
- Faster Efforts (less re-inventing, more reusing)

**Example impact:**
- After 10 Efforts: Framework has learned 15 patterns
- Effort 11-20: Start with those 15 patterns (30% faster)
- After 20 Efforts: Framework has 30 patterns
- Effort 21-30: Start with 30 patterns (50% faster)

**Framework compounds knowledge just like you do.**

---

## Prerequisite Document Needed

**Create:** `/ATLAS3/guides/TEMPLATE_EVOLUTION_GUIDE.md`

**Should contain:**
- How to analyze patterns (statistical vs anecdotal)
- What makes good template addition (vs framework bloat)
- How to update templates safely (backward compatibility)
- How to validate changes (test on past Efforts mentally)
- Examples (good updates vs bad updates)
- Philosophy (when to add vs when to resist complexity)

**This guide teaches HOW to improve framework** (meta-level skill).

**Create this separately** (complex topic, needs ~800 lines).

---

**This mode evolves ATLAS3 itself. Use quarterly for systematic improvement.**
