# Mode 3: Direct to Substep - Skip Scanning, Go Directly

**Purpose:** Human specifies exact substep, skip auto-detection scanning
**Usage:** ~8% (when human knows exactly what to work on)
**Trigger:** Human says "Work on STEP_X_Y directly" or "Continue STEP_X_Y without scanning"

---

## What This Mode Does

**Same as Mode 1 (Auto-Resume), but skips Step 1 (Locate Effort).**

Human already knows which substep to work on. Go directly to that substep's auto-detection.

---

## Workflow

**Human specifies:**
```
"Work on STEP_1_2 directly"
OR
"Continue STEP_1_2" (with emphasis/clarity that they know which)
```

**Usher does:**
1. Skip scanning (human told us STEP_1_2)
2. Go to Mode 1, Step 2 (Detect AI Phase for STEP_1_2)
3. Execute same as Mode 1 from there

---

## When to Use

**Use Mode 3 when:**
- Human knows exactly which substep to work on (no ambiguity)
- Large Effort is planned (save 30 seconds of scanning)
- Directing Usher explicitly (clarity over automation)

**Use Mode 1 when:**
- Uncertain which Effort is active (let framework scan)
- Multiple Efforts might be in progress (framework picks)
- Want full auto-detection (simpler invocation)

---

## Files Loaded

**Same as Mode 1** (see MODE1_AUTO_RESUME.md for complete context loading).

Difference: Skips effort directory scanning step (human specified STEP_X_Y).

---

## Reference

**See:** MODE1_AUTO_RESUME.md (Workflows A-E)

**This mode is a shortcut to Mode 1, not a separate workflow.**
