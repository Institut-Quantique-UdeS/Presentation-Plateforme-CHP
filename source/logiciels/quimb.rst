QUIMB
=====

Quimb is an easy but fast python library for quantum information and many-body calculations, including with tensor networks.

.. code-block:: bash

    module load StdEnv/2020 gcc/9.3.0 openmpi/4.0.3
    module load python/3.10 scipy-stack/2022a igraph/0.10.2 slepc/3.17.2 kahypar/1.3.2
    virtualenv env_quimb --no-download
    source env_quimb/bin/activate
    pip install quimb[tensor] cotengra --no-index
    pip install cupy jax --no-index #optional backend option
