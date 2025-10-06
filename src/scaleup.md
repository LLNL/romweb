<script type="text/x-mathjax-config">
  MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$']]}});
</script>
<script type="text/javascript"
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.2/MathJax.js?config=TeX-AMS_HTML">
</script>

# ScaleupROM

This page provides a list of ScaleupROM example applications. ScaleupROM is a projection-based reduced order model code with discontinuous Galerkin domain decomposition (DG-DD) using libROM and MFEM. It aims to create a robust and efficient large-scale ROM that is trained only from small scale component samples which can be used to solve a variety of physics PDEs. For more information, refer to the [ScaleupROM repo](https://github.com/LLNL/scaleupROM) and [online wiki](https://github.com/LLNL/scaleupROM/wiki).

Select from the categories below to display examples that contain
the respective feature. _All examples support (arbitrarily) high-order meshes
and finite element spaces_.  The numerical results from the example codes can
be visualized using the GLVis or VisIt visualization tools. See the [GLVis
](http://glvis.org) and [VisIt](https://visit-dav.github.io/visit-website/)
websites for more details.

<div class="row" markdown="1">
<div class="col-sm-7 col-md-2 small" markdown="1">
   <h5><b>Application (PDE)</b></h5>
   <select id="group1" onchange="update()">
      <option id="all1">All</option>
      <option id="stokes">Stokes flow</option>
   </select>
</div>
<div class="col-sm-7 col-md-3 small" markdown="1">
   <h5><b>Reduced order model type</b></h5>
   <select id="group2" onchange="update()">
      <option id="all2">All</option>
      <option id="prom">pROM</option>
      <!-- <option id="dmd">DMD</option> -->
   </select>
</div>
<div class="clearfix hidden-md hidden-lg"></div>
<div class="col-sm-7 col-md-3 small" markdown="1">
   <h5><b>Assembly</b></h5>
   <select id="group3" onchange="update()">
      <option id="all3">All</option>
      <option id="dg">Discontinuous Galerkin</option>
   </select>
</div>
<div class="col-sm-7 col-md-4 small" markdown="1">
   <h5><b>Hyper-reduction</b></h5>
   <select id="group4" onchange="update()">
      <option id="all4">All</option>
      <!-- <option id="hr">Hyper-reduction</option> -->
      <option id="no_hr">No hyper-reduction</option>
   </select>
</div>
<div class="col-sm-7 col-md-5 small" markdown="1">
   <h5><b>Physics code</b></h5>
   <select id="group5" onchange="update()">
      <option id="all5">All</option>
      <option id="mfem">MFEM</option>
   </select>
</div>
</div>
<br>
<hr>

<!-- ------------------------------------------------------------------------- -->

<div id="stokes" markdown="1">
## Stokes flow
<a target="_blank">
<img class="floatright" src="../img/examples/scaleuprom_stokes_8x8_rom_vel_mag.png" width="300">
</a>

This example demonstrates the use of ScaleupROM to create a reduced order model for the Stokes flow problem discretized using Taylor-Hood elements. The governing equation for Stokes flow is defined as
$$ - \nu \nabla^2 \mathbf{\tilde{u}} + \nabla \mathit{\widetilde{p}} = 0 $$

$$ \nabla \cdot \mathbf{\tilde{u}} = 0 $$

with boundary conditions

$$ \mathbf{\tilde{u}} = \mathbf{g}_{di} $$

$$ \mathbf{n} \cdot ( - \nu \nabla \mathbf{\tilde{u}} + \mathit{\widetilde{p}} \mathbf{I}) = \mathbf{g}_{ne} $$

where $\mathbf{u}$ and $p$ denote the velocity and pressure field respectively, and $\nu \equiv \frac{\mu}{\mu_0} = 1.1$ is the non-dimensionalized dynamic viscosity with respect to a reference value.

The global-scale system is constructed using a random arrangement from five different reference components: empty, circle, triangle, square, and star. In this example, the fluid flows past an array of these components. Sample snapshots for basis training are generated on 2x2 component domains to better capture downstream flow. A total of 1400 sample snapshots were taken for this example.

On each sample domain, the inflow velocity Dirichlet boundary condition is parameterized as

$$ \mathbf{g}_{di} = (g_1 + \Delta g_1 \sin 2\pi (\mathbf{k}_1 \cdot x + \theta_1),\ g_2 + \Delta g_2 \sin 2\pi (\mathbf{k}_2 \cdot x + \theta_2)) $$

where the parameters are chosen from a uniform random distribution,

$$ g_1, g_2 \sim U[-1, 1] $$

$$ \Delta g_1, \Delta g_2 \sim U[-0.1, 0.1] $$

$$ \mathbf{k}_1, \mathbf{k}_2 \sim U[-0.5, 0.5]^2 $$

$$ \theta_1, \theta_2 \sim U[0, 1] $$

Boundaries at the surface of the object inside the domain have a no-slip wall boundary $g_{di} = 0$ and boundaries on interior interfaces have a homogeneous Neumann boundary $g_{ne} = 0$.

The figure above shows the ROM prediction for $\mathbf{u}$ on a 8x8 system composed of random components with parameter values $g_1 = 1.5, g_2 = -0.8, \Delta g_1 = \Delta g_2 = 0$.

One can follow the command line options below to reproduce the numerical results
summarized in the table below:

**Generate Meshes**:
```
cd build/examples/stokes
mkdir snapshots basis paraview rom-system
./setup_stokes.sh
```

* **Sample Generation**: `../../bin/main -i stokes.sampling.yml`
* **ROM Training**: `../../bin/main -i stokes.sampling.yml -f main/mode=train_rom`
* **ROM Building**: `../../bin/main -i stokes.sampling.yml -f main/mode=build_rom:main/use_rom=true`
* **ROM Prediction**: `../../bin/main -i array.8.yml`

The table below shows the ROM performance for the 8x8 system.

   | FOM Solution time | ROM Solution time | Speed-up | $\mathbf{u}$ relative error | $p$ relative error |
   | ----------------- | ----------------- | -------- | --------------------------- | ------------------ |
   |  0.08298 sec      |  0.00408 sec      |  20.34   |         4.193e-3            |      3.030e-3      |


_The code that generates the numerical results above can be found in
([stokes_flow](https://github.com/LLNL/scaleupROM/tree/main/examples/stokes/))_
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
   getBooleans("group5");

   numShown = 0 // expression continued...

   // example codes
   + showElement("stokes", (stokes) && (prom) && (dg) && (no_hr) && (mfem))
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
