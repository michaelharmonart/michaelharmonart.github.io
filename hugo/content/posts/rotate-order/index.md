---
title: "Picking Good Default Rotate Orders"
author: "Michael Harmon"
date: 2025-10-16
tags: ["maya", "rigging"]
---
{{< figure src="rotate-order.webp" 
alt="Comparison of a Bad rotateOrder and a Good rotateOrder" 
caption="Early work from a friend showing the chaos they witnessed when switching to splined keys, and after re-ordering the rotation of the shoulder controls." >}}

Good default rotation orders are incredibly important but often forgotten about, sometimes even in high quality rigs. 
Please don't just think of rotation orders as un-important or a black-box that can't be understood! 
A good default rotateOrder setting could be the difference between a rig that's a joy to use and one that makes an animator want to tear their hair out.

People always seem to over-complicate this, but it's not hard once you understand this general rule of thumb:
### **TLDR:** In Maya the rotate order for a control should be (Twist Axis, Least Important Axis, Primary/Hinge Axis)
Keep in mind that in certain software you may need to switch the first and last axes depending on how rotation order are represented [See Intrinsic vs. Extrinsic Rotation Orders](#intrinsic-vs-extrinsic-euler-angles).

## What are Rotation Orders?
Representing rotation is actually pretty tough, and there are a number of methods to do so.
However, for animation [Euler Angles](https://en.wikipedia.org/wiki/Euler_angles) are the most common rotation representation (the other most popular being [Quaternions](https://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation)).

Euler Angles are conceptually simple, they're just values for how much the object is rotated along each axis (XYZ). This means they're easy to understand, and allow for things like storing a rotation of more than 360°. 

**They also have a problem: [Gimbal Lock](https://en.wikipedia.org/wiki/Gimbal_lock)**  
{{< figure src="gimbal-lock.webp" 
alt="Demo of gimbal lock" 
caption="A visualization of the Maya default XYZ rotation order. Created by parenting rings for each axis. X is parented to Y, Y is parented to Z." >}}
Here I have an object in Maya as well as a some rings parented to each other to visualize the Euler Angles, and how they cause gimbal lock.

You'll notice that the rotation values are very reasonable when rotating along the X and Z axis, but when the Y axis is rotated by 90 degrees suddenly the X axis is aligned with the Z axis and we've lost a degree of freedom! Even a very small rotation can wildly change the underlying Euler Angles that the animation curves are interpolating. That means crazy movements between keyframes and frustrated animators. 

The "solution" to the problem of gimbal lock is re-ordering the rotation axes. Remember that only the middle axis (in the above example the **Y** in X**Y**Z) will ever cause gimbal lock. Most 3D software will allow you to choose a rotation order for your controls/objects, allowing you to mitigate the symptoms of gimbal lock.

This visualization should also help you understand why the parent axis (last axis in the rotation order in Maya) should be the primary hinge axis. The middle axis causes gimbal lock, and the child axis (first axis in the rotation order in Maya) should be the axis of twist (like the twist of the radius and ulna in the forearm).

### How about that middle axis?
Unfortunately due to how Euler Angles work, you will always hit gimbal lock on at least one axis. Depending on the animation a different rotation order might be suitable (switching the primary axis and least important axis depending on which is used most in that particular animation).  
Luckily Maya now has a [Reorder Rotation Tool](https://help.autodesk.com/view/MAYAUL/2025/ENU/?guid=GUID-50116A2D-5BD7-48D4-BCF1-8AF89CB24205) built in. It allows you to change the rotation order of a control while keeping the poses you've keyed the same. This is incredibly useful, so make sure your rig is set up such that changing a control's rotate order doesn't break things!

If that doesn't work Maya also allows for animating certain controls with Quaternions, which can be handy.
> [Maya Docs Page:](https://help.autodesk.com/view/MAYACRE/ENU/?guid=GUID-AD9AEB91-63EC-44C5-9B25-00449351DEF9)
> 1. In the Graph Editor or Dope Sheet, select the curve whose rotation interpolation you want to change.
> You can change the rotation interpolation type only on rotation channels that have keyframes on all three channels (rotateX, rotateY, rotateZ). In addition, because the rotateX, rotateY and rotateZ channels always share the same interpolation type, changing interpolation for a single channel such as rotateX, automatically changes rotateY and rotateZ as well.
> 2. Select Curves > Change Rotation Interp and select the interpolation type you want from the list. See Change Rotation Interp for descriptions of the options.


## Intrinsic vs. Extrinsic Euler Angles
One thing you should keep in mind is that the same rotation order can mean different things depending on what convention the software uses.
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


The rotate order for a control should be (Twist Axis, Least Important Axis, Primary/Hinge Axis) in softwares that uses ***Extrinsic*** rotation orders. 

In software that uses ***Intrinsic*** rotation orders the order should be reversed (Primary/Hinge Axis, Least Important Axis, Twist Axis).  

## Defaults Matter
Especially in rigging. Production rigs will have hundreds of controls and options, and an animator already has *a ton* to juggle. Set **good defaults** that will be helpful in 90% of cases and then leave the option open to change it for the other 10%.
