# Port S21

Connecteur blanc 5 broches « S21 » sur la carte intérieure, juste sous le S16 (bleu, 4 broches), à côté de deux optocoupleurs (OIS200 / OIS201). Aucun fil branché d'origine. Le module Wi-Fi Daikin utilise S801 (5 fils).

## Brochage (broche 1 = côté triangle ▼ sur la carte)

| Broche | Fonction | Mesuré sur FTXM12WVJU9 (vs broche 5, unité sous tension) |
|---|---|---|
| 1 | 5 V (courant disponible inconnu) | 5 V à vide |
| 2 | TX de la thermopompe | 5 V au repos (UART inactif) |
| 3 | RX vers la thermopompe | 5 V au repos (rappel à 5 V côté thermopompe) |
| 4 | 12–14 V | **14,5 V** |
| 5 | GND | 0 V |

Série : **2400 bauds, 8 bits, parité paire, 2 bits d'arrêt (8E2)**, logique 5 V.
Source du brochage : wiki ESP32-Faikout. Les broches 1, 4 et 5 ont été confirmées à la main; 2 et 3 sont confirmées par leur tension au repos, pas encore par un échange de données.

## Connecteur
- Pas mesuré au pied à coulisse numérique : **2,04 à 2,08 mm** → pas de 2,0 mm.
- Compatible avec JST PA/PAP : boîtier **PAP-05V-S**, sertis **SPHD-001T-P0.5** (22–26 AWG). Non encore essayé physiquement.
- Kit Daikin EKRS21 : semble compatible, non vérifié.

## Conséquences pour le montage
- Alimenter l'ESP32 par la broche 4 via un abaisseur (entrée ≥ 20 V, sortie 5 V). Ne pas compter sur la broche 1 avant d'avoir mesuré son courant.
- Convertisseur de niveau 5 V ↔ 3,3 V sur les lignes 2 et 3; résistance série de 1 kΩ sur la ligne 3 pour le banc d'essai.
- Ne pas brancher l'USB de l'ordinateur pendant que le S21 alimente la carte.

## TODO
- [x] Photo de la carte, identification du S21
- [x] Mesure du pas (2 mm)
- [x] Tensions des broches 1 à 5
- [ ] Courant disponible sur la broche 1 (test sous charge)
- [ ] Premier échange S21 réel avec l'ESP32-C6
