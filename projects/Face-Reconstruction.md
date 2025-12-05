---
layout: project
type: project
image: images/face_reconstruction/front.png
title: Face Reconstruction
permalink: projects/FR
# All dates must be YYYY-MM-DD format!
date: 2025-12-05
labels:
  - Mitsuba 3
  - FLAME
  - Face Reconstruction
summary: Implementation of a face reconstruction pipeline using reverse rendering.
---
# Face Reconstruction Showcase [WORK IN PROGRESS]

## Phong interpolation and anti-aliasing
While implementing a progressive renderer, I noticed that the image quality was poor due to aliasing. The "jaggies" artifact on the outline of the sphere. This appearance stems from ray tracing through the center of each square pixel. This happens if the geometry details of the scene are smaller than the size of a single pixel, or if they change significantly from one pixel to the next, then the pixel grid doesn't have a high enough resolution to accurately capture these details.

To illustrate, I rendered two spheres using 20 samples per pixel. On the left I have an implicit sphere function that is rendered using ray-sphere intersection. On the right ray-triangle intersections. Additionally, each coordinate is mapped to a colour channel. The result are colours that represent the surface normal.

<p align="center">
<img src="../images/face_reconstruction/test.png" width="100%" height="100%">
</p>


<div style="display: flex; justify-content: center; gap: 20px;">
  <img src="../images/face_reconstruction/reference_sunlight.png" width="50%" height="50%">
  <img src="../images/face_reconstruction/10_lobes_sunlight.png" width="50%" height="50%">
</div>

<p align="center">
<img src="../images/face_reconstruction/Screencast From 2025-12-04 17-55-01.gif" width="60%" height="60%">
</p>

<p align="center">
<img src="../images/face_reconstruction/face_mitsuba_SG_all_mask.gif" width="60%" height="60%">
</p>


<div style="display: flex; justify-content: center; gap: 200px;">
  <img src="../images/face_reconstruction/Screencast From 2025-12-04 18-25-05.gif" width="25%" height="25%">
  <img src="../images/face_reconstruction/Screencast From 2025-12-04 18-27-13.gif" width="25%" height="25%">
</div>


<div style="display: flex; justify-content: center; gap: 20px;">
  <img src="../images/face_reconstruction/stage2_depthLoss.svg" style="width:500px; height:auto;">
  <img src="../images/face_reconstruction/subject_2_stage2_depthLoss.svg" style="width:500px; height:auto;">
</div>

*This image renders two spheres using 20 samples per pixel to illustrate the "jaggies" on light and shadow.*


## References

Physically Based Rendering: From Theory to Implementation. From https://pbrt.org/

