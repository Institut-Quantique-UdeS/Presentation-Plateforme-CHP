Pyqcm
=====

Pyqcm est une librairie Python développé par David Sénéchal qui implémente les méthodes des clusters pour pour les systèmes quantiques hautement corrélés.

Pyqcm est maintenant disponible comme librairie précompilée, l'installation se fait donc avec:

.. code-block:: bash

    module load StdEnv/2023
    module load python/3.10 scipy-stack/2023b
    virtualenv env_qcm --no-download #create virtual environment
    source env_qcm/bin/activate #activate it
    pip install pyqcm --no-index

Pour une installation personnalisée, par exemple, pour version de développement ou expérimentation des options (voir aussi la `documentation de Pyqcm, section installation <https://dsenech.github.io/qcm_wed_doc/intro.html#installation>`_):

.. code-block:: bash

    git clone https://bitbucket.org/dsenechQCM/qcm_wed #download
    cd qcm_wed #enter source dir
    module load StdEnv/2023 cmake/3.27.7 python/3.10 flexiblas/3.3.1 eigen/3.4.0 scipy-stack cuba/4.2.2 primme/3.2
    virtualenv env_qcm --no-download #create virtual environment
    source env_qcm/bin/activate #activate it
    export CMAKE_ARGS="-DEIGEN_HAMILTONIAN=1 -DWITH_PRIMME=1 -DBLA_VENDOR=FlexiBLAS -DPRIMME_DIR=$EBROOTPRIMME -DCUBA_DIR=$EBROOTCUBA -DWITH_GF_OPT_KERNEL=1"
    pip install . --no-index

Note: l'implémentation BLIS de la librairie BLAS possède de faible performance sur les processeurs AMD comme ceux des serveurs de calcul de l'IQ (voir `documentation de pyqcm, section calculs parallèles <https://qcm-wed.readthedocs.io/en/stable/parallel.html#numerical-integration>`_).
Ainsi, il est recommandé d'utiliser Intel MKL (défaut) ou OpenBLAS via la variable d'environnement FLEXIBLAS (voir `BLAS et LAPACK <https://docs.alliancecan.ca/wiki/BLAS_and_LAPACK/fr>`_).
