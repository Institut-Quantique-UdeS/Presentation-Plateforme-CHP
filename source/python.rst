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
 

Recherche des librairies Python précompilées
============================================

La commande ``avail_wheels`` permet de rechercher les librairies Python précompilées par les équipes de l'Alliance et optimisées pour les serveurs de l'IQ, par exemple pour Qiskit:

.. code-block:: bash

    [moroub@ip09-rockylinux8 ~]$ avail_wheels qiskit
    name    version    python    arch
    ------  ---------  --------  -------
    qiskit  0.39.3     py3       generic

Qiskit version 0.39.3 optimisé pour les serveurs de l'IQ peut donc être installé via ``pip install qiskit==0.39.3 --no-index``. 

En revanche, la commande précédente ne cherche que dans l'environnement standard chargé (par défaut en version 2020).
Il est possible que des versions plus récentes soient disponible dans le nouvel environnement standard 2023:

.. code-block:: bash

    [moroub@ip09 ~]$ module load StdEnv/2020 && avail_wheels pyqcm --all
    name    version    python    arch
    ------  ---------  --------  ------
    pyqcm   2.3.1      cp39      avx2
    pyqcm   2.3.1      cp311     avx2
    pyqcm   2.3.1      cp310     avx2
    
    [moroub@ip09 ~]$ module load StdEnv/2023 && avail_wheels pyqcm --all
    
    The following have been reloaded with a version change:
      1) StdEnv/2020 => StdEnv/2023          3) gentoo/2020 => gentoo/2023           5) libfabric/1.10.1 => libfabric/1.18.0     7) ucx/1.8.0 => ucx/1.14.1
      2) gcccore/.9.3.0 => gcccore/.12.3     4) imkl/2020.1.217 => imkl/2023.2.0     6) openmpi/4.0.3 => openmpi/4.1.5

    name    version    python    arch
    ------  ---------  --------  ---------
    pyqcm   2.4.3      cp311     x86-64-v3
    pyqcm   2.4.3      cp310     x86-64-v3


Environnement virtuel
=====================

Il est (vivement) recommandé d'utiiser des environnements virtuels Python pour lancer des tâches de calcul sur les serveurs de calcul de l'IQ, et à raison d'un environnement par tâche de calcul spécifique.
Les environnements virtuels Python ont tout d'abord l'avantage d'isoler chaque tâche de calcul, ce qui limite les conflits de version entre certaines librairies.
Ils fournissent de plus un environnement réplicable entre différentes machines.
La liste des librairies installées peut-être imprimer dans un fichier ``requirement.txt`` avec la commande:

.. code-block:: bash

   pip freeze > requirements.txt

Qui peut ensuite être transmis sur une autre machine pour reproduire l'environnement avec:

.. code-block:: bash

   pip install -r requirements.txt

La création d'un environnement virtuel sur les serveurs de calcul de l'IQ se fait comme suit:

.. code-block:: bash

   module load python/3.XX  		#chargement de Python 3.XX
   virtualenv --no-download ENV         #création environnement virtuel
   source ENV/bin/activate              #activation de l'environnement virtuel
   pip install --no-index X Y Z ...     #installation des librairies, l'option
                                        #--no-index permet d'installer les libraries
                                        #précompilées et optimisées par les équipe de l'Alliance


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
