# Windows: LaunchBox

LaunchBox is the one front end on Windows for the whole library: retro systems through RetroArch, and the PC storefronts (Steam, Epic, GOG and so on). You bring the ROM, BIOS and special files; LaunchBox downloads the emulators, box art and metadata.

Example layout (any drive works, just keep it out of Program Files):

```
D:\Games\
├── ROMs\        one folder per system (see the README for names and rules)
├── ToSort\      incoming ROMs, waiting for the RomVault check
├── BIOS\        master copy of every BIOS file you own
├── RomVault\    the ROM manager (see the ROM workflow)
└── LaunchBox\   the app itself, with RetroArch inside it
```

This PC is also where new ROMs get checked before they reach `ROMs`: see the [ROM workflow](rom-workflow.md).

Keep ROMs and BIOS outside the LaunchBox folder so a reinstall or rebuild never touches your game files. The LaunchBox folder grows a lot if you download all images, videos and audio for every game.

## You need

- Windows 10 or 11, 64-bit
- A drive with room for your ROMs plus several GB for media
- A LaunchBox account (the email registration is needed for the download; the paid Premium licence adds Big Box mode)

## Install LaunchBox and emulators

LaunchBox 13.15 and later ships with emulator plugins that download and configure RetroArch for you, so RetroArch is no longer installed by hand.

1. Download LaunchBox from <https://www.launchbox-app.com/download> and install it to `D:\Games\LaunchBox`.
2. Start LaunchBox and cancel the first-run import wizard. You import after the emulators are ready.
3. Open **Tools > Manage > Plugins** and check the RetroArch plugin is enabled. Dolphin, PCSX2, MAME and ScummVM plugins ship with it too.
4. Open **Tools > Manage > Emulators**, choose **Add**, pick **RetroArch** and let it download. RetroArch lands in `LaunchBox\Emulators\RetroArch`, its cores in `...\RetroArch\cores`.
5. In the RetroArch profile, open **Associated Platforms** and check each platform has a core selected (suggestions below).
6. Where a standalone emulator is better (PCSX2, Dolphin), add it the same way through its plugin and tick **Default Emulator** on that platform.

| System | Suggested emulator / core | Alternative | Notes |
| --- | --- | --- | --- |
| NES | RetroArch: Mesen | Nestopia | |
| SNES | RetroArch: Snes9x | | |
| Nintendo 64 | RetroArch: Mupen64Plus-Next | ParaLLEl N64 (accuracy) | |
| Game Boy / Color | RetroArch: Gambatte | | |
| Game Boy Advance | RetroArch: mGBA | | |
| Nintendo DS | RetroArch: melonDS DS | DeSmuME | |
| PC Engine / TurboGrafx-CD | RetroArch: Beetle PCE | | CD needs BIOS |
| Sega Master System / Genesis / CD | RetroArch: Genesis Plus GX | PicoDrive (also 32X) | Sega CD needs BIOS |
| Sega Saturn | RetroArch: Beetle Saturn | | needs BIOS |
| Sega Dreamcast | RetroArch: Flycast | | BIOS optional |
| PlayStation | RetroArch: SwanStation or Beetle PSX HW | | needs BIOS |
| PlayStation 2 | PCSX2 (plugin) | | needs BIOS |
| PSP | RetroArch: PPSSPP | | no BIOS |
| GameCube / Wii | Dolphin (plugin) | RetroArch Dolphin core | no BIOS |
| Arcade | RetroArch: FinalBurn Neo, or MAME (plugin) | | set must match emulator version |

### Updating

Update emulators from **Tools > Manage > Emulators** (edit, then **Update**). **Reinstall** wipes the RetroArch folder, including its BIOS folder, so keep the master BIOS copy outside it.

If RetroArch runs unstable with a game or core, try another core first, then a different RetroArch version (a nightly or an older release).

## BIOS files

Neither LaunchBox nor RetroArch downloads console BIOS files, because they are copyrighted. What is automatic is everything around them.

1. Start RetroArch (`LaunchBox\Emulators\RetroArch\retroarch.exe`), go to **Main Menu > Online Updater > Core System Files** and download the entries for your cores. These are free data files, not BIOS.
2. In LaunchBox, **Tools > Manage > Emulators**, edit RetroArch and open its BIOS / dependency files view. It lists each required file as present, missing or mismatched.
3. For each missing file, browse to it in `D:\Games\BIOS`; LaunchBox copies it to the right folder under the right name. Repeat for the PCSX2 profile.

Common BIOS files (exact names matter; RetroArch's folder is `LaunchBox\Emulators\RetroArch\system`):

| System | File name(s) | Required? |
| --- | --- | --- |
| PlayStation | scph5500.bin (JP), scph5501.bin (US), scph5502.bin (EU) | Yes |
| PlayStation 2 | any console BIOS dump, in PCSX2's own bios folder | Yes |
| Sega CD | bios_CD_U.bin, bios_CD_E.bin, bios_CD_J.bin | Yes |
| Sega Saturn | sega_101.bin (JP), mpr-17933.bin (US/EU) | Yes |
| Sega Dreamcast | dc\dc_boot.bin, dc\dc_flash.bin | Recommended |
| PC Engine CD | syscard3.pce | Yes |
| Famicom Disk System | disksys.rom | Yes |
| Neo Geo | neogeo.zip, beside the arcade ROMs | Yes |
| Game Boy Advance | gba_bios.bin | Optional |
| Nintendo DS | bios7.bin, bios9.bin, firmware.bin | Optional |

To confirm a core sees its BIOS, load the core in RetroArch and open **Main Menu > Information > Core Information**; each firmware line shows Present or Missing.

## Bulk import

Use **Tools > Import > ROM Files > Multiple Platforms** to bring in every system folder in one run. Test one small system first, so a naming mistake costs minutes, not hours.

**Trial run**

1. **Tools > Import > ROM Files > Single Platform**, pick one folder such as `ROMs\megadrive`, import 3 to 5 games.
2. When asked about files, choose **leave them where they are**.
3. Launch each game. If they run, move on; the full import skips games already in the library.

**Full import**

1. Set your preferred regions first in **Tools > Options > Region Priorities**.
2. **Tools > Import > ROM Files > Multiple Platforms**, **Add Folder**, pick `D:\Games\ROMs`.
3. Check each detected row:
    - **Platform**: the full name shown in your library (megadrive becomes Sega Genesis, and so on).
    - **Scrape As**: the LaunchBox Games Database platform used for matching. Must be a real database platform name.
    - Remove any folder you do not want imported.
4. In the advanced options, turn on **combine matching ROM titles** (one entry per game across regions; leave it off and force importing duplicates if you want every version listed) and set MAME / FinalBurn Neo handling for arcade.
5. Choose metadata and media (next section), review the list, then **Finish**. Media keeps downloading in the background.
6. **Tools > Manage > Emulators**: confirm every new platform has a default emulator.

Turn on **Tools > Options > Automated Imports** so new ROMs that the [ROM workflow](rom-workflow.md) adds to existing folders are picked up. **Tools > Scan** checks for added or removed games on demand.

## Box art and metadata

Chosen on the import's metadata and media step:

1. **Metadata source:** LaunchBox Games Database (free).
2. **Images:** at least Box - Front, Clear Logo and Screenshot - Gameplay. Add Fanart - Background for Big Box.
3. **Media limits:** on, one file per type per game. Saves a lot of disk space.
4. **Videos (optional):** EmuMovies needs a connected account.
5. **Bezels (optional):** the RetroArch integration can download Bezel Project bezels.

Wrong or missing matches: select them and use **Tools > Download > Update Metadata and Media**, or edit the game's metadata and search by another title. Getting **Scrape As** right prevents most mismatches.

## Controllers, graphics and sound

Plug in the controller and check Windows detects it (install drivers if needed). Most controllers are mapped automatically in RetroArch and need nothing else.

In RetroArch, **Settings > Drivers > Video** defaults to `gl`, which works with most cores. Try `vulkan` for better looks or speed; if a core misbehaves, go back to `gl`.

## Check and fix

- [ ] One game launches on every platform
- [ ] Disc systems (PlayStation, Sega CD, Saturn) boot past the BIOS screen
- [ ] Multi-disc games show as one entry and swap discs
- [ ] Box art appears for most games
- [ ] Controller works in-game without remapping

| Problem | Likely cause | Fix |
| --- | --- | --- |
| Game does nothing or RetroArch closes at once | No core set, or core not downloaded | Emulators > RetroArch > Associated Platforms: pick a core |
| Black screen or BIOS error on disc systems | BIOS missing or wrong name | Re-check names, then Core Information |
| Platform has no games after import | Folder nested too deep, or wrong Scrape As | Flatten the folder, re-import it |
| Arcade games fail | ROM set version does not match the emulator | Use the matching FinalBurn Neo or MAME version |
| Same game listed several times | Regional versions not combined | Re-import with combine matching ROM titles |
| Wrong box art | Wrong title or platform matched | Fix Scrape As, then Update Metadata and Media |
| Archive will not load | Emulator cannot read .zip/.7z | Tick Extract ROMs on that emulator row |

## Backup and rebuild

LaunchBox is portable: copying `D:\Games` to another drive or PC moves the whole setup, as long as the drive letter matches or paths are relative.

| What | Where | Why |
| --- | --- | --- |
| ROMs | `D:\Games\ROMs` | Cannot be re-downloaded |
| BIOS | `D:\Games\BIOS` | Master copy; a RetroArch reinstall wipes its own copy |
| Library and settings | `LaunchBox\Data` | Platforms, games, play counts, favourites |
| Media | `LaunchBox\Images`, `Videos`, `Manuals` | Re-downloadable, but saves hours |
| Saves | `LaunchBox\Emulators\RetroArch\saves` and `states`, plus each standalone emulator's save folder | Your progress |

Rebuild from scratch: copy ROMs and BIOS into place, follow Install and BIOS above, run the bulk import with the same Platform and Scrape As names, copy back saves and states. For an exact copy, restore the whole `LaunchBox` folder instead; LaunchBox also keeps rolling backups in `LaunchBox\Backups`.

## PC stores (to be completed)

Step 3 of the plan. From the old notes, Steam import works like this:

1. **Tools > Import > Steam Games**.
2. Enter your Steam profile id and a Steam Web API key (use an existing one or create one with any domain name).

Epic, GOG and the others are still to be written.

## Still to do

- RetroArch AI Service (on-screen translation): registration and setup.
- Per-core and per-game overrides: shaders, frame and latency settings.

## Sources

- [Choosing the Right Way to Import Your Games](https://feedback.launchbox-app.com/help/articles/7016587-choosing-the-right-way-to-import-your-games) (LaunchBox Help Center)
- [Multi-Platform Imports](https://launchbox.featurebase.app/help/articles/4046325-multi-platform-imports) (LaunchBox Help Center)
- [RetroArch LaunchBox Integration Plugin](https://feedback.launchbox-app.com/help/articles/8467441-retroarch-launchbox-integration-plugin) (LaunchBox Help Center)
- [Setting Up an Emulator Manually](https://feedback.launchbox-app.com/help/articles/3038328-setting-up-an-emulator-manually) (LaunchBox Help Center)
- [LaunchBox Plugin Manager FAQ](https://forums.launchbox-app.com/topic/83544-faq-launchbox-plugin-manager-everything-you-need-to-know/) (LaunchBox forums)
- [Easily import tens of platforms](https://forums.launchbox-app.com/topic/86710-easily-import-tens-of-platforms/) (LaunchBox forums)
- [ROM Import & Management Guide, RetroFrogg Method v2](https://forums.launchbox-app.com/topic/87876-rom-import-management-guide-retrofrogg-method-v2-updated-simpler-method/) (LaunchBox forums, October 2024)

BIOS file names and core suggestions are from general libretro knowledge; RetroArch's Core Information screen is the final word for each core.
