# Utilisateurs

1. Créez sur votre machine l'utilisateur suivant :
    1. Nom de login : secret
    2. Mot de passe : Pa$$w0rd
    3. Répertoire personnel : /home/secret
    4. Id user : par défaut
    5. Groupe d'utilisateurs : par défaut
    6. Description : Utilisateur Secret.
    7. Shell de démarrage : /bin/bash
    ```bash
    sudo useradd secret -m -d /home/secret -s /bin/bash -c "Utilisateur Secret."
    # set password
    sudo passwd secret
    ```
2. Vérifiez la présence de ce nouvel utilisateur dans le fichier _/etc/passwd_
    ```bash
    cat /etc/passwd | grep secret
    ```
3. Depuis votre identité lambda passez en root et à partir de root en secret.
    ```bash
    su root
    su secret
    ```
    1. Utilisez les commandes whoami pour vérifier à chaque fois ces changements d’identité
    2. Que remarquez-vous ?
        1. L'utilisateur a changé
    3. Utilisez la commande su avec l'option -, quelle identité vous donne cette commande ?
        1. root
4. Connecté(e) en cpnv, changez votre mot de passe avec la commande _passwd_.
    ```bash
    passwd
    ```
5. Essayez ensuite de changer celui de secret.
    ```bash
    su secret
    passwd
    ```
6. Connectez-vous en root et essayez de modifier le mot de passe de secret. Que remarquez-vous ?
    1. Il n'y a pas besoins de mettre le mot de passe actuel de l'utilisateur secret et il n'y a pas d'erreur mot de passe inchangé lorsque le nouveau mot de passe est le même que l'ancien
7. Tapez la commande ps alx pour retrouver l'UID de l’utilisateur propriétaire du démon cron
   ```bash
   # en utilisant less et la fonction de recherche avec /
   ps alx | less
   # en utilisant grep
   ps alx | grep cron
   # uid = 0
   ```
    1. Dans le fichier _/etc/passwd_, retrouvez le nom et le GID de cet utilisateur,
    ```bash
    cat /etc/passwd | grep :0
    # out
    root:x:0:0:root:/root:/bin/bash
    # name = root
    # GID = 0
    ```
    3. Dans le fichier _/etc/group_, retrouvez le nom de ce groupe.
    ```bash
    cat /etc/group | grep :0
    # out
    root:x:0:
    # nom = root
    ```
8. La commande sudo permet à un utilisateur d’exécuter des commandes normalement réservées à root, mais cette possibilité n’est pas offerte par défaut sur Debian.
    1. Installer le programme sudo
       ```bash
       su root
       apt install sudo
       ```
    2. Modifiez le fichier _/etc/sudoers_ (commande visudo) en vous inspirant de sa dernière ligne et autorisez cpnv
       ```bash
       visudo
       # /etc/sudoers.tmp
       # User privilege specification
       root    ALL=(ALL:ALL) ALL
       cpnv    ALL=(ALL:ALL) ALL

       # autre méthode
       adduser cpnv sudo
       ```
9.  Connecté en cpnv, simulez immédiatement un arrêt du système par la commande _/sbin/shutdown_.
    ```bash
    sudo /sbin/shutdown
    # out
    Shutdown scheduled for Mon 2021-05-17 09:52:57 CEST, use 'shutdown -c' to cancel.
    ```
