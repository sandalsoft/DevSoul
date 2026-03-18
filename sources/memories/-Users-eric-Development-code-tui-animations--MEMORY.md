# pql Project Learnings

## PromptQL API
- **v2 API format**: No `llm` field, no `ddn.url`. DDN config only has `headers` map + optional `build_id`/`build_version`.
- **Endpoint**: `https://api.promptql.pro.hasura.io/query` with `Authorization: Bearer {key}` header.
- **v2 SSE chunks**: `assistant_action_chunk` has fields: `type`, `index`, `message`, `plan`, `code`, `code_output`, `code_error`.
- **Reference implementations**: `github.com/hasura/promptql-ui` (v1 Next.js app), `github.com/hasura/promptql-python-sdk` (official SDK with v1+v2).
- `.env` has PROMPTQL_API_KEY, PROMPTQL_DDN_URL (DDN URL not needed for v2).

## Bubble Tea / Charmbracelet
- `bubbles/textarea` with Height=1 inside lipgloss borders causes ANSI control character leakage due to internal viewport rendering. Use `bubbles/textinput` for single-line inputs instead.
- `lipgloss.JoinHorizontal` with ANSI-heavy content (textarea viewport output) breaks width calculations.
- Sidebar component starts with `visible: false` — use `SetVisible(true)` in model init if you want it shown by default.

## Architecture
- Go Bubble Tea app: `cmd/pql/main.go` → `internal/ui/model.go` (root model) → `internal/ui/components/` (sidebar, chatview, inputbar, topbar)
- API: `internal/api/promptql.go` — SSE streaming client
- Config: `internal/config/config.go` — env vars + CLI flags
