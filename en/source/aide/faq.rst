.. faq

Frequently asked questions
==========================

Frequent problems
-----------------

“Illegal instruction” (``SIGILL``)
''''''''''''''''''''''''''''''''''''

Your job causes an “illegal instruction” or ``SIGILL`` error, for instance:

.. code-block:: console

   [alice@ip11 ~]$ cat slurm-3304643.out 
   /var/spool/slurmd/job3304643/slurm_script: line 11: 25047 Illegal instruction   (core dumped) python my_script.py

Such errors happen when a program was optimised for a specific class of
processors but is being run on an incompatible processor.

If you compile your code on ``ip11`` with GCC, use the ``-march=core-avx2``
optimisation option. If you use the Intel compilers, the corresponding option is
``-xCORE-AVX2``. Do not use ``-march=native`` or ``-xHost``. The latter attempt
to optimise for the Intel processors on ``ip11``. The resulting program can be
incompatible with some compute nodes’ AMD processors.

..
    My interactive task on ``c-blais`` crashes on startup
    '''''''''''''''''''''''''''''''''''''''''''''''''''''

    Interactive tasks started on the ``c-blais`` partition (Kerrcat workstation) are
    currently not working:

    .. code-block:: console

        [alice@ip11 ~]$ salloc -p c-blais
        salloc: Granted job allocation 5810877
        salloc: Waiting for resource configuration
        salloc: Nodes cp3707 are ready for job
        srun: error: _find_node_record(751): lookup failure for cp3707
        srun: error: hostlist2bitmap: invalid node specified cp3707
        srun: fatal: ROUTE: Failed to make bitmap from hostlist=cp3707.
        salloc: Relinquishing job allocation 5810877

    Job scripts submitted with ``sbatch`` work normally.

    If you wish to run interactive jobs on ``c-blais``, use the ``--no-shell``
    option as follows, and cancel your job explicitely once you have finished:

    .. code-block:: console

       [alice@ip11 ~]$ salloc -p c-blais --no-shell
       salloc: Granted job allocation 5944655
       salloc: Waiting for resource configuration
       salloc: Nodes cp3707 are ready for job
       [alice@ip11 ~]$ ssh cp3707
       [alice@cp3707-mp2 ~]$ ...
       [alice@cp3707-mp2 ~]$ exit
       [alice@ip11 ~]$ scancel 5944655

.. _calcul-lent-label:

My computation is much slower than on my laptop
'''''''''''''''''''''''''''''''''''''''''''''''

You tested a parallel program on your laptop (or another computer). The program
also works in a job on the IQ HPC Platform but is much slower there. What is
going on?

First, make sure to use the same number of CPU cores on your laptop and in your
job to ensure the comparison is valid. For instance, if your laptop has 8 cores
and your program uses them all, you should request 8 CPU cores in your job. If
you ask for fewer, or, worse, a single core, performance will of course be
lower!

If the problem persists, check if your task :ref:`uses allocated resources
correctly <tâches-actives-label>`. A common problem is a parallel program that
tries to use all the CPU cores on a compute node even though they are not all
allocated to the job. For instance, a program could start 96 execution threads
to try to use the 96 CPU cores on a compute node from the ``c-iq`` partition,
even though that job only has access to a single core. The operating system will
then alternate between the 96 threads so that each one gets a share of CPU time.
This context switching causes an important performance degradation. In addition,
thread synchronisation problems can make performance even worse.

In most cases, the number CPU cores allocated to a job should match exactly the
number of processes or threads started by the job. If a job starts to many
threads or processes, ``htop`` will show more execution threads than expected,
and each thread will not use 100% CPU time as expected.

For parallel programs that use OpenMP execution threads, the problem can be
solved by setting the number of threads to match the number of allocated cores.
Add this instruction to your job script before your actual calculation:

.. code-block:: bash

   export OMP_NUM_THREADS=${SLURM_CPUS_PER_TASK:-1}

Some Intel MKL functions are automatically parallelised. In HPC, this implicit
parallelism is usually undesirable. You can deactivate it with:

.. code-block:: bash

   export MKL_NUM_THREADS=1

If you would rather use these parallel algorithms, set the number of threads
with:

.. code-block:: bash

   export MKL_NUM_THREADS=${SLURM_CPUS_PER_TASK:-1}

.. seealso::

   - :ref:`This section <python-fils-label>` in our Python guide discusses
     threading problems in the context of that programming language.
