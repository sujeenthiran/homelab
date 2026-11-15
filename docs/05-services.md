# 05 · Services auto-hébergés

Tous les services tournent en **Docker Compose** sur un serveur Debian, derrière le reverse proxy **Caddy**.

| Service | Rôle |
|---|---|
| **Nextcloud** (+ MariaDB, Redis, cron) | Cloud familial : photos, fichiers, un compte séparé par personne, données sur un disque dédié |
| **Mon SOC** | Tableau de bord sécurité maison → [dépôt mon-soc](https://github.com/sujeenthiran/mon-soc) |
| **Homepage** | Page d'accueil avec tous les services |
| **Caddy** | Reverse proxy : un nom local par service, seul point d'entrée HTTP |

## Bonnes pratiques appliquées
- Les ports des conteneurs sont liés à **127.0.0.1** : seul Caddy est joignable depuis le réseau
- Noms de domaine locaux servis par le DNS de pfSense
- Secrets dans des fichiers `.env` non versionnés

Exemples de configuration : [configs/](../configs)
