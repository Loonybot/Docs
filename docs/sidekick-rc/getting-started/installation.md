# Installation
There are two components of **Sidekick** to install: 

1. The Android Studio library;
2. The PC application.

## 1. Library Installation
Go to the [Loonybot GitHub SidekickRC releases](https://github.com/Loonybot/SidekickRC/releases) page and find the newest version labeled "Sidekick RC Library". Follows the installation instructions there. 

If you have a minimal **build.gradle**, your file should look like the following, with the
changes highlighted. You might have many additional lines from other software packages.

```groovy title="Changes for a minimal build.gradle" hl_lines="14-16 20"
apply plugin: 'com.android.application'

apply from: '../build.common.gradle'
apply from: '../build.dependencies.gradle'

android {
    namespace = 'org.firstinspires.ftc.teamcode'

    packagingOptions {
        jniLibs.useLegacyPackaging true
    }
}

repositories {
    maven { url 'https://jitpack.io' }
}

dependencies {
    implementation project(':FtcRobotController')
    implementation 'com.github.Loonybot:SidekickRC:lib-v??.??.??'
}
```

Note that you shouldn't actually see `v??.??.??` in your **build.gradle** because you'll have used 
the version number of the latest library released on [GitHub](https://github.com/Loonybot/SidekickRC/releases).

Don't forget to sync your project with the updated Gradle file by pressing the Elephant icon in the top-right corner of Android Studio.

## 2. Application Installation
If you have a Windows PC, go to the [Loonybot GitHub SidekickRC releases](https://github.com/Loonybot/SidekickRC/releases) page and find the newest version labeled "Sidekick RC application". Follows those installation instructions. 

If you have a Mac PC, sorry, you'll have to wait until we port to Mac.

## Verifying Your Install
Once you've installed the **Sidekick** application and are actively running robot code that includes the **Sidekick** library, connect to the robot (use the `Connect` button in the application if you're not already Wi-Fi connected). 
If everything is working correctly, you should see a green "Connected" status for "Sidekick" in the lower-right corner of the window. 
Congratulations, Sidekick is enabled and working on your robot!

If you don't see "Connected" for either "Wi-Fi" or "Sidekick", that means that your PC is not connected to the robot. Try pressing the `Connect` button to establish a Wi-Fi connection.

If you see "Connected" for "Wi-Fi" but not for "Sidekick", then the library is not properly installed or enabled on the robot. 
Verify that synced with the updated Gradle file via the Elephant icon, that your code built properly, and that you were able to successfully deploy the result to the robot.
