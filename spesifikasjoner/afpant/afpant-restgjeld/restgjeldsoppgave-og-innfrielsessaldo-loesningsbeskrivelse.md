Innfrielsessaldo
================

>Digital samhandling ved eiendomshandel
> 
><bjorn.soland@bits.no>

# Innledning

I Norge er eiendomsmeglingsvirksomhet strengt regulert for å beskytte
forbrukerne i deres viktigste økonomiske investering1. Eiendomsmegleren
har plikt til å handle i tråd med god meglerskikk, og ivareta både
selgers og kjøpers interesser.

Dette innebærer blant annet at meglere innhenter skriftlig bekreftelse
på restgjeld fra panthavere i forkant, og hvor de bekrefter at pant blir
slettet ved innfrielse av nevnte lån. Det er heller ikke anledning til å
låne opp på eksisterende pant uten samtykke når megleren har etablert
sikring og panthavere har avgitt restgjeldsoppgave.

Ved oppgjørsdato, som regel ved overtakelse, er det meglers oppgave å
foreta oppgjøret. Megler innhenter da innfrielsessaldoen, et dokument
som gir en nøyaktig oversikt over det totale beløpet som gjenstår å
betale på lånet. Saldoen inkluderer påløpte og fremtidige renter på
gitte oppgjørsdatoer, samt eventuelle gebyrer.

Spesifikasjonen inkluderer også bankbytte. Bankbytte er et forhold
mellom låntaker og de involverte bankene og involverer ikke megler.

Denne funksjonelle spesifikasjonen beskriver både Restgjeldsoppgave og
Innfrielsessaldo. Tekniske spesifikasjoner utarbeides på bakgrunn av
kravene i denne spesifikasjonen.

# Avgrensninger

I dette kapittelet avgrenser vi oppgaven – hva løser vi ikke

* Oppgaver som har egne aktiviteter i DSVE og således ikke er en del av denne spesifikasjonen:
  * Pantefrafall (sletting av pant uten full innfrielse av lån)
  * Oppfordring om sletting (purring)
  * Bekreftelse på sletting av pant
* Håndtering av “spesialsaker” som ved fastrente og tredjemannspant/kausjon
  * Komplekse knytningsmatriser
  * Generalfullmakter og blankoskjøter

Disse må inntil videre håndteres som i dag.

# Beskrivelse av Restgjeld- og saldoforespørsel

## Overordnet flyt 

Flyten for innhenting av restgjeldsoppgave og innfrielsesoppgave er
identisk, men innholdet i meldingene er forskjellig.

![](./figurer/flyt.drawio.svg)

## Restgjeldsoppgave

Innhenting av restgjeldsoppgave på hjemmelshavers eiendom. Meglere
etterspør informasjon om restgjeld etter oppdragsinngåelse for å avdekke
om eiendommen er overbeheftet og om man må gjøre tiltak som å be om
pantefrafall fra en eller flere kreditorer. Når restgjeld etterspørres
er eiendommen enda ikke solgt, og megler vet foreløpig ikke
overtakelsesdato. Man er her ikke ute etter helt nøyaktig rentebærende
saldo. Banker kan også be om restgjeldsoppgave i forbindelse med
bankbytte/ny lånesak

## Innfrielsessaldo

Etter at eiendommen er solgt, og oppgjørsavdelingen forbereder
oppgjøret, etterspørres innfrielsessaldo fra kreditorene. Dette gjøres
tett på eller etter overtakelse. Svar på denne haster derfor mer enn for
restgjeld. Saldoen skal oppgis på en liste med datoer og skal angi saldo
inkludert renter på gitte datoer. Det er på dette tidspunktet viktig at
megler også mottar alle betalingsopplysninger for å kunne gjøre klart
oppgjøret. Denne meldingen kan også banker benytte når kunden har fått
innvilget lån i en annen bank og den nye banken skal gjøre opp
restgjelden i ny bank

# Informasjonselementer i de ulike meldingene

| Informasjonselement                                                                                                                                                                                    | Format       | Restgjelds-oppg. spm. | Restgjelds-oppg. svar | Innfrielse spm. | Innfrielse svar |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|----------------------|-----------------------|-----------------|-----------------|
| Mottakers referanse                                                                                                                                                                                    | DSVE-standard |                      | X*                    | X               | X*              |
| Avsenders referanse                                                                                                                                                                                    | DSVE-standard | X*                   | X*                    | X*              | X*              |
| Eiendomsinformasjon (liste over eiendommer):<ul><li>Fast eiendom/seksjon: Matrikkelinformasjon</li><li>Brl. leil: Org. nr og andelsnummer</li> <li>Aksjeleilighet: org.nummer og aksjenummer</li></ul> | DSVE-standard | X*                   | X*                    | X*              | X*              |
| Prisanslag (<u>anslag</u> - ikke bindende)                                                                                                                                                             |              | X                    | X                     |                 |                 |
| Hjemmelshaver                                                                                                                                                                                          | DSVE-standard | X*                   | X*                    | X*              | X*              |
| Liste over dagbok-/dokumentnummer                                                                                                                                                                      |              | X*                   | X*                    | X*              | X*              |
| Avsenders kontaktinformasjon                                                                                                                                                                           | DSVE-standard | X*                   |                       | X*              |                 |
| Mottakers kontaktinformasjon                                                                                                                                                                           | DSVE-standard |                      | X*                    |                 | X*              |
| Betalingsinformasjon (nødvendig informasjon for innfrielse)<ul><li>Lånenummer</li> <li>Kontonummer for innfrielse</li> <li>KID/melding</li></ul>                                                       | Numerisk     |                      | X                     |                 | X*              |
| Faktisk restgjeld                                                                                                                                                                                      | Numerisk     |                      | X*                    |                 |                 |
| Fastrente                                                                                                                                                                                              | Ja/nei       |                      | X*                    |                 | X*              |
| Sikkerhet for tredjemannspant?<ul><il>eventuelle navn på låntaker(e) tredjemannspant</il></ul>                                                                                                         | Ja/nei<br/>eventuelt liste med navn       |                      | X*                    |                 | X*              |
| Rammelån<ul><il>eventuelt størrelse på rammelånet</il></ul>                                                                                                                                            | Ja/nei<br/>eventuelt størrelse på ramme       |                      | X*                    |                 |                 |
| Bekreftelse på at panterett sperres for opplåning                                                                                                                                                      | Ja/nei       |                      | X*                    |                 |                 |
| Bekreftelse på at panterett slettes ved innfrielse                                                                                                                                                     | Ja/nei       |                      | X*                    |                 | X*              |
| Antatt innfrielsesdato                                                                                                                                                                                 |              |                      |                       | X*              |                 |
| Innfrielsesbeløp (liste med beløp på antatt innfrielsesdato (+1, 2, 3 arbeidsdager))                                                                                                                   |              |                      |                       |                 | X*              |

# Deling av status og feilhåndtering

Hva svarer bank dersom den ikke har noen lån på kunden. Det vil i alle
fall være to scenarioer der dette skjer:

1. Lånet er nedbetalt, men bank har ikke slettet pantet

2. Megler har forespurt feil bank

3. Finner relatert sak, men mismatch mellom noen id’er. F.eks. dersom
eierforhold ikke er tinglyst.

4. Bank/ kreditor har blitt kjøpt opp eller fusjonert med annen
kreditor, men det er ikke ryddet i Grunnboken. (ofte tilfellet med
inkasso?)

5. I en overgangsfase, dersom bank ikke kan svare fullt ut via API kan
det legges opp til at banken svarer at “melding er mottatt, du får svar
på epost”. Dette gjør at leverandørene kan dele opp oppgaven og levere i
etapper.

Sampant må hensyntas. Meldinger skal sendes til banken, ikke
boligkredittforetaket

Det er viktig med gode status/ feilmeldinger fra bank. Noe som HJELPER
megler.

Vi sender inn en liste – det må gis status pr dagboknummer

Her ønsker vi innspill (spesielt fokus) fra teknisk side:
* gode feilmeldinger og statuser
* andre scenarioer som kan oppstå
* Bør være mulig å melde ifra om at prosessen er avbrutt. F.eks vite
    om dersom bank ikke skal byttes likevel, sperre på lånet skal
    oppheves siden salget ikke blir noe av osv. Kan være vanskelig å
    vite hvor man skal henvende seg. Dette kan gjelde overordnet for
    prosjektet

# Juridisk grunnlag/personvern

Denne spesifikasjonen er laget for å erstatte informasjonsutveksling som
i dag foregår på papir, epost etc. Arbeidsgruppen anser derfor at det
denne spesifikasjonen i prinsippet er en strukturering av informasjon

Overføring av fullt fødselsnummer fra meglersystemene til bank begrunnes
med at det er behov for sikker identifikasjon av hjemmelshaver for å
finne rett person/pant/lån i bankens systemer og i offentlige registre.
Oppslag på navn alene vil gi stor risiko for feil pga. at dette ikke
entydig identifiserer den aktuelle personen (mange kan bære samme navn).
Videre er opplysningene nødvendige for at banken skal kunne vurdere om
banken kan gi pantefrafall. Bruk av fullt fødselsnummer for dette
formålet er saklig, all den tid dette bidrar til mer effektiv
gjennomføring av salgsprosess og overdragelsesprosess, med mindre risiko
for feil.

Dersom den juridiske vurderingen ender med at dagens myndighetskrav er
tilstrekkelig overførings- og behandlings-grunnlag, er det ikke
nødvendig med et samtykke fra kunden.

I tråd med prinsippet om «åpenhet», jf. GDPR art. 5 nr. 1 a., jf. art.
13 skal imidlertid megler opplyse selger om at megler må kontakte banken
for å be om opplysninger. Typisk gjøres dette gjennom informasjon i
salgsoppgaven, i det elektroniske budgivningssystemet eller i en
oppdragsavtale.
