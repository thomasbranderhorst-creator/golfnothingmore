# Bezorging · e-mail

Naar aanleiding van het gesprek met Jason Kellerman, 29 september 2026.
Dit gaat over één ding: komt de mail in de gewone inbox terecht, of in
Promotions en spam. Jason: in Promotions zitten staat gelijk aan niet
verzonden hebben.

---

## Wat Jason vertelde

- Deliverability is "het verschil tussen slagen en falen". Ook bij mensen
  die zich zelf hebben aangemeld.
- Hij heeft zijn verzendadres opgewarmd en beheert de DKIM-records zelf.
- Houd ongeveer twintig eigen adressen aan waar je elke mailing ook
  naartoe stuurt, en kijk per adres: inbox, Promotions of spam. Anders weet
  je het niet, want een open rate zegt niets over waar de mail belandde.
- Zijn cijfer na zes weken intensief werk, bij volledig opt-in gebruikers:
  **60 procent inbox, 40 procent Promotions**.
- Daarom stapt hij over op sms. Telefoonnummers bleek hij net zo vaak te
  krijgen als e-mailadressen, ongeveer 20 procent.
- Zijn rekensom: tien aanmeldingen per dag, 20 procent opent, 10 procent doet
  iets. Dat is 0,2 per dag. "I don't care if you multiply that by 100."

---

## Wat dat voor ons betekent

We hebben 62 abonnees. Het IP waarmee verstuurd wordt is van MailerLite en
wordt gedeeld, dus die reputatie is niet van ons. Opwarmen in de klassieke zin,
volume langzaam opbouwen, doet bij 62 adressen vrijwel niets.

Wat wel van ons is: **authenticatie, afzender, inhoud en betrokkenheid**.
Daar zit alle winst, en de eerste mailing bepaalt hoe Gmail ons daarna
inschaalt. Dus die moet goed.

De eerlijke verwachting voor de eerste: 62 ontvangers, bij een verse
double-opt-in lijst opent 35 tot 50 procent, en klikt daarvan 10 tot 20
procent. Dat zijn twee tot zes kliks. Dat is geen mislukking, dat is de
lijstgrootte. De lijst laten groeien is de hefboom, niet vaker mailen.

---

## Voor elke verzending

### 0. Stopconditie

MailerLite → **Domain authentication** → golfnothingmore.com moet **groen**
staan. Staat het niet groen, dan niet verzenden. Dit is het enige punt uit
deze lijst waarop je moet wachten.

### 1. DNS zelf nakijken, twee minuten

Ga naar `mxtoolbox.com/SuperTool.aspx` en doe drie lookups:

| Lookup | Wat je wilt zien |
|---|---|
| `spf:golfnothingmore.com` | **Eén** SPF-record, met daarin zowel Soverin als de `include:` van MailerLite. Twee SPF-records is fout en breekt allebei. |
| `dmarc:golfnothingmore.com` | `v=DMARC1; p=none; rua=mailto:...` |
| `txt:<selector>._domainkey.golfnothingmore.com` | De DKIM-sleutel. De selector staat in MailerLite bij de records die zij je gaven. |

DKIM en SPF zijn verplicht. DMARC is pas verplicht boven 5.000 mails per dag
naar Gmail, daar zitten we ver onder, maar het record kost niets en je krijgt
er rapporten van terug. Zet hem op `p=none` en laat hem staan.

### 2. Afzender: weg bij `deals@`

`deals@golfnothingmore.com` is een categoriewoord. Het is precies wat een
promotieafzender heet, voor Gmail en voor de lezer. Mensen openen mail van
een persoon.

- **From name:** `Thomas · Golf, nothing more`
- **From address:** `thomas@golfnothingmore.com`
- **Reply-to:** hetzelfde adres, en dat moet echt gelezen worden

`deals@` laten bestaan als alias, dan breekt er niets. Nu overstappen kost
niets omdat de lijst 62 mensen is. Over een jaar bij 5.000 kost het wel wat.

### 3. Kliktracking uit

MailerLite schrijft elke link in je mail om naar een eigen trackingdomein.
Dat is een vreemd domein in een mail van ons, en het is een van de signalen
waar filters naar kijken.

MailerLite → campagne → **Settings → Tracking → click tracking uit**.

We verliezen daar niets mee, want we meten het nu zelf: alle links in de mail
gaan naar `golfnothingmore.com/go/<merk>/?src=email` en die pagina stuurt een
`Go`-event naar Plausible met `brand`, `page` en `src`. Zelfde data, en op ons
eigen geauthenticeerde domein.

**Open tracking laten we wel aan.** Dat is één pixel, en het is het enige
signaal dat we hebben over of de mail geopend wordt.

### 4. Inhoud

Wat een mail naar Promotions duwt is vooral de vorm, niet de afzender.

- **Onderwerp:** geen `deal`, `discount`, `free`, `%`, `off`, geen hoofdletters,
  geen emoji. Schrijf alsof je één iemand schrijft.
- **Preheader:** een echte zin. Niet "view in browser".
- **Eerste regel:** een vraag waar iemand op kán antwoorden. Een reply is het
  sterkste positieve signaal dat er bestaat voor Gmail.
- **Links:** zo weinig mogelijk, richtlijn maximaal vier. Een mail met tien
  merklinks is een folder, en wordt ook zo ingedeeld.
- **Geen afbeelding bovenaan, geen kolommen, geen knoppenbalk.** Platte opmaak,
  zoals de bevestigingsmail.
- **Plain-text versie** moet overeenkomen met de HTML. MailerLite genereert hem,
  kijk hem één keer na.
- **Onderaan:** namen, geen bedrijfsblok.
- **P.S.:** vraag om een antwoord. Concreet, één vraag.

### 5. Seedadressen

Jason zegt twintig. Realistisch voor ons zijn er zes tot acht, maar dan wel
**echte, losse accounts**.

Let op: `thomas+test@gmail.com` en puntjes in een Gmail-adres komen in
**dezelfde** inbox en krijgen **dezelfde** indeling. Als seed zijn ze waardeloos.

| # | Adres | Provider |
|---|---|---|
| 1 | | Gmail (Thomas) |
| 2 | | Gmail (Chris) |
| 3 | | Gmail (nieuw, alleen hiervoor) |
| 4 | | Outlook / Hotmail |
| 5 | | Yahoo |
| 6 | | iCloud |
| 7 | | familie of vriend, Gmail |
| 8 | | familie of vriend, willekeurig |

Zet ze in een aparte groep in MailerLite en voeg die groep toe aan elke
verzending.

Daarnaast, vlak voor elke verzending: stuur een test naar het adres dat
**mail-tester.com** je geeft. Gratis, en je krijgt binnen een minuut een score
plus wat er precies aan mankeert: SPF, DKIM, DMARC, spamwoorden, verhouding
tekst tot afbeelding, blacklists.

### 6. Vlak na verzending

- Loop de seedadressen langs en vul het meetblad hieronder in.
- Beantwoord elk antwoord dat binnenkomt, binnen het uur. Elk antwoord dat
  wij terugsturen is opnieuw een positief signaal.

---

## Meetblad

Eén regel per verzending. Dit is het enige wat we over bezorging echt weten.

| Datum | Onderwerp | Verstuurd | Inbox | Promotions | Spam | mail-tester | Opens | Kliks | Uitschrijvingen |
|---|---|---|---|---|---|---|---|---|---|
| | | | | | | | | | |

Wat je eruit wilt halen: het aandeel **inbox** over de tijd. Jason zit op 60
procent. Onder de 50 is er iets mis met de inhoud of de authenticatie. Boven
de 70 doen we het beter dan hij.

---

## Wat we bewust niet doen

- **Adressen uit de toetredingsvraag importeren.** Die mensen gaven hun adres
  voor een gratis les, niet voor Member Deals. Geen geldige toestemming, in
  strijd met de voorwaarden van MailerLite, en de snelste manier om de
  bezorging te slopen voordat er één echte mailing uit is.
- **Vaker mailen om meer resultaat te krijgen.** Bij 62 abonnees is de lijst de
  beperking, niet de frequentie. En de belofte van één mail per maand staat op
  zes plekken op de site.

## Wat later kan

Telefoonnummer vragen in plaats van of naast het e-mailadres. Jason kreeg er
net zoveel als e-mailadressen, 20 procent, en de open rate daarvan is bijna
100 procent. Voor ons betekent dat WhatsApp, en dan wel met een echte
aanvinkbare toestemming erbij. Niet nu, wel noteren.
