---
description: package com.skeletonarmy.marrow.prompts
---

# MessagePrompt

## Overview

`MessagePrompt` is a prompt used to display information or alerts to the driver in pre-match configuration screens with [`Prompter`](./). It halts the `Prompter` sequence until the user acknowledges the message.

***

## Usage

To create a new prompt, provide the string you wish to display:

```java
new MessagePrompt("Ensure the intake is retracted!")
```

This will display the message on the Driver Station. The prompt remains active and prevents the sequence from advancing until the user confirms they have read it.

{% hint style="info" %}
You may prompt a `MessagePrompt` without providing a key: `.prompt(new MessagePrompt("..."))`
{% endhint %}

#### Use Cases

* Displaying pre-flight checklists.
* Warning drivers about specific robot states.
* Confirming that a previous configuration step was successful.

### Controls

* <kbd>CROSS/A</kbd>: Confirm and continue to the next prompt

### Telemetry Output Example

```
Ensure the intake is retracted!

Press CROSS/A to continue
```
