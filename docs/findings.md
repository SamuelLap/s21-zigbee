# Constats sur FTXM12WVJU9

## Adaptateur Wi-Fi intégré
- SSID de configuration `DaikinAP97851`, firmware 3.1.0, `pv=3.40`, `adp_kind=4`, `api_ver=1_0`, `reg=us`
- `GET /common/basic_info` : fonctionne
- `aircon/get_sensor_info`, `get_control_info`, `get_model_info`, points d'accès d'énergie, et BRP084 (`/dsiot/...`) : **404**
- Conséquence : l'intégration native Home Assistant échoue (`cannot_connect`).

## Menu Wi-Fi de la télécommande
Unité éteinte, maintenir POWERFUL/Wi-Fi ~5 s. Options : WPS, AP, statut, réinitialisation, OFF. Confirmer en maintenant ~2 s. Le comportement du voyant orange distingue les options (numérotation non confirmée).

## Précédent
Discussion asund/esphome-daikin-s21 n° 202 : un FTXM12WVJU9 `pv 3.40` répond à toutes les lectures S21 mais refuse deux commandes d'écriture étendues. Certaines fonctions (POWERFUL, ECO) pourraient ne pas être commandables par S21.
