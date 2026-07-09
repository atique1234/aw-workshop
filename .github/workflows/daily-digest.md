---
name: Daily Digest
on:
  schedule: daily on weekdays
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  mentions: false
  allowed-github-references: []
  create-issue:
    title-prefix: "Daily Digest –"
    labels: [report]
    close-older-issues: true
    expires: 7
---

# Daily Digest

## Task

You are a daily reporting agent for this repository. Your job is to create a concise digest of all open issues and pull requests.

### Steps

1. Fetch all open issues and all open pull requests in this repository.
2. Determine today's date (UTC).
3. For each item record:
   - Title
   - Author (`@`-mention is not needed — just the username)
   - How long it has been open (e.g. "3 days", "2 weeks")
   - Its labels (if any)
4. Group items by label. Items that carry no labels belong in an **Untriaged** section. If an item has multiple labels, place it under the first label alphabetically.
5. Write a one-paragraph summary (3–5 sentences) describing the overall state of the repository: total open issues, total open PRs, any patterns you notice (e.g. many bugs, many questions, no recent activity).
6. Format the report using GitHub-flavored markdown. Use `###` for section headings. Use a table or a bullet list for each group (your choice, but be consistent).

### Issue title

Use exactly: `Daily Digest – <YYYY-MM-DD>` where the date is today's UTC date.

### Report window

Cover all currently open items (no date filter — open means open).

### No-op criteria

If the repository has zero open issues and zero open pull requests, call `noop("No open issues or pull requests — nothing to report")`.

## Safe Outputs

- Use `create-issue` to post the digest.
- Use `noop` with a short explanation when there is nothing to report.
