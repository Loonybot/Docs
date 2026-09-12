# FAQ

??? faq "How do I report a Sidekick bug?"
    If you have a `.sidekick` capture file that causes **Sidekick** to crash or that captures a run-time failure, please email it to [bugreport@loonybot.com](mailto:bugreport@loonybot.com) along with a description of the problem. 
    We hate crashes but love bug reports that can reproduce them, so we always make it our top priority to fix such bugs when we get them. 
    However, please consider your privacy: **Sidekick** itself does not save any _Personally Identifiable Information_, but your opMode may output PII to the data that is recorded.
    Please be sure to send us only the `.sidekick` file and none of the video files.

    Bugs and suggestions can also be filed on [GitHub](https://github.com/Loonybot/SidekickRC/issues).

??? faq "My robot spontaneously reboots and Sidekick only shows Logcat data. What can I do?"
    Problems where the robot reboots in the middle of an opMode are tough to fix.
    **Sidekick** can't cleanly shut down and save its capture data when this happens, so you lose a lot of context. 

    **Sidekick** _does_ automatically show Logcat data leading up to the crash, however. 
    Logcat data is still available because it uses a system mechanism that frequently flushes its data to permanent storage so it's more impervious to memory getting wiped. **Sidekick** shows all Logcat data from boot to the last message recorded. 

    If your problem is reproducible, you can add Logcat messages to provide context for what the robot is doing that might provoke the crash when the crash occurs. 
    For example, you might instrument your code with Logcat messages like the following:
    ```java
    final String TAG = "Crash"; // Identifier for finding our crash
    Log.i(TAG, "About to launch projectile");
    // ...launch code is here...
    Log.i(TAG, String.format("About to move arm to position %.2f", armPosition));
    // ...move code is here...
    ```
    
    When examining the Logcat data in **Sidekick**, you can double-click on your tag ("Crash" in our example) in the left-side pane to focus just on your own output.

    We've found that, in practice, Logcat will typically lose around 100ms of data just prior to a crash so you can't be sure you'll see the very last output. Think of the last message you see as more of a rough hint as to the time rather than a guarantee that it was really the last code to run before the crash.

    We've found that these types of crashes occurred either because of power spikes we caused that make the system's voltage to dip too low, or because we somehow caused a hardware device to crash (as by overheating it). 
    For the former case, in addition to adding Logcat output, you should graph your voltage and current use while trying to reproduce the crash scenario--you may note bad behavior even if the robot doesn't crash.
    
    Be warned, you may have found a new way to cause a reboot that we haven't seen before. Good luck!

