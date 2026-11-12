# Buckshot Roulette shows flickering squares in Vulkan Forward+

Buckshot Roulette (`2835570`) starts from Highball and its window, Dock identity and sound entry work. Moving squares still flicker in the game scene in windowed mode.

The launch log lists `renderer=dxmt`. The game log identifies Godot 4.1.1 and `Vulkan API 1.2.357 - Forward+`. Changing Highball's Direct3D graphics mode did not remove the artifacts. With `--rendering-driver opengl3`, the menu opened, then the game crashed on entering a round. The logs include a `ParticlesCopyShaderGLES3` vertex shader compilation failure and a Wine access violation. The cause of the flicker and the relation between those errors are unconfirmed.

To isolate the regression, compare the same scene on stock r31 and the experiment with the same resolution and Vulkan mode. Record the game log and a short capture in each case. A fix should remove the artifacts during a playable round and keep the game stable. Until then, use a second Windows title to test window behavior.

See the [test plan](../experiments/native-macos/test-plan.md).
