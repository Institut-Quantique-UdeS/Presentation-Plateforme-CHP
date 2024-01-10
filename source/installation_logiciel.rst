.. Installation_logiciels:

Installation de logiciels (recettes)
------------------------------------

Cette page présente les recettes permettant d'installer les logiciels souvent utilisés à l'IQ.


Mathematica
===========

Mathematica est un logiciel propriétaire de calcul formel et numérique développé par Wolfram Research.
Mathematica version 12.1 est installé sur le NAS de l'IQ et les exécutables se trouvent sous ``/net/nfs-iq/data/software/Mathematica/12.1/Executables``.
Les licences sont distribuées via un serveur de licence en ligne sur le réseau de du département de physique et de l'université de manière transparente.
Néanmoins, il est de la responsabilité de l'usager de se renseigner quant aux politiques d'accès à ces licences (si elles existent)

Exemple d'utilisation de Mathematica en tâche batch:

.. code-block:: bash
    
    #!/bin/bash
    #SBATCH --time=02:00:00
    #SBATCH --cpus-per-task=2
    #SBATCH --mem=8G
    
    /net/nfs-iq/data/software/Mathematica/12.1/Executables/wolframscript -file script.wls




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

Pour une installation personnalisée, par exemple, pour version de développement ou expérimentation des options (voir aussi la `documentation de Pyqcm <https://dsenech.github.io/qcm_wed_doc/intro.html#installation>`_):

.. code-block:: bash

    git clone https://bitbucket.org/dsenechQCM/qcm_wed #download
    cd qcm_wed #enter source dir
    module load StdEnv/2023 cmake/3.27.7 python/3.10 flexiblas/3.3.1 eigen/3.4.0 scipy-stack cuba/4.2.2 primme/3.2
    virtualenv env_qcm --no-download #create virtual environment
    source env_qcm/bin/activate #activate it
    export CMAKE_ARGS="-DEIGEN_HAMILTONIAN=1 -DWITH_PRIMME=1 -DBLA_VENDOR=FlexiBLAS -DPRIMME_DIR=$EBROOTPRIMME -DCUBA_DIR=$EBROOTCUBA -DWITH_GF_OPT_KERNEL=1"
    pip install . --no-index

Note: l'implémentation BLIS de la librairie BLAS possède de faible performance sur les processeurs AMD comme ceux des serveurs de calcul de l'IQ (voir `documentation de pyqcm <https://qcm-wed.readthedocs.io/en/stable/parallel.html#numerical-integration>`_).
Ainsi, il est recommandé d'utiliser Intel MKL (défaut) ou OpenBLAS via la variable d'environnement FLEXIBLAS (voir `BLAS et LAPACK <https://docs.alliancecan.ca/wiki/BLAS_and_LAPACK/fr>`_).


Qiskit
======

.. code-block:: bash

    module load StdEnv/2020 
    module load python/3.9 scipy-stack/2022a symengine/0.9.0 flexiblas/3.0.4
    virtualenv --no-download env_qiskit
    source env_qiskit/bin/activate
    #manually download requests-ntlm because the precompiled version is problematic
    wget https://files.pythonhosted.org/packages/03/4b/8b9a1afde8072c4d5710d9fa91433d504325821b038e00237dc8d6d833dc/requests_ntlm-1.1.0-py2.py3-none-any.whl
    pip install ./requests_ntlm-1.1.0-py2.py3-none-any.whl
    pip install qiskit==0.42.0 --no-index


A noter que cela installe le simulateur Qiskit AER avec prise en charge des GPUs.
Il n'y a pas besoin d'installer la librairie``qiskit-aer-gpu``.


QUIMB
=====

Quimb is an easy but fast python library for quantum information and many-body calculations, including with tensor networks.

.. code-block:: bash

    module load StdEnv/2020 gcc/9.3.0 openmpi/4.0.3
    module load python/3.10 scipy-stack/2022a igraph/0.10.2 slepc/3.17.2 kahypar/1.3.2
    virtualenv env_quimb --no-download
    source env_quimb/bin/activate
    pip install quimb[tensor] cotengra --no-index
    pip install cupy jax --no-index #optional backend option
    


QuSpin
======

QuSpin is an open-source Python package for Exact Diagonalization and quantum dynamics of arbitrary boson, fermion and spin many-body systems, supporting the use of various (user-defined) symmetries in one and higher dimensional lattice systems and (imaginary) time evolution following a user-specified driving protocol.

.. code-block:: bash

    module load python/3.9 scipy-stack/2023a
    virtualenv env_quspin --no-download
    source env_quspin/bin/activate
    pip install dill==0.3.7 numba==0.57.0 numexpr==2.8.4 joblib==1.3.2 gmpy2==2.1.5 --no-index
    pip install /net/nfs-iq/data/software/QuSpin/quspin-0.3.7-cp39-cp39-linux_x86_64.whl --no-index



Stim
====

Stim is a fast simulator for quantum stabilizer circuits.
    

Suite Ansys
===========

La suite de logiciel Ansys est une suite commerciale et nécessite un accès à une licence, via la plateforme CMC Microsystems par exemple.
La plateforme de calcul haute performance de l'IQ est doté d'un serveur de licence CMC pour Ansys dédié.
La procédure pour charger Ansys sur la plateforme est la suivante:

#. Créer le fichier de licence ``~/.licences/ansys.lic`` avec le contenu suivant (voir :doc:`commandes_linux` pour la création et l'édition de fichier):

.. code-block:: bash

    setenv("ANSYSLMD_LICENSE_FILE", "6624@ip39.ccs.usherbrooke.ca")
    setenv("ANSYSLI_SERVERS", "2325@ip39.ccs.usherbrooke.ca")
    
#. Envoyer un courriel à CMC Microsystems (``mcsupport@cmc.ca``) avec votre nom d'utilisateur sur les serveurs de l'IQ, votre nom, le nom de la personne qui vous fourni la licence et le nom du serveur de licence (``ip39.ccs.usherbrooke.ca``).

#. CMC Microsystem active votre licence sur la plateforme de calcul de l'IQ sous quelques heures / jours.

Les modules Ansys se chargent de la même manière que sur les grappes de l'Alliance, par exemple avec la commande ``module load ansysedt/2021R2``. 
Vous pouvez aussi consulter la `documentation de l'Alliance <https://docs.alliancecan.ca/wiki/Ansys>`_  pour en savoir plus sur comment utiliser Ansys sur les serveurs de calcul.

Une version plus récente de AnsysEDT en version R2023.1 se trouve installer sur le NAS de l'IQ, sous ``/net/nfs-iq/data/software/AnsysEM/v231/``.

 

 
