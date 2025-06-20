---
title: Overzicht van snelle services
description: Leer hoe u met de snelste services die bij Adobe Commerce worden geleverd via de cloudinfrastructuur de levering van inhoud voor uw Adobe Commerce-sites kunt optimaliseren en beveiligen.
feature: Cloud, Configuration, Iaas, Paas, Cache, Security, Services
exl-id: 429b6762-0b01-438b-a962-35376306895b
source-git-commit: 3cef442321120d8ca813c760d2fd0435f4961235
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 0%

---

# Overzicht van snelle services

>[!WARNING]
>
>Als u de PCI-compatibiliteit wilt behouden voor Adobe Commerce-sites die op het Cloud-platform worden geïmplementeerd, stelt u snel in op uw Starter-hoofdvertakking, Pro Production en Pro Staging-omgevingen. Als u Adobe Commerce in een headless plaatsing gebruikt, adviseren wij hoogst dat u snel gebruikt om de reacties van GraphQL in het voorgeheugen onder te brengen. Zie [ Caching met Fastly ](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly) in de *Gids van de Ontwikkelaar van GraphQL*.

In Fastly worden de volgende services geleverd voor het optimaliseren en beveiligen van de levering van inhoud voor Adobe Commerce voor infrastructuurprojecten in de cloud. Deze services worden zonder extra kosten meegeleverd bij Adobe Commerce op cloudinfrastructuur.

- **het Netwerk van de Levering van de Inhoud (CDN)** - de op vernis-Gebaseerde dienst die uw plaatspagina&#39;s, activa, CSS, en meer in de centra van achtergrondgegevens in de cache plaatst u opstelling. Wanneer klanten toegang krijgen tot uw site en winkels, kunnen ze sneller in cache geplaatste pagina&#39;s laden. De CDN-service biedt de volgende functies:

- **beheer van het Geheime voorgeheugen** - Geheime voorgeheugen uw plaatspagina&#39;s, activa, CSS, en meer in achterste gegevenscentra die u opstelling om bandbreedtetoevoer en kosten te drukken

   - Het gebruik {de fragmenten van 0} snel douaneVCL [&#128279;](fastly-vcl-custom-snippets.md) (Varnish 2.1 volgzaam) om te wijzigen hoe het in het voorgeheugen onderbrengen aan verzoeken beantwoordt

   - De de dienststeun van de opstelling [ GeoIP ](fastly-custom-cache-configuration.md#configure-geoip-handling)

   - [Niet-gecodeerde aanvragen forceren naar TLS](fastly-custom-cache-configuration.md#force-tls)

   - [ pas Snelle onderbreking ](fastly-custom-cache-configuration.md#extend-fastly-timeout) montages aan om 503 reacties op bulkbewerkingsverzoeken te verhinderen

   - Creeer [ pagina&#39;s van de de foutenreactie van de douanefout ](fastly-custom-response.md)

- **Veiligheid** - nadat u de Snelle diensten voor de plaatsen van Adobe Commerce toelaat, zijn de extra veiligheidseigenschappen beschikbaar om uw plaatsen en netwerk te beschermen:

   - [&#128279;](fastly-waf-service.md) (WAF) - de Beheerde dienst van de de firewalltoepassing van het Web van 0&rbrace; Firewall van de Toepassing van het Web die PCI-Volgzame bescherming verleent om kwaadwillig verkeer te blokkeren alvorens het uw productieAdobe Commerce op de plaatsen van de wolkeninfrastructuur en netwerk kan beschadigen.  De WAF-service is alleen beschikbaar in Pro- en Starter Production-omgevingen.

   - [ Verdeelde Ontkenning van de bescherming van de Dienst (DDoS) ](#ddos-protection) - ingebouwde bescherming DDoS tegen gemeenschappelijke aanvallen zoals het Pingelen van Dood, de aanvallen van Smurf, en andere op ICMP-Gebaseerde overstromingsaanvallen.

   - [ SSL/TLS certificaten ](fastly-configuration.md#provision-ssltls-certificates) - de sneldienst vereist een SSL/TLS certificaat om veilig verkeer over HTTPS te dienen.

     Adobe Commerce biedt een door een domein gevalideerd SSL/TLS-certificaat voor elke staging- en productieomgeving. Adobe Commerce voltooit domeinvalidatie en certificaatprovisioning tijdens het installatieproces van Snel.

- **Oorsprong het camoufleren** - verhindert verkeer om snel WAF te mijden en verbergt de IP adressen van uw oorsprongsservers om hen tegen directe toegang en aanvallen te beschermen DDoS.

  Oorspronkelijke camouflage is standaard ingeschakeld in Adobe Commerce op cloudinfrastructuur Pro Production-projecten. Om oorsprong het camoufleren op Adobe Commerce op de projecten van de Productie van de Aanzet van de wolkeninfrastructuur toe te laten, leg een [ kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voor. Als u verkeer hebt dat geen caching vereist, kunt u de Fastly de dienstconfiguratie aanpassen om verzoeken toe te staan om [ het Fastly geheime voorgeheugen ](fastly-vcl-bypass-to-origin.md) te mijden.

- **[optimalisering van het Beeld](fastly-image-optimization.md)** - ontlaadt beeldverwerking en het resizing lading aan de Snelle dienst zodat de servers orden en omzettingen efficiënter kunnen verwerken.

- **[snel CDN en de logboeken van WAF](../monitor/new-relic-service.md#new-relic-log-management)** - voor Adobe Commerce op de Pro projecten van de wolkeninfrastructuur, kunt u de dienst van Logs van New Relic gebruiken om snel CDN en het logboekgegevens van WAF te herzien en te analyseren.

## Fastly CDN module for Magento 2

De snelle diensten voor Adobe Commerce op wolkeninfrastructuur gebruiken de [ snelste CDN module voor Magento 2 ] die in de volgende milieu&#39;s wordt geïnstalleerd: Pro Staging en Productie, de Productie van de Aanzet (`master` tak).

Bij de initiële provisioning of upgrade van uw Adobe Commerce-project installeert Adobe de nieuwste versie van de Fastly CDN-module in uw Staging- en Productomgevingen. Als u de updates van de module Fastly loslaat, ontvangt u meldingen in Admin voor uw omgevingen. Adobe raadt u aan uw omgevingen bij te werken om de nieuwste versie te gebruiken. Zie [ Snelle Verbetering ](fastly-configuration.md#upgrade-the-fastly-module).

## Snelle de dienstrekening en geloofsbrieven

Adobe Commerce on cloud Infrastructure projects krijgt geen toegewezen Fastly account. De snelservice wordt beheerd in een gecentraliseerde account die bij Adobe is geregistreerd, en het beheerdashboard is alleen toegankelijk voor het ondersteuningsteam voor cloud.

In plaats daarvan heeft elke omgeving voor Staging en Productie unieke Fastly-referenties (API-token en service-id) voor het configureren en beheren van Fastly-services van Commerce Admin. De snelste API is beschikbaar voor het uitvoeren van geavanceerd beheer van de sneldienst, die de geloofsbrieven zal vereisen om die verzoeken voor te leggen.

Tijdens projectlevering, voegt Adobe uw project aan de Fastly de dienstrekening voor Adobe Commerce op wolkeninfrastructuur toe en voegt de Fastly geloofsbrieven aan de configuratie voor de het Opvoeren en milieu&#39;s van de Productie toe. Zie [ krijgen de Snelle geloofsbrieven ](fastly-configuration.md#get-fastly-credentials).

### Fastly API-token wijzigen

Verzend een kaartje van de Steun van Adobe Commerce om een nieuwe Fastly API symbolische referentie [ uit te geven als het bevestiging/is verlopen ](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/error-when-validating-fastly-credentials) ontbreekt, of als u gelooft dat het is gecompromitteerd.

Wanneer u het nieuwe token ontvangt, werkt u de omgeving voor Staging of Productie bij om het nieuwe token te gebruiken.

**om de Fastly API symbolische referentie** te veranderen:

1. [ legt een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voor het vragen van nieuwe Fastly API geloofsbrieven.

   Neem uw Adobe Commerce op in de projectid van de cloud-infrastructuur en de omgevingen die een nieuwe referentie vereisen.

1. Nadat u het nieuwe API teken ontvangt, werk de symbolische waarde van API in de [ Snelle geloofsconfiguratie ](fastly-configuration.md#test-the-fastly-credentials) in Admin of van de [[!DNL Cloud Console]  milieuvariabelen ](../project/overview.md#configure-environment) bij.

1. [ Test de nieuwe referentie ](fastly-configuration.md#test-the-fastly-credentials).

1. Nadat u de referentie hebt bijgewerkt, verzendt u een Adobe Commerce-ondersteuningsticket om de oude API-token te verwijderen.

### Meerdere snelaccounts en toegewezen domeinen

U kunt snel alleen een apex-domein en de bijbehorende subdomeinen toewijzen aan één Fastly-service en -account. Als u een bestaande snelaccount hebt waarmee dezelfde map en subdomeinen die voor uw Adobe Commerce-site worden gebruikt, worden gekoppeld, hebt u de volgende opties:

- Verwijder de apex- en subdomeinen van het bestaande account voordat u de Fastly-servicegegevens aanvraagt voor uw Adobe Commerce in een cloud-infrastructuurprojectomgeving. Zie [ Werkend met Domeinen ] in de Fastly documentatie.

  Gebruik deze optie om het apex-domein en alle subdomeinen te koppelen aan het Fastly-serviceaccount voor Adobe Commerce op cloudinfrastructuur.

- Verzend een Adobe Commerce-ondersteuningsticket om domeindelegatie aan te vragen, zodat apex en subdomeinen aan verschillende accounts kunnen worden gekoppeld.

  Gebruik deze optie als u een ex-domein hebt met meerdere subdomeinen voor Adobe Commerce- en niet-Adobe Commerce-sites en u deze subdomeinen wilt koppelen aan verschillende snelaccounts.

#### Domeindelegatie aanvragen

*Scenario 1:*

Het apex-domein (`testweb.com` en `www.testweb.com` ) is gekoppeld aan een bestaande Fastly-account. U hebt een Adobe Commerce on cloud Infrastructure-project geconfigureerd met de volgende subdomeinen: `mcstaging.testweb.com` en `mcprod.testweb.com` . U wilt het apex-domein niet verplaatsen naar het Fastly-serviceaccount voor Adobe Commerce op cloudinfrastructuur.

Verzend a [ snel steunkaartje ] verzoekend dat subdomeinen van de bestaande Fastly rekening aan de Fastly rekening voor Adobe Commerce op wolkeninfrastructuur worden gedelegeerd. Neem uw Adobe Commerce-project-id op in het ticket.

Nadat de delegatie is voltooid, kunnen uw projectsubdomeinen aan de Fastly de dienstrekening voor Adobe Commerce op wolkeninfrastructuur worden toegevoegd. Zie [ krijgen de Snelle geloofsbrieven ](fastly-configuration.md#get-fastly-credentials).

*Scenario 2:*

Het apex-domein (`testweb.com` en `www.testweb.com` ) is gekoppeld aan de Adobe Commerce op de Fastly-serviceaccount voor cloudinfrastructuur. U wilt de snelservices voor de subdomeinen `service.testweb.com` en `product-updates.testweb.com` beheren vanuit een ander snelaccount.

Verzend een Adobe Commerce Support-ticket met het verzoek om de subdomeinen van de Adobe Commerce te delegeren naar de Fastly-account voor cloudinfrastructuur. Neem de service-id voor de snelaccount op in het ticket.

## DoS-beveiliging

DDOS-beveiliging is ingebouwd in de Fastly CDN-service. Zodra u de Snelle diensten voor uw plaatsen van Adobe Commerce hebt toegelaten, filters snel al Web en admin verkeer om potentiële aanvallen te ontdekken en te blokkeren.

- Voor aanvallen gericht op laag 3 of 4, filtert de Snelle dienst uit verkeer dat op haven en protocol wordt gebaseerd, die slechts HTTP of HTTPS verzoeken inspecteren. ICMP, UDP, en andere netwerk-in werking gestelde aanvallen worden gelaten vallen bij onze netwerkrand. Dit omvat bezinning en versterkingsaanvallen, die de diensten UDP zoals SSDP of NTP gebruiken. Door dit niveau van bescherming te bieden, blokkeren we effectief meerdere gemeenschappelijke aanvallen zoals Ping of Death, Smurf-aanvallen en andere op ICMP gebaseerde overstromingen.

  Beheert snel de vlakke aanvallen van TCP bij de geheim voorgeheugenlaag. Deze strategie verstrekt de noodzakelijke schaal en de context per cliënt om een de overstromingsaanval van SYN en zijn vele varianten, met inbegrip van de stapel van TCP, middelaanvallen, en de aanvallen van TLS binnen Fastly systemen te behandelen.

- Verstrekt snel ook bescherming tegen Laag 7 aanvallen. Als er prestatieproblemen optreden in uw winkel en u vermoedt dat er een Layer 7 DDoS-aanval plaatsvindt, stuurt u een Adobe Commerce Support-ticket naar u. Adobe kan douaneregels tot stand brengen en toepassen op de Snelle dienst om kwaadwillige verzoeken te inspecteren en uit te filtreren die op kopbal, lading, of een combinatie attributen worden gebaseerd die het aanvalsverkeer identificeren. Zie [ Controleren op aanvallen DDoS ] en [ hoe te kwaadwillig verkeer ] in het *Centrum van de Hulp van Adobe Commerce* blokkeren.

<!--Link definitions-->

[Caching with Fastly]: https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly

[Controleren op DDoS-aanvallen]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.html?lang=nl-NL

[Fastly CDN module for Magento 2]: https://github.com/fastly/fastly-magento2

[Kaart voor snelle ondersteuning]: https://docs.fastly.com/products/support-description-and-sla#support-requests

[Hoe te om kwaadwillig verkeer te blokkeren]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level.html?lang=nl-NL

[Werken met domeinen]: https://docs.fastly.com/en/guides/working-with-domains
