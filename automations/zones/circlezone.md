---
description: package com.skeletonarmy.marrow.zones
---

# CircleZone

## **Overview**

`CircleZone` defines a circular region for representing any circular field area.

***

## **Usage**

`CircleZone` offers multiple constructors:

```java
// --- Unit circle at the origin (radius = 1) ---
CircleZone unitCircle = new CircleZone();

// --- Circle at the origin with a custom radius ---
CircleZone centerCircle = new CircleZone(5);

// --- Circle defined by center point and radius ---
CircleZone circle = new CircleZone(new Point(24, 24), 12);
```
