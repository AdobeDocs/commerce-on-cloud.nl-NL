---
title: Site starten
description: Leer hoe u begint met het voorbereiden van de lancering van de site.
exl-id: 95abc7aa-ed4d-44f7-96aa-517c646bc00d
source-git-commit: 38ac38d4edd0f317155d0d4537021a29a21d5761
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Site starten

Wanneer u de implementatie en het testen in integratie- en staging-omgevingen hebt voltooid, kunt u beginnen met het voorbereiden van de start van de site. Eerst moet u alle ontwikkelings- en testbewerkingen voltooien voordat u in de productieomgeving gaat werken. Bent u klaar om te starten? Controlelijsten, aanbevolen procedures en laatste stappen om uw site te starten.

Als u deze informatie vóór het opstellen en het testen in het Staging controleerde, overweeg de voordelen van het testen in het Staging eerst in de volgende sectie. Staging is een omgeving in de buurt van de productie die wordt uitgevoerd op vergelijkbare hardware, configuraties, architectuur en services. Het kan uw onderbreking verminderen en uw uitbreiding maken, de dienst, douaneconfiguraties, en het Testen van de Erkenning van de Bedrijfs van de Gebruiker vitale componenten om uw plaatsen en opslag vrij te geven.

## Waarom volledig testen in integratie, staging, en productie?

Wij adviseren ten zeerste het testen in de milieu&#39;s van de Integratie, het Staging, en van de Productie wegens de ingewikkeldheid om ervoor te zorgen dat uw douanecode, thema&#39;s, uitbreidingen, en derdesintegratie allen samenwerken om uw opslag in werking te stellen. De volgende algemene problemen kunt u ontdekken en oplossen wanneer u het testen in de milieu&#39;s van de Integratie en van het Staging voltooit alvorens uw milieu van de Productie bij te werken:

- Het opvoeren steunt alle diensten van de Productie, eigenschappen, gegevensbestandgegevens, technologiestapel, architectuur, en meer. Het weerspiegelt Productie, wat betekent als de fouten in het Opvoeren voorkomen, hebt u een waarschuwing alvorens zij in Productie voorkomen.

- De code die in uw lokale integratiemilieu werkt zou niet in het Opvoeren en van de Productie milieu&#39;s kunnen werken.

- De milieu&#39;s van de integratie steunen niet sommige diensten die in het Opvoeren en Productie, zoals Fastly en New Relic beschikbaar zijn.

- [ test volledig ](../test/guidance.md) uw plaats met diverse hulpmiddelen in het Opvoeren voor lading, stress, prestaties, en plaatselementen.

- Omdat integratieomgevingen alleen databases hebben die zijn gevuld met testgegevens en die niet overeenkomen met een productieachtige omgeving, kunnen er extra fouten of onverwacht gedrag optreden tijdens het testen in testomgevingen of productieomgevingen.

## Vereisten voor het starten van de site

U hebt de volgende informatie en bronnen nodig als voorbereiding op het starten van de site:

- CNAME-recordgegevens voor het configureren van de DNS

- Lijst met alle storefront-domeinen die aan het certificaat moeten worden toegevoegd

- SSL/TLS-certificaat

Als onderdeel van Adobe Commerce voor een abonnement op een cloudinfrastructuur biedt Adobe een door domein gevalideerd SSL/TLS-certificaat dat is uitgegeven door Let&#39;s Encrypt. Elke ProProductie, het Staging, en milieu van de Productie van de Aanzet (`master`) heeft een uniek certificaat dat alle domeinen en subdomeinen in dat milieu behandelt. Deze certificaten worden provisioned en aan uw plaats automatisch geupload nadat u uw DNS configuratie voor ontwikkeling en productie bijwerkt. Zie [ Levering SSL/TLS certificaten ](../cdn/fastly-configuration.md#provision-ssltls-certificates).

>[!NOTE]
>
>Als u uw eigen Uitgebreide SSL van de Bevestiging voor uw bedrijf in plaats van het gebruiken van het certificaat van de Encryptie van de Let wilt opstellen, contacteer uw CTA of [ leg een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voor.

## Het gereedschap Beveiligingsscan instellen

>[!NOTE]
>
>Het hulpmiddel van het veiligheidsaftasten gebruikt de volgende openbare IP adressen:
>
>```text
>52.87.98.44
>34.196.167.176
>3.218.25.102
>```
>
>Voeg deze IP adressen aan een lijst van gewenste personen in uw regels van de netwerkfirewall toe om het hulpmiddel toe te staan om uw plaats af te tasten. Het hulpmiddel richt verzoeken aan havens 80 en 443 slechts.

Met het hulpprogramma Beveiligingsscan kunt u regelmatig uw winkelwebsites controleren en updates ontvangen voor bekende beveiligingsrisico&#39;s, malware en verouderde software. Dit hulpmiddel is een gratis dienst beschikbaar voor alle implementaties en versies van Adobe Commerce op wolkeninfrastructuur. U hebt toegang tot het hulpmiddel door uw [ rekening van Commerce Marketplace ](https://account.magento.com/customer/account/login).

- De beveiligingsstatus van uw sites controleren en beveiligingsupdates toepassen

- Beveiligingsupdates en sitespecifieke meldingen ontvangen

>[!NOTE]
>
>Adobe raadt u aan het hulpprogramma Beveiligingsscan te gebruiken in plaats van andere hulpmiddelen van derden om de beste kwaliteit van de service tijdens het onderzoek naar de bevindingen te garanderen.

Zie de [ Gids van de Gebruiker ](https://experienceleague.adobe.com/nl/docs/commerce-admin/systems/security/security-scan) voor informatie over vestiging en het gebruiken van het hulpmiddel van het veiligheidsaftasten. Doorgaans gebruikt u dit gereedschap wanneer u met het testen van gebruikersacceptatie (UAT) begint.

Elke site die u scant, moet zijn geregistreerd via het tabblad Beveiligingsscan. Tijdens het registratieproces moet u de disclaimer accepteren voordat u kunt beginnen met scannen. U beheert het schema en machtigt de gebruiker om meldingen te ontvangen wanneer elke scan is voltooid. U kunt scans voor een specifieke, terugkomende datum en tijd plannen, of een aftasten in werking stellen wanneer nodig.

Het hulpmiddel van het Scannen van de Veiligheid gebruikt verscheidene koorden van gebruikersagent om malwaresactiviteit in real time te simuleren. U zou de volgende gebruikersagenten in uw analyses of toegangslogboeken kunnen zien:

```text
Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:57.0) Gecko/20100101 Firefox/57.0
GuzzleHttp/6.3.3 curl/7.29.0 PHP/7.1.18
Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2062.120 Safari/537.36
Visbot/2.0 (+http://www.visvo.com/en/webmasters.jsp;bot@visvo.com)
```

## Uw site doorzoeken

1. Heb toegang tot uw [ rekening van Commerce Marketplace ](https://account.magento.com/customer/account/login).

1. Klik het Scanlusje van het Scannen van de Veiligheid en selecteer **gaan naar het Scannen van de Veiligheid**.

1. In de _kolom van Acties_ voor de plaats, uitgezochte **Scannen van de Looppas**. De geplande scan wordt weergegeven met de meldingsstatus.

### U kunt als volgt het rapport bekijken:

1. Wanneer het rapport voltooit, toont een berichtvertoningen.

1. In de plaatstrij, selecteer het rapport u van de **kolom van Rapporten** wilt bekijken. De volgorde is het meest recent.

Het rapport bevat een overzicht van problemen, zoals mislukte scans, niet-geïdentificeerde resultaten en geslaagde scans. Elk item bevat gedetailleerde informatie over de scan, een lijst met problemen die moeten worden onderzocht en de acties die moeten worden ondernomen. Voor sommige van deze handelingen moeten mogelijk beveiligingspatches worden gedownload en geïnstalleerd. Voeg om het even welke vereiste flarden aan een ontwikkelingstak op uw lokale werkstation toe alvorens hen aan de productievak toe te voegen.

De scanresultaten bevatten een label met een beschrijving van de status geslaagd of gezakt door de scan en gedetailleerde informatie over de uitgevoerde controles:

- &quot;Mislukt&quot; geeft aan dat de website een ernstige kwetsbaarheid bevat.

- &quot;Niet geïdentificeerd&quot;stelt voor dat een diepgaande overzicht door uw team of ontvangende leverancier wordt vereist om te bepalen als de verdere actie wordt vereist.

De resultaten van de scan geven ook suggesties voor herstelstappen voor elke mislukte beveiligingstest. De resultaten van beveiligingsscans zijn alleen beveiligd en kunnen door de geregistreerde gebruiker worden weergegeven. Alleen gebruikers die zijn aangewezen in het siteregistratieproces ontvangen berichten over het voltooien van de scan.

## Klaar om uw site te starten

Ga als volgt te werk wanneer u klaar bent om de site te starten:

- [Checklist starten](checklist.md)

- [Stappen starten](steps.md)
