# Start Here - [Substep Name]

**Substep:** STEP_X_Y from ATLAS_STEPS.md
**Researched by:** AI1
**Date:** [YYYY-MM-DD]
**Research Duration:** [X hours]

---

## Instructions for AI1

This template defines the structure for START_HERE.md (AI1's primary deliverable).

**Fill all sections completely.** This document enables AI2 to create perfect guides.

**Typical length:** 800-1,500 lines (comprehensive, not summary)

---

## Context

**What this substep builds:**
[2-3 paragraphs:]
- What is the deliverable? (product, feature, tool, system)
- Who is it for? (customers, internal team, end users)
- Why does it matter? (strategic importance, business impact)
- How does it advance company goals? (ties to Step, ties to vision)

**Specificity level of substep definition:**
[How specific was the substep in ATLAS_STEPS.md?]

- **Vague:** Substep just said "Build [thing]" - required heavy research to define what/how
- **Medium:** Substep had some specifics (tech stack, key features) - required validation and pattern research
- **Specific:** Substep was very detailed (exact features, exact tech) - required mostly validation and gotcha-finding

[This helps AI2 understand how much was defined vs discovered]

**Previous substep context:**
[If STEP_X_{Y-1} exists:]
- What did previous substep build? (summary from COMPLETION_SUMMARY)
- What infrastructure exists? (can we reuse Vercel project, database, etc.)
- What patterns were discovered? (what worked well, what to copy)
- What should we avoid? (what didn't work)

[If first substep (X.1):]
- No previous context. Starting fresh for this Step.

---

## Research Findings

### Competitive Analysis (if applicable)

**Researched:** [X] competitors/alternatives in this space

**Competitor 1: [Name/Product]**
- **What it does:** [Description]
- **Strengths:** [2-3 things they do well]
- **Weaknesses:** [2-3 gaps or issues]
- **Tech approach:** [Stack if visible]
- **Learnings:** [What we can learn/copy]
- **Differentiation:** [How we'll be different/better]

**Competitor 2: [Name]**
[Same structure]

[Continue for 5-10 competitors]

**Patterns identified:**
- [Pattern 1: What's common across all competitors]
- [Pattern 2: Industry standard approach]
- [Pattern 3: What everyone does (we should too)]

**Gaps found:**
- [Gap 1: What nobody does well (our opportunity)]
- [Gap 2: Underserved segment or feature]

**Competitive positioning:**
[How this substep's deliverable compares to/improves on competition]

---

### Technical Options Analysis

**Evaluated:** [X] approaches for building this

**Option 1: [Approach Name]**

**Description:**
[How this approach works - 2-3 sentences]

**Tech stack:**
[Specific technologies: Framework, database, hosting, services]

**Pros:**
- [Advantage 1 with reasoning]
- [Advantage 2]
- [Advantage 3]
- [Advantage 4]

**Cons:**
- [Disadvantage 1 with reasoning]
- [Disadvantage 2]
- [Disadvantage 3]

**Feasibility:**
- **Technical:** HIGH / MEDIUM / LOW [Can we build this?]
- **Team:** HIGH / MEDIUM / LOW [Do we have skills?]
- **Time:** HIGH / MEDIUM / LOW [Can we deliver in timeline?]
- **Cost:** HIGH / MEDIUM / LOW [Can we afford ongoing costs?]

**Time to implement:**
[Estimate: X days/weeks]

**Ongoing costs:**
[Monthly costs: Services, APIs, hosting]

**Examples found:**
- [Link to repo, case study, documentation showing this approach]
- [Link to example 2]

**Risks:**
- [Risk 1: What could go wrong with this approach]
- [Risk 2]

---

**Option 2: [Approach Name]**
[Same complete structure]

**Option 3: [Approach Name]**
[Same complete structure]

**Comparison Matrix:**

| Criteria | Option 1 | Option 2 | Option 3 |
|----------|----------|----------|----------|
| **Performance** | <2s load | 3-4s load | 2s load |
| **Cost (Year 1)** | $500 | $0 | $2,400 |
| **Time to Build** | 2 weeks | 4 weeks | 1 week |
| **Maintainability** | High | Medium | High |
| **Scalability** | High | Low | High |
| **Team Familiarity** | High | Low | Medium |
| **Feasibility** | HIGH | MEDIUM | HIGH |

**Recommendation: Option [X]**

**Rationale:**
[3-5 sentences explaining why this option is best given constraints]

**Specific reasons:**
1. [Reason 1 - tied to constraint or company goal]
2. [Reason 2 - comparative advantage over alternatives]
3. [Reason 3 - validated through example or test]

**Trade-offs accepted:**
[What we're giving up by not choosing Option Y]
[Why this trade-off is acceptable given context]

**Validation completed:**
[How approach was validated - tested? example found? expert confirmed?]

---

### Design/UX Patterns (if applicable)

**Researched:** [X] design patterns for this domain

**Pattern 1: [Pattern Name]**
- **What:** [Description of pattern]
- **Where used:** [Examples of sites using this]
- **Why it works:** [Reasoning]
- **How to implement:** [High-level approach]
- **References:** [Links to examples, documentation]

**Pattern 2:** [Same structure]

**Recommendations for this substep:**
- [Pattern X is best for this use case because...]
- [Avoid pattern Y because...]

**Content strategy:**
[If applicable: What content is needed, tone/voice, structure]

**Accessibility considerations:**
[WCAG requirements, specific to this domain]

---

### Integration Requirements (if applicable)

**External services/APIs needed:**

**Service 1: [Name]**
- **Purpose:** [What we use it for]
- **API documentation:** [Link]
- **Authentication:** [How to auth - API key, OAuth, etc.]
- **Rate limits:** [X requests per day/hour]
- **Cost:** [Free tier limits, paid tier pricing]
- **SDKs available:** [JavaScript library, REST API, etc.]
- **Gotchas:** [Common issues, things that go wrong]
- **Examples:** [Link to integration examples]

**Service 2:** [Same structure]

**Internal integrations:**
[If this substep connects to previous substeps' deliverables]
- Connects to: [STEP_X_{Y-1} output]
- Integration point: [How they connect]
- Data flow: [What data passes between]

---

### Risk Assessment

**Major risks for this substep:**

**Risk 1: [Risk Title]**
- **Description:** [What could go wrong]
- **Probability:** HIGH / MEDIUM / LOW
- **Impact:** HIGH / MEDIUM / LOW [If it happens, how bad?]
- **Mitigation:** [How to prevent or handle]
- **Contingency:** [Plan B if it occurs]
- **Owner:** [AI2 plans for it, AI3 executes mitigation, or Human decides]

**Risk 2:** [Same structure]

**Risk 3:** [Same structure]

[Document 5-10 major risks]

**Risk matrix:**

| Risk | Probability | Impact | Mitigation Owner |
|------|-------------|--------|------------------|
| [Risk 1] | HIGH | MEDIUM | AI3 (code defensively) |
| [Risk 2] | MEDIUM | HIGH | AI2 (plan alternatives) |
| [Risk 3] | LOW | LOW | Accept (monitor only) |

---

## Implementation Outcomes (VERY SPECIFIC)

**Critical:** These must be MORE specific than substep definition.

**Substep definition said:**
[Quote from ATLAS_STEPS.md - what the substep objective was]

**After research, implementation outcomes are:**

### Outcome 1: [Specific Deliverable]

**What exactly:**
[Detailed description - not vague]

**Features:**
- [Feature 1 with specifics]
- [Feature 2 with specifics]
- [Feature 3]

**Quality targets:**
- Performance: [<2s mobile load, Lighthouse 90+, etc.]
- Accessibility: [WCAG AA, zero critical errors]
- Security: [No vulnerabilities, input validated, etc.]
- Reliability: [Uptime target, error rate target]

**Technical specs:**
- Tech stack: [Exact technologies - Next.js 15, React 19, etc.]
- Architecture: [How it's structured - monorepo, microservices, etc.]
- Deployment: [Where deployed, how deployed]
- Database: [If applicable - what tables, what schema]

**Integration:**
- Connects to: [What other systems]
- APIs used: [External APIs with specifics]
- Data flow: [What data in, what data out]

### Outcome 2: [Specific Deliverable]
[Same complete structure]

### Outcome 3: [If applicable]

**Example of good specificity:**

NOT: "Build audit tool"

BUT: "Multi-tenant website audit tool with:
- **Input:** Any website URL (validates format: http/https, checks reachability)
- **Analysis:** 5 metrics scored 0-100 each
  - Performance: PageSpeed Insights API (mobile + desktop)
  - SEO: Meta tags, structured data, sitemap presence
  - Mobile: Viewport config, touch targets, responsive design
  - Accessibility: WCAG automated scan (color contrast, alt text, labels)
  - Webhooks: Real-time event processing for payment success/failure, subscription updates
- **Payments:** One-time charges (credit/debit cards, ACH, Apple Pay, Google Pay)
- **Subscriptions:** Monthly/annual billing with plan changes, proration, cancellations
- **Security:** PCI DSS compliant, webhook signature verification, encrypted transaction data
- **Diverse scenarios:** Tested with US cards, international cards, 3D Secure, declines, refunds
- **Performance:** <500ms payment processing, <1s webhook handling (async background jobs)
- **Architecture:** Next.js 15 + Stripe API + Supabase multi-tenant (RLS for transaction isolation)
- **Deployment:** app.yourdomain.com/checkout
- **Transaction history:** User dashboard with all payments, subscriptions, invoices
- **Monitoring:** Stripe dashboard, Vercel analytics, error tracking, webhook success rates
- **Cost target:** <$200/mo at 100 audits/day"

---

## Rough Checkpoint Breakdown (AI2 will refine)

**Estimated [X] checkpoints for this Effort:**

### CP0: Infrastructure Setup (Always first)

**Estimated duration:** [2-6 hours]

**Goal:** Prepare technical foundation

**Tasks:**
- [Task 1: Git initialization if needed]
- [Task 2: Vercel project creation or reuse]
- [Task 3: Database setup (new project or add tables to existing)]
- [Task 4: Environment configuration]
- [Task 5: Initial file structure]
- [Task 6: Dependency installation]
- [Task 7: Validate deployment works]

**Output:**
- Infrastructure operational
- Can build features in CP1+

---

### CP1: [Implementation Phase 1 Name]

**Estimated duration:** [X days]

**Goal:** [What this phase accomplishes]

**Tasks:**
[High-level tasks - AI2 will make detailed]

**Output:**
[What exists after this CP]

---

### CP2: [Implementation Phase 2 Name]

[Same structure]

---

### CPX: Testing & Deployment (Always last)

**Estimated duration:** [1-2 days]

**Goal:** Comprehensive validation and production launch

**Tasks:**
- Full E2E testing
- Performance validation
- Accessibility audit
- Cross-vertical testing (if applicable)
- Security scan
- Staging deployment and validation
- Production deployment (PR creation)
- Post-launch monitoring

**Output:**
- Production deployment
- All quality gates passed

---

**Rationale for [X] checkpoints:**

**Why [X] and not fewer?**
[Reasoning for splitting work this way]

**Why [X] and not more?**
[Reasoning for not over-splitting]

**Could adjust:**
[Under what conditions would different CP count make sense?]

**AI2's discretion:**
[What AI2 should consider when finalizing CP structure]

---

## For AI2 (What to research when creating guides)

**General guidance:**

**Reuse from previous Efforts:**
[If similar Effort exists, point AI2 to specific files to reference]
- Example: "Check STEP_1_1_AUDIT_ENGINE for Supabase setup patterns (lib/supabase/client.ts)"

**Company patterns to apply:**
[Standard tech stack, quality standards, deployment procedures]
- Example: "All tools use Next.js 15 + Supabase + Vercel (company standard)"

**Avoid based on learnings:**
[Known issues from past Efforts]
- Example: "Don't over-design database schema upfront (caused delays in STEP_1_1)"

---

**Creating CP0_GUIDE (Setup):**

**AI2 should research:**
1. [Specific topic 1 for setup]
   - Where to look: [Docs URL, example repo, previous Effort]
   - What to find: [Setup patterns, configuration examples]
2. [Specific topic 2]
3. [Specific topic 3]

**Include in CP0_GUIDE:**
- Exact commands (not "set up Vercel" but "vercel init, select team: your company, name: [exact], etc.")
- Exact configuration (database schema with column types, indexes)
- Exact validation (how to test setup worked - specific commands)

**Watch out for:**
- [Gotcha 1 specific to setup]
- [Gotcha 2]

---

**Creating CP1_GUIDE ([Implementation phase]):**

**AI2 should research:**
1. [Technical pattern for this phase]
   - Examples: [Where to find implementation examples]
   - Best practices: [Documentation sections to read]
2. [Integration approach]
   - API documentation: [Specific sections]
   - Code examples: [Repos, tutorials]

**Include in CP1_GUIDE:**
- Code examples (TypeScript snippets showing exact patterns)
- API integration steps (with error handling, rate limiting)
- Testing approach (how to validate this phase works)

**Watch out for:**
- [Gotcha 1 for this implementation]
- [Gotcha 2]

---

**Creating CP2_GUIDE ([Next phase]):**
[Same structure - what AI2 should research, what to include, gotchas]

---

**Creating CPX_GUIDE (Testing & Deployment):**

**AI2 should research:**
1. Testing strategy for this type of deliverable
   - What to test: [Specific test categories]
   - How to test: [Tools, procedures]
2. Deployment approach
   - Where: [Production URL, domain config]
   - How: [Deployment steps, validation]

**Include in CPX_GUIDE:**
- Comprehensive test checklist (E2E, performance, accessibility, security, cross-vertical if applicable)
- Deployment steps (merge to staging, create PR, human approval, merge to main)
- Post-launch monitoring (what to check, for how long)
- COMPLETION_SUMMARY creation (required)
- ATLAS_STEPS.md update (required)

**Watch out for:**
- [Gotcha 1 for testing/deployment]
- [Gotcha 2]

---

**Testing strategy guidance:**

**After each CP (incremental):**
- Build validation (npm run build must succeed)
- Unit tests (test new functions)
- Manual testing (feature works)

**Final CP (comprehensive):**
- [Specific testing requirements for this substep]
- [Cross-vertical if multi-vertical tool]
- [Performance if user-facing]
- [Accessibility if user-facing]
- [Security always]

---

**Quality standards (remind AI2 to enforce):**

**Performance:**
- [Specific targets for this substep]
- Example: <2s mobile load, Lighthouse 90+, <90s API response

**Accessibility:**
- WCAG AA minimum (zero critical errors)
- All images have alt text
- Forms have labels
- Keyboard navigation works

**Security:**
- No hardcoded secrets
- Input validation on all user input
- SQL injection prevention (parameterized queries)
- XSS prevention (sanitize output)

**Code quality:**
- TypeScript strict mode
- ESLint clean (zero errors)
- No console.log in production
- Proper error handling (all async wrapped)

---

## Next Steps for AI2

**When you (AI2) read this START_HERE:**

1. **Validate research (30-60 min)**
   - Spot-check findings (are claims accurate?)
   - Confirm recommendations (do they make sense?)
   - Identify gaps (what did AI1 miss?)

2. **Create OUTLINE (1 hour)**
   - Decide final CP count (AI1 estimated [X], you decide actual)
   - CP0: Always setup
   - CP1-CPX-1: Implementation (you decide split)
   - CPX: Always testing/deploy
   - Document rationale

3. **Research and create each CP guide (2-4 hours per CP)**
   - Follow "For AI2" sections above
   - Deep research per CP
   - Create detailed guide with examples

4. **Create support docs**
   - OVERVIEW_GUIDE.md (quick-start)
   - TODO_TRACKER.md (progress tracking)
   - effort.md (overview)

5. **Report complete**
   - All guides ready
   - AI3 can execute

---

**This START_HERE enables AI2 to plan with confidence. Be comprehensive.**
