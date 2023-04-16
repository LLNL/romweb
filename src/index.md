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

* [Proper Orthogonal Decomposition](features.md#proper-orthogonal-decomposition)
* [Dynamic mode decomposition](features.md#dynamic-mode-decomposition)
* [Projection-based reduced order models](features.md#projection-based-reduced-order-model)
* [Hyper-reduction](features.md#hyper-reduction)
* [Greedy algorithm](features.md#greedy-sampling-algorithm)

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


## News

Date         | Message
------------ | -----------------------------------------------------------------
June 3, 2023 | [Youngsoo Choi](https://people.llnl.gov/choi15) will present at [SIAM OP23](https://meetings.siam.org/sess/dsp_talk.cfm?p=127228) 
Mar 29, 2023 | [AAAI Spring Symposium](http://cogsys.org/symposium/discovery-2022/) was organized
Mar 10, 2023 | [gLaSDI](https://github.com/LLNL/gLaSDI) open source code is available in gitHub.
Mar 6, 2023 | [LaSDI](https://github.com/LLNL/LaSDI) open source code is available in gitHub.
Feb 15, 2023 | [parametric DMD](https://www.sciencedirect.com/science/article/pii/S0021999122009159) paper is published in JCP.
Oct 17, 2022 | [Rayleigh-Taylor instability ROM](https://doi.org/10.1016/j.jcp.2022.111655) paper is published in JCP.
Oct 1, 2022 | [CWROM stress lattice](https://www.sciencedirect.com/science/article/abs/pii/S0045782522005266) paper is published in CMAME.
Mar 29, 2022 | [S-OPT](https://arxiv.org/pdf/2203.16494.pdf) preprint is available in arXiv.
Nov 19, 2021 | [NM-ROM](https://www.sciencedirect.com/science/article/pii/S0021999121007361) paper is published in JCP.
Nov 10, 2021 | [Laghos ROM](https://www.sciencedirect.com/science/article/pii/S0045782521005739) is published at CMAME. 

## libROM tutorials in YouTube
Date         | Title
------------ | -----------------------------------------------------------------
July 22, 2021| [Poisson equation & its finite element discretization](https://youtu.be/YaZPtlbGay4)
Sep. 1, 2021| [Poisson equation & its reduced order model](https://youtu.be/YlFrBP31riA)
Sep. 23, 2021| [Physics-informed sampling procedure for reduced order models](https://youtu.be/A5JlIXRHxrI)
Sep. 11, 2022| [Local reduced order models and interpolation-based parameterization](https://youtu.be/KLyWZQRZ4hU)
Sep. 23, 2022| [Projection-based reduced order model for nonlinear system](https://youtu.be/EfoeOltd9Fo)

## Latest Release

[Examples](examples.md)
┊ [Code documentation](https://librom.readthedocs.io/en/latest/index.html)
┊ [Sources](https://github.com/LLNL/libROM)

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
