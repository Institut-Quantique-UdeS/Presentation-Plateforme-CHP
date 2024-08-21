QuSpin
======

QuSpin is an open-source Python package for Exact Diagonalization and quantum dynamics of arbitrary boson, fermion and spin many-body systems, supporting the use of various (user-defined) symmetries in one and higher dimensional lattice systems and (imaginary) time evolution following a user-specified driving protocol.

.. code-block:: bash

    module load python/3.9 scipy-stack/2023a
    virtualenv env_quspin --no-download
    source env_quspin/bin/activate
    pip install dill==0.3.7 numba==0.57.0 numexpr==2.8.4 joblib==1.3.2 gmpy2==2.1.5 --no-index
    pip install /net/nfs-iq/data/software/QuSpin/quspin-0.3.7-cp39-cp39-linux_x86_64.whl --no-index
