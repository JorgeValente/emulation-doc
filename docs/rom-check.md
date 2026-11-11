# Check ROMs with a ROM manager (optional)

Before importing, a ROM manager checks your files against official DAT lists, so every system holds good dumps with standard names. Clean names match the LaunchBox Games Database and ScreenScraper far more often, and you see at a glance which games are missing or bad.

## Which DAT for which system

| Systems | DAT source |
| --- | --- |
| Cartridge consoles and handhelds | [No-Intro](https://datomatic.no-intro.org/) |
| Disc systems (PlayStation, Saturn, Sega CD, Dreamcast) | [Redump](http://redump.org/) |
| Arcade | The MAME or FinalBurn Neo DAT for your emulator version |
| Older home computers | TOSEC |

## Which tool

- **[Igir](https://igir.io/)** (Windows, Linux and Mac, free, command line): one command verifies, renames and sorts into system folders. The same tool on every device.
- **[RomVault](https://www.romvault.com/)** (Windows, free): a visual tree that turns green when a set is complete; the tool the RetroFrogg guide uses. Its DatVault add-on downloads and updates DATs automatically, but needs a Patreon subscription; otherwise download DATs yourself.

## Steps (RomVault)

1. Install RomVault into its own folder, for example `D:\Games\RomVault`. It uses three subfolders: `DatRoot`, `RomRoot` and `ToSort`.
2. Put the DAT files in `DatRoot`, one subfolder per system (for example `DatRoot\Arcade\MAME`), and click **Update DATs**.
3. Map each DAT to its system folder in `D:\Games\ROMs` (for example the No-Intro SNES DAT to `ROMs\snes`).
4. Click **Scan ROMs**. Green means complete, yellow means renamable or fixable, red means missing.
5. Click **Find Fixes**, then **Fix ROMs**. RomVault renames files to the DAT names and moves unknown files to `ToSort`, so nothing is deleted.
6. Re-scan after adding games; the game count per system in your front end should match RomVault's count.
