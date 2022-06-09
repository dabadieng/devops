# Virtualisation

## virtualbox 


## configurer les vm 
Pour renommer les machines
$ sudo hostnamectl set-hostname <name>
$ sudo vim /etc/hoots #puis remplacer la chaine de caractères qui se
trouve à droite de l'adresse 127.0.1.1

Pour mettre l'IP en static et gérer la gateway taper la cde suivante : 
vi /etc/systemd/network/10-enp0s3.network 

    ex de config pour la mg01
    [Match]
    Name=enp0s3
    [Network]
    Address=192.168.0.2/Z9
    [Route]
    Gateway=192.168.0.1
    Destination=0.0.0.0/0


### Gérer les redirections 
--> gw01

Pour mettre l'IP en static et gérer la gateway taper la cde suivante : 
vi /etc/systemd/network/10-enp0s8.network 

    ex de config pour la gw01
    [Match]
    Name=enp0s8
    [Network]
    Address=192.168.0.1/Z9
    [Route]
    Gateway=192.168.0.1
    Destination=0.0.0.0/0

se placer dans la vm qui à pour rôle la gateway est taper cette commande : 
iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o enp0s3 -j MASQUERADE

pour vérifier que la précédante commande à réussit taper la cde suivante : 
ip route 

pour sauvegarder les régles iptables 
1- créer un dossier
mkdir /etc/iptables

2- sauvegarder à l'aide de la cde suivante : 
iptables-save > /etc/iptables/rules.v4

une fois la configuration faite, il faut redémarrer les services en tapant la cde suivante : 
systemctl restart systemd-network








