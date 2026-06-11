# Inburgeringsketen M2M gegevensuitwisseling DUO en Gemeente 

# Introductie
De informatie op deze pagina is opgesteld voor de gegevensuitwisseling in de inburgeringsketen tussen Dienst Uitvoering Onderwijs (DUO) en een gemeente. 
_De beschreven processen en functionaliteiten zijn daarmee niet relevant voor alle ketenpartners in de inburgeringsketen._

Voor het inburgeringsstelsel WI2021 is het programma Veranderopgave Inburgering (VOI) ingericht. Onderdeel van de VOI is het realiseren van een geautomatiseerde gegevensuitwisselingen tussen DUO en de ketenpartners in de inburgeringsketen. De doelstelling hierbij is tweeledig:
-	Zorgen dat vertrouwelijke gegevens binnen de inburgeringsketen op een eenduidige, betrouwbare en veilige manier geautomatiseerd uitgewisseld kunnen worden; 
- Gebruikmaken van oplossingen die toekomstvast, wendbaar en beheerbaar zijn.

De gegevensuitwisselingen worden technisch gerealiseerd op het Diginetwerk aan de hand van REST API’s welke werken met een JSON berichtformaat. Hierbij wordt de Digikoppeling standaard van Logius gehanteerd. 

Voor het beschrijven van de functionaliteit van de REST API’s wordt een open api specificatie gehanteerd. De open api specificaties geven hierbij invulling aan welke gegevens er in de inburgeringsketen worden uitgewisseld conform het ‘Informatiemodel keten inburgering’. 

De open api specificaties volgen de REST architectuurstijl waarin het concept van resources centraal staat. Een resource is een abstractie van de uit te wisselen informatie of gegevens. Aan elke resource is een globaal unieke URI (Uniform Resource Identifier) toegeschreven, welke de resource vernoemd en beschrijft. Resources kunnen zowel fysieke zaken beschrijven zoals personen of meer abstracte concepten zoals een inburgeringsplicht.

# Voorwaarden Gegevensuitwisseling
## Scope
De gegevensuitwisseling betreft alleen de gegevens van personen die aan de volgende voorwaarden voldoen:
- De persoon moet onder de Wet Inburgering 2021 vallen.
- De persoon die wordt geraadpleegd moet bekend zijn in de administratie van DUO.

De persoon moet relevant zijn voor de gemeente, hiervoor moet één van de onderstaande voorwaarden van toepassing zijn:
- De persoon is een ingezetene van de gemeente en niet woonachtig in een locatie van het Centraal Orgaan Opvang Asielzoekers (COA). 
- De persoon is woonachtig in een COA locatie en door de COA gekoppeld aan de gemeente.
- De persoon zijn actuele Persoonlijke plan Inburgering en Participatie (PIP) is van de vragende gemeente.
- De persoon zijn actuele PIP is jonger dan een maand en de voorgaande PIP is van de vragende gemeente.

## Basis pad URI
Alle gerealiseerde API's binnen dit project gebruiken hetzelfde basispad voor de URI:
- https://{DUO url:DUO poort}/{major version number API}

Bijvoorbeeld in het geval een API version 1.0.2:
- https://api.example.org:1234/v1

De volledige URI inclusief basispad ziet er dan bijvoorbeeld zo uit voor de Inburgeringsplicht van een persoon:
- https://api.example.org:1234/v1/personen/{bsn}/inburgeringsplicht

Het basispad is niet vermeld in de open api specificatie (.yml).

## Organisatieidentificatienummers (OIN)
Voor de identificatie van ketenpartners binnen deze gegevensuitwisseling wordt er gebruikt van een door Logius uitgegeven OIN, zie https://oinregister.logius.nl/  
De gemeente in de rol van eindorganisatie waarvoor de gegevensuitwisseling wordt uitgevoerd is de bron van een bericht. Het OIN van deze gemeente betreft het 'Bron OIN' in de header van het verzoekbericht.  
De doelorganisatie betreft het OIN van 'Dienst Uitvoering Onderwijs'. Dit betreft het doel OIN in de header van het verzoekbericht.

## Notificatie API
De gegevensuitwisseling wordt ondersteund een drietal interactiepatronen, zie [Interactiepatronen](Interactiepatronen/Interactiepatronen.md)

DUO notificeert de gemeente omtrent gebeurtenissen binnen haar domein, om de interactiepatronen te faciliteren. 
Voor het ontvangen van deze notificaties moet de gemeente de [Notificatie API](API/Notificatie/openapi.yml) hebben geimplementeerd.

### Gebeurtenissen
Zie het [Gebeurtenissen overzicht](Gebeurtenissen/Gebeurtenissen.md) voor de gebeurtenissen die DUO erkent binnen haar domein en waarvan de gemeente een notificatie kan verwachten op de Notificatie API.

## Persoonlijk Plan Inburgering en Participatie (PIP)
Ten aanzien van het [PIP](API/PIP/openapi.yml) gelden de volgende aanvullende voorwaarden:

### Raadplegen PIP
Een gemeente kan altijd de actuele PIP raadplegen die bij DUO bekend is. Dit kan zowel het PIP van eigen gemeente of het PIP van een voorgaande gemeente betreffen.

### Het aanleveren van een PIP
Een aangeleverde PIP wordt alleen geregistreerd als er aan de volgende voorwaarden wordt voldaan:

**Datum dagtekening**:
- De datum dagtekening mag niet voor de start van de inburgeringsplicht liggen.
- De datum dagtekening mag bij een gewijzigde PIP niet voor de start van de datum dagtekening van de initiële PIP OF voor de datum dagtekening van de actuele PIP liggen.
- De datum dagtekening mag niet voor de vestiging van de inburgeraar bij de gemeente liggen.

**Niveau**:
- Niveau A2 mag niet in combinatie met de onderwijsroute worden aangeleverd.
- Niveau B1  mag niet in combinatie met de Z-route worden aangeleverd.
- Niveau A2  mag niet in combinatie met de B1-route worden aangeleverd als dit de eerste PIP is die wordt aangeleverd voor de persoon ongeacht welke gemeente.
- Als het Niveau niet wordt aangeleverd in het verzoekbericht dan wordt Niveau B1 vastgesteld als er sprake is van de B1-route of onderwijsroute

**Geschatte intensiteit B1 route**:
- Geschatte intensiteit B1 route mag alleen aangeleverd worden bij een de B1-route en bij asielmigranten.

### Het verwijderen van een PIP
Het verwijderen van een PIP is alleen mogelijk als er aan de volgende voorwaaren kan worden voldaan:
- De inburgeringstermijn is nog niet is vastgesteld.
- Er zijn nog geen cursusdeelnameuren gerelateerd aan het actuele inburgeringsaanbod geregistreerd.

## Contactpersoon
Via de Contactpersoon API kan de contactpersoon, die bereikbaar is voor vragen vanuit de keten omtrent de inburgeraar, gemuteerd worden.

### Koppelen van een Contactpersoon
Bij het koppelen van een contactpersoon wordt een bestaande koppeling met een ander contactpersoon overschreven.

### Verwijderen van een contactpersoon
Bij het verwijderen van een contactpersoon worden nog eventueel aanwezige koppelingen met inburgeringsplichtigen verwijderd.

## Inburgeringsaanbod
Een aangeleverd Inburgeringsaanbod wordt alleen geregistreerd als er aan de volgende voorwaarden wordt voldaan:

* Het inburgeringsaanbod is voor een asielmigrant
* De persoon heeft een PIP
* De Opleidingsinstelling moet bekend zijn bij DUO als een door Blik op Werk (BoW) gekeurmerkte instelling of een erkende Taalschakelinstelling (TST) als de persoon de onderwijsroute volgt. De lijst met erkende instellingen kan worden geraadpleegd via de [Inburgeringsaanbod](API/Inburgeringsaanbod/openapi.yml) API
* De data van het inburgeringsaanbod ligt niet voor de dagtekening van de actuele PIP
* De 'datumAanvangTaalschakeltraject' ligt niet voor de 'datumEindeCursus' of de 'datumInburgeringsaanbod'
* De 'datumAanvangTaalschakeltraject' en 'datumEindeCursus' mogen niet buiten de inburgeringstermijn liggen.

Voor elk persoon kan er per instelling een inburgeringsaanbod worden aangedragen. Voorgaande registraties van het inburgeringsaanbod worden bij een nieuwe aanlevering voor elke cursusinstelling overschreven.

## Module Arbeidsmarkt en Participatie (MAP)
De datum eindgesprek MAP met indicatie verwijtbaarheid moet aan de volgende voorwaarden voldoen:
* Bij een wijziging moet de datum eindgesprek MAP eerder door uw gemeente zijn geleverd
* Uw gemeente moet een actuele PIP hebben voor de inburgeringsplichtige
* De inburgeringsplicht moet nog niet voldaan zijn via de Z-route
* De datum eindgesprek MAP mag niet voor de startdatum van de inburgeringstermijn liggen
* De datum eindgesprek MAP mag niet na de datum afronding Z-route liggen
* De datum eindgesprek MAP mag niet in de toekomst liggen
* Als de datum eindgesprek MAP leeg is (t.a.v. het intrekken van een eerder geregistreerde datum), dan mag de datum afronding Z-route niet geregistreerd zijn.
* Als het verzoekbericht geen 'Verwijtbaar (Ja/Nee)' bevat, dan mag er geen sprake zijn van een overschrijding van de inburgeringstermijn.
* Als de datum eindgesprek MAP voor de einddatum van de inburgeringstermijn ligt, dan mag de 'Verwijtbaar (Ja/Nee)' niet geleverd worden. 
* 'Verwijtbaar (Ja/Nee)' mag alleen de waarde 'Nee' hebben als de einddatum van de inburgeringstermijn binnen twee maanden valt.
* 'Verwijtbaar (Ja/Nee)' mag alleen de waarde 'Ja' hebben als er sprake is van een overschrijding van de inburgeringstermijn. 

Het doorgeven van de Datum eindgesprek MAP en indicatie verwijtbaarheid gebeurt via een PUT methode. Hierbij wordt de gehele resource vervangen door de inhoud uit het verzoekbericht. Het intrekken van een de Datum eindgesprek MAP of indicatie verwijtbaarheid kan daarom door het betreffende onderdeel niet op te nemen in de body van het verzoekbericht.

## Participatieverklaringstraject (PVT)
De Datum ondertekening PVT met indicatie verwijtbaarheid moet aan de volgende voorwaarden voldoen:
* Bij een wijziging moet de Datum ondertekening PVT eerder door uw gemeente zijn geleverd
* Uw gemeente moet een actuele PIP hebben voor de inburgeringsplichtige
* De inburgeringsplicht moet nog niet voldaan zijn via de Z-route
* De datum ondertekening PVT mag niet voor de startdatum van de inburgeringstermijn liggen
* De datum ondertekening PVT mag niet na de datum afronding Z-route liggen
* De datum ondertekening PVT mag niet in de toekomst liggen
* Als de datum ondertekening PVT leeg is (t.a.v. het intrekken van een eerder geregistreerde datum), dan mag de datum afronding Z-route niet geregistreerd zijn.
* Als het verzoekbericht geen 'Verwijtbaar (Ja/Nee)' bevat, dan mag er geen sprake zijn van een overschrijding van de inburgeringstermijn.
* Als de datum ondertekening PVT voor de einddatum van de inburgeringstermijn ligt, dan mag de 'Verwijtbaar (Ja/Nee)' niet geleverd worden. 
* 'Verwijtbaar (Ja/Nee)' mag alleen de waarde 'Nee' hebben als de einddatum van de inburgeringstermijn binnen twee maanden valt.
* 'Verwijtbaar (Ja/Nee)' mag alleen de waarde 'Ja' hebben als er sprake is van een overschrijding van de inburgeringstermijn. 

Het doorgeven van de Datum ondertekening PVT en indicatie verwijtbaarheid gebeurt via een PUT methode. Hierbij wordt de gehele resource vervangen door de inhoud uit het verzoekbericht. Het intrekken van een de Datum ondertekening PVT of indicatie verwijtbaarheid kan daarom door het betreffende onderdeel niet op te nemen in de body van het verzoekbericht.

## Gevolgde uren
Zie voor meer informatie omtrent de gevolgde uren de 'Handleiding Portal Inburgering Wet inburgering 2021' de paragraaf 'Deelgenomen uren en uren taalles en KNM'.

## Enumeratie omschrijving
De omschrijving van enumeratiewaarden die uit een code of cijfer bestaan is in een losstaand 'Description' schema opgenomen in de open API specificatie. Zie hieronder een voorbeeld van een open api specificatie van de enumeratie voor 'Alfabetiseringsonderwijs', waarbij:
- A = Onderwijs voor analfabeet
- AA = Onderwijs voor anders-analfabeet
- NVT = Niet van toepassing

```yaml
components:
  schemas:
    Alfabetiseringsonderwijs:
      type: string
      description: Een traject voor een analfabeet of anders-gealfabetiseerde om de
        basis van de Nederlandse taal te leren als onderdeel van de leerroute.
      enum:
      - A
      - AA
      - NVT
    AlfabetiseringsonderwijsDescription:
      type: string
      description: Een traject voor een analfabeet of anders-gealfabetiseerde om de
        basis van de Nederlandse taal te leren als onderdeel van de leerroute.
      enum:
      - Onderwijs voor analfabeet
      - Onderwijs voor anders-analfabeet
      - Niet van toepassing
      x-enum-varnames:
      - A
      - AA
      - NVT
```

## Vertrouwlijkheid
Authenticatie voor de gegevensuitwisseling gebeurt op basis van het PKIO certificaat. 

Het PKIO certificaat moet aan de volgende eisen voldoen:

- het PKIO certificaat moet geldig zijn; het mag niet verlopen of ingetrokken zijn
- het PKIO certificaat moet zijn van het type PKIoverheid private root

# Gerealiseerde API's binnen gegevensuitwisseling

| Open API Specificatie                                        | Versie | Versiedatum| Stelseldienst | Changelog |
|------------------------------------------------------------- | ---    | ---        | ---           |  ---      |
| [Notificatie](API/Notificatie/openapi.yml)                   | V1.8.0 | 02-10-2025 | n.v.t.        | [Notificatie](API/Notificatie/CHANGELOG.md) |
| [Inburgeringsplicht](API/Inburgeringsplicht/openapi.yml)     | V1.2.2 | 31-03-2025 | SDI005        | [Inburgeringsplicht](API/Inburgeringsplicht/CHANGELOG.md) |
| [Leerbaarheidstoets](API/Leerbaarheidstoets/openapi.yml)     | V1.2.0 | 06-11-2024 | SDI006        |[Leerbaarheidstoets](API/Leerbaarheidstoets/CHANGELOG.md) |
| [Inburgeringstermijn](API/Inburgeringstermijn/openapi.yml)   | V1.0.0 | 07-11-2024 | SDI007        |[Inburgeringstermijn](API/Inburgeringstermijn/CHANGELOG.md) |
| [Vrijstelling](API/Vrijstelling/openapi.yml)                 | V1.0.0 | 12-08-2025 | SDI012        |[Vrijstelling](API/Vrijstelling/CHANGELOG.md) |
| [Ontheffing](API/Ontheffing/openapi.yml)                     | V1.0.0 | 07-10-2025 | SDI013        |[Ontheffing](API/Ontheffing/CHANGELOG.md) |
| [PIP](API/PIP/openapi.yml)                                   | V1.1.3 | 16-01-2025 | SDI014        |[PIP](API/PIP/CHANGELOG.md) |
| [Contactpersoon](API/Contactpersoon/openapi.yml)             | V1.0.0 | 14-05-2025 | SDI014        |[Contactpersoon](API/Contactpersoon/CHANGELOG.md) |
| [Inburgeringsaanbod](API/Inburgeringsaanbod/openapi.yml)     | V1.0.0 | 27-01-2025 | SDI014        |[Inburgeringsaanbod](API/Inburgeringsaanbod/CHANGELOG.md) |
| [MAP, PVT, Z-route](API/MAP,PVT,Zroute/openapi.yml)          | V1.0.0 | 30-03-2026 | SDI016        |[MAP, PVT, Z-route](API/MAP,PVT,Zroute/CHANGELOG.md) |3
| [Gevolgde Uren](API/GevolgdeUren/openapi.yml)                | V1.0.0 | 30-03-2026 | SDI016        |[Gevolgde Uren](API/GevolgdeUren/CHANGELOG.md) |
| [Examen](API/Examen/openapi.yml)                             | V1.0.0 | 13-11-2025 | SDI017        | [Examen](API/Examen/CHANGELOG.md) |

# Geplande API's (Roadmap)
De onderstaande API's worden nog gerealiseerd binnen de scope van de VOI. Deze staan niet in volgorde van realisatie:
- Notifiatie inburgeringsplichtige om reden (SDI008)
- Beschikking voldaan inburgeringsplicht (SDI009)
- Beoordeling aanvraag verlenging (SDI011)
- Opgelegde Boete (SDI018)
- Inspanning Inburgeraar bij instelling (SDI019)
