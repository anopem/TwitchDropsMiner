# Twitch Drops Miner (for Docker)

This application allows you to AFK mine timed Twitch drops, without having to worry about switching channels when the one you were watching goes offline, claiming the drops, or even receiving the stream data itself. This helps you save on bandwidth and hassle. It also only builds the AppImage for linux, for that reason.

> This is a fork of [DevilXD/TwitchDropsMiner](https://github.com/fireph/TwitchDropsMiner) with some personal QOL improvements

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

> [!WARNING]
> Go to [DevilXD/TwitchDropsMiner](https://github.com/fireph/TwitchDropsMiner) to learn about how to run it in Docker. DO NOT report any Docker issues to [DevilXD/TwitchDropsMiner](https://github.com/DevilXD/TwitchDropsMiner)!

> [!TIP]
> [DevilXD/TwitchDropsMiner](https://github.com/DevilXD/TwitchDropsMiner) Original repository.
> 
> [fireph/TwitchDropsMiner](https://github.com/fireph/TwitchDropsMiner) Docker repository.

### Credits:

<!---
Note: The translations credits are sorted alphabetically, based on their English language name.
When adding a new entry, please ensure to insert it in the correct place in the second section.
Non-translations related credits should be added to the first section instead.

Note: When adding a new credits line below, please add two trailing spaces at the end
of the previous line, if they aren't already there. Doing so ensures proper markdown
rendering on Github. In short: Each credits line should end with two trailing spaces,
placed past the period character at the end.

• Last line can have the two trailing spaces omitted.
• Please ensure your editor won't trim the trailing spaces upon saving the file.
• Please ensure to leave a single empty new line at the end of the file.
-->

@DevilXD - Creating and maintaining the project.  
@fireph - Creating the Docker version.  

@guihkx - For the CI script, CI maintenance, and everything related to Linux builds.  
@kWAYTV - For the implementation of the dark mode theme.  

@Bamboozul - For the entirety of the Arabic (العربية) translation.  
@Suz1e - For the entirety of the Chinese (简体中文) translation and revisions.  
@wwj010 - For the Chinese (简体中文) translation corrections and revisions.  
@zhangminghao1989 - For the Chinese (简体中文) translation corrections and revisions.  
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
@Patriot99 - For the Polish (Polski) translation and revisions (co-authored with @DevilXD).  
@zarigata - For the entirety of the Portuguese (Português) translation.  
@Sergo1217 - For the entirety of the Russian (Русский) translation.  
@kilroy98 - For the Russian (Русский) translation corrections and revisions.  
@Shofuu - For the entirety of the Spanish (Español) translation and revisions.  
@alikdb - For the entirety of the Turkish (Türkçe) translation.  
@Nollasko - For the entirety of the Ukrainian (Українська) translation and revisions.  
@kilroy98 - For the Ukrainian (Українська) translation corrections and revisions.  
