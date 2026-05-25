# sfxr Flatpak

Flatpak build manifest for [sfxr](http://www.drpetter.se/project_sfxr.html), a retro sound effect generator by DrPetter. Originally created for Ludum Dare 48 #10 in 2007, sfxr lets you quickly generate 8-bit style sound effects for games — laser shots, explosions, pickups, jumps, and more.

This packages the [SDL port](https://github.com/fabiensanglard/sfxr-sdl) (sfxr-sdl 1.2.1).

## Building & Installing

```bash
flatpak-builder --force-clean --user --install build org.sfxr.sfxr.json
```

## Running

```bash
flatpak run org.sfxr.sfxr
```

## What this manifest does

The upstream source has two issues that need addressing for Flatpak:

- **SDL 1.2 dependency** — The freedesktop runtime only ships SDL2, so [sdl12-compat](https://github.com/libsdl-org/sdl12-compat) is built as a compatibility shim.
- **GTK3 file dialogs** — The upstream `sdlkit.h` uses GTK3 for open/save dialogs. This is replaced with a patched version (`sdlkit.h`) that calls `zenity --file-selection` instead, which automatically goes through the xdg-desktop-portal inside the sandbox. No GTK dependency needed.
- **Data file paths** — Hardcoded `/usr/share/sfxr/` paths are rewritten to `/app/share/sfxr/` at build time.
- **Non-square icon** — The upstream icon is 50×40. A padded 64×64 version (`org.sfxr.sfxr.png`) is shipped for desktop integration.

## Files

| File | Purpose |
|---|---|
| `org.sfxr.sfxr.json` | Flatpak build manifest |
| `sdlkit.h` | Patched SDL toolkit header (GTK3 → zenity) |
| `org.sfxr.sfxr.png` | Square 64×64 application icon |

## License

sfxr is [MIT licensed](https://opensource.org/licenses/MIT) — Copyright © 2007 Tomas Pettersson.
