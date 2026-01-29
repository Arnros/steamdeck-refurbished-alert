# Steam Deck Refurbished Monitor

Surveille la disponibilité des Steam Deck reconditionnés via l'API officielle Steam et envoie des alertes Signal.

## Fonctionnalités

- Utilise l'API officielle Steam (`CheckInventoryAvailableByPackage`)
- Surveille les 5 modèles : 64GB LCD, 256GB LCD, 512GB LCD, 512GB OLED, 1TB OLED
- Notifications Signal (via CallMeBot) et/ou Discord
- Détection des changements de stock (évite le spam)
- Support multi-pays (FR, DE, US, UK, etc.)

## Déploiement GitHub Actions

### 1. Configurer Signal avec CallMeBot

1. Ajoute ce numéro à tes contacts Signal : **+34 644 52 74 88**
2. Envoie-lui ce message : `I allow callmebot to send me messages`
3. Tu recevras une réponse avec ton **apikey**

Source: https://www.callmebot.com/blog/free-api-signal-send-messages/

### 2. Configurer les secrets GitHub

Dans ton repo : **Settings** → **Secrets and variables** → **Actions**

| Secret | Description | Requis |
|--------|-------------|--------|
| `SIGNAL_PHONE` | Ton numéro (ex: +33612345678) | Oui |
| `SIGNAL_APIKEY` | Clé API reçue de CallMeBot | Oui |
| `DISCORD_WEBHOOK` | URL webhook Discord | Non |

### 3. Activer le workflow

- Va dans l'onglet **Actions**
- Active les workflows
- Le script s'exécute automatiquement toutes les 5 minutes

## Configuration

Variables d'environnement dans `.github/workflows/monitor.yml` :

```yaml
env:
  COUNTRY_CODE: FR  # FR, DE, US, UK, etc.
```

## Usage local

```bash
pip install requests

export SIGNAL_PHONE="+33612345678"
export SIGNAL_APIKEY="ton_apikey"
export COUNTRY_CODE="FR"

python monitor_api.py
```

## API Steam utilisée

```
GET https://api.steampowered.com/IPhysicalGoodsService/CheckInventoryAvailableByPackage/v1
    ?origin=https://store.steampowered.com
    &country_code=FR
    &packageid=903905
```

| Package ID | Modèle |
|------------|--------|
| 903905 | 64GB LCD |
| 903906 | 256GB LCD |
| 903907 | 512GB LCD |
| 1202542 | 512GB OLED |
| 1202547 | 1TB OLED |

## Credits

Inspiré par [oblassgit/refurbished-steam-deck-notifier](https://github.com/oblassgit/refurbished-steam-deck-notifier)
