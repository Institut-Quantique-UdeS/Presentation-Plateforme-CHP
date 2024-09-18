Qiskit
======

Qiskit est une plateforme logicielle d’IBM pour le calcul quantique.

Installation
------------

.. code-block:: bash

    module load StdEnv/2020
    module load python/3.9 scipy-stack/2023b symengine/0.9.0
    virtualenv --no-download $HOME/venv/qiskit
    source $HOME/venv/qiskit/bin/activate
    pip install --no-index qiskit==0.44.2 qiskit-aer==0.12.2

A noter que cela installe le simulateur Qiskit AER avec prise en charge des GPU.
Il n’est donc pas nécessaire d’installer ``qiskit-aer-gpu``.
