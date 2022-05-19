.. mise_en_route

Connection à la plateforme
--------------------------

La connection à la plateforme se fait via un terminal et en utilisant le protocole SSH.


Mise en route
=============

.. _Mise_en_route_windows:

Windows
#######

MobaXterm / Recommander WSL


MacOS et Linux
##############

Aucune mise en route nécessaire. 
La connection se fait par le terminal.


Connection
==========

Les ressources CHP de l'IQ sont hebergés aux Centre de Calcul Scientifique de l'Université de Sherbrooke, et sont actuellement branchées sur la grappe nationale Mammouth Parallèle 2 (abrégée MP2).
Leur accès requiert un compte Calcul Canada Database (CCDB) ainsi que la signature d'un entente d'utilisation (voir XX).
Une fois l'accès garanti, la connection se fait via un terminal (MacOS et Linux, voir rubrique :ref:`Mise_en_route_windows` ci-dessus le cas échéant) et le protocole SSH:

.. code-block::

   ssh <nom_utilisateur_CCDB>@mp2.computecanada.ca


Utilisation
===========

Les usagers arrivent alors sur les noeuds de connection de la grappe MP2 et y naviguent par la ligne de commandes.
Pour les usagers peu familier de la ligne de commande, il est possible de suivre l'autoformation d'introduction de Software Carpentry (disponible `ici <https://swcarpentry.github.io/shell-novice/>`_), ou la formation de Calcul Québec (voir la page `EventBrite dédiée <https://www.eventbrite.ca/o/calcul-quebec-8295332683>`_).




