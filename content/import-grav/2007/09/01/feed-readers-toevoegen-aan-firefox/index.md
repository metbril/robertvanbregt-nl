---
title: Feed readers toevoegen aan Firefox
post_id: 1722
date: '2007-09-01T05:45:00+00:00'
published: true
taxonomy:
    migration-status: review
    category: [Ongecategoriseerd]
    tag: [computers,feeds,firefox,internet,javascript,programmeren,rss,computers,feeds,firefox,internet,javascript,programmeren,rss]
author: Robert van Bregt
metadata:
    author: Robert van Bregt
---
![Firefox](http://bp2.blogger.com/_N9rpl2-ad9s/Rtj4pueefXI/AAAAAAAAAD8/2RnkFeRl7SI/s144/firefox-mac.jpg)  
 In vorige versies van [Firefox](http://www.firefox.com/) kon ik via de Live Feeds optie eenvoudig een feed toevoegen aan [Google Reader](http://www.google.nl/reader/). Sinds kort, ik weet niet wat er gebeurd is, kan ik via de Google Reader optie alleen nog maar een feed toevoegen aan [iGoogle](http://www.google.nl/ig). En dat wil ik niet. Daarom heb ik maar weer even wat rondgesnuffeld om uit te zoeken hoe ik nieuwe feed readers toe kan voegen aan Firefox. Blijkt daar een mooie [API](http://developer.mozilla.org/en/docs/DOM:window.navigator.registerContentHandler) voor te bestaan.

WordPress staat geen javascript toe, dus kopieer onderstaande link en vervang eventjes de **http://** door **javascript:**:  
[Google Reader toevoegen aan Firefox](http://window.navigator.registerContentHandler%28%27application/vnd.mozilla.maybe.feed%27,%27http://www.google.com/reader/view/feed/%s%27,%27Google%20Reader%27%29;)