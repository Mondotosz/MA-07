# Redirections

Préambule : Créez dans votre répertoire personnel un répertoire TP2 dans lequel vous devrez effectuer tous les exercices présentés ci-dessous. Les exercices doivent être réalisés en tant qu'utilisateur lambda (n'ayant pas les droits root) sauf lorsque cela est précisé.

```bash
mkdir ~/TP2
cd ~/TP2
```

1. Utilisez la commande echo pour envoyer la ligne Quoi de plus joyeux dans le fichier sensamavie.txt.
    ```bash
    echo "Quoi de plus joyeux" > sensamavie.txt
    ```
2. Vérifiez ensuite le contenu du fichier en l'affichant à l'écran à l'aide de la commande more.
    ```bash
    less sensamavie.txt
    # more version
    more sensamavie.txt
    ```
3. Avec une autre redirection, placez à la suite de ce fichier la ligne que de travailler sous Linux ?.
    ```bash
    echo "que de travailler sous Linux ?" >> sensamavie.txt
    ```
4. Vérifiez en l'affichant à l'écran qu'il contient bien les 2 lignes l'une à la suite de l'autre à l'aide de la commande cat.
    ```bash
    cat sensamavie.txt
    ```
5. Placez-vous dans le répertoire TP2.
    ```bash
    cd ~/TP2
    ```
6. En utilisant la commande ls (sans option), créez un fichier usrlocal.txt contenant la liste des fichiers du répertoire /usr/local.
    ```bash
    ls /usr/local > usrlocal.txt
    ```
7. Avec la commande sort, triez ce fichier par ordre alphabétique inverse et mettez le résultat dans usrlocal-inverse.txt.
    ```bash
    sort -r usrlocal.txt > usrlocal-inverse.txt
    ```
8. Depuis votre répertoire personnel, essayez de détruire par la commande rmdir (sans -r !) le répertoire TP2.
    1. Avec la redirection adéquate, récupérez le message d'erreur dans un fichier TP2/erreur.txt.
        ```bash
        rmdir ~/TP2 2> erreur.txt
        ```
    2. Avec la redirection adéquate, arrangez-vous pour qu'aucun message d'erreur ne soit généré, ni à l'écran ni dans un fichier
        ```bash
        rmdir ~/TP2 2> /dev/null
        ```

# Pipes (|)

1. Pour une première approche du pipe (|), utilisons la commande yes.
    1. Dans le répertoire de TP2/test créez 5 fichiers (fichier1.txt, fichier2.txt, fichier3.txt, fichier4.txt, fichier5.txt) que vous devrez ensuite tous supprimer en demandant confirmation à l'utilisateur.
        ```bash
        mkdir test
        cd test
        touch fichier{1..5}.txt
        ```
    2. Afin d'éviter de devoir répondre par y à chaque suppression de fichier, utilisez la combinaison adéquate permettant d'envoyer cette réponse par la commande yes à la commande rm.
        ```bash
        yes | rm -i ./*
        ```
2. A l'aide des commandes ls et head et d'un pipe (|), affichez à l'écran la liste des 15 premiers fichiers du répertoire /etc.
    ```bash
    ls /etc | head -n 15
    ```
3. A l'aide des commandes ls, tail et sort et de 2 pipes (|), mettez la liste inversée des 20 derniers fichiers du répertoire /etc dans un fichier etc-inverse.txt
    ```bash
    ls /etc | tail -n 20 | sort -r > etc-inverse.txt
    ```
4. Trouvez une combinaison de commandes permettant d'afficher page par page les 100 dernières lignes retournées par la commande dmesg.
    ```bash
    sudo dmesg | tail -n 100 | less
    # more version
    sudo dmesg | tail -n 100 | more
    ```
5. Avec la commande grep, recherchez dans le fichier /etc/passwd les lignes contenant la chaîne bash.
    ```bash
    cat /etc/passwd | grep bash
    ```
6. Utilisez la commande find pour trouver tous les fichiers d'extension .conf du répertoire /etc.
    ```bash
    find /etc -name '*.conf'
    ```
7. Avec l'éditeur nano, créez un fichier cherche-conf.sh et recopiez-y la commande de la question précédente.
    ```bash
    touch cherche-conf.sh
    vim cherche-conf.sh
    # content
    #!/bin/bash
    find /etc -name '*.conf'
    # set permissions
    chmod +x cherche-conf.sh
    ```
    1. Exécutez ce script qui affichera dans un premier temps son résultat à l'écran.
        ```bash
        bash cherche-conf.sh
        ```
    2. Redirigez ensuite ce résultat dans un fichier liste-conf.txt
        ```bash
        bash cherche-conf.sh > list-conf.txt
        ```
    3. Arrangez-vous pour supprimer les messages d'erreur.
        ```bash
        bash cherche-conf.sh > list-conf.txt 2> /dev/null
        ```
