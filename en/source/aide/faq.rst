.. faq

Frequently asked questions
==========================

Frequent problems
-----------------

Missing file in a job
'''''''''''''''''''''

Did you submit a job script that cannot find one or more files from your home
directory? Did you start an interactive job but do not see your home directory
files?

This is “normal”. Your home directory on the compute nodes is the one from the
MP2 cluster, not the one from the IQ HPC Platform, unless your user account was
created recently. Files you put in your home directory when connected to
``ip09`` are therefore not accessible from your jobs.

There are two solutions. The first is to move your files to
``/net/nfs-iq/data``. This location should be used for all research data anyway
since it offers better performance. The second is to change your home directory
on the compute nodes to use the one from the IQ HPC Platform rather than the one
from MP2. :doc:`Contact us <support>` to make that change.

“Illegal instruction” (``SIGILL``)
''''''''''''''''''''''''''''''''''''

Your job causes an “illegal instruction” or ``SIGILL`` error, for instance:

.. code-block:: console

   [alice@ip09 ~]$ cat slurm-3304643.out 
   /var/spool/slurmd/job3304643/slurm_script: line 11: 25047 Illegal instruction   (core dumped) python my_script.py

Such errors happen when a program was optimised for a specific class of
processors but is being run on an incompatible processor.

First, check if you really submitted your job to the IQ HPC Platform compute
nodes using the ``--partition=c-iq`` option. Otherwise, your job will run on the
regular MP2 nodes, which have older processors that can be incompatible with
code compiled on ``ip09``.

If you compile your code on ``ip09`` with GCC, use the ``-march=core-avx2``
optimisation option. If you use the Intel compilers, the corresponding option is
``-xCORE-AVX2``. Do not use ``-march=native`` or ``-xHost``. The latter attempt
to optimise for the Intel processors on ``ip09``. The resulting program can be
incompatible with the compute nodes’ AMD processors.

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
