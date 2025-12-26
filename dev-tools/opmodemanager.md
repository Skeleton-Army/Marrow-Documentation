---
description: package com.skeletonarmy.marrow
---

# OpModeManager

## Overview

`OpModeManager` provides a simple interface for accessing the internal OpMode manager. It allows your code to read the current OpMode, robot state, hardware map, telemetry, and register lifecycle listeners - without direct access to the SDK internals.

This is useful when you need to interact with OpMode-level information from subsystems or utilities without manually passing references around.

{% hint style="warning" %}
Do not access the current OpMode before it is initialized. The hardware map may also change during initialization, so avoid relying on or caching it early.
{% endhint %}

***

## Usage

#### **getManager()**

Returns the active `OpModeManagerImpl` instance.

```java
OpModeManagerImpl manager = OpModeManager.getManager();
```

***

#### **getActiveOpMode()**

Returns the currently running OpMode, or `null` if none is running.

```java
OpMode active = OpModeManager.getActiveOpMode();
```

***

#### **getActiveOpModeName()**

Returns the name of the active OpMode.

```java
String name = OpModeManager.getActiveOpModeName();
```

***

#### **getRobotState()**

Returns the current `RobotState` enum (e.g., `INIT`, `RUNNING`, `STOPPED`).

```java
RobotState state = OpModeManager.getRobotState();
```

***

#### **getHardwareMap()**

Returns the active `HardwareMap`.

Useful when you need hardware access outside your OpMode.

```java
HardwareMap hardwareMap = OpModeManager.getHardwareMap();
```

***

#### **getTelemetry()**

Returns the active `Telemetry`.

Useful when you need to debug things outside your OpMode.

```java
Telemetry telemetry = OpModeManager.getTelemetry();
```

***

#### **registerListener(listener)**

Registers a listener for OpMode lifecycle changes.

The listener receives callbacks such as:

* `onOpModePreInit`
* `onOpModePreStart`
* `onOpModePostStop`

Returns the active OpMode at the time of registration.

```java
OpModeManager.registerListener(myListener);
```

***

#### **unregisterListener(listener)**

Removes a previously registered listener.

```java
OpModeManager.unregisterListener(myListener);
```
