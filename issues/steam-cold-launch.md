# Measure slow game launch when Steam is closed

With the Windows Steam client closed, clicking **Play** in Highball can take a long time before a game shows a usable window. The delay has not been timed. A Steam handoff or live game process does not establish when the game became usable.

Compare cold and warm launches of the same installed game in the same environment and renderer. Take at least three measurements of each. Separate first-run Steam updates and game prerequisites. Record time from **Play** to Steam startup, game process creation and the first usable frame. Note whether Highball reused or restarted Steam and why.

Use the timings to locate the delay. Check whether repeated launches spend time on an avoidable client restart, preparation before the handoff, Steam initialization or the game itself. Keep a warm client when its configuration matches. Compare the same measurements after any change and recheck sign-in, first-run setup and exit.

See the [test plan](../experiments/native-macos/test-plan.md).
