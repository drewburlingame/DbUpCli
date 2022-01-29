# DbUpCli
A console app for DbUp with additional safe guards to avoid developer errors.

Goals:
 
- [ ] **Support Manifest file for RunOnce migrations**
Provides merge conflict check when two different branches have RunOnce scripts.

- [ ] **Only run RunAlways scripts if they've changed, using checksum**

- [ ] **Throw error if the contents of a migration have changed, using checksum**

- [ ] **Throw error if a migration is inserted with a lower version than current**
- this migration wouldn't run and we should be warned
- option to ignore
- option to force

- [ ] **Dev environment commands**
- Drop
- Clear
- Reset (Drop and Run all migrations)

Strech goals: 
- Snapshot 
- Restore

- [ ] **MultiFolder with config file per folder**
Enables running groups of RunOnce and RunAlways migrations, in an order that matters for the migrations

01_Schemas
- .dbup.config { Run = Always, OnlyIfChanged = true }
- 001_ensure_schemas.sql
- 002_ensure_roles.sql
 
02_Tables
- .dbup.config { Run = Once, ErrorIfChanged = false, ErrorIfInserts = true }
- .dbup.manifest [ v--1_add_users.sql ]
- 001_add_users.sql
 
03_VerifyTables
- .dbup.config { Run = Always, OnlyIfChanged = false }
- 001_users_tests.sql
 
04_Sprocs
- .dbup.config { Run = Always, OnlyIfChanged = true }
- 001_sp_users_add.sql
- 002_sp_users_delete.sql

05_SeedData
- .dbup.config { Run = Always, OnlyIfChanged = true }
- 001_ensure_user_roles.sql
- 002_ensure_countries.sql

06_DataUpdates
- .dbup.config { Run = Once, ErrorIfChanged = false, ErrorIfInserts = true, NewTransaction = true }
- .dbup.manifest
- 001_fix_departments.sql
