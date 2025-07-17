<div class="col-md-6" markdown="1">

[![libROM logo](img/logo-libROM2.png)](gallery.md)

libROM is a _free_, _lightweight_, _scalable_ C++ library for data-driven
physical simulation methods.  It is the main tool box that the reduced order
modeling team at LLNL uses to develop efficient **model order reduction**
techniques and **physics-constrained data-driven methods**. We try to collect
any useful reduced order model routines, which are separable to the
high-fidelity physics solvers, into libROM. Plus, libROM is open source, so
anyone is welcome to suggest new ideas or contribute to the development. Let's
work together for better data-driven technology!

## Features

* [Proper Orthogonal Decomposition](features.md#proper-orthogonal-decomposition) ([libROM](https://github.com/LLNL/libROM), [pylibROM](https://github.com/LLNL/pylibROM))
* [Dynamic mode decomposition](features.md#dynamic-mode-decomposition) ([libROM](https://github.com/LLNL/libROM), [pylibROM](https://github.com/LLNL/pylibROM))
* [Projection-based reduced order models](features.md#projection-based-reduced-order-model) ([libROM](https://github.com/LLNL/libROM), [pylibROM](https://github.com/LLNL/pylibROM))
* [Hyper-reduction](features.md#hyper-reduction) ([libROM](https://github.com/LLNL/libROM), [pylibROM](https://github.com/LLNL/pylibROM)) 
* [Greedy algorithm](features.md#greedy-sampling-algorithm) ([libROM](https://github.com/LLNL/libROM), [pylibROM](https://github.com/LLNL/pylibROM)) 
* [Latent space dynamics identification](features.md#latent-space-dynamics-identification) ([LaSDI](https://github.com/LLNL/LaSDI), [gLaSDI](https://github.com/LLNL/gLaSDI), [GPLaSDI](https://github.com/LLNL/gpLaSDI))
* [Domain decomposition nonlinear manifold reduced order model](features.md#domain-decomposition-nonlinear-manifold-reduced-order-model) ([DD-NM-ROM](https://github.com/LLNL/DD-NM-ROM))

Many more features will be available soon. Stay tuned!

libROM is used in many projects, including
[BLAST](http://www.llnl.gov/casc/blast),
[ARDRA](https://computing.llnl.gov/projects/ardra-scaling-up-sweep-transport-algorithms),
[Laghos](https://github.com/CEED/Laghos/tree/rom), 
[SU2](https://su2code.github.io/),
[ALE3D](https://wci.llnl.gov/simulation/computer-codes/ale3d)
and [HyPar](http://hypar.github.io/a00126.html). Many [MFEM](https://mfem.org)-based ROM
examples can be found in [Examples](examples.md).

See also our [Gallery](gallery.md), [Publications](publications.md) and
[News](news.md) pages.

</div><div class="col-md-6 news-table" markdown="1">


## Recent News

Date         | Message
------------ | -----------------------------------------------------------------
July 14, 2025| [LaSDI-IT](https://arxiv.org/pdf/2507.10647) arXiv paper is available
July 2, 2025 | [Podcast on defining foundation model](https://hodgesj.substack.com/p/podcast-defining-foundation-models) is available 
June 24-27, 2025 | [Kevin Chung](https://scholar.google.com/citations?user=K7KuqccAAAAJ&hl=en) presented LaSDI-IT at [54th International Annual Conference of the Fraunhofer ICT](file:///Users/choi15/Downloads/Jahrestagung_CallforPapers_2025-2.pdf)
June 19, 2025 | [Youngsoo Choi](https://people.llnl.gov/choi15) presented DD-FEM at [Large-Scale Scientific Computations Conference](https://parallel.bas.bg/Conferences/SciCom25/)
June 10-12, 2025 | [Youngsoo Choi](https://people.llnl.gov/choi15) led a breakout session at [DOE ASCR Workshop on Inverse Methods for Complex Systems under Uncertainty](https://web.cvent.com/event/0fc81644-f4d8-416b-84d3-be802f613f7a/summary)
June 10, 2025 | [Parametric tLaSDI](https://arxiv.org/pdf/2506.08475?) arXiv paper is available 
June 10, 2025 | [mLaSDI](https://arxiv.org/pdf/2506.09207?) arXiv paper is available 
May 30, 2025 | [Defining Foundation Model](https://arxiv.org/pdf/2505.22904?) arXiv paper is available 

## libROM tutorials in YouTube
Date         | Title
------------ | -----------------------------------------------------------------
July 22, 2021| [Poisson equation & its finite element discretization](https://youtu.be/YaZPtlbGay4)
Sep. 1, 2021| [Poisson equation & its reduced order model](https://youtu.be/YlFrBP31riA)
Sep. 23, 2021| [Physics-informed sampling procedure for reduced order models](https://youtu.be/A5JlIXRHxrI)
Sep. 11, 2022| [Local reduced order models and interpolation-based parameterization](https://youtu.be/KLyWZQRZ4hU)
Sep. 23, 2022| [Projection-based reduced order model for nonlinear system](https://youtu.be/EfoeOltd9Fo)
Aug. 23, 2023| [Complete derivation of dynamic mode decomposition](https://youtu.be/YmxFkQAHSLM?si=03kdOe99j00IdUuM)

## Latest Release

[Examples](examples.md)
┊ [Code documentation](https://librom.readthedocs.io/en/latest/index.html)
┊ [libROM Sources](https://github.com/LLNL/libROM)
┊ [pylibROM Sources](https://github.com/LLNL/pylibROM)
┊ [LaghosROM Sources](https://github.com/CEED/Laghos/tree/rom/rom)
┊ [ScaleupROM](https://github.com/LLNL/scaleupROM)
┊ [LaSDI Sources](https://github.com/LLNL/LaSDI)
┊ [gLaSDI Sources](https://github.com/LLNL/gLaSDI)
┊ [GPLaSDI Sources](https://github.com/LLNL/GPLaSDI)
┊ [DD-NM-ROM Sources](https://github.com/LLNL/DD-NM-ROM)
┊ [NM-ROM Sources](https://github.com/LLNL/NM-ROM)
┊ [WLaSDI](https://github.com/MathBioCU/WLaSDI)
┊ [tLaSDI](https://github.com/pjss1223/tLaSDI)
┊ [gappyAE](https://github.com/youngkyu-kim/GappyAE)

[<button type="button" class="btn btn-success">
**Download libROM-master.zip**
</button>](https://github.com/LLNL/libROM/archive/refs/heads/master.zip)

<!---
[Older releases](download.md) ┊ [Python wrapper](https://github.com/mfem/PylibROM)
-->

## Documentation

[Building libROM](building.md)
┊ [Poisson equation](poisson.md)
┊ [Greedy for Poisson](poisson_greedy.md)

New users should start by examining the [example codes](examples.md) and
[tutorials](poisson.md).

We also recommend using [GLVis](http://glvis.org) or
[VisIt](https://visit-dav.github.io/visit-website/) for visualization.


## Contact

Use the GitHub [issue tracker](https://github.com/LLNL/libROM/issues)
to report [bugs](https://github.com/LLNL/libROM/issues/new?labels=bug)
or post [questions](https://github.com/LLNL/libROM/issues/new?labels=question)
or [comments](https://github.com/LLNL/libROM/issues/new?labels=comments).
See the [About](about.md) page for citation information.


</div>

<div class="col-md-12"></div>
