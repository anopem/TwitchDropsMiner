# Twitch Drops Miner (for Docker)

This application allows you to AFK mine timed Twitch drops, without having to worry about switching channels when the one you were watching goes offline, claiming the drops, or even receiving the stream data itself. This helps you save on bandwidth and hassle. This is a fork of [fireph](https://github.com/fireph/docker-twitch-drops-miner). 

This fork brings some quality of life features that i personally felt missing.

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

> [!NOTE]
> Symbola font is needed to render the arrows on the settings page. The buttons use very rare unicode characters and most fonts do not have them.

> [!WARNING]
> Anything below this point is for running the application normally, NOT in docker. Go to [fireph](https://github.com/fireph/docker-twitch-drops-miner) to learn about how to run it in Docker. DO NOT report any Docker issues to [DevilXD](https://github.com/DevilXD/TwitchDropsMiner)!

### How It Works:

Every several seconds, the application pretends to watch a particular stream by fetching stream metadata - this is enough to advance the drops. Note that this completely bypasses the need to download any actual stream video and sound. To keep the status (ONLINE or OFFLINE) of the channels up-to-date, there's a websocket connection established that receives events about streams going up or down, or updates regarding the current amount of viewers.

### Support

### DevilXD
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

@Bamboozul - For the entirety of the Arabic (العربية) translation.  
@Suz1e - For the entirety of the Chinese (简体中文) translation and revisions.  
@wwj010, @zhangminghao1989, @Self4215 - For the Chinese (简体中文) translation corrections and revisions.  
@Ricky103403 - For the entirety of the Traditional Chinese (繁體中文) translation.  
@LusTerCsI - For the Traditional Chinese (繁體中文) translation corrections and revisions.  
@nwvh - For the entirety of the Czech (Čeština) translation.  
@Kjerne - For the entirety of the Danish (Dansk) translation.  
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
