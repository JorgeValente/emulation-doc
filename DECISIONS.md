# Decisions and things to remember

## Guiding rule

As few tools as possible. One front end per device, one shared ROM and BIOS library, and a new tool only when it clearly earns its place. ES-DE is the common front end everywhere except Windows.

## Decided

| Date | Decision | Why |
| --- | --- | --- |
| 2026-11-11 | Linux desktop: ES-DE for retro, Lutris + Heroic for PC stores (replaces RetroDECK on the desktop) | Same front end as the Mac; RetroDECK is only needed where the OS is read-only |
| 2026-11-09 | Windows: keep LaunchBox, also for PC stores | Paid licence, mature, no clearly better alternative |
| 2026-11-09 | Mac: store apps directly for modern games, ES-DE for retro | Fewer Mac games, so a unified launcher adds little |
| 2026-11-09 | Steam Deck / Steam Machine: RetroDECK | SteamOS's read-only system is replaced on updates; RetroDECK is a self-contained Flatpak that survives them |
| 2026-10-14 | ROM manager check is optional, before import | Clean names match scrapers better |
| 2026-10-14 | Regional versions merged into one entry by default (LaunchBox combine matching ROM titles) | Smaller, cleaner library |
| 2026-10-13 | ROM folders use ES-DE / RetroDECK short names (snes, psx, megadrive) | One library for every device; LaunchBox maps names at import |
| 2026-10-13 | RetroArch is installed and updated by LaunchBox on Windows, not by hand | Fewer manual steps (LaunchBox 13.15 and later) |
| 2026-10-13 | ROMs and BIOS live outside every app folder, with one master BIOS copy | Apps can be reinstalled without touching game files |

## Things to remember

- BIOS files are never downloaded automatically by LaunchBox, RetroArch, ES-DE or RetroDECK, because they are copyrighted. The tools only check and place your own copies.
- A RetroArch **Reinstall** from LaunchBox wipes its BIOS folder; **Update** does not.
- Arcade ROM sets must match the MAME or FinalBurn Neo version of the emulator.
- Saves and emulator settings are per device, not shared.
- LaunchBox has no Linux build yet; its developers expect one in 2027.

## Still open

- Buy a Steam Deck or a Steam Machine? Only the software (RetroDECK) is decided.
- PC stores (step 3): write the LaunchBox store imports and the Heroic / Lutris setup.
- RetroArch AI Service (translation) and per-core graphics overrides: still to write.
