# AI1/AI2 Research Guide - Lessons from STEP_0.2

**Purpose:** Practical research methodology based on what actually worked in STEP_0.2
**Created:** 2025-12-27 (after STEP_0.2 AI2 planning complete)
**Grade:** A (96/100) - use this as template
**For:** Future AI1s and AI2s executing STEP_1, STEP_2, STEP_3, etc.

---

## What This Guide Provides

**Based on real STEP_0.2 execution:**
- What research to do (sources)
- How to research (methodology)
- How much time to allocate (50% research, 50% guides)
- What made the difference (grade A vs B)

---

## Core Research Principles (Apply to All Steps)

### Principle 1: Web Search for Latest Patterns (Don't Trust 6-Month-Old Docs)

**What happened in STEP_0.2:**
- CTO's MCP_ARCHITECTURE.md (6 months old) specified `SSEServerTransport`
- AI2 web searched: "MCP Streamable HTTP transport 2025"
- Discovered: SSE deprecated March 2025, Streamable HTTP is current
- Updated all guides to modern pattern
- **Impact:** Prevented building on deprecated technology

**How to apply:**

```markdown
For EACH technology in your substep:
1. Identify version/date in CTO docs
2. Web search: "[Technology] latest 2025 [feature]"
3. Check official docs for deprecation warnings
4. Compare CTO pattern vs current pattern
5. If different: Document decision to update (DECISION_LOG.md)

Example for STEP_1.1:
- CTO says: "shadcn/ui with Radix UI"
- Web search: "shadcn/ui December 2025 updates"
- Find: Base UI integration (Dec 2025), Registry Directory (Dec 21)
- Validate: Compatible with Next.js 16 + Tailwind v4?
- Document: "Updated to Base UI (Dec 2025), not legacy Radix only"
```

**Time allocation:** 30-60 min per technology (worth it to avoid deprecated patterns)

---

### Principle 2: Read Actual Files (Not Just Summaries)

**What happened in STEP_0.2:**
- AI1's START_HERE said: "v2/ has 7 config files"
- AI2 initially trusted summary
- Then actually inspected: `ls v2/`, `cat v2/package.json`, etc.
- Found: types/ directory, migrations/, .gitignore details
- Enhanced CP0 from 7 validations → 13 categories
- **Impact:** Caught issues that summaries missed

**How to apply:**

```markdown
For YOUR substep:
1. Don't trust START_HERE.md alone
2. Inspect actual directory structure
3. Read actual config files
4. Check actual migration files
5. Validate what AI1 said against reality

Example for STEP_1.1:
- START_HERE says: "16 blocks required"
- Don't just accept - Read COMPONENTS_AND_VALIDATION.md lines 1-1186 (ALL block specs)
- Check: Do contractors actually use these patterns?
- Validate: Are 16 blocks sufficient? (or need 12? or 20?)
- Browse 20 contractor sites: Count hero types, proof types, service layouts
- Document: "Analyzed 20 sites: 67% split hero, 22% centered → 3 hero types sufficient"
```

**Time allocation:** 1-2 hours per major assumption (prevents building wrong thing)

---

### Principle 3: Read ARCHIVE Code for Algorithms (But Don't Copy Structure)

**What happened in STEP_0.2:**
- CP1 needed platform detection, DOM metrics, screenshot capture
- AI2 read 6 ARCHIVE files:
  - platform-detector.ts (WordPress API probe logic)
  - dom-metrics-capture.ts (button/link/heading capture)
  - crawlee-fetcher.ts (Playwright patterns)
  - screenshot-capture.ts (viewport sizes)
  - clone-result.ts (type structures)
  - match-verification.ts (safety algorithm)
- Extracted: Algorithm logic (preserve)
- Rebuilt: MCP server structure (new)
- **Impact:** CP1 has complete working code with proven algorithms

**How to apply:**

```markdown
For YOUR algorithm references:
1. Identify which ARCHIVE files contain algorithms you need
2. Read complete files (not just snippets)
3. Extract logic patterns (regex, math, thresholds)
4. Document: "Reference lines X-Y for algorithm Z"
5. Rebuild structure from scratch (MCP, tests, modern patterns)

Example for STEP_2.2 (match-verification):
- Need: match-verification.ts (SAFETY CRITICAL)
- Read: ARCHIVE-V0/apps/enrichment/src/lib/match-verification.ts (381 lines)
- Extract: Domain match = 0.99, Phone match = 0.95, Display threshold = 0.70
- Copy: EXACTLY (git show command, character-for-character)
- Add: 100+ test cases IMMEDIATELY
- Document: "COPIED EXACT - DO NOT MODIFY"

Example for STEP_1.1 (no copying):
- Need: Hero layout patterns
- Research: 20 contractor sites (not ARCHIVE)
- Extract: Split 67%, Centered 22%, Fullbleed 11%
- Build: NEW components from scratch (no ARCHIVE code)
- Document: "Patterns from contractor research, no ARCHIVE copying"
```

**Time allocation:** 2-4 hours reading ARCHIVE (when algorithms needed)

---

### Principle 4: Read CTO Docs Completely (Not Just Skim)

**What happened in STEP_0.2:**
- Read DATABASE_SCHEMA.md fully (600 lines)
- Read MCP_ARCHITECTURE.md fully (1,061 lines)
- Read DEEP_STACK.md sections (400+ lines)
- Found: Complete schemas, RLS policies, client patterns, security rules
- Used in CP3_GUIDE for exact schema documentation
- **Impact:** Schemas match reality (no "close enough" errors)

**How to apply:**

```markdown
For YOUR CTO docs:
1. Identify which CTO docs apply to your substep
2. Read ENTIRE doc (not just AI1's referenced lines)
3. Extract: Patterns, schemas, code examples, gotchas
4. Validate: Does this still apply? (or outdated like SSE?)
5. Document sources in CP guides (line numbers for reference)

Example for STEP_1.1:
- Read: COMPONENTS_AND_VALIDATION.md (lines 1-1186, ALL blocks)
- Extract: Every prop for every block, every variant, every constraint
- Don't skim: Read block 1-16 completely
- Validate: Props make sense? Missing anything from contractor research?
- Document: "Hero_Split props from COMPONENTS line 45-67"

Example for STEP_2.1:
- Read: AGENT_SYSTEM.md (lines 137-494, state schema + graph topology)
- Extract: DemoGenerationState complete structure, all Annotated reducers
- Don't skim: Understand WHY each reducer (prevents what problem?)
- Validate: Schema supports all 13 agents? Missing fields?
- Document: "State schema from AGENT_SYSTEM lines 140-227"
```

**Time allocation:** 3-5 hours reading CTO docs (worth it for completeness)

---

### Principle 5: Validate Schemas Against Actual Reality

**What happened in STEP_0.2:**
- Initially wrote CP3 schemas from memory
- Human caught: "use the cli or migration file to verify"
- Read actual migration: `00000000000002_create_schema.sql`
- Found discrepancies:
  - enrichment_cache: Missing 15 columns
  - waitlist: Wrong PK (email vs UUID id)
  - demo_sites: Missing last_viewed_at, archived_at
- Fixed all schemas to match exact migration
- **Impact:** Prevented query errors in production

**How to apply:**

```markdown
For ANY schema documentation:
1. Don't trust memory or summaries
2. Read actual migration files
3. Or: Use CLI to query actual schema
4. Copy EXACT column names, types, constraints
5. Include indexes, RLS policies, helper functions

Example for STEP_1.1 (no schema work):
- N/A (components don't have schemas)

Example for STEP_2.1 (ai_generations table):
- Don't trust: "ai_generations has id, demo_request_id, thread_id"
- Read: v2/supabase/migrations/00000000000002_create_schema.sql lines 54-73
- Extract: ALL 10 columns (id, demo_request_id, langgraph_thread_id, cost_cents, tokens_used, agent_count, started_at, completed_at, final_state, agent_trace)
- Validate: Query Supabase - \d ai_generations
- Document: Exact schema in guides (copy-paste SQL)
```

**Time allocation:** 30 min verification (prevents hours of debugging)

---

## Research Allocation (50% Rule)

**STEP_0.2 Time Breakdown:**
- OUTLINE creation: 1 hour (10%)
- CP0 research: 2 hours → CP0 guide: 2 hours = 4h total
- CP1 research: 4 hours → CP1 guide: 2 hours = 6h total
- CP2 research: 3 hours → CP2 guide: 1.5h = 4.5h total
- CP3 research: 2 hours → CP3 guide: 2 hours = 4h total
- Support docs: 1 hour (10%)

**Total:** ~20 hours (50% research, 40% guides, 10% overhead)

**The pattern:** Research time ≈ Guide creation time (or more for complex CPs)

---

## Specific Research Advice by Step

### STEP_1.1 Research (Core Blocks - Heroes + Proof)

**What AI1 should research (6-8 hours):**

**1. Contractor Pattern Analysis (3 hours)**
```markdown
Method:
1. Select 20 contractor sites:
   - 7 plumbers (Cooper Plumbing + top Google "plumber [city]" for Houston, Denver, Phoenix, Seattle, Austin, Dallas, Atlanta)
   - 7 HVAC (top Google "HVAC [city]" for same cities)
   - 6 electricians (top Google "electrician [city]")

2. For EACH site (6 min per site = 2 hours total):
   - Screenshot: Desktop 1440×900, Mobile 375×812
   - Classify hero: Split (image left/right)? Centered? Fullbleed background? Other?
   - Extract brand colors: DevTools → Inspect CTA button → computed background-color → copy hex
   - Note typography: DevTools → h1 font-family (what fonts do contractors use?)
   - Identify proof: Reviews visible? Where? Badges? Stats? None?
   - Count services: How many services listed? (range: 3-12)

3. Create frequency table (1 hour):
   - Hero layouts: Split 67%, Centered 22%, Fullbleed 11%
   - Proof strategies: Reviews 30%, Badges 40%, Stats 60% (overlaps common)
   - Brand colors: Blues 70%, Reds 15%, Greens 10%, Neutrals 5%
   - Services count: 6 services 70%, 3-4 services 20%, 8+ services 10%
   - Typography: Sans-serif 95% (Inter, Roboto, System), Serif 5%

Deliverable: Pattern frequency table + 40 screenshots (20 sites × 2 viewports) in START_HERE.md
```

**2. Premium Quality Calibration (2 hours)**
```markdown
Method:
1. Study premium sites (45 min):
   - Stripe.com: Measure section padding (DevTools → <section> → computed padding-top)
     Result: 96px = 6rem (generous whitespace)
   - Vercel.com: Count accent colors (DevTools → find all colored elements → unique hex values)
     Result: 2 colors (blue, purple) - restrained palette
   - Linear.app: Extract type scale (h1, h2, h3, body font-size → calculate ratios)
     Result: 1.333 ratio (perfect fourth scale: 16 → 21 → 28 → 37 → 49px)
   - Raycast.com: Animation timing (DevTools → inspect Framer Motion → duration)
     Result: 0.4s entrance, 0.15s hover (subtle, quick)

2. Create premium checklist (45 min):
   - Spacing: ≥3rem section padding (48px minimum)
   - Colors: ≤3 accent colors (+ neutrals)
   - Typography: 1.25-1.5× ratio between heading levels
   - Motion: ≤0.5s animations, subtle transforms only
   - Mobile headlines: ≥32px (not cramped)

3. Apply to block specs (30 min):
   - Hero_Split: section padding 80px (5rem) ✓
   - Proof_ReviewCards: 2 accent colors max ✓
   - All blocks: 1.333 type ratio ✓
   - All blocks: Mobile h1 ≥32px ✓

Deliverable: Premium Design Checklist with measurements (not descriptions) in START_HERE.md
```

**3. shadcn/ui Latest Updates (1 hour)**
```markdown
Method:
1. Visit ui.shadcn.com (30 min):
   - Check: Dec 2025 updates (Base UI launched Dec 21)
   - Read: Installation guide for Next.js 16 + Tailwind v4
   - Test: Create test project, install Card component
   - Validate: Works with Tailwind v4? (test npm install)

2. Read source code for Card (30 min):
   - View: Card component on GitHub
   - Extract: Radix Primitive usage (accessibility built-in)
   - Understand: How to customize (variant prop, Tailwind classes)
   - Test: Can apply brand colors to Card? (className override)

Deliverable: shadcn/ui compatibility report (Dec 2025 features, Next.js 16 validated) in START_HERE.md
```

**4. Tailwind v4 Patterns (1 hour)**
```markdown
Method:
1. Read v4 blog post (30 min):
   - https://tailwindcss.com/blog/tailwindcss-v4
   - Extract: Rust engine (5× faster), No config needed (@import "tailwindcss"), Container queries (built-in), Backdrop-blur (native)
   - Breaking changes: Config format? Class changes? Migration path?

2. Test v4 installation (30 min):
   - Create test Next.js 16 project
   - Install: npm install tailwindcss@next
   - Test: @import "tailwindcss" in globals.css (works?)
   - Test: backdrop-blur-md class (glass nav requirement)
   - Measure: Build time vs v3 (should be 5× faster)

Deliverable: Tailwind v4 migration guide (breaking changes, patterns, build time validation) in START_HERE.md
```

**5. Accessibility Testing Approach (30 min)**
```markdown
Method:
1. Read axe-core + Playwright integration (15 min):
   - https://www.npmjs.com/package/@axe-core/playwright
   - Pattern: new AxeBuilder({ page }).withTags(['wcag2aa']).analyze()
   - Understand: What violations look like, how to fix

2. Test on example component (15 min):
   - Create simple button, run axe-core
   - Introduce violations: Missing alt text, low contrast
   - Verify: axe-core catches violations
   - Fix: Add alt, adjust color, re-test (zero violations)

Deliverable: Accessibility testing pattern (code example, common violations, fixes) in START_HERE.md
```

**Total AI1 Research:** 6-8 hours (comprehensive)

**What AI2 should research before creating guides (4-6 hours):**

**CP0_GUIDE research (1 hour):**
- Study: Turborepo package creation (pnpm workspace addition)
- Study: Storybook 8.0 + Next.js 16 setup
- Study: Chromatic free tier limits (5,000 snapshots/month)
- Read: STEP_0.2 RAILWAY.md (deployment patterns to reuse)

**CP1_GUIDE research (2 hours):**
- Study: Next.js Image component API (priority, blur, responsive srcset)
- Study: Framer Motion LazyMotion (how to import domAnimation)
- Read: Hero_Split_ImageLeft spec completely (props, variants, mobile behavior)
- Test: Create simple hero with image, verify responsive works

**CP2_GUIDE research (1.5 hours):**
- Study: shadcn/ui Card source code (how CardHeader/CardContent work)
- Study: Review safety gates (how to ensure verified=false NEVER renders)
- Read: Proof_ReviewCards_Grid spec completely
- Test: Create Card with conditional rendering (verified prop)

**CP3_GUIDE research (1.5 hours):**
- Study: Chromatic visual regression workflow (baseline, comparison, approval)
- Study: axe-core test suite patterns (how to scan all Storybook stories)
- Read: CEO rubric (8 categories, what ≥8/10 means)
- Plan: Composition test workflow (how to manually compose)

**Total AI2 Research:** 4-6 hours

**Total STEP_1.1:** 10-14 hours research (before any guide writing)

---

### STEP_2.1 Research (Tokens + Orchestrator)

**What AI1 should research (8-10 hours):**

**1. LangGraph PostgreSQL Checkpointer (3 hours)**
```markdown
Method:
1. Read official docs (1 hour):
   - https://pypi.org/project/langgraph-checkpoint-postgres/
   - Extract: from_conn_string method, .setup() sequence
   - Find: 2025 breaking changes (autocommit=True required)

2. Read community guides (1 hour):
   - https://sparkco.ai/blog/mastering-langgraph-checkpointing-best-practices-for-2025
   - Extract: Common pitfalls (row_factory=dict_row needed)
   - Pattern: Connection setup code

3. Test implementation (1 hour):
   - Create test script: Connect to Supabase v2
   - Run: await checkpointer.setup()
   - Verify: 4 tables created (checkpoints, checkpoint_blobs, checkpoint_writes, checkpoint_migrations)
   - Query: SELECT * FROM checkpoints (should be empty initially)
   - Test: Save checkpoint, retrieve checkpoint

Deliverable: AsyncPostgresSaver setup guide with working code + gotchas in START_HERE.md
```

**2. Annotated Reducers Testing (2 hours)**
```markdown
Method:
1. Read LangGraph state docs (1 hour):
   - https://sparkco.ai/blog/mastering-langgraph-state-management-in-2025
   - Extract: Why Annotated? (race condition prevention)
   - Patterns: Dict merge, List append, Integer add

2. Create test scenarios (1 hour):
   - Without reducers: Simulate parallel writes → data loss
   - With reducers: Simulate parallel writes → data preserved
   - Code: Test suite proving necessity (as shown in STEP_2.md)
   - Measure: Data loss rate (should be 0% with reducers, >0% without)

Deliverable: Reducer test suite (proves necessity) in START_HERE.md
```

**3. Design Token Extraction Testing (3 hours)**
```markdown
Method:
1. Test 5 contractor sites (2 hours):
   - Cooper Plumbing (known colors: #E26F2F, #2EA3F2)
   - Denver plumber (unknown colors)
   - Seattle HVAC (unknown colors)
   - Austin electrician (unknown colors)
   - Phoenix contractor (unknown colors)

2. For EACH site (24 min each):
   - Try Approach A: Search HTML for CSS variables (--brand-primary)
   - Try Approach B: Extract logo, use extract-colors library for dominant color
   - Try Approach C: Find CTA button, get background-color
   - Record: Which approach succeeded? Confidence level? Colors accurate?

3. Calculate success rates (1 hour):
   - CSS vars: 40% success, 0.9 avg confidence
   - Logo analysis: 60% success, 0.6 avg confidence
   - Button sampling: 80% success, 0.5 avg confidence
   - Fallback strategy: Try in order until ≥0.7 confidence

Deliverable: Color extraction algorithm comparison with success rates in START_HERE.md
```

**Total AI1 Research:** 8-10 hours

**What AI2 should research (4-6 hours):**

**CP1_GUIDE research (2 hours):**
- Study: extract-colors npm library API
- Study: chroma.js contrast calculation
- Test: Extract from actual logo (Cooper Plumbing logo if available)
- Read: BrandTokens schema completely (all fields, validation rules)

**CP2_GUIDE research (2 hours):**
- Study: StateGraph API (sequential, parallel, conditional edges)
- Read: AGENT_SYSTEM.md graph topology (lines 316-494)
- Test: Create simple graph (2 nodes), run, verify checkpoint saved
- Read: DemoGenerationState schema completely

**CP3_GUIDE research (1-2 hours):**
- Study: RetryPolicy configuration
- Study: LangSmith integration (LANGCHAIN_TRACING_V2=true)
- Test: Simulate agent failure, verify retry works
- Plan: Integration testing approach

**Total STEP_2.1:** 12-16 hours research

---

### STEP_2.2 Research (MCP Analyzer + Enrichment)

**What AI1 should research (6-8 hours):**

**1. ARCHIVE Algorithm Deep Read (4 hours)**
```markdown
Method:
1. Read brand-analyzer.ts completely (1 hour):
   - ARCHIVE-V0/apps/site-analyzer/src/analyzers/brand-analyzer.ts
   - Extract: Color extraction algorithm (CSS vars → logo → button cascade)
   - Extract: Confidence scoring logic (how 0.7 threshold determined)
   - Note: Which lines to preserve in NEW implementation

2. Read mobile-analyzer.ts completely (1 hour):
   - Lines for text size detection (<16px counting)
   - Lines for tap target measurement (<44px counting)
   - Lines for overflow detection (scrollWidth > clientWidth)
   - Thresholds: 16px text, 44px taps (CEO requirements)

3. Read match-verification.ts completely (2 hours):
   - All 381 lines
   - Understand: Domain match = 0.99, Phone match = 0.95, Address = 0.80, Name only = 0.60
   - Understand: Display threshold = 0.70 (hardcoded safety)
   - Extract: Phone normalization (E.164), domain extraction, fuzzy address matching
   - Document: "COPY EXACT - lines 1-381, no modifications"

Deliverable: Algorithm extraction guide (which logic to preserve, test coverage plan) in START_HERE.md
```

**2. MCP Stdio Server Patterns (1 hour)**
```markdown
Method:
1. Read MCP TypeScript SDK docs (30 min):
   - https://github.com/modelcontextprotocol/typescript-sdk
   - Pattern: StdioServerTransport (stdin/stdout communication)
   - Example: Tool registration, request handlers

2. Test from Python (30 min):
   - Create dummy MCP stdio server (TypeScript)
   - Spawn from Python with langchain-mcp-adapters
   - Validate: Can call tool, receive response
   - Measure: Spawn time, execution time

Deliverable: MCP stdio implementation pattern with Python test in START_HERE.md
```

**3. Google Places API Research (1 hour)**
```markdown
Method:
1. Read API docs (30 min):
   - Find Place API: Text search for business
   - Place Details API: Reviews, rating, hours
   - Rate limits: 100 requests/day free, paid tiers
   - Cost: ~$0.017 per lookup

2. Test API (30 min):
   - Use API key from Bitwarden
   - Search: "Cooper Plumbing Houston"
   - Validate: Returns correct business?
   - Extract: place_id, rating, review_count, top 5 reviews

Deliverable: Google Places integration guide (API calls, response parsing, rate limits) in START_HERE.md
```

**4. Regression Testing Strategy (1-2 hours)**
```markdown
Method:
1. Plan comparison test:
   - Run ARCHIVE CLI on Cooper clone
   - Run NEW MCP server on same clone
   - Diff outputs (should be identical)

2. For 5 contractor sites:
   - ARCHIVE brand colors vs NEW brand colors (should match)
   - ARCHIVE mobile issues vs NEW mobile issues (should match)
   - ARCHIVE match confidence vs NEW match confidence (should match)

3. Document: Regression test suite (proves algorithms preserved)

Deliverable: Regression testing plan in START_HERE.md
```

**Total AI1 Research:** 6-8 hours

**What AI2 should research (3-4 hours):**

**CP1_GUIDE research (1.5 hours):**
- Study: Cheerio API (HTML parsing, CSS selector patterns)
- Study: extract-colors library usage
- Test: Parse sample HTML, extract colors
- Read: brand-analyzer.ts algorithms (lines to reference)

**CP2_GUIDE research (1.5 hours):**
- Study: match-verification.ts completely (understand all logic)
- Study: Google Places API authentication
- Test: Call Places API, parse response
- Plan: 100+ test cases (categories, edge cases)

**CP3_GUIDE research (1 hour):**
- Plan: Regression testing (ARCHIVE vs NEW comparison)
- Plan: Integration testing (Python calling both MCP servers)
- Read: STEP_2.1 orchestrator (how Agent 2 will call these tools)

**Total STEP_2.2:** 9-12 hours research

---

### STEP_3.1 Research (Context Loader - Agent 2)

**What AI1 should research (5-7 hours):**

**1. langchain-mcp-adapters Deep Dive (2 hours)**
```markdown
Method:
1. Read PyPI docs (1 hour):
   - https://pypi.org/project/langchain-mcp-adapters/
   - Extract: create_mcp_client_and_tools() API
   - Pattern: HTTP transport (Railway), stdio transport (local)
   - Understand: Returns (client, tools) tuple, tools are LangChain-compatible

2. Test 3 MCP servers (1 hour):
   - Test: Spawn mcp-site-analyzer (stdio)
   - Test: Spawn mcp-enrichment (stdio)
   - Test: Connect to mcp-site-cloner (Railway HTTP)
   - Validate: All 3 callable from Python
   - Measure: Total time (cloner 30-60s, analyzer <1s, enrichment 2-4s)

Deliverable: langchain-mcp-adapters integration code (3 clients initialized) in START_HERE.md
```

**2. ContextBundle Schema Design (2 hours)**
```markdown
Method:
1. Map MCP outputs to bundle (1 hour):
   - Read: CloneResult schema (from STEP_0.2 CP1)
   - Read: AnalysisResult schema (from STEP_2.2)
   - Read: EnrichmentResult schema (from STEP_2.2)
   - Design: Normalized structure (flatten nested fields)
   - Example: enrichment.match_verification.display → context.reviews.display

2. Define pruning strategy (1 hour):
   - Measure: Full bundle size (from test data)
   - Identify: What to prune (reviews: all 488 → top 3, decisions: full text → 100 chars)
   - Priority: Screenshots removable, low-confidence fields removable, SAFETY fields NEVER removable
   - Validate: Pruned bundle <50KB? Still has all required data?

Deliverable: ContextBundle complete schema + pruning algorithm in START_HERE.md
```

**3. Safety Gate Extraction Testing (1 hour)**
```markdown
Method:
1. Create test cases (30 min):
   - Cooper Plumbing: enrichment.match_verification.display = true
   - Mismatched business: enrichment.match_verification.display = false
   - Missing enrichment: enrichment = null

2. Test extraction (30 min):
   - For each case: Run normalization
   - Validate: context.reviews.display matches expected
   - Ensure: If null/missing, defaults to false (safe default)
   - Test: 100% accuracy required

Deliverable: Safety gate test suite (3 test cases, 100% pass required) in START_HERE.md
```

**Total AI1 Research:** 5-7 hours

**What AI2 should research (2-3 hours):**

**CP0_GUIDE research (45 min):**
- Read: langchain-mcp-adapters API docs
- Read: MCP_ARCHITECTURE.md (Agent 2 implementation)
- Plan: 3 MCP client initialization

**CP1_GUIDE research (1 hour):**
- Read: ContextBundle schema (from AI1)
- Study: Zod safeParse patterns
- Plan: Normalization mapping (field-by-field)
- Plan: Pruning algorithm

**CP2_GUIDE research (45 min):**
- Plan: Safety gate extraction testing
- Plan: Integration testing (end-to-end MCP → bundle)
- Read: STEP_2.1 orchestrator (how Agent 2 plugs in)

**Total STEP_3.1:** 7-10 hours research

---

## Research Quality Checklist

**Before declaring research complete, verify:**

- [ ] **Web searched latest patterns** (not just CTO docs from 6 months ago)
- [ ] **Read actual files** (migration, config, ARCHIVE code - not just summaries)
- [ ] **Tested key technologies** (don't assume, validate compatibility)
- [ ] **Measured specifics** (padding in px, colors in hex, timing in ms - not descriptions)
- [ ] **Created frequency tables** (contractor patterns: 67% split, 22% centered - not "mostly split")
- [ ] **Documented sources** (URLs, file paths, line numbers - traceable)
- [ ] **Validated assumptions** (schema matches migration, SDK version current, approach works)
- [ ] **Planned testing** (how to validate what you researched actually works)

**Grade correlation:**
- 8/8 checks = A+ research (STEP_0.2 level)
- 6-7/8 checks = A research (good)
- 4-5/8 checks = B research (rushed)
- <4/8 checks = C research (insufficient)

---

## Red Flags (Research Was Insufficient)

**If you catch yourself doing these, stop and research deeper:**

1. **"I'll just copy CTO's example"** - without validating it's current
   - Risk: Building on deprecated pattern (like SSE)
   - Fix: Web search "[technology] latest 2025", check deprecation warnings

2. **"The summary says it has 7 validations"** - without inspecting actual
   - Risk: Missing critical checks (types/, .gitignore, migrations/)
   - Fix: List actual directory, cat actual files, verify claims

3. **"I understand the algorithm conceptually"** - without reading code
   - Risk: Missing critical details (thresholds, edge cases, normalization)
   - Fix: Read complete ARCHIVE file, extract exact logic

4. **"Stripe has good spacing"** - without measuring
   - Risk: Vague standard, can't validate compliance
   - Fix: DevTools → measure padding in px, document: "96px = 6rem"

5. **"I'll write the schema from the description"** - without reading migration
   - Risk: Wrong PK, missing columns, missing indexes
   - Fix: Read actual SQL migration, copy exact schema

6. **"It probably works with Next.js 16"** - without testing
   - Risk: Breaking changes, incompatibility discovered during build
   - Fix: Create test project, install, verify compatibility

7. **"Tailwind v4 is like v3"** - without reading changelog
   - Risk: Missing new features (container queries), using deprecated patterns
   - Fix: Read v4 blog post, test installation, validate breaking changes

8. **"16 blocks should cover patterns"** - without analyzing sites
   - Risk: Gaps in coverage (missing common patterns)
   - Fix: Analyze 20 sites, create frequency table, validate coverage

---

## Time Allocation Template

**For EACH substep (use this formula):**

```
Total AI1 + AI2 time = Substep duration estimate
AI1 research = 40-50% of total
AI2 research = 20-25% of total
AI2 guide creation = 25-35% of total
Overhead = 5-10%

Example STEP_1.1 (1 week = 40 hours):
- AI1 research: 16-20 hours (40-50%)
- AI2 research: 8-10 hours (20-25%)
- AI2 guides: 10-14 hours (25-35%)
- Overhead: 2-4 hours (5-10%)

Example STEP_0.2 (8 hours):
- AI1 research: 4 hours (50%)
- AI2 research: 2 hours (25%)
- AI2 guides: 1.5 hours (19%)
- Overhead: 0.5 hours (6%)
```

**The 50% rule:** Half the time should be research. Rushed research = poor guides = AI3 struggles.

---

## Sources to Always Check

**For ANY substep, always research:**

1. **CEO_VISION.md** - What quality bar? What non-negotiables?
2. **THE_BACKGROUND.md** - What worked? What failed? (learn from history)
3. **Relevant CTO docs** - Technical patterns, but verify still current
4. **ARCHIVE code** - Algorithms to preserve (if applicable)
5. **Official SDK/framework docs** - Latest APIs, deprecation warnings
6. **Community guides** - Real-world patterns, gotchas, best practices (2025 guides)
7. **STEP_0 docs** - Infrastructure patterns (Supabase, Railway, git workflow)
8. **Actual files** - Migrations, configs, directory structure (ground truth)

**Time per source:** 30-60 min each (8 sources = 4-8 hours baseline research)

---

## What Made STEP_0.2 Get A (96/100)

**Strengths (what to repeat):**
1. ✅ Web searched latest patterns (found SSE deprecated)
2. ✅ Read actual migration files (exact schemas)
3. ✅ Read 6 ARCHIVE files (algorithms for CP1)
4. ✅ Read CTO docs completely (not just AI1's referenced lines)
5. ✅ Enhanced CP0 beyond original (13 vs 7 validations)
6. ✅ Provided complete code (not pseudocode)
7. ✅ Documented all sources (URLs, line numbers)
8. ✅ Validated CEO alignment (mobile metrics, wow-ables)

**Weaknesses (what to avoid):**
1. ⚠️ CP3 could have more full examples (provided structure, not all content)
2. ⚠️ Directory structure initially deviated (fixed after review)
3. ⚠️ Time estimates slightly off (noted but not perfect)
4. ⚠️ OUTLINE not updated after research (SSE→Streamable HTTP discovery)

**For A+ (98-100):**
- All content complete (no "[Include schema...]" placeholders)
- All estimates accurate (time, CP count, deliverables)
- All docs updated after discoveries (OUTLINE, effort.md, etc.)
- Zero deviations from source docs (unless justified)

---

## Final Advice for Future AI1/AI2

**From STEP_0.2 experience:**

**AI1 (Researchers):**
- Budget 40-50% of substep time for research
- Web search EVERYTHING for "latest 2025" patterns
- Read actual files, not summaries
- Test key technologies (don't assume compatibility)
- Measure specifics (px, ms, %) not descriptions
- Document sources with line numbers

**AI2 (Planners):**
- Budget 20-25% MORE time for research BEFORE guides
- Read AI1's START_HERE completely first
- Re-validate AI1's research (check sources)
- Inspect actual state (files, schemas, directory structure)
- Enhance beyond AI1 if inspection reveals more
- Update all affected docs (OUTLINE, ATLAS_STEPS, LEARNINGS, DECISIONS)

**The Quality Bar:**
- A+ (98-100): Comprehensive research, zero gaps, all current, tested
- A (94-97): Thorough research, minor gaps, mostly current, mostly tested
- B (85-93): Good research, some gaps, some assumptions, partially tested
- C (<85): Rushed research, major gaps, outdated patterns, untested

**STEP_0.2 achieved A (96) - use as template for future Steps.**

---

**This guide based on real execution. Follow these patterns for consistent A-grade research.**
