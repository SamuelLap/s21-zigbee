# Banc d'essai ESPHome (ESP32-C6)

Fichier : [`bench-test.yaml`](bench-test.yaml). **Non testé** : à valider sur le matériel.
Copier `secrets.example.yaml` vers `secrets.yaml` (ignoré par git) et y mettre le Wi-Fi.

## Câblage (S21 → convertisseur de niveau → C6)

| S21 | Vers |
|---|---|
| 5 (GND) | GND commun (abaisseur, convertisseur, C6) |
| 4 (14,5 V) | Entrée de l'abaisseur Mini360, réglé à **5,0 V** avant de brancher la carte |
| 2 (TX thermopompe, 5 V) | HV1 du convertisseur; LV1 vers GPIO17 (RX du C6) |
| 3 (RX thermopompe) | HV2 du convertisseur; LV2 vers GPIO16 (TX du C6) |
| — | HV du convertisseur = 5 V de l'abaisseur; LV = 3V3 du C6 |

Broche 1 (5 V) : non utilisée pour l'instant. Ne pas brancher l'USB pendant que la carte est alimentée par l'abaisseur.

## Étapes
1. Flasher en USB-C (ESPHome), vérifier que la carte rejoint le Wi-Fi et apparaît dans Home Assistant.
2. Boucle : relier GPIO16 à GPIO17 et vérifier la réception (diagnostic `uart: debug`).
3. Brancher au S21 (disjoncteur coupé pour le câblage), remettre le courant et lire les journaux : la température intérieure et le mode doivent apparaître.
4. Seulement après des lectures cohérentes, essayer une commande (ex. consigne).

## Notes
- Si les lectures sont fausses, essayer l'inversion `invert: true` sur la broche RX (selon le montage) : un convertisseur BSS138 n'inverse pas, mais d'autres schémas oui.
- Certaines fonctions (POWERFUL, ECO) pourraient ne pas être commandables par S21 (discussion asund/esphome-daikin-s21 n° 202).
- Sur ESP32-C6, un fil de discussion HA mentionne des difficultés d'UART; si besoin, valider d'abord avec une boucle TX/RX.
