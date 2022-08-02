.. python

Tâches de calcul en Python
--------------------------

Les innformations présentées ci-dessous sont complémentaires de la documentation de l'Alliance relative à `Python <https://docs.alliancecan.ca/wiki/Python/fr>`_. 

Le language de programmation Python est disponible sur les serveurs de calcul de l'IQ.
Il existe de multiples versions installées, allant de Python 3.6 à 3.10.2 et qui peuvent être détaillées avec:

.. code-block:: bash

   module spider python

La version voulue de Python peut être ensuite chargée avec (exemple pour la 3.9.6):

.. code-block:: bash

   module load python/3.9.6
 

Environnement virtuel
=====================

Il est (vivement) recommandé d'utiiser des environnements virtuels Python pour lancer des tâches de calcul sur les serveurs de calcul de l'IQ, et à raison d'un environnement par tâche de calcul spécifique.
Les environnements virtuels Python ont tout d'abord l'avantage d'isoler chaque tâche de calcul, ce qui limite les conflits de version entre certaines librairies.
Ils fournissent de plus un environnement réplicable entre différentes machines.
La liste des librairies installées peut-être imprimer dans un fichier ``requirement.txt`` avec la commande:

.. code-block:: bash

   pip freeze > requirement.txt

Qui peut ensuite être transmis sur une autre machine pour reproduire l'environnement avec:

.. code-block:: bash

   pip install -r requirement.txt

Finalement, dans la configuration actuel des serveurs de l'IQ, la création d'environnements virtuels doit s'effectuer directement sur les serveurs afin de bénéfier des dernières librairies Python disponibles et optimisées pour les serveurs.

La création d'un environnement virtuel sur les serveurs de calcul de l'IQ se fait comme suit:

.. code-block:: bash

   salloc -p c-iq -t 01:00:00 --mem 4G  #allocation de 1 heure, 1 CPU, 4Gb de RAM
   module load StdEnv/2020 python/3.XX  #chargement de Python 3.XX
   virtualenv --no-download ENV         #création environnement virtuel
   source ENV/bin/activate              #activation de l'environnement virtuel
   pip install --no-index X Y Z ...     #installation des librairies, l'option
                                        #--no-index permet d'installer les libraries
                                        #précompilées et optimisées par Calcul Canada

À noter qu'un environnement virtuel créé sur les serveurs de l'IQ ne peut être utilisé sur les noeuds de connexion de MP2, car l'environnement a en effet été optimisé pour des processeurs plus récent.


Parallélisation avec Python
===========================


Généralités
###########

Par défault, les scripts Python ne sont pas parallélisés, et donc la réservation de plusieurs coeurs ne diminuera pas le temps de calcul.
C'est alors la responsabilité de l'usager de paralléliser son code explicitement (voir section suivante) ou de vérifier que les librairies qu'il utilise bénéficie d'une parallélisation (tel que certaines fonction de NumPy ou de SciPy).


Parallélisation de données
##########################

Par construction, Python ne permet pas la parallélisation d'une tâche de calcul par mémoire partagée.
En revanche, il est possible de coder et de paralléliser les opérations les plus longues dans un autre langage (comme C++), puis d'appeler ce code dans Python.
Aussi, lorsque qu'un script Python est utilisé pour traiter plusieurs jeux de données, par exemplen une expérience avec divers jeux de paramètres, la librairie ``multiprocessing`` peut être utilisé pour traiter les différents jeux de données en parallèle via plusieurs processus.
Ce type de parallélisation, dit "de données", est toujours plus efficace que d'effectuer la parallélisation du traitement d'un jeu de donnée. 
C'est à dire, si un usager doit effectuer le même calcul sur 40 jeux de données différents, il sera plus efficace d'utiliser 40 processus en parallèle avec un jeu de données par processus plutôt que de traiter chacun des 40 jeux de données avec 40 processus.


*Thread-oversubscription*
#########################

Les différentes manière de parallèliser des tâches de calcul peuvent parfois entrer en confilt, notamment à travers la sur-souscription de fils (*thread-oversubsciption* en anglais).
Prenons l'exemple d'un usager voulant traiter 8 jeux de données sur un processeur 8 ceours avec la librairie ``multiprocessing``, en assignant un jeu de donnée par coeur (pour rappel, ce type de parallélisation est plus efficace que de traiter un jeu à la fois avec les 8 coeurs).
Cet usager utilise une fonction de la librairie SciPy (par exemple ``scipy.sparse.linalg.eigsh``) qui est elle aussi automatiquement parallélisé.
Ainsi, lors de l'éxecution du code, chaque coeur traitera un jeu de donnée, mais comme la fonction est elle-même parallélisée et voit 8 coeurs disponibles, elle va automatiquement s'exécuter sur ces 8 coeurs.
L'usager se retrouvera donc avec 64 (8 fois 8) fils roulant sur son processeur 8 coeurs, réduisant ainsi drastiquement les performances de son code.

Pour pallier à ce problème, il est nécessaire de spécifier à la fonction SciPy parallèliser de ne s'exécuter que sur un seul fil.
La libraire Python `ThreadPoolCtl <https://pypi.org/project/threadpoolctl/>`_ peut être utilisée dans ce cas.
