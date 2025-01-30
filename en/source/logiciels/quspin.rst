QuSpin
======

QuSpin is an `Open Source` Python package for exact diagonalisation and
quantum dynamics of arbitrary bosons, fermions, and spin many-body systems. It
supports a variety of user-defined symmetries in one and higher dimensional
lattice systems, and time evolution following a user-specified protocol.

Installation
------------

.. code-block:: bash

    module load StdEnv/2020
    module load python/3.9 scipy-stack/2023a
    virtualenv --no-download $HOME/venv/quspin
    source $HOME/venv/quspin/bin/activate
    # Install dependencies:
    pip install --no-index dill==0.3.7 numba==0.57.0 numexpr==2.8.4 joblib==1.3.2 gmpy2==2.1.5
    # Install from a local package:
    pip install --no-index /net/nfs-iq/data/software/QuSpin/quspin-0.3.7-cp39-cp39-linux_x86_64.whl
