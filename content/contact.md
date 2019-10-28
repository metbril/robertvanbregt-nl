---
title: Contact
layout: page
permalink: /contact
navigation_weight: 90
navigation_title: Contact
sitemap: false
menu: 
  main:
    name: Contact
    weight: 90
---
Leuk dat je hier bent.

Zoek je contact, dan kan dat eenvoudig en snel via deze pagina.

Gebruik onderstaand formulier wel met verstand. Wees je er van bewust, voordat je dit formulier gebruikt, dat deze gegevens onversleuteld via een service van [Formspree](https://formspree.io) over het Internet worden verzonden.

Wil je me iets vertrouwelijks toesturen, doe dat dan in een bericht met [Signal](https://www.signal.org/) of stuur me een email met [ProtonMail](https://www.protonmail.com). En alleen als dat echt niet lukt, [stuur me dan een prive-bericht met Twitter](https://twitter.com/metbril).

<form action="https://formspree.io/contact@robertvanbregt.nl"
          method="POST">
        <table>
        <tr><td>Naam:</td><td><input type="text" name="name" placeholder="je naam" required /></td></tr>
        <tr><td>Email: </td><td><input type="email" name="_replyto" placeholder="je email" required /></td></tr>
        <tr><td>Onderwerp: </td><td><input type="text" name="_subject" placeholder="je onderwerp" required /></td></tr>
        <tr><td>Bericht:</td><td><textarea name="message" placeholder="je bericht"  rows="4" cols="50"></textarea></td></tr></table>
        <button type="submit">Verzenden</button>
        <input type="hidden" name="_next" value="{{ "/bedankt" | prepend: site.baseurl | prepend: site.url }}" />
        <input type="hidden" name="_format" value="plain" />
        <input type="text" name="_gotcha" style="display:none" />
        <input type="hidden" name="_language" value="nl" />
</form>