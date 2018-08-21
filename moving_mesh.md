# Moving meshes in Fluidity
## AMCG, ESE, ICL
Moving Meshes Workshop, Reading 3rd Sept 2018



## What is Fluidity?

 - Nonhydrostatic Finite Element/Control Volume Navier Stokes solver on unstructured meshes.
 - Extensive (local) mesh adaptivity/optimization.
 - [fluidityproject.github.io](http://fluidityproject.github.io)


## Existing mesh adaptivity

 - Update out-of-timestep to
 - Optimize for Hessian-based error estimate of "good" mesh
 - New mesh is a better representation for static problems/"now".
 - Mesh-to-mesh interpolation [not cheap]



## Motivation 1: Deforming Domains


### 3D Bed Scour/Sediment Transport


### Ice Melt


### Fluid Solid Interaction



## Motivation 2: Accurate Advection

<video style="max-height: 300px;" controls>
<source src="./moving_mesh_etc/comparison.mp4" type="video/mp4">
</video>



## ALE formulation

Transform to fixed mesh coordinate, $\boldsymbol{\chi}$, plus moving physical coordinate, $\mathbf{x}$.

$$\dot{\mathbf{x}}(\boldsymbol{\chi})=\mathbf{v}(\boldsymbol{\chi})$$

Consistency demands $\mathbf{v}$ is piecewise linear to preserve simplices.


## Variable updates

From chain rule:
$$\left.\frac{\partial a}{\partial t}\right|\_{\boldsymbol{\chi}}
=\left.\frac{\partial a}{\partial t}\right|\_{\mathbf{x}}+\mathbf{v}\cdot\nabla_{\mathbf{x}} a.$$

i.e. incompressible N-S eqns look like

$$\left.\frac{\partial \mathbf{u}}{\partial t}\right|\_{\boldsymbol{\chi}}
+(\mathbf{u}-\mathbf{v})\cdot\nabla\_{\mathbf{x}} \mathbf{u}=-\frac{\nabla\_\mathbf{x} p}{\rho} +\nabla\_\mathbf{x}\cdot\mathbf{\underline{\tau}},$$
$$ \nabla\_\mathbf{x}\cdot\mathbf{u} =0. $$


### Derivative transformations

$$\frac{\partial a}{\partial x\_i} = \sum\_j \frac{\partial \chi_j}{\partial x_i}\frac{\partial a}{\partial \chi\_j}:=\sum\_j\mathcal{J}^{-1}\_{ij}\frac{\partial a}{\partial \chi\_j}$$



## Which mesh velocity?

 A good mesh velocity should:

 - avoid mesh tangling.
 - preserve resolution in boundary layers.
 - track Lagrangian velocity where appropriate.


### Method 1: Laplacian smoothing

 - The engineer's approach
$$ \nabla\_\mathbf{x}\cdot \gamma \nabla\_\mathbf{x} \mathbf{v} = \mathbf{0},\quad
 \mathbf{v}=\mathbf{V}\mbox{ on }\delta\Omega. $$ 
 -  Cheap to calculate
 -  Well behaved in 1D


### Method 2: Lineal Spring Analogy

After Farhat(19??). Replace mesh edges with linear springs. Solve equilibrium force balance equation for external loads/forcings.


### Method 3: Linear Elastic Analogy

$$ \sigma(\mathbf{x})=\mathbf{0}. $$
$$ \sigma(\mathbf{x}):=\lambda\nabla\_{\mathbf{x}\_0}\nabla\_{\mathbf{x}\_0}\cdot \mathbf{x}
+\mu\nabla\_{\mathbf{x}\_0}\cdot\left(\nabla\_{\mathbf{x}\_0}\mathbf{x}\+\left(\nabla\_{\mathbf{x}\_0}\mathbf{x}\right)^T\right)$$


### Method 4: Viscous Analogy

$$ \sigma(\mathbf{v})=\mathbf{0}. $$
$$ \sigma(\mathbf{v}):=\lambda\nabla\_\mathbf{x}\nabla\_\mathbf{x}\cdot \mathbf{v}
+\mu\nabla\_\mathbf{x}\cdot\left(\nabla\_\mathbf{x}\mathbf{v}+\left(\nabla\_\mathbf{x}\mathbf{v}\right)^T\right) +\alpha(\mathbf{u}-\mathbf{v}) $$


## Method 5: Lineal- torsional spring analogy

Springs on edges + coil springs on vertices.



### Comparison - runtime


### Comparison - robustness



### Results - Scour


## Thankyou for your attention



## References


