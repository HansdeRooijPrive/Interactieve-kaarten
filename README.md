# Zeilen-Griekenland — Sunny Sailing · Routekaarten

Mobiele web-app met zeilroutekaarten voor een zeilvakantie in Griekenland.
De volledige applicatie zit in één bestand: [`index.html`](index.html).

## Live (GitHub Pages)

- **Productie** (stabiel, om te delen / als app toe te voegen):
  `https://hansderooijprive.github.io/Zeilen-Griekenland/`
- **Test** (voorproefje van nieuwe wijzigingen, met "TEST"-lint):
  `https://hansderooijprive.github.io/Zeilen-Griekenland/test/`

## Werkwijze: test → productie

Twee branches sturen twee omgevingen aan:

| Branch        | Omgeving   | URL                         |
|---------------|------------|-----------------------------|
| `main`        | Productie  | `/` (root)                  |
| `development` | Test       | `/test/`                    |

- Nieuwe wijzigingen commit je op **`development`**. Een push bouwt automatisch
  de test-omgeving (`/test/`). Die krijgt een zichtbaar **TEST**-lint en een
  eigen `localStorage`-sleutel, zodat test en productie elkaars gegevens niet
  raken.
- Ben je tevreden? Dan merge je `development` → **`main`**. Een push naar `main`
  publiceert de nieuwe versie op de **productie**-URL.
- De productie-URL wijzigt dus alleen wanneer je bewust naar `main` publiceert;
  meerdere mensen kunnen die stabiel benaderen en als app aan hun startscherm
  toevoegen.

De deploys lopen via GitHub Actions
([`.github/workflows`](.github/workflows)); source van Pages staat op
"GitHub Actions".

## Ontwikkeling

Dit is een statische single-file web-app — geen build-stap of dependencies nodig.
Wijzig `index.html` en ververs de browser.
