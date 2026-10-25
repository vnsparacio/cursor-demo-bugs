# Changelog

> **Sample data, fictional.** Built for a Notion demo. Not Cursor's real release history. Commit shas are invented and do not resolve. Format: `<sha>`: what was fixed and why (issue, Jira key).

## 3.4.2 (2026-10-20)

No fixes tracked in this repository.

## 3.4.1 (2026-10-06)

### Auth/Billing
- `9c41e7a`: **SSO sign-in loop after SAML signing certificate rotation.** The IdP metadata, including the signing certificate, was cached at configuration time and never refreshed. Signature validation now re-fetches the metadata once on failure and retries. Orgs pinned to 3.3.x still hit the loop. (#1, CUR-1371)

### Agent
- `e19c6d4`: **Auto-run allowlist bypassed by chained shell commands.** Only the first token of a command line was checked, so `git checkout -- .`, `git clean -fd` or `git reset --hard` chained with `&&` or `;` after an allowlisted command ran without approval. Commands are now split on shell operators and each segment is checked. Not changed: "Run everything" mode. (#4, CUR-1247)

### Background agents
- `7c30d9e`: **Background agent hangs on "Starting environment" with npm E401 against a private registry.** Repository secrets were not exposed to the `.npmrc` copied during setup, so `${NPM_TOKEN}` expanded to an empty string, and 401/403 responses were retried until the 10-minute environment timeout. Secrets are now injected before `npm install`, and registry auth errors fail fast with the registry host in the message. (#6, CUR-1290)

### Extensions
- `0b9d7e2`: **Python debugger fails to attach with a uv-created virtualenv.** Since 3.3.7 the debug adapter loaded `debugpy` from the workspace interpreter, which `uv` environments do not seed. The adapter now always uses the bundled `debugpy`. (#8, CUR-1337)

## 3.4.0 (2026-09-22)

### Tab
- `5d2b8f1`: **Tab completions stop after laptop sleep/resume in Remote-WSL.** The completion websocket was not re-established after resume, so Tab wrote to a dead socket without an error. The client now reconnects with exponential backoff and warns in the status bar if it cannot. Local and Remote-WSL only. (#2, CUR-1204)

### Indexing/Codebase
- `b7e03a9`: **Indexing stuck at 98% in monorepos: `.cursorignore` directory patterns ignored for nested folders.** Patterns with a trailing slash were anchored to the repository root, so `services/*/gen/` never matched. `.cursorignore` now follows gitignore semantics for directory patterns. (#3, CUR-1233)

### Agent, Editor
- `2a8f5c3`: **Agent edits the wrong file when two open files share a name across split editor groups.** The edit target was resolved from the tab label (basename) and the first match won. It is now resolved by file URI, preferring the focused editor group. Not covered: same-named tabs in the same editor group. (#5, CUR-1268)

### Integrations
- `4f6a1b8`: **Agent ends the turn with no message after an MCP tool call returns multiple content blocks.** The tool-result handler stopped after the first content block. All text blocks are now concatenated and returned to the model. (#7, CUR-1311)
