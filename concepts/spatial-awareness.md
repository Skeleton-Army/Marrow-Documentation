---
description: How to utilize Zones
---

# Spatial Awareness

Spatial awareness helps your robot understand where it is on the field and make decisions based on that position. You can write logic that responds intelligently to location during both autonomous and TeleOp.

***

## Why It Matters

Spatial awareness makes it possible to:

* Prevent mechanisms from activating in restricted areas.
* Automatically perform an action when entering a specific region (like scoring, collecting, or parking).
* Slow down or adjust drive speed near walls.
* Switch drive or scoring modes depending on field position.



In the **2025–2026 DECODE** season, for instance, you could:

* Prevent drivers from shooting outside the LAUNCH ZONE to avoid penalties.
* Shoot automatically once entering the LAUNCH ZONE.
* Adjust shot angle or power dynamically depending on the distance to the GOAL.

***

## Using Marrow

The [`Zones`](../automations/zones/) system in Marrow provides simple geometry classes for defining spatial regions:

* [`PolygonZone`](../automations/zones/polygonzone.md): defines triangular, rectangular, or multi-point areas.
* [`CircleZone`](../automations/zones/circlezone.md): defines circular areas.

For a full breakdown of how to use it in your own code, see the [`Zones` reference page](../automations/zones/).
