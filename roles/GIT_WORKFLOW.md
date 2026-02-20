# Git Workflow - Branching, Commits, Merging, Rollback

**Purpose:** Definitive git procedures for ATLAS Efforts
**Audience:** AI3 (primarily), all roles (reference)
**Status:** v1.0

---

## ⚠️ CUSTOMIZE THIS FILE TO MATCH YOUR EXACT WORKFLOW

**This file shows ONE git workflow example.** You MUST edit it to match your team's process.

**What to customize:**
- **Branching strategy:** This shows `staging → effort → staging → main`. Your team might use trunk-based (no staging), gitflow (develop/release/hotfix), or custom branches
- **PR requirements:** Edit merge commands to match YOUR approval process (1 approval? 2? CI must pass? Specific reviewers?)
- **Deployment gates:** When can code go to production? Who approves? What validations required?
- **Commit conventions:** Conventional commits? Ticket numbers? Signed commits?
- **Protected branches:** Which branches are protected in YOUR repo?

**Example customizations:**
- Trunk-based team: Remove all `staging` references, branch directly from `main`
- Enterprise team: Add compliance sign-off step before production merge
- Solo founder: Simplify to `feature → main` (no staging needed)

**Edit every git command in this file to match YOUR exact workflow. AI3 will follow these commands precisely.**

---

## Overview

This document defines **exact git procedures** for working with ATLAS Efforts.

**Key Principles (EXAMPLE - customize for your workflow):**
1. Branch from `staging` (not `main`)
2. Commit frequently with clear messages
3. Test before every commit
4. Merge to `staging` for validation
5. PR `staging → main` (human approval)
6. Never force push to protected branches

---

## Branch Structure

```
main (production - protected)
  ↑ PR (human approval only)
staging (pre-production - working branch)
  ↑ direct merge (AI3)
effort/STEP_X_Y_NAME (feature branch - per Effort)
```

**Branch Purposes:**
- **`main`**: Production code only. Deploys to live sites.
- **`staging`**: Pre-production testing. Deploys to staging.vercel.app
- **`effort/*`**: Working branches for specific Efforts. Auto-preview on Vercel.

---

## Starting New Effort

**When:** Beginning work on a new Effort (usually CP1)

**Steps:**

```bash
# 1. Ensure local staging is up to date
git checkout staging
git pull origin staging

# 2. Create effort branch FROM staging
git checkout -b effort/STEP_X_Y_SHORTNAME

# Example:
git checkout -b effort/STEP_1_2_SECOND_CUSTOMER

# 3. Verify branch
git branch
# Should show: * effort/STEP_1_2_SECOND_CUSTOMER

# 4. Initial commit (if creating new directory)
mkdir -p customers/second-customer-name
cd customers/second-customer-name
# [Create initial files]

git add .
git commit -m "[STEP_1_2] Initial scaffolding"

# 5. Push to remote
git push origin effort/STEP_1_2_SECOND_CUSTOMER

# Vercel will auto-deploy preview:
# URL: step-1-2-second-customer-abc123.vercel.app
```

**Result:** Effort branch exists, ready for implementation.

---

## Continuing Existing Effort

**When:** Starting work on CP2+ (effort branch already exists)

**Steps:**

```bash
# 1. Checkout effort branch
git checkout effort/STEP_1_2_SECOND_CUSTOMER

# 2. Pull latest changes (in case of updates)
git pull origin effort/STEP_1_2_SECOND_CUSTOMER

# 3. Optionally merge staging (get any staging updates)
git pull origin staging
# Resolve conflicts if any

# 4. Continue working
```

---

## During Implementation (Frequent Commits)

**Philosophy:** Commit often, not once at the end.

**Commit Cycle:**

```bash
# 1. Implement feature/component
[Write code]

# 2. Test locally (REQUIRED before commit)
npm run build   # Must succeed
npm test        # All must pass
npm run lint    # No errors

# Manual test
npm run dev
# Check feature works in browser

# 3. If tests pass, commit
git add .
# Or specific files:
git add customers/second-customer/components/Hero.tsx

git commit -m "[STEP_1_2] CP1 - add Hero component"

# 4. Push to effort branch
git push origin effort/STEP_1_2_SECOND_CUSTOMER

# 5. Repeat for next feature
```

---

## Commit Message Convention

**Format:**
```
[EFFORT_NAME] CPX - description
```

**Components:**
- `[EFFORT_NAME]`: e.g., `[STEP_1_2]` (identifies which Effort)
- `CPX`: e.g., `CP1`, `CP2` (identifies which Checkpoint)
- `description`: What this commit does (imperative mood)

**Examples:**

```bash
# During CP work
git commit -m "[STEP_1_2] CP1 - add Hero component"
git commit -m "[STEP_1_2] CP1 - add Services grid with pricing"
git commit -m "[STEP_1_2] CP1 - implement contact form validation"

# CP complete
git commit -m "[STEP_1_2] CP1 complete - design system implemented"

# Fixes
git commit -m "[STEP_1_2] CP1 - fix mobile responsive layout"
git commit -m "[STEP_1_2] CP2 - fix accessibility violations in form"

# Effort complete
git commit -m "[STEP_1_2] COMPLETE - site deployed and validated"
```

**Benefits:**
- Git log is scannable
- Easy to find CP boundaries
- Clear project history

---

## Checkpoint Complete (Merge to Staging)

**When:** CP is fully implemented, tested locally, ready for staging validation

**Steps:**

```bash
# 1. Ensure effort branch has all commits
git checkout effort/STEP_1_2_SECOND_CUSTOMER
git status  # Should be clean (nothing uncommitted)

# 2. Pull staging to get any updates
git pull origin staging
# Resolve conflicts if any
git push origin effort/STEP_1_2_SECOND_CUSTOMER

# 3. Switch to staging
git checkout staging
git pull origin staging

# 4. Merge effort branch (no fast-forward)
git merge effort/STEP_1_2_SECOND_CUSTOMER --no-ff \
  -m "Merge STEP_1_2 CP1: Design system complete"

# Why --no-ff?
# Creates merge commit (preserves Effort boundary in history)
# Easy to revert entire Effort if needed

# 5. Push staging
git push origin staging

# 6. Wait for Vercel deployment (~2 min)
# Check: https://vercel.com/dashboard
# Or staging URL: staging.yourdomain.com

# 7. Test on staging
# - Visit staging URL
# - Full manual test (all features)
# - Check mobile + desktop
# - Verify performance
# - Test all forms/interactions

# 8. If issues found:
# - Go back to effort branch
# - Fix issues
# - Re-merge to staging
# - Re-test

# 9. If staging passes:
# - Report to human
# - Ready for production (or next CP)
```

---

## Production Deployment (PR to Main)

**Who:** Human only (AI3 does NOT merge to main)

**When:** After staging validation passes

**Steps (Human Executes):**

```bash
# Option A: Via GitHub Pull Request (Recommended)
# 1. Go to GitHub repo
# 2. Create PR: staging → main
# 3. Title: "[STEP_1_2] Launch second customer site"
# 4. Description:
#    - What's being deployed
#    - What was tested
#    - Any DB migrations needed
# 5. Review code
# 6. Approve and merge
# 7. Verify production deployment

# Option B: Via Git Command Line
# 1. Checkout main
git checkout main
git pull origin main

# 2. Merge staging
git merge staging --no-ff -m "Deploy STEP_1_2: Second customer site"

# 3. Push to main
git push origin main

# 4. Verify production deployment
# Check Vercel dashboard
# Visit production URL
# Smoke test critical paths
```

---

## Branch Cleanup (After Production)

**When:** After effort is merged to main and deployed

**Steps:**

```bash
# 1. Delete local branch
git branch -d effort/STEP_1_2_SECOND_CUSTOMER

# 2. Delete remote branch
git push origin --delete effort/STEP_1_2_SECOND_CUSTOMER

# Optional: Keep effort branch for reference
# Don't delete if you might need to reference implementation history
```

---

## Rollback Scenarios

### **Scenario 1: Rollback Commit (Within Effort Branch)**

**When:** Single commit on effort branch is bad

```bash
# 1. Find problematic commit
git log --oneline
# Example output:
# abc1234 [STEP_1_2] CP1 - bad feature (THIS ONE)
# def5678 [STEP_1_2] CP1 - good feature

# 2. Revert specific commit
git revert abc1234

# 3. Push
git push origin effort/STEP_1_2_SECOND_CUSTOMER

# Result: Commit is undone, history preserved
```

---

### **Scenario 2: Rollback to Previous CP (Effort Branch)**

**When:** Entire CP needs to be undone

```bash
# 1. Find CP complete commit
git log --oneline
# Find: def5678 [STEP_1_2] CP1 complete

# 2. Reset to that commit (DESTRUCTIVE)
git reset --hard def5678

# 3. Force push (OK for effort branch, NOT for staging/main)
git push origin effort/STEP_1_2_SECOND_CUSTOMER --force

# Result: All commits after CP1 are gone
# WARNING: Only do this if no one else is working on this branch
```

---

### **Scenario 3: Rollback Staging Merge**

**When:** Staging deployment is broken after merge

```bash
# Option A: Revert the merge (safer)
git checkout staging
git log --oneline
# Find merge commit: abc1234 Merge STEP_1_2 CP1

git revert -m 1 abc1234
# -m 1 = keep staging history (parent 1)

git push origin staging

# Result: Merge is undone, staging works again

# Option B: Reset staging (DESTRUCTIVE)
git checkout staging
git reset --hard HEAD~1  # Remove last merge
git push origin staging --force

# Result: Merge is gone
# WARNING: Use only if Option A doesn't work
```

---

### **Scenario 4: Rollback Production (Emergency)**

**Who:** Human only

**When:** Production is broken after merge

```bash
# Option A: Revert via Git
git checkout main
git log --oneline
# Find merge: abc1234 Deploy STEP_1_2

git revert -m 1 abc1234
git push origin main

# Vercel redeploys (~2 min)
# Production restored

# Option B: Vercel Instant Rollback (Faster)
# 1. Go to Vercel dashboard
# 2. Deployments tab
# 3. Find previous working deployment
# 4. Click "Promote to Production"
# Result: Instant rollback (no git needed)
```

---

## Database Migrations

**When:** Implementation requires database schema changes

**Workflow:**

```bash
# 1. Create migration file BEFORE implementing code
mkdir -p migrations
touch migrations/2025-12-20_add_booking_table.sql

# 2. Write up/down migrations
cat > migrations/2025-12-20_add_booking_table.sql << 'EOF'
-- Up migration
CREATE TABLE bookings (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  customer_id UUID REFERENCES customers(id),
  appointment_date TIMESTAMP NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Down migration (for rollback)
-- DROP TABLE bookings;
EOF

# 3. Document in migrations/MIGRATIONS_LOG.md
# See format in MIGRATIONS_LOG.md template

# 4. Commit migration file
git add migrations/
git commit -m "[STEP_1_2] CP2 - add bookings table migration"
git push origin effort/STEP_1_2_SECOND_CUSTOMER

# 5. Implement code that uses new table

# 6. After staging validation, human applies migration
# Human runs:
psql $DATABASE_URL < migrations/2025-12-20_add_booking_table.sql

# 7. Human updates MIGRATIONS_LOG.md to mark as applied

# 8. If rollback needed:
psql $DATABASE_URL -c "DROP TABLE bookings;"
```

**Important:**
- Migrations are MANUAL for now (no auto-migration)
- Always write down migration (rollback strategy)
- Test locally first if possible

---

## Protected Branch Rules

### **Main Branch**

**Protection:**
- ✅ Require pull request before merging
- ✅ Require status checks (build, tests)
- ✅ Require human approval
- ❌ No force pushes (EVER)
- ✅ Require signed commits (optional but recommended)

**Who can merge:** Human only

**How to merge:** PR from staging → main

---

### **Staging Branch**

**Protection:**
- ❌ No PR required (AI3 merges directly)
- ⚠️ Force push ALLOWED but dangerous
- ✅ Should require status checks (build, tests)

**Who can merge:** AI3 or Human

**How to merge:** Direct merge from effort branch

---

### **Effort Branches**

**Protection:** None needed

**Who can work:** AI3 (usually single author)

**Cleanup:** Delete after merge to main

---

## Common Git Commands Quick Reference

### **Branch Management**
```bash
# List branches
git branch -a

# Create branch
git checkout -b effort/STEP_X_Y

# Switch branch
git checkout staging

# Delete local branch
git branch -d effort/STEP_X_Y

# Delete remote branch
git push origin --delete effort/STEP_X_Y
```

### **Syncing**
```bash
# Pull latest
git pull origin staging

# Pull and merge
git pull origin staging --rebase

# Push
git push origin effort/STEP_X_Y
```

### **Committing**
```bash
# Add files
git add .
git add specific/file.ts

# Commit
git commit -m "[STEP_X_Y] CP1 - description"

# Amend last commit (if not pushed)
git commit --amend -m "new message"
```

### **Merging**
```bash
# Merge with merge commit
git merge effort/STEP_X_Y --no-ff -m "Merge message"

# Merge and take all changes from other branch
git merge -X theirs effort/STEP_X_Y
```

### **History**
```bash
# View log
git log --oneline

# View log with graph
git log --graph --oneline --all

# View changes in commit
git show abc1234

# View file history
git log --oneline -- path/to/file.ts
```

### **Undoing**
```bash
# Undo uncommitted changes
git checkout -- file.ts

# Undo last commit (keep changes)
git reset HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert commit (safe)
git revert abc1234
```

---

## Troubleshooting

### **Problem: Merge Conflict**

**Solution:**
```bash
# 1. When conflict occurs
git merge effort/STEP_X_Y
# CONFLICT in file.ts

# 2. Open conflicted file, look for:
<<<<<<< HEAD
(staging version)
=======
(effort branch version)
>>>>>>> effort/STEP_X_Y

# 3. Edit file to resolve
# Keep what you want, delete markers

# 4. Mark as resolved
git add file.ts

# 5. Complete merge
git commit -m "Merge STEP_X_Y: resolved conflicts in file.ts"
```

---

### **Problem: Pushed Bad Commit**

**Solution:**
```bash
# If on effort branch (safe to force push)
git reset --hard HEAD~1
git push origin effort/STEP_X_Y --force

# If on staging (use revert instead)
git revert HEAD
git push origin staging
```

---

### **Problem: Accidentally Committed to Wrong Branch**

**Solution:**
```bash
# 1. Note commit hash
git log --oneline  # Find: abc1234

# 2. Switch to correct branch
git checkout effort/STEP_X_Y

# 3. Cherry-pick commit
git cherry-pick abc1234

# 4. Go back to wrong branch
git checkout wrong-branch

# 5. Remove commit from wrong branch
git reset --hard HEAD~1
```

---

### **Problem: Need to Update Effort Branch with Staging Changes**

**Solution:**
```bash
# 1. Checkout effort branch
git checkout effort/STEP_X_Y

# 2. Pull staging
git pull origin staging

# 3. Resolve conflicts if any

# 4. Push updated effort branch
git push origin effort/STEP_X_Y
```

---

## Verification Checklist

**Before pushing:**
- [ ] `npm run build` succeeds
- [ ] `npm test` passes
- [ ] `npm run lint` clean
- [ ] Commit message follows convention
- [ ] On correct branch

**Before merging to staging:**
- [ ] All CP tasks complete
- [ ] Effort branch pushed
- [ ] Local tests pass
- [ ] Success criteria met

**Before PR to main:**
- [ ] Staging validation complete
- [ ] Customer approval (if applicable)
- [ ] DB migrations documented
- [ ] No known blockers

---

## Best Practices

**✅ DO:**
- Commit frequently (after each logical change)
- Test before every commit
- Use clear commit messages
- Merge staging regularly (keep effort branch up to date)
- Ask for help if git issues arise

**❌ DON'T:**
- Force push to main or staging (without very good reason)
- Commit untested code
- Use vague commit messages ("fix stuff")
- Let effort branch get stale (weeks behind staging)
- Panic - git can undo almost anything

---

## Related Documentation

- `AI3_IMPLEMENTER_GUIDE.md` - Implementation workflow
- `AI3_DEVELOPER_BEST_PRACTICES.md` - Code quality standards
- `migrations/MIGRATIONS_LOG.md` - Database migration tracking

---

**Git is powerful and safe when used correctly. Follow these procedures and you'll be fine.** 📦
