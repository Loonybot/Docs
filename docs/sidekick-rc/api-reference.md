# API Reference
**Sidekick** has optional APIs that are callable from your Java code. 
Use them to configure **Sidekick** or supplement the recorded data.

## `Sk.enable()`
Enable **Sidekick** and inhibit its enable/disable opMode. This must be called from an `@OnCreate` method.

## `Sk.disable()`
Disable **Sidekick** and inhibit its enable/disable opMode. This must be called from an `@OnCreate` method.

### `Sk.suppressIssues()`
