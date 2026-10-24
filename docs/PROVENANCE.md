# Provenance

Scrap's original homepage was `http://www.math.leidenuniv.nl/~mommen/scrap/`.
The site is gone. Everything in this repository was recovered from the Internet
Archive on 24 October 2026.

## Captures used

| What | Wayback URL |
| --- | --- |
| Homepage | <https://web.archive.org/web/20130524032130/http://www.math.leidenuniv.nl/~mommen/scrap/> |
| Files linked from it | <https://web.archive.org/web/20130618083756id_/http://www.math.leidenuniv.nl/~mommen/scrap/> |

The homepage capture is 24 May 2013 (the last good one before the directory
stopped serving). The payload links were 302-redirected to the 18 June 2013
capture, which is where the tarballs, zip, `curses.dll` and screenshots were
actually fetched from. `archive/homepage-20130524.html` is the raw capture with
the Wayback toolbar stripped.

## Files recovered

| File in this repo | Original path | Note |
| --- | --- | --- |
| `archive/scrap-1.1-source.tar.gz` | `x10drl1_1/scrap.tar.gz` | Extended 10DRL 1.1, 15 Nov 2006 |
| `archive/scrap-1.1-win32.zip` | `x10drl1_1/scrap.zip` | Win32 binary, `scrap.exe` + `curses.dll` + readme + manual |
| `archive/scrap-1.0-source.tar.gz` | `x10drl/scrap.tar.gz` | first Extended 10DRL, 26 Oct 2006 |
| `archive/scrap-10drl-source.tar.gz` | `10drl/scrap.tar.gz` | the original Ten-Day Roguelike |
| `archive/curses.dll` | `10drl/curses.dll` | needed by the 10DRL binary |
| `screenshots/screen1.png` … `screen3.png` | `10drl/screen1.png` … | the three homepage screenshots |

`archive/SHA256SUMS` has the checksums of the archived payloads. The three
screenshots are byte-identical to the copies in the author's own repository.

## Fidelity

The source at the top of this repository is the 1.1 tarball, with exactly two
kinds of change:

1. The GPL copyright/licence header the author added when he published the game
   himself at <https://github.com/thijsvanommen/scrap> is prepended to every
   `.cpp` and `.h` file except `mt19937ar.h`, which already carries the Mersenne
   Twister BSD notice. The code below those headers is unchanged; it was diffed
   against the archive tarball to confirm that.
2. `#include <cstring>` was added to `main.cpp`, `ui.cpp`, `being.cpp` and
   `game.cpp`, which use `strcpy`/`strcat`/`strlen` without including the header
   that now declares them. Without it the 2006 code does not compile on a modern
   `g++`. No game logic was touched.

`legacy/10drl/` and `legacy/x10drl/` are the older releases unpacked for
browsing, untouched, exactly as they came out of their tarballs.

Build verified on g++ 16.2.1 / ncurses: `make -f makefile.linux` compiles
cleanly (only `-Wwrite-strings` warnings, which are inherent to the 2006 code),
and the resulting binary starts and renders a level.

## Upstream

The author's own repository is <https://github.com/thijsvanommen/scrap>, where
the game is published under the GPL. That is the canonical project; this one is
an archival mirror kept buildable.
