# Wishlist board

A single-file, drag-and-drop priority board (Backlog / In Progress / Blocked / Done). No build step, no server — just open `index.html` in a browser.

## Using it

Copy `index.html` anywhere (locally, a shared drive, an internal static host) and open it. Each person's items are saved in their own browser's `localStorage`, scoped to wherever the file is served from:

- Two people opening the *same file* from *different locations/copies* (or on different machines) never see each other's items.
- If you host it at one shared URL, everyone hits the same origin, so `localStorage` is still per-browser/per-device — not shared between viewers of that URL either.
- There is no backend and no sync between people. To move your board to a new machine or browser, you'd need to export/import manually (not built in yet).

The board starts empty for everyone — no pre-filled example items.

## Importing your Jira tickets

The board can't talk to Jira directly (no backend, and Jira Cloud doesn't allow browser calls from arbitrary origins). Instead, use your own Claude Code session (with your own Atlassian MCP connection) to fetch your tickets and write them to a file, then load that file into the board:

1. Ask your Claude: *"Fetch my assigned, unresolved Jira tickets and write them to `jira-import.json` next to this board's `index.html`, as a JSON array of `{key, title, status, urgency}` objects."*
   - `status` can be Jira's own wording (e.g. "In Progress", "To Do") — the importer maps common values to the board's columns (Backlog / In Progress / Blocked / Done).
   - `urgency` can be Jira's priority wording (Highest/High/Medium/Low/Lowest) — mapped to High/Medium/Low, or omit it to leave urgency unset.
2. In the board, click **Import from file** and select `jira-import.json`.
3. Re-running the import later updates existing cards in place (matched by ticket key) instead of duplicating them — so it's safe to re-import after your tickets change.

This only touches your own browser's local data — nothing is uploaded or shared with anyone else.
