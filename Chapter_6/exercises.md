# Liens symboliques

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

1. Placez-vous dans le répertoire INCLUDE. A l'aide de la commande ln, faites un lien physique appelé lien-solide-prog3 vers le fichier src/prog3.for avec un chemin relatif.
    ```bash
    ln ../src/prog3.for lien-solide-prog3
    ```
2. Pratiquez de même avec un lien symbolique appelé lien-symb-prog3.
    ```bash
    ln -s ../src/prog3.for lien-symb-prog3
    ```
3. Que constatez-vous pour les droits de ces liens et leur numéro d'inode ?
    ```bash
    ls -li
    # Output
    total 0
    523958 -rw-r--r-- 2 mon mon  0 May  4 11:27 lien-solide-prog3
    524614 lrwxrwxrwx 1 mon mon 16 May  4 11:53 lien-symb-prog3 -> ../src/prog3.for
    # le lien symbolique afficher le chemin vers l'original et à un inode different du fichier reel
    # il a aussi des permissions  777 (tous le monde a tout les droits)
    # le lien physique garde le meme inode et permissions que le fichier reel
    ```
4. Que se passera-t-il si vous détruisez le fichier destination de ces liens ?
    ```bash
    rm ~/TP1/progs/src/prog3.for
    ls -li
    # Output
    total 0
    523958 -rw-r--r-- 1 mon mon  0 May  4 11:27 lien-solide-prog3
    524614 lrwxrwxrwx 1 mon mon 16 May  4 11:53 lien-symb-prog3 -> ../src/prog3.for
    # Le lien symbolique devient rouge
    cat lien-symb-prog3
    # Output
    cat: lien-symb-prog3: No such file or directory
    # Le lien physique reste le meme
    ```
5. Toujours dans INCLUDE, créez un lien symbolique appelé lien-rep-src vers le répertoire src en utilisant le chemin absolu.
    ```bash
    ln -s /home/mon/TP1/progs/src lien-rep-src
    ```
    1. Utilisez ensuite ce lien pour vous déplacer dans le répertoire src.
        ```bash
        cd lien-rep-src
        ```
    2. Faites un help pwd pour utiliser les deux options possibles de cette commande et vérifier l'existence du lien.
        ```bash
        pwd
        # Output
        /home/mon/TP1/progs/INCLUDE/lien-rep-src
        pwd -P
        # Output
        /home/mon/TP1/progs/src
        ```
    3. Remontez à présent dans le répertoire parent.
        ```bash
        pwd
        # Output
        /home/mon/TP1/progs/INCLUDE
        ```
    4. Où vous retrouvez-vous ?
        1. dans INCLUDE
