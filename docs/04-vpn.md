# 04 · Accès distant : VPN Tailscale

## Pourquoi Tailscale
Accéder au réseau de la maison depuis le téléphone **sans ouvrir de port** sur la box ni sur pfSense (Tailscale est basé sur WireGuard et passe en sortant).

## Mise en place
- Tailscale installé sur le serveur Debian
- **Subnet router** : le serveur annonce le réseau LAN, le téléphone joint tous les services de la maison
- **Exit node** : possibilité de faire sortir tout le trafic du téléphone par la maison (utile sur un Wi-Fi public)
- **DNS global du tailnet → pfSense** : le filtrage pfBlockerNG s'applique même en 4G/5G
- HTTPS valide pour Nextcloud via `tailscale serve`, accessible seulement aux appareils du tailnet
