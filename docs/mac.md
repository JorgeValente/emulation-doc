# Mac: Heroic, Steam and ES-DE

On a Mac, PC store games go through two apps: Heroic Games Launcher for GOG and Epic (one app instead of GOG Galaxy and the Epic Games Launcher), and the Steam app for Steam. For retro, use ES-DE: the same front end as on Linux and inside RetroDECK on the Steam Deck, so it looks the same and reads the same ROM folders.

## PC store games

This guide assumes Heroic 3.0, which is still in beta (Beta 1, November 2026; the last stable version is 2.22.4). Bugs are expected, so make a backup with Heroic's Backup Wizard before changing settings or updating.

1. Download the macOS build of Heroic 3.0 from the [Heroic releases page](https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/releases) (pick the newest 3.0 beta, marked Pre-release) and move it to Applications.
2. Open Heroic, go to **Manage Accounts** and log in to GOG and Epic.
3. Install games from Heroic. Games with a Mac version install natively. Windows-only games need a Windows compatibility layer: Heroic can download one in **Settings > Wine Manager** (Game Porting Toolkit, Wine or CrossOver if you own it). Not every Windows game runs this way; check [AppleGamingWiki](https://www.applegamingwiki.com/) first.
4. Install the [Steam app](https://store.steampowered.com/about/) for Steam games and launch them from Steam. Heroic 3.0 can also show the Steam library, but it still needs the Steam app installed and the beta notes say some Steam games won't start and anti-cheat games probably won't work, so Steam stays the place to play them.

Back up with the Heroic Backup Wizard (logins, settings and game settings). Game folders are not part of it; they are re-downloadable.

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
