# Native macOS windows and game identity

This experiment uses Highball `01743aeb` and the x86_64 [CrossOver 26.3 r31 engine](../../spike/engines/x64-crossover26.3-r31.json). The engine changes are recorded as source patches for a local test build.

- [Steam window](patches/steam-native-frame.patch): pass Steam's unowned main `steamwebhelper.exe` / `SDL_app` window through Wine's existing frame handling when its window and visible bounds match. AeroSpace classified the result as an `AXStandardWindow` on a workspace. This patch does not change other windows or rename Steam.
- [Game identity](patches/steam-game-identity.patch): select a named Mac app bundle when Wine creates a child for an exact Windows executable path. Highball prepares the mapping before Steam Play from the installed game's launch entries in `appinfo.vdf`. The Mac bundle has a Steam app ID, the game's name and its PE icon when available. Steam itself retains its existing process identity.

## Rebuild the test engine

1. Start from [the CrossOver 26.3.0 sources](https://media.codeweavers.com/pub/crossover/source/crossover-sources-26.3.0.tar.gz). Follow the [r31 build workflow](https://github.com/gauthierpiarrette/highball-engine/actions/runs/41808353728) at highball-engine commit `09ceb3335b4fe6170c8d5b4b293663e5ffb5f268` to apply the upstream Wine patch series. Apply the two experiment patches with `patch -p1` from the Wine source root (`sources/wine`).
2. Build the x86_64 Wine Unix modules `dlls/winemac.drv/winemac.so` and `dlls/ntdll/ntdll.so`. The test used the r31 runtime and overlays with just these two modules replaced. Compare their exported symbols and linked libraries with r31 before copying them into the engine's `lib/wine/x86_64-unix` directory.
3. Put the modified engine in an isolated `HIGHBALL_HOME`. Give its directory and manifest the ID `x64-crossover26.3-r31-native-identity`, and set `"nativeGameIdentity": true` in that manifest. Point the test environment at the new engine. Stock manifests omit the capability and keep the existing launch path.
4. Run `swift build && swift test`, then `Scripts/make-app.sh debug` to bundle this branch. Run the app with the test `HIGHBALL_HOME`. Keep the engine and its generated game bundles in a writable directory under Application Support. In the previous test, a bundle under Documents could not load `libhbaudiobuf.dylib` when launched by Wine.

This branch carries the patches for review and reproduction. An upstream submission would put the Wine changes in highball-engine and point Highball at a separately built engine. The current experiment covers Rosetta x86_64; native ARM64 is outside this test.

Continue with the [test plan](test-plan.md).
