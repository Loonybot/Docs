# Disabling Sidekick

Sometimes, you may want to disable **Sidekick** on the robot without fully removing its library.
Although it is legal to have it enabled for FTC competitions, and even though it is designed to have minimal impact on your code's performance, it may sometimes cause unexpected behavior from its many system hooks, or it might simply have a bug that prevents your code from operating correctly.

As such, there are two ways to disable **Sidekick**'s library.

## 1. Disable With UI
**Sidekick** automatically adds an opMode called _Enable/Disable Sidekick_ to your list of opModes. Run it and press ▶ on the Driver Station to toggle its mode.

## 2. Disable With API
**Sidekick** can be disabled via a call to `Sk.disable()` from your robot code. Because **Sidekick** needs to know this state early in the boot process, you can only call `Sk.disable()` (or `Sk.enable()`) from a method marked with the `@OnCreate` annotation, like this:

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
    Be very careful of any code placed within the `@OnCreate` method as it executes during robot startup. If it raises an uncaught exception, it will cause an endless cycle of reboots and you'll need to reset the robot using a method such as the `REV Hardware Client`.
