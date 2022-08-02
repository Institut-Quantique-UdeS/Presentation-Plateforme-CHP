.. jobs

Lancement de tâches de calcul sur les serveurs
----------------------------------------------

Cette page est un complément d'information de la page de l'Alliance dédiée: `Exécuter des tâches <https://docs.alliancecan.ca/wiki/Running_jobs/fr>`_.

Les serveurs de calcul peuvent être utilisés de deux manières différentes qui correspondent à deux types de tâches distinctes:

* Les tâches dites interactives où les usagers sont redirigées sur les noeuds de calcul.

* Les tâches dites en batch où l'usager soumet la tâche à un ordonnanceur qui est responsable de l'exécution de la tâche sur les noeuds de calcul.

Dans tout les cas, il est interdit de lancer des tâches sur les noeuds de connexion.
En plus de pénaliser les autres utilisateurs qui font de la gestion de fichiers, ces noeuds ne disposent pas des derniers logiciels disponibles dans la pile de l'Alliance et offrent de mauvaises performances.


.. _taches_interactives:

Tâches interactives
===================

Les tâches interactives sont des tâches généralement courtes (moins de 4 heures) qui requiert l'action soutenue de l'usager, comme la réalisation de tests, l'exploration de données, le débogage ou la compilation de codes.
La commande ``salloc`` suivie de l'option ``-p c-iq`` permet d'être redirigé sur un noeuds de calcul de l'IQ avec 1 CPU et 8 Go de mémoire vive:

.. code-block:: bash

   salloc -p c-iq -t [HH]::[mm]:[ss] --mem=8G --cpu-per-task=1
   
À l'arrivé sur les serveurs de calcul, il est recommandé de charger de suite l'environnement standard le plus récent: 

.. code-block:: bash

   module load StdEnv/2020


Tâches en batch
===============

Les tâches en batch désignent toutes tâches qui ne nécessite pas l'action de l'usager (lancement d'un script Python par exemple).
Elle doit être la façon priviligié d'utiliser les serveurs de calcul car elle maximise leur l'efficacité.
Les scripts bash pour le lancement des tâches est exactement similaire aux scripts sur les autres grappes nationales de l'Alliance (voir la page `Exécuter des tâches <https://docs.alliancecan.ca/wiki/Running_jobs/fr>`_), à la seule différence qu'il est nécessaire de charger l'environnement standard ``StdEnv/2020`` dans le script.
La soumission se fait ensuite en précisant la partition des noeuds de l'IQ à l'ordonnanceur:

.. code-block:: bash

   sbatch -p c-iq job.sh


Calcul sur GPU
==============

Les tâches de calcul faisans l'utilisation de GPU ne sont pas différente des tâches CPU et peuvent être de type interactive ou en batch.

Au contraire des grappes nationales, les GPU ne sont pas connus de l'ordonnanceur et il faut donc spécifier explicitement le nom du serveur GPU (``cp3705``) de l'IQ à ce dernier avec l'option ``--nodelist=cp3705``.

Par exemple, pour soumettre une tâches interactive avec accès aux GPU, la commande est la suivante:

.. code-block:: bash

   salloc -p c-iq -t [HH]::[mm]:[ss] --mem=8G --cpu-per-task=1 --nodelist=cp3705
   
L'activité du GPU peut être suivi avec une tâches interactive sur le noeud GPU et avec la commande ``nvidia-smi``.
Cette dernière montre alors la mémoire GPU utilisé ainsi que la charge du processeur pour chacun des deux GPU du serveur ``cp3705``.

En revanche, comme les GPUs ne sont pas connus de l'ordonnanceur, il peut parfois être nécessaire de spécifier aux programmes exécutés quel GPU utiliser.
Par exemple, lors de l'entrainement de réseau de neuronne avec PyTorch, la méthode ``.to(device)`` permettant de spécifier quel processeur utilisé (CPU ou GPU) peut être appelé soit avec ``device='cpu'``, pour le CPU, ``device='cuda'`` pour un GPU, ``device='cuda:0'`` pour le GPU 0 ou ``device='cuda:1'`` pour le GPU 1 explicitement.
