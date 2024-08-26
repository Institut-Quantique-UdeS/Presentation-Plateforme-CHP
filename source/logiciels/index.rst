Logiciels
=========

Lorsque vous vous connectez à la plateforme CHP-IQ, votre environnement ne
contient initialement qu’un petit nombre de logiciels. Vous pouvez en ajouter à
partir du large éventail de `logiciels disponibles
<https://docs.alliancecan.ca/wiki/Available_software/fr>`_. Pré-installés et
optimisés pour le CHP, ces logiciels sont les mêmes qui sont disponibles sur les
grappes de la plateforme nationale, ce qui vous assure que vos tâches peuvent
être exécutées de manière reproductible sur toutes les grappes.

L’ajout de logiciels à votre environnement se fait principalement à l’aide de la
commande ``module``. Si vous n’êtes pas familier avec son utilisation, voyez
d’abord comment `utiliser des modules
<https://docs.alliancecan.ca/wiki/Utiliser_des_modules>`_. À titre d’exemple,
vous pouvez lister les modules chargés avec ``module list``, chercher des
modules avec ``module spider`` et les ajouter à votre environnement avec
``module load``. Par exemple :

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
         Autres candidats possibles :
            gromacs-colvars  gromacs-cp2k  gromacs-ls  gromacs-plumed  gromacs-ramd
            gromacs-swaxs

    --------------------------------------------------------------------------------------
      Pour trouver d'autres correspondances à votre recherche, exécutez :

          $ module -r spider '.*gromacs.*'

    --------------------------------------------------------------------------------------
      Pour de l'information détaillée à propos d'un module "gromacs" spécifique (incluant
      comment charger ce module), utilisez le nom complet. Par exemple :

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

        Propriétés:
          Chemistry libraries/apps / Logiciels de chimie

        Vous devrez charger tous les modules de l'un des lignes suivantes avant de pouvoir
        charger le module "gromacs/2023.2".

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

    Lmod a automatiquement remplacé "intel/2020.1.217" par "gcc/9.3.0"


    Dû à un changement dans la variable MODULEPATH, les modules suivants ont été rechargés :
      1) openmpi/4.0.3

    [ofisette@ip09 ~]$ module load gromacs/2023.2
    [ofisette@ip09 ~]$ module list

    Currently Loaded Modules:
      1) CCconfig                 6) gcc/9.3.0        (t)  11) fftw-mpi/3.3.8  (math)
      2) gentoo/2020     (S)      7) ucx/1.8.0             12) scalapack/2.1.0 (math)
      3) imkl/2020.1.217 (math)   8) libfabric/1.10.1      13) gromacs/2023.2  (chem)
      4) StdEnv/2020     (S)      9) openmpi/4.0.3    (m)
      5) gcccore/.9.3.0  (H)     10) flexiblas/3.0.4

Version de l’environnement logiciel
-----------------------------------

L’équipe de l’Alliance en charge des logiciels crée périodiquement de nouvelles
versions de l’environnement, par exemple ``StdEnv/2020`` ou ``StdEnv/2023``. Sur
la plateforme CHP-IQ, ``StdEnv/2020`` est l’environnement initialement chargé
lorsque vous vous connectez. Les autres environnements sont disponibles et
peuvent être chargés. Par exemple :

.. code-block:: console

    [ofisette@ip09 ~]$ module load StdEnv/2023

    Les modules suivants ont été rechargés avec un changement de version :
      1) StdEnv/2020 => StdEnv/2023           5) libfabric/1.10.1 => libfabric/1.18.0
      2) gcccore/.9.3.0 => gcccore/.12.3      6) openmpi/4.0.3 => openmpi/4.1.5
      3) gentoo/2020 => gentoo/2023           7) ucx/1.8.0 => ucx/1.14.1
      4) imkl/2020.1.217 => imkl/2023.2.0

Cible d’optimisation
--------------------

Les logiciels de l’Alliance disponibles sur la plateforme CHP-IQ sont optimisés
pour l’utilisation de processeurs x86 qui supportent le jeu d’instructions AVX2.
Ces logiciels n’ont pas été compilés pour utiliser d’instructions plus récentes
telles qu’AVX512. C’est le meilleur choix pour supporter à la fois les
processeurs Intel et AMD des nœuds de calcul tout en assurant une bonne
performance. Si vous compilez votre code avec GCC, l’option d’optimisation
correspondante est ``-march=core-avx2``. Avec les compilateurs Intel, utilisez
``-xCORE-AVX2``.

Nous ne recommendons pas d’utiliser une architecture différente (e.g. ``module
load arch/avx512``) ou de compiler votre code avec une option différente (e.g.
``-march=native`` ou ``-xHost``) car cela peut mener à des problèmes de
compatibilité.

Guides logiciels
----------------

Les pages suivantes portent sur l’utilisation de logiciels spécifiques. Certains
sont également disponibles sur les grappes de la plateforme nationale, auquel
cas l’accent est mis sur les particularités de leur utilisation avec la
plateforme CHP-IQ.

.. toctree::
   :maxdepth: 1

   ansys
   mathematica
   pyqcm
   python
   qiskit
   quimb
   quspin
