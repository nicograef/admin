# Neovim

Config: [templates/init.lua](../templates/init.lua). Setup: [guides/neovim.md](../guides/neovim.md).
Built-in tutorial: `nvim +Tutor` — interactive, an exercise flips from ✗ to ✓ when done.

## Survival

| Key                  | Action                                                        |
| -------------------- | ------------------------------------------------------------- |
| `Esc`                | Back to Normal mode — when in doubt, press it                 |
| `i` / `a` / `o`      | Insert before the cursor / after it / on a new line below     |
| `:w` / `:q` / `:wq`  | Save / quit / save and quit                                   |
| `:q!`                | Quit and discard changes                                      |
| `u` / `Ctrl-r`       | Undo / redo                                                   |
| `.`                  | Repeat the last change                                        |
| `:help <topic>`      | Open help; inside it `K` follows the tag under the cursor, `gO` lists its sections |

## Moving

Relative line numbers show the count: `7j` jumps to the line labelled 7.

| Key                 | Action                                                    |
| ------------------- | --------------------------------------------------------- |
| `h` `j` `k` `l`     | Left, down, up, right                                     |
| `w` / `b` / `e`     | Next word start / previous word start / word end          |
| `0` / `_` / `$`     | Line start / first non-blank / line end                   |
| `{` / `}`           | Previous / next paragraph                                 |
| `gg` / `G`          | File start / end                                          |
| `Ctrl-d` / `Ctrl-u` | Half a page down / up                                     |
| `/text` `n` `N`     | Search forward, next match, previous match                |
| `*`                 | Search the word under the cursor                          |
| `ma` … `'a`         | Set mark `a` … jump back to its line                      |
| `Ctrl-6`            | Switch to the previously edited file                      |

## Editing

| Key                       | Action                                                        |
| ------------------------- | ------------------------------------------------------------- |
| `d` / `c` / `y` + motion  | Delete / change / yank: `dw`, `d}`, `yy`, `dd`, `cc`           |
| `diw` / `ci"` / `da[`     | Text objects: inside a word, inside quotes, around brackets   |
| `p` / `P`                 | Paste after / before; `y` and `p` use the system clipboard    |
| `>>` / `<<`               | Indent / outdent the line                                     |
| `gcc`                     | Toggle a comment                                              |
| `[<Space>` / `]<Space>`   | Blank line above / below                                      |
| `v` / `V`                 | Character / line selection, then any operator                 |

## German keyboard (xkb `de`)

`[ ] { } /` sit behind AltGr or Shift. The config moves them to the umlaut keys in Normal,
Visual and Operator-pending mode. Insert mode and `f`, `t`, `r` still get the umlaut.

| Press       | Acts as             | Example                                                   |
| ----------- | ------------------- | --------------------------------------------------------- |
| `ö` / `ä`   | `[` / `]`           | `diö` deletes inside brackets; `ö<Space>` adds a blank line above |
| `Ö` / `Ä`   | `{` / `}`           | `Ä` jumps a paragraph down; `dÄ` deletes to the paragraph end |
| `ß`         | `/`                 | `ßword` searches for word                                 |
| `0` or `_`  | instead of `^`      | `^` is a dead key on `de`                                 |
| `'a`        | instead of `` `a `` | the backtick is a dead key on `de`                        |
| `Ctrl-6`    | `Ctrl-^`            | previous file                                             |
| `K` in help | `Ctrl-]`            | follows the help tag under the cursor                     |

Alternative: the US layout with umlauts on AltGr —
[guides/neovim.md](../guides/neovim.md#german-keyboard).

## Learning path

| Week | Do                                                                                   |
| ---- | ------------------------------------------------------------------------------------ |
| 1    | `:Tutor` daily, then `:Tutor vim-02-beginner`; every Markdown, YAML and JSON edit in nvim |
| 2    | One chapter of `:help user-manual` per day: `usr_02` to `usr_12`                     |
| 3    | precognition.nvim — hints where `w`, `b`, `e`, `f` land ([install](../guides/neovim.md#plugins)) |
| 4+   | hardtime.nvim — blocks key repeats and names the faster motion                       |

## Resources

| Resource                 | Cost | URL                                                                   |
| ------------------------ | ---- | --------------------------------------------------------------------- |
| Neovim user manual       | free | <https://neovim.io/doc/user/usr_toc.html>                             |
| Learn Vim (Igor Irianto) | free | <https://github.com/iggredible/Learn-Vim>                             |
| Vim cheat sheet          | free | <https://vim.rtorr.com/>                                              |
| Interactive drills       | free | <https://openvim.com/>                                                |
| Practical Vim, 2nd ed.   | paid | <https://pragprog.com/titles/dnvim2/practical-vim-second-edition/>    |
