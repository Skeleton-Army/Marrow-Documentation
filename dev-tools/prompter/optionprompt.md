---
description: package com.skeletonarmy.marrow.prompts
---

# OptionPrompt

## Overview

`OptionPrompt<T>` is a generic prompt used in pre-match configuration screens with [`Prompter`](./). It allows drivers to select from a list of options using the gamepad.

***

## Usage

To create a new prompt, provide a header and options:

```java
new OptionPrompt<>("Select Alliance", Alliance.RED, Alliance.BLUE)
```

You can also pass an Enum class directly. The prompt will automatically use all defined constants within that Enum:

```java
new OptionPrompt<>("Select Alliance", Alliance.class)
```

This will display a scrollable list with the options `RED` and `BLUE`. The selected option is returned when the user presses the <kbd>CROSS/A</kbd> button.

{% hint style="info" %}
Can be used with any object type that has a meaningful `toString()` method, since it uses `toString()` to display the options.
{% endhint %}

### Controls

* <kbd>D-PAD UP</kbd>: Move selection up
* <kbd>D-PAD DOWN</kbd>: Move selection down
* <kbd>CROSS/A</kbd>: Confirm selection

### Telemetry Output Example

```
=== Select Alliance ===

 - RED <
 - BLUE
```

After pressing <kbd>D-PAD DOWN</kbd>:

```
=== Select Alliance ===

 - RED
 - BLUE <
```
