# KYC POV Datagen — Project Memory

## Architecture Decisions
- **3-database split**: `kyc_entity_registry` (who), `kyc_compliance` (safe?), `kyc_monitoring` (audit trail) — mirrors real financial compliance infra. Cross-DB FKs become SQL comments; reference tables (`source_systems`, `countries`) replicated in all 3. Schema JSON v2.0 has `databases` section + per-table `database` field.
- **Schema files**: `schema_entity_registry.sql`, `schema_compliance.sql`, `schema_monitoring.sql` — old monolithic `schema.sql` deleted
- **Cross-DB FK pattern**: Columns keep UUID values + get indexed, but FK constraints become comments documenting target DB. Format: `-- Cross-database reference: table.col -> target_db.target_table.col`
- **CLI flags**: Both `create_postgres_schema.py` and `insert_data.py` support `--all` (default) and `--database <name>` for single-DB operation
- **Modular generators**: Split into `scripts/generators/` with one file per schema tier (base.py, reference_data.py, entities.py, fragmentation.py, kyc_lifecycle.py, monitoring.py) — avoids monolithic file that headless Claude can't manage across steps
- **Seed + expansion for company names**: `company_seeds.json` (~500 entries) + `expand_company_names.py` → `company_names.json` (~3,200 entries) — too large for single-pass LLM generation
- **Duplicate entity strategy**: `duplicate_entity_map.json` defines ~200 golden entities with 2-3 variant names each — no DB link between variants (that's what mastering discovers)
- **Countries in geo_data.json**: The `countries` DB table is generated from the `countries` section of `geo_data.json` — no separate asset file needed
- **Temporal constraints**: Formalized in `kyc_schema.json` under `temporal_constraints.kyc_lifecycle` — generators read these to enforce timestamp ordering

## Ralph Executor Notes
- Steps 1-8 (asset files) use `--model sonnet`, steps 9+ (code) use `--model opus`
- Prompt includes full asset file listing so each step knows what's available
- 20 total steps (up from 16) — the extra steps come from splitting the generator into separate files

## Key Files
- `plan.md` — master architecture doc
- `docs/interview-answers.md` — requirements from user interview
- `scripts/ralph/steps.json` — 20 execution steps
- `scripts/ralph/ralph.sh` — autonomous executor with model pinning
- `assets/kyc_schema.json` — single source of truth (v2.0, includes `databases` section)
- `schema_entity_registry.sql` / `schema_compliance.sql` / `schema_monitoring.sql` — 3 DDL files
- `scripts/create_postgres_schema.py` — generates DDL (supports `--all` / `--database`)
- `scripts/insert_data.py` — bulk loader (supports `--all` / `-d`)
