# Overview

## What is Sidekick RC?

**Sidekick RC** is a tool for FTC robotics that essentially does three things:

1. It manages the Wi-Fi and Android Debug Bridge (ADB) connection between your laptop and the robot, making it easy to push new code via Android Studio or run tools like FTC Dashboard.
2. It enables real-time graphing of data such as the Control Hub's voltage, current draw, and 
temperature, while your robot runs.
3. It captures a ton of data about every run that can be examined later.

It's comprised of two components:

1. A library that you include in your team's robot code.
2. A PC application that you install on your laptop. (Only Windows is supported for now. If you have a Mac,
sorry: that version is coming later.)

The library portion is responsible for the following:

- Every time you run an opMode, the library automatically records a firehose of data about 
the run. 
- It monitors a communication channel with the **Sidekick** application to transfer data.

The application is used for:

- Establishing a Wi-Fi and ADB connection between the PC and robot.
- Graphing data in real-time.
- After-the-fact (*postmortem*) analysis of the data from a robot's run.