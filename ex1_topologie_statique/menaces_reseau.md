# 🔒 Menaces identifiées sur la topologie réseau (Exercice 1 - Projet SOHO)

## 🧭 Contexte

Le réseau étudié est constitué de deux LAN interconnectés par un routeur :

- **Site A** : 192.168.10.0/24
- **Site B** : 192.168.20.0/24
- Le routeur R1 assure la communication entre les deux réseaux.

Ce type d’infrastructure est typique d’une PME : simple, mais vulnérable à certaines attaques s’il n’est pas correctement sécurisé.

---

## ⚠️ Menace n°1 : Attaque ARP Spoofing (ou ARP Poisoning)

### 🧩 Description

Le protocole **ARP (Address Resolution Protocol)** permet à un équipement du réseau de découvrir l’adresse MAC associée à une adresse IP.  
Ce protocole **ne comporte aucune authentification** : tout appareil peut envoyer des réponses ARP, même si elles sont fausses.

Un attaquant connecté sur le LAN (ex : un PC malveillant branché au switch du Site A) peut :

- Envoyer de **fausses réponses ARP** au reste du réseau.
- Faire croire qu’il est le **routeur** (ou un autre poste).
- Intercepter, modifier ou rediriger le trafic réseau entre les machines (attaque **Man-in-the-Middle**).

### 🎯 Conséquences

- Interception de données sensibles (identifiants, mots de passe, mails, etc.)
- Redirection du trafic vers un serveur pirate.
- Perturbation de la communication entre les deux sites.

### 🛡️ Contremesures

- **Activer la sécurisation ARP** sur les switches (`Dynamic ARP Inspection` sur matériel Cisco).
- Utiliser des **tables ARP statiques** sur les machines critiques.
- Segmenter le réseau avec des **VLANs** pour limiter la portée d’une attaque locale.
- Surveiller le trafic avec un **IDS/IPS** (ex : Snort).

---

## ⚠️ Menace n°2 : Accès non autorisé au réseau interne (Rogue Device)

### 🧩 Description

Sur un réseau d’entreprise non protégé, un utilisateur peut **brancher un PC personnel** ou un **appareil inconnu** (comme une clé Wi-Fi, un NAS, etc.) sur un port libre du switch.  
Une fois connecté, cet appareil obtient un accès direct au réseau interne et peut :

- Scanner les adresses IP internes.
- Lancer des attaques (brute force, sniffing, etc.).
- Propager des virus ou malwares.

### 🎯 Conséquences

- Compromission du réseau interne.
- Perte ou vol de données sensibles.
- Risque de ransomware ou d’intrusion à distance.

### 🛡️ Contremesures

- Mettre en place une **politique de contrôle d’accès** réseau :
  - **Port Security** sur les switches (limiter le nombre d’adresses MAC autorisées par port).
  - Désactiver les ports inutilisés.
  - Authentification 802.1X pour les utilisateurs.
- Surveiller régulièrement la **table MAC du switch** pour détecter des appareils non connus.
- Isoler les visiteurs dans un **VLAN “invité”** sans accès au réseau interne.

---

## ⚠️ Autres menaces possibles

- **Sniffing réseau** : capture de paquets non chiffrés circulant sur le LAN.
- **Propagation de malware** : via un poste compromis.
- **Attaque DoS interne** : saturation du switch ou du routeur.

---

## 🧠 Conclusion

La topologie SOHO de base est fonctionnelle mais vulnérable sans politiques de sécurité adaptées.  
Une bonne hygiène réseau repose sur :

- Une segmentation logique (VLAN, sous-réseaux),
- Des contrôles d’accès (Port Security, 802.1X),
- Et une surveillance active du trafic.

---

_Auteur : Théo FRANCOIS_  
_Formation : Wild Code School - TSSR_  
_Date : 09/10/2025_
