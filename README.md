# cursor-demo-bugs

> **Sample data, fictional.** Built for a Notion demo. This is not Cursor's real code, issues or release history. Every issue, person, Jira key (`CUR-xxxx`), version number and commit sha here is invented.

## What this repo is

A small, read-only sandbox of **past, already-fixed bugs** for a Notion Custom Agent demo (a bug triage agent). When a new bug report comes in, the agent searches this repo for related past issues and fixes, and links up to three of them in the triage brief. This repo is that history.

- **Closed issues** are the past bugs. Each has a component label, a severity label (`P0` to `P3`), the Jira key in the body, and a closing comment in the form `Fixed in <version> by <sha>: <root cause>`.
- **[`CHANGELOG.md`](CHANGELOG.md)** lists the same fixes by release and references the issues by number, so code search finds them too.
- **Labels**: one per component (`Tab`, `Agent`, `Editor`, `Indexing/Codebase`, `Background agents`, `Extensions`, `Auth/Billing`, `Integrations`), severity `P0` to `P3`, `bug` and `regression`.

## Notes

- There is no source code here. Commit shas in the issues and the changelog are made up and do not resolve.
- The fictional world: `3.4.2` is the current stable (2026-10-20), `3.4.1` the previous one, `3.3.9` the last 3.3 release.
- Nothing in this repo should be read as a statement about how any real product works.
