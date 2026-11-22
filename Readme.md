STM hunter
Big thanks to Lanz and to 2fabi1's GitHub website for the medal and time data.
Real Readme.md TMF STM Overlay

A lightweight in-game overlay for TrackMania Nations Forever and TrackMania United Forever that shows Super Trackmaster (STM) times and the Super Gold / Silver / Bronze cutoffs for every campaign track, right next to the game.

Pick a track, glance at the number you need to beat, keep racing.

Features
STM times for 401 tracks: 65 Nations, 294 United (7 environments × 42 tracks), 21 Puzzle, 21 Stunt
Super medal cutoffs: Super Gold, Super Silver and Super Bronze times, plus the regular Trackmaster time (RTM) for reference
Two views: a compact HUD box for use while racing, and a track-list panel for browsing nearby tracks and their STMs
Zero dependencies: a single 32-bit executable with all data compiled in; no config files, no network access
Two ways to run: as a standalone .exe, or as an .asi loaded into the game process
Quick start
Download the latest release and extract it.
Start TrackMania.
Run stm_overlay.exe.

[!IMPORTANT] The overlay is a transparent window on top of the game, so TrackMania must run in windowed or borderless mode. It cannot draw over exclusive fullscreen.

Loading as an ASI plugin

Copy stm_overlay.asi into the game folder and use an ASI loader such as Ultimate ASI Loader (installed as binkw32.dll). The overlay then starts and stops with the game.

Controls

Hotkeys only work while the game window is focused.

Key	Action
F6 / F7	Previous / next track
Shift + F6 / F7	Jump 10 tracks
Ctrl + F6 / F7	Jump to previous / next group (category, environment, difficulty)
F8	Toggle the HUD box
F9	Toggle the track-list panel

Tracks are ordered Nations, then United by environment and difficulty (White → Black), then Puzzle, then Stunt.

How the medal times work

For timed tracks, the Super medal cutoffs are derived from STM and RTM:

Medal	Time must be at most
STM	the STM time
Super Gold	STM + ⅛ × (RTM − STM)
Super Silver	STM + ¼ × (RTM − STM)
Super Bronze	STM + ½ × (RTM − STM)

Each cutoff is rounded up to the next hundredth of a second. These rules were inferred from the dataset rather than taken from an official source, and they reproduce the medal of all 68,288 timed results in it.

Stunt tracks are scored rather than timed, so the overlay shows only the STM and RTM scores with no cutoffs.

Limitations
Manual track selection. The overlay does not read the current track from the game. Use the hotkeys to select it.
Overlay, not a native plugin. It is a separate transparent window positioned over the game, not drawn inside TrackMania's own rendering.
Windowed or borderless only (see above).
Windows only, and untested on Wine/Proton.
Not yet tested in-game. It was cross-compiled on Linux, so bug reports are welcome.
Building from source

You need a 32-bit MinGW-w64 toolchain (on Debian/Ubuntu: g++-mingw-w64-i686).

bash
# Standalone executable
i686-w64-mingw32-g++-posix -O2 -std=c++17 -static -static-libgcc -static-libstdc++ \
  -mwindows -municode source/stm_overlay.cpp -o stm_overlay.exe -lgdi32 -luser32

# ASI plugin
i686-w64-mingw32-g++-posix -O2 -std=c++17 -static -static-libgcc -static-libstdc++ \
  -DBUILD_ASI -shared source/stm_overlay.cpp -o stm_overlay.asi -lgdi32 -luser32

Track data lives in source/stm_data.h as a plain C++ array. To change or extend it, edit that file or regenerate it from your own CSV.

Project layout
stm_overlay.exe        standalone build
stm_overlay.asi        ASI plugin build
source/
  stm_overlay.cpp      overlay window, hotkeys, rendering
  stm_data.h           generated track table (name, category, STM, RTM)
Disclaimer

This is an unofficial fan project. It is not affiliated with or endorsed by Nadeo or Ubisoft. TrackMania is a trademark of its respective owners.

Credits
Made by Claude and Raghuram.
Big thanks to Lanz and to 2fabi1's GitHub website for the medal and time data.
Old Readme.md 
info, told to me by claude.
I built the STM overlay as a 32-bit .exe and an .asi, packaged in tmf-stm-overlay.zip, but I haven't been able to run it in TrackMania. It was cross-compiled on Linux, so you're the first tester.

It covers all 401 tracks in your CSV (Nations, United, Puzzle, Stunt) and shows STM, RTM and the Super Gold, Silver and Bronze cutoffs. Champion and Warrior are left out, as you decided.

How to use it
Download the Zip file in this repository
Extract that

Start TrackMania, then run stm_overlay.exe. It attaches to the game window (TmForever.exe or TmNationsForever.exe).
You have to play in windowed or borderless mode. A window overlay can't draw over exclusive fullscreen.
The .asi version is for loading through an ASI loader instead.
F6 and F7 move between tracks. Shift jumps 10 tracks, and Ctrl jumps to the previous or next environment and difficulty group.
F8 toggles the small HUD box. F9 toggles a list panel showing the tracks around your selection with their STM times.

Limitations

Manual track selection. It doesn't read the current track from the game, because I don't have verified memory offsets for TMUF. If you have a way to read the loaded track name, I can add auto-detect.
Overlay, not a true in-game plugin. I couldn't find a plugin API for TMUF to hook into. It's the same overlay in both the HUD and panel views, not drawn inside the game's own interface.
Stunt tracks show only STM and RTM scores, with no cutoffs.

Medal cutoffs

Super Gold, Silver and Bronze are STM plus 1/8, 1/4 and 1/2 of the gap between RTM and STM, rounded up to the next hundredth.
I worked that out from your data, and it matches all 68,288 timed results. It's inferred rather than official.

If you test it, tell me whether the overlay appears and lines up with the game window, and I'll fix whatever misbehaves.
