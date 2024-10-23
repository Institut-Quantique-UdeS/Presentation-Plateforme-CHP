Python
======

The information below is complementary to the `Python
<https://docs.alliancecan.ca/wiki/Python/fr>`_ page in the Alliance technical
documentation.

Modules
-------

To search for Python modules and load one:

.. code-block:: console

    [alice@ip09 ~]$ module spider python

    --------------------------------------------------------------------------------------
      python:
    --------------------------------------------------------------------------------------
        Description:
          Python is a programming language that lets you work more quickly and integrate
          your systems more effectively.

         Versions:
            python/2.7.18
            python/3.6.10
            python/3.7.7
            python/3.7.9
            python/3.8.2
            python/3.8.10
            python/3.9.6
            python/3.10.2
            python/3.10.13
            python/3.11.2
            python/3.11.5
            python/3.12.4
    ...

    [alice@ip09 ~]$ module spider python/3.10.2

    --------------------------------------------------------------------------------------
      python: python/3.10.2
    --------------------------------------------------------------------------------------
        Description:
          Python is a programming language that lets you work more quickly and integrate
          your systems more effectively.

        Properties:
          Tools for development / Outils de développement

        You will need to load all module(s) on any one of the lines below before
        the "python/3.10.2" module is available to load.

          StdEnv/2020
    ...

    [alice@ip09 ~]$ module load python/3.10.2

In addition to modules for Python itself, the Alliance software contains modules
for `Scientific Python`. Named ``scipy-stack``, they provide ``scipy`` but also
``numpy``, ``pandas``, ``matplotlib``, etc. Once your module for Python itself
is loaded:

.. code-block:: console

    [alice@ip09 ~]$ module avail scipy-stack

    ------------------------------------- Core Modules --------------------------------------
       scipy-stack/2020a (math)    scipy-stack/2021a (math)    scipy-stack/2023a (math)
       scipy-stack/2020b (math)    scipy-stack/2022a (math)    scipy-stack/2023b (L,math,D)
    ...

    [alice@ip09 ~]$ module load scipy-stack/2023b

Virtual environments
--------------------

As explained in the next section, Python packages (other than `Scientific
Python`) can be installed with the ``pip`` command, either by downloading them
from PyPI or by choosing from a collection of packages precompiled by the
Alliance software team. However, we recommend to never install Python packages
without first activating a virtual environment.

Virtual Python environment are directories containing a set of packages
installed for a given job. For instance, you could have a virtual environment
to simulate quantum systems with QuTiP and another for machine learning with
TensorFlow. You could even have several virtual environments for different QuTiP
or TensorFlow versions, as required for various projects.

By systematically using a virtual environment for your Python jobs, you
facilitate software installation, debugging, and research reproducibility.
Conversely, if you install all your Python packages in the default location, you
will encounter more software compatibility issues, and installing or updating a
package can cause previously successful jobs to stop working. In addition, you
will not be able to switch between different versions of a given package.
Finally, it will be more difficult to rerun a job on another computer or to
provide instructions to reproduce your software environment and, therefore, your
research.

To conclude this long explanation, here is a short demonstration. First, load
the modules for Python and `Scientific Python`:

.. code-block:: console

    [alice@ip09 ~]$ module load python/3.10.2
    [alice@ip09 ~]$ module load scipy-stack/2023b

Then, create a virtual environment:

.. code-block:: console

    [alice@ip09 ~]$ virtualenv $HOME/venv/qutip

Activate the environment:

.. code-block:: console

    [alice@ip09 ~]$ source $HOME/venv/qutip/bin/activate

Notice that the command prompt changes to show the active virtual environment.
All actions performed by the ``pip`` command (installing, uninstalling, updating
packages) will now target the ``$HOME/venv/qutip`` directory.

The first thing to do is update ``pip``:

.. code-block:: console

    (qutip) [alice@ip09 ~]$ pip install --no-index --upgrade pip    

Then, install packages, such as QuTiP :

.. code-block:: console

    (qutip) [alice@ip09 ~]$ pip install --no-index qutip==4.7.2

Finally, deactivate the environment.

.. code-block:: console

    (qutip) [alice@ip09 ~]$ deactivate

Once the environment has been created, it can be reused simply by activating it
again; there is no need to reinstall any packages. For example, the above
environment can be used in a job script with:

.. code-block:: bash

   module purge
   module load python/3.10.2
   module load scipy-stack/2023b
   source $HOME/venv/qutip/bin/activate

Precompiled Python packages
---------------------------

The ``avail_wheels`` command lists Python software packages precompiled by the
Alliance software team. These packages are optimised for HPC. For instance, to
search for Qiskit:

.. code-block:: console

    [alice@ip09 ~]$ avai l_wheels qiskit
    name    version    python    arch
    ------  ---------  --------  -------
    qiskit  0.39.3     py3       generic

To install this precompiled version in an active virtual environment:

.. code-block:: console

    (qiskit) [alice@ip09 ~]$ pip install --no-index qiskit==0.39.3

The above command will only search the loaded software environment (by default
``StdEnv/2020``). More recent versions of some packages are available in more
recent environments:

.. code-block:: console

    [alice@ip09 ~]$ module load StdEnv/2020 && avail_wheels pyqcm --all
    name    version    python    arch
    ------  ---------  --------  ------
    pyqcm   2.3.1      cp39      avx2
    pyqcm   2.3.1      cp311     avx2
    pyqcm   2.3.1      cp310     avx2
    
    [alice@ip09 ~]$ module load StdEnv/2023 && avail_wheels pyqcm --all
    
    The following have been reloaded with a version change:
      1) StdEnv/2020 => StdEnv/2023          3) gentoo/2020 => gentoo/2023           5) libfabric/1.10.1 => libfabric/1.18.0     7) ucx/1.8.0 => ucx/1.14.1
      2) gcccore/.9.3.0 => gcccore/.12.3     4) imkl/2020.1.217 => imkl/2023.2.0     6) openmpi/4.0.3 => openmpi/4.1.5

    name    version    python    arch
    ------  ---------  --------  ---------
    pyqcm   2.4.3      cp311     x86-64-v3
    pyqcm   2.4.3      cp310     x86-64-v3


Parallel computing with Python
------------------------------

Python code is typically not parallel. As a consequence, asking for more than
one CPU core will not automatically accelerate your jobs! You first need to
parallelise your code, either explicitly or by using parallelised library
functions, such as some of those in NumPy or SciPy.

Due to an intrinsic limitation, the “global interpreter lock”, Python code
cannot be parallelised using the shared memory model. However, there are
alternatives. One is to create a C/C++ Python extension using a parallel
programming library such as OpenMP. Another is to use the distributed memory
model with multiple Python processes. To do so, you can use the
``multiprocessing`` module, or a library such as `mpi4py
<https://mpi4py.readthedocs.io/en/stable/>`_ (message passing) or `Dask
<https://www.dask.org/>`_ (data parallelism).

.. _python-fils-label:

Thread oversubscription
'''''''''''''''''''''''

A common problem when dealing with parallelism in Python is thread
oversubscription: the number of execution threads started in a job is greater
than the number of allocated CPU cores. The ``multiprocessing`` module, in
particular, starts by default as many threads as there are CPU cores, with no
regards to whether or not these cores are accessible. For example, by default,
``multiprocessing`` would start 64 execution threads when used in a job
allocated to an IQ HPC Platform CPU node, even if you requested only 2, 4, or 8
cores.

This problem is compounded when using parallelised functions that also start as
many threads as there are cores (for instance ``scipy.sparse.linalg.eigsh``). To
build on the above example, in a job that uses both ``multiprocessing`` and
``eigsh``, 4096 execution threads (64 × 64) would be started by default, even
if the job only has access to 2, 4, or 8 cores. Performance is thus drastically
reduced.

To paliate this problem, you must instruct SciPy, ``multiprocessing``, Dask,
etc. to use the right number of execution threads. By adding the following
instructions to your job script (before your actual calculation), you disable
implicit parallelism in most functions, including those in SciPy, which use
OpenMP or Intel MKL in the background:

.. code-block:: bash

    export OMP_NUM_THREADS=1
    export MKL_NUM_THREADS=1

To control the number of processes started by ``multiprocessing``:

.. code-block:: python

    from multiprocessing import Pool
    from os import environ

    nprocesses = int(environ.get('SLURM_CPUS_PER_TASK', default=1))

    pool = Pool(nprocesses)

With Dask:

.. code-block:: python

    from os import environ
    from dask.distributed import LocalCluster

    nprocesses = int(environ.get('SLURM_CPUS_PER_TASK', default=1))

    cluster = LocalCluster(n_workers=nprocesses)

Conversely, if you do not use ``multiprocessing``, Dask, etc. but would rather
take advantage of SciPy’s parallel functions, set the number of execution
threads with:

.. code-block:: bash

    export OMP_NUM_THREADS=${SLURM_CPUS_PER_TASK:-1}
    export MKL_NUM_THREADS=${SLURM_CPUS_PER_TASK:-1}

.. seealso::

   - :ref:`This FAQ entry <calcul-lent-label>` discusses threads and performance
     issues in general.
