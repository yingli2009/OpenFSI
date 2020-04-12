# OpenFSI Manual

## Table of contents
- [About OpenFSI](#About-OpenFSI)
  - [highlighted features](#Highlighted-features)
  - [code structure](#Code-structure)
- [Compile and Run](#Compile-and-Run)
- Use OpenFSI
  - Prepare input files
  - Application
- Troubleshooting

## About OpenFSI

 OpenFSI is a highly efficient and portable fluid-structure interaction (FSI) simulation package based on immersed-boundary method. The fluid dynamics is accounted by the software [Palabos](http://www.palabos.org/). And the structure solver is implemented within the framework of [LAMMPS](https://lammps.sandia.gov/). In current version, there are 1D, 2D and 3D lattice model and 3D shell model in structure solvers. Using these models, we can model a broad FSI problems including swimming of micro-organisms with tails, flapping of 2D or 3D plate mimicking bird flying and fish swimming and biological flow with large numbers of blood cells.

### Highlighted features

- **Particle based lattice model** The solid is discretized into lattice structure, and the mechanical properties such as stretching and bending are described by series of potential functions that are applied on the lattice nodes.
- **Coupling high-performance software packages** i.e., LAMMPS and Palabos.
- **Highly portable** There are broad applications including 2D and 3D FSI problems.

### Code structure
- `example`: Examples to show how OpenFSI runs 2D and 3D problems
- `src/fix_LB`: Revised `fix_lb` files embedded in LAMMPS for solving fluid dynamics using Latticel Boltzmann method (LBM)
- `src/IB_interface`: Implementation for immersed-boundary method including velocity and force couplings
- `src/lammps_palabos_coupling`: Technique to fulfill the consistant cpu mapping between LAMMPS and Palabos
- `src/main`: Main file to offer user interface to set up properties such as type of flow and boundary conditions
- `src/structure_potential`: Potentials to calculate lattice model and membrane model

## Compile and Run 
 
 Preparation: 
 1. First you should download Palabos source code from http://www.palabos.org/.
 2. Then you also need to download LAMMPS source code from https://lammps.sandia.gov/.
 3. Make sure you have installed the MPI library.
 4. Add the files in `src/structure_potential` into LAMMPS/src directory.

 Compiling:

- Compile the LAMMPS as a library
  
  Inside the directory `lammps/src/MAKE`, there are many options for the makefile. It is possibile to run lammps in serial
  , mpi or intel-optimised version, which depends on the computer architecture used in the simulation.
  For example, if you want to run the simulation in mpi mode, you should first observe that there is a makefile
  named `Makefile.mpi` in `lammps/src/MAKE`, then make it with library mode \
  `cd lammps/src` \
  `make mode=lib mpi` \
  You will find a lammps library named `liblammps_mpi.a` generated.

-   
 2. Modify the Makefile under the eaxmple. 
 - You need to include the LAMMPS library path. 
 - You should make sure the lammps_palabos_coupling and IB_model are in the includePaths.
 - Remeber to include the palabos root directory.
 3. Compile the example.
 
 Run:



