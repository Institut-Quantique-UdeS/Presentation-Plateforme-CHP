Qiskit
======

Qiskit est une plateforme logicielle d’IBM pour le calcul quantique.

Installation
------------

.. code-block:: bash

    module load StdEnv/2023
    module load python/3.11.5 scipy-stack/2024b symengine/0.11.2
    virtualenv --no-download $HOME/venv/qiskit
    source $HOME/venv/qiskit/bin/activate
    pip install --no-index qiskit==1.2.4 qiskit-aer==0.14.2

A noter que cela installe le simulateur Qiskit AER avec prise en charge des GPU.
Il n’est donc pas nécessaire d’installer ``qiskit-aer-gpu``.
