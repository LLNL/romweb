# Projection-based Reduced Order Model 

The reduced order models are achieved by applying data-driven model order
reduction techniques to high-fidelity physics models, typically represented by
partial differential equations (PDEs).

There is a large body of literature on reduced order models, including the
following excellent books:

- [Certified reduced basis methods for parametrized partial differential equations](https://link.springer.com/content/pdf/10.1007/978-3-319-22470-1.pdf) by *Jan S. Hesthaven* and *Gianluigi Rozza* and *Benjamin Stamm*
- [Model reduction of parametrized systems](https://www.springer.com/gp/book/9783319587851) by *Peter Benner* and *Mario Ohlberger* and *Anthony T. Patera* and *Gianluigi Rozza* and *Karsten Urban*
- [Reduced-order modeling (ROM) for simulation and optimization](https://www.springer.com/gp/book/9783319753188) by *Winfried Keiper* and *Anja Milde* and *Stefan Volkwein*
- [Approximation of large-scale dynamical systems](https://epubs.siam.org/doi/book/10.1137/1.9780898718713?mobileUi=0) by *Athanasios C. Antoulas*
- [Machine learning, low-rank approximations and reduced order modeling in computational mechanics](https://www.amazon.com/Learning-Low-Rank-Approximations-Computational-Mechanics/dp/3039214098) by *Felix Fritzen* and *David Ryckelynck*
- [Machine learning for model order reduction](https://www.amazon.com/Machine-Learning-Model-Order-Reduction/dp/331975713X) by *Khaled Salah Mohamed*
- [Reduced order methods for modeling and computational reduction](https://www.springer.com/gp/book/9783319020891) by *Alfio Quarteroni* and *Gianluigi Rozza*

The successful reduced order model development depends on many factors:

- Good quality and quantity of data
- Optimal and scalable data reduction schemes
- Optimal projection methods
- Efficient hyper-reduction for nonlinear reduction
- Sampling algorithms

The libROM is designed to provide useful and scalable 


identify the low-rank approximation 

be lightweight, general and
highly scalable reduced order model toolkit that provides the building blocks
for developing finite element algorithms in a manner similar to that of MATLAB
  for linear algebra methods.

The success measure for a reduced order model:

- speed-up 
- accuracy
- differentiability
- verifiability
- predictability


Some of the C++ classes for the finite element realizations of these
PDE-level concepts in libROM are described below.

