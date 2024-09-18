Mathematica
===========

Mathematica is a commercial software package for symbolic and numeric algebra
developed by Wolfram Research.

License
-------

Mathematica licenses are distributed by a server in the Physics Department. No
configuration is required but each user is responsible for respecting access
policies.

Usage
-----------

To list available Mathematica versions:

.. code-block:: console

    [alice@ip09 ~]$ ls /net/nfs-iq/data/software/Mathematica/
    12.1  14.0

To add Mathematica to your interactive environment:

.. code-block:: console

    [alice@ip09 ~]$ PATH="$PATH:/net/nfs-iq/data/software/Mathematica/12.1/Executables"

To use Mathematica in a job script:

.. code-block:: bash
    
    #!/bin/bash
    #SBATCH --time=02:00:00
    #SBATCH --cpus-per-task=2
    #SBATCH --mem=8G
    
    PATH="$PATH:/net/nfs-iq/data/software/Mathematica/12.1/Executables"

    wolframscript -file script.wls
