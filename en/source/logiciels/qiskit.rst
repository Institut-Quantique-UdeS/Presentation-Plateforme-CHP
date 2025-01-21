Qiskit
======

Qiskit is an IBM platform for quantum computing.

Installation
------------

.. code-block:: bash

    module load StdEnv/2023
    module load python/3.11.5 scipy-stack/2024b symengine/0.11.2
    virtualenv --no-download $HOME/venv/qiskit
    source $HOME/venv/qiskit/bin/activate
    pip install --no-index qiskit==1.2.4 qiskit-aer==0.14.2

This installs the Qiskit AER simulator with GPU support. It is therefore not
necessary to install ``qiskit-aer-gpu``.
