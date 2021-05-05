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
      <option id="dg">Discontinuous Galerkin (DG)</option>
      <option id="pa">Partial assembly</option>
   </select>
</div>
<div class="col-sm-6 col-md-4 small" markdown="1">
   <h5>**Solver**</h5>
   <select id="group4" onchange="update()">
      <option id="all4">All</option>
      <option id="rk">Explicit Runge-Kutta (ODE integration)</option>
   </select>
</div>
</div>
<br>
<hr>

<!-- ------------------------------------------------------------------------- -->

<div id="laghos" markdown="1">
##Laghos ROM Miniapp

**Laghos** (LAGrangian High-Order Solver) is a miniapp that solves the
time-dependent Euler equations of compressible gas dynamics in a moving
Lagrangian frame using unstructured high-order finite element spatial
discretization and explicit high-order time-stepping. **LaghosROM** introduces
reduced order models of Laghos simulations. 

A list of example problems that you can solve with LaghosROM includes Sedov
blast, Gresho vortex, Taylor--Green vortex, triple-point, and Rayleigh--Taylor
instability problems. Below are command line options for each problems and some
numerical results. For each problem, four different phases need to be taken,
i.e., the offline, hyper-reduction preprocessing, online, and restore phase. 

<!-- <a href="https://glvis.org/live/?stream=../data/laghos.saved" target="_blank"> -->
<img class="floatright" src="../img/examples/sedov.gif" width="300"  >
<!-- </a> -->

* **Sedov blast** problem is a three-dimensional standard shock hydrodynamic
  benchmark test. An initial delta source of internal energy deposited at the
  origin of a three-dimensional cube is considered. 
    * **offline**: ./laghos -p 1 -m data/cube01_hex.mesh -pt 211 -tf 0.8 -o tw_sedov -offline -writesol -nwinsamp 10 -romsns -rostype load -ef 0.9999 -visit -k fom 
    * **hyper-reduction preprocessing**: ./laghos -p 1 -m data/cube01_hex.mesh -pt 211 -tf 0.8 -o tw_sedov -online -romhrprep -nwin 71 -romsns -rostype load -sfacv 177 -sface 49
    * **online**: ./laghos -p 1 -m data/cube01_hex.mesh -pt 211 -tf 0.8 -o tw_sedov -online -romhr -nwin 71 -romsns -rostype load -sfacv 177 -sface 49
    * **restore**: ./laghos -p 1 -m data/cube01_hex.mesh -pt 211 -tf 0.8 -o tw_sedov -restore -soldiff -nwin 71 -romsns -rostype load -visit -k rom

   |    | FOM solution time | ROM solution time | Speed-up | Position relative error |
   | -- | ----------------- | ----------------- | -------- | ----------------------- |
   |    |  382 sec          |  77 sec           |   5.0    |           0.01          |


* **Gresho vortex** problem is a two-dimensional benchmark test for the
  incompressible inviscid Navier--Stokes equations. The computational domain is
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

  The initial density if given by $\rho=1$. The initial thermodynamic pressure
  is given by 

  $$p = \cases{
  5 + \frac{25}{2} r^2                             & for 0 $\leq$ r < 0.2 \cr
  9 - 4 \log(0.2) + \frac{25}{2} - 20r + 4 \log(r) & for 0.2 $\leq$ r < 0.4 \cr
  3 + 4\log(2)                                     & for r $\geq$ 0.4.}$$

    * **basic**: ./laghos -p 4 -m data/square_gresho.mesh -rs 4 -ok 3 -ot 2 -tf 0.62 -s 7 
* **Taylor--Green vortex** problem is a three-dimensional benchmark test for the
  incompressible Navier--Stokes equasions. 
    * **basic**: ./laghos -p 0 -m data/cube01_hex.mesh -cfl 0.1 -tf 0.25 
* **Triple-point** problem
    * **basic**: ./laghos -p 3 -m data/box01_hex.mesh -tf 0.8 
  

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
