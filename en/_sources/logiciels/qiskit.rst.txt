Qiskit
======

Qiskit is an IBM platform for quantum computing.

Installation
------------

.. code-block:: bash

    module load StdEnv/2020
    module load python/3.9 scipy-stack/2023b symengine/0.9.0
    virtualenv --no-download $HOME/venv/qiskit
    source $HOME/venv/qiskit/bin/activate
    pip install --no-index qiskit==0.44.2 qiskit-aer==0.12.2

This installs the Qiskit AER simulator with GPU support. It is therefore not
necessary to install ``qiskit-aer-gpu``.
