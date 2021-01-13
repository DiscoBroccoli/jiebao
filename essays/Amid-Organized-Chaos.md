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

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <mover>
          <mi>ρ</mi>
          <mo accent="true">‾</mo>
        </mover>
        <mi>k</mi>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <mi>t</mi>
      </mrow>
    </mfrac>
    <mo>+</mo>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <mover>
          <mi>ρ</mi>
          <mo accent="true">‾</mo>
        </mover>
        <mi>k</mi>
        <mover>
          <msub>
            <mi>u</mi>
            <mi>i</mi>
          </msub>
          <mo accent="true">̃</mo>
        </mover>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>i</mi>
        </msub>
      </mrow>
    </mfrac>
    <mo>=</mo>
    <mi>A</mi>
    <mo>+</mo>
    <mi>B</mi>
    <mo>+</mo>
    <mi>C</mi>
    <mo>+</mo>
    <mi>D</mi>
  </mrow>
</math>

<p align="center">
<img src="../images/table_PD.png">
</p>

Among the unknown terms in the turbulent kinetic transport equation, the Pressure Diffusion Turbulent Diffusion are small for simple shear flows. Therefore, in the case of a turbulent channel flow, we will focus on deconstructing the <i>Production Dissipation</i> terms.

<b> Production - <i>A</i> </b>

Similarly to the <i> Reynolds decomposition </i>, The <i> Favre averaging </i> has a mean and fluctuating part. It is applied to take into accound the density change in the flow field.  

Some useful rules:

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mover>
      <mi>f</mi>
      <mo accent="true">̃</mo>
    </mover>
    <mo>=</mo>
    <mfrac>
      <mover>
        <mrow>
          <mi>ρ</mi>
          <mi>f</mi>
        </mrow>
        <mo accent="true">¯</mo>
      </mover>
      <mover>
        <mi>ρ</mi>
        <mo accent="true">‾</mo>
      </mover>
    </mfrac>
  </mrow>
</math>

<br />

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi>f</mi>
    <mo>=</mo>
    <mover>
      <mi>f</mi>
      <mo accent="true">̃</mo>
    </mover>
    <mo>+</mo>
    <mi>f</mi>
    <mi>″</mi>
  </mrow>
</math>

<br />

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mover>
      <mover>
        <mi>f</mi>
        <mo accent="true">̃</mo>
      </mover>
      <mo accent="true">‾</mo>
    </mover>
    <mo>=</mo>
    <mover>
      <mi>f</mi>
      <mo accent="true">̃</mo>
    </mover>
  </mrow>
</math>

<br />

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mover>
      <mrow>
        <mi>ρ</mi>
        <mi>f</mi>
        <mi>″</mi>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>=</mo>
    <mn>0</mn>
  </mrow>
</math>

<br />

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi>A</mi>
    <mo>=</mo>
    <munder>
      <munder>
        <mrow>
          <mo>−</mo>
          <mover>
            <mrow>
              <mi>ρ</mi>
              <msub>
                <mi>u</mi>
                <mi>i</mi>
              </msub>
              <mi>″</mi>
              <msub>
                <mi>u</mi>
                <mi>j</mi>
              </msub>
              <mi>″</mi>
            </mrow>
            <mo accent="true">¯</mo>
          </mover>
        </mrow>
        <mo accent="true">⏟</mo>
      </munder>
      <mtext mathvariant="normal">part 1</mtext>
    </munder>
    <mspace width="0.222em" />
    <munder>
      <munder>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mover>
                <mi>u</mi>
                <mo accent="true">̃</mo>
              </mover>
              <mi>i</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
        <mo accent="true">⏟</mo>
      </munder>
      <mtext mathvariant="normal">part 2</mtext>
    </munder>
  </mrow>
</math>


<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mo>−</mo>
    <munder>
      <munder>
        <mover>
          <mrow>
            <mi>ρ</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
            <mi>″</mi>
            <msub>
              <mi>u</mi>
              <mi>j</mi>
            </msub>
            <mi>″</mi>
          </mrow>
          <mo accent="true">¯</mo>
        </mover>
        <mo accent="true">⏟</mo>
      </munder>
      <mtext mathvariant="normal">part 1</mtext>
    </munder>
    <mo>=</mo>
    <mo>−</mo>
    <mover>
      <mrow>
        <mi>ρ</mi>
        <msub>
          <mi>u</mi>
          <mi>i</mi>
        </msub>
        <msub>
          <mi>u</mi>
          <mi>j</mi>
        </msub>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>+</mo>
    <mover>
      <mrow>
        <mn>2</mn>
        <mi>ρ</mi>
        <msub>
          <mi>u</mi>
          <mi>i</mi>
        </msub>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <msub>
      <mover>
        <mi>u</mi>
        <mo accent="true">̃</mo>
      </mover>
      <mi>j</mi>
    </msub>
    <mo>−</mo>
    <mover>
      <mi>ρ</mi>
      <mo accent="true">‾</mo>
    </mover>
    <mover>
      <msub>
        <mi>u</mi>
        <mi>i</mi>
      </msub>
      <mo accent="true">̃</mo>
    </mover>
    <mover>
      <msub>
        <mi>u</mi>
        <mi>j</mi>
      </msub>
      <mo accent="true">̃</mo>
    </mover>
    <mo>=</mo>
    <mo>−</mo>
    <mover>
      <mrow>
        <mi>ρ</mi>
        <msub>
          <mi>u</mi>
          <mi>i</mi>
        </msub>
        <msub>
          <mi>u</mi>
          <mi>j</mi>
        </msub>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>+</mo>
    <mn>2</mn>
    <mover>
      <msub>
        <mi>u</mi>
        <mi>i</mi>
      </msub>
      <mo accent="true">‾</mo>
    </mover>
    <mover>
      <mrow>
        <mi>ρ</mi>
        <msub>
          <mi>u</mi>
          <mi>j</mi>
        </msub>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>−</mo>
    <mover>
      <mi>ρ</mi>
      <mo accent="true">‾</mo>
    </mover>
    <mfrac>
      <mover>
        <mrow>
          <mi>ρ</mi>
          <msub>
            <mi>u</mi>
            <mi>i</mi>
          </msub>
        </mrow>
        <mo accent="true">¯</mo>
      </mover>
      <mover>
        <mi>ρ</mi>
        <mo accent="true">‾</mo>
      </mover>
    </mfrac>
    <mfrac>
      <mover>
        <mrow>
          <mi>ρ</mi>
          <msub>
            <mi>u</mi>
            <mi>j</mi>
          </msub>
        </mrow>
        <mo accent="true">¯</mo>
      </mover>
      <mover>
        <mi>ρ</mi>
        <mo accent="true">‾</mo>
      </mover>
    </mfrac>
  </mrow>
</math>



<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <munder>
      <munder>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mover>
                <mi>u</mi>
                <mo accent="true">̃</mo>
              </mover>
              <mi>i</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
        <mo accent="true">⏟</mo>
      </munder>
      <mtext mathvariant="normal">part 2</mtext>
    </munder>
    <mo>=</mo>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <mrow>
          <mo stretchy="true" form="prefix">(</mo>
          <mfrac>
            <mover>
              <mrow>
                <mi>ρ</mi>
                <msub>
                  <mi>u</mi>
                  <mi>i</mi>
                </msub>
              </mrow>
              <mo accent="true">¯</mo>
            </mover>
            <mover>
              <mi>ρ</mi>
              <mo accent="true">‾</mo>
            </mover>
          </mfrac>
          <mo stretchy="true" form="postfix">)</mo>
        </mrow>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>j</mi>
        </msub>
      </mrow>
    </mfrac>
  </mrow>
</math>

<br />

Apply quotient rule on the numerator:

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mover>
            <mi>u</mi>
            <mo accent="true">̃</mo>
          </mover>
          <mi>i</mi>
        </msub>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>j</mi>
        </msub>
      </mrow>
    </mfrac>
    <mo>=</mo>
    <mfrac>
      <mrow>
        <mover>
          <mi>ρ</mi>
          <mo accent="true">‾</mo>
        </mover>
        <mspace width="0.222em" />
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <mover>
              <mrow>
                <mi>ρ</mi>
                <msub>
                  <mi>u</mi>
                  <mi>i</mi>
                </msub>
              </mrow>
              <mo accent="true">¯</mo>
            </mover>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
        <mo>−</mo>
        <mover>
          <mrow>
            <mi>ρ</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
          </mrow>
          <mo accent="true">¯</mo>
        </mover>
        <mspace width="0.222em" />
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <mover>
              <mi>ρ</mi>
              <mo accent="true">‾</mo>
            </mover>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>i</mi>
            </msub>
          </mrow>
        </mfrac>
      </mrow>
      <mrow>
        <mover>
          <mi>ρ</mi>
          <mo accent="true">‾</mo>
        </mover>
        <msup>
          <mspace width="0.222em" />
          <mn>2</mn>
        </msup>
      </mrow>
    </mfrac>
  </mrow>
</math>

<br />

Apply the product rule on the first term:

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mover>
            <mi>u</mi>
            <mo accent="true">̃</mo>
          </mover>
          <mi>i</mi>
        </msub>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>j</mi>
        </msub>
      </mrow>
    </mfrac>
    <mo>=</mo>
    <mfrac>
      <mrow>
        <mover>
          <mi>ρ</mi>
          <mo accent="true">‾</mo>
        </mover>
        <mrow>
          <mo stretchy="true" form="prefix">[</mo>
          <mspace width="0.222em" />
          <mover>
            <mrow>
              <mfrac>
                <mrow>
                  <mi>∂</mi>
                  <mi>ρ</mi>
                </mrow>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>x</mi>
                    <mi>j</mi>
                  </msub>
                </mrow>
              </mfrac>
              <msub>
                <mi>u</mi>
                <mi>i</mi>
              </msub>
            </mrow>
            <mo accent="true">¯</mo>
          </mover>
          <mo>+</mo>
          <mover>
            <mrow>
              <mi>ρ</mi>
              <mfrac>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>u</mi>
                    <mi>i</mi>
                  </msub>
                </mrow>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>x</mi>
                    <mi>j</mi>
                  </msub>
                </mrow>
              </mfrac>
            </mrow>
            <mo accent="true">¯</mo>
          </mover>
          <mspace width="0.222em" />
          <mo stretchy="true" form="postfix">]</mo>
        </mrow>
        <mo>−</mo>
        <mover>
          <mrow>
            <mi>ρ</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
          </mrow>
          <mo accent="true">¯</mo>
        </mover>
        <mspace width="0.278em" />
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <mover>
              <mi>ρ</mi>
              <mo accent="true">‾</mo>
            </mover>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
      </mrow>
      <mrow>
        <mover>
          <mi>ρ</mi>
          <mo accent="true">‾</mo>
        </mover>
        <msup>
          <mspace width="0.222em" />
          <mn>2</mn>
        </msup>
      </mrow>
    </mfrac>
  </mrow>
</math>

<br />
Finally, the production is:


<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi>A</mi>
    <mo>=</mo>
    <mo stretchy="false" form="prefix">(</mo>
    <mo>−</mo>
    <mover>
      <mrow>
        <mi>ρ</mi>
        <msub>
          <mi>u</mi>
          <mi>i</mi>
        </msub>
        <msub>
          <mi>u</mi>
          <mi>j</mi>
        </msub>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>+</mo>
    <mn>2</mn>
    <mover>
      <msub>
        <mi>u</mi>
        <mi>i</mi>
      </msub>
      <mo accent="true">‾</mo>
    </mover>
    <mover>
      <mrow>
        <mi>ρ</mi>
        <msub>
          <mi>u</mi>
          <mi>j</mi>
        </msub>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>−</mo>
    <mover>
      <mi>ρ</mi>
      <mo accent="true">‾</mo>
    </mover>
    <mfrac>
      <mover>
        <mrow>
          <mi>ρ</mi>
          <msub>
            <mi>u</mi>
            <mi>i</mi>
          </msub>
        </mrow>
        <mo accent="true">¯</mo>
      </mover>
      <mover>
        <mi>ρ</mi>
        <mo accent="true">‾</mo>
      </mover>
    </mfrac>
    <mfrac>
      <mover>
        <mrow>
          <mi>ρ</mi>
          <msub>
            <mi>u</mi>
            <mi>j</mi>
          </msub>
        </mrow>
        <mo accent="true">¯</mo>
      </mover>
      <mover>
        <mi>ρ</mi>
        <mo accent="true">‾</mo>
      </mover>
    </mfrac>
    <mo stretchy="false" form="postfix">)</mo>
    <mo>×</mo>
    <mfrac>
      <mrow>
        <mover>
          <mi>ρ</mi>
          <mo accent="true">‾</mo>
        </mover>
        <mrow>
          <mo stretchy="true" form="prefix">[</mo>
          <mspace width="0.222em" />
          <mover>
            <mrow>
              <mfrac>
                <mrow>
                  <mi>∂</mi>
                  <mi>ρ</mi>
                </mrow>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>x</mi>
                    <mi>j</mi>
                  </msub>
                </mrow>
              </mfrac>
              <msub>
                <mi>u</mi>
                <mi>i</mi>
              </msub>
            </mrow>
            <mo accent="true">¯</mo>
          </mover>
          <mo>+</mo>
          <mover>
            <mrow>
              <mi>ρ</mi>
              <mfrac>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>u</mi>
                    <mi>i</mi>
                  </msub>
                </mrow>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>x</mi>
                    <mi>j</mi>
                  </msub>
                </mrow>
              </mfrac>
            </mrow>
            <mo accent="true">¯</mo>
          </mover>
          <mspace width="0.222em" />
          <mo stretchy="true" form="postfix">]</mo>
        </mrow>
        <mo>−</mo>
        <mover>
          <mrow>
            <mi>ρ</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
          </mrow>
          <mo accent="true">¯</mo>
        </mover>
        <mspace width="0.278em" />
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <mover>
              <mi>ρ</mi>
              <mo accent="true">‾</mo>
            </mover>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
      </mrow>
      <mrow>
        <mover>
          <mi>ρ</mi>
          <mo accent="true">‾</mo>
        </mover>
        <msup>
          <mspace width="0.222em" />
          <mn>2</mn>
        </msup>
      </mrow>
    </mfrac>
  </mrow>
</math>

<br />

<b> Dissipation - <i> D </i> <b>

Firts, the laminar stress tensor must be defined and not to be confused with the mean molecular viscous stress. They use the same greek letter tau in the litterature.

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <msub>
      <mi>τ</mi>
      <mrow>
        <mi>i</mi>
        <mi>j</mi>
      </mrow>
    </msub>
    <mo>=</mo>
    <mi>λ</mi>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>u</mi>
          <mi>k</mi>
        </msub>
      </mrow>
      <msub>
        <mi>x</mi>
        <mi>k</mi>
      </msub>
    </mfrac>
    <msub>
      <mi>δ</mi>
      <mrow>
        <mi>i</mi>
        <mi>j</mi>
      </mrow>
    </msub>
    <mo>+</mo>
    <mi>μ</mi>
    <mrow>
      <mo stretchy="true" form="prefix">(</mo>
      <mfrac>
        <mrow>
          <mi>∂</mi>
          <msub>
            <mi>u</mi>
            <mi>i</mi>
          </msub>
        </mrow>
        <mrow>
          <mi>∂</mi>
          <msub>
            <mi>x</mi>
            <mi>j</mi>
          </msub>
        </mrow>
      </mfrac>
      <mo>+</mo>
      <mfrac>
        <mrow>
          <mi>∂</mi>
          <msub>
            <mi>u</mi>
            <mi>j</mi>
          </msub>
        </mrow>
        <mrow>
          <mi>∂</mi>
          <msub>
            <mi>x</mi>
            <mi>i</mi>
          </msub>
        </mrow>
      </mfrac>
      <mo stretchy="true" form="postfix">)</mo>
    </mrow>
  </mrow>
</math>

The equation with Einstein notation.

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi>D</mi>
    <mo>=</mo>
    <mover>
      <mrow>
        <msub>
          <mi>τ</mi>
          <mrow>
            <mi>i</mi>
            <mi>j</mi>
          </mrow>
        </msub>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
            <mi>″</mi>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>=</mo>
    <mover>
      <mrow>
        <mrow>
          <mo stretchy="true" form="prefix">(</mo>
          <munder>
            <munder>
              <mrow>
                <mi>λ</mi>
                <mfrac>
                  <mrow>
                    <mi>∂</mi>
                    <msub>
                      <mi>u</mi>
                      <mi>k</mi>
                    </msub>
                  </mrow>
                  <mrow>
                    <mi>∂</mi>
                    <msub>
                      <mi>x</mi>
                      <mi>k</mi>
                    </msub>
                  </mrow>
                </mfrac>
                <msub>
                  <mi>δ</mi>
                  <mrow>
                    <mi>i</mi>
                    <mi>j</mi>
                  </mrow>
                </msub>
              </mrow>
              <mo accent="true">⏟</mo>
            </munder>
            <mtext mathvariant="normal">part 1</mtext>
          </munder>
          <mo>+</mo>
          <mi>μ</mi>
          <mo stretchy="false" form="prefix">(</mo>
          <munder>
            <munder>
              <mfrac>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>u</mi>
                    <mi>i</mi>
                  </msub>
                </mrow>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>x</mi>
                    <mi>j</mi>
                  </msub>
                </mrow>
              </mfrac>
              <mo accent="true">⏟</mo>
            </munder>
            <mtext mathvariant="normal">part 2</mtext>
          </munder>
          <mo>+</mo>
          <munder>
            <munder>
              <mfrac>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>u</mi>
                    <mi>j</mi>
                  </msub>
                </mrow>
                <mrow>
                  <mi>∂</mi>
                  <msub>
                    <mi>x</mi>
                    <mi>i</mi>
                  </msub>
                </mrow>
              </mfrac>
              <mo accent="true">⏟</mo>
            </munder>
            <mtext mathvariant="normal">part 3</mtext>
          </munder>
          <mo stretchy="false" form="postfix">)</mo>
          <mo stretchy="true" form="postfix">)</mo>
        </mrow>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
            <mi>″</mi>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
  </mrow>
</math>

The final dissipation equation is:

<math display="block" xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi>D</mi>
    <mo>=</mo>
    <mover>
      <mrow>
        <mo>−</mo>
        <mfrac>
          <mn>2</mn>
          <mn>3</mn>
        </mfrac>
        <mi>μ</mi>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>k</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>k</mi>
            </msub>
          </mrow>
        </mfrac>
        <msub>
          <mi>δ</mi>
          <mrow>
            <mi>i</mi>
            <mi>j</mi>
          </mrow>
        </msub>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>+</mo>
    <mover>
      <mrow>
        <mfrac>
          <mn>2</mn>
          <mn>3</mn>
        </mfrac>
        <mi>μ</mi>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>k</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>k</mi>
            </msub>
          </mrow>
        </mfrac>
        <msub>
          <mi>δ</mi>
          <mrow>
            <mi>i</mi>
            <mi>j</mi>
          </mrow>
        </msub>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mover>
            <mi>u</mi>
            <mo accent="true">̃</mo>
          </mover>
          <mi>i</mi>
        </msub>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>j</mi>
        </msub>
      </mrow>
    </mfrac>
    <mo>+</mo>
    <mi>μ</mi>
    <mover>
      <mrow>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>−</mo>
    <mi>μ</mi>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mover>
            <mi>u</mi>
            <mo accent="true">‾</mo>
          </mover>
          <mi>i</mi>
        </msub>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>j</mi>
        </msub>
      </mrow>
    </mfrac>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mover>
            <mi>u</mi>
            <mo accent="true">̃</mo>
          </mover>
          <mi>i</mi>
        </msub>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>j</mi>
        </msub>
      </mrow>
    </mfrac>
    <mo>+</mo>
    <mi>μ</mi>
    <mover>
      <mrow>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>j</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>i</mi>
            </msub>
          </mrow>
        </mfrac>
        <mfrac>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>u</mi>
              <mi>i</mi>
            </msub>
          </mrow>
          <mrow>
            <mi>∂</mi>
            <msub>
              <mi>x</mi>
              <mi>j</mi>
            </msub>
          </mrow>
        </mfrac>
      </mrow>
      <mo accent="true">¯</mo>
    </mover>
    <mo>−</mo>
    <mi>μ</mi>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mover>
            <mi>u</mi>
            <mo accent="true">‾</mo>
          </mover>
          <mi>j</mi>
        </msub>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>i</mi>
        </msub>
      </mrow>
    </mfrac>
    <mfrac>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mover>
            <mi>u</mi>
            <mo accent="true">̃</mo>
          </mover>
          <mi>i</mi>
        </msub>
      </mrow>
      <mrow>
        <mi>∂</mi>
        <msub>
          <mi>x</mi>
          <mi>j</mi>
        </msub>
      </mrow>
    </mfrac>
  </mrow>
</math>

<br />

In the interest of keeping this short, the entire proof (similar to production) can be found on my <a href="https://github.com/DiscoBroccoli/Turbulent-Modelling-using-Machine-Learning-Techniques/blob/main/documents/Favre-Averaging.pdf"><i class="large github icon "></i>github</a> page. Notice how large the equation becomes, the code in python is included on my github page as well.


