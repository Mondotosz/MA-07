# Windows managers

1. Afin d'observer l'enchaînement des commandes sur une même ligne, tapez xterm ; xclock.
2. Pourquoi le programme xclock ne s'est-il pas lancé et à quel moment le fera-t-il ?
3. La commande kill permet de tuer un processus en lui envoyant un signal.
    1. Tapez man 7 signal pour afficher la liste des signaux disponibles pour kill
    2. Retrouvez le numéro du signal de type KILL qui est le plus efficace pour tuer un processus.
4. Les commandes pgrep et pkill permettent de gérer les processus par leur nom.
    1. Lancez deux commandes xeyes en tâches de fond.
    2. Utilisez les options de pgrep pour récupérer les numéros et les noms de ces 2 processus.
    3. Utilisez la commande pkill pour tuer uniquement le plus vieux des deux.
5. Lancez xterm
    1. Connectez-vous ensuite dans la première Console Virtuelle par la séquence Ctrl-Alt-F1 puis repérez et tuez le processus xterm qui tourne votre environnement graphique.
    2. Retournez ensuite dans votre environnement graphique en tapant Crtl-Alt-F7.
6. Installer le paquet psmisc
7. Ce paquet contient divers utilitaires qui utilisent le système de fichiers proc
8. fuser : identifie les processus utilisant des fichiers ou sockets.
9. killall : tue les processus par leur nom (ex « killall -HUP named »).
10. peekfd : affiche les données passant par un descripteur de fichier.
11. pstree : affiche un arbre des processus actifs.
12. prtstat : imprime le contenu de /proc//stat
13. Lancez une commande xterm puis placez-vous dans cette nouvelle fenêtre et lancer une nouvelle commande xclock.
    a. Avec la commande ps alx et le contenu de la colonne PPID, retrouvez le numéro du processus parent de votre nouvelle fenêtre xterm.
    b. Retrouvez ce lien de parenté à l'aide de la commande pstree.
    c. Tuez le processus parent. Que se passe-t-il ?
14. Lancez 3 fois le programme xclock en tâche de fond.
    a. Tuez les programme xclock en une seule fois avec la commande killall.
    b. Quel est l'inconvénient de cette commande ?
15. Lancez xterm en tâche de fond et retrouvez son numéro de processus.
16. Déplacez-vous ensuite dans le répertoire /proc puis dans celui correspondant au numéro de processus trouvé.
    a. Observez le contenu des fichiers status et environ.
17. Lancez la commande top pour voir fonctionner l'ordonnanceur des tâches du système.
18. Affichez seulement ceux dont l'utilisateur cpnv est le propriétaire.
19. Vérifiez l’espace RAM disponible par la commande free.
20. Obtenez les informations sur votre processeur en affichant le contenu du fichier /proc/cpuinfo.
21. Dans la liste des processus de votre système, vérifiez que le serveur ssh tourne bien. Pour cela, utilisez une option de pgrep permettant de chercher le mot sshd sur toute la longueur de la ligne dans la liste des processus et une autre affichant les détails sur le processus.
22. Dans le répertoire /etc/init.d, observez le contenu du script ssh permettant de lancer ce serveur et notamment les options pour l'arrêter ou le démarrer.
23. A l'aide de ces options, arrêtez le serveur puis redémarrez-le en vérifiant que cela a marché par la liste des processus actifs ou en tentant d'y accéder par le client ssh.
24. Utilisez ensuite la commande service pour redémarrer le serveur ssh.
25. Installer le paquet chkconfig
26. A l'aide de la commande chkconfig, vérifiez à quels niveaux de démarrage (RunLevel) ssh peut être démarré.
27. Installer le paquet sysv-rc-conf
28. A l'aide de la commande sysv-rc-conf, vérifiez à quels niveaux de démarrage (RunLevel) cron peut être démarré.
29. Utilisez la commande runlevel pour vérifier le niveau d’exécution auquel vous travaillez.
30. Passez en mode de maintenance mono-utilisateur (Runlevel 1).
31. Dans la liste des processus de votre système, vérifiez le statut des serveurs ssh et cron.
32. Installer le paquet gnome-core et gdm3 et supprimer xdm
33. Installer XRDP ( serveur RDP) pour se connecter depuis un client RDP® sur un serveur Linux
34. Editez le fichier /etc/xrdp/startwm.sh
    ```bash
    #!/bin/sh
    if [ -r /etc/default/locale ]; then
        . /etc/default/locale
        export LANG LANGUAGE
    fi
    #. /etc/X11/Xsession
    /usr/bin/openbox-session
    ```
