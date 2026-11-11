# Port S21

Connecteur blanc 5 broches « S21 » sur la carte intérieure (à côté de S16, bleu, 4 broches). Le module Wi-Fi Daikin utilise S801 (5 fils).

| Broche | Fonction | Notes |
|---|---|---|
| 1 | 5 V | pas toujours raccordée |
| 2 | TX de la thermopompe | logique 5 V |
| 3 | RX vers la thermopompe | 5 V; la plupart acceptent 3,3 V |
| 4 | 12–14 V | alimentation du module (abaisseur requis pour un ESP32) |
| 5 | GND | |

Câblage 1:1. Série : **2400 bauds, 8 bits, parité paire, 2 bits d'arrêt (8E2)**.

Source : wiki ESP32-Faikout (Wiring, S21 protocol). **À vérifier sur la vraie carte**, avec photo.

## Connecteur
- Unités récentes : JST PAP 2 mm (boîtier PAP-05V-S, sertis SPHD-001T-P0.5)
- Anciennes : JST EH 2,5 mm
- Kit Daikin EKRS21 : semble compatible, non vérifié

## TODO
- [ ] Photo de la carte (disjoncteur coupé)
- [ ] Confirmer le pas du connecteur
- [ ] Mesurer la tension de la broche 4 et le niveau logique de TX
