# Steam Deck Refurbished Monitor

Surveille la disponibilité des Steam Deck reconditionnés via l'API officielle Steam et envoie des alertes (Email / Discord).

## Fonctionnalités

- Utilise l'API officielle Steam (`CheckInventoryAvailableByPackage`)
- Surveille les 5 modèles : 64GB LCD, 256GB LCD, 512GB LCD, 512GB OLED, 1TB OLED
- Notifications Email (Gmail) et/ou Discord webhook
- Détection des changements de stock (évite le spam)
- Support multi-pays (FR, DE, US, UK, etc.)

## Déploiement GitHub Actions

### 1. Fork/Clone ce repo

```bash
git clone https://github.com/TON_USERNAME/steamdeck-monitor.git
```

### 2. Configurer les secrets

Dans ton repo GitHub : **Settings** → **Secrets and variables** → **Actions**

| Secret | Description | Requis |
|--------|-------------|--------|
| `EMAIL_FROM` | Ton adresse Gmail | Oui |
| `EMAIL_TO` | Adresse de destination | Oui |
| `EMAIL_PASSWORD` | [Mot de passe d'application Gmail](https://myaccount.google.com/apppasswords) | Oui |
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
pip install -r requirements.txt

# Définir les variables
export EMAIL_FROM="ton.email@gmail.com"
export EMAIL_TO="ton.email@gmail.com"
export EMAIL_PASSWORD="xxxx xxxx xxxx xxxx"
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
