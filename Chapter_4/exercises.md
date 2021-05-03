# Arborescence

## Exercice

1. Avec la commande cd, déplacez-vous dans le répertoire /usr/local
2. Testez et notez les différentes façons de revenir avec la commande cd dans votre répertoire personnel /home/mon
   A chaque étape, pensez à utiliser la commande pwd pour vérifier dans quel répertoire vous vous trouvez.
    ```bash
     cd /home/mon
     cd ~
     cd $HOME
     cd -
    ```
3. Testez la commande cd - et expliquez comment elle fonctionne.
    1. retourne à la location avant le dernier cd
4. Où vous place la commande cd utilisée sans paramètre ?
5. Créez dans votre répertoire personnel /home/mon un répertoire TP1 dans lequel vous devrez effectuer tous les exercices suivants.
    ```bash
    mkdir ~/TP1
    ```
6. Utilisez les commandes cd et mkdir pour créer dans votre répertoire TP1 l'arborescence présentée. Pour vous faciliter la tâche, utilisez l'option de la commande mkdir permettant de créer en une fois une arborescence à plusieurs niveaux.

    Pensez à utiliser les flèches du clavier pour récupérer les commandes précédemment tapées et à compléter automatiquement les noms de répertoires et de fichiers avec la touche de tabulation.

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

    ```bash
    mkdir -p ~/TP1/{courrier,progs/{bin,src,include},lib/{divers,images,web}}
    ```

7. Quand vous avez créé l'arborescence complète, affichez-la à l'aide de la commande ls (option de récursivité)
    ```bash
    ls -R
    # si tree est installé
    tree
    ```
8. En vous plaçant sur le répertoire web, notez les différentes manières de vous déplacer vers le répertoire src en utilisant les chemins absolu et relatif. Utilisez la touche tabulation pour compléter automatiquement les noms de répertoire avec la commande cd.
    ```bash
    cd /home/mon/TP1/progs/src
    cd ~/TP1/progs/src
    cd ../../progs/src
    ```
