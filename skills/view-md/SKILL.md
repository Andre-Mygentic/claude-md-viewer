---
name: view-md
description: /view-md — Open a markdown file in the Vollkorn viewer
---

# /view-md — Open a markdown file in the Vollkorn viewer

Launch the local viewer server for a markdown file. It opens the browser itself.

## Usage

`/view-md <file>` or `/view-md` (uses most recently mentioned .md file)

## Steps

1. Resolve the file to an absolute path. With no argument, use the most recently created or
   mentioned `.md` file in the conversation.

2. Launch it with Bash `run_in_background: true` (not `&`, which the harness may kill):
   ```bash
   view-md /absolute/path/to/file.md
   ```
   If `view-md` is not found, run the source directly and re-link it for next time:
   ```bash
   node ~/code/md-view/index.js /absolute/path/to/file.md
   (cd ~/code/md-view && npm link)
   ```

3. Confirm with a single line: `Opened in viewer: <filename>`

## Do NOT

- **Never `npx md-view` or `npx view-md`.** Neither name on npm is this tool: `md-view` is an
  unrelated package that fails (`marked: command not found`), and `view-md` 404s. This viewer is
  not published; its source is `~/code/md-view` (package `claude-md-viewer`, bin `view-md`).
- **Never run `open` on the URL.** The server already opens the browser; a second `open` spawns a
  duplicate tab.

## Notes

- Live-reloads when the file changes on disk — no need to reopen after edits.
- Each invocation starts a new server on the next free port from 7337.
