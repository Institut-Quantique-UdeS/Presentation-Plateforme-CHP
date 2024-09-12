Mathematica
===========

Mathematica est un logiciel commercial pour le calcul formel et numérique
développé par Wolfram Research.

License
-------

Les licences Mathematica sont distribuées par un serveur du département de
physique. Aucune configuration n’est requise mais chaque utilisateur est
responsable de se renseigner quant aux politiques d’accès à ces licences.

Utilisation
-----------

Pour voir les versions de Mathematica disponibles :

.. code-block:: console

    [alice@ip09 ~]$ ls /net/nfs-iq/data/software/Mathematica/
    12.1  14.0

Pour ajouter Mathematica à votre environnement interactif :

.. code-block:: console

    [alice@ip09 ~]$ PATH="$PATH:/net/nfs-iq/data/software/Mathematica/12.1/Executables"

Pour utiliser Mathematica dans un script de tâche :

.. code-block:: bash
    
    #!/bin/bash
    #SBATCH --time=02:00:00
    #SBATCH --cpus-per-task=2
    #SBATCH --mem=8G
    
    PATH="$PATH:/net/nfs-iq/data/software/Mathematica/12.1/Executables"

    wolframscript -file script.wls
