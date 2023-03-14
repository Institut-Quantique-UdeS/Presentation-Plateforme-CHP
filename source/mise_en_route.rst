.. mise_en_route

Connexion et utilisation de la plateforme
-----------------------------------------


.. _Mise_en_route_windows:

Installation d'un client SSH (Windows seulement)
================================================

La connection à la plateforme CHP se fait au moyen du `protocole SSH <https://docs.alliancecan.ca/wiki/SSH/fr>`_.
Par défault, alors que Linux et MacOS l'intègre nativement, les usagers de Windows doivent installer un client SSH.

Les utilisateurs ont le choix entre:

* `Putty <https://www.chiark.greenend.org.uk/~sgtatham/putty/>`_ (`Utilisation <https://docs.alliancecan.ca/wiki/Connecting_with_PuTTY/fr>`_)
* `MobaXterm <https://mobaxterm.mobatek.net/>`_ (`Utilisation <https://docs.alliancecan.ca/wiki/Connecting_with_MobaXTerm/fr>`_)
* ou  `Windows Subsystem for Linux <https://docs.microsoft.com/en-us/windows/wsl/install>`_

De manière général, PuTTY et MobaXterm sont assez semblable, mais MobaXterm inclus plus de fonctionnalité.
WSL a l'avantage de virtualiser une machine Linux sur votre installation Windows dont l'environnement est assez semblable à la plateforme CHP.
WSL est cependant plus complexe à installer.


Connexion
=========

Les ressources CHP de l'IQ sont hebergés aux Centre de Calcul Scientifique de l'Université de Sherbrooke, et sont actuellement branchées sur la grappe nationale Mammouth Parallèle 2 (abrégée MP2).
Leur accès requiert soit un compte de l'Alliance via la base de données Calcul Canada (CCDB), soit un compte dédiée et restreint sur la plateforme de l'IQ (nom d'utilisateur commençant par **iq-**), notamment pour les personnes ne pouvant obtenir de sponsors sur la CCDB.
La signature de l'entente d'utilisation de la plateforme de calcul de l'IQ est aussi requise (voir :ref:`demande_d_acces`).
Une fois l'accès garanti, la connection se fait par SSH via un terminal (MacOS et Linux) ou le client SSH Windows nouvellement installé:

.. code-block:: bash

   ssh <nom_utilisateur_CCDB_ou_iq->@ip09.ccs.usherbrooke.ca

Les utilisateurs sont ensuite invités à entrer leur mot de passe de la CCDB ou leur mot de passe pour leur compte dédié aux serveurs de l'IQ.
Notez qu'aucuns caractères ne s'affiche à l'écran mais ils sont bel et bien entrés dans le système.
Après connexion, les usagers arrivent sur le noeud de connexion de la plateforme de l'IQ.


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
Pour un complément d'informations sur l'utilisation des modules, voir la documentation correspondante sur le site de l'Alliance (`Utiliser des modules <https://docs.alliancecan.ca/wiki/Utiliser_des_modules>`_).


Stockage des données et spécificités réseau
===========================================

Le serveur de données de l'IQ d'une capacité de 180 To est accessible sur ``/net/nfs-iq/data`` (depuis les noeuds de connexion et les serveurs de calcul de l'IQ, MP2 et autre).
Chaque utilisateur possède un espace propre avec son nom d'utilisateur (par exemple, ``/net/nfs-iq/data/moroub`` pour l'utilisateur ``moroub``) et un espace partagée avec son groupe de la même manière que l'espace ``/project`` sur les grappes nationales (voir `Répertoire /project <https://docs.alliancecan.ca/wiki/Project_layout/fr>`_).
Les données enregistrées dans les répertoire ``/net/nfs-iq/`` sont dupliquées sur deux disques pour prévenir le bris d'un des disques de données et sont sauvegardées à tout les X jours.

L'interconnection entre le serveur de données et les serveurs de calcul de l'IQ est 25 fois plus performante que l'interconnection avec ``/project`` ou ``/home`` (25 Gbit/s contre 1 Gb/s). 
Les usagers sont donc fortement incités à utiliser cette espace de stockage leur étant dédié.


Connexion via MP2 (ancienne méthode, non recommandée)
=====================================================

Il est aussi possible d'avoir accès à la plateforme de calcul haute performance de l'IQ via la grappe national MP2:

.. code-block:: bash

   ssh <nom_utilisateur_CCDB>@mp2.computecanada.ca
   
Cependant, cette méthode n'est valide que pour les usagers disposant d'un compte à la CCDB.
L'accès par MP2 n'est plus recommandé car l'architecture de MP2 est différente de celle des serveurs de l'IQ, bien plus récente tant au niveau matériel que logiciel.
Principales différences (non exhaustif):

* L'environnement standard de MP2 sur lequel les serveurs de l'IQ sont connectés est ``nixpkgs/16.09`` qui n'est plus maintenu. Il est donc nécessaire de charger le dernier environnement standard ``module load StdEnv/2020`` dans le script lors de la soumission d'une tâche de calcul sur les serveurs de l'IQ, ou à l'arriver sur les serveurs de l'IQ lors d'une tâche interactive.

* Les noeuds de connexion de MP2 possède une architecture différente que celle des serveurs de l'IQ. En conséquence, pour de meilleurs performances et une meilleure expérience utilisateur, la création d'environnements virtuels et la compilation de logiciels doit à faire directement sur les serveurs de l'IQ, par exemple via une allocation interactive (``salloc``).

* À cause des deux dernières différences entre les noeuds de MP2 et les serveurs de l'IQ, certains logiciels et librairies (incluant Python) peuvent ne pas être visibles ni chargés sur les noeuds de connexion de MP2 . Une allocation (``salloc -t 01:00:00 --mem 8G --cpus-per-task=1``) sur les noeuds de l'IQ résout le problème.

* L'espace ``/scratch`` de MP2 est non accessible depuis les calculateurs de l'IQ.
