---
layout: essay
type: essay
title: Amid Organized Chaos 
# All dates must be YYYY-MM-DD format!
date: 2020-12-26
labels:
  - Turbulence
  - TKE Transport Equation
  - RANS
---

<img class="ui medium left floated image" src="../images/prod_diss.gif">


Fundamental research in turbulence is hard. It requires a good understanding of applied mathematics and a firm grasp of the physical phenomena into the dynamics of fluids. The closure problem to the Reynolds Averaged Navier-Stokes (RANS) motivated leading experts to construct models. This undertaking is called turbulence modelling. Calibration is the foundation underlying the constructions of such turbulent models. 

<br />

As such, the unknown double and triple correlations are replaced with algebraic expressions involving known quantities and closure coefficients. For instance, the k-w model's kinetic energy temporal derivative is calibrated to experimental obervation [see Townsend (1976)] for decaying homogeneous, isotropic turbulence.

New development in GPUs and machine/deep learning are changing the landscape for modern turbulence modelling. A new approach involves performing a limited amount of direct numerical simulation and training a neural network to predict the eddy viscosity.

The reader might already be aware, the equations are usually presented using the Einstein Covention. The turbulent kinetic energy equation is

<p align="center">
<img src="../images/TKE_transport.gif">
</p>

<p align="center">
<img src="../images/table_PD.png">
</p>

Among the unknown terms in the turbulent kinetic transport equation, the Pressure Diffusion Turbulent Diffusion are small for simple shear flows. Therefore, in the case of a turbulent channel flow, we will focus on deconstructing the <i>Production Dissipation</i> terms.

<b> Production - <i>A</i> </b>

Similarly to the <i> Reynolds decomposition </i>, The <i> Favre averaging </i> has a mean and fluctuating part. It is applied to take into accound the density change in the flow field.  

Some useful rules:

<p align="center">
<img src="../images/favre_f.gif">
</p>


<p align="center">
<img src="../images/favre_decomposition.gif">
</p>


<p align="center">
<img src="../images/favre_invariant.gif">
</p>


<p align="center">
<img src="../images/favre_zero.gif">
</p>

<br />

<p align="center">
<img src="../images/Production_A.gif">
</p>

<br />

<p align="center">
<img src="../images/Prod_part1.gif">
</p>


<p align="center">
<img src="../images/Prod_part2.gif">
</p>


<br />

Apply quotient rule on the numerator:

<p align="center">
<img src="../images/Prod_quot_rule.gif">
</p>

<br />

Apply the product rule on the first term:

<p align="center">
<img src="../images/Prod_product_rule.gif">
</p>

<br />
Finally, the production is:

<p align="center">
<img src="../images/Production_final.gif">
</p>


<br />

<b> Dissipation - <i> D </i> <b>

Firts, the laminar stress tensor must be defined and not to be confused with the mean molecular viscous stress. They use the same greek letter tau in the litterature.

<p align="center">
<img src="../images/laminar_stress_tensor.gif">
</p>

<br />

The equation with Einstein notation.

<p align="center">
<img src="../images/Dissip_prior.gif">
</p>

<br />

The final dissipation equation is:

<p align="center">
<img src="../images/Dissip_final.gif">
</p>

<br />

In the interest of keeping this short, the entire proof (similar to production) can be found on my <a href="https://github.com/DiscoBroccoli/Turbulent-Modelling-using-Machine-Learning-Techniques/blob/main/documents/Favre-Averaging.pdf"><i class="large github icon "></i>github</a> page. Notice how large the equation becomes, the code in python is included on my github page as well.


