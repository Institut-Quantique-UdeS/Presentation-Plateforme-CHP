Résumé
======

**Compte**
    Utilisez votre nom d’utilisateur et votre mot de passe `CCDB
    <https://ccdb.alliancecan.ca/>`_.

**Nœud de connexion**
    SSH: ``ip09.ccs.usherbrooke.ca``

**Répertoire personnel**
    - Emplacement : ``/home/$USER``
    - Ne pas utiliser pour les données de recherche (mauvaise performance
      entrée-sortie)

**Données de recherche**
    - Emplacement : ``/net/nfs-iq/data``
    - À utiliser pour les tâches (bonne performance entrée-sortie)
    - Capacité totale : 190T
    - Stockage redondant
    - Données individuelles : ``/net/nfs-iq/data/$USER``
    - Données des groupes : ``/net/nfs-iq/data/def-$PARRAIN``

**Nœuds de calcul publics**
    .. include:: nœuds/public.rst

**Accès à MP2**
    Les stockages ``/project`` et ``/scratch`` de MP2 ne sont pas accessibles.

**Accès à partir de MP2**
    Le stockage des données de recherche de la plateforme CHP-IQ est accessible
    à partir de MP2 à ``/net/nfs-iq/data``.

**Logiciels de l’Alliance**
    - Commande ``module`` pour les paquets logiciels
    - Commande ``avail_wheels`` pour les paquets Python
    - Environnement par défaut : ``StdEnv/2023``
    - Cible d’optimisation par défaut : AVX2
    - Bibliothèques BLAS/LAPACK par défaut : Intel MKL
