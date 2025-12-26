---
description: package com.skeletonarmy.marrow.zones
---

# CompositeZone

## **Overview**

`CompositeZone` defines a region that is the union of two or more independent zones. It allows a collection of zones to be treated as a single `Zone`.

***

## Usage

`CompositeZone` is created using a collection of existing `Zone` objects:

```java
PolygonZone square = new PolygonZone(4, 4);
CircleZone circle = new CircleZone(new Point(4, 0), 3.0);

CompositeZone composite = new CompositeZone(square, circle);
```
