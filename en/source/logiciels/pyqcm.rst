Pyqcm
=====

Pyqcm is a Python library developed by David Sénéchal, implementing quantum
cluster methods for highly correlated systems.

Pyqcm is available as a precompiled Python package:

.. code-block:: bash

    module load StdEnv/2023
    module load python/3.11.5 scipy-stack/2024b
    virtualenv $HOME/venv/qcm --no-download
    source $HOME/venv/qcm/bin/activate
    pip install --no-index pyqcm==2.4.3

For a custom installation, for instance a development version or to experiment
with options:

.. code-block:: bash

    git clone https://bitbucket.org/dsenechQCM/qcm_wed
    cd qcm_wed
    module load StdEnv/2023 gcc/12.3
    module load python/3.11.5 scipy-stack/2024b
    module load flexiblas/3.3.1 eigen/3.4.0 cuba/4.2.2 primme/3.2
    virtualenv $HOME/venv/qcm --no-download
    source $HOME/venv/qcm/bin/activate
    export CMAKE_ARGS="-DEIGEN_HAMILTONIAN=1 -DWITH_PRIMME=1 -DBLA_VENDOR=FlexiBLAS -DPRIMME_DIR=$EBROOTPRIMME -DCUBA_DIR=$EBROOTCUBA -DWITH_GF_OPT_KERNEL=1"
    pip install . --no-index

.. note::

    The Pyqcm authors `report low performance with BLIS
    <https://qcm-wed.readthedocs.io/en/stable/parallel.html#numerical-integration>`_.
    On the IQ HPC Platform, Intel MKL is used by default. We recommend not to
    substitute a different BLAS implementation.

.. seealso::

    - `Pyqcm documentation <https://dsenech.github.io/qcm_wed_doc/>`_
