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
- "We're using Stripe for payment processing (not PayPal or Square)"
- "We're focusing on B2B SaaS market (not B2C yet)"
- "We're pricing at $49/month (not $99/month)"
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
## 2025-12-20: Choose Stripe Over PayPal for Payment Processing

**Context:**
Planning STEP_0_2 (payment system). Need to choose payment provider for all future payment processing. This decision affects all subscription billing, one-time payments, and future financial integrations.

**Decision:**
Use Stripe API for all payment processing (not PayPal, not Square, not building custom processor).

**Alternatives Considered:**

**Option A: PayPal**
- **Pros:**
  - Brand recognition (users trust PayPal)
  - Global reach (202 countries, 25 currencies)
  - Buyer protection (users feel safe)
  - Lower ACH fees (0.8% vs Stripe's 0.8%)
- **Cons:**
  - Poor developer experience (clunky API, outdated docs)
  - Webhook reliability issues (delayed events, missed webhooks)
  - Account holds (PayPal freezes funds unpredictably)
  - Not developer-first (designed for eBay sellers, not SaaS)

**Option B: Stripe** (CHOSEN)
- **Pros:**
  - Best-in-class developer experience (excellent docs, SDKs, webhooks)
  - Reliable webhooks (real-time, retry logic, signature verification)
  - Subscription support (built-in recurring billing, plan changes, proration)
  - Modern API (RESTful, predictable, well-documented)
  - Strong ecosystem (integrations, tools, community)
  - Fast settlement (2-day for US, vs PayPal's 3-5 days)
- **Cons:**
  - 2.9% + 30¢ per transaction (vs PayPal 2.9% + 30¢ - same)
  - Less brand recognition than PayPal (users less familiar)
  - Requires custom UI (no hosted checkout in basic tier)

**Option C: Square**
- **Pros:**
  - Good for in-person + online (unified system)
  - Flat-rate pricing (2.9% + 30¢, simple)
  - Free hardware (card readers)
- **Cons:**
  - In-person focus (not optimized for pure SaaS)
  - Weaker subscription support (basic recurring billing)
  - Less international support (primarily US/Canada/UK)

**Rationale:**
Chose Stripe (Option B) because:
1. **Developer experience is critical** (from COMPANY_CONTEXT: "build fast, iterate quickly"). Stripe's API is 10x easier to integrate than PayPal's. Saves 2-3 days of development time.
2. **Subscription support is core requirement** (learned in market research: 80% of target users prefer monthly billing). Stripe has native recurring billing, plan changes, proration. PayPal's subscription support is basic.
3. **Webhook reliability is non-negotiable** (payment success/failure events must be real-time). Stripe webhooks are rock-solid with retry logic. PayPal webhooks have known reliability issues.
4. **Future platform trajectory** (payment system → invoicing → billing analytics → full financial platform). Stripe's ecosystem enables this. PayPal is more limited.

**Trade-Offs Accepted:**
- **Less brand recognition than PayPal** → Some users may not trust Stripe (acceptable - our target market is tech-savvy, they know Stripe)
- **Custom UI required** → Must build checkout flow ourselves (acceptable - gives us full control over user experience)
- **Same transaction fees as PayPal** → Not saving money (acceptable - developer time savings offset this)

**Evidence/Input:**
- User research: 15 of 20 target users prefer subscription billing over one-time payment
- Developer experience testing: Stripe integration took 2 days, PayPal integration took 5 days (in prototype)
- Strategic alignment: COMPANY_CONTEXT.md emphasizes "developer velocity" (Stripe's API enables fast iteration)

**Validation Plan:**
- **Metric:** 99%+ webhook success rate, <2 day integration time for future payment features
- **Timeline:** Validate by 100 paid transactions (Month 2)
- **Signal:** If webhook reliability is solid and no integration blockers → decision validated
- **Failure signal:** If webhook issues arise or integration takes >5 days for new features → reconsider

**Reversibility:** Medium
- Can switch to PayPal after 100 transactions (would need to rebuild payment flow, ~2 weeks)
- Can add PayPal as secondary option (offer both Stripe and PayPal)
- After 10,000 transactions: Very hard (too much data in Stripe, migration complex)

**Affected Steps:**
- STEP_0_2 (payment system uses Stripe)
- STEP_0_3 (notification service sends payment receipts via Stripe events)
- STEP_1_X (user dashboard shows Stripe transaction data)
- STEP_3+ (subscription management features built on Stripe API)

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

Entry: "Choose Stripe Over PayPal for Payment Processing"
Date: 2025-12-20
Affects: STEP_0_2, STEP_0_3, STEP_1_X (payment system and dependent features)

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
