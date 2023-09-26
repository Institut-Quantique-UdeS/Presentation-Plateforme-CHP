.. jobs

Lancement de tâches de calcul sur les serveurs
----------------------------------------------

Cette page est un complément d'information de la page de l'Alliance dédiée: `Exécuter des tâches <https://docs.alliancecan.ca/wiki/Running_jobs/fr>`_.

Les serveurs de calcul peuvent être utilisés de deux manières différentes qui correspondent à deux types de tâches distinctes:

* Les tâches dites interactives où les usagers sont redirigées sur les noeuds de calcul.

* Les tâches dites en batch où l'usager soumet la tâche à un ordonnanceur qui est responsable de l'exécution de la tâche sur les noeuds de calcul.

Dans tout les cas, il est interdit de lancer des tâches sur les noeuds de connexion.
Aussi, pour des calculs sur les serveur de l'IQ, il est recommandé d'enregistrer les données et de soumettre les tâches depuis le NAS de l'IQ qui possède de meilleures performances en entrée-sortie de données, c'est-à-dire depuis ``/net/nfs-iq/data/[nom_utilisateur]`` (voir aussi :ref:`stockage_et_reseau`).


.. _taches_batch:

Tâches en batch
===============

Les tâches en batch désignent toutes tâches qui ne nécessite pas l'action de l'usager pendant les calculs (lancement d'un script Python par exemple).
Les tâches en batch maximise l'efficacité des serveurs de calcul et elle doit donc être la façon priviligiée d'utiliser la plateforme de calcul de l'IQ.
Les scripts bash pour le lancement des tâches sont exactement les mêmes que les scripts utilisés pour soumettre sur les autres grappes nationales de l'Alliance (voir la page `Exécuter des tâches <https://docs.alliancecan.ca/wiki/Running_jobs/fr>`_).
La soumission se fait ensuite en précisant la partition des noeuds de l'IQ avec l'option ``-p c-iq`` à l'ordonnanceur:

.. code-block:: bash

   sbatch -p c-iq job.sh



.. _taches_interactives:

Tâches interactives
===================

Les tâches interactives sont des tâches généralement courtes (moins de 4 heures) qui requiert l'action soutenue de l'usager, comme la réalisation de tests, l'exploration de données, le débogage ou la compilation de codes.
La commande ``salloc`` suivie de l'option ``-p c-iq`` permet d'être redirigé sur un noeuds de calcul de l'IQ avec 1 CPU et 8 Go de mémoire vive:

.. code-block:: bash

   salloc -p c-iq -t [HH]::[mm]:[ss] --mem=8G --cpu-per-task=1



Calcul sur GPU
==============

Les tâches de calcul faisans l'utilisation de GPU ne sont pas différente des tâches CPU et peuvent être de type interactive ou en batch.

Au contraire des grappes nationales, les GPU ne sont pas connus de l'ordonnanceur et il faut donc spécifier explicitement le nom du serveur GPU (``cp3705``) de l'IQ à ce dernier avec l'option ``--nodelist=cp3705``.

Par exemple, pour soumettre une tâche batch ou interactive avec accès aux GPU, les commandes sont la suivante:

.. code-block:: bash

   sbatch -p c-iq --nodelist=cp3705  job.sh #batch job
   salloc -p c-iq --nodelist=cp3705 -t [HH]::[mm]:[ss] --mem=8G --cpu-per-task=1 #interactive job
   
L'activité du GPU peut être suivi avec une tâches interactive sur le noeud GPU et avec la commande ``nvidia-smi``.
Cette dernière montre alors la mémoire GPU utilisé ainsi que la charge du processeur pour chacun des deux GPU du serveur ``cp3705``.

En revanche, comme les GPUs ne sont pas connus de l'ordonnanceur, il peut parfois être nécessaire de spécifier aux programmes exécutés quel GPU utiliser.
Par exemple, lors de l'entrainement de réseau de neuronne avec PyTorch, la méthode ``.to(device)`` permettant de spécifier quel processeur utilisé (CPU ou GPU) peut être appelé soit avec ``device='cpu'``, pour le CPU, ``device='cuda'`` pour un GPU, ``device='cuda:0'`` pour le GPU 0 ou ``device='cuda:1'`` pour le GPU 1 explicitement.
La variable d'environnement ``CUDA_VISIBLE_DEVICES`` permet aussi de sélectionner explicitement quels GPUs utiliser, par exemple ``CUDA_VISIBLE_DEVICES=0`` pour le GPU 0 ou ``CUDA_VISIBLE_DEVICES=0,1`` pour les deux GPUs.


Efficacité d'une tâche de calcul
================================

La commande ``seff`` permet d'obtenir des statistiques sur l'efficacité des calculs effectués.
Il est recommandé à la fin de chaque tâche que les ressources demandées ont correctement été utilisées afin de prévenir le gaspillage de ressource.
Il est recommandé une efficacité CPU supérieure à 90% et une efficacité mémoire supérieure à 70%, avec un seuil minimum acceptable à 70% pour les CPUs et 50% pour la mémoire.
Si les tâches soumises sont en général en-dessous de ces seuils, merci de revoir la demande de ressources basée sur les résultats précédents.

La commande ``seff`` est à utiliser à partir de MP2 (elle n'est pas disponible sur ip09):

.. code-block:: bash

   ssh [utilisateur]@mp2.computecanada.ca
   seff [JobID]

Qui retourne le résultat suivant pour la tâche 1668335:

.. code-block:: bash

    [moroub@ip16-mp2 ~]$ seff 1668335
    Job ID: 1668335
    Cluster: mp2
    User/Group: anaida/anaida
    State: COMPLETED (exit code 0)
    Cores: 1
    CPU Utilized: 1-17:38:24
    CPU Efficiency: 99.64% of 1-17:47:32 core-walltime
    Job Wall-clock time: 1-17:47:32
    Memory Utilized: 9.42 GB
    Memory Efficiency: 12.06% of 78.12 GB

L'efficacité des tâches est publique.



Alias pour les commandes SLURM communes
=======================================

Pour éviter de nommer la partition de l'IQ à chaque soumission de scripts ou de tâches interactives, les usagers peuvent définir un alias de commandes spéciales pour les serveurs de l'IQ:

.. code-block:: bash

   alias sbatch-iq="sbatch -p c-iq"
   alias salloc-iq="salloc -p c-iq"
   alias sbatch-iq-gpu="sbatch -p c-iq --nodelist=cp3705"
   alias salloc-iq-gpu="salloc -p c-iq --nodelist=cp3705"

Ces trois commandes sont à ajouter à la fin du fichier ``~/.bash_profile``.
Ainsi, la soumission d'un script batch pour le serveur GPU de l'IQ s'écrit simplement:

.. code-block:: bash

   sbatch-iq-gpu job.sh


