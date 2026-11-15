# 03 · QoS anti-latence (FQ-CoDel)

## Problème
Quand quelqu'un télécharge ou envoie un gros fichier, le ping explose (« bufferbloat ») : lag en jeu, visio qui saccade.

## Solution
- Deux **limiteurs** pfSense avec l'algorithme **FQ-CoDel** : un pour la descente, un pour la montée
- Limites réglées un peu sous le débit réel, pour que la file d'attente reste dans pfSense et non dans la box
- Règle **Floating** de type *Match* sur le WAN qui envoie le trafic dans ces files

## Résultat
- Test de bufferbloat : **A+**
- Choix assumé : un peu moins de débit maximum en échange d'un ping stable
