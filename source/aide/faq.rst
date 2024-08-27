.. faq

Foire aux questions (FAQ)
=========================

Problèmes fréquents
-------------------

Un fichier est introuvable dans une tâche
'''''''''''''''''''''''''''''''''''''''''

Vous avez soumis un script de tâche qui ne trouve pas un ou plusieurs fichiers
de votre répertoire personnel ? Vous avez démarré une tâche interactive mais
vous ne voyez pas les fichiers dans votre répertoire personnel ?

C’est « normal ». Votre répertoire personnel sur les nœuds de calcul est celui
de la grappe MP2, pas celui de la plateforme CHP-IQ, sauf si votre compte
utilisateur a été créé récemment. Les fichiers que vous placez dans votre
répertoire personnel lorsque vous êtes connecté à ``ip09`` ne sont donc pas
accessibles à partir de vos tâches.

Il y a deux solutions. La première est de déplacer vos fichiers vers
``/net/nfs-iq/data``. Cet emplacement devrait de toute façon être utilisé pour
toutes les données de recherche puisqu’il offre une meilleure performance. La
deuxième est de changer votre répertoire personnel accessible à partir des nœuds
de calcul pour utiliser celui de la plateforme CHP-IQ plutôt que celui de MP2.
:doc:`Contactez-nous <support>` et nous ferons le changement.

« Illegal instruction » (``SIGILL``)
''''''''''''''''''''''''''''''''''''

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

Mon calcul est beaucoup plus lent que sur mon portable
''''''''''''''''''''''''''''''''''''''''''''''''''''''

Vous avez testé un programme parallèle sur votre portable (ou un autre
ordinateur). Ce programme fonctionne aussi dans une tâche sur la plateforme
CHP-IQ mais il est beaucoup plus lent. Que se passe-t-il ?

D’abord, assurez-vous d’utiliser le même nombre de cœurs CPU sur votre portable
et dans votre tâche pour que la comparaison soit valide. Par exemple, si votre
portable a 8 cœurs CPU et que votre programme les utilise tous, vous devriez
aussi demander 8 cœurs CPU dans votre tâche. Si vous demandez moins de cœurs,
voire un seul, il est normal que la performance soit moindre !

Si le problème persiste, vérifiez que votre tâche :ref:`utilise correctement les
ressources <tâches-actives-label>` qui lui sont allouées. Un problème commun est
un programme parallèle qui tente d’utiliser tous les cœurs CPU du nœud de calcul
même s’il ne sont pas tous alloués à la tâche. Par exemple, un programme
pourrait lancer 96 fils d’exécution pour tenter d’utiliser les 96 cœurs d’un
nœud CPU de la partition ``c-iq`` même si la tâche n’a accès qu’à un seul de ces
cœurs. Le système d’exploitation alterne alors entre les 96 fils pour que chacun
reçoive sa part de temps CPU. Cette alternance cause une dégradation importante
de la performance, sans compter les potentiels problèmes de synchronisation
entre les fils.

Dans la plupart des cas, le nombre de cœurs CPU alloués à une tâche devrait
correspondre exactement au nombre de processus ou de fils exécutés par la tâche.
Si une tâche exécute trop de fils ou de processus, ``htop`` montrera plus de
fils d’exécution qu’attendu, et ces fils utiliseront moins de 100 % de temps CPU.

Pour les programmes parallèles qui utilisent des fils d’exécution OpenMP, le
problème peut être corrigé en réglant le nombre de fils à exécuter pour qu’il
soit identique au nombre de cœurs alloués. Ajoutez cette instruction à votre
script de tâche avant l’exécution de votre programme :

.. code-block:: bash

   export OMP_NUM_THREADS=${SLURM_CPUS_PER_TASK:-1}
