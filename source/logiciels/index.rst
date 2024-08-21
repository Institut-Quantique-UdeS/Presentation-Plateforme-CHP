Logiciels
=========

Par défault, l'environnement de travail après la connexion ne contient aucuns logiciels.
Ceux-ci doivent donc être chargés manuellement sous la forme de module.
De nombreux logiciels sont pré-compilés et disponibles pour utilisation dans la pile logicielle d'Alliance qui est utilisée sur les serveurs de calcul.
Pour rechercher si un logiciel est installé et quelles versions sont disponibles:

.. code-block:: bash

   module spider <nom_du_logiciel>

Pour plus d'information sur une version spécifique et comment charger le module correspondant, il faut ajouter la version du logiciel:

.. code-block:: bash

   module spider <nom_du_logiciel>/<version>

Le chargement du logiciel se fait alors par la commande:

.. code-block:: bash

   module load <nom_du_logiciel>
   
Parfois, il est nécessaire de charger plusieurs modules avant de pouvoir charger le logiciel voulu.
En effet, certain modules dépendent d'autres modules qui doivent être présents pour assurer leur bon fonctionnement.
Il faut alors consulter la sortie de ``module spider X`` pour obtenir plus d'informations.
Pour un complément d'informations sur l'utilisation des modules, voir la documentation correspondante sur le site de l'Alliance (`Utiliser des modules <https://docs.alliancecan.ca/wiki/Utiliser_des_modules>`_).

Guides logiciels
----------------

.. toctree::
   :maxdepth: 1

   ansys
   mathematica
   pyqcm
   python
   qiskit
   quimb
   quspin
