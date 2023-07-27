.. Installation_logiciels:

Installation de logiciels (recettes)
------------------------------------

Cette page présente les recettes permettant d'installer les logiciels souvent utilisés à l'IQ.


Mathematica
===========

Mathematica est un logiciel propriétaire de calcul formel et numérique développé par Wolfram Research.
Mathematica version 12.1 est installé sur le NAS de l'IQ et les exécutables se trouvent sous ``/net/nfs-iq/data/software/Mathematica/12.1/Executables``.
Néanmoins, son utilisation requiert une licence disponible auprès du Département de physique de l'université.
Les licences sont distribuées via un serveur de licence en ligne sur le réseau de l'université, et les usagers doivent donc se connecter depuis les serveurs de calcul sur le réseau de l'université via le serveur Bethe avec un tunnel SSH (à faire avant chaque calcul):

.. code-block:: bash
    
    ssh -N -f -L 16286:10.44.34.42:16286 [cip_usherbrooke]@bethe.physique.usherbrooke.ca


Exemple d'utilisation de Mathematica en tâche interactive:

.. code-block:: bash
    
    salloc -p c-iq --mem=4G --cpu-per-task=1 --time=01:00:00 #demande d'allocation interactive
    ssh -N -f -L 16286:10.44.34.42:16286 [cip_usherbrooke]@bethe.physique.usherbrooke.ca #demande mot de passe usherbrooke pour le lien avec Bethe
    /net/nfs-iq/data/software/Mathematica/12.1/Executables/wolframscript -file script.wls #exécute les commandes dans le fichier script.wls


Pour les tâches en batch, il est nécessaire de créer une clé SSH car il n'est pas possible d'interagir pour entrer le mot de passe pour le lien vers le serveur Bethe:

* Création de la clé SSH dans ``~/.ssh/id_bethe_ed25519``:

.. code-block:: bash
    
    ssh-keygen -t ed25519 #à mettre dans ~/.ssh/id_bethe_ed25519
    

* Copie de la clé public sur Bethe:

.. code-block:: bash
    
    cat ~/.ssh/id_bethe_ed25519.pub
    ssh [cip_usherbrooke]@bethe.physique.usherbrooke.ca
    echo "[Le contenu de id_bethe_ed25519.pub affiché avec la commande cat]" >> ~/.ssh/authorized_keys


* Dans le script de tâche, spécifier le tunnel SSH d'utiliser la clé (exemple):

.. code-block:: bash
    
    #!/bin/bash
    #SBATCH --time=02:00:00
    #SBATCH --cpus-per-task=2
    #SBATCH --mem=8G
    
    ssh -N -f -L 16286:10.44.34.42:16286 [cip_usherbrooke]@bethe.physique.usherbrooke.ca -i ~/.ssh/id_bethe_ed25519
    /net/nfs-iq/data/software/Mathematica/12.1/Executables/wolframscript -file script.wls




Pyqcm
=====

Pyqcm est une librairie Python développé par David Sénéchal qui implémente les méthodes des clusters pour pour les systèmes quantiques hautement corrélés.

Instructions d'installation (voir aussi la `documentation de Pyqcm <https://dsenech.github.io/qcm_wed_doc/intro.html#installation>`_):

.. code-block:: bash

    git clone https://bitbucket.org/dsenechQCM/qcm_wed #download
    cd qcm_wed #enter source dir
    git checkout v2.1.4 #check the latest version (June 28th, 2023)
    module load StdEnv/2020 gcc/9.3.0 cmake/3.23.1 python/3.9 flexiblas/3.0.4 eigen/3.4.0 scipy-stack
    virtualenv env_qcm --no-download #create virtual environment
    source env_qcm/bin/activate #activate it
    export CMAKE_ARGS="-DDOWNLOAD_CUBA=1 -DEIGEN_HAMILTONIAN=1 -DWITH_PRIMME=1 -DDOWNLOAD_PRIMME=1 -DBLA_VENDOR=FlexiBLAS -DWITH_GF_OPT_KERNEL=1"
    pip install . --no-index

Ne pas oublier de charger le module FlexiBLAS avant de lancer un calcul avec Pyqcm afin d'utiliser la librairie BLIS plus performante sur les processeurs AMD comme ceux des serveurs de calcul de l'IQ (voir `BLAS et LAPACK <https://docs.alliancecan.ca/wiki/BLAS_and_LAPACK/fr>`_).


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

    module load StdEnv/2020  gcc/9.3.0  openmpi/4.0.3
    module load python/3.10 scipy-stack/2022a igraph/0.10.2 slepc/3.17.1
    virtualenv env_quimb --no-download
    source env_quimb/bin/activate
    pip install quimb[tensor] cotengra --no-index
    


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

 

 
