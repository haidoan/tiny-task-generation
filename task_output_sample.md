<!--
  task.md — managed by task.html quick-add tool.
  LLM instructions:
    - Work ONLY on tasks where `status: inprogress`.
    - Skip tasks with `status: todo` (not started) or `status: done`.
    - When you finish a task, change its `status:` from `inprogress` to
      `done` in this file. Leave the rest of the stanza unchanged.
    - The user refers to tasks by their `index:` (e.g. "work on task 3" =
      the stanza with `index: 3`). Indices are positional (1..N, top-down)
      and renumber whenever tasks are added/removed/reordered.
    - Each task is a YAML stanza separated by `---`. Fields:
        index:        1-based position. Authoritative reference for the user.
        name:         single-line task title
        status:       one of: todo | inprogress | done
        description:  free-form text. May be empty, single-line, or a `|` block.
        metadata:     free-form text. May be empty, single-line, or a `|` block.
    - For multi-line values the `|` block scalar is used and content is
      indented by 2 spaces. Content inside `|` is preserved verbatim,
      including code fences and nested lists.
    - Anything outside a stanza (and not inside this HTML comment) is commentary.
-->

index: 1
name: Task1
status: done
description:
metadata:

---

index: 2
name: Task2
status: inprogress
description: |
  Implement user registration API at @user.controller.ts
metadata:

---

index: 3
name: Task3
status: inprogress
description:
metadata:
