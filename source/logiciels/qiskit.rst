Qiskit
======

.. code-block:: bash

    module load StdEnv/2020
    module load python/3.9 scipy-stack/2023b symengine/0.9.0
    virtualenv --no-download env_qiskit
    source env_qiskit/bin/activate
    pip install qiskit==0.44.2 qiskit-aer==0.12.2 --no-index

A noter que cela installe le simulateur Qiskit AER avec prise en charge des GPUs.
Il n'y a pas besoin d'installer la librairie ``qiskit-aer-gpu``.
