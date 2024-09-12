Ligne de commande Linux
=======================

La plateforme CHP-IQ, les grappes de l’Alliance et tous les superordinateurs
recensés dans le TOP500 utilisent le système d’exploitation Linux. Vous devez
connaître les bases de la ligne de commande Linux/UNIX afin d’utiliser presque
n’importe quelle système dédié au calcul haute performance.

Si vous n’êtes pas déjà familier avec Linux ou si vous souhaitez rafraîchir vos
connaissances, nous vous recommandons fortement les `formations de Calcul Québec
<https://www.calculquebec.ca/services-aux-chercheurs/formation/>`_. Si aucune
formation n’est organisée prochainement, n’hésitez pas à contacter notre
:doc:`support technique <../aide/support>` pour des formations locales
personnalisées. Finalement, la documentation technique de l’Alliance offre une
courte `introduction à Linux
<https://docs.alliancecan.ca/wiki/Linux_introduction/fr>`_.

Aide-mémoire Linux
------------------

Navigation
''''''''''

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
   * - ``rm -r <dir>``
     - Supprime le répertoire donnée par le chemin `<file>` (attention, suppression permanente, pas de corbeille!)

À noter que ``./`` designe l'emplacement actuelle.
Par example, ``cd ./`` demande à la ligne de commande d'aller dans le répertoire actuel (donc ne fait rien), ou encore, ``cp folder1/foo.txt ./`` copie le fichier `foo.txt` situé dans le dossier `folder1` dans le répertoire actuel (d'où est appelé la commande ``cp``).
Aussi ``..`` désigne le répertoire parent. 
Par exemple ``cd ..`` signifie retourner dans le répertoire précédent.
Finalement, ``~`` désigne le répertoire *home*, soit le répertoire d'arrivée juste après la connexion par SSH.


Edition de fichier ASCII
''''''''''''''''''''''''

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
