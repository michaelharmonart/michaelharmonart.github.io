---
title: "Picking Good Default Rotate Orders"
author: "Michael Harmon"
date: 2025-10-14
tags: ["maya", "rigging"]
draft: true
---
{{< figure src="rotate-order.webp" 
alt="Comparison of a Bad rotateOrder and a Good rotateOrder" 
caption="Early work from a friend showing the chaos they witnessed when switching to splined keys, and after re-ordering the rotation of the shoulder controls." >}}

Good default rotation orders are incredibly important but often forgotten about, sometimes even in high quality rigs. 
Please don't just think of rotation orders as un-important or a black-box that can't be understood! 
A good default rotateOrder setting could be the difference between a rig that's a joy to use and one that makes an animator want to tear their hair out.

People always seem to over-complicate this, but it's not hard once you understand this general rule of thumb:
### **TLDR:** In Maya the rotate order for a control should be (Twist Axis, Least Important Axis, Primary/Hinge Axis)
Keep in mind tha in certain software you may need to switch the first and last axes depending on how rotation order are represented [See Intrinsic vs. Extrinsic Rotation Orders](#intrinsic-vs-extrinsic-euler-angles).

## What are Rotation Orders?
Representing rotation is actually pretty tough, and there are a number of methods (the other most popular is [Quaternions](https://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation)).
However for animation

## Intrinsic vs. Extrinsic Euler Angles
The [Euler Angles Wikipedia](https://en.wikipedia.org/wiki/Euler_angles#Definition_by_intrinsic_rotations) explains the difference as:
> Intrinsic rotations are elemental rotations that occur about the axes of a coordinate system XYZ attached to a moving body. Therefore, they change their orientation after each elemental rotation. The XYZ system rotates, while xyz is fixed. 

> Extrinsic rotations are elemental rotations that occur about the axes of the fixed coordinate system xyz. The XYZ system rotates, while xyz is fixed.

Here's a handy GIF from [Freya Holmér](https://www.acegikmo.com/) to visually explain the difference:
{{< figure src="intrinsic-extrinsic.gif" 
alt="Comparison of Intrinsic rotations and Extrinsic rotations" 
caption="Left: Intrinsic rotation x-y'-z'' Right: Extrinsic rotation Z-Y-X." >}}

Knowing which method your software uses might just require some experimentation or a quick google search.  

**Maya and Blender** use ***Extrinsic*** rotation orders  
I know at least **Godot** uses ***Intrinsic*** rotation orders  