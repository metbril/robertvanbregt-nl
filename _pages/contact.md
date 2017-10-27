---
title: Contact
layout: page
permalink: /contact
navigation_weight: 90
navigation_title: Contact
sitemap: false
---
Leuk dat je hier bent.

Zoek je contact, dan kan dat eenvoudig en snel via deze pagina.

Gebruik onderstaand formulier wel met verstand. Wees je er, voordat je dit formulier gebruikt, van bewust dat deze gegevens onversleuteld via een service van [Formspree](https://formspree.io) worden over het Internet worden verzonden.

Wil je me iets vertrouwelijks toesturen, doe dat dan in een bericht met [Signal](https://www.signal.org/) of stuur me een email met [ProtonMail](https://www.protonmail.com). En alleen als dat echt niet lukt, [stuur me dan een prive-bericht met Twitter](https://twitter.com/direct_messages/create/metbril).

<form action="https://formspree.io/contact@robertvanbregt.nl"
      method="POST">
    <input type="text" name="name" placeholder="je naam" /><br />
    <input type="email" name="_replyto" placeholder="je email" /><br />
    <textarea name="message" placeholder="je bericht"  rows="4" cols="50"></textarea><br />
    <button type="submit">Verzenden</button>

    <input type="hidden" name="_subject" value="Contactformulier" />
    <input type="hidden" name="_next" value="{{ "/bedankt" | prepend: site.baseurl | prepend: site.url }}" />
    <input type="hidden" name="_format" value="plain" />
    <input type="text" name="_gotcha" style="display:none" />
</form>
