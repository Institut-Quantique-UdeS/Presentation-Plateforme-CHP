.. _Recap_personnes_pressees:

Récapitulatif et importants conseils pour les personnes préssées
----------------------------------------------------------------

* Les serveurs de l'IQ sont actuellement branchés sur la grappe MP2. L'accès aux serveurs se fait donc via MP2 et par SSH (``ssh [utilisateur]@mp2.computecanada.ca``).

* Les serveurs de l'IQ accessible uniquement aux membres de l'IQ et configuré sur une partition spéciale ``c-iq`` de MP2. Il est obligatoire de spécifier la partition pour utiliser les serveurs de l'IQ, sinon, la tâche sera soumise aux noeuds réguliers de MP2. Exemple pour soumettre une tâche: ``sbatch -p c-iq job.sh``.

* L'environnement standard de MP2 sur lequel les serveurs de l'IQ sont connectés est ``nixpkgs/16.09`` qui n'est plus maintenu. Il est donc nécessaire de charger le dernier environnement standard ``module load StdEnv/2020`` dans le script lors de la soumission d'une tâche de calcul sur les serveurs de l'IQ, ou à l'arriver sur les serveurs de l'IQ lors d'une tâche interactive.

* Les noeuds de connexion de MP2 possède une architecture différente que celle des serveurs de l'IQ. En conséquence, pour de meilleurs performances et une meilleure expérience utilisateur, la création d'environnements virtuels et la compilation de logiciels doit à faire directement sur les serveurs de l'IQ, par exemple via une allocation interactive (``salloc``).

* À cause des deux dernières différences entre les noeuds de MP2 et les serveurs de l'IQ, certains logiciels et librairies (incluant Python) peuvent ne pas être visibles ni chargés sur les noeuds de connexion de MP2 . Une allocation (``salloc -t 01:00:00 --mem 8G --cpus-per-task=1``) sur les noeuds de l'IQ résout le problème.

* L'espace ``/scratch`` de MP2 est non accessible depuis les calculateurs de l'IQ.

* Les serveurs de l'IQ sont dottés d'un serveurs de données dédié de 384 To présent à ``/net/nfs-iq/data/[username]``. Espace partagé à ``/net/nfs-iq/data/def-[sponsor]``.

* Accès au serveur GPU de l'IQ en spécifiant explicitement le nom du noeud ``cp3705`` à l'ordonnanceur, exemple: ``sbatch mon_script_gpu.sh --nodelist=cp3705``.
