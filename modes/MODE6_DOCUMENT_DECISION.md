# Mode 6: Document Decision - Format Strategic Choices

**Purpose:** Help capture strategic decisions with proper structure
**Usage:** As needed (when strategic choice is made)
**Trigger:** Human says "Document decision: [topic]" or "Add to decision log"

---

## What This Mode Does

**Reduces friction on decision documentation:**

**Current pain:**
- Human makes strategic decision (tech stack, market focus, pricing change)
- Should document in DECISION_LOG.md (alternatives, rationale, trade-offs)
- Often skipped (execution pressure, documentation feels like overhead)
- Later: "Why did we choose X?" - no record, must guess

**With Mode 6:**
- Human states decision made
- Usher interviews (what alternatives? why chosen? trade-offs?)
- Usher drafts DECISION_LOG entry (proper format)
- Human reviews/approves (5 minutes vs 20)
- Usher adds to DECISION_LOG.md

**Ensures:**
- Decisions are captured (audit trail)
- Rationale is documented (don't re-litigate later)
- Trade-offs are explicit (honest about what we're giving up)

---

## Files Usher Loads

```
1. DECISION_LOG.md (to append to)
   Lines: Current state (~1,000-3,000)
   Tokens: ~15K
   Time: 5 min (skim recent to check for duplicates)

2. DECISION_LOG template (format reference)
   From: strategy/DECISION_LOG.md (template section)
   Tokens: ~2K
   Time: 2 min

3. Context for decision (ask human to provide)
   Examples:
   - If tech decision: Which Effort is this for? What's the context?
   - If market decision: What learnings prompted this?
   - If pricing decision: What data supports this?

   Variable context based on decision type

Total: ~1,000-2,000 lines, ~17-25K tokens, ~10-15 min
```

---

## Workflow: Interview & Document

### Step 1: Understand the Decision

**Usher asks:**
```
What decision was made?

Example responses:
- "We're switching from WordPress to Next.js for all customer sites"
- "We're focusing on contractors only (not law firms yet)"
- "We're pricing at $3,500 (not $5,000)"
- "We're using Supabase (not Firebase)"

[Human provides decision statement]
```

---

### Step 2: Gather Context

**Usher probes:**
```
Q: What situation prompted this decision?

Example: "We were planning STEP_1_1 and had to choose tech stack"
OR: "After STEP_0_1 completion, we learned WordPress is too slow"

Q: When was this decided?

[Date - for chronological tracking]

Q: Who was involved in this decision?

[Solo founder, team discussion, advisor input, etc.]
```

---

### Step 3: Identify Alternatives

**Usher asks:**
```
What alternatives did you consider? (At least 2, ideally 3-4)

For each alternative:

Option A: [Name]
- Description: What is this approach?
- Pros: Why might you choose this?
- Cons: Why might you not?
- Feasibility: Can you actually do this?
- Cost: What would it cost? (time, money, opportunity)

[Human provides for each alternative]
```

**Usher helps structure:**
- If human says "We could use Firebase"
- Usher prompts: "Pros of Firebase? Cons? Feasibility? Cost?"
- Ensures all dimensions covered

---

### Step 4: Extract Rationale

**Usher asks:**
```
Why did you choose [selected option] over alternatives?

Specific reasons:
- Reason 1: [Technical, strategic, cost, time, team capability]
- Reason 2: [...]
- Reason 3: [...]

What was the deciding factor?

[Human explains - Usher captures]
```

---

### Step 5: Clarify Trade-Offs

**Critical question:**
```
What are you giving up by not choosing [Alternative B or C]?

Example:
- Chose Next.js over WordPress
- Trade-off: Customer can't self-edit (WordPress has WYSIWYG editor)
- Why acceptable: Customers explicitly want hands-off (we handle updates for them)

What trade-offs are you accepting?

[Human explains - Usher ensures honesty]
```

---

### Step 6: Define Validation Plan

**Usher asks:**
```
How will you know if this was the right decision?

What metrics, signals, or outcomes will validate this choice?

Example:
- If Next.js choice is right: Sites consistently hit <2s mobile (validated by customer 5)
- If pricing at $3,500 is right: Close 10 customers at this price (validated by Month 6)

Timeline: When will you know?

[Human provides validation plan]
```

---

### Step 7: Assess Reversibility

**Usher asks:**
```
How hard is this decision to undo?

Reversibility levels:
- Easy (can change in 1 day with minimal cost)
- Medium (would take 1-2 weeks to pivot, some sunk cost)
- Hard (months to change, significant sunk cost or customer impact)

What would trigger reconsidering this decision?

Example: "If sites don't hit <2s mobile after 5 customers, reconsider Next.js"

[Human assesses]
```

---

### Step 8: Draft DECISION_LOG Entry

**Usher creates structured entry:**

```markdown
## 2025-12-20: Choose Next.js Over WordPress for All Customer Sites

**Context:**
Planning STEP_1_1 (first customer site). Need to choose tech stack for all future customer deliveries. This decision affects 10-50 customer sites (entire vertical delivery).

**Decision:**
Use Next.js 15 + Vercel for all customer sites (no WordPress, no site builders).

**Alternatives Considered:**

**Option A: WordPress + Premium Theme**
- **Pros:**
  - Customers can self-edit (WYSIWYG editor, no developer needed)
  - Huge plugin ecosystem (any feature imaginable)
  - Familiar to many customers
  - Cheaper hosting ($10/mo)
- **Cons:**
  - Slow (even optimized WP sites: 3-4s mobile load)
  - Security issues (constant updates, vulnerabilities)
  - Plugin conflicts (maintenance nightmare)
  - Not differentiated (competitors all use WordPress)

**Option B: Next.js + Vercel** (CHOSEN)
- **Pros:**
  - Fast by default (<2s mobile achievable easily)
  - Modern stack (React, TypeScript, AI-friendly)
  - No security updates (static generation)
  - Vercel hosting ($20/mo with zero-config)
  - Differentiation (few agencies use modern stack)
  - Scales to platform (component library reusable across customers)
- **Cons:**
  - Customers can't self-edit (must go through us for changes)
  - Smaller talent pool (fewer Next.js devs than WordPress devs)
  - Steeper learning curve (if we hire)

**Option C: Webflow**
- **Pros:**
  - Visual editor (customer can edit)
  - Fast sites (better than WordPress)
  - Designer-friendly
- **Cons:**
  - Vendor lock-in ($29/mo per site)
  - Less flexibility (can't customize deeply)
  - Not code-based (can't version control easily)

**Rationale:**
Chose Next.js (Option B) because:
1. **Performance is our #1 differentiator** (from your company_CONTEXT: "10× the speed"). WordPress can't hit <2s mobile. Next.js can.
2. **Customers explicitly want hands-off** (learned in customer research: "I don't want to learn tech, I want you to handle it"). No-edit is a feature, not a bug.
3. **Platform trajectory** (internal tools + customer sites share component library → SaaS products emerge). WordPress doesn't enable this.
4. **AI-assisted development** (Next.js + Cursor/Claude Code = 3x faster than WordPress customization)

**Trade-Offs Accepted:**
- **No self-edit for customers** → Creates dependency on us (acceptable - this creates recurring revenue through update packages)
- **Smaller talent pool** → Harder to hire (acceptable - AI assistance reduces need for developers)
- **Higher learning curve** → If we hire non-React dev (acceptable - upfront investment pays off long-term)

**Evidence/Input:**
- Customer research: 8 of 10 prospects said "I want hands-off, not DIY"
- Performance testing: Next.js test site 1.4s mobile vs WordPress test site 3.8s (even optimized WP)
- Strategic alignment: your company_CONTEXT.md emphasizes "ongoing operations" (requires control, not customer-editable)

**Validation Plan:**
- **Metric:** 100% of customer sites hit <2s mobile load
- **Timeline:** Validate by customer #5 (Month 3)
- **Signal:** If sites consistently hit <2s and customers don't request self-edit → decision validated
- **Failure signal:** If performance issues arise or 3+ customers request self-edit → reconsider

**Reversibility:** Medium
- Can pivot to WordPress after 5 customers (would need to rebuild, ~4 weeks)
- Can add Webflow option as alternative tier (keep Next.js as premium)
- After 15 customers: Very hard (too much invested in Next.js patterns)

**Affected Steps:**
- STEP_1_X (all customer delivery uses Next.js)
- STEP_0_3 (Rebuild Engine built for Next.js output)
- STEP_5+ (SaaS products built on shared component library)

**Decision Makers:** Ryan (solo founder, informed by customer research and performance testing)

---
```

**Usher asks: "Review this entry. Approve? (yes/no/edit)"**

---

### Step 9: Human Approves & Usher Adds to Log

**If approved:**
```bash
# Append to DECISION_LOG.md
cat >> /ATLAS3/strategy/DECISION_LOG.md << 'EOF'

## 2025-12-20: Choose Next.js Over WordPress...

[Complete entry as drafted]

EOF

# Commit
git add strategy/DECISION_LOG.md
git commit -m "Decision: Next.js for all customer sites (vs WordPress)"
git push
```

**Usher reports:**
```
Decision documented in DECISION_LOG.md.

Entry: "Choose Next.js Over WordPress for All Customer Sites"
Date: 2025-12-20
Affects: STEP_1_X (all customer delivery)

Future teams can reference this decision (no re-litigation).

DECISION_LOG now has 16 entries (strategic choices documented).
```

---

## Interview Template (Usher's Questions)

**For any decision, ask:**
1. What was decided?
2. What prompted this? (context)
3. What alternatives? (at least 2-3)
4. Pros/cons of each? (structured comparison)
5. Why chosen? (specific rationale)
6. What trade-offs? (what's given up, why acceptable)
7. How to validate? (metrics, timeline)
8. How reversible? (easy/medium/hard to change)
9. Who decided? (solo, team, advisor input)
10. What's affected? (which Steps/Efforts impacted)

**Structured interview ensures complete entry.**

---

## When to Use Mode 6

**Use when:**
- Made strategic choice (tech stack, market, pricing, approach)
- Eliminated alternative (decided NOT to do something)
- Changed direction (pivot from original plan)
- Trade-off made (accepted downside for upside)

**Don't use for:**
- Tactical implementation details (those go in CP implementation notes)
- Obvious choices (no real alternatives)
- Easily reversible decisions (low stakes)

**Frequency:** 1-3 times per month (strategic decisions are infrequent)

---

## Value

**Why document decisions:**
- Don't re-litigate (6 months later: "Why WordPress?" → Check log: "Already decided, here's why")
- Learn from outcomes (was decision right? check validation plan)
- Audit trail (investors, teammates, future self understand choices)
- Faster future decisions (see patterns in past decisions)

**Mode 6 makes it easy** (10 minutes vs 30, structured vs ad-hoc)

---

**Use this mode when making strategic choices. Future you will thank you.**
