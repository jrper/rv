# Moving meshes in Fluidity



## What is Fluidity?

 - [fluidityproject.github.io](http://fluidityproject.github.io)
 - Nonhydrostatic Finite Element/Control Volume Navier Stokes solver on unstructured meshes.
 - Extensive (local) mesh adaptivity/optimization.


## Existing mesh adaptivity

 - Update out-of-timestep to
 - Optimize for Hessian-based error estimate of "good" mesh
 - New mesh is a better representation for static problems/"now".
 - Mesh-to-mesh interpolation [not cheap]



## Deforming Domains



## Accurate Advection

<video style="max-height: 300px;" controls>
<source src="./moving_mesh_etc/comparison.mp4" type="video/mp4">
</video>



## ALE formulation

Transition to static mesh coordinate, $\boldsymbol{\chi}$, plus moving physical coordinate, $\mathbf{x}$.

$$\dot{\mathbf{x}}(\boldsymbol{\chi})=\mathbf{v}(\boldsymbol{\chi})$$

Consistency demands $\mathbf{v}$ is piecewise linear to preserve simplices.


## Variable updates

From chain rule:
$$\left.\frac{\partial a}{\partial t}\right|\_{\boldsymbol{\chi}}
=\left.\frac{\partial a}{\partial t}\right|\_{\mathbf{x}}+\mathbf{v}\cdot\nabla_{\mathbf{x}} a.$$

i.e.

$$\left.\frac{\partial \mathbf{u}}{\partial t}\right|\_{\boldsymbol{\chi}}
+(\mathbf{u}-\mathbf{v})\cdot\nabla\_{\mathbf{x}} \mathbf{u}=-\frac{\nabla\_\mathbf{x} p}{\rho} +\nabla\_\mathbf{x}\cdot\mathbf{\underline{\tau}},$$
$$ \nabla\_\mathbf{x}\cdot\mathbf{u} =0. $$



## Which mesh velocity?

 A good mesh velocity should:

 - avoid mesh tangling.
 - preserve resolution in boundary layers.
 - track Lagrangian velocity where appropriate.


### Method 1: Laplacian smoothing

 - The engineer's approach
$$ \nabla_\mathbf{x}^2 \mathbf{v} = \mathbf{0},\quad
 \mathbf{v}=\mathbf{V}\mbox{ on }\delta\Omega. $$ 
 -  Cheap to calculate
 -  Well behaved in 1D


### Method 2: Lineal Spring Analogy

After Farhat(19??). Replace mesh edges with linear springs. Solve equilibrium force balance equation for external loads/forcings.


### Method 3: Linear Elastic Analogy

$$ \sigma(\mathbf{x})=\mathbf{0}. $$
$$ \sigma(\mathbf{x}):=\lambda\nabla\_\mathbf{X}\nabla\_\mathbf{X}\cdot \mathbf{x}
+\mu\nabla\_\mathbf{X}\cdot\left(\nabla\_\mathbf{X}\mathbf{x}+\left(\nabla\_\mathbf{X}\mathbf{x}\right)^T\right)$$


### Method 4: Viscous Analogy

$$ \sigma(\mathbf{v})=\mathbf{0}. $$
$$ \sigma(\mathbf{v}):=\lambda\nabla\_\mathbf{x}\nabla\_\mathbf{x}\cdot \mathbf{v}
+\mu\nabla\_\mathbf{x}\cdot\left(\nabla\_\mathbf{x}\mathbf{v}+\left(\nabla\_\mathbf{x}\mathbf{v}\right)^T\right)$$


## Method 5: Lineal- torsional spring analogy

Springs on edges + coil springs on vertices.


### Comparison - runtime


### Comparison - robustness



## Thankyou for your attention



## References


