# Usage

## Don't Turn Off the Robot While an OpMode is Running
**Sidekick** has to hook opMode termination in order to successfully save its logs. 
If you turn off the robot while an opMode is still running, all of the Sidekick data for that run will be lost, except for Logcat data. It's best practice to always press stop (⏹) on the Driver Station once an opMode is complete, before turning off the robot. Autonomous opModes that properly terminate are not a problem, and for TeleOp opModes Sidekick will automatically stop capturing and save its files two minutes and one second after Start (▶) is pressed.

## If You Hit a Sidekick Bug
If you have a `.sidekick` capture file that causes **Sidekick** to crash, please email it to [bugreport@loonybot.com](mailto:bugreport@loonybot.com) along with a description of the problem. 
We hate crashes but love bug reports that can reproduce them, so we always make it our top priority to fix such bugs when we get them. 
However, please consider your privacy: **Sidekick** itself does not save any _Personally Identifiable Information_, but your opMode may output PII to the data that is recorded.
Please be sure to send us only the `.sidekick` file and none of the video files.

Bugs and suggestions can also be filed on [GitHub](https://github.com/Loonybot/SidekickRC/issues).

## Disabling Sidekick
Sometimes, you may want to disable **Sidekick** on the robot without fully removing its library.
Although it is legal to have it enabled for FTC competitions, and even though it is designed to have minimal impact on your code's performance, it may sometimes cause unexpected behavior from its many system hooks, or it might simply have a bug that prevents your code from operating correctly.

As such, there are two ways to disable **Sidekick**'s library.

### 1. Disable With UI
**Sidekick** automatically adds an opMode called _Enable/Disable Sidekick_ to your list of opModes. Run it and press ▶ on the Driver Station to toggle its mode.

### 2. Disable With API
**Sidekick** can be disabled by a call to `Sk.disable()` from your robot code. Because **Sidekick** needs to know this state early in the boot process, you can only call `Sk.disable()` (or `Sk.enable()`) from a method marked with the `@OnCreate` annotation, like this:

```Java title="Disable Sidekick"
@SuppressWarnings("unused")
class ConfigureSidekick {
    @OnCreate
    public static void onCreate(Context context) {
        Sk.disable(); // Temporarily disable Sidekick
    }
}
```

This `@OnCreate` declaration can appear anywhere in your code and will apply globally to all of your opModes. 
!!! warning
    Be very careful of any code placed within the `@OnCreate` method as it executes during robot startup. If it raises an uncaught exception, it will cause an endless cycle of reboots and you'll need to reset the robot via means such as the `REV Hardware Client`.


