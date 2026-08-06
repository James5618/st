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

## FreeBSD

This is the `freebsd` branch, built and installed the same way on FreeBSD 15.
It differs from `master` only in `config.mk`: the headers and libraries come
from `/usr/local` rather than `/usr/X11R6`. Nothing else needs changing —
`st.c` already picks `<libutil.h>` for `forkpty(3)` on FreeBSD by itself, and
that header does not depend on the BSD namespace, so `_XOPEN_SOURCE` stays.

The two helper scripts the Makefile installs alongside st needed porting too:
`st-copyout` used `tac`, `sed -i` with a `\x` escape and the `\s`/`\S` regex
extensions, and `st-urlhandler` used `setsid(1)`. They now use `tail -r`, `tr`,
character classes and `daemon(8)`.

Build dependencies: `pkg install xorg libX11 libXft libXrender fontconfig
freetype2 harfbuzz pkgconf`. The helpers additionally want `xclip` and
`xdg-utils`.
