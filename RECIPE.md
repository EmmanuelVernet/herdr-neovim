# LazyVim

Herdr dressed as a LazyVim session: a bufferline of tabs across the top, a
neo-tree style explorer of spaces and a Trouble style agents list on the left,
panes framed like nvim windows with a winbar each, and a lualine at the bottom
whose mode follows the focused pane (INSERT while an agent works or you type at
a shell prompt), and `cmd-shift-p` opens a noice-style cmdline that turns it
COMMAND. Tokyonight moon colors, LazyVim's default, all in JetBrainsMono
Nerd Font.

![LazyVim](mods/lazyvim/preview.png)

## What you see

Top to bottom, on a `chrome` (`#1e2030`) background, no system title bar:

- **Bufferline**, 28px, full width, drags the window. Left padding 78px on
  macOS for the traffic lights (placed at `[12, 8]`). One buffer per tab of the
  active space: a `▍` marker (blue `ansi4` when active, invisible otherwise),
  the program icon, the name (bold when active), then a status sign or a `󰅖`
  close button; a 1px `border` line on its right. The active buffer sits on
  `background` (`#222436`), the rest on `chrome` in `dim`. On the right: a `+`
  (new-menu), then one numbered tabpage per space (active one bold on
  `background`), then window buttons where the system draws none.
- **Body**, a row with a 1px `border` divider:
  - **Sidebar**, left, 300px (160–560), `chrome`:
    - **Source selector**, 26px: three equal tabs `󰉋 Spaces`, `󰉓 Files`,
      `󰊢 Git`; the active one on `background`, blue and bold.
    - **Explorer stack** (weight 3): `Spaces` is a tree. Root row `󰝰 herdr`
      (blue, bold) with a `+` for a new space. Each space is a folder row:
      `├╴`/`└╴` guide (`dim` at 50% alpha), chevron, folder icon (blue, open
      when expanded), name (bold and `foreground` when active, `muted`
      otherwise), machine `󰒋 name` if remote, branch ` name` in magenta
      (`ansi5`), status sign. Under an expanded space, one row per tab with
      `│`/`├╴`/`└╴` guides, program icon, name, pane count when above 1, status
      sign. The active tab of the active space has the `hover` background (the
      cursorline). Rows are 22px, 12.5px text. `Files` and `Git` are Herdr's
      shipped `files` and `changes` mods.
    - **Agents** (weight 2, min 60): a 24px header on `background`
      (`󰚩 Agents`, then counts: ` n` blocked in red, ` n` working in yellow,
      ` n` done in green), then agents grouped by space: a folder row with a
      count pill, then one row per agent: status sign (`󰒲` in `dim` when idle),
      program icon, title, `[tab]` in `dim`. The focused agent has the `hover`
      background. Under each agent, its live sub-agents (`hc run` children,
      nested): `├╴`/`└╴` guides, status sign, icon, title, address in `dim`.
  - **Main**: the active tab's panes, 4px padding around them on `chrome`, 4px
    gap, radius 2, each pane on `background` with a 1px `raised` border; the
    focused pane's border is 1px `accent` (blue). Every pane, even a lone one,
    has a 22px **winbar**: `▍` (in the lualine's mode color when focused,
    invisible otherwise),
    program icon, name (bold when focused), `[Z]` in yellow when zoomed, status
    sign, then the folder as breadcrumbs (`~  code  repo`). The focused
    winbar sits on `background` in `foreground`, the others on `chrome` in `dim`.
- **Lualine**, 24px, full width, powerline arrows (`` ``, 22px glyphs).
  Left: mode block (mode color background, dark `accent_foreground` text, bold),
  branch on `raised` in the mode color, then on `chrome`: `󱉭 space` in cyan,
  agent counts as diagnostics, the focused pane's icon, name and folder. Right:
  ` update` in yellow when an app update is ready, `󰒋 machine` when remote,
  then on `raised`: progress through the space's tabs (`All`, `Top`, `Bot`,
  `n%`) and `space:tab`, then a mode-colored block with ` HH:MM`.
- **Cmdline**, `cmd-shift-p`: a 600px popup 120px from the top, no dimming,
  no Herdr frame. noice's cmdline popup: a 34px box on `background`, rounded 6,
  1px `accent` border, `Cmdline` (11.5px, `accent`) cut into the top border,
  a chevron (`U+F054`) in `accent`, then the input. Under it, blink's completion
  menu: up to 10 rows of 24px on `background`, rounded 4, 1px `accent` border
  like the box; titles on one line, cut off when too long;
  each row a kind icon per group in its own color (spaces a blue `ansi4`
  folder, as in the explorer), the title (matched letters bold in `accent`),
  its key in `dim`, the group in `dim`. The selected row bold on `accent` at
  25% alpha (a theme's `selected` can sit too close to `background`);
  `hover` only lights the other rows, so the pointer never hides the
  selection.
- **Picker**, `cmd-o` (Files) and `cmd-p` (Go to): snacks' picker, a dialog 92% × 86% of the window,
  no Herdr frame, two boxes side by side with a 10px gap, each rounded 6 on
  `background` with a 1px `accent` border and its title (12.5px, bold,
  `accent`) centered in the top border. Left, `Files`: a 32px input row (the
  `U+F054` chevron in `accent`, the input, `shown/total` in `dim`) over a 1px
  `accent` line, then 22px rows: a file icon in its color (mini.icons' look,
  by name then extension), the path with its folders in `dim` and the name in
  `muted` (`foreground` when selected), matched letters bold in `accent`; the
  selected row on `hover`. Right: the selected file's name as title and the
  file read-only with syntax colors and line numbers (Herdr's code editor,
  12.5px); images as the picture; a `dim` note for binary or missing files.
  Under both lists, a 24px key line over a 1px `border` (11.5px, the key in
  `accent`, what it does in `dim`): `enter @ in <agent>` (its program name),
  `ctrl-o <editor>`, `ctrl-v/s split (<terminal editor>)` when the tab has an
  agent, else `enter <editor> (no agent in this tab)` and the split; Go to's `enter go`, `ctrl-n/p move`, `esc
  close`. Go to's rows, while the query is empty: the explorer's tree, its
  `├╴`/`└╴`/`│` guides in `dim` at 50%, a space as a chevron, an open blue
  folder, its bold name, `󰒋 machine`, ` branch` in magenta and its status
  sign; its tabs under it, each with its lead pane's program icon, name, pane
  count when above 1 and status sign. Then the agents (a blue robot,
  `program › title`, status sign, `Agent` in `dim`) and `+ New tab`,
  `+ New space`. While typing: a flat ranked list, tabs as `space › name`,
  each row with its kind icon and the kind in `dim`. `n` entries as the
  count, the title `Go to`. Its preview, titled with the
  entry. A tab or an agent: its panes stacked, 1px `border` between them,
  each a 22px winbar on `chrome` (program icon, bold name, status sign,
  folder in `dim`) over its screen's last lines as plain text (12px, `muted`,
  bottom-aligned, no colors), filling the box; past three panes, 14 lines
  each in a scroll. A space: an overview that scrolls, 10px padding: a line
  with its name (bold), `󰒋 machine`, ` branch` in magenta and its folder in
  `dim`, then one card per tab (rounded 4, 1px `border`, `accent` for the
  shown tab): a 22px header (tab icon, bold name, status sign, `n panes` and
  `· shown` in `dim` on the right) over its panes, 8 lines each.
- **Which-key**, `ctrl-space` (the leader): which-key's helix popup, bottom
  right, 8px from the edge and above the lualine. A 340px box on
  `background`, rounded 6, 1px `accent` border, the path so far
  (`<leader> w`) cut into the top border in `accent`. 22px rows, plain
  mappings first then groups, each alphanumeric: the key in cyan (`ansi6`,
  space as `U+F1050`, tab as `U+F0312`), a `➜` in `dim`, an icon and the
  description in magenta (`ansi5`), groups in blue (`ansi4`) as `+name`.
  Under them, `esc close` (and `bs back` below the top level) in `dim`.
- **Dashboard**, at start, on each new space and on `<leader>D`: snacks'
  dashboard as a 620×560 dialog, rounded 8 on `background`, 1px `accent`
  border, centered: the ANSI Shadow logo spelling `HERDR` with
  LazyVim's `Z z` trail, 14px in blue (`ansi4`), 17px a line; 28px under it,
  420px wide 30px rows (rounded 4, `hover` under the pointer): icon and
  description in cyan (`ansi6`), the key bold in yellow (`ansi3`) on the
  right; then `⚡ Herdr: n spaces · n tabs · n agents working` in cyan.
- **Notifications**: snacks.notifier's compact style inside Herdr's own toast
  frame (Herdr keeps its border, corners and size for toasts, so a thin
  outline of its own stays around): a box inset 6px (9px at the top),
  rounded 6 on `background` (`hover` under the pointer), its 1px border in
  the level's color, error red (`ansi1`, `U+F0159`), warning yellow (`ansi3`,
  `U+F0026`), success green (`ansi2`, `U+F05E0`), info cyan (`ansi6`,
  `U+F02FC`). The level icon (or the agent's own icon) and the bold title,
  12px in that color, are cut into the top border; the body inside in
  `foreground`, 12.5px, one line. A toast without a body shows its title
  there instead.
- **Lazy**, `<leader>l`: lazy.nvim's `:Lazy` as a dialog 80% × 80%, rounded
  6, 1px `accent` border on `background`. A 28px header: `herdr mods` bold on
  `ansi5`, then buttons `Home (H)`, `Check (C)`, `Help (?)` on `raised`
  (rounded 3), the shown one, or Check while checking, on `accent` in
  `accent_foreground`. Then 20px lines: `Total: n mods` (and `checked n/m`)
  bold, then sections `Failed (n)`, `Loaded (n)`, `Not Loaded (n)` in bold,
  each mod indented: a bullet (`●` blue `ansi4` loaded, `○` `dim` not, `✗`
  red `ansi1` failed), its name (`foreground`, `muted` when not loaded, bold
  when selected), a green `✓` (`ansi2`) once it passed a check, its reasons (`󰹘 layout` green
  `ansi2`, `󰌌 keys` yellow `ansi3`, `󰫢 mod` cyan `ansi6`), `⚙ herdr` in
  `dim` for Herdr's own, a failure's first line in red. The selected line on
  `hover`. Enter opens details under it: `dir`, `title`, `from`, `used by`,
  `check` (green passed, red failed), then two buttons on `raised`, `c check`
  and `o open folder`, the key in blue. Help lists the keys. The list
  scrolls, with a scrollbar.
- **Flash**, `cmd-;` (`ctrl-;`): flash.nvim's labels, a bold letter on
  `ansi5` (magenta) in `accent_foreground`, rounded 2, 4px padding: in each
  winbar after the `▍`, in each buffer after its `▍`, before each tabpage's
  number. Nothing else changes on screen.
- **Send context**, `cmd-shift-a` (`ctrl-shift-a`), `<leader>as`: the
  picker's look, a dialog 72% × 66% with two snacks boxes. Left, 2/5 wide,
  titled `Send to <agent>` (`No agent in this tab…` in `dim` without one),
  the sources: per row its number in `dim`, an icon (a green `ansi2`
  terminal for a pane, a magenta `ansi5` git icon for a diff), `Output of
  <pane>` (repeats in one tab numbered `#2`) over its last line that isn't
  a bare prompt (11.5px, `dim`; a pane's row is 38px), or `Git diff` / `Git
  diff (staged)`, and on the right in `dim` `this tab` / `in <tab>` (its
  bufferline name), or the diff's `+20 −3 · 2 files` (`nothing`, `not a
  repo`). The selected row on `hover`, its name bold. Under the list, the
  key line: `enter paste, not sent`, `1-9 pick`, `ctrl-n/p move`, `esc
  close`. Right, titled with the source, the exact text Enter pastes,
  12px in `muted`, scrolling (`Loading…`, `Nothing to send.`); a diff in
  nvim's diff colors: `+` lines green `ansi2`, `-` red `ansi1`, `@@` cyan
  `ansi6`, `diff --git` / `index` / `---` / `+++` bold `foreground`.
  While it's open, each listed pane's winbar shows its row number as a
  flash label, the target agent's a `➜`.
- **Agent inbox**, `cmd-shift-i` (`ctrl-shift-i`), `<leader>ai`: a dialog
  72% × 66%, two boxes side by side, 10px apart, each rounded 6 on
  `background` with a 1px `accent` border, 2 : 3. Left, the agents: a 26px
  title (`Agents`, or `Agents · n need you`, bold `accent`), then 38px rows,
  blocked first, then done, working, idle, then most recent: its sign
  (blocked `U+F057` in `blocked`, done `●` in `done`, working the spinner in
  `working`, idle `U+F04B2` in `dim`), the program name (bold `foreground`
  when selected, else `muted`) and its title in `dim`, under it `space ›
  tab` 11.5px in `dim`; on the right `needs you` in `blocked`, else `done` /
  `working` / `idle` in `dim`. The selected row on `hover`. When it's
  blocked, its numbered choices as buttons on `raised` (rounded 4, the digit
  in blue, the label). The key line: `enter type`, `j/k agent`, `1-9
  choose`, `o go to`, `esc close`. Right, a 26px header (sign, the name bold
  in `accent`, its status, its title, `typing here goes to the agent (esc
  too)` in `dim`) over the agent's own terminal, live, in its own colors.

Names: an agent's program name, a shell's folder name, else the terminal title;
a named tab keeps its name.

## How it behaves

- **Status signs** everywhere: working is a braille spinner (`frames`, 80ms) in
  `working`; blocked is `` in `blocked`; done is `●` in `done` (like a
  modified buffer); idle shows nothing (except `󰒲` in the agents list).
- **Mode**, first match wins: cmdline open `COMMAND` (yellow `ansi3`); then
  from the focused pane: blocked agent `REPLACE`
  (red `ansi1`); working agent or text at a shell prompt `INSERT` (green
  `ansi2`); zoomed pane `VISUAL` (magenta `ansi5`); nvim, vim, helix, nano
  or emacs `CODE` (teal `#4fd6be`); shell or other non-agent
  program `TERMINAL` (cyan `ansi6`); idle agent `NORMAL` (blue `ansi4`).
  Clicking the mode opens the cmdline.
- **Cmdline**: the same entries as Herdr's palette (commands, layouts,
  themes), recent first when empty, fuzzy ranked while typing. Enter runs,
  ↑/↓, `tab`/`shift-tab` and `ctrl-n`/`ctrl-p` move, page up/down jump 10,
  the wheel scrolls, Esc or a click beside it closes. "Go to space or tab…"
  closes it and opens the picker's Go to. "Duplicate mod" turns it into a
  name box (title `Duplicate mod`, a hint under it). Herdr's own picker and
  prompt never open from it.
- **Picker, both sources**: ↑/↓, `tab`/`shift-tab`, `ctrl-n`/`ctrl-p` and
  `ctrl-j`/`ctrl-k` move, page up/down jump a screen, the wheel scrolls, a
  click selects and a second click acts like Enter. Releasing a click
  anywhere but the code preview puts the keyboard back in the input. Esc or a click
  beside it closes. While open, the lualine shows `COMMAND`.
- **Go to**: every space, then its tabs (the explorer's names), then every
  agent (`program › title`), then New tab / New space;
  fuzzy ranked by title, else by branch, tab name or space. The preview
  re-reads the selected entry's terminals every 500ms. Enter selects the
  space or tab, or focuses the agent.
- **Files**: lists the git top of the focused pane's folder (else the folder
  itself): tracked and untracked files, not ignored ones, sorted, recent picks
  first while the query is empty, fuzzy ranked while typing (a match in the
  file name beats one across folders). The preview follows the selection
  40ms after it settles. Enter mentions the file in the tab's agent (the
  focused one, else the first): `@path ` relative to the agent's folder,
  pasted into its prompt and not sent, and focuses it; with no agent in the
  tab, Enter opens it like `ctrl-o`. `@path` is what Claude Code, Codex,
  Gemini CLI and opencode take; another agent gets the same text. `ctrl-o`
  opens the file in the tab's nvim (it focuses that pane), else with
  `$VISUAL` / `$EDITOR` (nvim when unset): a GUI one (`code`, `cursor`, `zed`,
  `subl`…) in its own window, without `-w`; a terminal one in a split to the
  right. `ctrl-v` / `ctrl-s` split right / down with a terminal editor: yours,
  else nvim, vim or vi.
- **Bufferline**: click selects a tab, double-click renames, right-click opens
  the tab menu, `󰅖` closes, scroll wheel goes to the previous/next tab.
  Tabpage click selects the space, right-click opens the space menu.
- **Explorer**: click a space to select it (and expand it); click the active
  space or its chevron to fold it (kept in the mod's `localStorage`). Click a
  tab to show it. Right-click opens the space or tab menu.
- **Agents**: sorted pinned first, then blocked, done, working, idle, then
  start order; this order drives `agent.next` / `agent.prev`. Click focuses the
  agent's pane; clicking a sub-agent peeks it (`terminal.peek`). A sub-agent's
  `error` shows as blocked and its `done` as idle (its parent carries the news).
- **Winbar**: click focuses the pane; on hover, split right, split down,
  zoom/unzoom and close buttons appear on the right.
- The clock refreshes every 15s; everything else re-renders on Herdr's data.
- **Which-key**: Herdr has no key chords, so the leader opens the popup and
  it takes the next keys: a group key goes down a level, backspace up (or
  closes at the top), any other bound key runs and closes. Esc, the leader
  again, a modified key, an unbound key or a click beside the box closes.
  Rows are clickable. LazyVim's leader keys on Herdr: buffers are tabs,
  tabpages are spaces. `<space>` files, `,` Go to, `:` cmdline, `e` sidebar,
  `?` Herdr's keys, `D` the dashboard, `j` flash, `l` lazy; `f` (`f` files, `b` Go to, `n` new tab, `t` terminal),
  `b` (`b` Go to, `d` close, `r` rename, `n`/`p` next/prev), `w` (`-`/`|`
  split, `d` close, `m` zoom, `hjkl` focus, `HJKL` swap), `<tab>` (`<tab>`
  new space, `]`/`[` next/prev, `d` close, `r` rename), `a` (`n`/`p` agent),
  `u` (`l` next layout, `s` settings, `+`/`-`/`=` zoom), `q` (`q` quit).
  Entries whose command this Herdr lacks are hidden.
- **Dashboard**: opens when the layout shows (app start, `layout.switch`)
  and when a new space becomes the shown one; a space made in the background
  doesn't count, and a second one replaces the first. Like snacks, it goes as
  soon as you act: `f` lists the shown space's folder in the picker, `n` a
  new tab, `g` Go to, `c` the picker on `~/.config/herdr-app`, `l` lazy, `q`
  only closes; any other key, Esc or a click beside it closes
  without acting. Rows click. Also in the cmdline as `Dashboard`.
- **Notifications**: every toast, Herdr's own (an agent blocked or done
  while you look elsewhere, errors) and each `notify()`. A click runs its
  action (going to the agent) and closes it; Herdr times them out.
- **Flash**: labels from `asdfghjklqwertyuiopzxcvbnm`, the shown tab's panes
  first, then the space's tabs, then the spaces. Pressing a label focuses
  that pane (`pane.focus`), selects that tab or space; any other key, a
  modified key or a click closes it. Also `<leader>j` and the cmdline.
- **Lazy**: lists every folder in `mods/` with a `main.js`, sorted by name
  in each section. Loaded: the shown layout names it (`mod`, `toast`,
  `terminal_menu` anywhere in `layout()`), a key in a section that applies
  here opens it (`mod.open:<name>` or `<name>.<command>`, not an app
  command), or a loaded mod opens it (`mod: "<name>"` or `name: "<name>"` in
  its `main.js`, two levels deep). `j`/`k`, arrows, `ctrl-n`/`ctrl-p` move,
  page up/down jump 15; the wheel scrolls. A click selects a mod, a
  click on the selected one opens or shuts its details; the header buttons
  and the details' buttons click too. `c` checks the selected mod, `C`
  all (eight at once, in a task of its own so each result redraws), moving
  failures to Failed; `o` closes it and opens the picker on the mod's
  folder; `H` home, `?` help, `q` or Esc close. Also the
  dashboard's `l` and the cmdline's `Lazy: mods`.
- **Send context**: the target is the shown tab's agent (the focused one,
  else the first). Sources: every other terminal pane of the space, this
  tab's first, then the unstaged and staged diff in the agent's folder.
  A click selects (the preview follows); a click on the selected one,
  Enter or `1`–`9` pastes it into the agent's prompt and focuses
  it: a pane as `Output of \`<name>\` in <folder>:` over its last 80 lines
  in a `text` fence; a diff as `\`git diff\` in <folder>:` in a `diff`
  fence, cut at 400 lines with a `… (n more lines)` line. Nothing is sent.
  An empty source says so under the box. `j`/`k`, arrows, `tab`,
  `ctrl-n`/`ctrl-p` move; Esc closes.
- **Agent inbox**: the list has the keyboard when it opens. `j`/`k`, arrows
  or `ctrl-n`/`ctrl-p` select another agent; Enter, `tab`, `→` or `i` move
  the keyboard into its terminal, where everything you type, Esc included,
  goes to the agent; a click on the list takes it back. `1`–`9` on a blocked
  agent press that choice in it (how Claude Code and others pick a dialog
  option) without leaving the list, as its buttons do. `o` closes and
  focuses its pane; `q`, Esc in the list, a click beside it or
  `cmd-shift-i` again close. A click selects, a click on the selected agent
  goes into its terminal. After the picker or cmdline opened over it, the
  list takes the keyboard back.

## Built from

- `layouts/lazyvim.json`: root `column` (`titlebar: "none"`, `theme:
  "lazyvim"`, `toast: "lazyvim-notify"`, `font` and `ui_font` `JetBrainsMono Nerd Font Mono`, loaded
  from `mods/lazyvim/fonts/`,
  `terminal_padding: [4, 8]`) → `tabs` block → `body` row (`sidebar` column:
  `sources` block, `explorer-body` stack of `tree` / `files` / `changes`,
  `trouble` block; `main` tab block with a pane frame and `header`) → `status`
  block.
- `themes/lazyvim.json`: tokyonight moon. Named like the layout, so Settings
  offers it only there; every color is read through `theme()`, so any theme works.
  `solid` / `solid_foreground` (`#82aaff` on `#1b1d2b`) color the primary
  button of Herdr's own dialogs (Confirm in "Close space?"), which can't be
  replaced; `popover`, `raised` and `input` color the rest of them.
- `mods/lazyvim/main.js`: one mod, the piece chosen by `props().role`:
  `bufferline`, `sources`, `explorer`, `trouble`, `lualine`; no role plus a
  `pane` prop is the winbar. Uses `spaces`, `panes`, `agents`, `focused`,
  `layout`, `window`, `updates`, `setAgentOrder`, `openOverlay` (the shipped
  `menu` and `new-menu`), and the shipped `mods/pane/*.svg` icons. Commands:
  `tab.select|rename|close|prev|next`, `space.select|new`, `layout.select`,
  `pane.focus|split|zoom|close`, `terminal.peek`, `mod.open`, `app.update`,
  `window.*`. Reads `shared("lazyvim.cmdline")` for COMMAND.
- `mods/lazyvim-cmdline/main.js`: a restyled copy of Herdr's
  `omarchy-palette` (its entries, fuzzy and recent list). `setShared
  ("lazyvim.cmdline", true)` in `init`, `false` in `async close()`, which
  Herdr calls however the overlay goes. `mod.json` overlay: `kind: "popup"`,
  `at: "top"`, `offset: 120`, 600×300, `frame: "none"`.
- `mods/lazyvim-picker/main.js`: standalone (no other lazyvim mod needed;
  the fuzzy scorer and tab names are copied). `props().source`: `"goto"`, else
  files. Files from `git ls-files -z
  -co --exclude-standard`, else `rg --files --null`, else `find`, capped at
  20000. Preview: `readTextFile` into a readonly `EditorState` (made in a
  task, never in `render`, released on change). Pictures are copied to
  `data/lazyvim-picker/preview/<path cksum>-<mtime>.<ext>` under Herdr's home,
  shrunk to 2048px with `sips` where there is one, and shown with `image()`;
  copies older than 7 days are removed on the next one. The mention: the text goes on the
  clipboard (`pbcopy`, `wl-copy` or `xclip`, PowerShell's `Set-Clipboard`),
  then `pane.focus` and `terminal.paste`. Go to: `places()` from `spaces()`,
  `panes()` and `agents()`, ranked again on each render, screens from
  `hc read <terminal>` on a 500ms timer.
  Opening in the tab's nvim: `hc get <terminal>` gives the foreground pid,
  a `sh` loop finds `nvim.<pid>.0` (or its child's) under
  `$TMPDIR/nvim.$USER/*/` or `$XDG_RUNTIME_DIR`, then `nvim --server <socket>
  --remote <file>`; on any failure, `pane.split {argv: ["nvim", file]}`.
  Recent picks per repo in `localStorage`. `setShared("lazyvim.cmdline")` like
  the cmdline. `mod.json` overlay: `kind: "dialog"`, 0.92×0.86, `frame: "none"`.
- `mods/lazyvim-whichkey/main.js`: the leader keys as a nested `SPEC`
  (`[key, desc, icon, command | function | group]`). `mod.json` overlay:
  `kind: "popup"`, `at: "bottom"`, 1×1 of the window, `frame: "none"`; the
  mod draws the box bottom right and closes on a press beside it.
- `mods/lazyvim-dashboard/main.js`: `mod.json` overlay `kind: "dialog"`,
  620×560, `frame: "none"`; `mod.open` from which-key and the cmdline. The
  lualine opens it with `openOverlay` (`mod.open` again would close it) in
  `init`, and from a 400ms timer comparing `spaces()` ids. It closes itself
  before acting, so the picker opens over the window. Opens the picker with
  `props: {root}`: the picker lists that folder instead of the focused
  pane's.
- `mods/lazyvim-notify/main.js`: named by the layout root's `"toast":
  "lazyvim-notify"`, so other layouts keep Herdr's toast. Reads `props()`:
  `{title, body, level, icon, action, overlay}`. A toast's `mod.json` overlay
  (size, `frame`) is ignored: Herdr frames and sizes it, so the mod insets
  its box in that frame, `flex_1` (not `size_full`, which overflows the
  padding and cuts the bottom border), the title inside the frame's top.
- `mods/lazyvim-lazy/main.js`: `mod.json` overlay `kind: "dialog"`,
  0.8×0.8, `frame: "none"`. Herdr's own mods from the keys of
  `installed.json`; the folder list from one `sh` loop; references from
  `grep -ohE` over the loaded mods' `main.js`; a title read when its details
  first open. Check: `herdr-app check <dir>` through `sh` with
  `~/.local/bin` added to `PATH`. The list is an
  `overflow_y_scrollbar` with a `ScrollHandle` (`scroll_to_item` on each
  move, `release()` in `close()`).
- `mods/lazyvim-inbox/main.js`: three roles. No role (`mod.open` from the
  key, `mod.json` overlay a 1×1 `popup` at the top, `frame: "none"`,
  `focusable: true`): closes itself, then opens the dialog, or closes it
  when `shared("lazyvim.inbox")` holds an open one. The dialog is
  `openOverlay({ kind: "dialog", 0.72×0.66, frame: "none", layout })`: a
  `row` (gap 10) of a `list` block (weight 2) and a column (weight 3) of a
  26px `header` block over `{ terminal: <address> }` (padding `[2, 8]`).
  A terminal block is fixed when the overlay opens, so selecting another
  agent opens a new dialog, then closes the old one. The list's `async
  close()` clears `lazyvim.inbox` only if it still names its own overlay.
  `nextCommand()` `"focus"` and a press on the list refocus it. Choices from
  one `hc read` when a blocked agent's dialog opens: the last 15 lines
  matching `1. …` / `❯ 2) …` (box borders allowed). Digits through `hc
  keys`; into the terminal with `pane.focus {terminal}`.
- `mods/lazyvim-context/main.js`: `mod.json` overlay `kind: "dialog"`,
  0.72×0.66, `frame: "none"`. Pane text from
  `hc read <terminal> --lines 80`, its `[hc] …` notes and trailing blank
  lines dropped; each source's text built once, when first selected, and
  reused by Enter; diffs from
  `git diff [--staged]` in the agent's `cwd`, their hints from
  `--shortstat`. The winbar badges go through
  `shared("lazyvim.flash")`, cleared in `async close()`. Pasted like the
  picker's mention: clipboard, `pane.focus`,
  `terminal.paste`, all in a task started before `dismiss()`.
- `mods/lazyvim-flash/main.js`: an invisible popup (`mod.json` overlay
  `kind: "popup"`, `at: "top"`, 1×1, `frame: "none"`) that takes the keys.
  It writes `shared("lazyvim.flash")` = `{ <pane, tab or space id>: letter }`
  in `init`, `null` in `async close()`; the lazyvim mod's `flashLabel()` draws
  them, and the lualine resets it when it starts.
- `keys.json`: `"layout:lazyvim": { "cmd-shift-p": "mod.open:lazyvim-cmdline",
  "cmd-p": "lazyvim.goto", "ctrl-shift-p": "mod.open:lazyvim-cmdline",
  "ctrl-shift-o": "lazyvim.goto", "cmd-o": "mod.open:lazyvim-picker",
  "ctrl-shift-e": "mod.open:lazyvim-picker",
  "ctrl-space": "mod.open:lazyvim-whichkey",
  "cmd-;": "mod.open:lazyvim-flash", "ctrl-;": "mod.open:lazyvim-flash",
  "cmd-shift-a": "mod.open:lazyvim-context", "ctrl-shift-a": "mod.open:lazyvim-context",
  "cmd-shift-i": "mod.open:lazyvim-inbox", "ctrl-shift-i": "mod.open:lazyvim-inbox" }`
  (the `ctrl-shift` pair for Linux and Windows; `ctrl-p` belongs to the
  shell), so other layouts keep Herdr's palette and picker.
  `lazyvim.goto` reaches the lualine's `nextCommand()`, which opens the
  picker with `openOverlay({ props: { source: "goto" } })`. `mod.open` can't
  pass props, hence the relay.
- `mods/lazyvim/insert.zsh`: zsh hooks (`line-init`, `line-pre-redraw`,
  `preexec`) that set the terminal title to `lv:insert` while the prompt has
  text, the folder when empty, the command while it runs. Only inside Herdr
  terminals (`$HC_TERMINAL_SOCKET`).

## Watch out

- The font ships in `mods/lazyvim/fonts/` (JetBrainsMono Nerd Font Mono
  Regular and Bold, about 2.3 MB each, with `OFL.txt`, which the license
  requires next to it). Herdr loads a mod's `fonts/` at start and on the next
  look change, so a fresh install shows it after `layout.switch`. No italic
  file: italics come from an installed copy, if any.
- Shell INSERT needs `source ~/.config/herdr-app/mods/lazyvim/insert.zsh` at
  the end of `~/.zshrc`, and a new shell. zsh only. Herdr can't see keystrokes,
  and an OSC 7501 report would turn the shell into an agent, hence the title.
- COMMAND only works with this cmdline: mods can't tell when Herdr's own
  palette (`app.palette`) is open, hence the replacement.
- Shared state is saved to disk: the lualine resets `lazyvim.cmdline` when it
  starts, or a crash with the cmdline open would leave COMMAND showing.
- The cmdline uses the terminal `background`, not `popover`: a theme file
  without `popover` (`tokyo-night-storm.json`, say) gets a lighter one derived
  by Herdr, and a layout's `colors` can't point it at another color name (hex
  only), so Herdr's own popups keep the derived one.
- The terminal find bar (`cmd-f`) is Herdr's own: no mod or layout key
  restyles it, and `terminal.search` takes no query, so a mod can't stand in.
- Don't name a method `close` for closing the overlay: that's Herdr's cleanup
  hook. The cmdline uses `dismiss()`.
- `done` turns `idle` once its pane is looked at, so it never shows as a mode.
- Read props with `props()`, not `init`'s first argument.
- Sub-agents without a pane aren't in `agents()`: walk `terminals()` by
  `parent` (live only). An agent's in-process helpers (Claude Code's own
  subagents) aren't terminals and never show.
- Tab numbers in the tabpages are positions, not names.
- Files: finish the nvim lookup before closing the overlay. Its tasks stop
  once it closes, so the open runs first and `dismiss()` comes last.
- Files: the code editor has no scroll-to-line, so a grep picker couldn't
  show the match in place; this one previews from the top.
- Picker: `image()` reads only paths under Herdr's home (absolute and `../`
  paths show nothing), hence the copy into `data/`. A space on another
  machine gets no image preview.
- Picker: Herdr keeps every image it decodes until it quits (in memory and
  as a GPU texture): a 5120×2880 PNG is 56 MB decoded. A new file name per
  look grew the app past 1.4 GB; one name per picture version, shrunk,
  keeps it to one small copy each.
- Picker: the input lets go of the keyboard on any press beside it, so the
  focus comes back on mouse up (on mouse down, the input's own blur wins).
- Picker: `hc keys` types named keys only (no `@`, `/` or `.`) and `hc send`
  always presses Enter, so a mention goes through the clipboard: it replaces
  what was copied.
- Picker: a mod can't draw a live terminal, and an overlay's `{terminal}`
  block is fixed when it opens, so Go to previews `hc read` text, not the
  terminal itself.
- Picker: the input keeps `ctrl-e` (end of line) and `ctrl-a` for itself,
  and a mod can't catch a key before it, hence `ctrl-o` to open.
- Picker: `sign()` is null for idle; pass it through `children(opt(...))`,
  `.child(null)` throws.
- Dashboard: a key it doesn't bind closes it but doesn't reach the shell
  (`hc keys` types named keys only); the first keystroke goes to it.
- Dashboard: saving any lazyvim file reloads the lualine, which opens it.
- Dashboard: `line_height()` takes rems, not px: the logo lines get a
  fixed `h(17)` instead.
- Which-key: `ctrl-space` on macOS also switches input source when several
  are set up (System Settings › Keyboard › Shortcuts). In zsh it was
  set-mark, now taken in this layout.
- Flash: mods aren't told where panes are drawn, so labels sit in the pieces
  that draw each target, not over the terminals.
- Lazy: `herdr-app shot` returns the last frame Herdr painted, and an
  overlay that changes with no window event isn't repainted in it: take two
  shots, or wait for an event, before judging a "Loading…".

- Lazy: no times next to mods. Unlike lazy.nvim's load times, `herdr-app
  check` takes 0.4–0.6s for any mod (mostly its own start-up, eight at once),
  and Herdr doesn't report a mod's load or draw cost.

- Send context: the paste replaces what was on the clipboard, like the
  picker's mention.
- Agent inbox: a terminal has one size; while the dialog shows it, the
  agent reflows to the dialog's size (its own pane too), and back when it
  closes, like `terminal.peek`.
- Agent inbox: Esc typed into the terminal goes to the agent (Claude Code
  stops what it's doing); close from the list, or with `cmd-shift-i`.
- Agent inbox: `hc read` gives text without colors; the first version drew
  that and polled it. The terminal block is live and native instead.

## Done when

- `herdr-app check ~/.config/herdr-app/mods/lazyvim` passes and `herdr-app
  status` shows no errors after `layout.switch {name: "lazyvim"}`.
- Each role draws its own piece (not five lualines).
- Focusing another pane moves the blue border and the lit winbar.
- `printf '\e]7501;state=blocked\a'` in a shell turns the mode `REPLACE`;
  typing at a prompt (with `insert.zsh` sourced) turns it `INSERT`, `ctrl+u`
  back to `TERMINAL`; zooming the pane shows `VISUAL`.
- `cmd-shift-p` opens the cmdline and the lualine shows `COMMAND`; Esc, a
  click beside it, or running an entry brings the old mode back.
- Clicking `Files` / `Git` swaps the explorer for the shipped panels.
- `cmd-o` opens the file picker on the focused pane's repo; typing `main`
  ranks the `main.js` files first; selecting `preview.png` shows the picture;
  Enter in a tab with Claude Code leaves `@path ` in its prompt, in a tab with
  no agent opens the file; `ctrl-o` with nvim in the tab opens the file
  there, without one opens it with `$EDITOR` (VS Code in its window for
  `EDITOR=code`).
- `cmd-p` opens Go to as the explorer's tree; moving through it shows a
  space's tabs as cards and a tab's or agent's panes with their current
  text; Enter goes there. Clicking the preview, then the list, keeps the
  arrows working.
- `ctrl-space` shows the which-key box bottom right; `w` lists the window
  keys with `<leader> w` as title, `bs` goes back, `|` splits right and
  closes it; Esc or `ctrl-space` again closes it.
- `layout.switch {name: "lazyvim"}` and `space.new` show the dashboard:
  the HERDR logo, six keys and the counts; `f` opens the picker on the
  space's folder, `c` on `~/.config/herdr-app`, `x` just closes it;
  `<leader>D` brings it back.
- A shell in a tab you aren't looking at running
  `printf '\e]7501;state=blocked\a'` posts `An agent needs you` bottom right
  in a red bordered box, the title in its
  border; clicking it goes to that tab.
- `cmd-;` shows a magenta letter in every winbar, buffer and tabpage;
  pressing a pane's letter focuses it, a tabpage's selects that space, Esc
  clears them all.
- `<leader>l` lists 100-odd mods with the lazyvim ones Loaded; `C` checks
  them all, a `✓` on each, and a broken one moves to Failed; Enter on a mod shows
  its folder and title; `o` opens that folder in the picker.
- In a tab with Claude Code and a shell that just ran a failing command,
  `cmd-shift-a` shows `1` on the shell's winbar and `➜` on Claude's;
  `1` leaves `Output of …` and the shell's last lines in
  a fence in Claude's prompt, unsent; `Git diff` shows `+n −n · n files`
  and pastes the diff.
- With Claude Code asking permission in another tab, `cmd-shift-i` lists it
  first as `needs you`, its terminal live on the right and `1 Yes` / `2 …`
  as buttons; `1` answers it and its status moves on; Enter, typing a
  message and Enter sends it; `j` shows the next agent; after `cmd-o` and
  Esc the arrows still move the list.
