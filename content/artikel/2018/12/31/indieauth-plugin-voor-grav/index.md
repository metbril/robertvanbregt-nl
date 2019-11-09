---
title: 'IndieAuth plugin voor Grav'
date: '2018-12-31 09:49:00'
tags:
    - indieweb
    - grav
---

Vanochtend heb ik een eerste versie van de <a href="https://github.com/metbril/grav-plugin-indieauth" target="_blank" rel="noopener">IndieAuth plugin voor Grav</a> werkend gekregen. Binnenkort zal deze ook beschikbaar zijn via de Grav Plugin Manager.
<!--more-->
Het is vakantie. Dus had ik weer wat tijd om aan mijn website te werken. De overstap van WordPress naar Grav wil ik echter pas maken zodra ik gebruik kan maken van een robuuste [Webmention](https://indieweb.org/Webmention) en [Micropub](https://indieweb.org/Micropub) functie. Voor die laatste is het nodig om te kunnen authenticeren. Daarvoor is het [IndieAuth protocol](https://indieauth.spec.indieweb.org/) beschikbaar en de eenvoudige implementatie daarvan via de website IndieAuth.com.

Je kunt de benodigde configuratie daarvan eenvoudig opnemen in de content van je website, maar het is wel zo netjes en eenvoudig om dit met een simpele, basale plugin te kunnen doen.

Zo'n plugin was er nog niet, is vrij eenvoudig te maken en dus een mooie manier om mijn kennis van PHP en Grav in het bijzonder te vergroten. De hele maand december loopt bovendien de <a href="https://indieweb.org/2018-12-indieweb-challenge" target="_blank" rel="noopener">IndieWeb challenge</a> nog, dus het leek me wel een idee om dat snel nog voor elkaar te krijgen. Met succes.