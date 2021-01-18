---
layout: project
type: project
published: True
image: images/side-180.gif
title: Turbulence Modeling with Tensorflow
permalink: projects/Turbulence_Modeling
# All dates must be YYYY-MM-DD format!
date: 2020-11-01
labels:
  - Machine Learning
  - TKE Transport Equation
  - RANS
summary: MASc research on artificially intelligent turbulence models built using direct numerical simulation.
---

## <i>Introduction</i>
The ubiquitous nature of turbulence is all around us. It influences many aspect of our every daily life. The air flowing in and out of our lungs is turbulent, as is the invisible air in the room in which you sit. Turbulent boundary layers dictate the vehicle's performance whether it's in the air or on the ground. Even the Earth's outer core of molten iron is turbulent, and it is this chaotic behaviour which maintains the terrestrial magnetic field against solar flares.

Needless to say, to hold a predictive model of turbulence would be paramount for the next step in human evolution. 

Our closest attempt to "<i>cage the beast</i>" is the direct numerical simulation (DNS). In theory, these type of simulations mimic the flow field down to the smallest eddy. However, they are tremendously expansive computational wise. Its greed exponentially with the Reynolds number, assuming computing rate of 1 gigaflop the time in days is (Pope, 2000): 

<br />

<div align="center">
  <img class="ui image" src="../images/MASc/pope_days.gif">
</div>

<br />

Currently, the Reynolds-averaged Navier-Stokes (RANS) equations are the most popular models
for simulating turbulence. Performing RANS simulation requires additional closure for the anisotropic
Reynolds stress tensor. Traditional approaches to the Reynolds stress closure are partially reliable
predictions. This is due to the elusive anisotropic nature of the eddy viscosity. In this project, data-driven turbulence models for the turbulent kinetic energy's production and dissipation terms have been developed to improve RANS accuracy. This model focuses on the turbulent channel case and the NACA 0012. Using limited training data a predictive 99% R2 score has been achieved.

## <i>Canonical Channel Case, Re=180 DNS</i>

<b> <i> The simulation was possible using the GPU cluster of Compute Canada and Calcul Quebec. </i> </b>

  <img class="ui image" src="../images/MASc/Dimension.gif">
<br />
  <img class="ui image" src="../images/MASc/Values.gif">


<div align="center">
  <img class="ui image" src="../images/iso.gif">
</div>


The simulation showcased above below is a direct numerical simulation (DNS) of the canonical wall bounded turbulent channel case. In which the whole spatial and temporal spectrum are solved for accurate turbulence prediction. The showcased simulation is from the dimensionless shear Reynolds of 180. The bulk Reynolds is found using the relationship from [Dean(1978)](https://ui.adsabs.harvard.edu/abs/1974STIN...7522638D/abstract).

<div align="center">
  <img class="ui image" src="../images/MASc/re_bulk.gif">
</div>

<br />

The flow field starts laminar and will transition into turbulent regime. However, this transition process can be very slow. Therefore, we can accelerate the transition by adding perturbation in the initial condition:

<div align="center">
  <img class="ui image" src="../images/MASc/transition_u.gif">
</div>

<br />

<div align="center">
  <img class="ui image" src="../images/MASc/transition_vv.gif">
</div>

<br />

<div align="center">
  <img class="ui image" src="../images/MASc/transition_w.gif">
</div>


### Production and Dissipation
<div align="center">
  <img class="ui image" src="../images/MASc/Production.gif">
</div>

<br />

<div align="center">
  <img class="ui image" src="../images/MASc/Dissipation.gif">
</div>



<br />

Another important disctinction is the compressibility of the fluid. We know for higher Mach numbers, the flow field's density will start to fluctuate. Although, it is not the case here. The Favre averaging is applied for future application with compressible flows. To see how the derivation is applied visit this [page](https://jiebao.ca/essays/Amid-Organized-Chaos.html) and the source can be found on official <a href="https://www.sto.nato.int/publications/AGARD/Forms/AllItems.aspx?RootFolder=%2Fpublications%2FAGARD%2FAGARD%2DR%2D819&FolderCTID=0x0120D5200078F9E87043356C409A0D30823AFA16F60B00B8BCE98BB37EB24A8258823D6B11F157&View=%7B7E9C814C-056A-4D31-8392-7C6752B2AF2B%7D
">AGARD-R-819 </a>.

## Turbulence Modeling with Tensorflow

### Data Pre-processing

The dataset consists of 56 features, 1 continuous output, and 32 325 instances. All features are complete with no missing values. Notice the high number of features. To filter out the unecessary features, we must remember the end goal of the machine learning approach; to improve the RANS solver. This means we are limited to the same input. In other words, the dataset (production and dissipation) are extracted from the DNS of the Turbulent Channel. As such, the Reynolds stress is known but not in the RANS in framework. The plot below is an implementation of the Relief algorithm for regression problem with all the features that would be available.

<div align="center"  ><b> RReliefF Feature Importance</b></div>

<div align="center">
  <img class="ui image" src="../images/MASc/RReliefF.png" width="80%" height="80%">
</div>

<br />

Another aspect is from the mechanics of turbulence. A corollary is that the cross-correlation vanishes inside the unstrained turbulence. In the turbulence channel case, this corresponds to the region in the center of the channel. Albeit with a certain lag. Thus, it was decided to remove those features. 
 
<div align="center">
  <img class="ui image" src="../images/MASc/features.gif" >
</div>

<br />

Once the features are determined, feature scaling is performed. Data transformation by [standardization ](https://arxiv.org/abs/1502.03167) is applied since it has been shown to speed up convergence via gradient descent and implicitly balances the contribution of all features. Standardization is also required for proper L2 regularization.

```js
def get_data_validation(self, test: bool = False) -> Tuple[pd.DataFrame, pd.DataFrame]:
    """
    Similar to get_data(), this function will take the non-shuffled data instead.
    """
    df_x = self.X_test if test else self.X_train
    df_y = self.y_test if test else self.y_train
    return df_x.copy(deep=True), df_y.copy(deep=True)

def _set_standardize_values_validation(self, test):
    # we do not standardize the test labels
    df = self.get_continuous_data()[0]
    self.means = df.mean()
    self.stds = df.std()
    df = (df - self.means) / self.stds
    return df
```

At the time of writing this, more physics based solution are being tested. Such as replacing a layer's bias to the corresponding shear Reynolds Number of the training instance. Add more physics based features such as the wall shear velocity. <b> The intuition is to give the machine learning training a higher-level of understanding. </b>

### MLP Architecture

<div align="center">
  <img class="ui image" src="../images/MASc/table_cases.png">
</div>

You can see the Python code on my<a href="https://github.com/DiscoBroccoli/Turbulent-Modelling-using-Machine-Learning-Techniques"><i class="large github icon"></i>Github repo </a>(soon to come...).


<div align="center">
  <img class="ui image" src="../images/side-180.gif">
</div>

Sources:

* S. Ioffe and C. Szegedy, “Batch normalization: Accelerating deep network training by reducing
internal covariate shift,” 2015.




