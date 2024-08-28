.. IQ-Plateforme-CHP documentation master file, created by
   sphinx-quickstart on Sun May 15 20:28:55 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Plateforme de calcul haute performance de l’institut quantique
==============================================================

.. important::

   Les chercheurs pressés devraient au miminum lire cette page ainsi que le
   :doc:`résumé <résumé>` avant de lancer leur première tâche.

   Les chercheurs débutants devraient consulter nos pages sur l’apprentissage de
   :doc:`Linux <apprentissage/linux>` et du :doc:`calcul haute performance
   <apprentissage/chp>`.

La plateforme de calcul haute performance (CHP) de l’`Institut quantique (IQ)
<https://www.usherbrooke.ca/iq/>`_ est une grappe de calcul de petite taille
réservée aux chercheurs de l’IQ et à leurs collaborateurs. Gérée par le `Centre
de calcul scientifique (CCS) <https://www.ccs.usherbrooke.ca/>`_, elle est une
extension de la grappe MP2 (Mammouth parallèle) de l’`Université de Sherbrooke
<https://www.usherbrooke.ca/>`_. En plus de nœuds de calcul et d’un espace de
stockage disponibles pour tous les chercheurs de l’IQ, la plateforme contient
des nœuds contribués par des chercheurs spécifiques et dont l’utilisation est
restreinte. Les chercheurs peuvent utiliser la plateforme sans limite et sans
frais. Les coûts sont assumés grâce à une subvention de la Fondation canadienne
pour l’innovation (FCI). 

La configuration de la plateforme CHP-IQ est similaire à celle des grappes
nationales gérées par l’Alliance de recherche numérique du Canada (auparavant
Calcul Canada) : environnement Linux, logiciels disponibles, commandes pour
lancer et gérer les tâches, etc. La `documentation technique de l’Alliance
<https://docs.alliancecan.ca/wiki/Technical_documentation/fr>`_ s’applique donc
également à la plateforme CHP-IQ et déplacer un calcul d’une grappe à une autre
ne demande qu’un effort minime.

La plateforme CHP-IQ sert de ressource intermédiaire et de tremplin vers les
grappes de calcul plus puissantes de l’Alliance. Lorsqu’une station de travail
individuelle n’est pas suffisante pour exécuter tous vos calculs ou stocker vos
données, la plateforme CHP-IQ vous permet d’augmenter rapidement vos
possibilités. Pour vos projets de recherche computationnelle de plus grande
envergure, voyez le `guide de démarrage
<https://docs.alliancecan.ca/wiki/Getting_started/fr>`_ de l’Alliance.

.. toctree::
   :maxdepth: 2
   :titlesonly:
   :hidden:
   
   compte
   connexion
   stockage
   nœuds
   tâches
   logiciels/index
   résumé
   
.. toctree::
   :caption: Aide
   :maxdepth: 2
   :titlesonly:
   :hidden:

   aide/faq
   aide/support

.. toctree::
   :caption: Apprentissage
   :maxdepth: 2
   :titlesonly:
   :hidden:

   apprentissage/linux
   apprentissage/chp

.. toctree::
   :caption: Liens externes
   :hidden:

   Documentation technique de l’Alliance <https://docs.alliancecan.ca/wiki/Technical_documentation/fr>
   Formations de Calcul Québec <https://www.calculquebec.ca/services-aux-chercheurs/formation/>
   Portail CCDB <https://ccdb.alliancecan.ca/>

.. toctree::
   :caption: À réorganiser
   :maxdepth: 2
   :titlesonly:
   :hidden:

.. note::

   Cette documentation est gérée par le CCS. Son auteur original est Moïse
   Rousseau, son responsable actuel Olivier Fisette. Pour toute question ou
   commentaire ou pour rapporter une erreur ou un problème, consultez notre
   :doc:`support technique <aide/support>`.
