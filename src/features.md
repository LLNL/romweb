# Features

The goal of libROM is is to provide high-performance scalable library for
data-driven physical simulation modeling, such as surrogate and reduced order
models.

## Efficient data collection

High-fidelity physical simulations generate intensive data in its size, which
makes the data collection daunting. The libROM can be integrated in the physics
solver and the data is extracted dynamically as the physics solver is running.
For example the following line can be inserted in the time loop of the physics
solver where the solution is computed:

## Proper orthogonal decomposition

The proper othogonal decomposition (POD) is a popular way of compressing
physical simulation data and obtain an optimal "reduced" bases. The POD modes
can be obtained by two equivalent ways: (i) eigenvalue decomposition and (ii)
singular value decomposition (SVD). We take the latter approach.  The POD can be
applied to both spatial and temporal data whose procedure is schematically
depicted in the figure below:

<img src="../img/svd.png" align="right" alt="H(curl) and H(div) spaces">

We introduce three different ways of SVDs:

- Static SVD
- incremental SVD
- randomized SVD
- space--time SVD

### Static SVD

### Incremental SVD

### Randomized SVD

## Greedy algorithm

Greedy algorithm is a major approach to build a 

## Hyper-reduction

Hyper-reduction is essential to reduced the complexity caused of nonlinear terms
in physical simulations.

## Extensive Examples

MFEM includes a number of well-documented [example codes](examples.md) that can
be used as tutorials, as well as simple starting points for user applications.
Some of the included example codes are:

 - [Example 1](http://mfem.github.io/doxygen/html/examples_2ex1_8cpp_source.html): nodal H1 FEM for the Laplace problem,
 - [Example 2](http://mfem.github.io/doxygen/html/ex2_8cpp_source.html): vector FEM for linear elasticity,
 - [Laghos](https://github.com/CEED/Laghos): high-order Lagrangian hydrodynamics miniapp,
 - [Remhos](https://github.com/CEED/Remhos): high-order advection remap miniapp,
 - [Mulard](https://computation.llnl.gov/projects/co-design/mulard): multigroup thermal radiation diffusion mini application.

## Open Source

libROM is an open-source software, and can be freely used under the terms of the
[MIT](https://github.com/LLNL/libROM/blob/master/LICENSEi-MIT) and
[APACHE](https://github.com/LLNL/libROM/blob/master/LICENSE-APACHE) license.

<!-- To update the SVG images: in the gh-pages branch of mfem/doxygen do:
     grep 'id="node1" href="$classmfem_1_1FiniteElementCollection.html"' html/inherit*map -->

[FiniteElement]:           http://mfem.github.io/doxygen/html/inherit_graph_389.svg
[FiniteElementCollection]: http://mfem.github.io/doxygen/html/inherit_graph_119.svg
[Element]:                 http://mfem.github.io/doxygen/html/inherit_graph_94.svg
[HyperelasticModel]:       http://mfem.github.io/doxygen/html/inherit_graph_175.svg
[NonlinearFormIntegrator]: http://mfem.github.io/doxygen/html/inherit_graph_296.svg
[LinearFormIntegrator]:    http://mfem.github.io/doxygen/html/inherit_graph_203.svg
[Operator]:                http://mfem.github.io/doxygen/html/inherit_graph_361.svg
[Vector]:                  http://mfem.github.io/doxygen/html/inherit_graph_437.svg

[BlockMatrix]:             http://mfem.github.io/doxygen/html/classmfem_1_1BlockMatrix.html
[ElementTransformation]:   http://mfem.github.io/doxygen/html/classmfem_1_1ElementTransformation.html
[HypreParMatrix]:          http://mfem.github.io/doxygen/html/classmfem_1_1HypreParMatrix.html
[HypreSmoother]:           http://mfem.github.io/doxygen/html/classmfem_1_1HypreSmoother.html
[IterativeSolver]:         http://mfem.github.io/doxygen/html/classmfem_1_1IterativeSolver.html
[ODESolver]:               http://mfem.github.io/doxygen/html/classmfem_1_1ODESolver.html
[SLBQPOptimizer]:          http://mfem.github.io/doxygen/html/classmfem_1_1SLBQPOptimizer.html
[SparseMatrix]:            http://mfem.github.io/doxygen/html/classmfem_1_1SparseMatrix.html
[SparseSmoother]:          http://mfem.github.io/doxygen/html/classmfem_1_1SparseSmoother.html
