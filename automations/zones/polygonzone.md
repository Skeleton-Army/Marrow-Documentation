---
description: package com.skeletonarmy.marrow.zones
---

# PolygonZone

## **Overview**

`PolygonZone` defines a multi-point polygon region for representing triangular, rectangular, or arbitrary-shaped areas.

A common use case is representing the robot as a `PolygonZone`.

***

## **Usage**

`PolygonZone` offers multiple constructors:

```java
// --- Triangle defined by three corners ---
PolygonZone triangle = new PolygonZone(
    new Point(0, 0),
    new Point(12, 0),
    new Point(12, 6)
);

// --- Rectangle defined by width and height ---
PolygonZone unitRect = new PolygonZone(10, 5);

// --- Rectangle centered at a point ---
PolygonZone centered = new PolygonZone(new Point(24, 24), 12, 6);

// --- Rotated rectangle centered at a point ---
PolygonZone rotated = new PolygonZone(new Point(24, 24), 12, 6, Math.toRadians(45));

// --- Thin rectangular line between two points with a thickness ---
PolygonZone line = new PolygonZone(new Point(4, 4), new Point(10, 10), 5);
```

`PolygonZone` can also be used to represent the robot as a zone:

```java
// Represent the robot as an 18" by 18" square
PolygonZone robotZone = new PolygonZone(18, 18);
```

***

## **Unique Methods**

`PolygonZone` provides methods specific to polygon geometry:

<table><thead><tr><th width="393">Method</th><th>Description</th></tr></thead><tbody><tr><td><code>double getRotation()</code></td><td>Gets the current rotation of the polygon in radians.</td></tr><tr><td><code>double getRotationDegrees()</code></td><td>Gets the current rotation of the polygon in degrees.</td></tr><tr><td><code>void rotateBy(double angleRadians)</code></td><td>Rotates the polygon around its center by the given angle in radians.</td></tr><tr><td><code>void rotateByDegrees(double angleDegrees)</code></td><td>Rotates the polygon around its center by the given angle in degrees.</td></tr><tr><td><code>void setRotation(double angleRadians)</code></td><td>Sets the polygon rotation to the specified angle in radians.</td></tr><tr><td><code>void setRotationDegrees(double angleDegrees)</code></td><td>Sets the polygon rotation to the specified angle in degrees.</td></tr></tbody></table>
