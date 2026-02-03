---
title: Overzicht van snelle services
description: Leer hoe u met de snelste services die bij Adobe Commerce worden geleverd via de cloudinfrastructuur de levering van inhoud voor uw Adobe Commerce-sites kunt optimaliseren en beveiligen.
feature: Cloud, Configuration, Iaas, Paas, Cache, Security, Services
exl-id: 429b6762-0b01-438b-a962-35376306895b
source-git-commit: 0300930577959631a2331997ebb104381136f240
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 0%

---

# Overzicht van snelle services

>[!WARNING]
>
>Als u de PCI-compatibiliteit wilt behouden voor Adobe Commerce-sites die op het Cloud-platform worden geïmplementeerd, stelt u snel in op uw Starter-hoofdvertakking, Pro Production en Pro Staging-omgevingen. Als u Adobe Commerce in een headless plaatsing gebruikt, adviseren wij hoogst dat u snel gebruikt om de reacties van GraphQL in het voorgeheugen onder te brengen. Zie [&#x200B; Caching met Fastly &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly) in de *Gids van de Ontwikkelaar van GraphQL*.

In Fastly worden de volgende services geleverd voor het optimaliseren en beveiligen van de levering van inhoud voor Adobe Commerce voor infrastructuurprojecten in de cloud. Deze services worden zonder extra kosten meegeleverd bij Adobe Commerce op cloudinfrastructuur.

- **het Netwerk van de Levering van de Inhoud (CDN)** - de op vernis-Gebaseerde dienst die uw plaatspagina&#39;s, activa, CSS, en meer in de centra van achtergrondgegevens in de cache plaatst u opstelling. Wanneer klanten toegang krijgen tot uw site en winkels, kunnen ze sneller in cache geplaatste pagina&#39;s laden. De CDN-service biedt de volgende functies:

- **beheer van het Geheime voorgeheugen** - Geheime voorgeheugen uw plaatspagina&#39;s, activa, CSS, en meer in achterste gegevenscentra die u opstelling om bandbreedtetoevoer en kosten te drukken

   - Het gebruik {de fragmenten van 0} snel douaneVCL [&#x200B; (Varnish 2.1 volgzaam) om te wijzigen hoe het in het voorgeheugen onderbrengen aan verzoeken beantwoordt](fastly-vcl-custom-snippets.md)

   - De de dienststeun van de opstelling [&#x200B; GeoIP &#x200B;](fastly-custom-cache-configuration.md#configure-geoip-handling)

   - [Niet-gecodeerde aanvragen forceren naar TLS](fastly-custom-cache-configuration.md#force-tls)

   - [&#x200B; pas Snelle onderbreking &#x200B;](fastly-custom-cache-configuration.md#extend-fastly-timeout) montages aan om 503 reacties op bulkbewerkingsverzoeken te verhinderen

   - Creeer [&#x200B; pagina&#39;s van de de foutenreactie van de douanefout &#x200B;](fastly-custom-response.md)

- **Veiligheid** - nadat u de Snelle diensten voor de plaatsen van Adobe Commerce toelaat, zijn de extra veiligheidseigenschappen beschikbaar om uw plaatsen en netwerk te beschermen:

   - [&#x200B; (WAF) - de Beheerde dienst van de de firewalltoepassing van het Web van 0&rbrace; Firewall van de Toepassing van het Web die PCI-Volgzame bescherming verleent om kwaadwillig verkeer te blokkeren alvorens het uw productieAdobe Commerce op de plaatsen van de wolkeninfrastructuur en netwerk kan beschadigen. &#x200B;](fastly-waf-service.md) De WAF-service is alleen beschikbaar in Pro- en Starter Production-omgevingen.

   - [&#x200B; Verdeelde Ontkenning van de bescherming van de Dienst (DDoS) &#x200B;](#ddos-protection) - ingebouwde bescherming DDoS tegen gemeenschappelijke laag 3 en 4 aanvallen zoals Ping van Dood, de aanvallen van Smurf, en andere op ICMP-Gebaseerde overstromingsaanvallen. De ingebouwde bescherming omvat geen bescherming tegen Laag 7 aanvallen. Zie [&#x200B; bescherming DDoS &#x200B;](#ddos-protection).

   - [&#x200B; SSL/TLS certificaten &#x200B;](fastly-configuration.md#provision-ssltls-certificates) - de sneldienst vereist een SSL/TLS certificaat om veilig verkeer over HTTPS te dienen.

     Adobe Commerce biedt een door een domein gevalideerd SSL/TLS-certificaat voor elke staging- en productieomgeving. Adobe Commerce voltooit domeinvalidatie en certificaatprovisioning tijdens het installatieproces van Snel.

- **Oorsprong het camoufleren** — De eigenschap van de Veiligheid die alle verkeersstromen door Vast verzekert en directe toegang tot oorsprongservers blokkeert. Zie de [&#x200B; Bron het camoufleren &#x200B;](#origin-cloaking) hieronder sectie.

- **[optimalisering van het Beeld](fastly-image-optimization.md)** - ontlaadt beeldverwerking en het resizing lading aan de Snelle dienst zodat de servers orden en omzettingen efficiënter kunnen verwerken.

- **[snel CDN en de logboeken van WAF](../monitor/new-relic-service.md#new-relic-log-management)** - voor Adobe Commerce op de Pro projecten van de wolkeninfrastructuur, kunt u de dienst van Logs van New Relic gebruiken om snel CDN en het logboekgegevens van WAF te herzien en te analyseren.

## Oorspronkelijke opmaak {#origin-cloaking}

Oorspronkelijke camouflage is een beveiligingsfunctie die voorkomt dat niet-snel verkeer de Adobe Commerce bereikt op basis van de cloudinfrastructuur. Alle verzoeken moeten deze gedwongen weg volgen:

**snel > de toepassingsinstanties van de Balancer van de Lading > van Adobe Commerce**

Het gebruiken van deze weg zorgt ervoor dat al verkeer door de Fastly Firewall van de Toepassing van het Web (WAF) en door interne WAF op het taakverdelingsmechanisme wordt geïnspecteerd. Camoufleren van de oorsprong beschermt uw plaatsen tegen direct-toegangspogingen en vermindert het risico van aanvallen DDoS.

### Inschakelingsstatus

Oorsprongscamouflage is sinds 2021 volledig ingeschakeld voor alle Adobe Commerce-infrastructuurprojecten in de cloud.\
De projecten die na 2021 worden geleverd omvatten deze configuratie door gebrek.\
**geen actie wordt vereist** om oorsprong het camoufleren toe te laten.

#### Welke blokken oorsprong camoufleren

Oorsprong blokkeert directe toegang tot de oorspronkelijke infrastructuur, zoals:

```
mywebsite.com.c.abcdefghijkl.ent.magento.cloud
mcstaging2.mywebsite.com.c.abcdefghijkl.dev.ent.magento.cloud
mcstagingX.mywebsite.com.c.abcdefghijkl.X.dev.ent.magento.cloud
```

De verzoeken door uw openbaar domein blijven normaal werken, met inbegrip van REST API verkeer. Voorbeelden:

```
mywebsite.com/rest/default/V1/integration/admin/token
mywebsite.com/rest/default/V1/orders/
mywebsite.com/rest/default/V1/products/
mywebsite.com/rest/default/V1/inventory/source-items
```

#### Gevolgen voor het gedrag van de dienst

- **Uitgaande IP adressen veranderen niet.**
- **REST APIs wordt niet beïnvloed.In** worden snel geen API-aanroepen in het cachegeheugen opgeslagen.
- **Inzet en onderbreking worden niet beïnvloed.**
- Als een project veelvoudige het opvoeren milieu&#39;s heeft, **oorsprong het camoufleren is op elk van hen** van toepassing.

## Fastly CDN module for Magento 2

De snelle diensten voor Adobe Commerce op wolkeninfrastructuur gebruiken de [ snelste CDN module voor Magento 2 ] die in de volgende milieu&#39;s wordt geïnstalleerd: Pro Staging en Productie, de Productie van de Aanzet (`master` tak).

Bij de initiële provisioning of upgrade van uw Adobe Commerce-project installeert Adobe de nieuwste versie van de Fastly CDN-module in uw Staging- en Productomgevingen. Als u de updates van de module Fastly loslaat, ontvangt u meldingen in Admin voor uw omgevingen. Adobe raadt u aan uw omgevingen bij te werken om de nieuwste versie te gebruiken. Zie [&#x200B; Snelle Verbetering &#x200B;](fastly-configuration.md#upgrade-the-fastly-module).

## Snelle de dienstrekening en geloofsbrieven

Adobe Commerce on cloud Infrastructure projects krijgt geen toegewezen Fastly account. De snelservice wordt beheerd in een gecentraliseerde account die bij Adobe is geregistreerd, en het beheerdashboard is alleen toegankelijk voor het ondersteuningsteam voor cloud.

In plaats daarvan heeft elke omgeving voor Staging en Productie unieke Fastly-referenties (API-token en service-id) voor het configureren en beheren van Fastly-services van Commerce Admin. De snelste API is beschikbaar voor het uitvoeren van geavanceerd beheer van de sneldienst, die de geloofsbrieven zal vereisen om die verzoeken voor te leggen.

Tijdens projectlevering, voegt Adobe uw project aan de Fastly de dienstrekening voor Adobe Commerce op wolkeninfrastructuur toe en voegt de Fastly geloofsbrieven aan de configuratie voor de het Opvoeren en milieu&#39;s van de Productie toe. Zie [&#x200B; krijgen de Snelle geloofsbrieven &#x200B;](fastly-configuration.md#get-fastly-credentials).

### Fastly API-token wijzigen

Verzend een kaartje van de Steun van Adobe Commerce om een nieuwe Fastly API symbolische referentie [&#x200B; uit te geven als het bevestiging/is verlopen &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/error-when-validating-fastly-credentials) ontbreekt, of als u gelooft dat het is gecompromitteerd.

Wanneer u het nieuwe token ontvangt, werkt u de omgeving voor Staging of Productie bij om het nieuwe token te gebruiken.

**om de Fastly API symbolische referentie** te veranderen:

1. [&#x200B; legt een kaartje van de Steun van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor het vragen van nieuwe Fastly API geloofsbrieven.

   Neem uw Adobe Commerce op in de projectid van de cloud-infrastructuur en de omgevingen die een nieuwe referentie vereisen.

1. Nadat u het nieuwe API teken ontvangt, werk de symbolische waarde van API in de [&#x200B; Snelle geloofsconfiguratie &#x200B;](fastly-configuration.md#test-the-fastly-credentials) in Admin of van de [[!DNL Cloud Console]  milieuvariabelen &#x200B;](../project/overview.md#configure-environment) bij.

1. [&#x200B; Test de nieuwe referentie &#x200B;](fastly-configuration.md#test-the-fastly-credentials).

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

Nadat de delegatie is voltooid, kunnen uw projectsubdomeinen aan de Fastly de dienstrekening voor Adobe Commerce op wolkeninfrastructuur worden toegevoegd. Zie [&#x200B; krijgen de Snelle geloofsbrieven &#x200B;](fastly-configuration.md#get-fastly-credentials).

*Scenario 2:*

Het apex-domein (`testweb.com` en `www.testweb.com` ) is gekoppeld aan de Adobe Commerce op de Fastly-serviceaccount voor cloudinfrastructuur. U wilt de snelservices voor de subdomeinen `service.testweb.com` en `product-updates.testweb.com` beheren vanuit een ander snelaccount.

Verzend een Adobe Commerce Support-ticket met het verzoek om de subdomeinen van de Adobe Commerce te delegeren naar de Fastly-account voor cloudinfrastructuur. Neem de service-id voor de snelaccount op in het ticket.

## DoS-beveiliging

DDOS-beveiliging is ingebouwd in de Fastly CDN-service. Zodra u de Snelle diensten voor uw plaatsen van Adobe Commerce hebt toegelaten, filters snel al Web en admin verkeer om potentiële aanvallen te ontdekken en te blokkeren.

- Voor aanvallen gericht op laag 3 of 4, filtert de Snelle dienst uit verkeer dat op haven en protocol wordt gebaseerd, die slechts HTTP of HTTPS verzoeken inspecteren. ICMP, UDP, en andere netwerk-in werking gestelde aanvallen worden gelaten vallen bij onze netwerkrand. Dit omvat bezinning en versterkingsaanvallen, die de diensten UDP zoals SSDP of NTP gebruiken. Door dit niveau van bescherming te bieden, blokkeren we effectief meerdere gemeenschappelijke aanvallen zoals Ping of Death, Smurf-aanvallen en andere op ICMP gebaseerde overstromingen.

  Beheert snel de vlakke aanvallen van TCP bij de geheim voorgeheugenlaag. Deze strategie verstrekt de noodzakelijke schaal en de context per cliënt om een de overstromingsaanval van SYN en zijn vele varianten, met inbegrip van de stapel van TCP, middelaanvallen, en de aanvallen van TLS binnen Fastly systemen te behandelen.

>[!NOTE]
>
>De bescherming tegen Laag 7 aanvallen wordt niet behandeld door de Fastly dienst CDN die met Adobe Commerce wordt geïntegreerd. Voor uiteinden bij het beschermen tegen Laag 7 aanvallen, zie [&#x200B; het Controleren op DoS Aanvallen &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli) en [&#x200B; hoe te kwaadwillige aanvallen &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level) in de *Kennisbank van Adobe Commerce* blokkeren.

<!--Link definitions-->

[Caching with Fastly]: https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly

[Checking for DDoS attacks]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.html

[Fastly CDN module for Magento 2]: https://github.com/fastly/fastly-magento2

[Kaart voor snelle ondersteuning]: https://docs.fastly.com/products/support-description-and-sla#support-requests

[How to block malicious traffic]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level.html

[Werken met domeinen]: https://docs.fastly.com/en/guides/working-with-domains
