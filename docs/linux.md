# Linux: ES-DE and Heroic

On a Linux desktop, ES-DE is the front end for retro games, the same one used on the Mac and inside RetroDECK on the Steam Deck. PC store games go through Steam and Heroic Games Launcher (GOG and Epic). LaunchBox has no Linux version yet; its developers expect one in 2027.

On a Steam Deck or Steam Machine use RetroDECK instead: see [the last section](#steam-deck-or-steam-machine).

## Retro: install ES-DE and emulators

Most emulators install as Flatpaks from Flathub. ES-DE finds Flatpak emulators on its own, so there is no emulator setup inside ES-DE.

1. Make sure Flatpak and Flathub are set up (most distros ship both; otherwise follow [flathub.org/setup](https://flathub.org/setup)).
2. Install RetroArch, plus the standalone emulators you use:

    ```
    flatpak install flathub org.libretro.RetroArch
    flatpak install flathub net.pcsx2.PCSX2              # PlayStation 2
    flatpak install flathub org.DolphinEmu.dolphin-emu   # GameCube / Wii
    ```

3. Start RetroArch once and download cores in **Main Menu > Online Updater > Core Downloader** (the same cores as in the [Windows table](windows-launchbox.md#install-launchbox-and-emulators)). Also download **Online Updater > Core System Files**.
4. Download the ES-DE AppImage for Linux from [es-de.org](https://es-de.org/), make it executable (`chmod +x`) and start it.
5. On first start, ES-DE asks for the ROM directory. Point it at the shared `ROMs` folder. The short system names already match, so nothing needs renaming.

If the library is on another drive or a NAS mount, give the Flatpak emulators access to it, for example:

```
flatpak override --user --filesystem=/mnt/games org.libretro.RetroArch
```

## BIOS files

As on Windows, BIOS files are never downloaded for you.

1. Copy your BIOS files into RetroArch's system folder. For the Flatpak it is `~/.var/app/org.libretro.RetroArch/config/retroarch/system` (RetroArch shows it under **Settings > Directory > System/BIOS**).
2. PS2 BIOS files go in the folder PCSX2 asks for on its first start.
3. File names are the same as in the [Windows BIOS table](windows-launchbox.md#bios-files). To confirm a core sees its BIOS, load it and open **Main Menu > Information > Core Information**.

## Add ROMs and download box art

There is no import step: ES-DE scans the ROM folder every time it starts, so copying files into the right system folder is the import.

1. New ROMs reach the `ROMs` folder through the [ROM workflow](rom-workflow.md). Restart ES-DE; every system with games appears.
2. Create a free account at [screenscraper.fr](https://www.screenscraper.fr/). ES-DE's best box art and metadata come from it, and an account raises the download limits.
3. In ES-DE, **Main Menu > Scraper**: choose ScreenScraper, enter the account, pick the media types and systems, then **Start**. For a big library this takes hours; re-run later with "only missing media".

## PC store games (to be completed)

Step 3 of the plan. The tools:

- **Steam:** the native client, from your distro or Flathub.
- **Heroic Games Launcher:** GOG and Epic (`flatpak install flathub com.heroicgameslauncher.hgl`).

Lutris is left out: it is only needed for stores Heroic does not cover (Battle.net, EA, Ubisoft).

## Check, back up and rebuild

- [ ] One game launches on every system
- [ ] Core Information shows no missing BIOS for the systems you use
- [ ] Box art appears after scraping
- [ ] Controller works in menus and in-game

| Problem | Fix |
| --- | --- |
| System not shown | Folder name must match the ES-DE short name exactly (lower case) |
| Game won't start on a disc system | Check the BIOS file name in RetroArch's system folder |
| Emulator can't see games on another drive | Give the Flatpak access with `flatpak override --filesystem` |
| Wrong game matched when scraping | Edit the game's metadata in ES-DE and scrape it alone with a corrected name |

**Back up** the shared `ROMs` and `BIOS` (irreplaceable), RetroArch's `saves` and `states` under `~/.var/app/org.libretro.RetroArch/config/retroarch/`, and `~/ES-DE` (settings and scraped media, re-downloadable but slow).

**Rebuild:** install the Flatpaks and ES-DE again, point ES-DE at the same ROM folder, copy back the BIOS, saves and `~/ES-DE`.

## Steam Deck or Steam Machine

Use RetroDECK here rather than plain ES-DE. SteamOS has a read-only system filesystem that is replaced on every update, so emulators and configs installed by hand can break or vanish. RetroDECK is ES-DE with the emulators already bundled and configured, as one self-contained Flatpak in your user space, so it survives SteamOS updates and needs almost no setup. It looks and works like ES-DE on the desktop and the Mac.

1. Switch to Desktop Mode, open Discover, search for RetroDECK and install it.
2. On first run, choose internal storage or the SD card for the `retrodeck` folder. It creates `roms/` (with the same short system names), `bios/`, `saves/` and `states/`.
3. Copy or sync your shared ROMs into `retrodeck/roms` and your BIOS into `retrodeck/bios`.
4. Check BIOS files in **RetroDECK Configurator > Tools > BIOS Checker**.
5. Scrape box art in ES-DE as above.
6. To launch from Game Mode, add RetroDECK to Steam as a non-Steam game (**Games > Add a Non-Steam Game**).

A Steam Machine also runs SteamOS, so the same steps apply. Back up the whole `retrodeck` folder; to rebuild, install RetroDECK and pick the same folder location on first run.

## Sources

- [ES-DE](https://es-de.org/) (official site: Windows, Linux, macOS)
- [RetroDECK wiki](https://retrodeck.readthedocs.io/)
- [LaunchBox should get a Linux version in 2027](https://gamingonlinux.com/2026/08/game-launcher-launchbox-should-get-a-linux-version-in-2027) (GamingOnLinux, August 2026)

Flatpak ids, folder paths and menu names are from general knowledge of ES-DE, RetroArch and RetroDECK, not checked page by page; each project's own docs are the final word.
