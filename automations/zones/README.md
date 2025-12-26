---
description: package com.skeletonarmy.marrow.zones
---

# Zones

## Overview

The `Zones` system defines geometric regions on the field used for spatial reasoning and autonomous decision-making.

Zones represent physical areas - such as scoring areas - and can be [circle-based](circlezone.md) or [polygon-based](polygonzone.md).

Check out the ["Spatial Awareness" page](../../concepts/spatial-awareness.md) to learn how to use `Zones` for autonomous behaviors.

<figure><img src="../../.gitbook/assets/Zones.gif" alt="A GIF showing Zones in action" width="422"><figcaption></figcaption></figure>

{% hint style="info" %}
For `Zones` to function properly, you must ensure that your robot's position is accurate.
{% endhint %}

***

## Usage

All zones implement the `Zone` interface, which provides common geometry methods.

Two built-in implementations are available:

* [`CircleZone`](circlezone.md) - circular areas defined by center and radius
* [`PolygonZone`](polygonzone.md) - triangular, rectangular, or arbtrary-shaped areas defined by three or more points.

| Method                                 | Description                                                      |
| -------------------------------------- | ---------------------------------------------------------------- |
| `boolean contains(Point p)`            | Checks if a point lies within or on the zone.                    |
| `double distanceTo(Point p)`           | Returns the shortest distance from a point to the zone boundary. |
| `double distanceTo(Zone other)`        | Returns the shortest distance between two zones.                 |
| `boolean isInside(Zone other)`         | True if this zone overlaps or is contained in another.           |
| `boolean isFullyInside(Zone other)`    | True if this zone is fully contained in another.                 |
| `void moveBy(double dx, double dy)`    | Translates the zone.                                             |
| `void setPosition(double x, double y)` | Moves the zone’s center or reference point.                      |

***

## Example Usage

The following example shows how `Zones` can be used with [Pedro Pathing](https://pedropathing.com) to detect if the robot is inside or near key areas on the 2025–2026 DECODE field:

```java
@TeleOp
public class TeleOpApp extends OpMode {
    private final PolygonZone closeLaunchZone = new PolygonZone(new Point(144, 144), new Point(72, 72), new Point(0, 144));
    private final PolygonZone farLaunchZone = new PolygonZone(new Point(48, 0), new Point(72, 24), new Point(96, 0));
    private final PolygonZone blueBase = new PolygonZone(new Point(105.5, 33.5), 20, 20);
    private final PolygonZone redBase = new PolygonZone(new Point(38.5, 33.5), 20, 20);
    
    // Represent the robot as an 18" by 18" zone
    private final PolygonZone robotZone = new PolygonZone(18, 18);

    private Follower follower;

    @Override
    public void initialize() {
        follower = Constants.createFollower(hardwareMap);
        follower.startTeleopDrive(true);
        follower.setStartingPose(new Pose(72, 72));
    }

    @Override
    public void run() {
        follower.update();
        follower.setTeleOpDrive(-gamepad.left_stick_y, -gamepad.left_stick_x, -gamepad.right_stick_x,true);

        // Sync robot zone with actual robot position and rotation
        robotZone.setPosition(follower.getPose().getX(), follower.getPose().getY());
        robotZone.setRotation(follower.getPose().getHeading());

        if (robotZone.isInside(closeLaunchZone)) {
            // Robot is partially in the launch zone
        }
        
        if (robotZone.isFullyInside(redBase)) {
            // Robot is fully parked in the red base
        }

        double distanceToBlueBase = robotZone.distanceTo(blueBase);
        if (distanceToBlueBase < 10) {
            // Robot is near the blue base
        }
    }
}

```
