---
description: package com.skeletonarmy.marrow.settings
---

# Settings

## Overview

`Settings` provide a simple way to store, change, and persist configuration values on the robot - even after the robot gets restarted. This is useful for things like enabling a debug mode, adjusting teleop or autonomous behavior, or saving preferences across sessions.

You can configure these options inside a [`SettingsOpMode`](settings.md#defining-settings), which lets you edit values directly from the Driver Hub - no code changes or redeploys required.

<figure><img src="../.gitbook/assets/Settings.gif" alt="A GIF showing Settings in action" width="563"><figcaption></figcaption></figure>

{% hint style="warning" %}
We strongly recommend disabling any settings that could interfere with TeleOp before starting autonomous to avoid issues in a match.
{% endhint %}

***

## Usage

### Defining Settings

To define settings, extend `SettingsOpMode` and implement `defineSettings()`:

```java
@TeleOp
public class MySettings extends SettingsOpMode {
    @Override
    public void defineSettings() {
        add("debug_mode", "Debug Mode", new BooleanPrompt("Enable debug mode?", false));
        add("tabletop_mode", "Tabletop Mode", new BooleanPrompt("Enable tabletop mode (disables movement)?", false));
        add("alliance", "Select Alliance", new OptionPrompt<>("Select alliance", Alliance.RED, Alliance.BLUE));
    }
}
```

Each setting requires:

1. **Key** - a unique, case-insensitive identifier.
2. **Display Name** - shown in the menu on the driver station.
3. **Prompt** - an instance of a [`Prompt<T>`](prompter/) which determines how the value is entered.



### Interacting With Settings

When the OpMode runs:

* Navigate options using the <kbd>D-PAD</kbd>.
* Press <kbd>A</kbd> to modify a setting.
* Press <kbd>B</kbd> to exit a prompt without saving changes.

Settings are automatically saved to a JSON file on the Control Hub (`FIRST/marrow/settings.json`).



### Accessing Settings in Code

Use the `Settings` API to read or write settings programmatically:

```java
boolean debugMode = Settings.get("debug_mode", false); // default is false

Settings.set("alliance", Alliance.BLUE);
```

* `get(key, defaultValue)` retrieves a value, returning the default if missing.
* `set(key, value, (optional) save)` - Stores a value under the given key. If `save` is `true` (default), the settings are immediately written to file.

{% hint style="info" %}
You can use `Settings` even without any `SettingsOpMode`. It can serve just as a central hub for saving variables between OpModes and restarts.
{% endhint %}
