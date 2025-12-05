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

## [WORK IN PROGRESS]

## Monocular Face Reconstruction
We work with synthetically generated faces using the FLAME morphable model. Reconstructing the face using differentiable rendering with Mitsuba 3. The pipeline is fully differentiable with differentiable mask and regularizers. Below shows the face reconstruction progression from various snapshot during the optimization phase.

<p align="center">
<img src="../images/face_reconstruction/test.png" width="100%" height="100%">
</p>

## Differentiable Foreground Mask
Early during the project we observed increased accuracy when we restrict the training space on the face only. We used SAM from Meta as a differentiable mask for the photo loss. 

<p align="center">
<img src="../images/face_reconstruction/face_mitsuba_SG_all_mask.gif" width="40%" height="40%">
</p>

## Depth Regularizer
We also found that incorporating depth estimation was essential when reconstructing a 3D face from a single image. Because one photo provides limited geometric cues, the optimization can drift toward incorrect shapes. Using Depth Anything as a depth prior helped anchor the reconstruction.

<div style="display: flex; justify-content: center; gap: 200px;">
  <img src="../images/face_reconstruction/Screencast From 2025-12-04 18-25-05.gif" width="25%" height="25%">
  <img src="../images/face_reconstruction/Screencast From 2025-12-04 18-27-13.gif" width="25%" height="25%">
</div>

<div style="display: flex; justify-content: center; gap: 20px;">
  <img src="../images/face_reconstruction/stage2_depthLoss.svg" style="width:500px; height:auto;">
  <img src="../images/face_reconstruction/subject_2_stage2_depthLoss.svg" style="width:500px; height:auto;">
</div>

<p align="center">
<img src="../images/face_reconstruction/depth_subject_9.gif" width="30%" height="30%">
</p>

## Environment Map

To disentangle the skin reflectance and the light properties we used 2 approaches. Spherical Gaussian and a VAE-GAN.
<div style="display: flex; justify-content: center; gap: 20px;">
  <img src="../images/face_reconstruction/reference_sunlight.png" width="50%" height="50%">
  <img src="../images/face_reconstruction/10_lobes_sunlight.png" width="50%" height="50%">
</div>

<p align="center">
<img src="../images/face_reconstruction/Screencast From 2025-12-04 17-55-01.gif" width="60%" height="60%">
</p>
Low resolution gif creates aliasing artifact.

Using a generative approach provides some prior on the environment map. We use the data from Poly Haven. Below we see the comparison between the reference and the inference.
<div align="center">
  <img src="../images/face_reconstruction/vaegan1.png" style="width:800px; height:auto;">
</div>

The VAE-GAN approach provides a more continuous reconstruction over the blurry artifacts from a VAE. 
<div align="center">
  <img src="../images/face_reconstruction/vaegan_opt.png" style="width:800px; height:auto;">
</div>

## Symmetry Regularizer

We also explored using facial symmetry to regularize ear placement. Since only the right side is visible in the input image, we mirror its geometry to guide the occluded left side. The reflected ear provides a more accurate proxy allowing us to better constrain the reconstruction in regions without direct visual evidence.

## Next Steps

* Adaptive Sampling

* Texture Learning

* Autoencoder Model for the face

* Results and more information is available on request by contacting me: jiebao995@gmail.com

## References

Physically Based Rendering: From Theory to Implementation. From https://pbrt.org/

