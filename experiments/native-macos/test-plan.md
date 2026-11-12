# Acceptance plan for Windows Steam games

Use the isolated Highball build, the `Games` environment and DXMT. Record the build and engine IDs, macOS version, renderer, app ID and exact launch path for each run. Test the Windows Steam installation of each title.

## Current evidence

| Title | Launch and identity | Window and graphics |
| --- | --- | --- |
| Buckshot Roulette (`2835570`) | Highball Play reused the running Steam client. The game had its own name and icon in Dock and Vorssaint. | Windowed mode could move to a separate desktop and capture a window screenshot. Flickering squares remain in Vulkan Forward+. |
| Bloody Hell (`2056220`) | Highball sent `steam -applaunch 2056220`, but the tester did not get a usable window from Highball. Launch from Windows Steam worked; Dock and Vorssaint showed the game identity. | Windowed mode showed a macOS frame. The green fullscreen button was absent, moving the window in Mission Control failed, and the game did not close via the window controls. |
| Windows Steam | The client opened with DXMT. On WineD3D it showed a black window and logged three GPU process crashes. Dock still showed `wine` and the menu bar showed `steamwebhelper`. | AeroSpace classified the patched main window as a standard window. Retest capture of the Steam window with DXMT. |

## Next test pass

1. **Retest Bloody Hell from Highball.** Start with the game installed and Windows Steam closed. Click **Play** and record the times to Steam startup, game process creation and the first usable frame. Repeat with Steam open. If Play fails, preserve the launch log and test Play inside Steam as a separate control.
2. **Test another Windows title.** Start with [The Supper](https://store.steampowered.com/app/1171370/The_Supper/) (`1171370`, free, 280 MB required). Use [Unsorted Horror](https://store.steampowered.com/app/2433730/Unsorted_Horror/) (`2433730`, free, 1 GB required) as a second title for window and fullscreen checks. Check the game's own display settings; record an unavailable mode separately.
3. **Check the window.** In the game's windowed mode, move it between AeroSpace workspaces and between desktops in Mission Control. Check whether the green button can enter and exit macOS fullscreen. Separately test the game's own fullscreen mode and switching back with ⌘Tab. Capture a window screenshot with ⇧⌘4 then Space.
4. **Check identity and exit.** Verify the game name and icon in Dock and Vorssaint. Close it from the window and retest with the game's Quit command. Verify that the game exits, its audio entry disappears and Steam remains usable. Record each failure with the game mode and exact action.

Acceptance needs a second Windows title to open from Highball and pass the window checks. A frame, a live PID or a successful launch from inside Steam is partial evidence. Record cold launch latency and any graphics defects independently.
