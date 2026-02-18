# Outline - [Effort Name]

**Effort:** STEP_X_Y_[SHORTNAME]
**Created by:** AI2
**Date:** [YYYY-MM-DD]
**Total Checkpoints:** [X] (AI2 decision)
**Estimated Duration:** [X days/weeks]

---

## Instructions for AI2

This template defines the structure for OUTLINE.md (your high-level checkpoint map).

**Create this FIRST** (before detailed CP guides).

**Purpose:** Show checkpoint structure at a glance, document CP count decision.

**Length:** 200-400 lines (high-level, not detailed)

---

## Effort Summary

**What we're building:**
[1-2 paragraphs describing the deliverable]

**Strategic importance:**
[Why this Effort matters to overall company goals]

**Builds on:**
[Previous substeps, if applicable - what foundation exists]

---

## Checkpoint Breakdown

**Total checkpoints:** [X] (AI2 decision based on complexity)

---

### CP0: Infrastructure Setup

**Role:** AI3 (Implementer)
**Duration:** [2-6 hours estimated]
**Type:** Setup/Initialization (always first checkpoint)

**Goal:**
[1-2 sentences: What infrastructure is prepared]

**Key tasks:**
- [Task 1: Git branch creation]
- [Task 2: Service initialization (Vercel, Supabase, etc.)]
- [Task 3: Environment configuration]
- [Task 4: Dependency installation]
- [Task 5: Initial deployment validation]

**Output:**
- Infrastructure operational (can build features in CP1+)
- Git branch created
- Deployment pipeline verified

**Success criteria:**
- Build succeeds
- Deployment works
- Database accessible (if applicable)

---

### CP1: [Implementation Phase 1 Name]

**Role:** AI3 (Implementer)
**Duration:** [X hours/days estimated]
**Type:** Implementation

**Goal:**
[1-2 sentences: What this checkpoint accomplishes]

**Key tasks:**
- [High-level task 1]
- [High-level task 2]
- [High-level task 3]

**Output:**
[What exists after this CP - deliverables, code, features]

**Success criteria:**
- [How to know CP1 is complete]
- [Measurable outcomes]

**Dependencies:**
- Requires: CP0 complete (needs infrastructure)

---

### CP2: [Implementation Phase 2 Name]

**Role:** AI3
**Duration:** [X hours/days]
**Type:** Implementation

**Goal:**
[What CP2 accomplishes]

**Key tasks:**
[High-level task list]

**Output:**
[Deliverables]

**Success criteria:**
[How to validate complete]

**Dependencies:**
- Requires: CP1 complete (builds on CP1 output)

---

### CP3: [Continue for all middle CPs]

[Same structure for CP3, CP4, ..., CPX-1]

---

### CPX: Testing & Deployment (Final checkpoint)

**Role:** AI3 (Implementer) + Human (approval)
**Duration:** [1-2 days estimated]
**Type:** Comprehensive Validation & Production Launch (always last checkpoint)

**Goal:**
Validate all work, deploy to production, create handoff documentation

**Key tasks:**
- Comprehensive testing (E2E, performance, accessibility, security)
- Cross-vertical validation (if multi-vertical tool)
- Full staging validation
- Create PR to main (human approves)
- Production deployment (after PR merge)
- Create COMPLETION_SUMMARY.md
- Update ATLAS_STEPS.md (mark substep complete)
- Post-launch monitoring

**Output:**
- Production deployment (live at [URL])
- COMPLETION_SUMMARY.md (handoff to next substep)
- Updated ATLAS_STEPS.md (progress tracking)
- All quality gates passed

**Success criteria:**
- All Effort success criteria met (from effort.md)
- Comprehensive testing passed
- Production stable (no critical errors in first 24h)
- COMPLETION_SUMMARY comprehensive

**Dependencies:**
- Requires: All previous CPs complete (CP0 through CPX-1)

---

## Rationale for [X] Checkpoints

**Why [X] checkpoints and not fewer?**

[Explain reasoning:]
- Example: "Why 5 not 3? Because scraping, extraction, and generation are distinct concerns. Combining into one 'implement everything' CP would be >1 week (too large for single checkpoint). Splitting enables incremental testing and clearer progress tracking."

**Why [X] checkpoints and not more?**

[Explain reasoning:]
- Example: "Why 5 not 8? Because over-splitting creates overhead (too many handoffs, too much documentation). Content extraction could be split (HTML, CSS, JS, images), but keeping together maintains cohesion and is still <1 week per CP."

**Could adjust to [X-1] if:**
[Conditions under which fewer CPs makes sense]
- Example: "Could be 4 if time pressure (combine CP2+CP3 extraction and generation). Trade-off: Larger checkpoint, less incremental validation, but faster overall."

**Could adjust to [X+1] if:**
[Conditions under which more CPs makes sense]
- Example: "Could be 6 if complexity increases (split CP1 into scraping + asset management). Trade-off: More checkpoints, more granular testing, but slower due to handoffs."

**Decision:** [X] CPs balances [testability/speed/clarity/granularity]

---

## Dependencies Between Checkpoints

**Sequential order required:**

```
CP0 (Setup)
  ↓ Produces infrastructure
CP1 (First implementation)
  ↓ Produces core functionality
CP2 (Second implementation)
  ↓ Produces additional features
...
CPX (Testing & Deploy)
  ↓ Produces production deployment
```

**No parallel checkpoints.** Each CP builds on previous.

**Why sequential:**
- CP1 needs CP0's infrastructure
- CP2 needs CP1's core functionality
- CPX needs all previous CPs complete (comprehensive testing)

**If CPs could be parallel:**
[Note if any CPs are independent - rare but document if true]

---

## Testing Strategy

**After each CP (incremental validation):**
- Build must succeed (npm run build)
- Unit tests must pass (npm test)
- Lint must be clean (npm run lint)
- Manual testing (feature works as expected)
- Merge to staging (preview deployment for validation)

**Final CP (comprehensive validation):**
- **E2E testing:** [Specific flows to test end-to-end]
- **Performance:** [Lighthouse 90+, <2s mobile, specific targets]
- **Accessibility:** [WCAG AA, axe DevTools scan, zero critical errors]
- **Cross-vertical:** [If applicable - test on contractor, law, healthcare sites]
- **Security:** [No secrets, no vulnerabilities, input validation]
- **Load testing:** [If applicable - can handle expected traffic]
- **Staging validation:** [Full manual test on deployed staging environment]

**Quality gates (all must pass):**
- Performance targets met (from effort.md success criteria)
- Accessibility compliant (WCAG AA minimum)
- Security validated (no vulnerabilities)
- Cross-vertical working (if applicable)
- All Effort success criteria met

---

## Key Risks & Mitigations

**From AI1's research, key risks for this Effort:**

**Risk 1:** [Title]
- **Mitigation in CP[X]:** [How specific checkpoint addresses this]

**Risk 2:** [Title]
- **Mitigation in CP[X]:** [How handled]

**General mitigations:**
- Incremental testing (after each CP)
- Staging validation (before production)
- Rollback plans (documented in guides)

---

## Effort Estimate

**Total effort:** [X] days/weeks

**Breakdown:**
- CP0: [X hours]
- CP1: [X days]
- CP2: [X days]
- ...
- CPX: [X days]

**Buffer:** +20% ([Y] days) for unknowns, testing, fixes

**Expected completion:** [Date]

**Critical path:**
[Which CPs are critical? Which have slack?]

---

## Next Steps for AI2

**After creating this OUTLINE:**

1. **Get human approval (optional but recommended for complex Efforts)**
   - Share OUTLINE with human
   - Confirm CP structure makes sense
   - Adjust if needed based on feedback

2. **Research CP0 deeply (1-2 hours)**
   - What does setup entail specifically?
   - Find examples and patterns

3. **Create CP0_GUIDE.md (1 hour)**
   - Detailed instructions for AI3

4. **Repeat for all CPs (2-4 hours per CP)**
   - Research each individually
   - Create guide for each

5. **Create OVERVIEW_GUIDE.md (30-45 min)**
   - Synthesize all CPs into quick-start

6. **Create TODO_TRACKER.md (15-30 min)**
   - List all CPs as PENDING

7. **Create effort.md (15 min)**
   - High-level overview

8. **Report AI2 complete**
   - Ready for AI3

---

## Related Documents

**This OUTLINE connects to:**
- **START_HERE.md** - AI1's research (your input)
- **CP guides** - Detailed instructions (you'll create these next)
- **OVERVIEW_GUIDE.md** - Quick-start (you'll create after guides)
- **TODO_TRACKER.md** - Progress tracking (you'll create)
- **effort.md** - High-level overview (you'll create)

---

**This OUTLINE is the roadmap. Make it clear and well-reasoned.**
