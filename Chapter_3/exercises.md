# Exercises

1. Tapez man man et retrouvez l'option permettant d'afficher la description courte des pages du manuel correspondant.
    1. -k ou --apropos
2. Dans le man de la commande chown, détaillez le SYNOPSIS pour préciser quels sont les paramètres obligatoires pour exécuter la commande et quelles sont les options facultatives.
    1. ````man
        SYNOPSIS
        chown [OPTION]... [OWNER][:[GROUP]] FILE...
        chown [OPTION]... --reference=RFILE FILE...```
       ````
    2. Obligatoire
        1. `[OWNER][:[GROUP]] FILE`
        2. `--reference=RFILE FILE`
    3. Facultatives
        1. `-c, --change`
        2. `-f, --silent, --quiet`
        3. `-v, --verbose`
        4. `--dereference`
        5. `-h, --no-dereference`
        6. `--from=CURRENT_OWNER:CURRENT_GROUP`
        7. `--no-preserve-root`
        8. `--preserve-root`
        9. `-R, --recursive`
        10. `-H if a command line argument is a symbolic link to a directory, traverse it`
        11. `-L traverse every symbolic link to a directory encountered`
        12. `-P do not traverse any symbolic links (default)`
        13. `--help display this help and exit`
        14. `--version`
3. Utilisez la commande man pour obtenir des informations sur la commande rm (destruction de fichier et répertoire) et trouver les options permettant de :
    1. Détruire tout fichier sans demander confirmation à l’utilisateur
        1. `-f`
    2. Demander confirmation avant toute destruction de fichier
        1. `-i`
    3. Détruire toute une arborescence en une seule commande
        1. `-r`
    4. Voir ce que fait la commande (affiche les noms de fichiers)
       1. `-v`
    5. Tapez ensuite rm --help pour retrouver les mêmes options
4. Tapez les commandes ci-dessous et observez les informations qu'elles vous donnent
    1. `apropos kill`
       1. affiche toutes les fonctions contenant le mot kill
    2. `whatis kill`
       1. affiche une short description de la commande kill
    3. `man kill`
       1. affiche la page de manuel de kill
    4. `man 2 kill`
       1. affiche la section 2 de kill, comme kill n'as qu'une section, affiche une erreur
5. `La commande alias est une commande interne au shell bash et n'a donc pas sa propre page de man. Tapez d'abord la commande help pour avoir la liste des commandes internes du shell bash, puis help alias pour obtenir l'aide sur la commande alias.`
   1. ```bash
        mon@MA-07-debian:~$ help alias
        alias: alias [-p] [name[=value] ... ]
        Define or display aliases.

        Without arguments, `alias' prints the list of aliases in the reusable
        form `alias NAME=VALUE' on standard output.

        Otherwise, an alias is defined for each NAME whose VALUE is given.
        A trailing space in VALUE causes the next word to be checked for
        alias substitution when the alias is expanded.

        Options:
        -p        print all defined aliases in a reusable format

        Exit Status:
        alias returns true unless a NAME is supplied for which no alias has been
        defined.```
