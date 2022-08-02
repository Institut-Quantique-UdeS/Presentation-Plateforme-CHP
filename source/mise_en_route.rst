.. mise_en_route

Connection à la plateforme
--------------------------


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
Leur accès requiert un compte Calcul Canada Database (CCDB) ainsi que la signature d'un entente d'utilisation (voir :ref:`demande_d_acces`).
Une fois l'accès garanti, la connection se fait par SSH via un terminal (MacOS et Linux) ou le client SSH Windows nouvellement installé:

.. code-block:: bash

   ssh <nom_utilisateur_CCDB>@mp2.computecanada.ca

Les utilisateurs sont ensuite invités à entrer leur mot de passe de la CCDB.
Notez qu'aucuns caractères ne s'affiche à l'écran mais ils sont bel et bien entrés dans le système.
Après connexion, les usagers arrivent sur les noeuds de connexion de MP2.

Utilisation
===========

IMPORTANT! 
Les noeuds de connexion de la grappe MP2 ont une architecture CPU différente de celle des serveurs de calcul de l'IQ, en plus d'être configuré avec un environnement standard obsolète (``nixpkgs/16.09``).
Ainsi, les noeuds de connexion doivent être utilisés uniquement pour la gestion de l'espace de travail et des fichiers.
Toutes autres tâches, tel que la compilation de logiciel, la création d'environnement virtuel Python, ou le debogage de code doit se fare directement sur les serveurs de l'IQ via une allocation interactive (voir :ref:`taches_interactives`).


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
Pour un complément d'informations sur l'utilisation des modules, voir la documentation correspondante sur le site de l'Alliance (`Utiliser des modules <ttps://docs.alliancecan.ca/wiki/Utiliser_des_modules>`_).

Aussi, il se peut que certains logiciels peuvent apparaître comme non disponibles lorsque chargés sur les noeuds de connexion de MP2 (essayer ``module spider triqs`` par exemple).
Cela est dû à l'architecture différente des les noeuds de connexion de MP2, et pour laquelle ces logiciels n'ont pas été compilés.
Néanmoins, il se peut que ces logiciels soient tout de même disponibles et compilés pour l'architecture des noeuds de calcul de l'IQ.
Ainsi, il est nécessaire de se connecter directement sur les noeuds de l'IQ (via une allocation interactive, ``salloc -p c-iq -t 01:00:00 --mem 4G --cpus-per-task=1``) et de relancer la recherhce pour vérifier que ces logiciels sont bien disponibles.


Accéder au serveur de données de l'IQ et spécificités réseau
============================================================

Le serveur de données de l'IQ d'une capacité de 384 To est accessible sur ``/net/nfs-iq/data`` (depuis les noeuds de connexion et les serveurs de calcul de l'IQ, MP2 et autre).
Chaque utilisateur possède un espace propre avec son nom d'utilisateur (par exemple, ``/net/nfs-iq/data/moroub`` pour l'utilisateur ``moroub``) et un espace partagée avec son groupe de la même manière que l'espace ``/project`` sur les grappes nationales.

L'interconnection entre le serveur de données et les serveurs de calcul de l'IQ est 25 fois plus performante que l'interconnection avec ``/project`` ou ``/home`` (25 Gbit/s contre 1 Gb/s). 
Les usagers sont donc fortement incités à utiliser cette espace de stockage leur étant dédié.

