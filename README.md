# ATLAS v3.0

**Adaptive Task & Lifecycle Architecture System**

Structured orchestration framework for building companies from zero to scale.

**New in v3.0:** Clean installation with improved strategy structure (individual step files, high-level tracker)

---

## What Is ATLAS?

ATLAS is a **three-phase AI orchestration system** that transforms strategic vision into systematic execution.

**Three AI phases (sequential):**
1. **AI1 Research** → Investigates entire substep, produces comprehensive START_HERE
2. **AI2 Planning** → Validates research, creates execution guides for all checkpoints
3. **AI3 Execution** → Implements all checkpoints, produces working deliverables

**Not checkpoint-based roles.** Linear handoff: AI1 completes → AI2 completes → AI3 executes all checkpoints.

---

## Technology Stack (Examples)

**Examples in this framework use:** Next.js + Vercel + Supabase

The framework structure (AI1→AI2→AI3 phases, checkpoints, progress tracking) is **technology-agnostic**. The orchestration system works with any tech stack - Python, Go, mobile, desktop, or any other platform. Examples show web development patterns, but adapt the implementation details to your stack while keeping the framework workflow intact.

See [ONBOARDING.md](./ONBOARDING.md) for guidance on adapting to your technology choices.

---

## Customization is Critical

**ATLAS provides orchestration structure, not project-specific guardrails.**

You must customize role files to encode YOUR engineering standards as AI instructions:
- **Security requirements:** HIPAA compliance checks vs reasonable auth vs minimal (internal tools)
- **Quality standards:** API stability requirements, performance targets, testing depth
- **Git workflow:** Your specific branching strategy, PR requirements, deployment process
- **Documentation needs:** API docs, compliance documentation, or minimal internal notes
- **Domain-specific validations:** What should AI watch for in YOUR project type?

**The framework works because you adapt it.** Generic guardrails fit no one perfectly. Customized guardrails make AI follow your exact engineering practices.

See [ONBOARDING.md - Phase 3](./ONBOARDING.md#phase-3-customize-role-files-for-your-domain-1-2-hours) for detailed customization guide with concrete examples.

---

## When to Use ATLAS

**Perfect for:**
- Building companies from 0 to 1
- Multi-month projects with evolving strategy
- Work requiring deep research → detailed planning → precise execution
- Teams needing exact progress tracking and resume capability
- Projects where learning can compound over time (with later efforts becoming more efficient)

**Not needed for:**
- Weekend projects
- Simple bug fixes
- Well-defined 1-week tasks
- Work with no strategic uncertainty

---

## Important Context

**What ATLAS provides:**
- Structured workflow for planning and execution
- Knowledge capture and compounding mechanisms
- Progress tracking and resume capability
- Systematic approach to complex projects

**What ATLAS does not guarantee:**
- Market fit (you must validate your market)
- Execution quality (requires skilled execution)
- Business outcomes (framework reduces chaos, doesn't ensure success)
- Speed improvements (gains depend on consistent application and learning)

**Reality check:**
Building a successful company is extremely difficult. Most fail due to market factors, not execution frameworks. ATLAS helps with the "how to build" - you're responsible for "what to build" and "who wants it."

---

## Quick Links

**New to ATLAS?**
→ [QUICK_START.md](./QUICK_START.md) - *30 minutes to operational*

**Want complete understanding?**
→ [ATLAS_OVERVIEW.md](./ATLAS_OVERVIEW.md) - *Complete system explanation*

**Ready to configure for your company?**
→ [ONBOARDING.md](./ONBOARDING.md) - *Setup guide*

**Need technical specification?**
→ [ATLAS_SPECIFICATION.md](./ATLAS_SPECIFICATION.md) - *Complete workflow spec*

**Validating framework?**
→ [ATLAS_VALIDATION.md](./ATLAS_VALIDATION.md) - *Verify correctness*

---

## File Structure

```
ATLAS3/
├── README.md                          # You are here
├── ATLAS_OVERVIEW.md                  # System explanation
├── ATLAS_GLOSSARY.md                  # Terminology
├── ATLAS_ENTRY_POINT.md               # Auto-detection & routing
├── ATLAS_SPECIFICATION.md             # Technical spec
├── ATLAS_VALIDATION.md                # Validation checklist
├── QUICK_START.md                     # Fast-track guide
├── ONBOARDING.md                      # Company setup guide
├── HUMAN_GUIDE.md                     # Human operational manual
│
├── roles/                             # AI role guides
│   ├── AI1_RESEARCHER_GUIDE.md
│   ├── AI2_GUIDE_CREATOR_GUIDE.md
│   ├── AI3_IMPLEMENTER_GUIDE.md
│   ├── AI3_DEVELOPER_BEST_PRACTICES.md
│   └── GIT_WORKFLOW.md
│
├── templates/                         # File templates
│   ├── START_HERE_TEMPLATE.md
│   ├── OUTLINE_TEMPLATE.md
│   ├── OVERVIEW_GUIDE_TEMPLATE.md
│   ├── TODO_TRACKER_TEMPLATE.md
│   ├── COMPLETION_SUMMARY_TEMPLATE.md
│   ├── CP_GUIDE_TEMPLATE.md
│   └── EFFORT_TEMPLATE.md
│
├── strategy/                          # Strategic layer
│   ├── ATLAS_STEPS_TRACKER.md         # High-level status
│   ├── STEP_DEFINITION_GUIDE.md       # How to write steps
│   ├── steps/                         # Individual step files
│   │   ├── STEP_TEMPLATE.md           # Template
│   │   └── (STEP_1.md, STEP_2.md created during setup)
│   ├── ATLAS_ASSUMPTIONS.md           # Template
│   ├── LEARNINGS_LOG.md               # Template
│   └── DECISION_LOG.md                # Template
│
├── context/
│   └── CONTEXT_INDEX.md               # Context loading rules
│
└── migrations/
    └── MIGRATIONS_LOG.md              # Database tracking
```

---

## The Workflow (Correct)

```
Substep Defined (steps/STEP_X.md)
  ↓
AI1 Research Phase (6-12 hours)
  - Researches ENTIRE substep scope
  - Produces START_HERE.md
  → Marker: START_HERE.md exists
  ↓
AI2 Planning Phase (8-15 hours)
  - Reads & validates START_HERE
  - Creates OUTLINE (3-10 CPs)
  - Researches EACH CP deeply
  - Creates CP guides (one per CP)
  - Creates OVERVIEW_GUIDE, TODO_TRACKER
  → Marker: All guides + TODO_TRACKER exist
  ↓
AI3 Execution Phase (1-4 weeks)
  - Pre-flight checks (git sync)
  - Executes CP0 (setup)
  - Updates TODO_TRACKER
  - Executes CP1 (implementation)
  - Updates TODO_TRACKER
  - ... continues for all CPs
  - Final CP: Testing, PR creation
  - Creates COMPLETION_SUMMARY
  - Updates ATLAS_STEPS_TRACKER.md + steps/STEP_X.md
  → Marker: COMPLETION_SUMMARY exists, PR created
  ↓
Human Approves PR
  - Merges to main
  - Substep complete
  ↓
Next Substep AI1 Reads COMPLETION_SUMMARY
  - Cycle continues
```

---

## Core Principles

**1. Linear AI Handoff**
- AI1 → AI2 → AI3 (sequential phases, not role-per-checkpoint)

**2. Research Tapers**
- AI1: 80% research (deep investigation)
- AI2: 50% research (validation + CP-specific)
- AI3: 20% research (spot-checks + sanity validation)

**3. Progress is Always Known**
- File existence shows AI phase
- TODO_TRACKER shows CP progress
- ATLAS_STEPS.md shows Step/Substep status

**4. Auto-Detection**
- "Continue ATLAS on X" → Framework determines phase and CP automatically
- No manual state tracking required

**5. Learning Compounds**
- COMPLETION_SUMMARY → Next AI1 (efficient handoff)
- LEARNINGS_LOG → Future planning (patterns applied)
- Velocity can improve (Effort 20 may be 2-5x more efficient than Effort 1, depending on execution)

---

## Version

**Current:** v3.0
**Status:** Structured framework (clean installation)
**Designed for:** Complex software projects requiring systematic execution discipline (any scale, commercial or non-commercial)

---

## Philosophy

ATLAS v3.0 embodies:

**Measure thrice, cut once:**
- AI1 researches deeply (measure)
- AI2 plans thoroughly (measure again)
- AI3 executes precisely (cut)

**Exact progress tracking:**
- Always know: Which Step? Which Substep? Which CP?
- Resume from exact point (never lose state)

**Knowledge compounds:**
- Each Effort teaches the next
- Templates evolve based on learnings
- Velocity can improve with consistent application

**Quality is non-negotiable:**
- Security gates (AI3 checks vulnerabilities)
- Testing after each CP (not deferred)
- Human approval for production (final quality gate)

---

## Get Started

**First time:**
1. Read [ATLAS_OVERVIEW.md](./ATLAS_OVERVIEW.md) - 20 minutes
2. Read [ONBOARDING.md](./ONBOARDING.md) - 30 minutes
3. Create your company vision doc - 1 hour
4. Create ATLAS_STEPS_TRACKER.md and steps/STEP_X.md files (your strategy) - 1-2 hours
5. Start executing - "Run ATLAS to research STEP_1_1"

**Quick start:**
1. Read [QUICK_START.md](./QUICK_START.md) - 10 minutes
2. Minimal config - 1 hour
3. Start immediately

---

## Built For

Companies that benefit from systematic planning and execution discipline, particularly those building complex software products with evolving requirements.

---

## Support

**Questions?**
- Read [ATLAS_SPECIFICATION.md](./ATLAS_SPECIFICATION.md) - Complete technical spec
- Check [ATLAS_VALIDATION.md](./ATLAS_VALIDATION.md) - Verify setup
- Review [HUMAN_GUIDE.md](./HUMAN_GUIDE.md) - Operational procedures

**Issues?**
- Validate setup (ATLAS_VALIDATION.md Level 1-6)
- Check workflow (specification vs implementation)
- Review examples (see how it should work)

---

**Welcome to ATLAS v3.0. A framework for disciplined company building.**
