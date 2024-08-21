Mathematica
===========

Mathematica est un logiciel propriétaire de calcul formel et numérique développé par Wolfram Research.
Mathematica version 12.1 est installé sur le NAS de l'IQ et les exécutables se trouvent sous ``/net/nfs-iq/data/software/Mathematica/12.1/Executables``.
Les licences sont distribuées via un serveur de licence en ligne sur le réseau de du département de physique et de l'université de manière transparente.
Néanmoins, il est de la responsabilité de l'usager de se renseigner quant aux politiques d'accès à ces licences (si elles existent)

Exemple d'utilisation de Mathematica en tâche batch:

.. code-block:: bash
    
    #!/bin/bash
    #SBATCH --time=02:00:00
    #SBATCH --cpus-per-task=2
    #SBATCH --mem=8G
    
    /net/nfs-iq/data/software/Mathematica/12.1/Executables/wolframscript -file script.wls
