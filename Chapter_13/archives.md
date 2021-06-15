# Archives

1. Avec la commande tar, créez dans votre répertoire personnel une archive TP1.tar de votre répertoire TP1. Vérifiez ensuite son contenu pour vous assurer de l'absence de chemins absolus.
    ```bash
    tar -cvf TP1.tar ~/TP1/
    ```
2. Mettez à jour (update) cette archive en y ajoutant le répertoire TP2 de votre répertoire personnel.
    ```bash
    tar -uvf TP1.tar ~/TP2/
    ```
3. Compressez puis décompressez ce fichier TP1.tar avec les commandes bzip2 et gzip. Vérifiez notamment les extensions et les tailles des fichiers après la compression.
    ```bash
    # Tar file
    # -rw-r--r-- 1 mon mon  30K Jun 14 09:28 TP1.tar
    bzip2 -c TP1.tar >> TP1.tar.bz2
    # -rw-r--r-- 1 mon mon 2.0K Jun 14 09:30 TP1.tar.bz2
    bzip2 -dc TP1.tar.bz2 >> TP1.tar.bz2.decompressed
    # -rw-r--r-- 1 mon mon  30K Jun 14 09:32 TP1.tar.bz2.decompressed
    gzip -c TP1.tar >> TP1.tar.gz
    # -rw-r--r-- 1 mon mon 2.1K Jun 14 09:30 TP1.tar.gz
    gzip -dc TP1.tar.gz >> TP1.tar.gz.decompressed
    # -rw-r--r-- 1 mon mon  30K Jun 14 09:32 TP1.tar.gz.decompressed
    ```
4. Créez la même archive avec l'option z de la commande tar qui active la compression compatible avec gzip. Quelle précaution faut-il prendre concernant l'extension du fichier créé ?
    ```bash
    # Ajouter une .gz pour indiquer la compression
    tar -czvf TP.tar.gz ~/TP1 ~/TP2
    ```
5. Créez un script nommé tp1_backup.sh qui sauvegarde le répertoire TP1 dans un fichier /tmp/\_tp1.tar.gz
    ```bash
    touch tp1_backup.sh
    vim tp1_backup.sh
    : '
    #!/bin/bash
    tar -czf /tmp/_tp1.tar.gz /home/mon/TP1
    '
    chmod +x tp1_backup.sh
    ```
6. cron est un programme qui permet aux utilisateurs des systèmes Linux d’exécuter automatiquement des scripts, des commandes ou des logiciels à une date et une heure spécifiées à l’avance, ou selon un cycle défini à l’avance.
7. À l'aide de la commande cron exécutez automatiquement ce script tous les jours à 23h00.
    ```bash
    crontab -e
    : '
    0 23 * * * /home/mon/scripts/tp1_backup.sh
    '
    ```
8. À l'aide de la commande date, qui permet de régler l'heure manuellement :
    1. Fixez la date de votre machine au 1er aout 2011
        1. `sudo date -s "2011-08-01"`
    2. Fixez l'heure à 22h59.
        1. `sudo date -s "22:59"`
    3. Contrôler l'exécution du script tp1_backup.sh à 23h00
        1. `ls /tmp -lh | grep "_tp1"` => `-rw-r--r-- 1 mon mon 858 Aug 1 23:00 _tp1.tar.gz`
    4. Refixez ensuite les valeurs normales.
        1. `sudo apt install ntp` => `sudo reboot`
9. Si vous souhaitez effectuer une action particulière dans la journée (par exemple dans 15 minutes ou à une heure précise), vous n'utiliserez pas cron (car il n'y a pas de répétition, c'est juste une exécution unique programmée), il faudra utiliser la commande at. Exemple, nous allons demander de créer un fichier à 14 h 17 :
    ```bash
    $ at 14:17
    warning: commands will be executed using /bin/sh
    at> touch fichier.txt
    at> [Control-D]
    job 5 at Mon Nov 10 14:17:00 2010
    ```
10. Programmez l'exécution unique du script tp1_backup.sh dans 5 minutes (now +5 minutes)
    ```bash
    at now + 5 min
    warning: commands will be executed using /bin/sh
    at> /bin/bash /home/mon/scripts/tp1_backup.sh
    at> <EOT>
    job 2 at Tue Jun 15 11:39:00 2021
    ```
