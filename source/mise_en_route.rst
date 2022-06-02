.. mise_en_route

Connection à la plateforme
--------------------------


.. _Mise_en_route_windows:

Installation d'un client SSH (Windows seulement)
================================================

La connection à la plateforme CHP se fait au moyen du protocole SSH.
Par défault, alors que Linux et MacOS l'intègre nativement, les usagers de Windows doivent installer un client SSH.

Les utilisateurs ont le choix entre:

* Putty (`lien2 <https://www.chiark.greenend.org.uk/~sgtatham/putty/>`_, `utilisation <https://docs.alliancecan.ca/wiki/Connecting_with_PuTTY/fr>`_)
* MobaXterm (`lien <https://mobaxterm.mobatek.net/>`_, `utilisation <https://docs.alliancecan.ca/wiki/Connecting_with_MobaXTerm/fr>`_)
* ou Windows Subsystem for Linux (WSL, `lien <https://docs.microsoft.com/en-us/windows/wsl/install>`_)

De manière général, PuTTY et MobaXterm sont assez semblable, mais MobaXterm inclus plus de fonctionnalité.
WSL a l'avantage de virtualiser une machine Linux sur votre installation Windows dont l'environnement est assez semblable à la plateforme CHP.
WSL est cependant plus complexe à installer.


Connexion
=========

Les ressources CHP de l'IQ sont hebergés aux Centre de Calcul Scientifique de l'Université de Sherbrooke, et sont actuellement branchées sur la grappe nationale Mammouth Parallèle 2 (abrégée MP2).
Leur accès requiert un compte Calcul Canada Database (CCDB) ainsi que la signature d'un entente d'utilisation (voir XX).
Une fois l'accès garanti, la connection se fait par SSH via un terminal (MacOS et Linux) ou le client SSH Windows nouvellement installé - voir rubrique :ref:`Mise_en_route_windows` ci-dessus:

.. code-block:: bash

   ssh <nom_utilisateur_CCDB>@mp2.computecanada.ca

Les utilisateurs sont ensuite invités à entrer leur mot de passe de la CCDB.
Notez qu'aucuns caractères ne s'affiche à l'écran mais ils sont bel et bien entrés dans le système.

Après connexion, les usagers arrivent sur le noeuds de connexion de la grappe MP2 avec une architecture très différente de celle des serveurs de calcul de l'IQ.
Ainsi, les noeuds de connexion doivent être utilisés uniquement pour la gestion de l'espace de travail et des fichiers, mais pas pour la compilation de logiciel ou la création d'environnement virtuel Python.
Ces derniers doivent s'effectué directement sur les serveurs de l'IQ via une allocation interactive (voir `TODO`_).


Chargement des logiciels
========================

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

Pour un complément d'informations sur l'utilisation des modules, voir la documentation correspondance sur le site de l'Alliance `ici <https://docs.alliancecan.ca/wiki/Utiliser_des_modules>`_.


Accéder au serveur de données de l'IQ et spécificités réseau
============================================================

Serveur de données accessible sur ``/net/nfs-iq/data``.
Chaque utilisateur possède un espace propre avec son nom d'utilisateur (par exemple, ``/net/nfs-iq/data/moroub`` pour l'utilisateur ``moroub``) et un espace partagée avec son groupe de la même manière que l'espace ``/project`` sur les grappes nationales.

Espace ``/scratch`` non accessible depuis les calculateurs de l'IQ

Connexion entre les noeuds de calcul de l'IQ et le répertoire ``/home`` et ``/project`` à 1 Gb/s.

Connexion internoeuds de calcul de l'IQ et avec le serveur de donnée à 10 Gb/s.
