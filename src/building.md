# Building libROM

A simple tutorial on how to build and run libROM. For more details, see the
[README](https://github.com/LLNL/libROM/blob/master/README.md) file.

## Clone libROM 

- [https://github.com/LLNL/libROM](https://github.com/LLNL/libROM)


## General Installation

To compile libROM with default build settings (Mac and LLNL LC Machines):
```sh
 ./scripts/compile.sh
```
To compile libROM for Ardra (LLNL LC Machines only):
```sh
./scripts/ardra_compile.sh
```

To compile libROM using a different toolchain within cmake/toolchains 
(Mac and LLNL LC Machines):
```sh
./scripts/toolchain_compile.sh toolchain.cmake
```
Compilation options:

- -a: Compile a special build for the LLNL codebase: Ardra
- -d: Compile in debug mode.
- -m: Compile with MFEM (required to run the libROM examples)
- -t: Use your own cmake/toolchain
- -u: Update all of libROM's dependencies.

## Using Docker container

Probably the most reliable way is to use docker container. You can find the
instruction on how to use docker container to install libROM in your machine is
described at [Using Docker
container](https://github.com/LLNL/libROM/wiki/Using-Docker-container) wiki
page.


## Compiling on LC Machines

libROM provides several CMake toolchains which can be used to compile on LLNL
LC machines.  For more information on installing and using libROM on specific
LC machines, refer to [the libROM wiki
page](https://github.com/LLNL/libROM/wiki/Compiling-on-LC-Machines).

## Spack

In addition to the build system described above, libROM packages are
also available in Spack:

- [Spack](https://github.com/spack/spack)



