Connexion
=========

L’accès à la plateforme CHP-IQ se fait par SSH (Secure Shell). L’adresse du nœud
de connexion est ``ip09.ccs.usherbrooke.ca``.

Les systèmes d’exploitation récents (Linux, MacOS, Windows 11) incluent
habituellement un client SSH. Pour vous connecter à la plateforme en mode ligne
de commande, ouvrez d’abord une fenêtre de terminal (nommé PowerShell dans
Windows). Dans cette fenêtre, utilisez la commande ``ssh`` pour établir une
connexion :

.. code-block:: console

   $ ssh alice@ip09.ccs.usherbrooke.ca
   alice@ip09.ccs.usherbrooke.ca's password:

Remplacez ``alice`` par votre nom d’utilisateur. (Si vous avez un compte
restreint à la plateforme CHP-IQ, il débutera par ``iq-``, par exemple
``iq-alice``.)

Entrez ensuite votre mot de passe CCDB (ou le mot de passe de votre compte
restreint). Notez qu’aucun caractère ne s’affiche à l’écran pendant la saisie de
votre mot de passe.

.. seealso::
   - `SSH <https://docs.alliancecan.ca/wiki/SSH/fr>`_ (documentation technique
     de l’Alliance)

Clients SSH alternatifs
-----------------------

Bien qu’un client SSH soit maintenant inclut avec Windows (depuis la version
10 1803), certains chercheurs préfèrent utiliser un client tierce partie,
pour bénéficier de fonctions supplémentaires ou simplement par habitude. Des
choix populaires sont :

* `MobaXterm <https://mobaxterm.mobatek.net/>`_
* `PuTTY <https://www.chiark.greenend.org.uk/~sgtatham/putty/>`_
* `Windows Subsystem for Linux (WSL) <https://docs.microsoft.com/en-us/windows/wsl/install>`_

Nous recommandons MobaXterm aux nouveaux utilisateurs plutôt que PuTTY puisque
le premier offre davantage de fonctionnalités. Pour sa part, WSL n’est pas un
client SSH proprement dit, mais plutôt un système Linux virtuel installé à
l’intérieur de Windows. WSL donne accès aux commandes Linux de base, incluant
les commandes pour SSH.

.. seealso::
   - Documentation technique de l’Alliance :
       - `Connexion à un serveur avec MobaXterm <https://docs.alliancecan.ca/wiki/Connecting_with_MobaXTerm/fr>`_  
       - `Connexion à un serveur avec PuTTY <https://docs.alliancecan.ca/wiki/Connecting_with_PuTTY/fr>`_

Clés SSH
--------

Vous pouvez utiliser une paire de clés SSH pour vous connecter plutôt que votre
mot de passe. Cela améliore la sécurité tout en étant plus pratique.

La page `Clés SSH <https://docs.alliancecan.ca/wiki/SSH_Keys/fr>`_ de la
documentation technique de l’Alliance explique comment générer une paire de clés
et installer la clé publique sur le serveur. Pour l’installation, suivez les
instructions de la section `Par le fichier authorized_keys` plutôt que `Via
CCDB` puisque la plateforme CHP-IQ n’utilise pas les clés SSH de votre compte
CCDB.

Accès par MP2
-------------

Bien qu’il soit possible d’utiliser la plateforme CHP-IQ à partir d’un nœud de
connexion régulier de MP2, nous ne le recommendons pas car les architectures des
deux systèmes sont très différentes. Utiliser la plateforme CHP-IQ via MP2 mène
à des problèmes de compatibilité logicielle.
