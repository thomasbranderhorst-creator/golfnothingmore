# MailerLite — teksten en instellingen

Alles hieronder is bedoeld om over te nemen in MailerLite. Volgorde is bewust:
zonder stap 1 komen de mails niet aan en is de rest zinloos.

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

Twice a month at most, golf offers only, and one click to leave
whenever you like.

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

— Twice a month at most. Often less. If there's nothing worth
  sending, we don't send.
— Deals only. No newsletter, no roundups, no checking in.
— We earn a commission on some of them and we'll say which ones.
  That never changes what we put in front of you.
— One click to leave, and it works straight away.

We're two people: Chris, who started the Golf, nothing more group
years ago, and Thomas, who now runs it day to day. The group is
246,000 golfers and it stays exactly what it was. This list is the
part where we go and find things worth buying.

If an offer is ever not worth your time, hit reply and say so. We
read everything that comes back.

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
