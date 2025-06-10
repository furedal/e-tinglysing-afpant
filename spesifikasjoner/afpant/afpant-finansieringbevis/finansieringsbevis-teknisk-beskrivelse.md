Finansieringsbevis - teknisk beskrivelse
=======================================

![Flyt Finansieringsbevis](./finansieringsbevis.svg)

Flyten over beskriver hvordan finansieringen av et bud godkjennes av en bank under en budgivning.
For hvert nytt bud gjentas flyten.


# Meldingstyper
## Oversikt over meldingstyper for finansieringsbevis
| Navn                                                                                         | Beskrivelse                                                                                                                                                | Payload/vedlagt fil                    | 
|----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
| [FinansieringsbevisRequest](#meldingstype-finansieringsbevisrequest)                         | Bank forespør finansiering av et bud                                                                                                                     | XSD: FinansieringsbevisRequest         |
| [FinansieringsbevisResponse](#meldingstype-finansieringsbevisresponse)                       | Svar på finansieringsbevisRequest                                                                                                                         | XSD: FinansieringsbevisResponse        |

# Meldingstype: FinansieringsbevisRequest
Megler forespør finansieringbevis från bank.

## Validering og ruting (banksystem)
Megler forespør finansieringbevis från bank.

Skal innehold megler(`finansieringsbevisRequest.megler`), bank(`finansieringsbevisRequest.bank`) 
, (`finansieringsbevisRequest.budinformation`) og (`finansieringsbevisRequest.salgsobjekt`).

[Se XML-eksempel:](./examples/finansieringsbevisRequest-example.xml)

## Payload
En ZIP-fil som inneholder en XML med requestdata ihht. [definert skjema.](../afpant-model/xsd/dsve.xsd)

**Krav til filnavn i ZIP-arkiv:** 
* Filnavnet til meldingen FinansieringsbevisRequest må følge konvensjonen: _finansieringsbevisrequest*.xml_ . (navnet til meldingen i lowercase)

## Manifest
(BrokerServiceInitiation.Manifest.PropertyList)

|Manifest key|Type|Obligatorisk|Beskrivelse|
|--- |--- |--- |--- |
|messageType|String|Yes|FinansieringsbevisRequest|

# Meldingstype: FinansieringsbevisResponse
Svar på [FinansieringsbevisRequest](#meldingstype-finansieringsbevisrequest) fra banken.

Banken svarar med status på denne spørselen.

## Payload
En ZIP-fil som inneholder en XML med requestdata ihht. [definert skjema.](../afpant-model/xsd/dsve.xsd)

**Krav til filnavn i ZIP-arkiv:** 
* Filnavnet til meldingen FinansieringsbevisResponse må følge konvensjonen: _finansieringsbevisresponse*.xml_ . (navnet til meldingen i lowercase)

## Manifest
(BrokerServiceInitiation.Manifest.PropertyList)

|Manifest key|Type|Obligatorisk|Beskrivelse|
|--- |--- |--- |--- |
|messageType|String|Yes|FinansieringsbevisResponse|
|status|String (enum)|Yes|Denne kan være en av følgende statuser: <ol><li>**APPROVED**<br/>Banken bekräftar at budet kan finansieras av banken.</li><li>**DISAPPROVED**<br/>Banken kan ej bekräfta finansiering av budet.</li><li>**OTHER**<br/>Banken behöver mer information för att hantera begäran. Budgivaren skall bli notifierad att ta kontakt med sin bank.</li></ol> Övriga stautsar skall anses som NACK (negative acknowledgement).|


