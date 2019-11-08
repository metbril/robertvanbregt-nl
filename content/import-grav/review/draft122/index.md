---
title: Twitter met Growl en Quicksilver
post_id: 122
date: '2009-08-12T07:03:04+00:00'
published: false
taxonomy:
    migration-status: review
    category: [Ongecategoriseerd]
    tag: [apple,mac,osx,twitter,apple,mac,osx,twitter]
author: Robert van Bregt
metadata:
    author: Robert van Bregt
---
Je kunt twitteren via de normale web client, maar het jezelf ook gemakkelijk maken met Quicksilver en Growl.

1. Installeer de Xcode Tools (staan in de Optional Installs op de DVD)
2. Installeer de Ruby Twitter Gem
3. Installeer growlnotify
4. Installeer de twitter monitor

**Installeer de Xcode Tools**  
 Vreemd genoeg moet je als eenvoudige eindgebruiker de Xoce ontwikkelomgeving van Apple installeren. Eigenlijk is dat alleen maar nodig om voor het gebruik van Rubu de foutmelding “can’t find header files for ruby” te voorkomen.

**Installeer de Ruby Twitter Gem**  
 Met de twitter gem is het mogelijk om via de commando-regel in een terminal venster een tweet te versturen.

> sudo gem update<br></br>
>     sudo gem install twitter

Vul vervolgens in het bestand ~/.twitter je Twitter naam en wachtwoord in. Als je dit goed hebt gedaan, kun je via de commandoregel de twitter status opvragen of bijvoorbeeld een tweet versturen.

> twitter timeline<br></br>
>     twitter post "Tweet met de Ruby Twitter Gem"

**Installeer growlnotify**  
 In de map Extras van de Growl diskimage is growlnotify toegevoegd. Met deze tool kun je Growl berichten versturen via de commando-regel.