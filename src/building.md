# Building libROM

A simple tutorial on how to build and run libROM. For more details, see the
[README](https://github.com/LLNL/libROM/blob/master/README.md) file.

In addition to the native build system described below, libROM packages are
also available in Spack:

- [Spack](https://github.com/spack/spack)


## Instructions

Clone libROM  

- [https://github.com/LLNL/libROM](https://github.com/LLNL/libROM)


## Installation

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
