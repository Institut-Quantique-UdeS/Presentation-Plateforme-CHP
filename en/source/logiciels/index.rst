Software
========

When you connect to the IQ HPC Platform, your environment contains only minimal
software. You can add more from a vast selection of `available software
<https://docs.alliancecan.ca/wiki/Available_software/en>`_. Pre-installed and
optimised for HPC, these packages are the same ones that are available on the
national clusters, which guarantees that your jobs can run reproducibly on all
clusters.

Adding software to your environment is mostly done with the ``module`` command.
If you are not familiar with its usage, read `using modules
<https://docs.alliancecan.ca/wiki/Utiliser_des_modules/en>`_ first. Briefly, you
can list loaded modules with ``module list``, search for modules with ``module
spider``, and add them to your environment with ``module load``. For instance:

.. code-block:: console

    [ofisette@ip09 ~]$ module list

    Currently Loaded Modules:
      1) CCconfig             4) imkl/2020.1.217  (math)   7) libfabric/1.10.1
      2) gentoo/2020    (S)   5) intel/2020.1.217 (t)      8) openmpi/4.0.3    (m)
      3) gcccore/.9.3.0 (H)   6) ucx/1.8.0                 9) StdEnv/2020      (S)

      Où :
       S:     Module is Sticky, requires --force to unload or purge
       m:     MPI implementations / Implémentations MPI
       math:  Mathematical libraries / Bibliothèques mathématiques
       t:     Tools for development / Outils de développement
       H:                Hidden Module

    [ofisette@ip09 ~]$ module spider gromacs

    --------------------------------------------------------------------------------------
      gromacs:
    --------------------------------------------------------------------------------------
        Description:
          GROMACS is a versatile package to perform molecular dynamics, i.e. simulate the
          Newtonian equations of motion for systems with hundreds to millions of
          particles. This is a CPU only build, containing both MPI and threadMPI builds. 

         Versions:
            gromacs/2016.6
            gromacs/2020.4
            gromacs/2020.6
            gromacs/2021.2
            gromacs/2021.4
            gromacs/2021.6
            gromacs/2022.2
            gromacs/2022.3
            gromacs/2023
            gromacs/2023.2
            gromacs/2023.3
            gromacs/2024.1
     Other possible modules matches:
            gromacs-colvars  gromacs-cp2k  gromacs-ls  gromacs-plumed  gromacs-ramd
            gromacs-swaxs

    --------------------------------------------------------------------------------------
      To find other possible module matches execute:

          $ module -r spider '.*gromacs.*'

    --------------------------------------------------------------------------------------
    For detailed information about a specific "gromacs" package (including how
    to load the modules) use the module's full name. Note that names that have a
    trailing (E) are extensions provided by other modules. For example:

         $ module spider gromacs/2024.1
    --------------------------------------------------------------------------------------

    [ofisette@ip09 ~]$ module spider gromacs/2023.2

    --------------------------------------------------------------------------------------
      gromacs: gromacs/2023.2
    --------------------------------------------------------------------------------------
        Description:
          GROMACS is a versatile package to perform molecular dynamics, i.e. simulate the
          Newtonian equations of motion for systems with hundreds to millions of
          particles. This is a GPU enabled build, containing both MPI and threadMPI
          builds. 

        Properties:
          Chemistry libraries/apps / Logiciels de chimie

        You will need to load all module(s) on any one of the lines below before
        the "gromacs/2023.2" module is available to load.

          StdEnv/2020  gcc/9.3.0  cuda/11.4  openmpi/4.0.3
          StdEnv/2020  gcc/9.3.0  openmpi/4.0.3
     
        Help:
          Description
          ===========
          GROMACS is a versatile package to perform molecular dynamics, i.e. simulate the
          Newtonian equations of motion for systems with hundreds to millions of
          particles.
          
          More information
          ================
           - Homepage: http://www.gromacs.org

    [ofisette@ip09 ~]$ module load StdEnv/2020 gcc/9.3.0 openmpi/4.0.3

    Lmod is automatically replacing "intel/2020.1.217" with "gcc/9.3.0".


    Due to a MODULEPATH change, the following have been reloaded:
      1) openmpi/4.0.3

    [ofisette@ip09 ~]$ module load gromacs/2023.2
    [ofisette@ip09 ~]$ module list

    Currently Loaded Modules:
      1) CCconfig                 6) gcc/9.3.0        (t)  11) fftw-mpi/3.3.8  (math)
      2) gentoo/2020     (S)      7) ucx/1.8.0             12) scalapack/2.1.0 (math)
      3) imkl/2020.1.217 (math)   8) libfabric/1.10.1      13) gromacs/2023.2  (chem)
      4) StdEnv/2020     (S)      9) openmpi/4.0.3    (m)
      5) gcccore/.9.3.0  (H)     10) flexiblas/3.0.4

Software environment version
----------------------------

The Alliance team in charge of software periodically releases new versions of
the environment, such as ``StdEnv/2020`` or ``StdEnv/2023``. On the IQ HPC
Platform, ``StdEnv/2020`` is the environment initially loaded when you connect.
The other environments are available and can be loaded. For instance:

.. code-block:: console

    [ofisette@ip09 ~]$ module load StdEnv/2023

    The following have been reloaded with a version change:
      1) StdEnv/2020 => StdEnv/2023           5) libfabric/1.10.1 => libfabric/1.18.0
      2) gcccore/.9.3.0 => gcccore/.12.3      6) openmpi/4.0.3 => openmpi/4.1.5
      3) gentoo/2020 => gentoo/2023           7) ucx/1.8.0 => ucx/1.14.1
      4) imkl/2020.1.217 => imkl/2023.2.0

Optimisation target
-------------------

Alliance software available on the IQ HPC Platform is optimised for x86
processors that support the AVX2 instruction set. It was not compiled to use
more recent instruction sets such as AVX512. This is the best choice to support
both the Intel and AMD CPUs on the compute nodes while ensuring good
performance. If you compile your code with GCC, the corresponding optimisation
option is ``-march=core-avx2``. With Intel compilers, use ``-xCORE-AVX2``.

We do not recommend to use a different architecture (e.g. ``module load
arch/avx512``) or to compile your code with a different option (e.g.
``-march=native`` or ``-xHost``) since that can lead to compatibility issues.

BLAS/LAPACK libraries
---------------------

The Alliance software offers several implementations of the `BLAS and LAPACK
<https://docs.alliancecan.ca/wiki/BLAS_and_LAPACK/en>`_ libraries for linear
algebra. Intel MKL is used by default on the IQ HPC Platform and most Alliance
clusters.

Software guides
---------------

The following pages detail the use of specific software packages. Some are also
available on the national clusters, in which case the focus is on the
specificities of using that software on the IQ HPC Platform.

.. toctree::
   :maxdepth: 1

   ansys
   mathematica
   pyqcm
   python
   qiskit
   quimb
   quspin
