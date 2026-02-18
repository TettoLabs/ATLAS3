# Mode 5: Learning Capture - Extract from COMPLETION_SUMMARY

**Purpose:** Help extract strategic learnings from Effort completion
**Usage:** Weekly (after each Effort completes)
**Trigger:** Human says "Capture learnings from STEP_X_Y" or Friday learning session

---

## What This Mode Does

**Reduces friction on critical weekly task:**

**Current pain:**
- Human manually reads COMPLETION_SUMMARY (500-1,000 lines)
- Extracts 3-5 strategic learnings
- Writes in LEARNINGS_LOG format
- Takes 30-60 minutes
- Often skipped (busy, feels like overhead)

**With Usher Mode 5:**
- Usher reads COMPLETION_SUMMARY
- Drafts 3-5 learning entries (extracts key discoveries)
- Human reviews/refines (10 minutes vs 30)
- Usher adds to LEARNINGS_LOG.md (formatted correctly)

**Time savings:** 20-30 minutes per Effort (20 Efforts = 10 hours saved)

---

## Files Usher Loads

```
1. COMPLETION_SUMMARY.md for specified Effort
   File: efforts/STEP_X_Y_[NAME]/COMPLETION_SUMMARY.md
   Lines: ~500-1,000
   Tokens: ~8K
   Time: 8 min

2. LEARNINGS_LOG.md (to append to)
   Lines: Current state (might be 1,000-3,000)
   Tokens: ~15K
   Time: 5 min (skim recent to avoid duplicates)

3. LEARNINGS_LOG template (format reference)
   File: templates/LEARNINGS_LOG_FORMAT.md (if exists)
   OR: Extract format from existing entries
   Tokens: ~2K
   Time: 2 min

4. COMPANY_CONTEXT.md (strategic frame)
   Tokens: ~4K
   Time: 3 min (focus on success definition, hypotheses)

Total: ~1,500-2,000 lines, ~29K tokens, ~18 min
```

---

## Workflow: Extract & Format Learnings

### Step 1: Read COMPLETION_SUMMARY

**Usher analyzes sections:**
- "What Worked" → Extract patterns to repeat
- "What Didn't Work" → Extract lessons to avoid
- "Key Decisions" → Extract approaches that worked/failed
- "Tactical Learnings" → Extract discoveries with strategic implications

---

### Step 2: Draft Learning Entries

**Usher creates 3-5 entries:**

```markdown
## 2025-12-20: STEP_0_2_SITE_CLONER - Parallel I/O 5x Faster Than Sequential

**Context:** Building Site Cloner tool, needed to download 50+ assets per cloned site.

**Discovery:** Parallel asset downloads (Promise.all with concurrency limit: 10) completed in 90 seconds vs sequential download taking 8 minutes.

**Evidence:**
- Sequential: 50 images × 10s average = 500s (8.3 minutes)
- Parallel (10 concurrent): 50 images / 10 batches × 9s per batch = 90 seconds
- 5.5x performance improvement

**Implications:**
- **Strategy:** Not applicable (tactical optimization, not strategic)
- **Execution:** Make parallel I/O the default pattern for all future Efforts (network, file system)
- **Future Efforts:** Start with parallelization (don't optimize sequentially first, then refactor)

**Actions Taken:**
- [x] Updated AI3_DEVELOPER_BEST_PRACTICES.md (added "Parallelize I/O" section)
- [x] Documented pattern in STEP_0_2 COMPLETION_SUMMARY (reusable code reference)
- [ ] Apply in STEP_0_3 (Rebuild Engine will need asset handling - use parallel pattern)

---

## 2025-12-20: STEP_0_2 - Cross-Vertical Testing Catches Assumptions Early

**Context:** Testing Site Cloner on diverse sites (contractor, law, healthcare).

**Discovery:** Law firm sites use different color schemes (navy/gray vs contractor blue/orange). Universal color detection algorithm initially failed for law firms (hardcoded blue extraction).

**Evidence:**
- Tested on 10 contractor sites: 100% success
- Tested on 3 law firm sites: 2 of 3 failed (color scheme incorrect)
- Fixed universal color detection: All sites now work (tested on 15 diverse sites)

**Implications:**
- **Strategy:** Cross-vertical testing is CRITICAL, not optional. Must be in every tool Effort.
- **Execution:** Test on all 3 verticals (contractor, law, healthcare) in CP3-4 (not just final CP)
- **Future Efforts:** Add "cross-vertical validation" to all multi-vertical tool success criteria

**Actions Taken:**
- [x] Made cross-vertical testing mandatory in Rebuild Engine planning (STEP_0_3)
- [x] Updated ATLAS_STEPS success criteria (all tools must validate on 3 verticals)
- [x] Fixed color detection (now universal)

---

[Usher drafts 3-5 total, extracting most strategic discoveries]
```

---

### Step 3: Human Reviews & Refines

**Usher presents:**
```
Extracted 4 learning entries from STEP_0_2 COMPLETION_SUMMARY.

Entry 1: Parallel I/O 5x faster
Entry 2: Cross-vertical testing catches assumptions
Entry 3: Reusing infrastructure saves 30% setup time
Entry 4: Template system complexity risk (over-engineering)

Review each:
1. Approve as-is
2. Edit (provide refinements)
3. Skip (not strategic enough)
4. Add entry (I missed something important)

What would you like to do?
```

**Human refines:**
- Might add business context ("This enables faster customer delivery")
- Might adjust implications ("Actually, this changes our pricing model because...")
- Might combine entries ("Entries 1 and 3 are related")

---

### Step 4: Append to LEARNINGS_LOG

**After human approval, Usher adds to LEARNINGS_LOG.md:**

```bash
# Append entries to file
cat >> /ATLAS3/strategy/LEARNINGS_LOG.md << 'EOF'

[Entry 1]
[Entry 2]
[Entry 3]
[Entry 4]

EOF

# Commit
git add strategy/LEARNINGS_LOG.md
git commit -m "Learnings: Added 4 entries from STEP_0_2 completion"
git push
```

**Usher reports:**
```
Learning capture complete.

Added to LEARNINGS_LOG.md:
- 4 entries from STEP_0_2 (Site Cloner)
- Tagged: technical, multi-vertical, performance, infrastructure

Total learnings: 18 entries (across 3 completed Efforts)

Next: These learnings will inform AI1's research for STEP_0_3 (Rebuild Engine)
```

---

## When to Use Mode 5

**Use:**
- After every Effort completion (Friday afternoon learning session)
- Weekly discipline (capture while fresh)
- Before planning next Effort (ensure learnings are in log for AI1/AI2 to read)

**Time:**
- Without Mode 5: 30-60 minutes (manual extraction)
- With Mode 5: 10-15 minutes (Usher drafts, human refines)

**Savings:** 20-45 minutes per Effort × 20 Efforts = 10+ hours saved

---

**This mode makes learning capture easy. Use it every week.**
