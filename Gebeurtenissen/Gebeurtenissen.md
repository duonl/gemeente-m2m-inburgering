Deze pagina geeft een overzicht van de gebeurtenissen die DUO erkend binnen haar domein en hun relatie tot de verschillende API's die zijn gerealiseerd voor deze gegevensuitwisseling. Voor meer informatie met betrekking tot gebeurtenissen zie [Interactiepatronen](../Interactiepatronen/Interactiepatronen.md)

[TOC]

# Nieuwe inburgeringsplichtige
DUO erkent onder deze gebeurtenissen de volgende situaties:
 - Reguliere nieuwe inburgeringsplichte
 - Inburgeringsplichtige is al langer in Nederland en heeft nu pas een Inburgeringsplichtig verblijfsrecht
 - Inburgeringsplichtige die bijna de AOW leeftijd bereikt
 - Inburgeringsplicht geworden na het intrekken van een tijdelijke vrijstelling zonder een eerdere leerroute
 - Inburgeringsplichtige is 18 jaar en geen deelname aan een vrijstellende opleiding
 - Inburgeringsplichte heeft vrijstelling van de kwalificatieplicht en is op verzoek inburgeringsplichtig gemaakt voordat degene 18 jaar is

DUO signaleert de gemeente van de Inburgeringsplichtige zodra als de gemeente waaronder de inburgeringsplichtige valt vastgesteld is. Het type gebeurtenis hangt af van de achtergrond van de nieuwe inburgeringsplichtige:

| gebeurtenisId | gebeurtenisomschrijving                                          | Relevante API's |
| ---           | ---                                                              | ---             |
| SS101         | Persoon is inburgeringsplichtig.                                  | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) <br>- Examenresultaten |
| SS128         | Persoon is inburgeringsplichtig, maar bereikt AOW-leeftijd binnen 6 maanden. | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) <br>- Examenresultaten |
| SS139         | Persoon is inburgeringsplichtig en de termijn van 10 weken voor vaststellen leerroute is gestart. <br>- Deze gebeurtenis verschijnt ook als de persoon al eerder aan de gemeente gekoppeld is, maar DUO nu vastgesteld heeft dat de persoon bij het COA uitgestroomd is en nu in de gemeente verblijft | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) <br>- Examenresultaten |
| SS129         | Tijdelijke vrijstelling ingetrokken, nog geen leerroute bekend.   | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) <br>- Examenresultaten  <br>- [Vrijstelling](../API/Vrijstelling/openapi.yml) |

# Wijziging van gemeente
DUO erkent onder deze gebeurtensisen de volgende situaties waardoor een gemeente waaronder de inburgeringsplichtige valt wijzigt:
 - Verblijfslocatie onder COA en wijziging gekoppelde gemeente door COA of wijziging bij uitstroom COA.
 - Bij uitstroom van het asielzoekerscentrum en definitieve vestiging uitstroomgemeente conform de BRP.
 - Wijziging van het adres conform het BRP - vertrek uit Nederland **(of dakloos?)** of vertrek naar andere gemeente in Nederland"

DUO signaleert de nieuwe gemeente ten behoeve van de inburgeringsplicht. De gebeurtenis hangt af van de situatie:

| gebeurtenisId | gebeurtenisomschrijving                                          | Relevante API's |
| ---           | ---                                                              | ---             |
| SS120         | Inburgeringsplichte in gemeente gevestigd zonder PIP.            | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) <br>- Examenresultaten |
| SS121         | Inburgeringsplichte in gemeente gevestigd met PIP vorige gemeente | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) <br>- [Inburgeringstermijn](../API/Inburgeringstermijn/openapi.yml) <br>- Examenresultaten |


# Wijziging doelgroep
Wijziging van de gehanteerde doelgroep ten aanzien van de rechten en plichten voor het inburgeren.  
De gemeente kan verzoek inburgeraar voor afzien van asielrechten en plichten naar DUO. Als DUO dit kan verwerkt volgt gebeurtenis SS124.  

Het vervallen van asielrechten door nieuwe gegevens van de IND ziet DUO niet als gebeurtenis. DUO blijft in dit geval van asielrechten en plichten uitgaan. De inburgeraar kan dan wel beroep doen op afzien van de asielrechten en plichten via de gemeente.

| gebeurtenisId | gebeurtenisomschrijving                                          | Relevante API's |
| ---           | ---                                                              | ---             |
| SS124         | Doelgroep van asielstatushouder naar gezinsmigrant en overige migrant gewijzigd    | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) |
| SS125         | Doelgroep van gezinsmigrant en overige migrant naar asielstatushouder gewijzigd | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) |

# Intrekken Inburgeringsplicht
De gemeente kan deze gebeurtenissen zien als aansporing om de administratie van verrichte inspanningen en resultaten voor zover relevant aan te vullen. Deze administratie is relevant voor het hervatten inburgeringsplicht, tenzij de persoon is overleden.

| gebeurtenisId | gebeurtenisomschrijving               | Relevante API's |
| ---           | ---                                   | ---             |
| SS109         | Tijdelijke vrijstelling toegekend     | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) <br> - [Vrijstelling](../API/Vrijstelling/openapi.yml) |
| SS110         | Inburgeringsplicht ingetrokken:  <br> - intrekken verblijfsrecht / langer dan jaar uit NL <br> - genaturaliseerd <br> - AOW geworden <br> - genaturaliseerd <br> - overleden | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) |
| SS111         | Persoon is overleden                  | - [Inburgeringsplicht](../API's/Inburgeringsplicht/openapi.yml) |

# Inburgeringsplicht voldaan
DUO informeert de gemeente ten behoeve van de [Inburgeringsplicht](../API/Inburgeringsplicht/openapi.yml). Het type gebeurtenis hangt af van de situatie:

| gebeurtenisId | gebeurtenisomschrijving               | Relevante API's |
| ---           | ---                                   | ---             |
| SS106         | Diploma behaald                       | - [Inburgeringsplicht](../API/Inburgeringsplicht/openapi.yml) |
| SS107         | Gehele vrijstelling toegekend         | - [Inburgeringsplicht](../API/Inburgeringsplicht/openapi.yml)  <br> - [Vrijstelling](../API/Vrijstelling/openapi.yml) |
| SS108         | Gehele ontheffing toegekend           | - [Inburgeringsplicht](../API/Inburgeringsplicht/openapi.yml) |

# Leerroute en termijn vastgesteld
Ten aanzien van het vaststellen van de leerroute en het starten van de inburgeringstermijn kunnen de volgende gebeurtenissen plaatsvinden:

| gebeurtenisId | gebeurtenisomschrijving                                | Relevante API's |
| ---           | ---                                                    | ---      |
| SS137         | Persoon is aangemeld voor de leerbaarheidstoets        | - [Leerbaarheidstoets](../API/Leerbaarheidstoets/openapi.yml) |
| SS131         | Leerbaarheidstoets is afgenomen en resultaat is bekend | - [Leerbaarheidstoets](../API/Leerbaarheidstoets/openapi.yml)|
| SS102         | Inburgeringstermijn gestart                            | - [Inburgeringstermijn](../API/Inburgeringstermijn/openapi.yml)   |

# Leerroute wijziging en resultaten
Zodra de gemeente een PIP wijzigt of vaststelt, dan kan deze met PIP API (SDI014) aan DUO doorgegeven worden. Met de 'Resultaten PVT, MAP, Z-route API (SDI016)' kan de gemeente de resultaten voor PVT, MAP en/of de Z-route doorgeven. Met de 'Inschrijving inburgeraar bij instelling API (SDI019)' kan de gemeente de opleidings- en participatieinspanning (via de gemeente geregeld bij de intake of voor de asielmigrant) doorgeven.
Voor de ad hoc aanroep van de gemeente kan ook reden zijn bij bijv. het melden van een nieuwe inburgeraar voor de gemeente (gebeurtenissen SS101/128/139/120/121/129/130)."

## Examenresultaten
De gemeente kan bij DUO de examenresultaten bevragen via Examenresultaten API (SDI017). 

| gebeurtenisId | gebeurtenisomschrijving                  | Relevante API's |
| ---           | ---                                      | ---      |
| SS199         | Uitslag examen bekend                    | - [Examen](../API/Examen/openapi.yml) |

# Termijn gewijzigd
De inburgeringstermijn kan worden gewijzigd door de volgende situaties:
- Door verlenging van de termijn ambtshalve of op verzoek van de inburgeraar.
- Door het intrekken van een tijdelijke vrijstelling met een al vastgestelde leerroute of termijn van voor de tijdelijke vrijstelling.

| gebeurtenisId | gebeurtenisomschrijving                  | Relevante API's |
| ---           | ---                                      | ---      |
| SS103         | Termijn ambtshalve verlengd              | - [Inburgeringstermijn](../API/Inburgeringstermijn/openapi.yml) |
| SS104         | Termijn op verzoek verlengd              | - [Inburgeringstermijn](../API/Inburgeringstermijn/openapi.yml) <br> - Beoordeling aanvraag verlenging (SDI014) |
| SS130         | Tijdelijke vrijstelling ingetrokken, PIP al bekend. Eerdere inburgeringsplicht wordt hervat, maar leerroute was al door huidige of eerdere gemeente voor de tijdelijke vrijstelling vastgesteld       | - [Inburgeringsplicht](../API/Inburgeringsplicht/openapi.yml) <br> - [Inburgeringstermijn](../API/Inburgeringstermijn/openapi.yml) <br> - [PIP](../API/PIP/openapi.yml) <br> - Examenresultaten (SDI017) <br> - [Vrijstelling](../API/Vrijstelling/openapi.yml) |

# Verzoeken inburgeraar
Een aantal gebeurtenissen kunnen ontstaan door de afhandeling van verzoeken die de inburgeraar heeft ingediend bij DUO.

| gebeurtenisId | gebeurtenisomschrijving                      | Relevante API's |
| ---           | ---                                          | ---      |
| SS113         | Verzoek verlenging afgewezen                 | - Beoordeling aanvraag verlenging (SDI011) |
| SS114         | Verzoek gehele vrijstelling afgewezen        | - [Vrijstelling](../API/Vrijstelling/openapi.yml) |
| SS115         | Verzoek tijdelijke vrijstelling afgewezen    | - [Vrijstelling](../API/Vrijstelling/openapi.yml) |
| SS116         | Verzoek gedeeltelijke vrijstelling afgewezen | - [Vrijstelling](../API/Vrijstelling/openapi.yml) | 
| SS117         | Verzoek gedeeltelijke vrijstelling toegekend | - [Vrijstelling](../API/Vrijstelling/openapi.yml) <br> - Examenresultaten (SDI017) |
| SS118         | Verzoek ontheffing afgewezen                 | - Beoordeling aanvraag verlenging (SDI013) |
| SS119         | Verzoek gedeeltelijke ontheffing toegekend | - Beoordeling aanvraag verlenging (SDI013) <br> - Examenresultaten (SDI017) |


Hiernaast ontstaan onderstaande gebeurtenissen ook naar aanleiding van een verzoek. Zie per gebeurtenis de relevante paragraaf.

| gebeurtenisId | gebeurtenisomschrijving                                     | Paragraaf                                                     |
| ---           | ---                                                         | ---                                                           |
| SS104         | Termijn op verzoek verlengd                                 | [Termijn gewijzigd](#termijn-gewijzigd)                       |
| SS109         | Tijdelijke vrijstelling toegekend                           | [Intrekken Inburgeringsplicht](#intrekken-inburgeringsplicht) |
| SS129         | Tijdelijke vrijstelling ingetrokken, nog geen PIP ontvangen | [Nieuwe inburgeringsplichtige](#nieuwe-inburgeringsplichtige) |
| SS130         | Tijdelijke vrijstelling ingetrokken, PIP al bekend          | [Termijn gewijzigd](#termijn-gewijzigd)                       |

# Overzicht Gebeurtenissen En Relevante API's
Zie het document [Gebeurtenissen overzicht](../Gebeurtenissen/Gebeurtenissen%20overzicht.xlsx) voor een lijst van alle gebeurtenissen en hun relatie tot relevante API's.