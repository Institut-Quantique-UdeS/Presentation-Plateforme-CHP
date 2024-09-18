Connecting
==========

Access the IQ HPC Platform through SSH (Secure Shell). The login node address is
``ip09.ccs.usherbrooke.ca``.

Récent operating systems (Linux, MacOS, Windows 11) typically include an SSH
client. To connect to the platform in command line mode, first open a terminal
window (called PowerShell in Windows). In that window, use the ``ssh`` command
to connect:

.. code-block:: console

   $ ssh alice@ip09.ccs.usherbrooke.ca
   alice@ip09.ccs.usherbrooke.ca's password:

Replace ``alice`` by your username. (If you have a restricted IQ HPC account, it
starts with ``iq-``, for instance ``iq-alice``.)

Next, type in your CCDB password (or the password for your restricted account).
Note that no characters are shown on the screen as you type.

.. seealso::
   - `SSH <https://docs.alliancecan.ca/wiki/SSH/en>`_ (Alliance technical
     documentation)

Alternative SSH clients
-----------------------

Even though an SSH client is now included with Windows (since version 10 1803),
some researchers prefer to use a third-party client, either for its
functionalities or simply by habit. Popular choices include:

* `MobaXterm <https://mobaxterm.mobatek.net/>`_
* `PuTTY <https://www.chiark.greenend.org.uk/~sgtatham/putty/>`_
* `Windows Subsystem for Linux (WSL) <https://docs.microsoft.com/en-us/windows/wsl/install>`_

We recommend MobaXterm to new users rather than PuTTY since the former offers
better functionalities. WSL is not an SSH client per say but rather a virtual
Linux system installed inside Windows. WSL provides access to basic Linux
commands, including those for SSH.

.. seealso::
   - Alliance technical documentation:
       - `Connecting with MobaXterm <https://docs.alliancecan.ca/wiki/Connecting_with_MobaXTerm/en>`_
       - `Connecting with PuTTY <https://docs.alliancecan.ca/wiki/Connecting_with_PuTTY/en>`_

SSH keys
--------

You can use an SSH key pair to connect rather than your password. This provides
added security in addition to being more practical.

The `SSH Keys <https://docs.alliancecan.ca/wiki/SSH_Keys/en>`_ page in the
Alliance technical documentation explains how to generate a key pair and install
the public key on the server. To install the key, follow the instructions in the
`Using the authorized_keys file` section rather than `Using CCDB` since the IQ
HPC Platform does not use the SSH keys in your CCDB account.

Access through MP2
------------------

While it is possible to use the IQ HPC Platform from a regular MP2 login node,
we advise against it since the architecture of the two systems are very
different. Using the IQ HPC Platform via MP2 leads to software compatibility
problems.
