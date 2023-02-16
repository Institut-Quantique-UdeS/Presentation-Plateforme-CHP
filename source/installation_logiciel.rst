.. Installation_logiciels:

Installation de logiciels (recettes)
------------------------------------

Cette page présente les recettes permettant d'installer les logiciels souvent utilisés à l'IQ.
Toutes les installations sont à faire sur les noeuds de calcul de l'IQ, et PAS sur les noeuds de connexions de MP2 (différentes architectures).

Qiskit
======

.. code-block:: bash

    module load StdEnv/2020 
    module load python/3.9 scipy-stack symengine/0.9.0 flexiblas/3.0.4
    virtualenv --no-download env_qiskit
    source env_qiskit/bin/activate
    pip install qiskit==0.39.1 --no-index


Pyqcm
=====

Pyqcm est une librairie Python développé par David Sénéchal qui implémente les méthodes des clusters pour pour les systèmes quantiques hautement corrélés.

Instructions d'installation:

.. code-block:: bash

    git clone https://bitbucket.org/dsenechQCM/qcm_wed #download
    cd qcm_wed #enter source dir
    git checkout v1.1.2 #check the latest version (16 feb 2023)
    module load StdEnv/2020 gcc/9.3.0 cmake/3.23.1 python/3.9
    virtualenv env_qcm --no-download #create virtual environment
    source env_qcm/bin/activate #activate it
    pip install . --no-index


