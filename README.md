Projet Personnel – Mise en place d’un partage de fichiers sécurisé sur réseau local virtualisé
Contexte et Objectif
Réalisation d’un partage de fichiers sécurisé entre plusieurs machines virtuelles (Ubuntu, Kali, Windows) sous VirtualBox, dans un réseau local totalement isolé. Le but est de :

Comprendre les mécanismes de partage sur différents OS
Mettre en œuvre des pratiques de cybersécurité (droits d’accès, gestion des utilisateurs…)
Maîtriser la configuration réseau sous VirtualBox
Étapes du Projet
1. Installation d’une VM Windows gratuite
Utilisation des images de test officielles de Microsoft (Windows 10, 90 jours).
Import de la VM dans VirtualBox (OVA), configuration minimale.
2. Création du réseau local interne
Mise en place d’un réseau privé (“interne”) pour relier Ubuntu, Kali et Windows.
Problème rencontré : Impossibilité d’accéder à internet depuis les VM lors de la configuration en “Réseau interne”.
Solution : Ajout d’une deuxième carte réseau par VM pour permettre un double accès (Internet et réseau local).
Modification des fichiers netplan sous Linux pour gérer plusieurs interfaces réseau.
3. Attribution d’IP fixes
Configuration manuelle sur chaque VM (ex. Ubuntu : 192.168.56.101, Windows : 192.168.56.103…).
Vérification des communications (ping).
4. Installation et configuration du partage Samba sur Ubuntu
Installation du serveur Samba.
Création d’un dossier dédié avec droits restreints.
Création d’un utilisateur spécifique Samba, paramétrage du partage sécurisé (guest ok = no).
Problème rencontré :
Ubuntu/Linux ne parvenait pas à joindre Windows via le réseau (impossible de pinger la VM Windows).
Cause identifiée : Le pare-feu Windows bloquait les requêtes ICMP (ping).
Solution : Création d’une règle personnalisée dans le pare-feu Windows pour autoriser les pings entrants.
Communication rétablie après ajustement.
5. Accès aux partages depuis Kali et Windows
Accès testé et validé depuis toutes les machines.
Essai d’accès non autorisé pour vérifier la sécurité : échec comme attendu (bonne configuration Samba).
6. Sécurisations supplémentaires
Restriction exclusive aux seuls utilisateurs autorisés.
Confinement des droits Unix sur le dossier partagé.
Activation et configuration du pare-feu UFW sur Ubuntu pour n’autoriser que les connexions Samba du réseau interne.
Surveillance des journaux Samba pour détecter les tentatives d’accès non autorisé.
Bilan et Compétences mobilisées
Maîtrise de la virtualisation multi-OS (VirtualBox)
Administration réseau (routage, IP fixes, multi-cartes réseaux)
Gestion avancée de la configuration sur Linux (netplan, droits Unix, pare-feu UFW)
Déploiement d’un partage de fichiers sécurisé (Samba)
Application de méthodes de diagnostic réseau et résolution de problèmes liés à la sécurité (pare-feu et permissions)
Renforcement des bonnes pratiques de sécurité (accès limité, aucun invité, surveillance des logs)
Problèmes rencontrés et solutions apportées
Non communication des VM en réseau interne
Cause : Mauvaise gestion des cartes réseau virtuelles
Solution : Ajout d’une seconde carte réseau + reconfiguration netplan

Ping impossible entre Linux et Windows
Cause : Blocage par le pare-feu Windows
Solution : Ajout d’une règle entrante dans le pare-feu Windows (ICMP autorisé)

Contrôle d’accès au partage
Cause : Paramétrage insuffisant de Samba (risque d’accès invité)
Solution : Configuration stricte des droits et utilisateurs Samba, tests de refus

Conclusion
Ce projet m’a permis de :

Renforcer ma polyvalence en environnements Windows et Linux.
Acquérir une expérience concrète en gestion de la sécurité réseau et de la virtualisation.
Développer des compétences de troubleshooting, essentielles en support IT et administration système.
