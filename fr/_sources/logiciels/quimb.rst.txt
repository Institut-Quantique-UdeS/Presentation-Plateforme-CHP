QUIMB
=====

Quim est une bibliothèque Python pour l’information quantique et le problème à
plusieurs corps.

Installation
------------

.. code-block:: bash

    module load StdEnv/2023
    module load python/3.11.5
    virtualenv --no-download $HOME/venv/quimb
    source $HOME/venv/quimb/bin/activate
    pip install --no-index quimb==1.11.1

Pour générer des figures :

.. code-block:: bash

    pip install --no-index matplotlib==3.10.1 networkx==3.5

Pour utiliser Jax comme moteur d’optimisation :

.. code-block:: bash

    pip install --no-index jax==0.6.0

Pour utiliser Autograd comme moteur d’optimisation :

.. code-block:: bash

    pip install --no-index autograd==1.8.0
