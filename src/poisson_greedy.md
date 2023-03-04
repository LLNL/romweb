<script type="text/x-mathjax-config">
  MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$']]}});
</script>
<script type="text/javascript"
  src="//cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

# Greedy for Poisson equation

The main code for this tutorial can be found at
[poisson_local_rom_greedy.cpp](https://github.com/LLNL/libROM/blob/master/examples/prom/poisson_local_rom_greedy.cpp),
which demonstrates how to use libROM to execute greedy procedure for the ROM of
the Poisson problem introduced in the [Poisson equation tutorial](poisson.md).
For the recap, the general procedure of the greedy algorithm follows:

  1. Define a parameter space 
  2. Pick an initial point in the parameter space to build a ROM there (a good
     cancidiate initla point is either the centroid or one of end points)
  3. Evaluate *error indicator* of the current ROM (either global or local ROM)
     at $N$ random points within the parameter space
  4. Check if the maximum error indicator value is less than the desirable
     accuracy threshold
  5. If the answer to Step 4 is yes, then *terminate* the greedy process.
  6. If the answer to Step 4 is no, then collect the full order model
     simulation data at the maximum error indicator point and add them to
     update the ROM
  7. Go to Step 3. 

As in the [Poisson equation tutorial](poisson.md), we choose to vary the
frequency $\kappa$ as parameter. First, we define the parameter space to be
from $0.5$ to $3$, which is larger than the one used in [Poisson equation
tutorial](poisson.md). You can try the following command line options to run
the greedy procedure:

```sh
./poisson_local_rom_greedy -build_database -greedy-param-min 0.5 -greedy-param-max 3 -greedy-param-size 40 -greedysubsize 10 -greedyconvsize 20 -greedyrelerrortol 0.01
```

The lower and upper bounds of the parameter are determined by the options,
*-greedy-param-min* and *-greedy-param-max*, respectively. The option
*-greedy-param-size* specifies the total number of random sample points within
the parameter space for the whole greedy procedure.  The option
*-greedysubsize* sets the number of sub-sample points, where the error
indicator is evaluated at every greedy iterations.  The option
*-greedyconvsize* sets the number of convergence-sample points on which the
error indicator is checked and the termination of the greedy algorithm is
determined if the error indicators are below the convergence threshold after
the error indicator tests on the sub-sample points have been passed.  Finally,
*-greedyrelerrortol* sets the desirable relative error for the greedy algorithm
to achieve.

The core class of the libROM for the greedy procedure is [
GreedySampler](https://librom.readthedocs.io/en/latest/class_c_a_r_o_m_1_1_greedy_sampler.html),
which is defined on Line 126 of [poisson_local_rom_greedy.cpp](https://github.com/LLNL/libROM/blob/master/examples/prom/poisson_local_rom_greedy.cpp)
The GreedySampler generates sampling points within a given
parameter space. 
The class has two sub-classes, i.e.,
[GreedyCustomSampler](https://librom.readthedocs.io/en/latest/class_c_a_r_o_m_1_1_greedy_custom_sampler.html)
and
[GreedyRandomSampler](https://librom.readthedocs.io/en/latest/class_c_a_r_o_m_1_1_greedy_random_sampler.html).
The GreedyCustomSampler generates *pre-defined* sampling
points, e.g., a tensor product sampling points, while the
GreedyRandomSampler generates *random* sampling points, e.g.,
Latin hyper-cube sampling points. The GreedySampler also does
book-keeping job of at which sampling point to evaluate the error indicator,
when to move onto the next greedy step, and which sampling point has the
maximum error indicator value. 

Just to be clear, the libROM does not do everything for you.  For example, the
error indicator must be defined in the physics solver. For the Poisson example,
the residual-based error indicator is defined at Lines
529-535 of [poisson_loca_rom_greedy.cpp](https://github.com/LLNL/libROM/blob/master/examples/prom/poisson_local_rom_greedy.cpp). 

Once the greedy procedure completes, the log file, called
*poisson_greedy_algorithm_log.txt*, is generated to show the progress of the
greedy procedure and the final parameter points on which the global ROM was
built. For example, you will see the following block at the end of the file,
indicating the final parameter points on which the *global* ROM is built.

```sh
Sampled Parameter Points
[ 0.591166 ]
[ 0.844964 ]
[ 1.066678 ]
[ 1.353370 ]
[ 1.710334 ]
[ 1.992794 ]
[ 2.568171 ]
[ 2.985638 ]
```

Because we set the *-greedyrelerrortol* to be 0.01, the *global* ROM built
through the greedy procedure must be able to predict a solution with a relative
error less than 1$\%$ for any points in the parameter space. Indeed, let's try
to predict the solution at $\kappa = 2.2$, which was not one of the final
parameter points. Let's first generate the full order model solution with the
following command line option:

```sh
./poisson_local_rom_greedy -offline -f 2.2
```

This full order model solution will be used to compute the relative error for
the ROM solution. The ROM solution can be obtained by the following command
line option:

```sh
./poisson_local_rom_greedy -use_database -online -f 2.2
```

Indeed, the relative error of 0.00167671 is achieved 


