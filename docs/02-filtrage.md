# 02 · Filtrage : pfBlockerNG et CrowdSec

## pfBlockerNG
- **Listes IP** : blocage des adresses connues comme malveillantes (entrant et sortant)
- **DNSBL** : blocage des domaines de pubs, trackers et malwares, avec plusieurs listes dont celles de **HaGeZi**
- Adresse virtuelle dédiée pour la page de blocage, autorisée par une règle LAN placée au-dessus des blocages
- **Blocage DoH/DoT** : empêche les navigateurs et applis de contourner le DNS de pfSense

> Constat : un navigateur avec VPN intégré ou « DNS sécurisé » contourne complètement le filtrage. D'où le blocage des DNS extérieurs dans les règles du pare-feu.

## CrowdSec
- Installé sur pfSense : moteur d'analyse des journaux + composant de remédiation (bouncer pare-feu)
- Connecté à l'API centrale CrowdSec pour recevoir la **blocklist communautaire**
