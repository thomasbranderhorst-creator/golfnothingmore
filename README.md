# golfnothingmore.com

Landingspagina voor Golf, nothing more. Eén statische pagina, geen build, geen dependencies.

## Bestanden

- `index.html` — de hele pagina (CSS inline, lettertypen via Google Fonts)
- `hero.jpg` — de foto onder het formulier
- `favicon.svg` — het tabblad-icoon

## Lokaal bekijken

Open `index.html` in een browser. Meer is er niet.

## Live zetten

**Cloudflare Pages** (aanbevolen — dan staan DNS, hosting en e-mailforwarding op één plek)

1. Cloudflare-account, Workers & Pages → Create → Pages → Connect to Git
2. Kies deze repo, framework preset: **None**, build command: leeg, output directory: `/`
3. Custom domain toevoegen: `golfnothingmore.com` en `www.golfnothingmore.com`

**Netlify** — repo koppelen, build command leeg, publish directory `/`.

**GitHub Pages** — Settings → Pages → Source: Deploy from a branch → `main` / root. Custom domain invullen en "Enforce HTTPS" aanzetten.

## Nog te doen voordat dit echt live kan

- [ ] Inschrijfformulier koppelen aan een e-mailprovider (dubbele opt-in). Nu vangt het formulier de submit af en toont een melding; er wordt niets verstuurd.
- [ ] `privacy.html` schrijven en de link in de footer laten wijzen
- [ ] E-mailadressen op het domein: `hello@` en `partners@`
- [ ] Cover- en profielfoto's van de groep gelijktrekken met deze stijl
- [ ] Statistieken, cookieloos (Plausible of Umami) — scheelt een cookiebanner

## Aanpassen

Alle tekst staat gewoon in `index.html`. Kleuren en lettertypen staan bovenaan in `:root`, met een tweede set voor donkere modus eronder.
