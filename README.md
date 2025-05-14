# Réseaux machine virtuelle
Un réseaux de machine virtuelle avec Ubuntu comme serveur, Kali comme test sécurité et un client Windows 11
Windows 11 était à la base mon premier choix, mais visiblement microsoft à mis fin aux versions de tests pour les développeurs, mon choix s'est donc rabbatu sur la version 10 d'évalutaion, ça ne devrait pas changer grand choses. 

Étape 2 : Faire communiquer les 3 machines sur un réseaux interne
Une fois les 3 machines installées, je dois configurer les réseaux des 3 machines pour les faire fonctionner sur un réseaux interne, que j'appelerais "LAB-NETWORK".
Ensuite je fais : sudo nano /etc/netplan/01-netcfg.yaml Pour entrer les informations de ma nouvelle ip.
Problème, les permissions était trop haute pour netplan, Ubuntu à donc bloquer les modifications, j'ai donc modifier les permissions avec chmod 600.
Une fois, je fais le même processus avec les autres VM, en gardant la même structure IP pour faciliter les choses, tout en incrémentant de 1 le dernier chiffre. 
Sur Kali, netplan n'éxiste pas, il faut donc configurer le réseaux à l'aide de network interfaces, mais le principe reste le même. 
Avec cette commande : sudo nmcli con add type ethernet ifname eth0 con-name eth0-manuel ipv4.addresses 192.168.56.102/24 ipv4.gateway 192.168.56.1 ipv4.dns "8.8.8.8 8.8.4.4" ipv4.method manual
sudo nmcli con up eth0-manuel
J'ai pu configurer l'IP souhaité aur KALI, avec un ping sur ma machine Ubuntu, je confirme que la connexion est établi entre les deux machines.
Je fais la même chose avec Windows, je ping entre les trois machines, tout fonctionne. Je vérifie également que je n'ai pas accès à internet avec un ping 8.8.8.8.

Étape 3 : 
Création d'un serveur avec Samba sur Ubuntu.
