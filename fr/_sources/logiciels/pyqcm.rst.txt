Pyqcm
=====

Pyqcm est une bibliothèque Python développée par David Sénéchal, qui implémente
les méthodes des grappes pour les systèmes quantiques hautement corrélés.

Pyqcm est disponible comme paquet Python précompilé :

.. code-block:: bash

    module load StdEnv/2023
    module load python/3.11.5 scipy-stack/2024b
    virtualenv --no-download $HOME/venv/qcm
    source $HOME/venv/qcm/bin/activate
    pip install --no-index --upgrade pip
    pip install --no-index pyqcm==2.4.3

Pour une installation personnalisée, par exemple une version de développement ou
pour expérimenter avec des options :

.. code-block:: bash

    git clone https://bitbucket.org/dsenechQCM/qcm_wed
    cd qcm_wed
    module load StdEnv/2023 gcc/12.3
    module load python/3.11.5 scipy-stack/2024b
    module load flexiblas/3.3.1 eigen/3.4.0 cuba/4.2.2 primme/3.2
    virtualenv --no-download $HOME/venv/qcm
    source $HOME/venv/qcm/bin/activate
    pip install --no-index --upgrade pip
    export CMAKE_ARGS="-DEIGEN_HAMILTONIAN=1 -DWITH_PRIMME=1 -DBLA_VENDOR=FlexiBLAS -DPRIMME_DIR=$EBROOTPRIMME -DCUBA_DIR=$EBROOTCUBA -DWITH_GF_OPT_KERNEL=1"
    pip install . --no-index

.. note::

    Les auteurs de Pyqcm `rapportent une faible performance avec BLIS
    <https://qcm-wed.readthedocs.io/en/stable/parallel.html#numerical-integration>`_.
    Sur la plateforme CHP-IQ, Intel MKL est utilisé par défaut. Nous
    recommandons de ne pas lui substituer une autre implémentation de BLAS.

.. seealso::

    - `Documentation de Pyqcm <https://dsenech.github.io/qcm_wed_doc/>`_
