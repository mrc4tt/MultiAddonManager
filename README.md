# MultiAddonManager

A MetaMod plugin that allows you to use multiple workshop addons at once and have clients download them.

## ConVars
- `mm_extra_addons <ids>` The workshop IDs of extra addons separated by commas, addons will be downloaded (if not present) and mounted (e.g. "3090239773,3070231528").
  Once downloads are done, the map is automatically reloaded so content can be precached.
- `mm_client_extra_addons <ids>` The workshop IDs of extra client-side only addons that will be loaded by all clients, separated by commas. These addons are not loaded or downloaded by the server.
  Changes will only apply to future clients.

- `mm_extra_addons_timeout <seconds> (default 10)` How long until clients are timed out in between connects for extra addons, timed out clients will reconnect for their current pending download.
- `mm_addon_connection_timeout <seconds> (default 30)` // How long until clients are timed out while downloading the first required addon (usually the current map), 0 disables
- `mm_print_searchpaths` Print all the search paths currently mounted by the server.
- `mm_addon_mount_download <0/1> (default 0)` If enabled, the plugin will initiate an addon download every time even if it's already installed, this will guarantee that updates are applied immediately.
- `mm_cache_clients_with_addons <0/1> (default 0)` If enabled, the plugin will keep track of which addons client SteamIDs have downloaded to prevent sending them addons when they already have them (i.e. when they rejoin or the map changes).
- `mm_cache_clients_duration <0/seconds> (default 0)` How long to cache clients' downloaded addons list, pass 0 for forever.
- `mm_block_disconnect_messages <0/1> (default 0)` If enabled, the plugin will block *ALL* disconnect events with the "loop shutdown" reason. This will prevent disconnect chat messsages whenever someone reconnects because they're getting an addon.
- `mm_addon_debug <0/1> (default 0)` Whether to print some extra debug information (mainly when clients are joining)

## Commands
- `mm_download_addon <id>` Download an addon manually.

 Both of these commands require a map reload to apply changes.
- `mm_add_addon <id>` Add an addon to the list, but don't mount.
- `mm_remove_addon <id>` Remove an addon from the list, but don't unmount.

 These following commands will only affect future clients:
- `mm_add_client_addon <id>` Add a workshop ID to the global client-only addon list.
- `mm_remove_client_addon <id>` Remove a workshop ID from the global client-only addon list.

## Usage in other MetaMod plugins
- Include the [public header](https://github.com/mrc4tt/MultiAddonManager/blob/main/public/imultiaddonmanager.h).
- Query the interface in `AllPluginsLoaded` like this:
```cpp
IMultiAddonManager *pInterface = (IMultiAddonManager*)g_SMAPI->MetaFactory(MULTIADDONMANAGER_INTERFACE, nullptr, nullptr);
```

## Installation

- Install [Metamod](https://cs2.poggu.me/metamod/installation/)
- Download the package for your server from the [latest release](https://github.com/mrc4tt/MultiAddonManager/releases/latest) (see [Which download?](#which-download) below)
- Extract the package contents into `game/csgo` on your server
- Edit the config file at `game/csgo/cfg/multiaddonmanager/multiaddonmanager.cfg`

### Which download?

Every [release](https://github.com/mrc4tt/MultiAddonManager/releases/latest) has three packages:

| Package | For |
| --- | --- |
| `MultiAddonManager-<version>-steamrt3.tar.gz` | Linux servers. The CS2 dedicated server runs in Steam Runtime 3 ("sniper"); this build loads there, in Steam Runtime 4 and on any newer distribution. **Take this one if unsure.** |
| `MultiAddonManager-<version>-steamrt4.tar.gz` | Linux servers that run in Steam Runtime 4. |
| `MultiAddonManager-<version>-windows.zip` | Windows servers. |

The top of each release lists the exact glibc and libstdc++ every Linux build needs and the distributions it loads on. A build that is too new for the server fails at load time with `version 'GLIBC_2.xx' not found` in the console.

## Support

Need help, found a bug, or have a feature idea? Join the Discord support server:

[![Discord](https://img.shields.io/badge/Discord-Join%20the%20server-5865F2?logo=discord&logoColor=white)](https://discord.gg/zuQN3U2ZEh)

- **Questions and setup help:** ask in the support channels on Discord.
- **Bug reports:** open a [GitHub issue](https://github.com/mrc4tt/MultiAddonManager/issues) with your server log, plugin version and steps to reproduce. Discord is fine for a quick check first.
- **Feature requests:** post them on Discord or open an [issue](https://github.com/mrc4tt/MultiAddonManager/issues).

Please do not send support requests by direct message. Asking in the public channels means others can help and find the answer later.
