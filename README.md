# emulation-doc

Emulation and game library documentation.

After getting tired of learning and re-reading a lot of documentation every time a new install was needed, I decided to write the documentation myself. No BS, straight-to-the-point instructions, kept up to date with current quirks and problems.

The rule for every choice here: **as few tools as possible**. One front end per device, one ROM and BIOS library shared by every device, and only add a tool when it clearly earns its place.

## Which tool on which device

| Device | Retro games | PC store games | Guide |
| --- | --- | --- | --- |
| Windows | LaunchBox (paid licence, decided: keep it) | LaunchBox too | [windows-launchbox.md](docs/windows-launchbox.md) |
| Linux desktop | ES-DE + RetroArch | Steam, plus Heroic for GOG and Epic | [linux.md](docs/linux.md) |
| Steam Deck or Steam Machine | RetroDECK (ES-DE with the emulators bundled) | Steam | [linux.md](docs/linux.md#steam-deck-or-steam-machine) |
| Mac | ES-DE + RetroArch | Each store's own app (Steam, GOG and so on) | [mac.md](docs/mac.md) |

ES-DE is the same front end on Linux, Mac and (inside RetroDECK) the Steam Deck, so those three look and work the same and use the same folder names. Only Windows differs, because LaunchBox is already paid for and handles the PC stores too.

## One shared library

Keep one master copy of ROMs and BIOS and point every device at it:

- **Several machines:** keep the master copy on a NAS or external drive and copy or sync it to each machine.
- **One PC dual-booting Windows and Linux:** keep `Games` on a separate data partition formatted exFAT or NTFS so both OSes can read and write it.

 Game files never live inside an app folder, so any app can be reinstalled without touching them.

```
Games/
├── ROMs/          one folder per system, short names (below)
│   ├── nes/
│   ├── snes/
│   ├── megadrive/
│   ├── psx/
│   └── ...
└── BIOS/          master copy of every BIOS file you own
```

System folders use the ES-DE / RetroDECK short names, because ES-DE only recognises its own names. LaunchBox accepts any folder name: you set the full Platform name once per folder at import.

| Folder | LaunchBox Platform |
| --- | --- |
| nes | Nintendo Entertainment System |
| snes | Super Nintendo Entertainment System |
| n64 | Nintendo 64 |
| gb / gbc / gba | Nintendo Game Boy / Game Boy Color / Game Boy Advance |
| nds | Nintendo DS |
| gc / wii | Nintendo GameCube / Nintendo Wii |
| mastersystem / megadrive / segacd | Sega Master System / Sega Genesis / Sega CD |
| saturn / dreamcast | Sega Saturn / Sega Dreamcast |
| pcengine / pcenginecd | NEC TurboGrafx-16 / NEC TurboGrafx-CD |
| psx / ps2 / psp | Sony Playstation / Sony Playstation 2 / Sony PSP |
| arcade (or mame, fbneo) | Arcade |

Rules for the ROM folders, on every device:

1. One system per folder, never two platforms mixed.
2. Flat inside each system folder: no A–Z, region or genre subfolders. Multi-disc games keep their .cue/.bin or .chd files together with an .m3u playlist.
3. No extra category level: `ROMs/Consoles/megadrive` breaks detection, `ROMs/megadrive` works.
4. Cartridge ROMs stay zipped (.zip/.7z). Arcade sets stay zipped and must match the MAME or FinalBurn Neo version.
5. Saves and emulator settings stay per device, because the emulators differ.

New ROMs never go straight into the library: they are checked first on one computer. See the [ROM workflow](docs/rom-workflow.md).

## Decisions and open questions

See [DECISIONS.md](DECISIONS.md) for what was decided, why, and what is still open.
