# ROM workflow: add, check, play

ROMs go through one checkpoint before any front end sees them. You run the ROM manager on **one computer only** (the Windows PC in this guide), and only when you add a new system or a batch of new games. Every device then reads the checked library.

```
Incoming  ──►  RomVault (check, rename, sort)  ──►  ROMs library  ──►  LaunchBox / ES-DE / RetroDECK
(ToSort)                                            (shared, short names)
```

The tool is **[RomVault](https://www.romvault.com/)**: free, Windows, and its tree shows at a glance what is complete (green), fixable (yellow) and missing (red). Igir does the same from the command line on any OS, if you ever need it off Windows.

## Folders

```
D:\Games\
├── ROMs\          the library every front end reads (RomVault's RomRoot)
├── ToSort\        incoming: drop new files here, never straight into ROMs
├── BIOS\
└── RomVault\
    └── DatRoot\   one DAT per system
```

If the library lives on a NAS, `ROMs` and `ToSort` are folders on the share; RomVault runs on the PC and works on them over the network.

## 1. Set up RomVault (once)

1. Install RomVault into `D:\Games\RomVault`.
2. In its settings, set **RomRoot** to `D:\Games\ROMs` and **ToSort** to `D:\Games\ToSort`.
3. Download the DATs for your systems:

    | Systems | DAT source |
    | --- | --- |
    | Cartridge consoles and handhelds | [No-Intro](https://datomatic.no-intro.org/) |
    | Disc systems (PlayStation, Saturn, Sega CD, Dreamcast) | [Redump](http://redump.org/) |
    | Arcade | The MAME or FinalBurn Neo DAT for the exact emulator version you play with |
    | Older home computers | TOSEC |

4. Put each DAT in `DatRoot`, one subfolder per system named like the library folder (for example `DatRoot\snes`), so each DAT lines up with `ROMs\snes`. Click **Update DATs**.

## 2. Add a new system

1. Copy all files for that system into `ToSort`, in any state (zipped, badly named, mixed).
2. Add its DAT (step 1.3 and 1.4) and click **Update DATs**.
3. Click **Scan ROMs**, then **Find Fixes**, then **Fix ROMs**. RomVault moves every file that matches the DAT out of `ToSort` into `ROMs\<system>`, under its official name.
4. Read the tree for that system:
    - **Green:** you have it, correct and named right.
    - **Red:** in the DAT but you don't have it. This is your missing list.
    - Anything left in `ToSort` matched nothing: a bad dump, a hack, or a wrong system. Check it by hand, then delete it or keep it in a separate folder outside `ROMs`.
5. Now add the system to the front ends (section 4).

## 3. Add new games to an existing system

1. Drop the new files into `ToSort`.
2. **Scan ROMs**, **Find Fixes**, **Fix ROMs**. Good files land in the right system folder with the right name; the rest stay in `ToSort`.
3. The front ends pick them up (section 4).

When a newer DAT comes out, replace the old one in `DatRoot` and run the same three buttons. RomVault may rename files to match; see the note in section 4 about LaunchBox.

## 4. Into the front ends

Only `ROMs` is ever read by a front end, so whatever RomVault rejected never reaches them.

| Front end | New games in an existing system | New system |
| --- | --- | --- |
| LaunchBox (Windows) | Picked up by **Automated Imports**, or run **Tools > Scan** | **Tools > Import > ROM Files > Single Platform**, set Platform and Scrape As, check a core is set ([guide](windows-launchbox.md#bulk-import)) |
| ES-DE (Linux, Mac) | Restart ES-DE, then scrape with "only missing media" | Same, as long as the folder uses the ES-DE short name |
| RetroDECK (Steam Deck) | Copy or sync `ROMs` into `retrodeck/roms`, restart, scrape missing media | Same |

**Renames and LaunchBox:** LaunchBox stores each game's file path. If RomVault renames files that LaunchBox already imported (usually after a DAT update), run **Tools > Scan** in LaunchBox: it removes the entries for the old names and adds the new ones. ES-DE has no such problem because it rescans every start, though scraped media for a renamed game may need re-scraping.

## Rules of thumb

- Never copy straight into `ROMs`. Everything goes through `ToSort`.
- Run RomVault from one computer only, and only after adding files or DATs.
- Arcade: keep the DAT version and the emulator version the same; update both together.
- Disc games: check the .bin/.cue against the Redump DAT before converting to .chd.
