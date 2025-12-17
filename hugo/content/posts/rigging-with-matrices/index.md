---
title: "Rigging with Matrices"
author: "Michael Harmon"
date: 2025-12-16
tags: ["maya", "rigging", "matrix"]
draft: true
---
{{< figure src="cover.svg" 
alt="A 4x4 transformation matrix with its corresponding basis vectors" >}}
## "It's all just points in space!"

Rigging is just layering transformations to move those points in clever ways. 
At the end of the day: it's transformation matrices all the way down. 
Having an intuition of how to use and construct these matrices will be invaluable on your rigging journey.

## 4x4 Transformation Matrix Basics

Matrices are particularly suited for representing transformations as they can represent translation, scale, rotation, and shear. 
Representing a parent child relationship is also super simple with matrices, as calculating the final transformation of a hierarchy just takes the local matrix of each object in a hierarchy 
and multiplying each until you're left with the final matrix of the child. 
(The order you multiply in [might depend on the software](#row-vs-column-major-matrix-multiplication).)

For this reason, most software that deals with any sort of 3D Transformation is using transformation matrices under the hood.

### Row vs. Column Major Matrix Multiplication
