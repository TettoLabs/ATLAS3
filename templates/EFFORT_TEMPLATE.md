# Effort: STEP_X_Y_[SHORTNAME]

**Substep:** STEP_X_Y from ATLAS_STEPS.md
**Status:** PLANNED / AI1_RESEARCH / AI2_PLANNING / IN_PROGRESS / COMPLETE
**Created by:** AI2
**Created:** [YYYY-MM-DD]
**Owner:** AI3 (execution)
**Timeline:** [Start date] to [Est. end date]
**Duration estimate:** [X] days ([Y] checkpoints)

---

## Instructions for AI2

This template defines effort.md (high-level Effort overview).

**Create this** during AI2 planning phase (after OUTLINE, guides, OVERVIEW_GUIDE, TODO_TRACKER).

**Purpose:** Quick reference for goals, success criteria, strategic context.

**Length:** 200-400 lines (concise, links to detailed docs)

---

## Overview

[2-3 paragraphs:]

**What this Effort builds:**
[Clear description of deliverable]

**Who this serves:**
[End users, internal team, customers, etc.]

**Why this matters strategically:**
[How this advances Step goal, how it advances company vision]

**How this fits in company roadmap:**
[Context: Previous substeps built X, this builds Y, next substeps will build Z]

---

## Goals

**Primary goal:**
[The ONE thing this Effort must accomplish - non-negotiable]

**Secondary goals:**
- [Supporting goal 1 - important but not critical]
- [Supporting goal 2]
- [Supporting goal 3]

**Stretch goals (if time permits):**
- [Optional enhancement 1]
- [Optional enhancement 2]

---

## Success Criteria

**This Effort is complete when:**

**Functional:**
- [ ] [Specific functional requirement 1]
- [ ] [Specific functional requirement 2]
- [ ] [All core features implemented and working]

**Technical:**
- [ ] Performance: [Specific target - <2s mobile, Lighthouse 90+, etc.]
- [ ] Accessibility: [WCAG AA, zero critical errors]
- [ ] Security: [No vulnerabilities, secrets secured]
- [ ] Multi-vertical: [If applicable - works for contractor, law, healthcare]
- [ ] Reliability: [Uptime target, error rate target]

**Deployment:**
- [ ] Deployed to: [Production URL]
- [ ] Staging validated: [Full manual test passed]
- [ ] PR merged: [staging → main]
- [ ] Monitoring: [Plan in place for post-launch]

**Documentation:**
- [ ] COMPLETION_SUMMARY.md created
- [ ] ATLAS_STEPS.md updated (substep marked complete)
- [ ] TODO_TRACKER complete (all CPs ✅)
- [ ] README up to date (if applicable)

**Quality gates:**
- [ ] All tests passing
- [ ] Code quality standards met
- [ ] Human approval received (PR approved)

**All criteria must be met before declaring Effort complete.**

---

## Approach

**High-level strategy:**
[How we'll accomplish the goals - 2-3 paragraphs]

**Technical approach:**
- **Stack:** [Technologies chosen - Next.js, Supabase, Puppeteer, etc.]
- **Architecture:** [How it's structured - multi-tenant, monorepo, microservices, etc.]
- **Deployment:** [Where and how - Vercel, subdomain, auto-deploy]
- **Rationale:** [Why this approach - from AI1's research and recommendations]

**Key decisions:**

**Decision 1: [Tech/approach decision]**
- **Chose:** [What we're doing]
- **Alternatives:** [What else was considered]
- **Rationale:** [Why this choice]
- **Trade-off:** [What we're giving up]
- **From:** [AI1's research, previous Effort pattern, strategic decision]

**Decision 2:** [Same structure]

[Document 3-5 key decisions that shape implementation]

---

## Checkpoints

**Total:** [X] checkpoints (CP0 through CPX)

**See OUTLINE.md for high-level map.**
**See guides/*.md for detailed instructions.**

**Quick reference:**

### CP0: [Setup] (AI3, [X]h)
- Goal: [One sentence]
- Output: Infrastructure ready

### CP1: [Implementation Phase 1] (AI3, [X]d)
- Goal: [One sentence]
- Output: [What's delivered]

### CP2: [Continue for all CPs]

### CPX: [Testing & Deploy] (AI3, [X]d)
- Goal: Production launch
- Output: Live deployment + handoff docs

**Detailed guides:** /guides/CP0_GUIDE.md through CPX_GUIDE.md

---

## Timeline Estimate

**By checkpoint:**
- CP0: [X] hours
- CP1: [X] days
- CP2: [X] days
- ...
- CPX: [X] days

**Total:** [X] days

**Buffer:** +20% ([Y] days) for unknowns

**Expected completion:** [Date]

**Critical path:**
[Which CPs must stay on schedule? Which have slack?]

---

## Dependencies

**Required before starting this Effort:**
- [Prerequisite 1 - previous substep complete, infrastructure exists, etc.]
- [Prerequisite 2]

**This Effort blocks:**
- [Future substep/Effort that depends on this]

**Can run in parallel with:**
- [Other Efforts that are independent]
- [Or: "None - sequential execution required"]

---

## Risks

**Major risks for this Effort:**

**Risk 1: [Title]**
- **Description:** [What could go wrong]
- **Probability:** HIGH / MEDIUM / LOW
- **Impact:** HIGH / MEDIUM / LOW [If occurs, how bad?]
- **Mitigation:** [How we'll prevent or handle]
- **Mitigated in:** [Which CP addresses this]
- **Owner:** AI3 (executes mitigation) or Human (decides if occurs)

**Risk 2:** [Same structure]

**Risk 3:** [Same structure]

[Document 5-8 major risks from AI1's research + any AI2 identified]

---

## Resources & Context

**Research:**
- /START_HERE.md (AI1's comprehensive research)
- /OUTLINE.md (AI2's checkpoint map)

**Execution guides:**
- /OVERVIEW_GUIDE.md (quick-start - read first)
- /guides/CP0_GUIDE.md through CPX_GUIDE.md (detailed instructions)

**Progress tracking:**
- /TODO_TRACKER.md (update after each CP)

**Strategic context:**
- ATLAS_STEPS.md (Step X, Substep Y definition)
- COMPANY_CONTEXT.md (company vision, constraints)

**Previous work:**
- STEP_X_{Y-1} COMPLETION_SUMMARY (if exists)
- Relevant LEARNINGS_LOG entries

---

## Quality Standards

**All deliverables must meet:**

**Performance:**
- [Specific targets for this Effort]
- Example: <2s mobile load, Lighthouse 90+, API <500ms response

**Accessibility:**
- WCAG AA minimum (if user-facing)
- Zero critical errors (axe DevTools scan)
- Keyboard navigation works
- Screen reader compatible

**Security:**
- No hardcoded secrets (all in .env)
- Input validation (never trust user input)
- SQL injection prevention (parameterized queries)
- XSS prevention (sanitize output)
- OWASP Top 10 checked

**Code quality:**
- TypeScript strict mode
- ESLint zero errors
- No console.log in production
- Proper error handling
- Test coverage >70% (if measured)

**Multi-vertical (if applicable):**
- Works for contractor sites
- Works for law firm sites
- Works for healthcare sites
- Scoring/layout universal (not vertical-specific)

---

## Related Documentation

**Created by AI1:**
- START_HERE.md (research)

**Created by AI2:**
- OUTLINE.md (CP map)
- OVERVIEW_GUIDE.md (quick-start)
- guides/*.md (all CP guides)
- TODO_TRACKER.md (progress)
- effort.md (this file)

**Created by AI3:**
- Code/implementation
- artifacts/*.md (per-CP notes)
- COMPLETION_SUMMARY.md (final handoff)

**External:**
- ATLAS_STEPS.md (strategy)
- Company CONTEXT.md (vision)
- LEARNINGS_LOG.md (past discoveries)

---

## Status History

### [Date]: Effort Created
- AI2 completed planning
- All guides created
- Ready for AI3 execution
- Status: PLANNED

### [Date]: Execution Started
- AI3 began CP0
- Status: IN_PROGRESS

### [Date]: CPX Complete
- Final checkpoint done
- PR created
- Status: COMPLETE (awaiting PR merge)

### [Date]: PR Merged
- Human approved and merged
- Production deployed
- Substep officially complete

---

**Created by AI2. Links to all Effort documentation. Quick reference for status and goals.**
