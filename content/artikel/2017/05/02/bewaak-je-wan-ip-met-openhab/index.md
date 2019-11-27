---
title: Bewaak je WAN IP met openHAB
date: '2017-05-02T21:21:04+00:00'
tags: [computers,netwerk,openhab,huisautomatisering]
syndicate-to:
    - https://community.openhab.org/t/how-to-monitor-a-dynamic-wan-ip-address/11368
    - https://github.com/openhab/openhab1-addons/wiki/Samples-Tricks#how-to-monitor-a-dynamic-wan-ip-address
---
*(Dit artikel heb ik in het Engels eerder geplaatst op het [openHAB forum](https://community.openhab.org/t/how-to-monitor-a-dynamic-wan-ip-address/11368) en in de [openHAB wiki](https://github.com/openhab/openhab1-addons/wiki/Samples-Tricks#how-to-monitor-a-dynamic-wan-ip-address))*

## Het probleem

De meeste Internet Service Providers (ISP) voorzien je van een dynamisch IP-adres.  
 Dit adres kan in de loop van de tijd veranderen.  
 Als je op dit adres vertrouwt, bijvoorbeeld om een computer binnen je thuisnetwerk te benaderen, wil je dit adres misschien in de gaten houden.

## De oplossing

Websites zoals [icanhazip](http://icanhazip.com) geven je publieke IP-adres terug als platte tekst.  
 Deze kun je met openHAB prima verwerken en bijhouden in een item.  
 Een ‘rule’ (regel) bewaakt wijzigingen van het item en acteert daarop.

## Voorwaarden

Voor deze toepassing is het nodig dat je de HTTP Binding al hebt geinstalleerd.

Opmerking: Wees aardig voor de website die je aanroept.  
 Roep deze liefst eens per 5 minuten aan, maar zeker niet vaker dan iedere minuut.

## Configuratie

**valid_ip.js**

Dit script controleert of het antwoord van de website een geldig IP adres is.  
Soms gebeurt het dat de pagina een foutmelding geeft.  
Die wordt hiermee voorkomen.

```javascript
// return valid IP or '-'
(function(ip) {

    // remove blanks first
    ip = ip.replace(/\s/g, '');

    // http://stackoverflow.com/a/26445549
    var rx=/^(?!.*\.$)((1?\d?\d|25[0-5]|2[0-4]\d)(\.|$)){4}$/;
    if (rx.test(ip)) {
    return (ip);
    }
    else {
    return "-";
    }
})(input)
// input variable contains data passed by openhab
```

**demo.items**

Bij het item kun je instellen hoe vaak je het wilt controleren.  
 Een keer per uur is eigenlijk voldoende.

```
// check for WAN IP address changes every 60 mins (3600 seconds)
String Network_WAN_IP "WAN IP address [%s]" <network> (Network) { http="<[http://icanhazip.com:3600000:JS(valid_ip.js)]"
```

**demo.rules**

Deze regel “gaat af” zodra het IP adres wijzigt.  
 Bij het opstarten van openHAB is de waarde leeg,  
 dus de eerste wijziging moet je negeren.

```
rule "Monitor WAN IP"
when
    Item Network_WAN_IP changed
then
    if (previousState != NULL) { // NULL when system started
        val currentState = Network_WAN_IP.state
        if (currentState == "-") {
            logError('MonitorWanIp', 'Unable to determine WAN IP')
        }
        else {
            logInfo('MonitorWanIp', 'WAN IP has changed to: ' + currentState)
        }
    }
end
```

**demo.sitemap**

```
sitemap demo label="Demo" {
    Frame {
        Text item=Network_WAN_IP
    }
}
```