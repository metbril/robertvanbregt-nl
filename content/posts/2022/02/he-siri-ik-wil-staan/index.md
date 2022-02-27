---
title: "Hé Siri, ik wil staan!"
slug: "he-siri-ik-wil-staan"
date: 2022-02-02T19:29:00+01:00
author: Robert van Bregt
tags: [apple,siri,automatisering]
categories:
  - Technologie
---

Sinds het begin van de pandemie [werk ik veel thuis](https://robertvanbregt.nl/2021/03/02/een-jaar-covid-19/). In het begin met bestaande apparatuur, en bestaand meubilair. Maar in de loop van de tijd heb ik mijn werkplek steeds een beetje verbeterd. Een van de zaken waarin ik heb geïnvesteerd, is een zit-stabureau. Via mijn werkgever kon ik met een voorschotregeling een vergoeding krijgen, maar dan had ik de keuze uit één enkel model dat me niet echt beviel. Uiteindelijk ben ik daarna terecht gekomen bij IKEA. Daar viel mijn keus op de zwarte uitvoering van het robuuste model [IDÅSEN](https://www.ikea.com/nl/nl/cat/idasen-bureaus-47426/) in 160×80 cm.

{{< figure src="idasen-desk-sit-stand-black-dark-grey-1.jpg" >}}
{{< figure src="idasen-desk-sit-stand-black-dark-grey-2.jpg" >}}
{{< figure src="idasen-desk-sit-stand-black-dark-grey-3.jpg" >}}

Het mooie daarvan is, en eerlijk gezegd was dat stiekem mede ook beetje een reden voor de keuze, dat het bureau draadloos is te bedienen. Aan de motor van het bureau zit een Bluetooth BLE module die gekoppeld kan worden met je Android of iOS telefoon. Dat biedt perspectief voor [automatisering](/tags/automatisering/)!

## Bedienen met een iPhone app

LINAK, de fabrikant van de module, heeft voor de draadloze besturing van de module een eigen app “Desk Control” gemaakt. Die heb ik geprobeerd en dat werkt op zich prima. Maar de app ondersteunt geen Siri-opdrachten. Maar er zijn inmiddels ook onafhankelijke ontwikkelaars die een alternatieve app hebben ontwikkeld. Een beetje zoeken in de AppStore levert meerdere resultaten. De app waar ik eindelijk op ben uitgekomen is Idasen Controller van Tiago Alves. Een gratis app (want ik ben Nederlander), die ook nog eens keurig Siri-opdrachten ondersteund. En inderdaad, daarmee is het gelukt het instellen van mijn bureau te automatiseren.

Nadat je de app hebt geinstalleerd, moet je deze calibreren, zodat de app weet welke hoogte in centimeters bij de laagste stand hoort. Na de calibratie kun je eenvoudig voorkeuren instellen. Ik heb er 3 ingesteld: ‘Stahoogte’, ‘Zithoogte’ en ‘Halverwege’. Die laatste, daar kom ik verderop op terug.

Nadat je de hoogtes in de app juist hebt ingesteld, kun je ze met een klik op het scherm kiezen. Magisch. Maar dat kan beter.

{{< figure src="idasen-controller.png" width="300" >}}

## Bedienen met Siri-opdrachten

Idasen Controller heeft ondersteuning voor Siri-opdrachten. Dat zijn eenvoudige tot heel complexe automatiseringen, die je zelf kunt maken zonder programmeerkennis. Die opdrachten maak je eenmalig, en daarna kun je ze steeds opnieuw opstarten. Ik heb apart opdrachten gemaakt om het bureau in te stellen op zithoogte en op stahoogte. Dat doe je als volgt.

Start op je iPhone de app Opdrachten. (Installeer deze eerst als je hem ooit verwijderd hebt.)

Maak een nieuwe Opdracht, geef deze een naam (bijvoorbeeld ‘Ik wil staan’ en kies een icoon (bijvoorbeeld een pijltje omhoog).

Voeg een taak toe aan de nieuwe opdracht. Kies de Idasen Controller app en kies de actie ‘Move desk to position’. 

{{< figure src="shortcut-idasen-1.png" width="300" >}}

Kies een hoogte (bijvoorbeeld ‘Stahoogte’) en zet het schuifje ‘Toon bij uitvoeren’ uit.

{{< figure src="shortcut-idasen-2.png" width="300" >}}

Test de opdracht, door rechtsonder op het driehoekige afspeel-symbool te klikken. Als het goed is verandert nu de hoogte.

Als de opdracht werkt, plaats je daarvan een snelkoppeling op je beginscherm. Dan kun je namelijk met 1 klik de opdracht starten.

Open daarvoor het ‘Delen’ menu onderaan. Kies voor ‘Zet op beginscherm’ en kies voor ‘Voeg toe’.

{{< figure src="shortcut-idasen-3.png" width="300" >}}

Maak een opdracht voor zowel stahoogte als zithoogte. Nu heb je 2 iconen op je beginscherm. Eén voor stahoogte en één voor zithoogte. Leuk! Maar dat kan nog leuker!

## Bedienen met je stem

Je kunt nu je bureau handmatig instellen met de knoppen van de module, met de app, of via de snelkoppelingen op je beginscherm. Maar hoe gaaf is het, om je bureau in beweging te zetten met alleen je stem. Daarvoor is deze laatste stap nodig.

Iedere Siri-opdracht kun je ook met je stem activeren. Standaard door “Hé Siri” te roepen, gevolgd door de naam van de opdracht. Dus als de opdracht “Ik wil staan” heet, kun je deze direct activeren met je stem. Wil je een ander commando gebruiken dan de naam van je opdracht, dan kun je via Instellingen het commando aanpassen naar iets anders.

Probeer maar. Roep “Hé Siri, ik wil staan!”. Bij mij toverde dat de eerste keer een enorme glimlach op mijn gezicht.

Helaas ben je er nog niet helemaal. Weet je nog van die tussenstand “Halverwege”? Die komt nu aan de beurt. Acties in opdrachten die je met je stem activeert, mogen niet langer dan 10 seconden duren. En het bureau heeft helaas 15 seconden nodig om van hoog naar laag te bewegen. De enige oplossing is dus, om het bureau in twee stappen in hoogte te verstellen.

Open een van de opdrachten en voeg vooraan een extra actie ‘Move desk to position’ toe, maar kies nu de stand ‘Halverwege’. Je begrijpt vast wat er dan gebeurt. Die twee stappen zijn iets minder magisch, maar het werkt wel.

Als je het een paar keer hebt geprobeerd, wil je nooit meer anders.

Een tenslotte. Laat je collega’s tijdens een Team-vergadering eens zien hoe je je bureau met je stem instelt. Succes en plezier verzekerd.

## De toekomst: automatisering met Home Assistant

Op dit moment kan ik het bureau nog niet instellen via [Home Assistant][homeassistant]. Daarvoor bestaat [een ESP Home module  die via Bluetooth kan verbinden met het bureau][esphome]. Als ik dat voor elkaar krijg, kan ik het verstellen van het bureau zelfs automatiseren. Bijvoorbeeld het bureau automatisch op stahoogte instellen als ik 1 uur gezeten heb, of als ik deelneem aan een Teams-vergadering.
De mogelijkheden zijn oneindig. Een leuk projectje voor een rustig moment in een winter.

[deskcontrol]: https://apps.apple.com/nl/app/desk-control/id1203254365
[idasencontroller]: https://apps.apple.com/nl/app/id%C3%A5sen-controller/id1562124476
[homeassistant]: https://home-assistant.io/
[esphome]: https://github.com/j5lien/esphome-idasen-desk-controller
