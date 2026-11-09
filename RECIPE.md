# LazyVim

Herdr dressed as a LazyVim session: a bufferline of tabs across the top, a
neo-tree style explorer of spaces and a Trouble style agents list on the left,
panes framed like nvim windows with a winbar each, and a lualine at the bottom
whose mode follows the focused pane (INSERT while an agent works or you type at
a shell prompt), and `cmd-shift-p` opens a noice-style cmdline that turns it
COMMAND. Tokyonight moon colors, LazyVim's default, all in JetBrainsMono
Nerd Font.

![LazyVim](preview.png)

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
  turns the same popup into a list of spaces and their tabs (title `Go to`);
  Tabs carry the explorer's names (`space › name`; an unnamed tab is its lead
  pane's agent or folder). "Duplicate mod" turns it into a name box (title `Duplicate mod`, a hint
  under it). Herdr's own picker and prompt never open from it. `cmd-p` opens
  it straight on `Go to` (with New tab / New space at the end).
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

## Built from

- `layouts/lazyvim.json`: root `column` (`titlebar: "none"`, `theme:
  "lazyvim"`, `font` and `ui_font` `JetBrainsMono Nerd Font Mono`, loaded
  from `mods/lazyvim/fonts/`,
  `terminal_padding: [4, 8]`) → `tabs` block → `body` row (`sidebar` column:
  `sources` block, `explorer-body` stack of `tree` / `files` / `changes`,
  `trouble` block; `main` tab block with a pane frame and `header`) → `status`
  block.
- `themes/lazyvim.json`: tokyonight moon. Named like the layout, so Settings
  offers it only there; every color is read through `theme()`, so any theme works.
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
- `keys.json`: `"layout:lazyvim": { "cmd-shift-p": "mod.open:lazyvim-cmdline",
  "cmd-p": "lazyvim.goto", "ctrl-shift-p": "mod.open:lazyvim-cmdline",
  "ctrl-shift-o": "lazyvim.goto" }`
  (the `ctrl-shift` pair for Linux and Windows; `ctrl-p` belongs to the
  shell), so other layouts keep Herdr's palette and picker.
  `lazyvim.goto` reaches the lualine's `nextCommand()`: it sets
  `shared("lazyvim.goto")` and opens the cmdline, which starts on `Go to` and
  clears the flag. `mod.open` can't pass props, hence the relay.
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
