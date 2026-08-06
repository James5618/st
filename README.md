# st — my build

The terminal for my [bootstrap](https://github.com/james5618/bootstrap) rice.
Based on [Luke Smith's build](https://github.com/LukeSmithxyz/st) of the
[suckless terminal](https://st.suckless.org/).

## Features

- Catppuccin colors by default; Xresources (and pywal) override them at
  runtime — set colors, font and `*.alpha` transparency there and run `xrdb`
- Follow urls with `alt-l`, copy urls with `alt-y`, copy command output with
  `alt-o` (all via dmenu)
- Scrollback with `alt-↑/↓`, `alt-pageup/down`, shift+mouse-scroll, or
  vim-style `alt-k/j` (`alt-u/d` for faster)
- Zoom/font size with the same bindings plus shift; `alt-home` resets
- Copy with `alt-c`, paste with `alt-v` or `shift-insert`
- Boxdraw, ligatures and font2 patches

## Installation

Requires `make`, Xlib headers, `libXft`, `fontconfig` and harfbuzz.

```sh
git clone https://github.com/james5618/st.git
cd st
sudo make install
```

Run a compositor (picom) if you want transparency. On OpenBSD, remove `-lrt`
from `$LIBS` in `config.mk` first.
