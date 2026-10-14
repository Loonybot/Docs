# API Reference
**Sidekick** has optional APIs that are callable from your Java code. 
Use them to configure **Sidekick** or add data to the capture. All of the APIs are exposed as `public static` methods of the `Sk` class. 

## Sk.enable()
`public static void enable(boolean enable);`

Enable or disable **Sidekick** and inhibit its enable/disable op mode. 

When **Sidekick** is disabled, all of its functionality and methods (other than `Sk.enable()`) become _no-ops_.

Calling this method (for either enabling or disabling) inhibits the **Sidekick** enable/disable op mode from getting added to your op mode list.

Because **Sidekick** needs to know the new state early in the boot process, this method can only be called from an [@OnCreate](api-reference.md#setting-state-in-oncreate) method.

## Sk.setRetentionDays()
`public static void setRetentionDays(int days);`

Set the number of days that **Sidekick** retains captures on the robot's internal storage.
By default, **Sidekick** stores captures for up to 7 days.
Regardless of this setting, **Sidekick** will try to free up at least 100 MB of storage at the beginning of every op mode by deleting the oldest captures.

Because **Sidekick** needs to know the new state early in the boot process, this method can only be called from an [@OnCreate](api-reference.md#setting-state-in-oncreate) method.

## Sk.suppressIssues()
`public static void suppressIssues(int... issueCodes);`

Suppress specific warnings, errors and suggestions from showing up in Dr. Robot's tab. The function takes a list of issue codes to disable. For example, to disable issues 101 and 107, specify:

```Java
Sk.suppressIssues(101, 107);
```

This method can be called from `@OnCreate` or from an op mode.

## Sk.registerSerializer()
`public static <T> void registerSerializer(T sample, String format, Serializer<T> serializer);`

Register a serializer to enable **Sidekick** to decode class objects when it saves (_serializes_) instances to the capture file and later displays them in the app for analysis.

Let's say you define your own `Target` class that tracks the distance and robot-relative angle to a target:

```java
class Target {
    double distance; // Inches
    double angle; // Radians
}
Target target; 
```

If you used the `target` instance when writing it to **Sidekick**, you get an ugly result:

```java
Sk.note("Basket target: ", target);
```

The **Sidekick** will show something like this:

`Basket target: `

You could avoid this problem by always referring to the component fields, e.g.:

```java
Sk.note("Basket target: ", target.distance, target.angle);
```

Alternatively, you could define a `toString()` method for your class that converts an instance to a string, and **Sidekick** will use that.

The preferred solution, though, is to register a _serializer_ that tells **Sidekick** how to directly decode the components of a class. 
You can do that like this:

```java
Sk.registerSerializer(
    new Target(0, 0), 
    "distance=in, angle=rad", 
    x->new Object[]{x.distance, x.angle});
```

`Sk.registerSerializer` gives **Sidekick** a `sample` instance, a `format` string, and a  `serializer` whose function takes an instance of that type and returns an array of primitive types. 

The `sample` argument is first used by **Sidekick** to determine the type of the class to be serialized, and then it's used to call the `serializer` function to determine the count and types of the component variables so that it can pre-compile the serialization process.
The value of `sample` can be anything at all, so long as the `serializer` function returns valid values for it.

The `format` string tells **Sidekick** the names and optionally the units of every component variable. 
It's fine not to specify units--for example, a `Point` might be "x=, y=".

A `serializer` implements the Serializer interface. 
Its function takes an instance of the object and returns the values of the component variables as an array. 
The types of the values can be anything, but its preferable to use primitive types like `double`, `int`, `boolean`, `String`, etc. 
A strict requirement for `serializer` is that it must always return the same sized array regardless of input, and the types of the values within the array must always be the same.

The benefits of a serializer over `toString()` are:

- **Sidekick** can automatically graph the component values (`distance` and `angle` in our example).
- **Sidekick** knows the units (`angle` can be automatically converted to degrees for easier understanding, for example).
- Less space is consumed in the capture file.
- The run-time overhead for a serializer is just a fraction of the CPU cost of `toString()`.
- You can register serializers for classes of third party libraries that you use (e.g., Road Runner's `Pose2d` class) where it's not feasible to add a `toString()` method.

## Setting state in @OnCreate
**Sidekick** requires that some state APIs are callable only from `@OnCreate`. Any code that is marked `@OnCreate` gets executed before the first op mode can even be run. The annotation can be put on any method in any class of your code; here is a recommended template:

```Java title="Set Sidekick state in @OnCreate"
@SuppressWarnings("unused")
class ConfigureSidekick {
    @OnCreate
    public static void onCreate(Context context) {
        Sk.enable(); // Make Sidekick's enable/disable op mode disappear
        Sk.setRetentionDays(31); // Increase from the 7 day default
    }
}
```
!!! warning
    Be very careful of any code placed within the `@OnCreate` method as it executes during robot startup. If it raises an uncaught exception, it will cause an endless cycle of reboots and you'll need to reset the robot via means such as the `REV Hardware Client`.
