QUIMB
=====

Quim est une bibliothèque Python pour l’information quantique et le problème à
plusieurs corps.

Installation
------------

.. code-block:: bash

    module load StdEnv/2020 gcc/9.3.0 openmpi/4.0.3
    module load python/3.10 scipy-stack/2022a igraph/0.10.2 slepc/3.17.2 kahypar/1.3.2
    virtualenv --no-download $HOME/venv/quimb
    source $HOME/venv/quimb/bin/activate
    pip install --no-index quimb[tensor] cotengra
    # Moteur supplémentaire optionel :
    pip install --no-index cupy jax
