# /swing-review/

Eigen pagina voor de ledendeal van deze maand: een gratis swing review,
geleverd door partner Sandbag. Uitleg en vertrouwen op ons eigen domein,
daarna door naar de upload bij Sandbag met onze bron erin.

We slaan zelf geen video's op en sturen geen adressen door.

## De links die we gebruiken

| Waar | Link | Wat de bezoeker ziet |
|---|---|---|
| Manychat, na het e-mailadres | `https://golfnothingmore.com/swing-review?src=messenger` | Meteen de uitleg en de knop **Upload my swing**. Geen formulier. |
| Deals-reel | `https://golfnothingmore.com/swing-review?src=reel` | Eerst **Join Member Deals to unlock this deal**. Na het versturen verschijnt de knop. |
| Post in de groep | `https://golfnothingmore.com/swing-review?src=post` | Zelfde als reel. |
| Zonder `src` | `https://golfnothingmore.com/swing-review` | Zelfde als reel. Bron wordt `swing-review`. |

Alleen bronnen die in `CONFIG.TRUSTED_SOURCES` staan slaan het formulier over.
Nu is dat alleen `messenger`, want dat is de enige route waar het adres al is
gegeven. Wil je er later een bij, zet hem dan in die lijst en nergens anders.

## Instellingen

Alles staat bovenaan het `<script>` in `index.html`, in `CONFIG`:

- `PARTNER_URL` — de uploadlink van Sandbag. `{src}` wordt vervangen door de bron.
- `ML_ACCOUNT_ID` / `ML_FORM_ID` — MailerLite, gelijk aan de homepage.
- `TRUSTED_SOURCES` — bronnen die het formulier overslaan.
- `DEFAULT_SOURCE` — waarde als er geen `?src` in de URL staat.
- `EVENT_NAME` — naam van het Plausible-event.

## Meten

Plausible krijgt naast de pageview een event `Swing review` met twee props:

- `src` — de bron uit de URL
- `step` — `view-direct`, `view-gated`, `signup` of `upload`

Daarmee zie je per bron hoeveel mensen binnenkwamen, hoeveel er inschreven
en hoeveel er doorklikten naar Sandbag.

## Nog open

- [ ] **`PARTNER_URL`**: Jasons GNM-link van Sandbag. Staat nu op
  `TODO_JASON_GNM_LINK?src={src}`. Zolang daar `TODO_` in staat is de knop
  bewust uitgeschakeld en stuurt hij niemand naar een dode URL.
- [x] **Veld `source` in MailerLite**: bestaat niet onder die naam. Het veld
  heet `signup_source` en werd al gebruikt door de homepage (waarden `site`,
  `intro`, `welcome`). Deze pagina schrijft daar de `src` in, of
  `swing-review` als er geen `src` is. Er hoeft niets nieuws aangemaakt te
  worden.

## Let op

De pagina staat op `noindex, nofollow`. Hij hoort niet in Google, want hij is
bedoeld voor mensen die de link van ons krijgen.
