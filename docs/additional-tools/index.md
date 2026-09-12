# More Tools from Loonybot

## Test Bench

**Test Bench** is a tool for inspecting and testing the devices of a robot. 
It reads your robot's configuration and presents a menu for each device. 
Use the gamepad to activate motors, servos, I2C devices, etc., and verify that
they are configured and wired correctly.
A wide range of devices are supported, including goBilda Pinpoint Odometry Computers and
Limelight 3A cameras.

Some uses:

- Test a device in isolation when the robot doesn't appear to be functioning correctly
as a whole.
This can be helpful when you're having a debate as to whether bad behavior is a hardware bug or
a software bug.
- Use it as an *acceptance* test when first handing the robot from the hardware team to the
software team, to ensure that the hardware is fully functional without having to run any
new software.

**Test Bench** is simple to integrate. The code is a single `.java` file with no non-SDK
dependencies, so you can simply copy it into your code. Alternatively, include it as a library.

**Test Bench** has support for a wide range of devices and is easy to extend for those that are missing.
We're happy to consider Pull Requests for new devices.

## TurboRC

**TurboRC** enables *turbo mode* for your robot. It starts a low-priority thread when Start is 
pressed that consumes CPU cycles to cause the Linux kernel to change to the highest CPU clock 
frequency until your opMode finishes.
Use **Sidekick RC** to verify that the performance improvement for your control loop.


