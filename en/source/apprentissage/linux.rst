Linux command line
==================

The IQ HPC Platform, Alliance clusters, and all supercomputers in the TOP500 use
the Linux operating system. You need basic knowledge of the Linux/UNIX command
line to use almost any high performance computing system.

If you are not already familiar with Linux or if you wish to refresh your
memory, we highly recommend the `Calcul Québec training
<https://www.calculquebec.ca/en/academic-research-services/training/>`_. If no
training is available soon, feel free to contact our :doc:`technical support
<../aide/support>` for custom local training. Finally, the Alliance technical
documentation offers a short `Linux introduction
<https://docs.alliancecan.ca/wiki/Linux_introduction/fr>`_.

Linux quick reference
---------------------

Moving around
'''''''''''''

Basic commands to navigate the file system are shown in this table:

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Command
     - Description
   * - ``pwd``
     - Give the absolute path of the current working directory
   * - ``ls``
     - List files and directories
   * - ``cd <dir>``
     - Go to directory ``<dir>``
   * - ``mv <orig> <dest>``
     - Move or rename the ``<orig>`` file or directory to ``<dest>``
   * - ``cp <orig> <dest>``
     - Copy the ``<orig>`` file to ``<dest>``
   * - ``cp -r <orig> <dest>``
     - Copy the ``<orig>`` directory and its contents to ``<dest>``
   * - ``rm <file>``
     - Delete a file (be careful! this is definitive, there is no trash)
   * - ``rm -r <dir>``
     - Delete a directory and its contents (be careful! this is definitive,
       there is no trash)

Note that ``./`` represents the current working directory. For instance, ``cd
./`` goes to the current directory (i.e. nothing changes), and ``cp
folder1/foo.txt ./`` copies ``foo.txt`` from ``folder1`` to the current
directory. Similarly, ``../`` represents the parent directory. For instance,
``cd ..`` goes to the parent directory. Finally, ``~`` represents your home
directory, your initial location when you connect with SSH.

Editing ASCII files
'''''''''''''''''''

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Command
     - Description
   * - ``cat <file>``
     - Show the content of ``<file>``
   * - ``head -n X <file>`` 
     - Show the first X lines of ``<file>``
   * - ``tail -n X <file>``
     - Show the last X lines of ``<file>``
   * - ``less <file>``
     - Browse the content of ``<file>`` (type `q` to quit)
   * - ``touch <file>``
     - Create an empty file named ``<file>``
   * - ``nano <file>``
     - Open ``<file>`` in the Nano text editor. Type `Crtl+O` to save, `Ctrl+X` to quit
