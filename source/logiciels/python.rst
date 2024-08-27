Python
======

L’informations ci-dessous est complémentaire à la documentation technique de
l’Alliance sur `Python <https://docs.alliancecan.ca/wiki/Python/fr>`_. 

Modules
-------

Pour voir les modules Python disponibles et en charger un :

.. code-block:: console

    [alice@ip09 ~]$ module spider python

    --------------------------------------------------------------------------------------
      python:
    --------------------------------------------------------------------------------------
        Description:
          Python is a programming language that lets you work more quickly and integrate
          your systems more effectively.

         Versions:
            python/2.7.18
            python/3.6.10
            python/3.7.7
            python/3.7.9
            python/3.8.2
            python/3.8.10
            python/3.9.6
            python/3.10.2
            python/3.10.13
            python/3.11.2
            python/3.11.5
            python/3.12.4
    ...

    [alice@ip09 ~]$ module spider python/3.10.2

    --------------------------------------------------------------------------------------
      python: python/3.10.2
    --------------------------------------------------------------------------------------
        Description:
          Python is a programming language that lets you work more quickly and integrate
          your systems more effectively.

        Propriétés:
          Tools for development / Outils de développement

        Vous devrez charger tous les modules de l'un des lignes suivantes avant de pouvoir
        charger le module "python/3.10.2".

          StdEnv/2020
    ...

    [alice@ip09 ~]$ module load python/3.10.2

En plus de modules de base pour Python lui-même, les logiciels de l’Alliance
contiennent ``scipy-stack``, un module pour `Scientific Python` fournissant
``scipy`` lui-même mais aussi ``numpy``, ``pandas``, ``matplotlib``, etc. Une
fois votre module de base pour Python lui-même chargé :

.. code-block:: console

    [alice@ip09 ~]$ module avail scipy-stack

    ------------------------------------- Core Modules --------------------------------------
       scipy-stack/2020a (math)    scipy-stack/2021a (math)    scipy-stack/2023a (math)
       scipy-stack/2020b (math)    scipy-stack/2022a (math)    scipy-stack/2023b (L,math,D)
    ...

    [alice@ip09 ~]$ module load scipy-stack/2023b

Environnements virtuels
-----------------------

Tel qu’expliqué dans la section suivante, les paquets Python (autres que
`Scientific Python`) peuvent être installés avec la commande ``pip``, en les
téléchargeant de PyPI ou en les choisissant parmis les paquets précompilés par
l’équipe des logiciels de l’Alliance. Toutefois, nous recommandons de ne jamais
installer de paquets Python sans d’abord activer un environnement virtuel.

Les environnements virtuels Python sont des répertoires contenant un ensemble de
paquets installés pour une tâche donnée. Par exemple, vous pourriez avoir un
environnement virtuel pour simuler des systèmes quantiques avec QuTiP et un
autre pour l’apprentissage machine avec TensorFlow. Vous pourriez même avoir
plusieurs environnements virtuels pour différentes versions de QuTiP ou
TensorFlow au gré de vos projets.

En utilisant systématiquement un environnement virtuel pour vos tâches Python,
vous faciliterez l’installation de vos logiciels, le déboguage de vos calculs et
la reproducibilité de votre recherche. À l’inverse, si vous installez tous vos
paquets Python dans l’emplacement par défaut sans discernement, vous ferez face
à plus de problèmes de compatibilité et l’installation ou la mise à jour d’un
paquet pourrait boguer une tâche qui fonctionnait précédemment. De plus, vous ne
pourrez pas alterner entre différentes versions d’un paquet. Finalement, il sera
plus difficile de ré-exécuter une tâche sur un autre ordinateur ou de fournir
des instructions pour reproduire votre environnement logiciel et, donc, votre
recherche.

Pour suivre cette longue explication, voici une courte démonstration. D’abord,
chargeons les modules pour Python et `Scientific Python` :

.. code-block:: console

    [alice@ip09 ~]$ module load python/3.10.2
    [alice@ip09 ~]$ module load scipy-stack/2023b

Ensuite, créons un environnement virtuel :

.. code-block:: console

    [alice@ip09 ~]$ virtualenv $HOME/venv/qutip

Activons l’environnement :

.. code-block:: console

    [alice@ip09 ~]$ source $HOME/venv/qutip/bin/activate

Vous remarquerez que l’invite de commande change pour indiquer l’environnement
virtuel actif. Toutes les actions de la commande ``pip`` (installer,
désinstaller, mettre à jour des paquets) cibleront désormais le répertoire
``$HOME/venv/qutip``. La première chose à faire est de mettre à jour ``pip`` :

.. code-block:: console

    (qutip) [alice@ip09 ~]$ pip install --no-index --upgrade pip    

Ensuite, nous pouvons installer des paquets, par exemple QuTiP :

.. code-block:: console

    (qutip) [alice@ip09 ~]$ pip install --no-index 'qutip==4.7.2'

Finalement, l’environnement peut être désactivé :

.. code-block:: console

    (qutip) [alice@ip09 ~]$ deactivate

Une fois l’environnement créé, il peut être réutilisé simplement en l’activant à
nouveau ; nul besoin de réinstaller les paquets. Par exemple, l’environnement
construit ci-dessus peut être utilisé dans un script de tâche avec :

.. code-block:: bash

   module purge
   module load python/3.10.2
   module load scipy-stack/2023b
   source $HOME/venv/qutip/bin/activate

Paquets Python précompilés
--------------------------

La commande ``avail_wheels`` liste les paquets logiciels Python précompilés par
l’équipe des logiciels de l’Alliance. Ces paquets sont optimisés pour le CHP.
Par exemple, pour chercher Qiskit:

.. code-block:: console

    [alice@ip09 ~]$ avail_wheels qiskit
    name    version    python    arch
    ------  ---------  --------  -------
    qiskit  0.39.3     py3       generic

Pour installer cette version pré-compilée dans un environnement virtuel actif :


.. code-block:: console

    (qiskit) [alice@ip09 ~]$ pip install --no-index 'qiskit==0.39.3'

La commande précédente ne cherche que dans l'environnement logiciel chargé (par
défaut ``StdEnv/2020``). Des versions plus récentes de certains paquets sont
disponibles dans les environnements plus récents :

.. code-block:: console

    [alice@ip09 ~]$ module load StdEnv/2020 && avail_wheels pyqcm --all
    name    version    python    arch
    ------  ---------  --------  ------
    pyqcm   2.3.1      cp39      avx2
    pyqcm   2.3.1      cp311     avx2
    pyqcm   2.3.1      cp310     avx2
    
    [alice@ip09 ~]$ module load StdEnv/2023 && avail_wheels pyqcm --all
    
    The following have been reloaded with a version change:
      1) StdEnv/2020 => StdEnv/2023          3) gentoo/2020 => gentoo/2023           5) libfabric/1.10.1 => libfabric/1.18.0     7) ucx/1.8.0 => ucx/1.14.1
      2) gcccore/.9.3.0 => gcccore/.12.3     4) imkl/2020.1.217 => imkl/2023.2.0     6) openmpi/4.0.3 => openmpi/4.1.5

    name    version    python    arch
    ------  ---------  --------  ---------
    pyqcm   2.4.3      cp311     x86-64-v3
    pyqcm   2.4.3      cp310     x86-64-v3


Parallélisation avec Python
---------------------------

Le code Python n’est pas typiquement parallélisé. Par conséquent, demander
plusieurs cœurs CPU n’accélérera pas vos tâches automatiquement ! Vous devez
d’abord paralléliser votre code, soit explicitement, soit en utilisant des
fonctions parallélisées d’une bibliothèque, comme certaines fonctions de NumPy
ou SciPy.

À cause d’une limitation intrinsèque, le « global interpreter lock », le code
Python ne peut être parallélisé avec le modèle de mémoire partagée. Il existe
toutefois des alternatives. L’une d’elles est de coder une extension Python en
C/C++ en utilisant une bibliothèque de programmation parallèle telle qu’OpenMP.
Une autre est d’utiliser le modèle de mémoire distribué avec de multiple
processus Python. Pour ce faire, vous pouvez utiliser le module
``multiprocessing``, ou encore une bibliothèque telle que `mpi4py
<https://mpi4py.readthedocs.io/en/stable/>`_ (passage de messages) ou `Dask
<https://www.dask.org/>`_ (parallélisme des données).

.. _python-fils-label:

Sur-souscription de fils
''''''''''''''''''''''''

Un problème commun avec le parallélisme dans Python est la sur-souscription de
fils d’éxécution (« thread oversubscription »), c’est-à-dire que le nombre de
fils d’exécution lancés dans une tâche est supérieur au nombre de cœurs CPU
alloués à la tâche. Le module ``multiprocessing``, en particulier, lance par
défaut autant de fils d’exécution qu’il y a de cœurs CPU, sans considérer si les
cœurs sont tous accessibles. Par exemple, ``multiprocessing`` lancera par défaut
64 fils d’exécution si vous l’utilisez dans une tâche sur un nœud CPU de la
plateforme CHP-IQ, même si n’avez demandé que 2, 4 ou 8 cœurs.

Ce problème est aggravé si l’on utilise aussi une fonction parallélisée qui
lance par défaut fils qu’il y a de cœurs (telle que
``scipy.sparse.linalg.eigsh``). Si l’on poursuit l’exemple ci-haut, dans une
tâche qui utilise à la fois ``multiprocessing`` et ``eigsh``, 4096 fils
d’exécution (64 × 64) seront lancés par défaut, même si la tâche n’a accès qu’à
2, 4 ou 8 cœurs. La performance sera drastiquement réduite.

Pour palier à ce problème, vous devez spécifier à ``multiprocessing``, Dask,
SciPy, etc. le nombre de fils d’exécution à utiliser. La bibliothèque Python
`ThreadPoolCtl <https://pypi.org/project/threadpoolctl/>`_ peut être utile à cet
effet.

.. seealso::

   - :ref:`Cette entrée <calcul-lent-label>` de notre FAQ discute les problèmes
     de performance et de fils d’exécution de manière plus générale.
