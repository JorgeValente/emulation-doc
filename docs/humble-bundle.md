# Humble Bundle: download a whole bundle in one go

Ebook and comic bundles can hold dozens of files in several formats. Instead of clicking every link, one small program downloads the whole bundle into its own folder, on the Windows PC.

The tool is **[humble-cli](https://github.com/smbl64/humble-cli)**: free, open source, a single `.exe` with nothing else to install. A launcher file, `Download Humble Bundle.bat`, asks the questions so you never type commands.

```
Downloads\
└── <bundle name>\
    ├── <book or comic 1>\   one folder per item, e.g. book.epub, book.pdf
    ├── <book or comic 2>\
    └── ...
```

- Files you already have are skipped, and half-finished downloads continue where they stopped. Running the same bundle again is safe and only fetches what is missing.
- Steam keys are not downloaded. The launcher lists them and shows whether each one is redeemed; you redeem them at [humblebundle.com/home/keys](https://www.humblebundle.com/home/keys).
- Downloads go to the Windows Downloads folder, even if it was moved to another drive.

## 1. Install (once)

1. Make a folder for it, here `C:\Users\jorgi\OneDrive\ClaudeOutputs\humble-cli`.
2. From the [latest release](https://github.com/smbl64/humble-cli/releases/latest), download `humble-cli-windows-amd64.exe.zip`, unzip it into that folder and rename the file to `humble-cli.exe`.
3. Put `Download Humble Bundle.bat` (below) in the same folder. Pin it to Start or make a desktop shortcut if you like.

Use version 2.0 or later. Humble changed its login, and older versions can no longer sign in.

## 2. Sign in (first time, and when it expires)

The launcher asks for this on its first run, or when you answer **y** after an "Unauthorized (401)" error.

1. Log in at [humblebundle.com](https://www.humblebundle.com) in Chrome or Edge.
2. Press **F12**, open the **Application** tab, then **Cookies** > `https://www.humblebundle.com`.
3. Find the cookie whose name starts with `ory_session_`. Paste its **name** and then its **value** into the launcher.

In Firefox it is **F12** > **Storage** > **Cookies**.

The cookie works like your password, so never share it. It is saved in `C:\Users\jorgi\.humble-cli-key`. Delete that file to sign out.

## 3. Download a bundle

1. Double-click `Download Humble Bundle.bat`.
2. Paste the bundle's download link (the `humblebundle.com/downloads?key=...` link from the purchase email or your library), or press **Enter** to list all your bundles and copy a key from there.
3. It shows what's in the bundle, including Steam keys.
4. Type the formats you want, e.g. `epub pdf`, or press **Enter** for everything.
5. When it's done, the Downloads folder opens. Paste another link, or type **Q** to quit.

## Commands, if you ever need them

Run these from the humble-cli folder:

| Task | Command |
| --- | --- |
| List bundles | `humble-cli list` (slow on big libraries, because it also checks keys) |
| Bundles with unclaimed keys | `humble-cli list --claimed no` |
| What's in a bundle | `humble-cli details <key>` |
| Download, only some formats | `humble-cli download <key> -f epub -f pdf` |
| Download only some items | `humble-cli download <key> -i 1,3,5-10` |

A key can be shortened to its first few characters, as long as no other bundle starts the same way.

## The launcher

Save this as `Download Humble Bundle.bat`, next to `humble-cli.exe`:

```bat
@echo off
setlocal
title Download Humble Bundle
rem Downloads every file of a Humble Bundle into Downloads\<bundle name>.
rem Needs humble-cli.exe in the same folder as this file.
rem Files already downloaded are skipped; half-finished ones are resumed.

set "HC=%~dp0humble-cli.exe"
if exist "%HC%" goto finddl
echo humble-cli.exe was not found next to this file.
pause
exit /b 1

:finddl
rem Find the real Downloads folder, even if it was moved to another drive.
set "DL="
for /f "usebackq delims=" %%D in (`powershell -NoProfile -Command "(New-Object -ComObject Shell.Application).NameSpace('shell:Downloads').Self.Path"`) do set "DL=%%D"
if not defined DL set "DL=%USERPROFILE%\Downloads"
echo Downloads go to: %DL%

if not exist "%USERPROFILE%\.humble-cli-key" goto login
goto ask

:login
echo.
echo === Sign in (first time, or when the sign-in has expired) ===
echo 1. Open humblebundle.com in your browser and make sure you are logged in.
echo 2. Press F12, open the Application tab, then Cookies ^> https://www.humblebundle.com
echo 3. Find the cookie whose name starts with ory_session_
echo.
set "CNAME="
set "CVAL="
set /p "CNAME=Paste the cookie NAME:  "
set /p "CVAL=Paste the cookie VALUE: "
if not defined CNAME goto login
if not defined CVAL goto login
"%HC%" auth "%CNAME%=%CVAL%"
if errorlevel 1 goto login
echo Saved.

:ask
echo.
set "INPUT="
set /p "INPUT=Paste the bundle's download link or key (just Enter = list my bundles, Q = quit): "
if not defined INPUT goto list
if /i "%INPUT%"=="q" exit /b 0

rem Accept a full link like https://www.humblebundle.com/downloads?key=XXXX or a bare key.
set "KEY=%INPUT%"
echo "%INPUT%" | find /i "key=" >nul && set "KEY=%INPUT:*key=%"
for /f "tokens=1 delims=&=# " %%K in ("%KEY%") do set "KEY=%%K"

echo.
"%HC%" details "%KEY%"
if errorlevel 1 goto failed

echo.
set "FMT="
set /p "FMT=Formats to download, e.g. epub pdf (just Enter = everything): "
pushd "%DL%"
if defined FMT goto withfmt
"%HC%" download "%KEY%"
goto afterdl
:withfmt
set "FMT=%FMT: =,%"
"%HC%" download "%KEY%" -f "%FMT%"
:afterdl
set "RC=%errorlevel%"
popd
if not "%RC%"=="0" goto failed
echo.
echo Done. The bundle is in its own folder inside %DL%
start "" "%DL%"
goto ask

:list
"%HC%" list --field key --field name
if errorlevel 1 goto failed
goto ask

:failed
echo.
echo Something went wrong (see the message above).
echo "Unauthorized (401)" means the sign-in expired.
set "ANS="
set /p "ANS=Sign in again now? (y/n): "
if /i "%ANS%"=="y" goto login
goto ask
```
