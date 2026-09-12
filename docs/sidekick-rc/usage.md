# Usage

## Don't turn off the robot while an opMode is running
**Sidekick** has to hook opMode termination in order to successfully save its logs. 
If you turn off the robot while an opMode is still running, all of the Sidekick data for that run will be lost, except for Logcat data. It's best practice to always press stop (⏹) on the Driver Station once an opMode is complete, before turning off the robot. Autonomous opModes that properly terminate are not a problem, and for TeleOp opModes Sidekick will automatically stop capturing and save its files two minutes and one second after Start (▶) is pressed.

## Sidekick saves can be composed of multiple files
When you save a file in **Sidekick**, the bulk of the data is stored in a file with a `.sidekick` file extension while videos are kept as separate files. 
So if, for example, you saved your capture as "Test1" and it had a Limelight video along with an imported spectator video, you would get three files with the following names:

- Test1.sidekick
- Test1 limelight.lvc
- Test1 spectator.mp4

When **Sidekick** loads a `.sidekick` file, it looks for the companion video files in the same directory with the same root name.
As such, if you use the Operating System to copy or move your capture, copy or move all of the component files together. 
If you use the OS to rename your capture, rename all of the component files similarly. 
If **Sidekick** can't find a companion video file, the capture can still be analyzed but the video won't be viewable.

## How to disable Sidekick
Sometimes, you may want to disable **Sidekick** on the robot without fully removing its library.
Although it is legal to have it enabled for FTC competitions, and even though it is designed to have minimal impact on your code's performance, it may sometimes cause unexpected behavior from its many system hooks, or it might simply have a bug that prevents your code from operating correctly.

As such, there are two ways to disable **Sidekick**'s library.

### 1. Disable with UI
**Sidekick** automatically adds an opMode called _Enable/Disable Sidekick_ to your list of opModes. Run it and press Start (▶) on the Driver Station to toggle its mode.

### 2. Disable with API
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


