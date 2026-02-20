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
- STEP 0: Build Core Features
  - STEP_0_1: User Dashboard ✅ COMPLETE (2025-12-15)
  - STEP_0_2: Payment System 🔄 IN_PROGRESS (AI3 on CP3 of 5)
  - STEP_0_3: Notification Service ⏸️ PLANNED
- STEP 1: Launch Beta
  - STEP_1_1: First Beta Users ⏸️ PLANNED
  - STEP_1_2-1_10: Expand to 10 users ⏸️ PLANNED
- STEP 2: Build Marketing Site ⏸️ PLANNED

**PART 2: Scale (Steps 3-5)**
- STEP 3: Scale to 25 Active Users ⏸️ PLANNED
- STEP 4: Add Premium Tier ⏸️ PLANNED
- STEP 5: Launch Public v1.0 ⏸️ PLANNED

**PART 3: Platform (Steps 6-10)**
- All PLANNED (will be defined after Part 2 learnings)

**Overall progress:**
- Steps complete: 2 of 10 (20%)
- Substeps complete: 2 of 50+ (4%)
- Current work: STEP_0_2 (Payment System, 60% done)
- Next planned: STEP_0_3 (Notification Service)

**Recent learnings (last 5):**
1. Multi-tenant architecture pays off (STEP_0_1, STEP_0_2)
2. Early user testing critical (caught UX assumptions)
3. Reusing infrastructure saves 30-40% setup time
4. API rate limits require retry logic with exponential backoff
5. Shared component patterns proven (use across features)
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

**Human selects: "Refine STEP_0_3 (Notification Service)"**

**Usher loads additional context:**

```
8. STEP_0_1 COMPLETION_SUMMARY (~800 lines, ~8K tokens, 8min)
   Why: User Dashboard is related (both use shared UI components)

9. STEP_0_2 START_HERE.md (if exists - ~1,200 lines, ~12K tokens, 10min)
   Why: Payment System is related (Notification Service sends payment confirmations)

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

#### STEP_0_3: Build Notification Service
**Target:** Email and in-app notifications for key user events
**Timeline:** 2 weeks
**Focus:** Reliable delivery with user preferences

Let's make this more specific. I'll ask questions to refine.

---

Q1: What exactly is "Notification Service"?

Based on research:
- Payment System (STEP_0_2) triggers events (payment success/failure)
- Notification Service sends emails and in-app notifications for these events
- "Service" means: Event handlers, template system, delivery infrastructure

Should substep be:
A) "Build notification templates + email delivery system"
B) "Build event-driven notification system with user preferences"
C) "Build notification service (email + in-app) + delivery tracking"

[Human chooses or refines]

---

Q2: What are the specific deliverables?

Current says: "Email and in-app notifications for key user events"

More specific would be:
"Deliverables:
1. Event handler system (listens to payment events, user actions, system events)
2. Notification template engine (email templates + in-app notification formats)
3. Delivery infrastructure (email provider integration + in-app notification storage)
4. User preference management (opt-in/opt-out, notification frequency settings)
5. Validation: Notifications sent within 30s, delivery tracked, user preferences respected"

Is this correct? What would you add/change?

[Human refines]

---

Q3: What are the success criteria?

Current: Generic

More specific:
"Success criteria:
- Event handling: Listens to all payment events, user events, system events
- Template system: 5-8 notification templates (payment success, payment failure, welcome, password reset, etc.)
- Delivery reliability: 99%+ delivery rate, <30 second latency
- User preferences: Users can opt-in/opt-out per notification type
- Monitoring: Track delivery success/failure, bounce rates, open rates (email)
- Integration: Works with both email provider (e.g., SendGrid) and in-app notification system"

Does this capture requirements? Anything missing?

[Human confirms or adds]

---

Q4: How should this be broken into substeps?

Current: One substep (STEP_0_3)

Could be split:
- STEP_0_3_1: Build event handler system + notification templates
- STEP_0_3_2: Build delivery infrastructure (email + in-app)
- STEP_0_3_3: Build user preference management + monitoring

Or stay as one:
- STEP_0_3: All in one (event handlers + templates + delivery + preferences)

Given 2 week estimate, is one substep manageable or should we split?

[Human decides]

---

Q5: What risks should we call out?

From STEP_0_1, STEP_0_2 learnings:
- Email deliverability complexity (could over-engineer - start simple)
- Third-party provider dependency (SendGrid, Mailgun, etc. may have downtime)
- Template scope creep (limit to 5-8 core notification types)

Should document:
"Risks:
- Over-engineering delivery infrastructure (mitigation: start with one provider, add redundancy later)
- Provider downtime affecting user experience (mitigation: implement retry queue, monitor delivery)
- Scope creep on notification types (mitigation: hard cap at 8 types, defer extras to STEP_3)"

Anything else?

[Human adds risks]
```

**Usher helps structure thinking, not just transcribe.**

---

### Step 5: Update ATLAS_STEPS_PARTX.md

**Usher drafts update:**

```markdown
#### STEP_0_3: Build Notification Service

**Status:** ⏸️ PLANNED
**Timeline:** 2 weeks (estimated)
**Focus:** Reliable event-driven notifications (email + in-app + user preferences)

**Objective:**
Build the Notification Service: event handler system (listens to payment/user/system events), notification template engine, delivery infrastructure (email + in-app), and user preference management.

**Deliverables:**
1. **Event Handler System**
   - Listens to: Payment events, user signup/login, password resets, system alerts
   - Event queue with retry logic (handle failures gracefully)
   - Extensible (easy to add new event types)

2. **Notification Template Engine** (5-8 core templates)
   - Email templates: Payment success, payment failure, welcome, password reset, invoice ready
   - In-app notification formats: Toast, banner, inbox message
   - Template variables: User name, transaction details, action links

3. **Delivery Infrastructure**
   - Email: Integration with provider (e.g., SendGrid, Mailgun)
   - In-app: Real-time notification storage + delivery via WebSocket or polling
   - Delivery tracking: Success/failure, bounce handling, retry queue

4. **User Preference Management**
   - Opt-in/opt-out per notification type (email, in-app, both)
   - Notification frequency settings (immediate, daily digest, weekly)
   - User-facing preferences UI (settings page)
   - Respects preferences in delivery logic

**Success Criteria:**
- [ ] Event handlers work for all event types (payment, user, system)
- [ ] 5-8 notification templates built and tested (email + in-app)
- [ ] Email delivery: 99%+ delivery rate, <30s latency
- [ ] In-app delivery: Real-time or <10s polling latency
- [ ] User preferences: Opt-in/opt-out works, settings persist
- [ ] Monitoring: Track delivery success/failure, bounce rates, retry queue depth

**Could split into sub-substeps if needed:**
- STEP_0_3_1: Event handlers + notification templates
- STEP_0_3_2: Delivery infrastructure (email + in-app)
- STEP_0_3_3: User preferences + monitoring

**Decision:** Keep as one substep (2 weeks manageable, logical unit)

**Risks:**
- Over-engineering delivery infrastructure (mitigation: start with one provider, add redundancy later)
- Provider downtime affecting user experience (mitigation: retry queue, monitor delivery rates)
- Scope creep on notification types (mitigation: hard cap 8 types, defer extras to STEP_3)

**Dependencies:**
- Requires: STEP_0_2 complete (Payment System triggers payment events)
- Enables: STEP_1_X (beta users receive notifications)

**Hypotheses:**
- H1: Event-driven architecture handles all notification types (test in CP validation)
- H2: Single email provider is reliable enough (vs multi-provider redundancy)

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
## 2025-12-11: Refined STEP_0_3 Definition (Notification Service)

**Context:** STEP_0_3 was vague ("Build notification service"). Before AI1 starts research, refined with human to make very specific.

**Changes made:**
- Added specific deliverables (4 distinct outputs: event handlers, templates, delivery infrastructure, user preferences)
- Added measurable success criteria (99%+ delivery rate, <30s latency, user preference support)
- Added risks (over-engineering, provider downtime, scope creep) with mitigations
- Clarified dependencies (needs STEP_0_2 Payment System event triggers)

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
