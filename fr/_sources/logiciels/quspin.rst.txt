QuSpin
======

QuSpin est un paquet Python `Open Source` pour la diagonalisation exacte et la
dynamique quantique de bosons, fermions et systèmes à plusieurs corps
arbitraires. Il supporte diverses symétries définies par l’utilisateur pour les
réseaux à dimension quelconque, ainsi que l’évolution temporelle suivant un
protocole spécifié par l’utilisateur.

Installation
------------

.. code-block:: bash

    module load StdEnv/2020
    module load python/3.9 scipy-stack/2023a
    virtualenv --no-download $HOME/venv/quspin
    source $HOME/venv/quspin/bin/activate
    # Installation des dépendances :
    pip install --no-index dill==0.3.7 numba==0.57.0 numexpr==2.8.4 joblib==1.3.2 gmpy2==2.1.5
    # Installation à partir d’un paquet local :
    pip install --no-index /net/nfs-iq/data/software/QuSpin/quspin-0.3.7-cp39-cp39-linux_x86_64.whl
