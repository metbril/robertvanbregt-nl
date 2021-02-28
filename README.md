[![Netlify Status](https://api.netlify.com/api/v1/badges/c2dd1d8f-70bf-4823-bbe3-e0beeab0871b/deploy-status)](https://app.netlify.com/sites/robertvanbregt/deploys)
[![Netlify](https://img.shields.io/netlify/c2dd1d8f-70bf-4823-bbe3-e0beeab0871b)](https://app.netlify.com/sites/robertvanbregt/deploys)
[![Uptime Robot ratio (30 days)](https://img.shields.io/uptimerobot/ratio/m778967457-ef70f48943056678f234ac2b)](https://stats.uptimerobot.com/9987YCk75y/778967457)
[![Website](https://img.shields.io/website?url=https%3A%2F%2Frobertvanbregt.nl)](https://robertvanbregt.nl)

# robertvanbregt.nl

## IndieWeb

De site is gebaseerd op principes van het [IndieWeb](https://indieweb.org/). 
De meeste zaken worden geregeld door het [Grotius thema](https://robertvanbregt.nl/hugo-grotius).

Mijn site heeft in ieder geval gebruik van:

- [IndieAuth](https://indieweb.org/IndieAuth). Ik gebruik mijn domeinnaam als identiteit om mee in te loggen.
- [Micropub](https://indieweb.org/Micropub). Hiermee kan ik eenvoudig berichten plaatsen op de site.
- [Webmention](https://indieweb.org/Webmention). Je kunt reageren op berichten op de site door een Webmention te sturen.

## Permalinks

Permalinks naar berichten zijn altijd een pad vanaf de root van de server met `/<jaar>/<maand>/<dag>/<slug>/`. Deze staat los van de organisatie van de content in het CMS.

In sommige CMS'en moet de slug uniek zijn binnen de gehele site (WordPress, Grav), maar voor mijn structuur is dat niet nodig. Het is voldoende als de volledige permalink uniek is.

## Organisatie van content

### Secties

Voor het [Grotius thema](https://robertvanbregt.nl/hugo-grotius) is het nodig alle post types op te slaan in een aparte sectie. 
En daarmee in een aparte hoofdmap binnen de map `content`.

### Submappen

Binnen een sectie kan het aantal mappen (1 per gepubliceerde pagina) daardoor flink oplopen. 
Een vorm van organisatie is daarom op zijn plaats. 
Bijvoorbeeld om op datum berichten te kunnen terugvinden. 
Dat kan door de datum vooraan op te nemen in de mapnaam, of door de mappen in een diepere structuur van submappen te bewaren. 
Ik heb er voor gekozen dezelfde indeling aan te houden als de permalink structuur. 
Vaak zal er dan maar 1 of een enkel bericht per datum zijn. 
Met alleen een map per datum blijft dat aantal nog steeds behoorlijk over de jaren heen en een map per jaar geeft wel meer organisatie, maar daarbinnen loopt het dan toch nog flink op. Kortom, toch maar een diep geneste structuur. 

### Page Bundles

Uitgangspunt is, om een pagina en de bijbehorende resources (afbeeldingen, video, audio etc.) bij elkaar te houden. Dit kan door ze bij elkaar in een map op te slaan. Hugo noemt dat [Page Bundles](https://gohugo.io/content-management/organization/#page-bundles).

## Post Types

### Artikelen

Artikelen zijn per datum georganiseerd in Page Bundles.

### Notities

Notities worden allemaal opgeslagen in één map. De bestandsnaam is de epoch timestamp. De permalink is gemaakt uit de datum en de filename. 

Aannames: 

- Notities hebben geen titel. Om geen slug in het bestand te hoeven opslaan, 
- Notities hebben geen afbeelding. Daarom hoeven ze niet als page bundle te worden bewaard.

### Bladwijzers

### Likes

### Reacties
