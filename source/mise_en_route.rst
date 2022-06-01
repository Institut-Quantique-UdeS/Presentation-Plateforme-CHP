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


Rappel des commandes Linux basiques
===================================

Navigation
##########

Les commandes basiques pour la navigation dans le système de fichiers sont disponibles dans le tableau ci-dessous:

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Commande
     - Description
   * - ``pwd``
     - Retourne le chemin absolu vers l'emplacement actuel
   * - ``ls``
     - Liste les fichiers et répertoires à l'emplacement actuel
   * - ``cd <dir>``
     - Entre dans le répertoire ``<dir>``
   * - ``mv <orig> <dest>``
     - Déplace ou renomme le fichier ou le répertoire ``<orig>`` à ``<dest>``
   * - ``cp <orig> <dest>``
     - Copie le fichier donnée par le chemin ``<orig>`` au chemin de destination ``<dest>``
   * - ``cp -r <orig> <dest>``
     - Copie le répertoire ``<orig>`` au chemin de destination ``<dest>``
   * - ``rm <file>``
     - Supprime le fichier donnée par le chemin `<file>` (attention, suppression permanente, pas de corbeille:)
   * - ``rm <dir>``
     - Supprime le répertoire donnée par le chemin `<file>` (attention, suppression permanente, pas de corbeille!)

À noter que ``./`` designe l'emplacement actuelle.
Par example, ``cd ./`` demande à la ligne de commande d'aller dans le répertoire actuel (donc ne fait rien), ou encore, ``cp folder1/foo.txt ./`` copie le fichier `foo.txt` situé dans le dossier `folder1` dans le répertoire actuel (d'où est appelé la commande ``cp``).
Aussi ``..`` désigne le répertoire parent. 
Par exemple ``cd ..`` signifie retourner dans le répertoire précédent.
Finalement, ``~`` désigne le répertoire *home*, soit le répertoire d'arrivée juste après la connexion par SSH.


Edition de fichier ASCII
########################

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Commande
     - Description
   * - ``cat <file>``
     - Affiche le contenu du fichier ``<file>`` dans le terminal
   * - ``head -n X <file>`` 
     - Affiche les X premières lignes du fichier ``<file>`` dans le terminal
   * - ``tail -n X <file>``
     - Affiche les X dernières lignes du fichier ``<file>`` dans le terminal
   * - ``less <file>``
     - Affiche le contenu du fichier ``<file>`` avec defilement (appuyer sur ``q`` pour quitter)
   * - ``touch <file>``
     - Crée un fichier vide nommé `<file>``
   * - ``nano <file>``
     - Ouvre le fichier ``<file>`` dans un éditeur de fichier interactif. Appuyer sur `Crtl+O` pour sauvegarder et `Ctrl+X` pour quitter


Autres ressources
#################

Pour une introduction plus profonde à la ligne de commande, il est possible de suivre l'autoformation d'introduction de Software Carpentry (disponible `ici <https://swcarpentry.github.io/shell-novice/>`_), ou les formations de Calcul Québec (voir la page `EventBrite dédiée <https://www.eventbrite.ca/o/calcul-quebec-8295332683>`_)

