# Neovim

Minimal Neovim for prose, Markdown, YAML and JSON: one config file, no plugins, no IDE layer.
Keys and learning path: [cheatsheets/neovim.md](../cheatsheets/neovim.md).

- [templates/init.lua](../templates/init.lua) is the whole config; it sets only non-defaults.
- [scripts/install-dotfiles.sh](../scripts/install-dotfiles.sh) links it to `~/.config/nvim/init.lua`.
- Distributions (kickstart, LazyVim, NvChad, AstroNvim) ship LSP and completion machinery
  that text editing never uses.

## Prerequisites

- Ubuntu 24.04+ or Debian 13+: apt ships Neovim 0.10 or newer. Debian 12 ships 0.7 — too old.
- The handbook cloned and [`install.sh`](../install.sh) run — [bootstrap.md](bootstrap.md#new-dev-machine).
- A desktop clipboard needs `wl-clipboard` (Wayland) or `xclip` (X11).
  Over SSH, Neovim uses OSC 52 by itself when the terminal supports it.

## Steps

1. **Install.** Name the clipboard tool in the same command; alone, apt satisfies the
   `xclip | xsel | wl-clipboard` recommendation with X11 `xclip`.

   ```bash
   sudo apt install neovim wl-clipboard   # desktop
   sudo apt install neovim                # server: no tool, OSC 52 over SSH
   ```

2. **Link the config.** `install.sh` is idempotent; re-run it when the clone predates the link.

   ```bash
   ./install.sh                           # from the handbook clone
   ```

3. **Check the providers.** A desktop lists `wl-copy`; a server reports no tool, which is expected.

   ```bash
   nvim +'checkhealth vim.provider'
   ```

4. **Start the tutorial.** It is interactive: an exercise flips from ✗ to ✓ when done.

   ```bash
   nvim +Tutor
   ```

## German keyboard

The `de` layout puts `[ ] { } /` behind AltGr or Shift; `^` and the backtick are dead keys.
The config keeps the layout and remaps the free umlaut keys — the table is in the
[cheatsheet](../cheatsheets/neovim.md#german-keyboard-xkb-de).

- `'langmap'` translates the umlaut keys for built-in commands and text objects (`di[`).
- The keymaps cover mapped commands such as `[<Space>`; `remap = true` makes them reach.
- `f`, `t`, `r` and marks still take the literal umlaut; Insert mode is untouched.
- Dead keys stay dead: use `0` or `_` for `^`, `'a` for a mark, `Ctrl-6` for `Ctrl-^`.

Alternative — switch the layout to **German (US)**: the US layout with umlauts on AltGr+u/o/a
and eszett on AltGr+s. Every Vim key then sits in its US position, dead keys included.

```bash
gsettings set org.gnome.desktop.input-sources sources "[('xkb','de+us'),('xkb','de')]"   # Super+Space toggles
gsettings set org.gnome.desktop.input-sources sources "[('xkb','de')]"                    # revert
```

Sources: [`:help 'langmap'`](https://neovim.io/doc/user/options.html#'langmap'),
[`:help CTRL-^`](https://neovim.io/doc/user/editing.html#CTRL-%5E),
[Vim Tips Wiki: map extra keys on non-US keyboards](https://web.archive.org/web/2023/https://vim.fandom.com/wiki/Map_extra_keys_on_non_US_keyboards).

## Plugins

Later, one `git clone` each into Neovim's package path — no plugin manager
([`:help packages`](https://neovim.io/doc/user/repeat.html#packages)).
The config calls `setup()` for each one it finds.

```bash
P=~/.local/share/nvim/site/pack/plugins/start
git clone https://github.com/tris203/precognition.nvim "$P/precognition.nvim"   # motion hints
git clone https://github.com/MunifTanjim/nui.nvim      "$P/nui.nvim"            # hardtime dependency
git clone https://github.com/m4xshen/hardtime.nvim     "$P/hardtime.nvim"       # blocks key repeats

git -C "$P/precognition.nvim" pull                                              # update
```

## Verify

```bash
readlink -f ~/.config/nvim/init.lua                                  # → <clone>/templates/init.lua
nvim --headless -c 'lua print(vim.o.shiftwidth, vim.o.clipboard)' -c q   # → 2 unnamedplus (desktop) / 2 (server)
nvim +'checkhealth vim.provider'                                     # Clipboard: wl-copy (desktop)
```
