.. _Recap_personnes_pressees:

Récapitulatif et importants conseils pour les personnes préssées
----------------------------------------------------------------

* Serveurs de l'IQ branchés sur la grappe MP2 (``ssh [utilisateur]@mp2.computecanada.ca``), même environnement que sur les grappes nationales de l'Alliance (anciennement Calcul Canada).

* Serveur de l'IQ accessible uniquement aux membres de l'IQ via et configuré sur une partition spéciale ``c-iq``. Exemple pour soumettre une tâche: ``sbatch -p c-iq job.sh``.

* Certains logiciels et librairies (incluant Python) ne sont pas visibles et ne peuvent être chargés sur les neouds de connexion (différente architecture que les grappes nationales). Une allocation (``salloc``) sur les noeuds de l'IQ résout le problème.

* Création d'environnements virtuels et compilation de logiciels à faire directement sur les serveurs de l'IQ en mode interactif (optimisation pour l'architecture des serveurs IQ).

* Accès au serveur GPU de l'IQ en spécifiant explicitement le nom du noeud ``cp3705`` à l'ordonnanceur, exemple: ``sbatch mon_script_gpu.sh --node-list=cp3705``.
