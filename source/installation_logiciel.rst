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

Instructions d'installation (voir aussi la `documentation de Pyqcm <https://dsenech.github.io/qcm_wed_doc/intro.html#installation>_`):

.. code-block:: bash

    git clone https://bitbucket.org/dsenechQCM/qcm_wed #download
    cd qcm_wed #enter source dir
    git checkout v1.1.2 #check the latest version (16 feb 2023)
    module load StdEnv/2020 gcc/9.3.0 cmake/3.23.1 python/3.9
    virtualenv env_qcm --no-download #create virtual environment
    source env_qcm/bin/activate #activate it
    pip install . --no-index


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

 

 
