# Mac: store apps and ES-DE

On a Mac, launch modern games from their own store apps (Steam, GOG and so on). The Mac has fewer games, so a unified launcher adds little. For retro, use ES-DE: the same front end as on Linux and inside RetroDECK on the Steam Deck, so it looks the same and reads the same ROM folders.

## Install

1. Download ES-DE for macOS from [es-de.org](https://es-de.org/) and install it.
2. Install [RetroArch](https://www.retroarch.com/), start it once and download cores in **Main Menu > Online Updater > Core Downloader** (same cores as in the [Windows table](windows-launchbox.md#install-launchbox-and-emulators)). Add standalone emulators only where you need them.
3. When ES-DE first starts, point its ROM directory at the shared `ROMs` folder. The short system names match, so nothing needs renaming.

## BIOS

Copy your BIOS files into RetroArch's system folder, shown under **Settings > Directory > System/BIOS**. File names are in the [Windows BIOS table](windows-launchbox.md#bios-files).

## Box art

Scrape with ScreenScraper, the same way as on [Linux](linux.md#add-roms-and-download-box-art).

## Back up

The shared `ROMs` and `BIOS`, RetroArch's `saves` and `states` folders, and `~/ES-DE` (settings and scraped media).
