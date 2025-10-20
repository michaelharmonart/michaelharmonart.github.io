---
title: "Deformation Layering in Maya’s Parallel GPU World"
author: "Charles Wardlaw"
date: 2025-10-20
tags: ["maya", "rigging", "performance", "gpu"]
original_url: "https://medium.com/@kattkieru/deformation-layering-in-mayas-parallel-gpu-world-15c2e3d66d82"
---
{{< figure src="preview.webp" link="https://medium.com/@kattkieru/deformation-layering-in-mayas-parallel-gpu-world-15c2e3d66d82" alt="Maya Profiler showing multiple stacked skin clusters running in just over 1 millisecond." >}}

This article shows how to improve on the technique of deformation layering by using multiple "stacked" skinClusters such that you don't screw up your rig's GPU override and lose performance. This is a great technique, and these are principles seen in production rigs at the highest levels.

<!--more-->
[Link to Original Site 🔗]({{< param original_url >}})  
  
---
{{< linkarchive >}}  
[Archived Code](archive/skin_merge.py)  