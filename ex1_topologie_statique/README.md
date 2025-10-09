# Exercice 1 - Projet SOHO

## Topologie

Deux LAN reliés par un routeur :

- Site A : 192.168.10.0/24
- Site B : 192.168.20.0/24

## Adressage

- Routeur R1 G0/0 → 192.168.10.1
- Routeur R1 G0/1 → 192.168.20.1
- PC-A1 → 192.168.10.11 / GW 192.168.10.1
- PC-B1 → 192.168.20.11 / GW 192.168.20.1
  (et ainsi de suite)

## Tests

Ping entre PC-A1 et PC-B1 : OK ✅
Ping entre PC du même LAN : OK ✅

## Menaces identifiées

1. ARP Spoofing / Man-in-the-Middle
2. Accès non autorisé sur un port de switch

## 💾 Fichiers Packet Tracer

Le fichier `.pkt` contient la topologie complète de l’exercice.
Il peut être ouvert avec **Cisco Packet Tracer** version 8.x ou supérieure.

- [Theo_FRANCOIS_Ex1_SOHO.pkt](Theo_FRANCOIS_Ex1_SOHO.pkt)
