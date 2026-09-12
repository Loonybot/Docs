# Introducing Sidekick RC
## The Essential Software Companion for First Tech Challenge
**Sidekick RC** makes it easy to understand, iterate on, and improve your robot performance, whether you're a new Blocks user or a world champion.

## Features
- **Eliminate the headaches of connecting to your robot.** 
FTC's Wi-Fi and wireless Android Debug Bridge (ADB) connections are notoriously unreliable and difficult to use, but now with **Sidekick** you get:
    - A single button to connect to the robot via Wi-Fi and ADB;
    - Fewer dropped connections;
    - Easy and robust recovery when ADB hangs.
- **Monitor your robot's hardware as it runs.** Graph the robot's real-time performance to inspect performance characteristics such as amperage draw, hub temperature, and CPU usage.
- **Record a wealth of data for offline analysis, automatically, with no work needed by you.** Context is essential for debugging and performance work. Without perturbing your robot's performance, **Sidekick** automatically records:
    - All your calls that interact with the hardware, including parameters and results.
    - All "bulk" data from an API call to a device that invokes a bulk read. (So it gets free over-current warnings from motors, for example.) 
    - The performance of your control loop and all hardware calls.
    - System performance including CPU utilization, CPU clock, CPU temperature, etc.
    - Thread performance.
    - All Logcat data.
    - `telemetry.addValue()`, `addLine()` and all other telemetry calls.
    - All Gamepad input.
    - The robot's configuration of devices.
    - All FTC Dashboard Canvas visualizations.
    - The Limelight camera stream, complete with visualizations.
    - The camera stream of regular cameras when ADB is connected. **Sidekick** records an MP4 of all visualizations that are output to the Robot Controller's "screen".
- **Benefit from automatic analysis.** *Dr. Roboto* is a built-in mentor that diligently examines all recorded data and makes suggestions and points out errors and warnings, based on years of real-life mentoring experience. It addresses both performance and correctness.
- **Enjoy intuitive analysis for humans.** It loves to graph and make it easy to navigate and understand the data.
- **Extend its functionality.** Use optional API calls to enable features such as run-time assertions and performance timing.
- **Back up your configuration.** We've had our robot configuration wiped more than once. Now it's saved after every opMode and can be restored with a single button.

**Sidekick** is easy to install and use, and it's fast and robust. It works with Java, Kotlin, Blocks, and all FTC libraries. 
