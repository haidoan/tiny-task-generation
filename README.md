# task.html

A single-file, keyboard-driven task tracker that stores tasks in a
plain-text Markdown file (`task.md`) you can read with any editor — or
hand to an LLM as input.

No server. No build step. No `node_modules`. One HTML file, one data
file, in any modern Chromium browser.

![Task list view](images/task_list.png)

## Highlights

- **100% keyboard navigation** — every action (add, move, view, toggle
  status, delete) has a single-key shortcut. Mouse optional.
- **100% local** — your tasks live in a `task.md` on your own disk.
  No account, no server, no cloud sync, no telemetry. The browser
  talks directly to the file via the File System Access API.
- **LLM-friendly** — `task.md` is YAML stanzas with a self-describing
  header that tells any LLM how to read the format and which tasks to
  act on. Built for the "capture in the UI, let Claude do the work"
  loop.

## Where the idea came from

I kept catching myself sending Claude a stream of small, related
prompts: "fix X", "also rename Y", "and update Z". Each one was its
own round-trip — me typing, Claude re-loading context, both of us
paying the switching cost.

`task.html` is the answer to that: dump every small task into the
list in seconds (it's just `N` + type + `Enter`), mark the ones you
want done, and then hand the whole batch to Claude in a single
prompt — *"read `task.md` and work through everything marked
`inprogress`"*. One conversation, many tasks done.

## Why

Most task apps either lock your data into a proprietary store or
need a server to sync. `task.html` is a ~30 KB local file that talks
directly to a `task.md` on your disk through the
[File System Access API](https://developer.mozilla.org/docs/Web/API/File_System_Access_API),
so:

- Your tasks live in a file you fully own.
- You can `cat`, `grep`, `git diff`, and version-control them.
- An LLM can read `task.md` directly — the file's header explicitly
  documents the format and which tasks the LLM should act on.

## Quick start

1. Download `task.html` (just the single file).
2. Open it in **Chrome, Edge, Arc, Brave, or any Chromium-based
   browser**. Safari and Firefox are **not** supported (they don't yet
   expose the File System Access API).
3. Click **Open task.md** and either pick an existing file or create a
   new one. The file handle is remembered in IndexedDB so the same
   file reopens on subsequent visits (you'll be asked once per browser
   session to re-grant permission).
4. Start adding tasks — press `N`, type, hit `Enter`.

## Keyboard shortcuts

### List view

| Key                | Action                                   |
| ------------------ | ---------------------------------------- |
| `N`                | Focus the quick-add input                |
| `J` / `K` / arrows | Move focus up / down                     |
| `Enter`            | Open the focused task                    |
| `Space`            | Cycle status (todo → in-progress → done) |
| `Backspace`        | Remove focused task (asks to confirm)    |
| `Esc`              | Cancel / blur the input                  |

### Inside the quick-add input

| Key     | Action                              |
| ------- | ----------------------------------- |
| `Enter` | Add the typed task to the bottom    |
| `Esc`   | Clear and unfocus                   |

### Inside the edit modal

![Task detail / edit modal](images/task_detail.png)

| Key             | Action                                       |
| --------------- | -------------------------------------------- |
| `Tab`           | Move between Name / Description / Metadata / Status |
| `Space`         | Cycle status (when focus is on the button, not a text field) |
| `⌘Enter` / `Enter` outside a textarea | Save and close         |
| `Esc`           | Close without saving                         |

Edits in the modal autosave to disk after ~600 ms of inactivity.

## File format (`task.md`)

Each task is a YAML stanza, separated by `---`. The format is chosen
to be compact and unambiguous for LLMs:

```yaml
index: 1
name: Buy milk
status: inprogress
description: |
  Pick up 2L whole milk.
  ```sh
  echo "code fences are fine inside descriptions"
  ```
metadata: |
  - due: today
  - priority: low

---

## License

MIT (replace this with your preferred license before publishing).
