Qiskit
======

Qiskit is an IBM platform for quantum computing.

Installation
------------

.. code-block:: bash

    module load StdEnv/2023
    module load python/3.11.5 symengine/0.13.0
    virtualenv --no-download $HOME/venv/qiskit
    source $HOME/venv/qiskit/bin/activate
    pip install --no-index --upgrade pip
    pip install --no-index qiskit==2.0.2 qiskit-aer
    # For GPU support
    pip install --no-index qiskit-aer-gpu
