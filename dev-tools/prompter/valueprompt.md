---
description: package com.skeletonarmy.marrow.prompts
---

# ValuePrompt

## Overview

`ValuePrompt` is a numeric input prompt used in pre-match configuration screens with [`Prompter`](./). It allows drivers to adjust a value within a defined range using the gamepad.

**Supported types:** `Integer, Long, Double, Float, Short, Byte`

***

## Usage

To create a new prompt, provide a header, type, minimum, maximum, default value, and increment:

```java
new ValuePrompt<>(
    "Select a Start Delay", // Header
    Double.class,           // Type class (Integer.class, Double.class, etc.)
    0.0,                    // Minimum
    10.0,                   // Maximum
    2.0,                    // Default value
    0.5                     // Increment
);
```

This will display a value prompt starting at 2.0, adjustable in increments of 0.5, clamped between 0.0 and 10.0.

### Constructors

<table><thead><tr><th width="363">Constructor</th><th>Example</th></tr></thead><tbody><tr><td><code>ValuePrompt(String header, Class&#x3C;T> type)</code></td><td><code>new ValuePrompt&#x3C;>("Delay", Integer.class)</code></td></tr><tr><td><code>ValuePrompt(String header, Class&#x3C;T> type, T defaultValue)</code></td><td><code>new ValuePrompt&#x3C;>("Delay", Double.class, 2.0)</code></td></tr><tr><td><code>ValuePrompt(String header, Class&#x3C;T> type, T defaultValue, T increment)</code></td><td><code>new ValuePrompt&#x3C;>("Delay", Double.class, 2.0, 0.5)</code></td></tr><tr><td><code>ValuePrompt(String header, Class&#x3C;T> type, T minValue, T maxValue, T defaultValue, T increment)</code></td><td><code>new ValuePrompt&#x3C;>("Delay", Double.class, 0.0, 10.0, 2.0, 0.5)</code></td></tr></tbody></table>

### Controls

* <kbd>D-PAD UP / RIGHT</kbd>: Increase value
* <kbd>D-PAD DOWN / LEFT</kbd>: Decrease value
* <kbd>CROSS/A</kbd>: Confirm selection

### Telemetry Output Example

```
=== Select a Start Delay ===

< 2.0 >
```

After pressing <kbd>D-PAD UP</kbd>:

```
=== Select a Start Delay ===

< 2.5 >
```
