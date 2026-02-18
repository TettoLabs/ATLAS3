# ATLAS Steps Template - How to Define Strategic Steps

**Purpose:** Instructions for creating/maintaining `ATLAS_STEPS.md`
**Audience:** Strategic AI (AI2 in strategic mode) or human strategist
**Status:** v1.0 template

---

## What This File Is

This is a **template and instruction guide** for creating the actual `ATLAS_STEPS.md` file.

`ATLAS_STEPS.md` is the **master strategy document** that defines what needs to happen for a project/company to succeed.

**This file (the template) explains HOW to write that file.**

---

## Core Principles for Defining Steps

### 1. Steps Are Strategic, Not Tactical

**Good Step:**
> "Acquire first 3 paying customers"

**Bad Step:**
> "Set up Stripe account and add payment buttons"
↑ This is a task, not a Step

**Why it matters:**
- Steps answer "WHAT must become true?"
- Tasks answer "HOW do we do it?"
- ATLAS handles HOW through Efforts and Checkpoints
- You define WHAT through Steps

---

### 2. Steps Should Be Outcome-Focused

**Good Step:**
> "Validate your company positioning with 5 real customer conversations"

**Bad Step:**
> "Do customer development"
↑ Too vague, no concrete outcome

**Why it matters:**
- Clear outcomes = clear success criteria
- Vague goals = endless work
- Outcome focus enables learning (did we achieve it? why/why not?)

---

### 3. Steps Should Be "Big Enough to Matter"

**Too small (not a Step):**
> "Buy domain name"
↑ This is a subtask

**Too large (needs Substeps):**
> "Build and launch entire SaaS platform"
↑ This could be 6 months - needs breakdown

**Just right:**
> "Ship MVP of SaaS with 3 core features and onboarding"
↑ Meaningful milestone, achievable scope

**Rule of thumb:**
- If Step takes <2 weeks → probably too small (make it a task)
- If Step takes >8 weeks → probably too large (break into Substeps)
- If Step takes 2-8 weeks → probably right-sized

---

### 4. Substeps Refine Large Steps

When a Step is too big, break it into Substeps (X.Y numbering).

**Example:**

**Step 1:** "Acquire first 10 customers"
↑ This could take months

**Broken into Substeps:**
- **Substep 1.1:** "Close first 3 customers"
- **Substep 1.2:** "Close next 4 customers (7 total)"
- **Substep 1.3:** "Close final 3 customers (10 total)"

**Why Substeps:**
- Each Substep is Effort-sized (1-4 weeks)
- Incremental progress visible
- Can adjust strategy between Substeps based on learnings

---

## Step Definition Format

Each Step should include:

### **Step Number & Title**
```markdown
## STEP 1: [Clear, Outcome-Focused Title]
```

### **Objective**
What must become true? 1-2 sentences.

### **Why This Matters**
Strategic rationale. How does this advance the company/project?

### **Success Criteria**
Concrete, measurable outcomes. How do we know when Step is complete?

### **Substeps (if applicable)**
If Step is large, break into X.Y substeps. Each substep should be Effort-sized.

### **Dependencies**
What must be complete before this Step? (Optional - use sparingly)

### **Hypotheses (optional)**
What are we testing with this Step? What do we expect to learn?

---

## Example Step (Full Format)

```markdown
## STEP 1: Acquire First 3 Paying Customers

### Objective
Close 3 paid contracts for website redesign + hosting, validating our go-to-market approach and service delivery model.

### Why This Matters
- Revenue validation (proves people will pay)
- Service delivery learning (refine process before scaling)
- Case study creation (testimonials for future sales)
- Positioning refinement (discover what resonates)

### Success Criteria
- [ ] 3 contracts signed ($5K-$10K each)
- [ ] 3 websites delivered and launched
- [ ] 3 customers on monthly hosting/maintenance ($200-$500/mo each)
- [ ] Learnings documented about:
  - What customers care most about
  - Where our process broke down
  - What we should systematize next

### Substeps

#### STEP_1_1: Close First Customer
- **Target:** 1 signed contract, site delivered
- **Timeline:** 3-4 weeks
- **Focus:** Prove we can deliver end-to-end

#### STEP_1_2: Close Second Customer
- **Target:** 1 signed contract, site delivered
- **Timeline:** 2-3 weeks (faster with learnings)
- **Focus:** Refine sales pitch and delivery process

#### STEP_1_3: Close Third Customer
- **Target:** 1 signed contract, site delivered
- **Timeline:** 2-3 weeks
- **Focus:** Systematize what's working

### Dependencies
- **Before starting:**
  - your company brand defined (logo, positioning, site)
  - Sales process documented
  - Service delivery workflow established

- **Blocks:**
  - Step 2 (building internal tools) - need customer insights first

### Hypotheses Being Tested
1. **H1:** Local service businesses will pay $5K-$10K for professional redesign
   - **Expected:** Yes, if we show compelling demo
   - **Measurement:** Conversion rate from demo to contract

2. **H2:** Proactive demo approach (we build first) beats traditional sales
   - **Expected:** Yes, shows vs tells
   - **Measurement:** Time to close, objection patterns

3. **H3:** Post-launch hosting creates recurring revenue
   - **Expected:** Yes, they want hands-off maintenance
   - **Measurement:** % of customers choosing hosting package
```

---

## Substep Numbering Rules

### Format: `STEP_X_Y`

**Examples:**
- STEP_1_1 (Step 1, Substep 1)
- STEP_1_2 (Step 1, Substep 2)
- STEP_3_4 (Step 3, Substep 4)

### When to Use Substeps

**Use when:**
- Step would take >8 weeks
- Step has natural phases (design → build → launch)
- Want incremental validation (close 3, then 7 more)

**Don't use when:**
- Step is already Effort-sized (2-4 weeks)
- Breakdown doesn't add clarity
- Substeps would be arbitrary

### Substep Guidelines

Each Substep should:
- ✅ Be independently completable
- ✅ Produce meaningful progress
- ✅ Take 1-4 weeks
- ✅ Have clear success criteria

---

## Step Sequencing

### Sequential Steps (Default)
```markdown
STEP 1: Acquire 3 customers
STEP 2: Build internal evaluation tool
STEP 3: Launch SaaS MVP
```
↑ Step 2 depends on learnings from Step 1

### Parallel Steps (Rare)
```markdown
STEP 1: Acquire 3 customers
STEP 2: Build company brand site (can happen in parallel)
```
↑ Mark explicitly: "Can run parallel to Step 1"

**Default assumption: Steps are sequential unless marked otherwise.**

---

## Evolution and Refinement

### ATLAS_STEPS.md Is a Living Document

**It WILL change:**
- New Steps added based on learnings
- Substeps refined
- Success criteria adjusted
- Hypotheses updated

**How to update:**
1. Complete a Step or Substep
2. Capture learnings in `LEARNINGS_LOG.md`
3. Review strategic implications
4. Update `ATLAS_STEPS.md` if needed
5. Log decision in `DECISION_LOG.md`

**Version Steps:**
```markdown
## STEP 1: Acquire First 3 Customers (v2 - Updated 2025-12-15)

[Updated based on learnings from STEP_1_1]
[Original: "Acquire 5 customers" - revised down based on delivery capacity]
```

---

## Common Mistakes to Avoid

### ❌ Mistake 1: Steps That Are Tasks
**Bad:**
> "Set up hosting infrastructure"

**Why bad:** This is a task, not a strategic outcome

**Fix:**
> "Deploy first customer site to production with <2sec load time"
↑ Outcome-focused, meaningful

---

### ❌ Mistake 2: Vague Steps
**Bad:**
> "Improve website quality"

**Why bad:** What's "quality"? How do we know when done?

**Fix:**
> "Implement site evaluation checklist covering speed, mobile, SEO, and accessibility (tested on 10 sites)"
↑ Concrete, measurable

---

### ❌ Mistake 3: Too Many Steps Upfront
**Bad:**
Creating STEP 1 through STEP 20 on Day 1

**Why bad:** You don't know what Step 15 should be yet - strategy will evolve

**Fix:**
- Define next 2-3 Steps clearly
- Outline next 3-5 Steps loosely
- Leave Steps 8+ undefined until you get closer
- Add Steps as you learn

---

### ❌ Mistake 4: Hard-Coding Dates
**Bad:**
> "STEP 1: Launch by March 15, 2025"

**Why bad:** Dates become stale, Steps get re-ordered

**Fix:**
> "STEP 1: Launch MVP (estimated: 6-8 weeks from Step 0 completion)"
↑ Relative timing, not absolute dates

---

## Step Lifecycle States

Track Step progress with simple states:

**States:**
- **PLANNED** - Defined, not started
- **ACTIVE** - Currently executing (has active Efforts)
- **COMPLETE** - Success criteria met, learnings captured
- **PAUSED** - Started but deprioritized
- **REVISED** - Changed based on learnings (note version)

**Example:**
```markdown
## STEP 1: Acquire First 3 Customers
**Status:** COMPLETE (2025-12-20)
**Outcome:** 3 customers acquired, $22K revenue, hosting packages all signed
**Learnings:** [Link to LEARNINGS_LOG entries]
```

---

## Integration with Efforts

### How Steps → Efforts

**Each Substep becomes ONE Effort (usually):**

```
STEP 1: Acquire 3 customers
  ├─ STEP_1_1 → EFFORT: STEP_1_1_FIRST_CUSTOMER
  ├─ STEP_1_2 → EFFORT: STEP_1_2_SECOND_CUSTOMER
  └─ STEP_1_3 → EFFORT: STEP_1_3_THIRD_CUSTOMER
```

**Or, if no Substeps:**

```
STEP 2: Build evaluation tool
  └─ EFFORT: STEP_2_EVAL_TOOL
```

**One Substep → Multiple Efforts (rare but allowed):**

```
STEP 3: Launch SaaS MVP
  └─ STEP_3_1: Design and validate MVP features
       ├─ EFFORT: STEP_3_1_FEATURE_DESIGN
       └─ EFFORT: STEP_3_1_USER_TESTING
```

**Rule:** Keep it simple. Default: 1 Substep = 1 Effort.

---

## Template for ATLAS_STEPS.md

Use this structure when creating your actual `ATLAS_STEPS.md`:

```markdown
# ATLAS Steps - [Project Name]

**Project:** [e.g., your company]
**Version:** 1.0
**Last Updated:** [Date]
**Status:** [X Steps defined, Y complete, Z in progress]

---

## Overview

[1-2 paragraphs: What is this project? What's the strategic goal?]

---

## STEP 1: [Title]

### Objective
[What must become true]

### Why This Matters
[Strategic rationale]

### Success Criteria
- [ ] [Measurable outcome 1]
- [ ] [Measurable outcome 2]

### Substeps (if applicable)

#### STEP_1_1: [Title]
- **Target:** [Outcome]
- **Timeline:** [Estimate]
- **Focus:** [What we're learning/validating]

[Repeat for all Substeps]

### Dependencies
[What must be done first, if anything]

### Hypotheses
[What we're testing, optional]

---

## STEP 2: [Title]

[Same structure]

---

[Continue for all Steps]

---

## Step Status Summary

| Step | Status | Completion | Learnings |
|------|--------|------------|-----------|
| 1    | COMPLETE | 2025-12-20 | [Link]   |
| 2    | ACTIVE   | In progress | N/A     |
| 3    | PLANNED  | Not started | N/A     |

---

## Strategic Adjustments Log

### [Date]: [Change Description]
- **What changed:** [e.g., "Reduced Step 1 from 5 to 3 customers"]
- **Why:** [e.g., "Learnings showed delivery capacity constraint"]
- **Impact:** [e.g., "Faster completion, but need more Steps for revenue target"]
```

---

## Quality Checklist for ATLAS_STEPS.md

Before finalizing Steps, verify:

**✓ Strategic Clarity**
- [ ] Each Step has clear objective (outcome-focused)
- [ ] Each Step has "why this matters" (strategic rationale)
- [ ] Success criteria are measurable
- [ ] Steps advance overall project/company goal

**✓ Right-Sized**
- [ ] Each Step is 2-8 weeks (or has Substeps)
- [ ] Substeps (if used) are Effort-sized (1-4 weeks)
- [ ] Not too granular (tasks) or too vague (themes)

**✓ Sequencing**
- [ ] Step order makes sense (foundations before features)
- [ ] Dependencies noted
- [ ] Parallel Steps marked explicitly

**✓ Learnings Integration**
- [ ] Hypotheses defined (what we're testing)
- [ ] Clear how learnings will inform next Steps
- [ ] Feedback loop to LEARNINGS_LOG established

**✓ Maintainability**
- [ ] Version numbers if Steps change
- [ ] Status tracking (PLANNED/ACTIVE/COMPLETE)
- [ ] Links to Efforts and artifacts

---

## Related Documentation

- `ATLAS_OVERVIEW.md` - System overview
- `ATLAS_GLOSSARY.md` - Terminology (Step, Substep, Effort)
- `LEARNINGS_LOG.md` - Captures discoveries that inform strategy
- `DECISION_LOG.md` - Records strategic decisions
- `efforts/README.md` - How Efforts map to Steps

---

## Now Create Your ATLAS_STEPS.md

Use this template and principles to create:

`/ATLAS/strategy/ATLAS_STEPS.md`

**Start with:**
- Project name and overview
- First 2-3 Steps (clearly defined)
- Next 3-5 Steps (loosely sketched)
- Status tracking structure

**Remember:**
- Steps will evolve - that's expected
- Strategy sharpens through execution
- Capture learnings, adjust Steps, repeat

**Good luck building your company, systematically. 🏗️**
