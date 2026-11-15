# 06 · Audit de sécurité avec Kali

## Méthode
1. **Découverte des hôtes** du LAN : `nmap -sn <réseau-LAN>`
2. **Scan complet des ports** du pare-feu et du serveur : `nmap -p- -sV <cible>`
3. Analyse : qu'est-ce qui est exposé, et est-ce nécessaire ?
4. Corrections, puis **nouveau scan** pour vérifier

## Constats
| Cible | Avant | Analyse |
|---|---|---|
| pfSense | DNS, interface web, ntopng | Normal, tout le reste est filtré |
| Serveur | 5 ports : SSH, Caddy, et 3 applis Docker en accès direct | Les applis contournaient le reverse proxy ; SSH acceptait les mots de passe |

## Corrections
- Ports Docker liés à `127.0.0.1` → les applis ne sont joignables que via **Caddy**
- SSH : **clé ed25519 uniquement** (`PasswordAuthentication no`), **root interdit** (`PermitRootLogin no`)

## Résultat
Second scan : le serveur n'expose plus que **2 ports** (SSH par clé + reverse proxy). **5 → 2**.
