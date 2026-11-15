# 01 · Pare-feu pfSense

## Installation
- **pfSense CE 2.9** dans une VM **VMware Workstation** (4 vCPU, 4 Go de RAM)
- 2 cartes réseau **vmxnet3** (passées d'e1000 à vmxnet3 : débit LAN en descente passé d'environ 50 à environ 436 Mbit/s)
  - **WAN** : réseau virtuel relié à la carte Ethernet intégrée → box opérateur
  - **LAN** : réseau virtuel relié à un adaptateur USB Gigabit → switch → appareils de la maison
- Administration en **HTTPS**, fuseau horaire et NTP configurés

## Règles LAN (de haut en bas)
Approche « maison » : on autorise Internet par défaut et on bloque ce qui est dangereux.

| # | Action | Rôle |
|---|---|---|
| 1 | Pass | Anti-lockout (accès admin) |
| 2 | Pass | Vers l'adresse virtuelle de pfBlockerNG (page de blocage) |
| 3 | Pass | Vers ntopng sur le pare-feu |
| 4 | Pass | DNS vers pfSense uniquement |
| 5 | Block | DNS extérieurs (alias `Ports_DNS_Externe` : 53, 853) |
| 6 | Block | Réseaux privés (alias `Reseaux_Prives` : 10/8, 172.16/12, 192.168/16) → le LAN ne peut pas joindre la box ni le réseau invités |
| 7 | Block | Ports dangereux (alias `Ports_Dangereux` : Telnet, RPC, NetBIOS, SMB, RDP, VNC) |
| 8 | Pass | Tout le reste vers Internet |

**WAN : aucune règle** → rien n'est joignable depuis Internet.

## DHCP et DNS
- Plage DHCP dynamique séparée d'une plage réservée aux **IP fixes** (serveur en réservation par adresse MAC)
- **DNS Resolver** (Unbound) avec liste d'accès limitée au LAN
- **Host Overrides** pour des noms locaux (`accueil.<domaine-local>`, `cloud.<domaine-local>`…)

## Sauvegarde
- Snapshot VMware avant chaque changement important
- Export du `config.xml` après chaque modification
