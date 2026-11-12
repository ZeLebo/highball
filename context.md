# Native macOS windows experiment

This branch records a test build based on Highball `01743aeb` and the x86_64 CrossOver 26.3 r31 engine. Start with the [test plan](experiments/native-macos/test-plan.md). The [build notes](experiments/native-macos/README.md) explain how the app changes and the two Wine patches fit together.

**Status: acceptance is open.** Buckshot Roulette passed direct launch, window and identity checks, but flickers in Vulkan Forward+. Bloody Hell showed the correct name and icon in Dock and Vorssaint when launched from Windows Steam. It did not pass launch from Highball or the window controls check.

- [Cold Steam launch takes too long](issues/steam-cold-launch.md)
- [Buckshot Roulette flickers in Vulkan Forward+](issues/buckshot-vulkan-flicker.md)

The stock engine and the main branch are unchanged. The experiment is ready for another test pass before proposing upstream changes.
