---
description: package com.skeletonarmy.marrow.prompts
---

# MultiOptionPrompt

## Overview

`MultiOptionPrompt<T>` is a generic prompt used in pre-match configuration screens with `Prompter`. It allows drivers to select **multiple** options from a list using the gamepad. Each selected item is clearly marked, and the selection can be confirmed by navigating to the `DONE` entry and pressing the confirm button.

***

## Usage

To create a new prompt, provide:

1. A **header** for the prompt.
2. A **boolean** indicating whether the user must select at least one option.
3. A **boolean** indicating whether the selection order should be displayed.
4. A **list of selectable options**.

Example:

```java
new MultiOptionPrompt<>(
    "Select Starting Items",  // Header
    true,                     // Require at least one selection
    false,                    // Do not order the options
    Item.RED, Item.BLUE, Item.GREEN  // Options
);
```

This will display a scrollable list with checkboxes. Drivers can toggle each option by pressing the confirm button while the option is highlighted. The prompt returns a `List<T>` containing all selected options when `DONE` is confirmed.

{% hint style="info" %}
Can be used with any object type that has a meaningful `toString()` method, since it uses `toString()` to display the options.
{% endhint %}

### Controls

* <kbd>D-PAD UP</kbd>: Move selection up
* <kbd>D-PAD DOWN</kbd>: Move selection down
* <kbd>A</kbd>: Select

### Telemetry Output Example

```
=== Select Starting Items ===

[ ] RED <
[ ] BLUE
[ ] GREEN

-----------------
       DONE
```

After pressing <kbd>A</kbd> on `RED`:

```
=== Select Starting Items ===

[x] RED <
[ ] BLUE
[ ] GREEN

-----------------
       DONE
```

Attempting to confirm `DONE` without any selections (if `requireSelection` is `true`):

```
=== Select Starting Items ===

[ ] RED
[ ] BLUE
[ ] GREEN

-----------------
       DONE <

! You must select at least one option !
```
