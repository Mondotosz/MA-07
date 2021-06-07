# Windows managers

1. Afin d'observer l'enchaînement des commandes sur une même ligne, tapez `xterm ; xclock`.
2. Pourquoi le programme xclock ne s'est-il pas lancé et à quel moment le fera-t-il ?
    1. Les programmes se lances de manière linéaire, bash attend la fin de l'execution de xterm pour lancer xclock
3. La commande kill permet de tuer un processus en lui envoyant un signal.
    1. Tapez `man 7 signal` pour afficher la liste des signaux disponibles pour kill
        ```bash
        man 7 signal
        # out
        : '
        Term Terminate process
        Ign  Ignore signal
        Core Terminate process and dump core
        Stop Stop process
        Cont Continue stopped process
        '
        ```
    2. Retrouvez le numéro du signal de type KILL qui est le plus efficace pour tuer un processus.
        1. Terminate, `kill(2)` donc 2?
4. Les commandes pgrep et pkill permettent de gérer les processus par leur nom.
    1. Lancez deux commandes xeyes en tâches de fond.
        ```bash
        xeyes &
        xeyes &
        ```
    2. Utilisez les options de pgrep pour récupérer les numéros et les noms de ces 2 processus.
        ```bash
        pgrep -l xeyes
        ```
    3. Utilisez la commande pkill pour tuer uniquement le plus vieux des deux.
        ```bash
        pkill -o xeyes
        ```
5. Lancez xterm
    1. Connectez-vous ensuite dans la première Console Virtuelle par la séquence Ctrl-Alt-F1 puis repérez et tuez le processus xterm qui tourne votre environnement graphique.
        ```bash
        pgrep -l xterm
        # 16379 xterm
        killall xterm
        ```
    2. Retournez ensuite dans votre environnement graphique en tapant Crtl-Alt-F7.
6. Installer le paquet psmisc
    ```bash
    sudo apt install psmisc
    ```
7. Ce paquet contient divers utilitaires qui utilisent le système de fichiers proc
    1. `fuser` : identifie les processus utilisant des fichiers ou sockets.
    2. `killall` : tue les processus par leur nom (ex « killall -HUP named »).
    3. `peekfd` : affiche les données passant par un descripteur de fichier.
    4. `pstree` : affiche un arbre des processus actifs.
    5. `prtstat` : imprime le contenu de /proc//stat
8. Lancez une commande xterm puis placez-vous dans cette nouvelle fenêtre et lancer une nouvelle commande xclock.
    1. Avec la commande ps alx et le contenu de la colonne PPID, retrouvez le numéro du processus parent de votre nouvelle fenêtre xterm.
        ```bash
        # use / to search for xclock
        ps alx | less
        # F   UID    PID   PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
        # 0  1000  16713  16664  25   5  33996  6564 x64_sy SN   pts/1      0:00 xclock
        ```
    2. Retrouvez ce lien de parenté à l'aide de la commande pstree.
        ```bash
        pstree 16664
        #zsh───xclock
        ```
    3. Tuez le processus parent. Que se passe-t-il ?
        ```bash
        pkill -P 16664
        # kill la shell mais le terminal reste present et relance une session
        ```
9. Lancez 3 fois le programme xclock en tâche de fond.
    ```bash
    for i in {1..3}; do xclock &; done
    ```
    1. Tuez les programme xclock en une seule fois avec la commande killall.
        1. `killall xclock`
    2. Quel est l'inconvénient de cette commande ?
        1. tue tous les process du nom donné
10. Lancez xterm en tâche de fond et retrouvez son numéro de processus.
    ```bash
    xterm&
    psl alx | grep xterm
    # F   UID    PID   PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    # 0  1000  17190  17138  25   5  39316 10320 core_s SN   pts/3      0:00 xterm
    ```
11. Déplacez-vous ensuite dans le répertoire /proc puis dans celui correspondant au numéro de processus trouvé.
    ```bash
    cd /proc/17190
    ```
    2. Observez le contenu des fichiers status et environ.
        ```bash
        ls
        : '
        attr             cwd       map_files   oom_adj        schedstat     syscall
        autogroup        environ   maps        oom_score      sessionid     task
        auxv             exe       mem         oom_score_adj  setgroups     timers
        cgroup           fd        mountinfo   pagemap        smaps         timerslack_ns
        clear_refs       fdinfo    mounts      patch_state    smaps_rollup  uid_map
        cmdline          gid_map   mountstats  personality    stack         wchan
        comm             io        net         projid_map     stat
        coredump_filter  limits    ns          root           statm
        cpuset           loginuid  numa_maps   sched          status
        '
        ```
12. Lancez la commande top pour voir fonctionner l'ordonnanceur des tâches du système.
    1. `top` ou `htop` pour un gestionnaire de tache plus agréable
13. Affichez seulement ceux dont l'utilisateur cpnv est le propriétaire.
    1. `top -u mon`
14. Vérifiez l’espace RAM disponible par la commande free.

    ```bash
    free
    #               total        used        free      shared  buff/cache   available
    # Mem:        2018216      406264      652460        6712      959492     1417552
    # Swap:        498684        7768      490916

    # df donne plus d'informations pour l'espace libre
    df
    ```

15. Obtenez les informations sur votre processeur en affichant le contenu du fichier /proc/cpuinfo.
    ```bash
    less /proc/cpuinfo
    ```
16. Dans la liste des processus de votre système, vérifiez que le serveur ssh tourne bien. Pour cela, utilisez une option de pgrep permettant de chercher le mot sshd sur toute la longueur de la ligne dans la liste des processus et une autre affichant les détails sur le processus.
    ```bash
    pgrep -l sshd
    # 597 sshd
    ```
17. Dans le répertoire /etc/init.d, observez le contenu du script ssh permettant de lancer ce serveur et notamment les options pour l'arrêter ou le démarrer.
    ```bash
    cat /etc/init.d/ssh
    # start
    # stop
    ```
18. A l'aide de ces options, arrêtez le serveur puis redémarrez-le en vérifiant que cela a marché par la liste des processus actifs ou en tentant d'y accéder par le client ssh.
    ```bash
    sudo systemctl stop sshd
    sudo systemctl status sshd
    # inactive (dead)
    sudo systemctl start sshd
    sudo systemctl status sshd
    # active (running)
    ```
19. Utilisez ensuite la commande service pour redémarrer le serveur ssh.
    1.  `sudo service sshd restart`
20. Installer le paquet chkconfig
    1.  `sudo apt install chkconfig` => unavailable or obsolete => use sysv-rc-conf
21. A l'aide de la commande chkconfig, vérifiez à quels niveaux de démarrage (RunLevel) ssh peut être démarré.
22. Installer le paquet sysv-rc-conf
23. A l'aide de la commande sysv-rc-conf, vérifiez à quels niveaux de démarrage (RunLevel) cron peut être démarré.
24. Utilisez la commande runlevel pour vérifier le niveau d’exécution auquel vous travaillez.
25. Passez en mode de maintenance mono-utilisateur (Runlevel 1).
26. Dans la liste des processus de votre système, vérifiez le statut des serveurs ssh et cron.
27. Installer le paquet gnome-core et gdm3 et supprimer xdm
28. Installer XRDP ( serveur RDP) pour se connecter depuis un client RDP® sur un serveur Linux
29. Editez le fichier /etc/xrdp/startwm.sh
    ```bash
    #!/bin/sh
    if [ -r /etc/default/locale ]; then
        . /etc/default/locale
        export LANG LANGUAGE
    fi
    #. /etc/X11/Xsession
    /usr/bin/openbox-session
    ```
