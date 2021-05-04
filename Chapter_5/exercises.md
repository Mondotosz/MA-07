# Manipulation de fichiers

```
/home/[user]/TP1
                |--courrier
                |--progs
                    |--bin
                    |--src
                    |--include
                    |--lib
                |--divers
                    |--images
                    |--web
```

1. A l'aide de la commande touch, créez les fichiers vides prog1.c, prog2.c, prog3.for et prog4.for dans le répertoire src.
    ```bash
    touch ~/TP1/progs/src/prog{{1,2}.c,{3,4}.for}
    ```
2. Relevez les options de la commande ls qui permettent d'obtenir
    1. la sous-arborescence récursive d'un répertoire
        ```bash
        ls ~/TP1/* -R
        # -R : list subdirectories recursively
        ```
    2. la liste des fichiers cachés
        ```bash
        ls -ld .?*
        ```
    3. les principales informations (type, droits, propriétaire...)
        ```bash
        ls -l
        ```
    4. les numéros d'inode
        ```bash
        ls -i
        ```
    5. la date de dernière modification pour trier la liste des fichiers
        ```bash
        ls -ct
        ```
    6. la taille des fichiers pour trier la liste des fichiers
        ```bash
        ls -st
        ```
    7. Testez en les combinant ces différents critères pour afficher et trier la liste des fichiers de votre répertoire personnel.
        ```bash
        ls ~ -scilah
        ```
3. Affichez la liste des fichiers du répertoire /var/log triée par date de modification pour voir quel est le fichier de logs du système le plus récent.
    ```bash
    ls /var/log -lct
    ```
4. Depuis votre répertoire personnel, affichez la liste et les informations sur les fichiers de configuration (avec une extension .conf) contenus dans le répertoire /etc.
    ```bash
    ls /etc/*.conf -la
    ```
5. Toujours depuis votre répertoire personnel affichez le contenu du fichier "resolv.conf" stocké dans /etc. Quelles informations contient ce fichier ?
    ```bash
    cat /etc/resolve.conf
    # Output
    domain localdomain
    search localdomain
    nameserver 192.168.1.2
    ```
6. Créez le fichier vide fichier-cache dans le reprtoire TP1 et vérifiez sa présence par la commande ls.
    ```bash
    touch ~/TP1/fichier-cache
    ls ~/TP1
    ```
7. Renommez à présent ce fichier pour que la commande ls ne le fasse plus apparaître, à moins d'utiliser l'option -a.
    ```bash
    mv ~/TP1/fichier-cache ~/TP1/.fichier-cacher
    ```
8. Avec la commande mv, renommez le fichier prog4.for en prog3.for.
    ```bash
    mv ~/TP1/progs/src/prog4.for ~/TP1/progs/src/prog3.for
    ```
    1. Que s'est-il passé et quel est le moyen de sécuriser cette commande ?
        1. Fichier 3 écrasé, utiliser le flag -i
9. Utilisez la commande sécurisée précédemment pour renommer le répertoire include en INCLUDE.
    ```bash
    mv -i ~/TP1/progs/include ~/TP1/progs/INCLUDE
    ```
10. Pourquoi le système ne pose-t-il pas la question pour renommer ?
    1. L'action ne va rien écraser
11. Que se passerait-il si le répertoire INCLUDE existait déjà avant d'utiliser la commande ?
    1. Il demanderait une question yes/no pour valider l'action
12. Avec la commande mv, déplacez le fichier prog1.c vers le répertoire web en utilisant un chemin relatif.
    ```bash
    ~/TP1/progs/src $
    mv prog1.c ./../../divers/web
    ```
13. Avec cp, copiez le fichier prog2.c dans le répertoire courrier en utilisant des chemins absolus.
    ```bash
    cp /home/mon/TP1/progs/src/prog2.c /home/mon/TP1/courrier
    ```
    2. Relancez la même commande et notez vos remarques.
        ```bash
        cp /home/mon/TP1/progs/src/prog2.c /home/mon/TP1/courrier
        # Pas d'output
        ```
    3. Que faire pour sécuriser la commande ?
        1. utiliser le flag -i
14. Placez-vous dans divers et, en une seule commande, copiez-y le répertoire src et son contenu en le renommant src2.
    ```bash
    cp ~/TP1/progs/src src2 -R
    ```
    2. Quel problème rencontrez-vous et quelle alternative devez-vous utiliser ?
        1. pas eu de problème, il faut utiliser le flag -R pour copier le contenu du dossier
15. Trouvez la commande permettant de supprimer le répertoire src2. Elle devra être sécurisée et demander confirmation à l'utilisateur avant toute destruction de fichier.
    ```bash
    rm ~/TP1/diver/src2 -iR
    ```
