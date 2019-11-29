---
title: 'Post Kinds in het Nederlands'
date: 2019-11-22T09:59:00+01:00
tags:
    - indieweb
    - meta
    - wordpress
syndicateto:
    - https://news.indieweb.org/nl/robertvanbregt.nl/2019/11/22/post-kinds-in-het-nederlands/
---
Mijn website is gebaseerd op de uitgangspunten van het IndieWeb. Daarvoor maak ik, onder andere, gebruik van de [Post Kinds](https://wordpress.org/plugins/indieweb-post-kinds) plugin. Die is gebouwd door de Amerikaan [David Shanske](https://david.shanske.com/), waardoor alles in het engels is. Een deel van de teksten zijn netjes vertaald of te vertalen, maar niet alles.

De plugin maakt 'Kinds' aan van IndieWeb berichten (['posts'](https://indieweb.org/posts)) met behulp van een nieuwe taxonomie. Een lijst met alle artikelen zijn daarvoor bijvoorbeeld standaard bereikbaar via de link `/kind/article`. Dat wil ik ook nog eens in het Nederlands hebben, maar voor nu neem ik genoegen met Nederlandstalige omschrijvingen.

De manier om daar bij te komen zit een beetje verstopt. De plugin heeft dat nog niet toegankelijk gemaakt. Maar via een omweg kan dat wel. Hieronder de stappen:

**Stap 1:** Ga naar het Dashboard, en kies het Berichten menu. Je ziet daar nu onder andere een link naar Categorieën en Tags.

**Stap 2:** Klik op 'Tags'. Je komt dan in het onderhoudsgedeelte voor je tags. In de adresbalk van je browser zie je nu een link die eindigt op `wp-admin/edit-tags.php?taxonomy=post_tag`.

**Stap 3:** Pas de link in de adresbalk aan. Vervang `post_tag` door `kind` en druk op de Enter-toets. De pagina voor het beheren van de 'Kinds' taxonomie wordt voor je geopend.

Nu kun je aan de slag!