# Installation

1. Download iso from [debian.org](https://www.debian.org/releases/stretch/debian-installer/)
2. Install in a vm using VMware
    1. Language : English
    2. Location : Europe/Switzerland
    3. Locale : United Kingdom
    4. Layout : EN_UK
    5. root password : Pa$$w0rd
    6. User
        1. Username : mon
        2. Password : Pa$$word
    7. Partitioning
        1. 10GB primary / bootable ext4
        2. 512M primary swap swap
        3. 21GB primary /home ext4
    8. Install grub on /dev/sda
3. aptitude (package manager)
    1. add mirror
    2. `apt update`
    3. `apt upgrade`
4. ssh
    1. `apt install openssh-server`
    2. systemctl enable ssh
    3. systemctl start ssh
    4. `mkdir ~/.ssh`
    5. `touch ~/.ssh/authorized_keys`
    6. `ssh-keygen` (on windows)
    7. `type $env:USERPROFILE\.ssh\id_rsa.pub | ssh {IP-ADDRESS-OR-FQDN} "cat >> .ssh/authorized_keys"` (on windows)
