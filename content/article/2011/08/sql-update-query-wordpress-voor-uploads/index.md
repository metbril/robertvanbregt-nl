---
title: SQL update query WordPress voor uploads
post_id: 1429
date: '2011-08-25T11:16:25+00:00'
published: true
taxonomy:
    migration-status: review
    category: [Ongecategoriseerd]
tags: [bloggen,wordpress,bloggen,wordpress]
author: Robert van Bregt
metadata:
    author: Robert van Bregt
---
![](/wp-content/uploads/2011/08/wordpress-logo-150x150.png "wordpress-logo")Ik heb mijn weblog verplaatst van de subfolder `/blog/` naar `/`. Een van de zaken die **echt** handmatig moest worden geregeld was het wijzigen van de URI naar de geuploade afbeeldingen. Daar zat ik niet op te wachten. Dat moest toch handiger kunnen. En dat kan natuurlijk ook; met een UPDATE query op de mySQL database. Altijd een beetje tricky, en ik heb dat niet zo heel vaak gedaan. Dus heb ik een goede backup van de database gemaakt en toen het volgende statement losgelaten:

 
    UPDATE `wp_posts` SET post_content = replace(post_content, "/blog/wp-content/", "/wp-content/") WHERE `post_content` LIKE '%/blog/wp-content/%' 

In *0.0085 seconden* was het gepiept.

Nu weer lekker verder schrijven.