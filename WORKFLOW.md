# A day with herdr-neovim

One pass through a working session with agents, in the order you'd meet each
feature. Keys are macOS first, Linux and Windows in brackets. `<leader>` is
`ctrl-space`: press it, and a box at the bottom right lists what comes next.

## 1. Open Herdr

The **dashboard** greets you: `f` find a file, `n` new tab, `g` go to a space
or tab, `c` your Herdr config, `l` the mods list. Any other key closes it and
leaves you in the shell.

What's on screen:

- **Bufferline** (top): this space's tabs. On the right, one number per space.
- **Explorer** (left): spaces as folders, their tabs under them. `Files` and
  `Git` swap it for a file tree or the changed files.
- **Agents** (bottom left): every agent, the ones that need you first.
- **Lualine** (bottom): the mode of the focused pane. `INSERT` while an agent
  works or you type at a prompt, `REPLACE` when one is blocked on you, `CODE`
  in an editor, `NORMAL` for an idle agent.

## 2. Set up a task

1. `<leader>` `tab` `tab` opens a new space for the task (the dashboard shows
   again; `x` to dismiss it).
2. Start your agent in it: `claude`, `codex`, whatever you use.
3. `<leader>` `w` `|` splits a shell beside it for tests and git.

`<leader>` `w` then `h`/`j`/`k`/`l` moves between panes, `m` zooms one.

## 3. Get around

- `cmd-p` (`ctrl-shift-o`): **Go to**. Every space, tab and agent as a tree,
  with a live preview of their screens. Type to filter.
- `cmd-;` (`ctrl-;`): **Flash**. A letter on every pane, tab and space; press
  it to jump there.
- `cmd-shift-p` (`ctrl-shift-p`): the **cmdline**, every command Herdr has,
  fuzzy matched. The lualine shows `COMMAND` while it's open.

## 4. Give the agent context

- `cmd-o` (`ctrl-shift-e`): **Files**, with a preview. Enter puts `@path` in
  the tab's agent prompt (not sent), `ctrl-o` opens the file in your editor
  (the tab's nvim if there is one), `ctrl-v` / `ctrl-s` split it open.
- `cmd-shift-a` (`ctrl-shift-a`): **Send context**. A test failed in the shell
  beside it? Pick `Output of <shell>`, check the preview on the right, Enter:
  the output lands in the agent's prompt in a fence, unsent, ready for your
  question. Same for `Git diff` and `Git diff (staged)`. While it's open, the
  panes it lists show their number on their winbar, the target agent a `➜`.

## 5. While agents work

Go do something else. When an agent finishes or needs you somewhere you
aren't looking, a **notification** comes in, in the level's color; click it
to go there. The Agents list and the lualine keep count.

## 6. Answer them

`cmd-shift-i` (`ctrl-shift-i`): the **agent inbox**. Every agent, the ones
that need you first, and the selected one's terminal live beside the list.

- `j` / `k`: next or previous agent.
- `1`–`9`: answer a blocked agent's numbered choice ("1. Yes") without
  leaving the list.
- Enter: type straight into its terminal; click the list to come back.
- `o`: go to its tab. `cmd-shift-i` again closes the inbox.

With three agents running, this is the loop: `cmd-shift-i`, answer, `j`,
answer, close.

## 7. Review what they did

- The explorer's `Git` source lists the changed files.
- `cmd-shift-a` then `Git diff (staged)` hands the diff back to an agent for a
  review pass.
- `cmd-o`, `ctrl-o` opens a file in your editor to finish it yourself.

## 8. Keep it healthy

- `<leader>` `l` (or `l` on the dashboard): the **mods list**, lazy.nvim
  style. What's loaded and why (the layout, a key, another mod). `C` checks
  every mod still loads, which is worth doing after a Herdr update.
- `<leader>` `?`: every key Herdr knows.
- `ctrl-shift-l` switches back to your other layouts.

## Cheat sheet

| What | macOS | Linux, Windows | Leader |
|---|---|---|---|
| Leader (which-key) | `ctrl-space` | `ctrl-space` | |
| Find files | `cmd-o` | `ctrl-shift-e` | `<leader>` `space` |
| Go to space, tab, agent | `cmd-p` | `ctrl-shift-o` | `<leader>` `,` |
| Cmdline | `cmd-shift-p` | `ctrl-shift-p` | `<leader>` `:` |
| Flash jump | `cmd-;` | `ctrl-;` | `<leader>` `j` |
| Send context to agent | `cmd-shift-a` | `ctrl-shift-a` | `<leader>` `a` `s` |
| Agent inbox | `cmd-shift-i` | `ctrl-shift-i` | `<leader>` `a` `i` |
| Next / previous agent | `cmd-]` / `cmd-[` | | `<leader>` `a` `n` / `p` |
| New space | | | `<leader>` `tab` `tab` |
| Split right / down | | | `<leader>` `w` `\|` / `-` |
| Toggle sidebar | | | `<leader>` `e` |
| Dashboard | | | `<leader>` `D` |
| Mods list | | | `<leader>` `l` |
