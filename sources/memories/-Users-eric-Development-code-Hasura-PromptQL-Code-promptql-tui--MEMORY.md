# promptql-tui Memory

## API Schema Drift (2026-02-14)

The PromptQL/DDN APIs have been removing fields aggressively. Fields removed so far:

- **`ddn_projects.ddn_builds`** — removed from control plane `ddn_projects` type (was nested field for build FQDN)
- **`lookupProject` arguments**: `fqdn` removed
- **`lookupProject` fields**: `buildFqdn`, `consoleUrl`, `ddnProjectId`, `name` all removed

The `lookupProject` query now only returns `projectId`.

Regression test `TestLookup_QueryDoesNotContainRemovedFields` in `internal/sdk/projects_test.go` inspects the actual request body to ensure none of these removed fields/arguments appear.

### Impact on threads
Thread mutations (`startThread`, `sendMessage`) still declare `$buildFqdn: String!` as required. Since no API provides this value anymore, `m.buildFQDN` in the TUI will be empty. This may cause thread creation to fail — watch for it.

## Key Architecture
- SDK client: `internal/sdk/` — GraphQL queries against PromptQL API + DDN control plane
- TUI: `internal/tui/app.go` — Bubble Tea app with views: setup, projects, threads, chat
- Config: `internal/config/` — JSON config at `~/.config/promptql-tui/config.json`
- Test helpers: `internal/sdk/mock_transport_test.go` — `newTestClient`, `graphqlJSON`, `jsonResponse`
