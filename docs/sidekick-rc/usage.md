# Usage

## Typical development workflow
During robot development, a typical **Sidekick** workflow is:

1. Use the Connect button to establish a Wi-Fi and ADB connection between your laptop and the robot.
2. Use Android Studio to deploy a new build of your robot code.
3. Run your op mode and monitor current draw using **Sidekick**'s real-time graphing.
4. When the op mode is done, press the download button to import its captured data into **Sidekick** and analyze what happened.

## Sidekick automatically captures every op mode run
Captures are stored on your Robot Controller's internal storage. **Sidekick** will try to ensure that at least 100 MB of free space is available at the beginning of every op mode by deleting the oldest **Sidekick** captures to make room. You can also configure **Sidekick** to delete captures after a certain number of days via the [Sk.setRetentionDays()](api-reference.md#sksetretentiondays) API.

!!! warning
    Don't turn off the robot while an op mode is running. 
    **Sidekick** has to hook op mode termination in order to successfully save its logs. 
    If you turn off the robot while an op mode is still running, all of the Sidekick data for that run will be lost, except for Logcat data. It's best practice to always press stop (⏹) on the Driver Station once an op mode is complete, before turning off the robot. Autonomous op modes that properly terminate are not a problem, and for TeleOp op modes Sidekick will automatically stop capturing and save its files two minutes and one second after Start (▶) is pressed.

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

All of the companion video files except for the Limelight `.lvc` file can be played in a standard video player. The `.lvc` Limelight video capture file is a custom MJPEG container.

## Sidekick can be disabled
Sometimes, you may want to disable **Sidekick** on the robot without fully removing its library.
Although it is legal to have it enabled for FTC competitions, and even though it is designed to have minimal impact on your code's performance, it may sometimes cause unexpected behavior from its many system hooks, or it might simply have a bug that prevents your code from operating correctly.

As such, there are two ways to disable **Sidekick**.

### 1. Disable with UI
**Sidekick** automatically adds an op mode called _Enable/Disable Sidekick_ to your list of op modes. Run it and press Start (▶) on the Driver Station to toggle the mode.

### 2. Disable with API
**Sidekick** can be disabled by a call to [`Sk.enable(false)`](api-reference.md#skenable) from your robot code. 
