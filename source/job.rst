.. jobs

Lancement de tâches de calcul sur les serveurs
----------------------------------------------

Les serveurs de calcul peuvent être utilisés de deux manières différentes qui correspondent à deux types de tâches distinctes:

* Les tâches dites interactives où les usagers sont redirigées sur les noeuds de calcul.

* Les tâches dites en batch où l'usager soumet la tâche à un ordonnanceur qui est responsable de l'exécution de la tâche sur les noeuds de calcul.

Dans tout les cas, il est interdit de lancer des tâches sur les noeuds de connexion.
En plus de pénaliser les autres utilisateurs qui font de la gestion de fichiers, ces noeuds ne disposent pas des derniers logiciels disponibles dans la pile de l'Alliance et offrent de mauvaises performances.


Tâches interactives
===================

Tâches courte pour la réalisation de tests, l'exploration de donnée ou la compilation de code.
Requiert l'action d'un humain.
Généralement courtes (moins de 4 heures)


Tâches en batch
===============

Toutes tâches qui ne nécessite pas l'action d'un humain (lancement d'un script Python par exemle).
Doit être la façon priviligié d'utiliser les serveurs de calcul car elle maximise l'efficacité.


Calcul sur GPU
==============

Les tâches de calcul faisans l'utilisation de GPU ne sont pas différente des tâches CPU et peuvent être de type interactive ou en batch.

Accès au serveur GPU de l'IQ en spécifiant explicitement le nom du noeud ``cp3705`` à l'ordonnanceur, exemple: ``sbatch mon_script_gpu.sh --nodelist=cp3705``.
