.. faq

Foire aux questions
===================

Problèmes fréquents
-------------------

« Illegal instruction » (``SIGILL``)
''''''''''''''''''''''''''''''''

Votre tâche cause une erreur de type « Illegal instruction » ou ``SIGILL``, par
example:

.. code-block:: console

   [alice@ip09 ~]$ cat slurm-3304643.out 
   /var/spool/slurmd/job3304643/slurm_script: line 11: 25047 Illegal instruction   (core dumped) python my_script.py

Cette erreur se produit lorsqu’un programme optimisé pour une classe de
processeurs particuliers est exécuté sur un processeur qui n’est pas compatible.

Vérifiez d’abord si vous avez bien soumis votre tâche aux nœuds de calcul de la
plateforme CHP-IQ avec l’option ``--partition=c-iq``. Sinon, votre tâche sera
exécutée sur les nœuds réguliers de la grappe MP2, dont les processeurs sont
plus anciens et potentiellement incompatibles avec le code compilé sur ``ip09``.

Si vous compilez votre code sur ``ip09`` avec GCC, utilisez l’option
d’optimisation ``-march=core-avx2``. Si vous utilisez les compilateurs Intel,
l’option correspondante est ``-xCORE-AVX2``. N’utilisez pas ``-march=native`` ou
``-xHost``. Ces dernières tentent d’optimiser pour les processeurs Intel
d’``ip09``. Le programme résultant peut être incompatible avec les processeurs
AMD des nœuds de calcul.

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

