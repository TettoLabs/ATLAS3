# ATLAS3 Validation Checklist

**Purpose:** Verify ATLAS3 is correctly built and operational
**Use:** After all files created, before using for real company
**Status:** Master validation document

---

## Validation Levels

**Level 1:** File Structure (all required files exist)
**Level 2:** Workflow Correctness (AI handoffs work)
**Level 3:** Progress Tracking (can always determine state)
**Level 4:** Context Management (AIs load correct files)
**Level 5:** File Ownership (clear who creates/updates/reads)
**Level 6:** Integration (all pieces connect properly)

---

## Level 1: File Structure Validation

### **Core System Files**
```bash
# Required core files
ls ATLAS3/README.md
ls ATLAS3/ATLAS_OVERVIEW.md
ls ATLAS3/ATLAS_GLOSSARY.md
ls ATLAS3/ATLAS_ENTRY_POINT.md
ls ATLAS3/ATLAS_SPECIFICATION.md  # This spec
ls ATLAS3/ATLAS_VALIDATION.md     # This file
```

**Check:** ✅ All 6 core files exist

---

### **Role Guides**
```bash
ls ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
ls ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
ls ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
ls ATLAS3/roles/AI3_DEVELOPER_BEST_PRACTICES.md
ls ATLAS3/roles/GIT_WORKFLOW.md
```

**Check:** ✅ All 5 role guides exist

---

### **Templates**
```bash
ls ATLAS3/templates/START_HERE_TEMPLATE.md
ls ATLAS3/templates/OUTLINE_TEMPLATE.md
ls ATLAS3/templates/OVERVIEW_GUIDE_TEMPLATE.md
ls ATLAS3/templates/TODO_TRACKER_TEMPLATE.md
ls ATLAS3/templates/COMPLETION_SUMMARY_TEMPLATE.md
ls ATLAS3/templates/CP_GUIDE_TEMPLATE.md
ls ATLAS3/templates/EFFORT_TEMPLATE.md
```

**Check:** ✅ All 7 templates exist

---

### **Strategy Files**
```bash
ls ATLAS3/strategy/ATLAS_STEPS_TEMPLATE.md
ls ATLAS3/strategy/ATLAS_ASSUMPTIONS.md      # Template
ls ATLAS3/strategy/LEARNINGS_LOG.md          # Template
ls ATLAS3/strategy/DECISION_LOG.md           # Template
```

**Check:** ✅ All 4 strategy files exist (templates, not filled)

---

### **Supporting Files**
```bash
ls ATLAS3/context/CONTEXT_INDEX.md
ls ATLAS3/migrations/MIGRATIONS_LOG.md
ls ATLAS3/HUMAN_GUIDE.md
ls ATLAS3/ONBOARDING.md
ls ATLAS3/QUICK_START.md
```

**Check:** ✅ All 5 supporting files exist

---

## Level 2: Workflow Correctness

### **AI1 Workflow Validation**

**Check AI1_RESEARCHER_GUIDE.md contains:**

```bash
# Must say AI1 researches ENTIRE substep (not just CP0)
grep -i "entire substep" ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
# Should find matches

# Must say AI1 produces START_HERE.md
grep -i "START_HERE" ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
# Should find matches

# Must NOT say "execute CP0"
grep -i "execute CP0" ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
# Should find ZERO matches (or only in "what NOT to do" section)

# Must define what START_HERE.md contains
grep -A10 "START_HERE.md structure" ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
# Should show: Context, Research Findings, Implementation Outcomes, CP Breakdown, For AI2
```

**Check:** ✅ AI1 workflow is correct (research entire substep, produce START_HERE)

---

### **AI2 Workflow Validation**

**Check AI2_GUIDE_CREATOR_GUIDE.md contains:**

```bash
# Must say AI2 reads START_HERE.md
grep -i "read START_HERE" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should find matches

# Must say AI2 validates AI1's research
grep -i "validate.*AI1" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should find matches

# Must say AI2 creates OUTLINE first
grep -i "create OUTLINE" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should find matches (before creating detailed guides)

# Must say AI2 researches EACH CP
grep -i "research.*each.*CP\|research.*each checkpoint" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should find matches

# Must define AI2 creates these files:
grep -i "OVERVIEW_GUIDE\|TODO_TRACKER" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should find both

# Must NOT say "AI2 creates guides for AI1"
grep -i "guide.*for AI1" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should find ZERO (AI2 only guides AI3)
```

**Check:** ✅ AI2 workflow is correct (validate, outline, research CPs, create guides for AI3)

---

### **AI3 Workflow Validation**

**Check AI3_IMPLEMENTER_GUIDE.md contains:**

```bash
# Must have pre-flight checklist
grep -i "pre-flight\|preflight" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should find section on git sync validation

# Must say update TODO_TRACKER after each CP
grep -i "update TODO_TRACKER\|update TODO" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should find matches

# Must say create COMPLETION_SUMMARY in final CP
grep -i "COMPLETION_SUMMARY\|completion summary" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should find matches

# Must say spot-check security/vulnerabilities
grep -i "security\|vulnerability\|red flag" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should find section on security gates

# Must say update ATLAS_STEPS.md when substep complete
grep -i "update ATLAS_STEPS\|mark substep complete" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should find matches
```

**Check:** ✅ AI3 workflow is correct (pre-flight, execute, update TODO, create summary, mark complete)

---

## Level 3: Progress Tracking Validation

### **Can Framework Determine Current State?**

**Test scenario: Effort is mid-execution**

**Given state:**
- STEP_1_2 Effort exists
- START_HERE.md exists (AI1 done)
- OUTLINE.md + guides exist (AI2 done)
- TODO_TRACKER shows: CP0-2 complete, CP3 in progress

**Framework should detect:**
```
Active Step: STEP 1
Active Substep: STEP_1_2
AI Phase: AI3 (guides exist)
Current CP: CP3
Next action: "Run ATLAS as AI3 for STEP_1_2, CP3"
```

**Check entry point can detect this:**

```bash
# Entry point should have auto-detection logic
grep -A20 "Auto-Detection\|Determine.*state\|Scan for.*progress" ATLAS3/ATLAS_ENTRY_POINT.md
# Should show logic that:
# 1. Finds IN_PROGRESS Effort
# 2. Checks file existence (START_HERE, OUTLINE, guides)
# 3. Reads TODO_TRACKER for current CP
# 4. Determines next action
```

**Check:** ✅ Auto-detection logic exists and is complete

---

### **Tracking at Each Level Works?**

**Step/Substep tracking (ATLAS_STEPS.md):**
```bash
# File should show how to mark Steps/Substeps complete
grep -A5 "Status:.*COMPLETE\|mark.*substep complete" ATLAS3/strategy/ATLAS_STEPS_TEMPLATE.md
# Should show examples of status tracking
```

**AI Phase tracking (file existence):**
```
START_HERE.md exists → AI1 complete
OUTLINE.md exists → AI2 started
All guides + TODO_TRACKER exist → AI2 complete, AI3 can start
COMPLETION_SUMMARY.md exists → AI3 complete, substep done
```

**CP tracking (TODO_TRACKER.md):**
```bash
# Template should show CP progress format
grep -A10 "CP0:.*COMPLETE\|CP1:.*IN_PROGRESS\|CP2:.*PENDING" ATLAS3/templates/TODO_TRACKER_TEMPLATE.md
# Should show: ✅ COMPLETE, 🔄 IN_PROGRESS, ⏸️ PENDING markers
```

**Check:** ✅ Three-level tracking is defined and clear

---

### **Who Updates What?**

**Verify file ownership is documented:**

```bash
# Should have ownership section in spec or each guide
grep -i "who updates\|updated by\|created by" ATLAS3/ATLAS_SPECIFICATION.md
# Should show clear ownership for each file type
```

**Expected ownership:**
- START_HERE.md → Created: AI1, Updated: Never
- OUTLINE.md → Created: AI2, Updated: AI2 (if CP count changes)
- Guides → Created: AI2, Updated: Rarely
- TODO_TRACKER → Created: AI2, Updated: AI3 (after each CP)
- COMPLETION_SUMMARY → Created: AI3, Updated: Never
- ATLAS_STEPS.md → Created: Human/AI2, Updated: AI3 (substep status), AI2 (strategy)
- LEARNINGS_LOG.md → Created: Framework, Updated: Human (from COMPLETION_SUMMARY)
- DECISION_LOG.md → Created: Framework, Updated: Human/AI2 (strategic decisions)

**Check:** ✅ Ownership is explicitly defined for all file types

---

## Level 4: Context Management Validation

### **AI1 Context Loading**

**Check AI1_RESEARCHER_GUIDE.md specifies files to load:**

```bash
grep -A15 "Context.*Load\|Files to.*Read\|Load.*Order" ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
# Should show ordered list:
# 1. ATLAS_OVERVIEW.md
# 2. ATLAS_GLOSSARY.md
# 3. AI1_RESEARCHER_GUIDE.md
# 4. ATLAS_STEPS.md (relevant section)
# 5. Previous COMPLETION_SUMMARY (if exists)
# 6. Company CONTEXT.md
# 7. LEARNINGS_LOG.md (recent entries)
```

**Check:** ✅ AI1 has explicit ordered file list (8-12 files, no more)

---

### **AI2 Context Loading**

```bash
grep -A20 "Context.*Load\|Files to.*Read" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should show:
# 1. ATLAS_OVERVIEW.md
# 2. AI2_GUIDE_CREATOR_GUIDE.md
# 3. START_HERE.md (from AI1)
# 4. ATLAS_STEPS.md (relevant section)
# 5. Previous COMPLETION_SUMMARY
# 6. Company CONTEXT
# 7. LEARNINGS_LOG (recent)
# 8. Templates
# 9. Previous similar Effort (optional)
```

**Check:** ✅ AI2 has explicit ordered file list (12-18 files max)

---

### **AI3 Context Loading**

```bash
# For CP0 (first CP)
grep -A15 "CP0.*context\|First.*checkpoint.*load" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should show:
# 1. OVERVIEW_GUIDE.md
# 2. TODO_TRACKER.md
# 3. START_HERE.md
# 4. effort.md
# 5. CP0_GUIDE.md
# 6. AI3_IMPLEMENTER_GUIDE.md (if first time)
# 7. AI3_DEVELOPER_BEST_PRACTICES.md (if first time)
# 8. GIT_WORKFLOW.md (if first time)

# For CP1+ (subsequent)
grep -A10 "Subsequent.*CP\|CP1.*context\|Continue.*checkpoint" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should show lighter load:
# 1. OVERVIEW_GUIDE.md (quick refresher)
# 2. TODO_TRACKER.md
# 3. CPX_GUIDE.md
# 4. Previous CP implementation notes
```

**Check:** ✅ AI3 context loading is optimized (heavy first time, light after)

---

### **No Unnecessary Loading**

**Verify AIs DON'T load:**

```bash
# AI1 should NOT load:
grep -i "AI3_DEVELOPER_BEST_PRACTICES\|GIT_WORKFLOW\|implementation guide" ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
# Should find ZERO (or only in "don't load" section)

# AI3 during CP2 should NOT load:
grep -A10 "CP2.*context\|Implementation.*CP.*load" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md | grep -i "ATLAS_STEPS\|full.*learnings"
# Should NOT require loading full ATLAS_STEPS or all LEARNINGS (only if needed)
```

**Check:** ✅ Context loading is selective (skip unnecessary files)

---

## Level 5: File Ownership Validation

### **Every File Has Clear Ownership**

**Check specification documents this:**

```bash
grep -A50 "File Ownership" ATLAS3/ATLAS_SPECIFICATION.md
# Should show table or list:
# File → Created by → Updated by → Read by → Purpose
```

**Verify for each major file type:**
- [ ] START_HERE.md ownership clear
- [ ] OUTLINE.md ownership clear
- [ ] OVERVIEW_GUIDE.md ownership clear
- [ ] CPX_GUIDE.md ownership clear
- [ ] TODO_TRACKER.md ownership clear
- [ ] COMPLETION_SUMMARY.md ownership clear
- [ ] ATLAS_STEPS.md ownership clear
- [ ] LEARNINGS_LOG.md ownership clear
- [ ] DECISION_LOG.md ownership clear

**Check:** ✅ All file types have documented ownership

---

## Level 6: Handoff Validation

### **AI1 → AI2 Handoff**

**AI1 completes when:**
- START_HERE.md created and saved to efforts/STEP_X_Y/

**Framework detects:**
- START_HERE.md exists → AI1 done

**AI2 begins when:**
- Human says "Continue ATLAS on STEP_X_Y"
- Framework detects START_HERE exists, no OUTLINE → AI2 phase

**AI2 reads:**
- START_HERE.md (primary input from AI1)
- Validates and builds on it

**Check handoff is documented:**
```bash
grep -A10 "AI1.*complete\|AI1.*→.*AI2\|handoff.*AI2" ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
# Should explicitly state: "Create START_HERE.md, then AI2 takes over"

grep -A10 "Read START_HERE\|Input from AI1" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should explicitly state: "Read START_HERE from AI1"
```

**Check:** ✅ AI1 → AI2 handoff is explicit and clear

---

### **AI2 → AI3 Handoff**

**AI2 completes when:**
- All CP guides created (CP0 through CPX)
- OUTLINE.md created
- OVERVIEW_GUIDE.md created
- TODO_TRACKER.md created

**Framework detects:**
- All guides exist + TODO_TRACKER exists → AI2 done

**AI3 begins when:**
- Human says "Continue ATLAS on STEP_X_Y"
- Framework detects guides + TODO exist → AI3 phase, reads TODO for current CP

**AI3 reads:**
- OVERVIEW_GUIDE.md (quick context)
- TODO_TRACKER.md (progress state)
- CPX_GUIDE.md (current checkpoint instructions)

**Check handoff is documented:**
```bash
grep -A10 "AI2.*complete\|ready for AI3\|AI2.*→.*AI3" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should state what files are created and that AI3 takes over

grep -A10 "Read OVERVIEW\|Read TODO_TRACKER\|from AI2" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should state AI3 reads AI2's outputs
```

**Check:** ✅ AI2 → AI3 handoff is explicit and clear

---

### **AI3 → Next Substep AI1 Handoff**

**AI3 completes when:**
- All CPs executed (per TODO_TRACKER)
- COMPLETION_SUMMARY.md created
- ATLAS_STEPS.md updated (substep marked complete)
- PR to main created (awaiting human)

**Human approves PR:**
- PR merged → Substep officially complete

**Next substep AI1 reads:**
- Previous COMPLETION_SUMMARY.md (not all artifacts - efficiency)

**Check handoff is documented:**
```bash
grep -A10 "COMPLETION_SUMMARY\|final.*task\|next.*substep" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should state: Create COMPLETION_SUMMARY in final CP

grep -A5 "previous.*COMPLETION\|read.*COMPLETION_SUMMARY" ATLAS3/roles/AI1_RESEARCHER_GUIDE.md
# Should state: Read previous substep's COMPLETION_SUMMARY
```

**Check:** ✅ AI3 → Next AI1 handoff is explicit (via COMPLETION_SUMMARY)

---

## Level 7: Checkpoint Structure Validation

### **CP0 is ALWAYS Setup**

**Check CP_GUIDE_TEMPLATE or docs say:**

```bash
grep -i "CP0.*setup\|CP0.*infrastructure\|CP0.*initialization" ATLAS3/templates/
# Should find clear statement: CP0 is setup, not research

grep -i "CP0.*research" ATLAS3/templates/
# Should find ZERO (or only in "CP0 is NOT research" context)
```

**Check:** ✅ CP0 is clearly defined as setup/initialization

---

### **Last CP is ALWAYS Testing/Deployment**

**Check docs say:**

```bash
grep -i "last.*CP\|final.*checkpoint\|CPX" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should state: Last CP is comprehensive testing + deployment

grep -A5 "CP.*testing.*deployment\|final.*CP.*testing" ATLAS3/templates/
# Should have template or guidance for final CP structure
```

**Check:** ✅ Last CP is clearly defined as testing/deployment/completion

---

### **CP Count is Variable (3-10)**

**Check AI2 guide says:**

```bash
grep -i "variable.*CP\|3-10.*checkpoint\|AI2 decides" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should state: AI2 decides CP count based on complexity
# Should give examples: Simple = 3 CPs, Complex = 8 CPs
```

**Check:** ✅ CP count is documented as flexible (not fixed at 4)

---

## Level 8: Auto-Detection Validation

### **Entry Point Has Auto-Detection**

**Check ATLAS_ENTRY_POINT.md contains:**

```bash
grep -A30 "auto-detect\|automatic.*detection\|resume work" ATLAS3/ATLAS_ENTRY_POINT.md
# Should show logic:
# 1. Find IN_PROGRESS Effort
# 2. Check START_HERE exists?
# 3. Check OUTLINE + guides exist?
# 4. Read TODO_TRACKER for current CP
# 5. Invoke appropriate AI with context
```

**Verify detection covers:**
- [ ] No START_HERE → AI1 phase
- [ ] START_HERE exists, no OUTLINE → AI2 phase (starting)
- [ ] OUTLINE exists, incomplete guides → AI2 phase (continuing)
- [ ] All guides exist, check TODO → AI3 phase
- [ ] All CPs complete → Create PR or mark Effort complete

**Check:** ✅ Auto-detection is comprehensive

---

## Level 9: Template Completeness

### **All Templates Exist**

**Required templates:**
1. [ ] START_HERE_TEMPLATE.md - Shows AI1 output structure
2. [ ] OUTLINE_TEMPLATE.md - Shows AI2 CP map structure
3. [ ] OVERVIEW_GUIDE_TEMPLATE.md - Shows effort quick-start structure
4. [ ] TODO_TRACKER_TEMPLATE.md - Shows progress tracking structure
5. [ ] COMPLETION_SUMMARY_TEMPLATE.md - Shows handoff doc structure
6. [ ] CP_GUIDE_TEMPLATE.md - Shows generic CP guide structure
7. [ ] EFFORT_TEMPLATE.md - Shows effort.md structure

**Check all exist:**
```bash
ls ATLAS3/templates/*.md | wc -l
# Should be: 7 files minimum
```

**Check:** ✅ All 7 core templates exist

---

### **Templates Have Required Sections**

**START_HERE_TEMPLATE must have:**
- Context section
- Research Findings section
- Implementation Outcomes section (very specific)
- Rough CP Breakdown section
- For AI2 section

**TODO_TRACKER_TEMPLATE must have:**
- Overall status header
- CP progress section (CP0, CP1, ... with checkboxes)
- Current CP indicator
- Notes section
- Blockers section

**COMPLETION_SUMMARY_TEMPLATE must have:**
- What Was Built section
- Key Decisions section
- What Worked section
- What Didn't Work section
- Recommendations for Next section
- Technical Foundation section

**Check each template has all sections:**
```bash
# Example for START_HERE
grep -i "## Context\|## Research Findings\|## Implementation Outcomes\|## For AI2" ATLAS3/templates/START_HERE_TEMPLATE.md
# Should find all sections
```

**Check:** ✅ Templates are complete with all required sections

---

## Level 10: Examples & Documentation

### **Workflow is Explained Correctly**

**Check ATLAS_OVERVIEW.md describes:**
- [ ] Three-phase workflow (AI1 → AI2 → AI3)
- [ ] NOT checkpoint-based roles
- [ ] Research happens before Effort (AI1)
- [ ] CP0 is setup (not research)

```bash
grep -A20 "workflow\|three.*phase\|AI1.*AI2.*AI3" ATLAS3/ATLAS_OVERVIEW.md
# Should describe correct flow
```

**Check:** ✅ Overview explains correct workflow

---

### **Examples Match Specification**

**If examples exist, verify they show:**
- AI1 producing START_HERE
- AI2 creating OUTLINE, then guides
- AI3 executing CPs with TODO updates
- COMPLETION_SUMMARY feeding next substep

```bash
# If examples directory exists
grep -i "START_HERE\|OUTLINE\|TODO_TRACKER" ATLAS3/examples/*.md
# Examples should reference new file types
```

**Check:** ✅ Examples (if exist) match specification

---

## Level 11: Integration Checks

### **Files Reference Each Other Correctly**

**OVERVIEW_GUIDE references:**
- START_HERE.md (for research context)
- CP guides (for detailed instructions)
- TODO_TRACKER.md (for progress)

**CP guides reference:**
- START_HERE.md (for research findings)
- Previous CP artifacts (for building on)
- TODO_TRACKER.md (for update instructions)

**Check cross-references work:**
```bash
# Pick a template, check it references correct files
grep -i "START_HERE\|TODO_TRACKER\|OVERVIEW" ATLAS3/templates/CP_GUIDE_TEMPLATE.md
# Should see references to other files in Effort
```

**Check:** ✅ Files are properly linked/referenced

---

### **Completion Triggers Next Phase**

**AI1 completion marker triggers AI2:**
- START_HERE.md created → Entry point detects → Suggests AI2 planning

**AI2 completion marker triggers AI3:**
- All guides + TODO_TRACKER created → Entry point detects → Starts AI3 on CP0

**AI3 CP completion triggers next CP:**
- TODO_TRACKER updated → Entry point detects next unchecked CP → Continues AI3

**Check this flow is documented:**
```bash
grep -i "completion.*marker\|triggers.*next\|detects.*ready" ATLAS3/ATLAS_ENTRY_POINT.md
# Should show detection logic
```

**Check:** ✅ Completion markers trigger next phase automatically

---

## Level 12: Testing Validation

### **Testing Happens After Each CP**

**Check CP guide templates say:**

```bash
grep -A5 "test.*after\|validation.*checkpoint\|success criteria" ATLAS3/templates/CP_GUIDE_TEMPLATE.md
# Should show: Each CP ends with testing/validation section
```

**Check:** ✅ Testing is integrated into each CP (not deferred)

---

### **Final CP Has Comprehensive Testing**

**Check final CP template or guidance says:**

```bash
grep -A10 "final.*CP\|last.*checkpoint\|comprehensive.*test" ATLAS3/roles/AI2_GUIDE_CREATOR_GUIDE.md
# Should state: Last CP includes full E2E, performance, accessibility, deployment
```

**Check:** ✅ Final CP is comprehensive testing + deployment

---

## Level 13: Security Gates

### **AI3 Has Security Checklist**

**Check AI3_IMPLEMENTER_GUIDE.md contains:**

```bash
grep -i "security\|vulnerability\|OWASP\|secrets" ATLAS3/roles/AI3_IMPLEMENTER_GUIDE.md
# Should find section on security spot-checks

# Must check for:
# - No hardcoded secrets
# - No SQL injection
# - No XSS vulnerabilities
# - Input validation
# - Authentication/authorization
```

**Check:** ✅ Security gates are defined for AI3

---

## Level 14: Git Workflow Integration

### **Staging → Main Flow**

**Check git workflow is:**
- Branch from staging (not main)
- Merge to staging after each CP (validation)
- PR staging → main (human approval)
- Never force push to main

```bash
grep -i "branch from staging\|staging.*→.*main\|never force push" ATLAS3/roles/GIT_WORKFLOW.md
# Should explicitly state this flow
```

**Check:** ✅ Git workflow matches user's actual workflow

---

## Level 15: Human Role Clarity

### **Human Responsibilities Defined**

**Check HUMAN_GUIDE.md (or equivalent) specifies:**
- [ ] Approve PRs to main (not AI3)
- [ ] Capture strategic learnings (from COMPLETION_SUMMARY to LEARNINGS_LOG)
- [ ] Quarterly strategic reviews
- [ ] Apply database migrations (manual, not auto)

```bash
grep -i "human.*approve\|human.*update\|human.*review" ATLAS3/HUMAN_GUIDE.md
# Should show human-only tasks
```

**Check:** ✅ Human role is clearly defined (what only human does)

---

## Final Validation Checklist

**Before declaring ATLAS3 ready:**

### ✓ **Structure**
- [ ] All 27+ files exist (core + roles + templates + supporting)
- [ ] Directory structure is clean (roles/, templates/, strategy/, context/, migrations/)
- [ ] No files from ATLAS1 copied without review

### ✓ **Workflow**
- [ ] AI1 workflow correct (research entire substep, produce START_HERE)
- [ ] AI2 workflow correct (validate, outline, research CPs, create guides)
- [ ] AI3 workflow correct (pre-flight, execute, update TODO, create summary)
- [ ] Handoffs explicit (AI1 → AI2 → AI3 → Next AI1)

### ✓ **Progress Tracking**
- [ ] Three-level tracking defined (Step/Substep, AI phase, CP progress)
- [ ] TODO_TRACKER shows CP status
- [ ] ATLAS_STEPS.md shows Step/Substep status
- [ ] File existence shows AI phase
- [ ] Can always determine "where are we?"

### ✓ **Context Management**
- [ ] Each AI has ordered file list (what to read, in what order)
- [ ] Context is selective (8-25 files, not 50+)
- [ ] Unnecessary files skipped (documented what NOT to load)
- [ ] Context loading optimized (heavy first time, light after)

### ✓ **File Ownership**
- [ ] Every file type has clear ownership (who creates, updates, reads)
- [ ] No ambiguity about responsibilities
- [ ] Updates are explicit (when and by whom)

### ✓ **Checkpoints**
- [ ] CP0 is setup (not research)
- [ ] CP count is variable (AI2 decides 3-10)
- [ ] Last CP is testing/deployment
- [ ] Testing after each CP (integrated, not separate)

### ✓ **Auto-Detection**
- [ ] Entry point can determine phase from files
- [ ] "Continue ATLAS on X" works (auto-loads context)
- [ ] Resume logic exists (find IN_PROGRESS, determine CP)

### ✓ **Security**
- [ ] AI3 has security checklist
- [ ] Vulnerabilities are checked
- [ ] Red flags are documented

### ✓ **Documentation**
- [ ] ATLAS_OVERVIEW explains correct workflow
- [ ] ONBOARDING shows how to configure
- [ ] QUICK_START has accurate flow
- [ ] Examples (if exist) match specification

### ✓ **Integration**
- [ ] Files reference each other correctly
- [ ] Completion markers trigger next phase
- [ ] Learnings flow to strategy
- [ ] No broken links or references

---

## Test Scenarios (Manual Validation)

### **Scenario 1: Start New Substep**

**Action:** "Run ATLAS to research STEP_1_1"

**Expected:**
1. Framework detects: No START_HERE for STEP_1_1 → AI1 phase
2. AI1 loads: OVERVIEW, GLOSSARY, AI1 guide, ATLAS_STEPS (Step 1, Substep 1.1), Company CONTEXT, LEARNINGS
3. AI1 researches (6 hours)
4. AI1 creates: efforts/STEP_1_1/START_HERE.md
5. AI1 reports: "Research complete, ready for AI2 planning"

**Verify:** ✅ START_HERE.md exists and is comprehensive

---

### **Scenario 2: Continue to Planning**

**Action:** "Continue ATLAS on STEP_1_1"

**Expected:**
1. Framework detects: START_HERE exists, no OUTLINE → AI2 phase
2. AI2 loads: OVERVIEW, AI2 guide, START_HERE, ATLAS_STEPS, LEARNINGS, templates
3. AI2 validates AI1's research
4. AI2 creates OUTLINE (decides 4 CPs)
5. AI2 researches each CP deeply
6. AI2 creates 4 guides (CP0-CP3)
7. AI2 creates OVERVIEW_GUIDE, TODO_TRACKER
8. AI2 reports: "Planning complete, ready for AI3"

**Verify:**
- ✅ OUTLINE.md exists
- ✅ 4 guides exist (CP0-CP3)
- ✅ OVERVIEW_GUIDE.md exists
- ✅ TODO_TRACKER.md exists (all CPs marked PENDING)

---

### **Scenario 3: Start Execution**

**Action:** "Continue ATLAS on STEP_1_1"

**Expected:**
1. Framework detects: Guides exist, TODO_TRACKER shows all PENDING → AI3 phase, CP0
2. AI3 loads: OVERVIEW_GUIDE, TODO_TRACKER, START_HERE (brief), CP0_GUIDE, role guides
3. AI3 does pre-flight (git sync)
4. AI3 executes CP0 (setup)
5. AI3 updates TODO_TRACKER (marks CP0 complete)
6. AI3 reports: "CP0 complete, ready for CP1"

**Verify:**
- ✅ CP0 tasks executed
- ✅ TODO_TRACKER updated (CP0 marked ✅)
- ✅ Git branch created

---

### **Scenario 4: Resume After Pause**

**State:** Effort paused mid-execution (CP2 of 5 complete)

**Action:** "Continue ATLAS on STEP_1_1"

**Expected:**
1. Framework scans: efforts/STEP_1_1/effort.md shows IN_PROGRESS
2. Reads TODO_TRACKER: CP0-2 complete, CP3 pending
3. Detects: AI3 phase, current CP is CP3
4. Loads: OVERVIEW_GUIDE, TODO_TRACKER, CP3_GUIDE, CP2 notes
5. AI3 continues from CP3 (doesn't redo CP0-2)

**Verify:** ✅ Resumes at correct CP, doesn't redo completed work

---

### **Scenario 5: Complete Substep**

**State:** CP4 (last CP) complete

**Expected:**
1. AI3 creates COMPLETION_SUMMARY.md
2. AI3 updates ATLAS_STEPS.md (marks STEP_1_1 complete)
3. AI3 creates PR staging → main
4. AI3 reports: "Substep complete, awaiting PR approval"
5. Human approves PR, merges
6. Substep officially complete

**Verify:**
- ✅ COMPLETION_SUMMARY.md exists and is comprehensive
- ✅ ATLAS_STEPS.md updated (STEP_1_1 marked ✅)
- ✅ PR exists
- ✅ Ready for next substep (STEP_1_2)

---

## Red Flags (Framework is Broken)

**🚩 Warning signs ATLAS3 has issues:**

**Workflow:**
- AI1 guide says "execute CP0"
- AI2 creates "guides for AI1"
- CP0 is labeled "research phase"
- Fixed 4 checkpoints (CP0-CP3) with no mention of variability

**Progress:**
- No TODO_TRACKER.md
- No way to determine current CP
- Can't resume work after pause
- Manual state tracking required

**Context:**
- AIs load 40+ files
- Full ATLAS_STEPS.md loaded (not just relevant Step)
- All LEARNINGS loaded (not recent entries)
- Context explosion warnings

**Ownership:**
- Unclear who updates LEARNINGS_LOG
- Unclear who creates COMPLETION_SUMMARY
- Ambiguous about TODO_TRACKER updates

**If 3+ red flags:** Stop. Framework is broken. Re-evaluate against specification.

---

## Success Indicators (Framework is Correct)

**✅ Green flags ATLAS3 is well-built:**

**Workflow:**
- AI1 guide clearly says "research entire substep"
- AI2 guide says "read START_HERE, validate, research each CP"
- CP0 is setup/infrastructure
- CP count is variable (AI2 decides)

**Progress:**
- TODO_TRACKER exists and is updated by AI3
- Can determine state from file scanning
- "Continue work" auto-resumes at correct CP
- Three-level tracking (Step, AI phase, CP)

**Context:**
- Context loading is 8-25 files max
- Selective loading rules (relevant section only)
- Each AI has explicit ordered list
- No unnecessary file loading

**Ownership:**
- Every file type has documented ownership
- Clear who creates, updates, reads
- No ambiguity

**If 10+ green flags:** ✅ Framework is well-designed. Proceed with confidence.

---

## Final Sign-Off

**Before using ATLAS3 for your company:**

**Human validates:**
- [ ] Read ATLAS_SPECIFICATION.md (understand correct workflow)
- [ ] Read this ATLAS_VALIDATION.md (understand validation process)
- [ ] All Level 1-15 checks pass
- [ ] Test scenarios work (manually trace through)
- [ ] No red flags present
- [ ] Confident framework is correct

**If all checked:** ✅ ATLAS3 is ready for production use

**If any unchecked:** Address issues before using framework

---

**This validation ensures ATLAS3 works correctly for building billion-dollar companies. Measure thrice. Cut once.** ✅
