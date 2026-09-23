# Wishlist board

A single-file, drag-and-drop priority board (Backlog / In Progress / Blocked / Done). No build step, no server — just open `index.html` in a browser.

## Using it

Copy `index.html` anywhere (locally, a shared drive, an internal static host) and open it. Each person's items are saved in their own browser's `localStorage`, scoped to wherever the file is served from:

- Two people opening the *same file* from *different locations/copies* (or on different machines) never see each other's items.
- If you host it at one shared URL, everyone hits the same origin, so `localStorage` is still per-browser/per-device — not shared between viewers of that URL either.
- There is no backend and no sync between people. To move your board to a new machine or browser, you'd need to export/import manually (not built in yet).

The board starts empty for everyone — no pre-filled example items.
