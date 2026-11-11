# s21-zigbee

Passerelle **Zigbee locale** pour thermopompes Daikin (série FTXM-W) via le port série **S21**, pour Home Assistant (Zigbee2MQTT). Aucun nuage, aucune API Daikin.

> **Statut : début de projet.** Rien n'est encore testé sur le matériel. Ce dépôt documente la démarche.

## Pourquoi

L'adaptateur Wi-Fi intégré des FTXM-W récents (firmware 3.1.0, `pv=3.40`) n'expose plus l'API locale `aircon/*` (404 sur tous les points d'accès; seul `/common/basic_info` répond). L'intégration native « Daikin AC » de Home Assistant ne peut donc pas fonctionner. Voir [docs/findings.md](docs/findings.md).

## Idée

```
Thermopompe (carte intérieure, port S21)
   │  UART 2400 bauds 8E2, logique 5 V
ESP32-H2 (routeur Zigbee)
   │  Zigbee (thermostat 0x0201 + fan_control 0x0202)
Zigbee2MQTT ── MQTT ── Home Assistant (entité climate)
```

## Plan

1. **Banc d'essai** : ESP32 ordinaire + ESPHome ([`esphome/`](esphome/)) pour valider la lecture/commande S21 sur FTXM12WVJU9.
2. **Option A** : ESP32-H2 avec ESPHome (`daikin_s21` + composant Zigbee).
3. **Option B** : firmware natif ESP-IDF ([`zigbee-h2/`](zigbee-h2/)), vrai thermostat Zigbee.
4. **Z2M** : convertisseur externe ([`z2m/`](z2m/)).
5. **HA** : carte thermostat ([`homeassistant/`](homeassistant/)).

## Matériel visé

- Intérieur FTXM12WVJU9 (fabriqué 2024-09, 208/230 V, R32), télécommande ARC466A70
- Connecteur blanc **S21** à 5 broches sur la carte intérieure (non câblé)
- ESP32 (banc d'essai), ESP32-H2 (final), convertisseur abaisseur 12–14 V → 3,3 V

## Sécurité

La carte intérieure est reliée au secteur. **Coupez le disjoncteur** avant d'ouvrir l'unité. Ouvrir l'appareil peut affecter la garantie. Le projet est fourni sans garantie.

## Remerciements et projets apparentés

- [revk/ESP32-Faikout](https://github.com/revk/ESP32-Faikout) (Faikin) et son wiki sur le protocole S21
- [joshbenner/esphome-daikin-s21](https://github.com/joshbenner/esphome-daikin-s21)
- [luar123/zigbee_esphome](https://github.com/luar123/zigbee_esphome)
- [Espressif esp-zigbee-sdk](https://github.com/espressif/esp-zigbee-sdk)

Aucun code de ces projets n'est copié ici; vérifier les licences avant toute reprise.

## Licence

MIT pour ce que nous écrivons ici. Voir [LICENSE](LICENSE).
