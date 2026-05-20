# Jira Integration

## Project

- **Key:** `PBT`
- **Board:** https://procyoncreative.atlassian.net/jira/software/c/projects/PBT/boards/267
- **REST API base:** https://procyoncreative.atlassian.net/rest/api/3

## Board columns

The PBT board uses the Software Simplified Workflow: **Backlog → In Progress → Done**. There is no QA / Code Review column yet, so the GitHub workflow only transitions to **Done** on PR merge (no QA transition on PR open).

To add a QA column later: open the PBT board → **⋯ → Board settings → Columns → + Add column**, name it `QA`. Then add a `jira-transition-qa` job to `.github/workflows/jira.yml` mirroring the `jira-transition-done` job, with `TARGET_COLUMN=QA`.

## MCP Server

- **Server:** `procyon_atlassian` (SSE) — registered in `.mcp.json`
- **URL:** https://mcp.atlassian.com/v1/sse
- Tools available as `mcp__procyon_atlassian__*` once Claude Code re-loads the project.
- **Note:** Atlassian's HTTP+SSE transport is being deprecated 2026-06-30. The replacement endpoint is `https://mcp.atlassian.com/v1/mcp` (Streamable HTTP). Update before that date.

## Auth

- **Email:** set as the `JIRA_EMAIL` repo secret.
- **API token:** generate at https://id.atlassian.com/manage-profile/security/api-tokens
- `JIRA_API_TOKEN` is required as a repo secret. Never commit it. For local scripts, source it from `.env` (gitignored).
- `JIRA_BASE_URL` repo secret: `https://procyoncreative.atlassian.net`

## Workflow Rules

- **No work without a ticket.** Every branch must reference a `PBT-NNN` Jira ticket. If one doesn't exist, create it first via `/jira-ticket create`.
- **Branch name format:** `PBT-NNN-short-description` (e.g. `PBT-1-jira-setup-and-scaffold`).
- **Ticket requirements:**
  - **Hours estimate** in `timetracking.originalEstimate` (`30m`, `2h`, `1d`).
  - **Acceptance Criteria** including the mandatory line: `Use Red/Green TDD`.
- **PR merge → ticket moves to Done.** Handled automatically by `.github/workflows/jira.yml`.

## CI Workflow

The `.github/workflows/jira.yml` action:

1. On PR open / synchronize / reopen / close: syncs ticket metadata (comment, labels) onto the PR via [`procyon-creative/jira-action-man@v2`](https://github.com/procyon-creative/jira-action-man).
2. On PR merge: transitions any referenced ticket to `Done`.

## Quick reference

- Create / edit a ticket via Claude: `/jira-ticket`
- Set up a new project: `/jira-setup <PROJECT_KEY>`
