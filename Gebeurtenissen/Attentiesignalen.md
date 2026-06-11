--> Alle informatie m.b.t. attentiesignalen even op deze pagina gezet als mental note. Is voorlopig nog niet relevant.

[TOC]

# Wijziging van gemeente
De oude gemeente krijgt een attentiesignaal **(via attentiesignaal API (SDI008))** als aansporing de administratie van verrichte inspanningen en resultaten voor zover relevant aan te vullen ten behoeve van het hervatten van de inburgeringsplicht:

| gebeurtenisId | gebeurtenisomschrijving                                          | Relevante API's |
| ---           | ---                                                              | ---             |
| SS122         | Vertrokken naar andere gemeente                                  | Moeten er inspanningen en resultaten worden doorgegeven? |
| SS123         | Vertrokken uit Nederland                                         | Moeten er inspanningen en resultaten worden doorgegeven? |

# Inburgeringsplicht voldaan
Indien voldaan aan de Z-route ontvangt de gemeente van DUO het attentiesignaal SS141 (via attentiesignaal API, SDI008), zodra via de portal de tekst voor het certificaat gedownload kan worden.

# Leerroute en termijn vastgesteld
Mocht conform DUO de 10 weektermijn gelden en is er aan het eind van de 10 weken nog geen leerroute, dan zal attentiesignaal SS126 (via attentiesignaal API SDI008) volgen.

# Leerroute wijziging en resultaten
Rondom de opleiding van de inburgeraar kan DUO onderstaande signalen (via attentiesignaal API (SDI008)) verstrekken:
 - SS142	Niet-vrijstellende opleiding beëindigd wegens uitschrijving. Indien nodig graag contact opnemen met inburgeraar en PIP herzien
 - SS127	Nog geen inburgeringsaanbod ontvangen (bij asielmigrant met al vastgestelde leerroute en geen aanbod)
 - Bij een van een instelling ontvangen contract van een (nog) niet verwachte soort opleiding:
   - SS132	Opleidingscontract ontvangen (nog geen PIP)
   - SS133	Opleidingscontract ontvangen met taalniveau niet conform de opgegeven leerroute voor inburgering
   - SS135	Opleidingscontract ontvangen met te hoog taalniveau conform de PIP (Z-route)
   - SS136	Opleidingscontract voor taalschakeltraject ontvangen, geen onderwijsroute

# Verzoeken inburgeraar
Bij een verzoek voor ontheffing op bijzonder individuele omstandigheden (BIO) verstuurd DUO het attentiesignaal SS140 (via attentiesignaal API (SDI008)) om een advies hierover te geven.

SS112 Verzoek verlenging ingediend