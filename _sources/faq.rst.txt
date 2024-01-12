.. faq

Problèmes courants
------------------

Erreur Illegal instruction
==========================

Votre tâche en batch ou interactive vous retourne une erreur de type ``Illegal instruction``, par example:

.. code-block:: bash

   [moroub@ip09 ~]$ cat slurm-3304643.out 
   /var/spool/slurmd/job3304643/slurm_script: line 11: 25047 Illegal instruction   (core dumped) python my_script.py

Cette erreur est causée par une instruction plus récente dans votre programme qui n'est pas supportée sur le processeur utilisé plus ancien.
Vérifiez que vous avez bien soumis la tâche sur les serveurs de l'IQ avec l'option ``-p c-iq`` placé avant le nom du script de soumission (voir _taches_batch).
Aussi, si vous avez compiler un programme vous-même, tentez de recompiler le programme directement sur les noeud de l'IQ ou remplacer l'option de compilation ``-march=native`` par ``-march=core-avx2`` (GCC) ou ``-xHost`` par ``-xCORE-AVX2`` (compilateur Intel).


Erreur fichier introuvable mais bien présent
============================================

Vous avez soumis une tâche en batch ou interactive mais celle-ci n'arrive pas à trouver vos données.
Si vous vous connectez sur le noeud d'interconnexion de l'IQ ``ip09`` (comment le savoir: votre terminal indique ``[nom_utilisateur@ip09 ~]$`` devant les commandes que vous entrez), vos données se trouvent probablement dans votre ``$HOME`` qui n'est pas accessible par les serveurs de l'IQ.
Déplacez toutes vos données depuis votre ``$HOME`` vers ``/net/nfs-iq/data/$USER``.


Mes calculs sont beaucoup plus lents que sur mon laptop
=======================================================

Vous avez testé votre code avec succès sur votre laptop mais les calculs sur les serveurs sont beaucoup plus lents (c'est à dire au moins 10x plus lent) que sur votre laptop.
Assurez-vous tout d'abord de comparer ce qui est comparable, c'est-à-dire utiliser le même nombre de CPUs sur les serveurs que sur votre laptop.
Ensuite, assurez-vous d'utiliser le bon nombre de CPUs sur les serveurs en définissant la variable d'environnement ``OMP_NUM_THREADS`` dans votre script de soumission:

.. code-block:: bash

   export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK

En effet, sans cette variable, votre tâche pourrait prendre tout les CPUs des serveurs de l'IQ (48 ou 96) et non pas le nombre défini dans le script de tâche (voir `Tâche multifil ou tâche OpenMP <https://docs.alliancecan.ca/wiki/Running_jobs/fr#T%C3%A2che_multifil_ou_t%C3%A2che_OpenMP>`_ sur la documentation de l'Alliance), soit beaucoup plus que disponible et causant de mauvaise performance.

