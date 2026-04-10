---
description: package com.skeletonarmy.marrow.actions
---

# RetryAction

## Overview

`RetryAction` is the RoadRunner Actions equivalent of [RetryCommand](https://www.google.com/search?q=%23). It allows you to build adaptable and reliable action sequences by executing an action and automatically retrying it if a specified condition is not met upon completion.

Just like its command-based counterpart, this is especially useful for actions that may fail on the first attempt, such as vision-based alignment, object grabbing, or precise mechanism positioning.

Check out the ["Retries" page](../../concepts/retries.md) to learn how to use `RetryAction` for autonomous behaviors.

***

## Usage

### **Setup**

To use `RetryAction`, you provide the constructor with:

* **Action to run** - the initial action you want to execute.
* **(Optional) Alternative action to run on retries** - lets you customize the retry behavior per attempt (e.g., switching to a vision-assisted action if the initial attempt fails).
* **Success condition** - a boolean supplier that checks whether the action was successful. If this condition returns `false`, the action will be retried.
* **Maximum number of retries** - defines the maximum number of times the action can be retried.

```java
new RetryAction(
    () -> intake.grabPixel(),  // Initial action
    () -> intake.isFull(),     // Success condition: finish if true, retry if false
    3                          // Max retries
)
```

Or with an alternative retry action:

```java
new RetryAction(
    () -> vision.alignToTag(),      // Initial attempt
    () -> vision.searchAndAlign(),  // Action to run on every retry
    () -> vision.isAligned(),       // Success condition
    2                               // Max retries
)
```

***

#### Example Usage

Here is an example of how to integrate `RetryAction` into a RoadRunner `Action` sequence:

{% hint style="info" %}
This is by no means a functional autonomous program.
{% endhint %}

```java
@Autonomous
public class MyAuto extends LinearOpMode {
    @Override
    public void runOpMode() {
        MecanumDrive drive = new MecanumDrive(hardwareMap, new Pose2d(0, 0, 0));
        Claw claw = new Claw(hardwareMap);

        waitForStart();

        Actions.runBlocking(
            new SequentialAction(
                drive.actionBuilder(new Pose2d(0, 0, 0))
                    .lineToX(24)
                    .build(),

                // Attempt to grab a pixel. 
                // If the sensor doesn't detect it, retry the grab up to 3 times.
                new RetryAction(
                    () -> claw.close(),
                    () -> claw.hasPixel(),
                    3
                ),

                drive.actionBuilder(new Pose2d(24, 0, 0))
                    .lineToX(0)
                    .build()
            )
        );
    }
}
```
