<script type="text/x-mathjax-config">
  MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$']]}});
</script>
<script type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-AMS_HTML">
</script>

# Example Applications

This page provides a list of libROM example applications.  For detailed
documentation of the libROM sources, including the examples, see the [online
Doxygen documentation](http://mfem.github.io/doxygen/html/index.html),<- (needs
update) or the `doc` directory in the distribution.  The goal of the example
codes is to provide a step-by-step introduction to libROM in simple model
settings. 

Select from the categories below to display examples and miniapps that contain
the respective feature. _All examples support (arbitrarily) high-order meshes
and finite element spaces_.  The numerical results from the example codes can be
visualized using the GLVis visualization tool (based on libROM). See the [GLVis
website](http://glvis.org) for more details.

Users are encouraged to submit any example codes and miniapps that they have
created and would like to share. <br>
_Contact a member of the libROM team to report
[bugs](https://github.com/LLNL/libROM/labels/bug)
or post [questions](https://github.com/LLNL/libROM/labels/question) 
or [comments](https://github.com/LLNL/libROM/labels/comments)_.

<div class="row" markdown="1">
<div class="col-sm-6 col-md-2 small" markdown="1">
   <h5>**Application (PDE)**</h5>
   <select id="group1" onchange="update()">
      <option id="all1">All</option>
      <option id="diffusion">Diffusion</option>
      <option id="compressibleflow">Compressible flow</option>
   </select>
</div>
<div class="col-sm-6 col-md-3 small" markdown="1">
   <h5>**Finite Elements**</h5>
   <select id="group2" onchange="update()">
      <option id="all2">All</option>
      <option id="h1">H1 nodal elements</option>
      <option id="l2">L2 discontinuous elements</option>
   </select>
</div>
<div class="clearfix hidden-md hidden-lg"></div>
<div class="col-sm-6 col-md-3 small" markdown="1">
   <h5>**Discretization**</h5>
   <select id="group3" onchange="update()">
      <option id="all3">All</option>
      <option id="galerkin">Galerkin FEM</option>
      <option id="staticcond">Static condensation</option>
      <option id="nurbs">Isogeometric analysis (NURBS)</option>
      <option id="dg">Discontinuous Galerkin (DG)</option>
      <option id="pa">Partial assembly</option>
   </select>
</div>
<div class="col-sm-6 col-md-4 small" markdown="1">
   <h5>**Solver**</h5>
   <select id="group4" onchange="update()">
      <option id="all4">All</option>
      <option id="gs">Gauss-Seidel</option>
      <option id="pcg">PCG</option>
      <option id="umfpack">UMFPACK (serial direct)</option>
      <option id="petsc">PETSc solvers</option>
      <option id="amg">Algebraic Multigrid (BoomerAMG)</option>
      <option id="rk">Explicit Runge-Kutta (ODE integration)</option>
   </select>
</div>
</div>
<br>
<hr>

<!-- ------------------------------------------------------------------------- -->

<div id="poisson" markdown="1">
## Poisson Problem
<a target="_blank">
<img class="floatright" src="../img/examples/poisson.png" width="250">
</a>

This example code demonstrates the use of libROM and MFEM to define a reduced
order model for a simple isoparametric finite element discretization of the
Poisson problem $$-\Delta u = f$$ with homogeneous Dirichlet boundary
conditions. The example parameterizes the righthand side with frequency
variable, $\kappa$:

$$f =  
  \cases{
  \displaystyle \sin(\kappa (x_0+x_1+x_2)) & for 2D  \cr
  \displaystyle \sin(\kappa (x_0+x_1))     & for 3D  
  }$$

The 2D solutoin contour plot for $\kappa=1$ is shown in the figure
on the right to show the effect of $\kappa$. For demonstration, we sample
solutions at $\kappa=1$, $1.1$, and $1.2$. Then a ROM is build with basis size
of 3, which is used to predict the solution for $\kappa = 1.15$.  The ROM is
able to achieve a speedup of $7.5$ with a relative error of $6.4\times10^{-4}$.
One can follow the command line options below to reproduce the numerical results
summarized in the table below:

* **offline1**: poisson -offline -f 1.0 -id 0
* **offline2**: poisson -offline -f 1.1 -id 1
* **offline3**: poisson -offline -f 1.2 -id 2
* **merge**: poisson -merge -ns 3 
* **online**: poisson -online -f 1.15

   |    | FOM solution time | ROM solution time | Speed-up | Solution relative error |
   | -- | ----------------- | ----------------- | -------- | ----------------------- |
   |    |  0.22 sec         |  0.029 sec        |   7.5    |           6.4e-4        |


_The code to generate the numerical results above can be found in ([poisson.cpp](https://github.com/LLNL/libROM/blob/master/examples/poisson.cpp)) and the explanation of codes is provided in [here]()_
<div style="clear:both;"></div>
<br></div>

<div id="laghos" markdown="1">
##Laghos ROM Miniapp

**Laghos** (LAGrangian High-Order Solver) is a miniapp that solves the
time-dependent Euler equations of compressible gas dynamics in a moving
Lagrangian frame using unstructured high-order finite element spatial
discretization and explicit high-order time-stepping. **LaghosROM** introduces
reduced order models of Laghos simulations. 

A list of example problems that you can solve with LaghosROM includes Sedov
blast, Gresho vortex, Taylor-Green vortex, triple-point, and Rayleigh-Taylor
instability problems. Below are command line options for each problems and some
numerical results. For each problem, four different phases need to be taken,
i.e., the offline, hyper-reduction preprocessing, online, and restore phase. The
online phase runs necessary full order model (FOM) to generate simulation data.
libROM dynamically collects the data as the FOM simulation marches in time
domain. In the hyper-reduction preprocessing phase, the libROM builds a library
of reduced basis as well as hyper-reduction operators. The online phase runs the
ROM and the restore phase projects the ROM solutions to the full order model
dimension.  

<!-- <a href="https://glvis.org/live/?stream=../data/laghos.saved" target="_blank"> -->
<img class="floatright" src="../img/examples/sedov.gif" width="300"  >
<!-- </a> -->

###Sedov blast problem
**Sedov blast** problem is a three-dimensional standard shock hydrodynamic
benchmark test. An initial delta source of internal energy deposited at the
origin of a three-dimensional cube is considered. The computational domain is
the unit cube $\tilde{\Omega} = \[0,1\]^3$ with wall boundary conditions on all
surfaces, i.e., $v\cdot n = 0$. The initial velocity is given by $v=0$. The
initial density is given by $\rho = 1$. The initial energy is given by a delta
function at the origin. The adiabatic index in the ideal gas equations of state
is set $\gamma = 1.4$. The initial mesh is a uniform Catesian hexahedral mesh,
which deforms over time. It can be seen that the radial symmetry is maintained
in the shock wave propagation in both FOM and ROM simulations. One can reproduce
the numerical result, following the command line options described below:

* **offline**: ./laghos -o twp_sedov -m ../data/cube01_hex.mesh -pt 211 -tf 0.8 -s 7 -pa -offline -visit -romsvds -ef 0.9999 -writesol -romos -rostype load -romsns -nwinsamp 21 -sample-stages
* **hyper-reduction preprocessing**: ./laghos -o twp_sedov -m ../data/cube01_hex.mesh -pt 211 -tf 0.8 -s 7 -pa -online -romsvds -romos -rostype load -romhrprep -romsns -romgs -nwin 66 -sfacv 2 -sface 2
* **online**: ./laghos -o twp_sedov -m ../data/cube01_hex.mesh -pt 211 -tf 0.8 -s 7 -pa -online -romsvds -romos -rostype load -romhr -romsns -romgs -nwin 66 -sfacv 2 -sface 2
* **restore**: ./laghos -o twp_sedov -m ../data/cube01_hex.mesh -pt 211 -tf 0.8 -s 7 -pa -restore -soldiff -romsvds -romos -rostype load -romsns -romgs -nwin 66

   |    | FOM solution time | ROM solution time | Speed-up | Velocity relative error |
   | -- | ----------------- | ----------------- | -------- | ----------------------- |
   |    |  191 sec          |  8.3 sec          |   22.8   |         2.2e-4          |

<img class="floatright" src="../img/examples/gresho.png" width="250"  >

### Gresho vortex problem
**Gresho vortex** problem is a two-dimensional benchmark test for the
incompressible inviscid Navier-Stokes equations. The computational domain is
the unit square $\tilde\Omega = [-0.5,0.5]^2$ with wall boundary conditions on
all surfaces, i.e., $v\dot n = 0$. Let $(r,\phi)$ denote the polar coordinates
of a particle $\tilde{x} \in \tilde{\Omega}$. The initial angular velocity is
given by 

$$v_\phi =  
  \cases{
  \displaystyle 5r   & for 0 $\leq$ r < 0.2 \cr
  \displaystyle 2-5r & for 0.2 $\leq$ r < 0.4 \cr
  \displaystyle 0 i  & for r $\geq$ 0.4.                                             
  }$$

The initial density if given by $\rho=1$. The initial thermodynamic pressure is
given by 

$$p = \cases{
5 + \frac{25}{2} r^2                             & for 0 $\leq$ r < 0.2 \cr
9 - 4 \log(0.2) + \frac{25}{2} - 20r + 4 \log(r) & for 0.2 $\leq$ r < 0.4 \cr
3 + 4\log(2)                                     & for r $\geq$ 0.4 }$$

* **offline**: ./laghos -o twp_gresho -p 4 -m ../data/square_gresho.mesh -rs 4
  -ok 3 -ot 2 -tf 0.62 -s 7 -visit -writesol -offline -ef 0.9999 -romsvds -romos
  -rostype load -romsns -nwinsamp 21 -sample-stages 
* **hyper-reduction preprocessing**: ./laghos -o twp_gresho -p 4 -m
  ../data/square_gresho.mesh -rs 4 -ok 3 -ot 2 -tf 0.62 -s 7 -online -romhrprep
  -romsvds -romos -rostype load -romsns -romgs -nwin 152 -sfacv 2 -sface 2
* **online**: ./laghos -o twp_gresho -p 4 -m ../data/square_gresho.mesh -rs 4
  -ok 3 -ot 2 -tf 0.62 -s 7 -online -romhr -romsvds -romos -rostype load -romsns
  -romgs -nwin 152 -sfacv 2 -sface 2
* **restore**: ./laghos -o twp_gresho -p 4 -m ../data/square_gresho.mesh -rs 4
  -ok 3 -ot 2 -tf 0.62 -s 7 -soldiff -restore -romsvds -romos -rostype load
  -romsns -romgs -nwin 152

   |    | FOM solution time | ROM solution time | Speed-up | Velocity relative error |
   | -- | ----------------- | ----------------- | -------- | ----------------------- |
   |    |  218 sec          |   8.4 sec         |   25.9   |      2.1e-4             |

<img class="floatright" src="../img/examples/taylorGreen.png" width="250"  >

### Taylor-Green vortex
**Taylor-Green vortex** problem is a three-dimensional benchmark test for the
incompressible Navier-Stokes equasions. A manufactured smooth solution is
considered by extending the steady state Taylor-Green vortex solution to the
compressible Euler equations. The computational domain is the unit cube
$\tilde{\Omega}=\[0,1\]^3$ with wall boundary conditions on all surfaces,
i.e., $v\cdot n = 0$. The initial velocity is given by

$$ v = (\sin{(\pi x)} \cos{(\pi y)} \cos{(\pi z)}, -\cos{(\pi x)}\sin{(\pi y)}\cos{(\pi z)}, 0)  $$

The initial density is given by $\rho =1$. The initial thermodynamic pressure
is given by

$$ p = 100 + \frac{(\cos{(2\pi x)} + \cos{(2\pi y))(\cos{(2\pi z)+2})-2}}{16} $$

The initial energy is related to the pressure and the density by the equation
of state for the ideal gas, $p=(\gamma-1)\rho e$, with $\gamma = 5/3$. The
initial mesh is a uniform Cartesian hexahedral mesh, which deforms over time.
The visualized solution is given on the right.  One can reproduce the
numerical result, following the command line options described below:

* **offline**: ./laghos -o twp_taylor -m ../data/cube01_hex.mesh -p 0 -rs 2 -cfl
  0.1 -tf 0.25 -s 7 -pa -offline -visit -romsvds -ef 0.9999 -writesol -romos
  -rostype load -romsns -nwinsamp 21 -sdim 1000 -sample-stages 
* **hyper-reduction preprocessing**: ./laghos -o twp_taylor -m
  ../data/cube01_hex.mesh -p 0 -rs 2 -cfl 0.1 -tf 0.25 -s 7 -pa -online -romsvds
  -romos -rostype load -romhrprep -romsns -romgs -nwin 82 -sfacv 2 -sface 2
* **online**: ./laghos -o twp_taylor -m ../data/cube01_hex.mesh -p 0 -rs 2 -cfl
  0.1 -tf 0.25 -s 7 -pa -online -romsvds -romos -rostype load -romhr -romsns
  -romgs -nwin 82 -sfacv 2 -sface 2
* **restore**: ./laghos -o twp_taylor -m ../data/cube01_hex.mesh -p 0 -rs 2 -cfl
  0.1 -tf 0.25 -s 7 -pa -restore -soldiff -romsvds -romos -rostype load -romsns
  -romgs -nwin 82

   |    | FOM solution time | ROM solution time | Speed-up | Velocity relative error |
   | -- | ----------------- | ----------------- | -------- | ----------------------- |
   |    |  170 sec          |   5.4 sec         |   31.2   |      1.1e-6             |


<img class="floatright" src="../img/examples/triple.png" width="280"  >

### Triple-point problem
**Triple-point** problem is a three-dimensional shock test with two materials in
three states. The computational domain is $\tilde{\Omega} = \[0,7\] \times \[0,3
\] \times \[0,1.5\]$ with wall boundary conditions on all surfaces, i.e.,
$v\cdot n = 0$. The initial velocity is given by $v=0$. The initial density is
given by

$$\rho =  
  \cases{
  \displaystyle 1   & for x $\leq$ 1 or y $\leq$ 1.5, \cr
  \displaystyle 1/8 & for x $>$ 1 and y $>$ 1.5 
  }$$

The initial thermodynamic pressure is given for

$$p =  
  \cases{
  \displaystyle 1   & for x $\leq$ 1, \cr
  \displaystyle 0.1 & for x $>$ 1
  }$$

The initial energy is related to the pressure and the density by the equation
of state for the ideal gas, $p=(\gamma-1)\rho e$, with 

$$\gamma =  
  \cases{
  \displaystyle 1.5   & for x $\leq$ 1 or y $>$ 1.5\cr
  \displaystyle 1.4   & for x $>$ 1 and y $\leq$ 1.5
  }$$

The initial mesh is a uniform Cartesian hexahedral mesh, which deforms over
time.  The visualized solution is given on the right.  One can reproduce the
numerical result, following the command line options described below:

* **offline**: ./laghos -o twp_triple -p 3 -m ../data/box01_hex.mesh -rs 2 -tf
  0.8 -s 7 -cfl 0.5 -pa -offline -writesol -visit -romsvds -romos -rostype load
  -romsns -nwinsamp 21 -ef 0.9999 -sdim 200 -sample-stages 
* **hyper-reduction preprocessing**: ./laghos  -o twp_triple -p 3 -m
  ../data/box01_hex.mesh -rs 2 -tf 0.8 -s 7 -cfl 0.5 -pa -online -romhrprep
  -romsvds -romos -rostype load -romgs -romsns -nwin 18 -sfacv 2 -sface 2
* **online**: ./laghos -o twp_triple -p 3 -m ../data/box01_hex.mesh -rs 2 -tf
  0.8 -s 7 -cfl 0.5 -pa -online -romhr -romsvds -romos -rostype load -romgs
  -romsns -nwin 18 -sfacv 2 -sface 2
* **restore**: ./laghos  -o twp_triple -p 3 -m ../data/box01_hex.mesh -rs 2 -tf
  0.8 -s 7 -cfl 0.5 -pa -restore -soldiff -romsvds -romos -rostype load -romgs
  -romsns -nwin 18 
 
   |    | FOM solution time | ROM solution time | Speed-up | Velocity relative error |
   | -- | ----------------- | ----------------- | -------- | ----------------------- |
   |    |  122 sec          |  1.4  sec         |   87.8   |     8.1e-4              |


<img class="floatright" src="../img/examples/rt-2x1-q12.gif" width="60"  >

### Rayleigh-Taylor instability problem 
**Rayleigh-Taylor instability** problem

* **offline**: ./laghos -p 7 -m ../data/rt2D.mesh -tf 1.5 -rs 4 -ok 2 -ot 1 -pa
  -o twp_rt -s 7 -writesol -offline -romsns -sdim 200000 -romsvds -romos -romgs
  -nwinsamp 21 -ef 0.9999999999 -sample-stages
* **hyper-reduction preprocessing**: ./laghos -p 7 -m ../data/rt2D.mesh -tf 1.5
  -rs 4 -ok 2 -ot 1 -pa -o twp_rt -s 7 -online -romsns -romos -romgs -nwin 187
  -sfacv 2 -sface 2 -romhrprep
* **online**: ./laghos -p 7 -m ../data/rt2D.mesh -tf 1.5 -rs 4 -ok 2 -ot 1 -pa
  -o twp_rt -s 7 -online -romsns -romos -romgs -nwin 187 -sfacv 2 -sface 2
  -romhr
* **restore**: ./laghos -p 7 -m ../data/rt2D.mesh -tf 1.5 -rs 4 -ok 2 -ot 1 -pa
  -o twp_rt -s 7 -restore -romsns -romos -romgs -soldiff -nwin 187

   |    | FOM solution time | ROM solution time | Speed-up | Velocity relative error |
   | -- | ----------------- | ----------------- | -------- | ----------------------- |
   |    |  127 sec          |  8.7  sec         |   14.6   |     7.8e-3              |

_This is an external miniapp, available at
[https://github.com/CEED/Laghos/tree/rom](https://github.com/CEED/Laghos/tree/rom)._
<div style="clear:both;"/></div>
<br></div>

<!-- ------------------------------------------------------------------------- -->

<div id="nomatch">
<br/><br/><br/>
<center>
No examples or miniapps match your criteria.
</center>
<br/><br/><br/>
<hr>
</div>

<div style="clear:both;"/></div>
<script type="text/javascript"><!--

function showElement(id, show)
{
    //document.getElementById(id).style.display = show ? "block" : "none";

    // workaround because Doxygen splits and duplicates the divs for some reason
    var divs = document.getElementsByTagName("div");
    for (i = 0; i < divs.length; i++)
    {
       if (divs.item(i).id == id) {
          divs.item(i).style.display = show ? "block" : "none";
       }
    }
    return show ? 1 : 0;
}

function getBooleans(comboId)
{
   combo = document.getElementById(comboId);

   first_selected = false;
   for (i = 0; i < combo.options.length; i++)
   {
      opt = combo.options[i];
      selected = opt.selected || first_selected;
      if (!i) { first_selected = selected; }

      // create a boolean variable named after the option
      this[opt.id] = selected;
   }
}

function update()
{
   getBooleans("group1");
   getBooleans("group2");
   getBooleans("group3");
   getBooleans("group4");

   numShown = 0 // expression continued...

   // example codes
   + showElement("poisson",  (diffusion) && h1 && (galerkin || nurbs || staticcond || pa) && (gs || pcg || umfpack || amg || petsc))

   // external miniapps
   + showElement("laghos", (compressibleflow) && (l2 || h1) && (galerkin || dg || pa) && (rk))

   ; // ...end of expression

   // show/hide the message "No examples match your criteria"
   showElement("nomatch", numShown == 0);
}

function initCombos()
{
   var query = location.search.substr(1);
   query.split("&").forEach(function(id)
   {
      if (id) {
         opt = document.getElementById(id);
         if (opt) { opt.selected = true; }
      }
   });
}

// make sure "no match" div is not visible after page is loaded
window.onload = update;

// force vertical scrollbar
document.getElementsByTagName("body")[0].style = "overflow-y: scroll"

// parse URL part after '?', e.g., http://.../index.html?elasticity&nurbs
initCombos();

//--></script>
