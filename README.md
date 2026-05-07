<div align="center">

![Twitch Drops Miner Icon](https://raw.githubusercontent.com/DevilXD/TwitchDropsMiner/master/appimage/pickaxe.png)

# Twitch Drops Miner (for Docker)

This application allows you to AFK mine timed Twitch drops, without having to worry about switching channels when the one you were watching goes offline, claiming the drops, or even receiving the stream data itself. This helps you save on bandwidth and hassle. 

This is a fork of [fireph](https://github.com/fireph/docker-twitch-drops-miner)'s version, that brings some quality of life features that i personally felt missing.

[![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/anopem/TwitchDropsMiner/ci.yml?style=for-the-badge&logo=python&logoColor=white)](https://github.com/anopem/TwitchDropsMiner/actions/workflows/ci.yml) [![GitHub](https://img.shields.io/badge/GitHub-Repository-blue?style=for-the-badge&logo=github)](https://github.com/anopem/docker-twitch-drops-miner)
</div>

### Docker Fork Modifications:
This fork has been specifically modified for Docker deployment with the following key changes:
- **System tray removed** - All system tray functionality has been disabled and runtime dependencies removed
- **Console logging** - Added `--stdlog` command line option to output logs to stdout/stderr
- **Streamlined settings** - Moved settings into ./config folder
- **AppImage only** - Build process modified to only generate Linux AppImage builds
- **Automated upstream sync** - Workflow to automatically merge updates from the upstream repository
- **Enhanced error handling** - Improved error messages when settings files can't be loaded
- **Login URL management** - Login URLs are copied to clipboard
- **About tab links** - Repository URL updated in about tab
- **Web UI** - Added web-based interface via NiceGUI, see [webui/README.md](webui/README.md)

> [!WARNING]
> Anything below this point is for running the application normally, NOT in docker. Go to https://github.com/fireph/docker-twitch-drops-miner to learn about how to run it in Docker. DO NOT report any Docker issues to https://github.com/DevilXD/TwitchDropsMiner!

### How It Works:

Every several seconds, the application pretends to watch a particular stream by fetching stream metadata - this is enough to advance the drops. Note that this completely bypasses the need to download any actual stream video and sound. To keep the status (ONLINE or OFFLINE) of the channels up-to-date, there's a websocket connection established that receives events about streams going up or down, or updates regarding the current amount of viewers.

### Features:

- Stream-less drop mining - save on bandwidth.
- Game priority and exclusion lists, allowing you to focus on mining what you want, in the order you want, and ignore what you don't want.
- Sharded websocket connection, allowing for tracking up to `199` channels at the same time.
- Automatic drop campaigns discovery based on linked accounts (requires you to do [account linking](https://www.twitch.tv/drops/campaigns) yourself though).
- Stream tags and drop campaign validation, to ensure you won't end up mining a stream that can't earn you the drop.
- Automatic channel stream switching, when the one you were currently watching goes offline, as well as when a channel streaming a higher priority game goes online.
- Login session is saved in a cookies file, so you don't need to login every time.
- Mining is automatically started as new campaigns appear, and stopped when the last available drops have been mined.

### Usage:

- Download and unzip [the latest release](https://github.com/DevilXD/TwitchDropsMiner/releases) - it's recommended to keep it in the folder it comes in.
- Run it and login/connect the miner to your Twitch account by using the in-app login form.
- After a successful login, the app should fetch a list of all available campaigns and games you can mine drops for - you can then select and add games of choice to the Priority List available on the Settings tab, and then press on the `Reload` button to start processing. It will fetch a list of all applicable streams it can watch, and start mining right away. You can also manually switch to a different channel as needed.
- If you wish to keep the miner occupied with mining anything it can, beyond what you've selected via the Priority List, you can use the Priority Mode setting to specify the mining order for the rest of the games.
- Make sure to link your Twitch account to game accounts on the [campaigns page](https://www.twitch.tv/drops/campaigns), to enable more games to be mined.

### Pictures:

![Main](https://user-images.githubusercontent.com/4180725/164298155-c0880ad7-6423-4419-8d73-f3c053730a1b.png)
![Inventory](https://user-images.githubusercontent.com/4180725/164298315-81cae0d2-24a4-4822-a056-154fd763c284.png)
![Settings](https://user-images.githubusercontent.com/4180725/164298391-b13ad40d-3881-436c-8d4c-34e2bbe33a78.png)

### Notes:

> [!WARNING]  
> Due to how Twitch handles the drop progression on their side, watching a stream in the browser (or by any other means) on the same account that is actively being used by the miner, will usually cause the miner to misbehave, reporting false progress and getting stuck mining the current drop.  
> 
> Using the same account to watch other streams during mining is thus discouraged, in order to avoid any problems arising from it.

> [!CAUTION]  
> Persistent cookies will be stored in the `cookies.jar` file, from which the authorization (login) information will be restored on each subsequent run. Make sure to keep your cookies file safe, as the authorization information it stores can give another person access to your Twitch account, even without them knowing your password!

> [!IMPORTANT]  
> Successfully logging into your Twitch account in the application may cause Twitch to send you a "New Login" notification email. This is normal - you can verify that it comes from your own IP address. The detected browser during the login will be "Chrome", as that's what the miner currently presents itself to the Twitch server.

> [!NOTE]  
> The time remaining timer always countdowns a single minute and then stops - it is then restarted only after the application redetermines the remaining time. This "redetermination" can happen at any time Twitch decides to report on the drop's progress, but not later than 20 seconds after the timer reaches zero. The seconds timer is only an approximation and does not represent nor affect actual mining speed. The time variations are due to Twitch sometimes not reporting drop progress at all, or reporting progress for the wrong drop - these cases have all been accounted for in the application though.

> [!NOTE]  
> The source code requires Python 3.10 or higher to run.

### Notes about the Windows build:

- To achieve a portable-executable format, the application is packaged with PyInstaller into an `EXE`. Some antivirus engines (including Windows Defender) might report the packaged executable as a trojan, because PyInstaller has been used by others to package malicious Python code in the past. These reports can be safely ignored. If you absolutely do not trust the executable, you'll have to install Python yourself and run everything from source.
- The executable uses the `%TEMP%` directory for temporary runtime storage of files, that don't need to be exposed to the user (like compiled code and translation files). For persistent storage, the directory the executable resides in is used instead.
- The autostart feature is implemented as a registry entry to the current user's (`HKCU`) autostart key. It is only altered when toggling the respective option. If you relocate the app to a different directory, the autostart feature will stop working, until you toggle the option off and back on again

### Notes about the Linux build:

- The Linux app is built and distributed using two distinct portable-executable formats: [AppImage](https://appimage.org/) and [PyInstaller](https://pyinstaller.org/).
- There are no major differences between the two formats, but if you're looking for a recommendation, use the AppImage.
- The Linux app should work out of the box on any modern distribution, as long as it has `glibc>=2.35`, plus a working display server.
- Every feature of the app is expected to work on Linux just as well as it does on Windows. If you find something that's broken, please [open a new issue](https://github.com/DevilXD/TwitchDropsMiner/issues/new).
- The size of the Linux app is significantly larger than the Windows app due to the inclusion of the `gtk3` library (and its dependencies), which is required for proper system tray/notifications support.
- As an alternative to the native Linux app, you can run the Windows app via [Wine](https://www.winehq.org/) instead. It works really well!

### Notes about the macOS build:

- The macOS version is packaged using PyInstaller into a standalone `.app` bundle, distributed as a ZIP archive.
- Since this application is not signed with a paid Apple Developer Certificate, **macOS Gatekeeper will block it** on the first run (saying it "The application is damaged and can't be opened").
  - **To fix this**: Either open the Terminal in the folder the app is in (or navigating with `cd path/to/folder`) and enter `xattr -cr Twitch Drops Miner (by DevilXD).app` or just type `xattr -cr ` (make sure to put a space at the end), drag and drop the `Twitch Drops Miner (by DevilXD).app` file into the terminal window (this will auto-fill the path) and enter
- Persistent files (like `cookies.jar`, `settings.json`, `lock.file` and the `cache` folder) are stored inside the application bundle in `Twitch Drops Miner (by DevilXD).app/Contents/MacOS` (to access them Right-click the application and select `Show Package Contents`)

### Advanced Usage:

If you'd be interested in running the latest master from source or building your own executable, see the wiki page explaining how to do so: https://github.com/DevilXD/TwitchDropsMiner/wiki/Setting-up-the-environment,-building-and-running

### Support

If you'd encounter any issues with the miner:

- Please see the [troubleshooting page](https://github.com/DevilXD/TwitchDropsMiner/wiki/Troubleshooting) for some common issues and their explanation.  
- Please [search the issues page](https://github.com/DevilXD/TwitchDropsMiner/issues?q=sort%3Aupdated-desc%20is%3Aissue) to see if your issue hasn't been reported yet.  
- If it's not been reported yet, feel free to open a new issue, describing your problem.

If you like the application and found it useful, please consider donating a small amount of money to support me. Thank you!

<div align="center">

[![Buy me a coffee](https://i.imgur.com/cL95gzE.png)](
    https://www.buymeacoffee.com/DevilXD
)
[![Support me on Patreon](https://i.imgur.com/Mdkb9jq.png)](
    https://www.patreon.com/bePatron?u=26937862
)

</div>


@DevilXD - Creating the miner and maintaining it.

@fireph - Converting the original application to docker.

@guihkx - For the CI script, CI maintenance, and everything related to Linux builds.  
@kWAYTV - For the implementation of the dark mode theme.  
@crocchetto - For the macOS port.  

@Bamboozul - For the entirety of the Arabic (العربية) translation.  
@Suz1e - For the entirety of the Chinese (简体中文) translation and revisions.  
@wwj010, @zhangminghao1989, @Self4215 - For the Chinese (简体中文) translation corrections and revisions.  
@Ricky103403 - For the entirety of the Traditional Chinese (繁體中文) translation.  
@LusTerCsI - For the Traditional Chinese (繁體中文) translation corrections and revisions.  
@nwvh - For the entirety of the Czech (Čeština) translation.  
@Kjerne - For the entirety of the Danish (Dansk) translation.  
@lmdpocus - For the entirety of the Dutch (Nederlandse) translation.  
@Rensoraa - For the Traditional Dutch (Nederlandse) translation corrections and revisions.  
@roobini-gamer - For the entirety of the French (Français) translation.  
@Calvineries - For the French (Français) translation revisions.  
@ThisIsCyreX - For the entirety of the German (Deutsch) translation.  
@Eriza-Z - For the entirety of the Indonesian translation.  
@casungo - For the entirety of the Italian (Italiano) translation.  
@ShimadaNanaki - For the entirety of the Japanese (日本語) translation.  
@biroman -  For the entirety of the Norwegian (Norsk) translation.  
@Patriot99 - For the Polish (Polski) translation and revisions (co-authored with @DevilXD).  
@zarigata - For the entirety of the Portuguese (Português) translation.  
@Sergo1217 - For the entirety of the Russian (Русский) translation.  
@kilroy98, @flamesv - For the Russian (Русский) translation corrections and revisions.  
@Shofuu - For the entirety of the Spanish (Español) translation and revisions.  
@Forero-0 = For the Spanish (Español) translation revisions.  
@alikdb - For the entirety of the Turkish (Türkçe) translation.  
@DogancanYr - For the Turkish (Türkçe) translation revisions.  
@Elderly-Emre - For the Turkish (Türkçe) translation revisions.  
@Nollasko - For the entirety of the Ukrainian (Українська) translation and revisions.  
@kilroy98 - For the Ukrainian (Українська) translation corrections and revisions.  
