Finansieringsbevis - funksjonell løsningsbeskrivelse
====================================================

# Introduksjon

Dette dokumentet beskriver en løsning for megler å verifisere at en budgiver har et gyldig finansieringsbevis fra en valgt bank når de ønsker å legge inn bud på en bolig.

## Generell beskrivelse

Informasjon fra Finansieringsbeviset skal kunne overføres fra banken til megleren, via AFPANT.

En megler kan be en bank om en person har et finansieringsbevis som dekker et visst beløp basert på:

| Felt                                    | Beskrivelse                                  |
|-----------------------------------------|----------------------------------------------|
| Referanse                               | Et unikt id som refererer til budgivningen   |
| Personens fødselsnummer                 | 11 siffer                                    |
| Budbeløp                                | inkl alle omkostninger                       |
| Matrikkelinformasjon                    | Vid Fast eiendom                             |
| Org nummer og andelsnummer              | Vid Brl. leil                                |
| Org nummer og aksjenummer               | Vid Aksjeleil                                |
| Matrikkelinformasjon                    | Vid Eierseksjon                              |
| Fellesgjeld                             |                                              |
| Felleskostnader                         |                                              |
| Utleiemulighet                          |                                              |
| Salgsoppgave                            |                                              |
| Akseptfrist                             |                                              |
| Meglers kontaktinformasjon              |                                              |

Banken vil svare på forespørselen med strukturert data hvor svarene kan inneholde tre ulike svartyper:

| Status  | Beskrivelse |
|---------|-------------|
| APPROVED | Banken bekrefter at personen har et finansieringsbevis som dekker budet for boligen. |
| DISAPPROVED | Banken kan ikke bekrefte at personen har et finansieringsbevis som dekker budet for boligen. |
| OTHER | Banken trenger mer informasjon for å kunne håndtere saken. Budgiveren skal bli henvist til å ta kontakt med banken. |
