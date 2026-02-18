# Database Migrations Log

**Purpose:** Track all database schema changes with up/down scripts for rollback
**Status:** Living document (update with every migration)
**Critical:** EVERY database change must be logged here

---

## Migration Philosophy

**Core principles:**
1. **Every change is tracked** - No ad-hoc schema changes
2. **Every change is reversible** - Always write down migration
3. **Migrations are manual** - No auto-execution (too risky)
4. **Test before applying** - Validate on local/staging first
5. **Document thoroughly** - Future you needs context

---

## Migration Workflow

### **Step 1: Plan Migration (During CP1 or CP2)**

```bash
# When you identify need for database change:

# 1. Create migration file
touch migrations/YYYY-MM-DD_descriptive_name.sql

# Example:
touch migrations/2025-12-20_add_bookings_table.sql
```

---

### **Step 2: Write Up/Down Scripts**

```sql
-- migrations/YYYY-MM-DD_example_migration.sql

-- ================================================
-- UP: Apply Migration
-- ================================================

CREATE TABLE example_table (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  name TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- ================================================
-- DOWN: Rollback Migration
-- ================================================

DROP TABLE IF EXISTS example_table;
```

---

### **Step 3: Test on Local/Staging**

```bash
# Test UP migration
psql $DATABASE_URL -f migrations/YYYY-MM-DD_example_migration.sql

# Verify it worked
psql $DATABASE_URL -c "\d example_table"

# Test DOWN migration
psql $DATABASE_URL -c "DROP TABLE IF EXISTS example_table;"
```

---

### **Step 4: Document in This Log**

Add entry below with:
- Date and description
- Link to migration file
- Status (planned/applied staging/applied production)
- Any notes or issues

---

## Migration Log

(Entries added as migrations are created and applied)

---
