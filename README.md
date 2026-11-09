# herdr-neovim

A LazyVim look for the [Herdr](https://herdr.dev) app: bufferline tabs, a
neo-tree explorer of spaces, a Trouble-style agents list, nvim-style window
bars, a lualine whose mode follows the focused pane and a noice-style cmdline
on `cmd-shift-p` (`ctrl-shift-p` on Linux and Windows).

![LazyVim layout](preview.png)

## Demo

https://github.com/user-attachments/assets/59c5c430-b5ca-4858-a29c-6eb278b876ea

## Install

Ask your agent to add `herdr.dev/layouts/EmmanuelVernet/herdr-neovim`, or by hand:

```sh
git clone https://github.com/EmmanuelVernet/herdr-neovim
cd herdr-neovim
cp layouts/lazyvim.json ~/.config/herdr-app/layouts/
cp themes/lazyvim.json ~/.config/herdr-app/themes/
cp -r mods/lazyvim mods/lazyvim-cmdline ~/.config/herdr-app/mods/
herdr-app do layout.switch --name lazyvim
```

Then merge `keys.json` into `~/.config/herdr-app/keys.json` (add its
`layout:lazyvim` section), in this layout only:

| | macOS | Linux, Windows |
|---|---|---|
| cmdline | `cmd-shift-p` | `ctrl-shift-p` |
| Go to (spaces and tabs) | `cmd-p` | `ctrl-shift-o` |

`ctrl-p` stays with the shell (previous command), hence `ctrl-shift-o`.

No font to install: `mods/lazyvim/fonts/` ships JetBrainsMono Nerd Font Mono
(Regular and Bold, [SIL OFL](mods/lazyvim/fonts/OFL.txt)), loaded by Herdr when
the layout shows. Italics come from an installed
[JetBrainsMono Nerd Font](https://www.nerdfonts.com/font-downloads) if you have
one.

Optional, zsh only: show INSERT in lualine while you type at a shell prompt.

```sh
echo 'source ~/.config/herdr-app/mods/lazyvim/insert.zsh' >> ~/.zshrc
```

## Modes

| Focused pane | Mode |
|---|---|
| cmdline open | COMMAND |
| agent blocked (needs you) | REPLACE |
| agent working, or typing at a shell prompt | INSERT |
| pane zoomed | VISUAL |
| nvim, vim, helix, nano or emacs | CODE |
| shell or other program | TERMINAL |
| idle agent | NORMAL |

`ctrl-shift-l` cycles back to your other layouts. See [RECIPE.md](RECIPE.md)
for the full build brief.
