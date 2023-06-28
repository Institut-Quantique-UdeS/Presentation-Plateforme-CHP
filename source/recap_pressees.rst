.. _Recap_personnes_pressees:

Récapitulatif et importants conseils pour les personnes préssées
----------------------------------------------------------------

* La plateforme de calcul haute perfomance de l'IQ a été concue pour avoir la même expérience que les grappes nationnales. La présente documentation ainsi que `celle de l'Alliance <https://docs.alliancecan.ca>`_ s'applique donc sur la plateforme.

* L'accès aux serveurs se fait par SSH, nom du noeud de connexion ``ip09.ccs.usherbrooke.ca``.

* La plateforme est branchée à la grappe nationnale MP2, et les serveurs de l'IQ sont accessibles sur une partition spéciale ``c-iq`` de MP2. Toutes les ressources de MP2 peuvent être atteintes, par exemple les partitions ``c-apc``, ``c-aphex``, ``c-royer``, ...

* Les serveurs de l'IQ (partition ``c-iq``) sont accessibles uniquement aux membres de l'IQ. Il est obligatoire de spécifier la partition pour utiliser les serveurs de l'IQ, sinon, la tâche sera soumise aux noeuds réguliers de MP2. Exemple pour soumettre une tâche: ``sbatch -p c-iq job.sh [job_argument]``.

* Il est recommandé de travailler sur le serveur de données dédié de l'IQ pour de meilleures performances en entrée-sortie de fichier. Le serveur de donnée de l'IQ est accessible à ``/net/nfs-iq/data/[username]``. Espace partagé à ``/net/nfs-iq/data/def-[sponsor]``. Capacité de 180 To (stockage redondant).

* L'espace ``/scratch`` de MP2 est non accessible depuis les calculateurs de l'IQ.

* Accès au serveur GPU de l'IQ en spécifiant explicitement le nom du noeud ``cp3705`` à l'ordonnanceur, exemple: ``sbatch -p c-iq --nodelist=cp3705 mon_script_gpu.sh``. Note: les GPUs ne sont pas définis dans SLURM, les GPUs doivent être spécifiée dans la tâche. Par exemple, pour PyTorch, utiliser la méthode ``.to("cuda:0")`` ou ``.to("cuda:1")`` pour le GPU 0 ou 1 respectivement.
