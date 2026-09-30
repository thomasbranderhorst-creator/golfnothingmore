# MailerLite — teksten en instellingen

Alles hieronder is bedoeld om over te nemen in MailerLite. Volgorde is bewust:
zonder stap 1 komen de mails niet aan en is de rest zinloos.

Voor het waarom achter de keuzes hieronder, en voor de checklist per
verzending, zie `deliverability.md` in deze map.

---

## 1. Domeinauthenticatie (eerst doen)

MailerLite → **Integrations / Domain authentication** → golfnothingmore.com.
Zij geven drie of vier DNS-records (DKIM, een return-path CNAME, soms een
tracking-CNAME). Die zet je bij Mijndomein erbij.

Let op: je hebt al een SPF-record voor Soverin. Maak er **geen tweede** aan —
één domein mag maar één SPF-record hebben. Voeg MailerLite's `include:` toe aan
het bestaande record.

Wacht tot MailerLite groen aangeeft voordat je iets verstuurt.

---

## 1b. Afzender en tracking

**Afzender**

```
From name:     Thomas · Golf, nothing more
From address:  thomas@golfnothingmore.com
Reply-to:      thomas@golfnothingmore.com
```

Niet `deals@`. Dat is een categoriewoord en dat is precies hoe het gelezen
wordt, door Gmail en door de lezer. `deals@` blijft bestaan als alias.

**Tracking**

Per campagne: **click tracking uit**, open tracking aan. MailerLite schrijft
anders elke link om naar een eigen trackingdomein, en dat is een vreemd domein
in een mail van ons.

We meten de kliks zelf. Alle links in de mail gaan naar
`golfnothingmore.com/go/<merk>/?src=email`. Die pagina stuurt een `Go`-event
naar Plausible met `brand`, `page` en `src`.

---

## 2. Bevestigingsmail (double opt-in)

**Onderwerp**

```
Confirm your email — Golf, nothing more
```

**Preheader**

```
One click and you're on the list.
```

**Body**

```
You asked for Member Deals. One click and you're on the list.

[ Confirm my email ]

Once a month, plus a short note when a new code lands. Golf offers
only, and one click to leave whenever you like.

One small favour while you're here. If this landed anywhere other
than your main inbox, drag it across. Otherwise the codes go to a
tab you never open.

If you didn't sign up, ignore this email. Nothing happens and we
delete the address.

Golf, nothing more
golfnothingmore.com
```

De knop wijst naar MailerLite's bevestigingslink. Verder geen afbeeldingen,
geen kolommen: een korte platte mail komt beter aan dan een opgemaakte.

---

## 3. Bedanktpagina

MailerLite → formulier → **na bevestiging doorsturen naar een eigen URL**:

```
https://golfnothingmore.com/thanks.html
```

Staat klaar in de repo. Vervangt MailerLite's eigen bedanktpagina.

---

## 4. Welkomstmail (automation, direct na bevestiging)

MailerLite → **Automations** → trigger: *when subscriber joins a group* →
delay: none.

**Onderwerp**

```
You're in
```

**Body**

```
That's it, you're on the list.

Here's what you signed up for, so there are no surprises later:

— Once a month, plus a short note when a new code lands. If there's
  nothing worth sending, we don't send.
— You see new codes first. A new partner code goes out in the
  email a week before it lands on the members page.
— Deals only. No newsletter, no roundups, no checking in.
— We earn a commission on some of them and we'll say which ones.
  That never changes what we put in front of you.
— One click to leave, and it works straight away.

We're two people: Chris, who started the Golf, nothing more group
years ago, and Thomas, who now runs it day to day. The group is
246,000 golfers and it stays exactly what it was. This list is the
part where we go and find things worth buying.

One question, and a real answer helps us more than you'd think:
what's the one thing you'd actually buy this year if the price was
right? Hit reply and tell us. We read every one.

Chris & Thomas
golfnothingmore.com
```

**Plek voor de foundercode**

Zodra Sandbag akkoord is komt hier één blok bij, tussen de opsomming en
"We're two people":

```
You're one of the first 500 on this list, which gets you [aanbod],
using the code below. It isn't available anywhere else.

[ CODE ]
```

Nu nog niet toevoegen — de deal bestaat pas als er getekend is.

---

## 5. Wat er in het formulier veranderd is

- **Honeypot toegevoegd.** Een verborgen veld dat alleen bots invullen. Wordt
  het ingevuld, dan tonen we wel de bevestigingstekst maar versturen we niets.
- **Beperking die blijft:** de site praat met MailerLite via `mode: 'no-cors'`,
  dus de browser mag het antwoord niet lezen. We weten dus niet of MailerLite
  het adres accepteerde. Daarom zegt de tekst "check your inbox" en niet "je
  staat erop" — dat laatste zouden we niet kunnen waarmaken.

---

## 6. Adressen uit de toetredingsvraag

Niet importeren. Zie de uitleg in het gesprek: die mensen gaven hun adres voor
een gratis les, niet voor Member Deals. Dat is geen geldige toestemming, het is
in strijd met MailerLite's eigen voorwaarden, en het is de snelste manier om je
bezorging te slopen voordat je één echte mailing hebt verstuurd.
