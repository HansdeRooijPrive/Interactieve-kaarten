# Interactieve-kaarten

Mobiele web-app met interactieve routekaarten voor meerdere reizen. Bij het
openen kies je een bestemming:

- **⛵ Zeilen · Griekenland** — routekaarten voor de Ionische Zee (offline).
- **🏍️ Rondrit · Schotland** — motorroutes in delen (deel 1: Dinnet → Ardullie).

## Live (GitHub Pages)

- **Productie** (stabiel, om te delen / als app toe te voegen):
  `https://hansderooijprive.github.io/Interactieve-kaarten/`
- **Test** (voorproefje van nieuwe wijzigingen, met "TEST"-lint):
  `https://hansderooijprive.github.io/Interactieve-kaarten/test/`

## Architectuur

- **`index.html`** — stabiele ingang die **niet wijzigt**. Leest `version.json`
  en opent automatisch de nieuwste app-versie. Dit is de URL die je op je
  startscherm zet.
- **`version.json`** — wijst naar de huidige versie, bv. `app-v1.1.html`.
- **`app-vX.Y.html`** — de volledige app (één bestand) met de versie-logica:
  een `APP_VERSIE`-object, een versie-chip en een "Over deze app"-changelog.
  Elke versie is een eigen bestand → cache-vrij.

### Nieuwe versie uitbrengen
1. Kopieer de huidige `app-vX.Y.html` naar een hoger versienummer.
2. Pas de app aan en voeg bovenaan `APP_VERSIE.historie` een regel toe
   (`soort`: `klein`/`middel`/`groot`) + bump `versie`/`datum`.
3. Zet `version.json` op het nieuwe bestand.

## Werkwijze: test → productie

Twee branches sturen twee omgevingen aan:

| Branch        | Omgeving   | URL         |
|---------------|------------|-------------|
| `main`        | Productie  | `/` (root)  |
| `development` | Test       | `/test/`    |

- Nieuwe wijzigingen commit je op **`development`**. Een push bouwt automatisch
  de test-omgeving (`/test/`). Die krijgt een zichtbaar **TEST**-lint en een
  eigen `localStorage`-sleutel, zodat test en productie elkaars gegevens niet
  raken.
- Ben je tevreden? Dan merge je `development` → **`main`**. Een push naar `main`
  publiceert de nieuwe versie op de **productie**-URL.

De deploys lopen via GitHub Actions
([`.github/workflows`](.github/workflows)); source van Pages staat op
"GitHub Actions".
