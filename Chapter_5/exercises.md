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
    4. les numéros d'inode1
        ```bash
        ls -i
        ```
    5. la date de dernière modification pour trier la liste des fichiers
    6. la taille des fichiers pour trier la liste des fichiers
    7. Testez en les combinant ces différents critères pour afficher et trier la liste des fichiers de votre répertoire personnel.
3. Affichez la liste des fichiers du répertoire /var/log triée par date de modification pour voir quel est le fichier de logs du système le plus récent.
4. Depuis votre répertoire personnel, affichez la liste et les informations sur les fichiers de configuration (avec une extension .conf) contenus dans le répertoire /etc.
5. Toujours depuis votre répertoire personnel affichez le contenu du fichier "resolv.conf" stocké dans /etc. Quelles informations contient ce fichier ?
6. Créez le fichier vide fichier-cache dans le reprtoire TP1 et vérifiez sa présence par la commande ls.
7. Renommez à présent ce fichier pour que la commande ls ne le fasse plus apparaître, à moins d'utiliser l'option -1.
8. Avec la commande mv, renommez le fichier prog4.for en prog3.for.
    1. Que s'est-il passé et quel est le moyen de sécuriser cette commande ?
9. Utilisez la commande sécurisée précédemment pour renommer le répertoire include en INCLUDE.
10. Pourquoi le système ne pose-t-il pas la question pour renommer ?
11. Que se passerait-il si le répertoire INCLUDE existait déjà avant d'utiliser la commande ?
12. Avec la commande mv, déplacez le fichier prog1.c vers le répertoire web en utilisant un chemin relatif.
13. Avec cp, copiez le fichier prog2.c dans le répertoire courrier en utilisant des chemins absolus.
    1. Relancez la même commande et notez vos remarques.
    2. Que faire pour sécuriser la commande ?
14. Placez-vous dans divers et, en une seule commande, copiez-y le répertoire src et son contenu en le renommant src2.
    1. Quel problème rencontrez-vous et quelle alternative devez-vous utiliser ?
15. Trouvez la commande permettant de supprimer le répertoire src2. Elle devra être sécurisée et demander confirmation à l'utilisateur avant toute destruction de fichier.
16. Les inodes sont des structures de données contenant des informations concernant les fichiers stockés dans certains systèmes de fichiers. À chaque fichier correspond un numéro d'inode dans le système de fichiers dans lequel il réside, unique au périphérique sur lequel il est situé. ↩︎
