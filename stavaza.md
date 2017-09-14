# Periode April-Mei-Juni

## Intro 

Deze periode behelst de opstart van de van effectieve werking. Het aantrekken van medewerkers verliep vanuit verschillende hoeken: en deel door losse werving, een deel vanuit de app4ghent competitie (winnaar beste idee) en een paar studenten die voor een proef hadden samengewerkt met Dienst mobiliteit. 

## Projecten 

Er werden 2 projecten opgezet en 450 uur gepresteerd.

* Apps/beacons: [Krookie App](https://github.com/lab9k/Krookie) (60%)
* Blockchain: [Soupcoin](https://github.com/lab9k/SoupCoin) (40%)

De keuze voor deze projecten lag deels bij de technologie (blockchain) deels bij eerder gemaakte keuzes (laureaten A4G) en tenslotte op de opportuniteiten die voor ons lagen (Linked open data GF, en studenten die summiere ervaring hadden met chatbots).

## Return

De **soupcoin** zal een blockchain applicatie opleveren die in september bij Digipolis geïmplementeerd zal worden. Origineel komt dit idee uit 'tijd voor innovatie' het stelt medewerkers van Digipolis in staat soup te bestellen via de blockchain. 

Het laat ons toe om een use case te hebben die effectief geëvalueerd kan worden binnen de context van Digipolis. De lessen die we hieruit leren kunnen ons helpen te evalueren wanneer de technologie matuur genoeg is om effectief te gaan gebruiken bij de burger. 

De **krookie app** geeft ons een inzicht of en hoe de beacons in de Krook werken. De app werkt op dit moment maar nog niet volledig. Interessant is dat het opzetten van dit project ons de mogelijkheid gaf om verder met de leverancier op te volgen of het systeem wel degelijk werkt, in eerste instantie deed het dit niet. 

Los van alles zijn hier de lessons learned dat beacon technologie sterk afhankelijk is van het device dat mensen gebruiken, en niet enkel apple/android maar sterk afhankelijk van android versie en implementatie. 

# Periode Juli

## Projecten 
Er werd 806 uur gepresteerd op de volgende projecten:  

* Apps/beacons: [Krookie App](https://github.com/lab9k/Krookie)(40%)
* Blockchain: [Soupcoin](https://github.com/lab9k/SoupCoin) (30%)
* Chatbot Gentse Feesten: [ChatbotGF](https://github.com/lab9k/ChatbotGF) (20%)
* Reserveer vergaderzaal: [Reservatie](https://github.com/lab9k/reservatie_OpenCV) (10%)

## Return

De ontwikkeling van **soupcoin** en **krookie app**  liepen verder tot aan de GF. 

De **chatbot** wees de mensen de weg naar dichtbijzijnde podia op de gentse feesten, werd door 3 mensen in 9 dagen opgeleverd en haalde meer dan duizend unieke gebruikers. We hebben hieruit de mogelijkheden van chatbots beter geleerd, de piste van AI lieten we al snel varen wegens nog niet matuur genoeg. Een menu met knoppen in de chat werkt beter. De applicatie was volledig stateless en werkte op onze linked open data, we willen deze kennis en code opnieuw gebruiken als de data van visit gent als LOD beschikbaar wordt. 

Het **Reserveer vergaderzaal** verhaal was een klein experiment door Frederik Waeyaert aangehaald, het keek of het mogelijk was met gezichtsherkenning vergaderzalen te boeken. Belangrijkste lessons learned: nee. Het is niet mogelijk dit te doen binnen een context van de Groep Gent via OpenCV, er zijn té veel mensen binnen de groep om betrouwbare resultaten terug te krijgen. Zie hier [een demo](https://www.youtube.com/watch?v=giro7kRbgkc).

# Periode Augustus

## Projecten 
Er werd 380 uur gepresteerd op de volgende projecten:  

* Reserveer vergaderzaal: [Reservatie](https://github.com/lab9k/reservatie_OpenCV) (20%)
* LAb9Kos: [L9Kos](https://github.com/lab9k/lab9kos) (40%)
* Open311: Er werd onderzoek gedaan naar open311 standaard. (40%)

## Return

Het **Reserveer vergaderzaal** verhaal was een klein experiment door Frederik Waeyaert aangehaald, het keek of het mogelijk was met gezichtsherkenning vergaderzalen te boeken. Belangrijkste lessons learned: nee. Het is niet mogelijk dit te doen binnen een context van de Groep Gent via OpenCV, er zijn té veel mensen binnen de groep om betrouwbare resultaten terug te krijgen. Zie hier [een demo](https://www.youtube.com/watch?v=giro7kRbgkc).

Lab9kOS is een aanzet om meer structuur te krijgen, het is een tool waarbij de studenten hun uren kunnen opgeven voor de komende periode. Was nodig om de verwarring van wie komt wanneer op te heffen. Staat op [https://admin.lab9k.gent/](https://admin.lab9k.gent/) wordt gerbuikt. 

Open311: We hebben hier onderzocht of er een mogelijkheid is met open source tools iets te doen rond mapping, meldingen en routing. Er werd geëxperimenteerd met [https://www.ushahidi.com/](https://www.ushahidi.com/),  [FixMyStreet](https://github.com/mysociety/fixmystreet) en mapit.

Er zijn veel lessons learned van deze experimenten, voornamelijk op het gebied van MapIt. Het experiment ging zo ver dat meldingen op de kaart werden herleid naar de wijken en dat meldingen op basis van wijk en type naar het correct mailadres geroute kunnen worden. Uiteindelijk hebben we gepoogd zelf een open311 backend op te zetten maar daar bleek geen goede software voor te zijn.

# Periode September

## Projecten
Er werd tot nu 406 uur gepresteerd op de volgende projecten:  

* [Busje komt zo](https://github.com/lab9k/BusjeKomtZo)(20%)
* [ParkingCoin](https://github.com/lab9k/Parking) (40%)
* [Erkende verenigingen](https://github.com/lab9k/Verenigingen)(40%)

## Return

In samenspraak met dienst Mobiliteit zochten we een manier om de park and ride bus te visualiseren die tussen Weba en St jacobs rijdt. Er zou een api opgeleverd moeten zijn, maar dat is niet het geval en nu is er een omweg daarvoor gezocht. De code is af en werkt, volgende week wordt dit project live gezet.

Parkingcoin en verenigingen komen dan weer vanuit de ambitie om ervaring op te doen rond blockchain. 

Verenigingen wil een lijst van erkende vereingingen bijhouden op de blockchain (idee Franky). Zie [de challenge](https://github.com/lab9k/Verenigingen/blob/develop/README.md).

Parkingcoin wil betaling voor parking mogelijk maken via de blockchain, interessant om hierbij te melden is dat het herleiden van locatie naar parkeertarief automatisch gebeurt op basis van de MapIt van het open311 project. We lezen de parkeerzones als opendata binnen en geven een antwoord op basis van gps locatie om het correcte tarief te berekenen.

----

# Andere return

* Het concept inspireert mensen en leert ons nieuwe organisaties kennen.
* De meetups worden bezocht
* Het spreekt externe onderwijsinstellingen aan.
* Het laat laagdrempelig samenwerken tussen de verschillende diensten en digipolis toe.

# Vooruit kijkend

* We moeten een goede stagewerking opzetten, nodig omdat studenten door het jaar niet zo'n zoveel tijd hebben.
* Er is werk aan promotie van het Lab met Digipolis.
* Er moet meer ruimte gemaakt worden om PoC's van bedrijven te embedden in Lab9K 
* Er dient een betere structurele samenwerking tussen foresight, de rest van digipolis en lab9K opgezet.
* Met de cases die we nu hebben kunnen we een Blockchain@Gent meeting doen.
