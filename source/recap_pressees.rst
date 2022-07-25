.. _Recap_personnes_pressees:

Récapitulatif et importants conseils pour les personnes préssées
----------------------------------------------------------------

* Configuration du matériel de l'IQ de manière à mimer les grappes nationales.

* Serveurs de l'IQ branchés sur la grappe MP2 (``ssh [utilisateur]@mp2.computecanada.ca``), même environnement que sur les grappes nationales de l'Alliance (anciennement Calcul Canada).

* Serveurs de l'IQ accessible uniquement aux membres de l'IQ via et configuré sur une partition spéciale ``c-iq``. Exemple pour soumettre une tâche: ``sbatch -p c-iq job.sh``.

* L'environnement standard sur MP2 est ``nixpkgs/16.09`` qui n'est plus maintenu. Il est donc nécessaire de charger le dernier environnement standard ``StdEnv/2020`` lors de la soumission d'une tâche de calcul sur les serveurs de l'iQ.

* Certains logiciels et librairies (incluant Python) peuvent ne pas être visiblesni chargés sur les noeuds de connexion de MP2 (différente architecture que les grappes nationales). Une allocation (``salloc -t 01:00:00 --mem 8G --cpus-per-task=1``) sur les noeuds de l'IQ résout le problème.

* Création d'environnements virtuels et compilation de logiciels à faire directement sur les serveurs de l'IQ en mode interactif (optimisation pour l'architecture des serveurs IQ).

* Espace ``/scratch`` non accessible depuis les calculateurs.

* Accès à espace de stockage privé sur les serveurs de données de l'IQ (384 To) à ``/net/nfs-iq/data/[username]``. Espace partagé à ``/net/nfs-iq/data/def-[sponsor]``.

* Accès au serveur GPU de l'IQ en spécifiant explicitement le nom du noeud ``cp3705`` à l'ordonnanceur, exemple: ``sbatch mon_script_gpu.sh --nodelist=cp3705``.
