# Basic Networking

## OSI model

![Untitled](Basic%20Networking%2009fc9ee80932423c8271e71b6fedf98b/Untitled.png)

**phrase mnémotechnique** : ***A Peine Serré, Tu Rends Le Portefeuille*** 

4/**Transport** : Protocoles communs = 

- TCP ( précision → si une donnée est perdue elle est renvoyée )
- UDP ( rapidité → ne s'intéresse pas aux données perdues durant le trajet )

La couche va découper la transmission en pièces de la taille d'un bit ( segments si TCP et datagrams si UDP

3/**Réseau** 

Localise la destination de la requête avec l'adressage logique ( ex : IP )

2/**Liaison** 

S'occupe de l'adressage physique → reçoit les paquets et ajoute l'adresse MAC du récepteur 

→ chaque appareil qui va sur le réseau a une NIC avec une adresse MAC unique 

→ présente la data dans un format correct et vérifie que rien n'est corrompu 

1/**Physique** 

Binary data → signal → binary data

## TCP/IP Model ( ce qui se passe vraiment )

![Untitled](Basic%20Networking%2009fc9ee80932423c8271e71b6fedf98b/Untitled%201.png)

vérification que la connexion est stable → **Three-way Handshake** :

![Untitled](Basic%20Networking%2009fc9ee80932423c8271e71b6fedf98b/Untitled%202.png)

## Encapsulation :

![Untitled](Basic%20Networking%2009fc9ee80932423c8271e71b6fedf98b/Untitled%203.png)

Quand l'ordi reçoit → de-encapsulation 

## Firewalls ( couche réseau et transport )

La PAF du réseau → admin configure pour "permit" ou "deny" selon différents facteurs :

- D'où le trafic vient ?
- Où il va ?
- Pour quel port est le trafic ?
- Quel protocole est utilisé ( TCP ? UDP ?... )

→ packet inspection

### Deux catégories de pare-feu :

- **Stateful** : se base sur l'info entière

→ gourmand en ressources / + problème → si une connexion de l'hôte est mauvaise il bloque tout

- **Stateless** : Set de règles pour des paquets individuels

→ moins gourmand mais plus bête car très dépendant des règles

→ utile pour bloquer les DDOS

## VPN Basics

Virtual Private Network

→ permet de connecter des appareils à travers un "tunnel" qui forme leur propre réseau privé

→ protège du sniffing ( analyse de trafic pour repérer des infos )

→ anonymat ( sauf si il y a des logs dans le service VPN )

### Quelques technologies VPN :

- PPP : Authentication and encryption

→ grâce à une clé privée et un certificat public ( ~SSH sur le principe ) 

→ non-routable 

- PPTP : utilise PPP et permet à la data du PPP de voyager et de quitter le réseau

→ faiblement encrypté et pas facile

- IPSec : utilise l'IP framework

→ difficile à mettre en place mais fortement encrypté + bien supporté