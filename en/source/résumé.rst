Summary
=======

**Account**
    Use your Utilisez `CCDB <https://ccdb.alliancecan.ca/>`_ username and
    password.

**Login node**
    SSH: ``ip09.ccs.usherbrooke.ca``

**Home directory**
    - Location: ``/home/$USER``
    - Do not use for jobs (bad input/output performance)

**Research data**
    - Location: ``/net/nfs-iq/data``
    - Toujours utiliser pour les tâches (bonne performance entrée-sortie)
    - Total capacity: 190T
    - Redundant storage
    - Individual data: ``/net/nfs-iq/data/$USER``
    - Group data: ``/net/nfs-iq/data/def-$PARRAIN``

**Public compute nodes**
    .. include:: nœuds/public.rst

    - Jobs must be submitted to the ``c-iq`` partition.
        - Interactive job: ``salloc -p c-iq``
        - In a job script: ``#SBATCH --partition=c-iq``
    - GPUs are not managed by the job scheduler.
        - Interactive job: ``-p c-iq -w cp3705``
        - Job script: ``#SBATCH --partition=c-iq`` ``#SBATCH --nodelist=cp3705``
        - Use ``export CUDA_VISIBLE_DEVICES=[...]`` to control which GPU(s) to
          use.

**MP2 access**
    Most MP2 resources are accessible from the IQ HPC Platform. This includes
    partitions such as ``c-apc``, ``c-aphex``, ``c-royer``, etc. MP2
    ``/project`` and ``/scratch`` storage are not accessible.

**Access from MP2**
    The IQ HPC Platform’s research data storage is accessible from MP2 at
    ``/net/nfs-iq/data``.

**Alliance software**
    - Use the ``module`` command for software packages
    - Use the ``avail_wheels`` command for Python packages
    - Default environment: ``StdEnv/2020``
    - Default optimisation target: AVX2
    - Default BLAS/LAPACK libraries: Intel MKL
