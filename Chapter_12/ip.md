# Configuration IP

1. Déterminez quelle est la configuration actuelle de vos interfaces réseau avec la commande ip.
    1. `ip -c addr`
    2. lo (loopback) => 127.0.0.1/8
    3. ens33 => 192.168.1.128/24
2. Quelle est votre adresse IP, votre masque, votre adresse MAC et votre MTU.
    1. ip : 192.168.1.128 mask : 255.255.255.0 MAC : 00:0c:29:74:34:b6 MTU : 1500
3. Déterminez les cartes réseau dont vous disposez sur votre machine avec la commande lspci.
    1. `lspci` => `02:01.0 Ethernet controller: Intel Corporation 82545EM Gigabit Ethernet Controller (Copper) (rev 01)`
    ```bash
    lshw -class network
    :'
    *-network
        description: Ethernet interface
        product: 82545EM Gigabit Ethernet Controller (Copper)
        vendor: Intel Corporation
        physical id: 1
        bus info: pci@0000:02:01.0
        logical name: ens33
        version: 01
        serial: 00:0c:29:74:34:b6
        size: 1Gbit/s
        capacity: 1Gbit/s
        width: 64 bits
        clock: 66MHz
        capabilities: pm pcix bus_master cap_list rom ethernet physical logical tp 10bt 10bt-fd 100bt 100bt-fd 1000bt-fd autonegotiation
        configuration: autonegotiation=on broadcast=yes driver=e1000 driverversion=7.3.21-k8-NAPI duplex=full ip=192.168.1.128 latency=0 link=yes mingnt=255 multicast=yes port=twisted pair speed=1Gbit/s
        resources: irq:19 memory:fd5c0000-fd5dffff memory:fdff0000-fdffffff ioport:2000(size=64) memory:fd500000-fd50ffff
    '
    ```
4. La configuration des interfaces réseau se fait au démarrage au moyen, entre autre, du fichier /etc/network/interfaces (parce que la distribution GNU/Linux est une Debian). Vérifiez que la configuration est bien faite via DHCP.
   1. `cat /etc/network/interfaces` => `iface ens33 inet dhcp`
5. Retrouvez l'adresse de loopback et précisez en quoi elle est utile au système.
   1. ` ip -br a show lo` => `lo               UNKNOWN        127.0.0.1/8 ::1/128`
   2. Elle permet aux différents services de communiquer entre eux en interne sans s'exposer aux autres appareils du reseau
6. Désactivez votre interface Ethernet ens32 (ifdown)
   1. `sudo /sbin/ifdown ens33`
7. Activez la carte ens32 (ifup)
   1. `sudo /sbin/ifup ens33`
8. Essayez de pinguer votre machine hôte qui devra être dans le même subnet.
   1. `ping 192.168.1.1` => `64 bytes from 192.168.1.1: icmp_seq=1 ttl=128 time=0.425 ms`
9.  Retrouvez le fichier de log du répertoire /var/log qui vient d'être modifié par la question précédente.
    1.  `sudo cat /var/log/daemon.log`
10. Observez les dernières lignes de ce fichier pour retrouver :
    1. Le port par défaut et l'adresse de broadcast pour l'émission des requêtes DHCP
       1. `Jun  8 12:00:38 MA-07-debian dhclient[4340]: DHCPDISCOVER on ens33 to 255.255.255.255 port 67 interval 8` => `255.255.255.255:67`
    2. L'adresse du serveur qui vous a fourni votre adresse IP
       1. `Jun  8 12:00:39 MA-07-debian dhclient[4340]: DHCPOFFER of 192.168.1.128 from 192.168.1.254` => `192.168.1.254`
