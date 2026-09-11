# What is Sidekick RC?

**Sidekick RC** is a tool for FTC robotics that has three different aspects:

1. It manages the Wi-Fi and Android Debug Bridge (ADB) connection between your laptop and the robot, making it easy to push code from Android Studio or run tools like FTC Dashboard.
2. It enables real-time graphing of data such as the Control Hub's voltage, current draw, and temperature, while your robot runs.
3. It captures a ton of data about every opMode run that can be examined later.

It's comprised of two components:

1. A library that you include in your team's robot code.
2. A PC application that you install on your laptop. 

The library is responsible for:

- Automatically recording a mass of data every time you run an opMode.
- Monitoring and transferring data via the communication channel to the **Sidekick** application.

The application is used for:

- Establishing a Wi-Fi and ADB connection between the PC and robot.
- Graphing data in real-time.
- Transferring data from from a robot's run to the PC.
- Analyzing the data after-the-fact (*postmortem analysis*).