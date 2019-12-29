# emulation-doc
Emulation - Retroarch Documentation

After getting tired to learn and having to re-read a lot of documentation everytime a new install was needed, I decided to write the documentation myself. Will try to follow a no BS straight to the point instructions; will also try to keep this updated with current quirks & problems.

For example:

- Games: D:\Games\EmulationRoms\
- RetroArch: D:\Games\RetroArch\
- LaunchBox: D:\Games\LaunchBox\

# RetroArch

Before start, define 3 directories (not under Program Files) for: Games, RetroArch & LaunchBox. Keep the games where they reside, do not Copy or Move into RetroArch, this is the most flexible installation (both programs can be reinstalled independently without affecting the other).

__Note:__ The Subdirectory of LaunchBox will grow substantially if all images, videos & audio is downloaded from the Internet for each game.

## Installation

Download & Install latest Version (In this case: 1.8.2 Win Installer x64).

Double Click install file and Accept all Dialogs (Default Install to : C:\Users\XXX\AppData\Roaming\RetroArch\ ). Due to the use of LaunchBox (see below) we will install into another user Directory defined above.

Run RetroArch to check installation was okay.

__Note:__ if RetroArch runs unstable with target ROM or ROM Core, try a different version; moving forward to Nigthies or backwards to older versions may work better.

## Install Cores

Go to Load Core > Download a Core and Select the ones to install

For Reference, these seem to work best for their platform:

- Arcade: MAME
- NEC PC Engine & TurboGrafx-CD: Beetle PCE (Mednafen)
- Nintendo DS: Desume
- Game Boy Advance: mGBA
- Nintendo GameCube & Wii: Dolphin
- NES: Nestopia
- N64: Mupen64 (performance), ParaLLEl (accuracy)
- SNES: Snes9X (Current)
- Sega Dreamcast: Flycast
- Sega Master System/Genesis/CD: Genesis Plus GX
- *Maybe try this:* Sega MS/MD/CD/32X: PicoDrive; or also use Genesis Plus GX TODO: test this core
- PS1: Beetle PSX HW

## Load Games

Load Games into Collections, ie per console platform.

__Note:__ May Skip step if using LaunchBox for all game launch.

From Main Menu: Import Content icon, select Scan Directory -> Parent Directory or Directories of ROMs.

## Controller Setup

Plug in the controller and check OS detects it properly or install any drivers necessary.

Most controllers are setup and mapped properly at this point and no further setup needed. 

__Note__: Else send comment to me with your problems.

## Tweaks for Graphics & Sound

First set the maximum / best graphics & sound preferences for your Computer Spec. I change "Global" Settings > Drivers > Video from  gl to vulkan.

Current setup defaults to GL (OpenGL) which works with most Cores. For "newer" or "more advanced" Cores, Vulkan may be preferred. In other words, I prefer, if Vulkan works fine it can look better or give better performance; if it creates problems, default back to GL.

For Core specific settings, Load the Core first. TODO.

TODO : Graphics, Plugins and other tweaks & Shaders (For each Core or Game, override using...); Frames & Latency settings.

## Launchbox extra frontend

Download Launchbox from: <https://www.launchbox-app.com/download> (Must register email for download, Latest version 10.7).

Install Launch Box into user directory (not Program Files) defaults to: C:\Users\XXX\LaunchBox .

In Launchbox, Go to Tools > Manage Emulators > Add. In the 'Emulator Name' box, select Retroarch from the dropdown menu, then point the 'Emulator Application Path' box to the directory of Retroarch.exe.

### Import Console Games

Import games to Launchbox: Go to Tools -> Import -> Rom Files and follow the wizard.

### Import Steam Games

Import Steam games to Launchbox: Go to Tools -> Import -> Steam Games

Input user name as id: *url set here*
API Key, either use existing or create a new one with a Domain.

## AI Service Setup 

TODO: registration & setup


## Updating RetroArch & Other Components

TODO: Everything.