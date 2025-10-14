---
title: Cloudarchitectuur voor Commerce
description: Leer hoe Starter en Pro-projectarchitecturen contrasteren voor Commerce op Cloud-infrastructuur.
feature: Cloud, Iaas, Paas
topic: Architecture
recommendations: noDisplay
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Cloudarchitectuur voor Commerce

Adobe Commerce on cloud Infrastructure heeft een Starter- en een Pro-plan. Elk plan heeft een unieke architectuur om uw ontwikkeling en plaatsingsproces van Adobe Commerce te drijven. Zowel het plan van de Aanzet als de Pro planarchitectuur stellen gegevensbestanden, Webservers, en caching servers over veelvoudige milieu&#39;s voor het testen van begin tot eind op terwijl het steunen van ononderbroken integratie.

Ter vergelijking, omvat elk plan de volgende infrastructuureigenschappen en gesteunde producten.

|          | Starter | Pro |
| -------- | --------------------| ------------------ |
| Kernfuncties | <ul><li>[&#x200B; Alle eigenschappen van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html?lang=nl-NL)</li><li>PayPal on boarding Tool</li><li>[&#x200B; Commerce die &#x200B;](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209) meldt</li></ul> | <ul><li>[&#x200B; Alle eigenschappen van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/release/features.html?lang=nl-NL)</li><li>PayPal on boarding Tool</li><li>[&#x200B; Commerce die &#x200B;](https://business.adobe.com/products/magento/business-intelligence.html?_ga=2.85288604.442698376.1665067470-1322106587.1655147209) meldt</li><li>[&#x200B; B2B module &#x200B;](https://business.adobe.com/products/magento/b2b-ecommerce.html?_ga=2.105948422.442698376.1665067470-1322106587.1655147209)</li></ul> |
| Infrastructuur en implementatie | <ul><li>Doorlopende tools voor cloudintegratie met onbeperkte gebruikers</li><li>Het netwerk van de Levering van de Inhoud (CDN), de Optimalisering van het Beeld (IO), en toegevoegde veiligheid met genereuze bandbreedteemissierechten. De dienst van de Firewall van de Toepassing van het Web (WAF) is beschikbaar slechts op productiemilieu&#39;s.</li><li>[&#x200B; New Relic &#x200B;](../monitor/new-relic-service.md) APM (de Controle van Prestaties) op 3 takken: `master` en 2 van uw keus <br> Platform als de productie, het opvoeren, en ontwikkelomgevingen (4 totaal actieve milieu&#39;s) die voor Adobe Commerce worden geoptimaliseerd</li><li>Egress-filtering (uitgaande firewall)</li></ul> | <ul><li>Doorlopende tools voor cloudintegratie met onbeperkte gebruikers</li><li>Het netwerk van de Levering van de Inhoud (CDN), de Optimalisering van het Beeld (IO), en toegevoegde veiligheid met genereuze bandbreedteemissierechten. De dienst van de Firewall van de Toepassing van het Web (WAF) is beschikbaar slechts op productiemilieu&#39;s.</li><li>[&#x200B; New Relic &#x200B;](../monitor/new-relic-service.md) Infrastructuur op Productie + APM (de Controle van Prestaties) op het opvoeren en productie. Het [&#x200B; Beheerde alarmeringsbeleid &#x200B;](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts) voor het beleid van Adobe Commerce voert controle beste praktijken uit om u over toepassing en infrastructuurkwesties proactively mee te delen die plaatsprestaties beïnvloeden.</li><li>Platform als de dienst (PaaS) gebaseerde [&#x200B; ontwikkelings &#x200B;](pro-architecture.md#integration-environment) milieu&#39;s van de Integratie (2 totaal actieve milieu&#39;s) die voor Adobe Commerce worden geoptimaliseerd</li><li>Infrastructuur als dienst (IaaS) - specifieke virtuele infrastructuur voor het Opvoeren en van de Productie milieu&#39;s</li></ul> |
| Infrastructuur voor hoge beschikbaarheid | | [&#x200B; Hoge beschikbaarheidsarchitectuur &#x200B;](pro-architecture.md#redundant-hardware) met een drie-serveropstelling in de onderliggende Infrastructuur als dienst (IaaS) om de betrouwbaarheid en de beschikbaarheid van ondernemingskwaliteit te verstrekken |
| Speciale hardware | | Geïsoleerde en toegewijde hardware in de onderliggende infrastructuur als een dienst (IaaS) om nog hogere niveaus van betrouwbaarheid en beschikbaarheid te verstrekken |
| 24x7 e-mailondersteuning | 24x7 controle en e-mailondersteuning voor de kerntoepassing en de cloudinfrastructuur | 24x7 controle en e-mailondersteuning voor de kerntoepassing en de cloudinfrastructuur |
| Een toegewijde Technische Adviseur van de Klant (CTA) | | Specifiek technisch accountbeheer voor de eerste startperiode, vanaf uw abonnement tot uw eerste site wordt gestart |
| Invoegtoepassingen\* | <ul><li>[&#x200B; B2B module &#x200B;](https://business.adobe.com/products/magento/b2b-ecommerce.html)</li></ul> |

\* _Beschikbaar voor een extra tarief_

## Startersprojecten

De [&#x200B; architectuur van het Plan van de Aanzet &#x200B;](starter-architecture.md) heeft vier milieu&#39;s:

- **Integratie** - het integratiemilieu verstrekt twee testable milieu&#39;s. Elke omgeving bevat een actieve Git-vertakking, database, webserver, caching, sommige services, omgevingsvariabelen en configuraties.

- **het Staging** - aangezien de code en de uitbreidingen uw tests overgaan, kunt u uw `integration` tak aan het het Staging milieu samenvoegen, dat uw pre-productie testend milieu wordt. Dit omvat de `staging` actieve vertakking, database, webserver, caching, services van derden, omgevingsvariabelen, configuraties en services, zoals Fastly en New Relic.

- **Productie** - wanneer de code klaar en getest is, voegt alle code aan `master` voor plaatsing aan de productie levende plaats samen. Deze omgeving omvat uw actieve `master` vertakking, database, webserver, caching, services van derden, omgevingsvariabelen en configuraties.

- **Inactief** - u hebt een onbeperkt aantal inactieve takken.

## Pro-projecten

De [&#x200B; Pro planarchitectuur &#x200B;](pro-architecture.md) heeft globaal `master` met drie milieu&#39;s:

- **Integratie** - het integratiemilieu verstrekt een testable milieu dat een gegevensbestand, Webserver, caching, sommige diensten, milieuvariabelen, en configuraties omvat. U kunt uw code ontwikkelen, opstellen en testen alvorens aan het Opvoeren milieu samen te voegen.

   - _Inactief_ - u kunt een onbeperkt aantal inactieve takken hebben die op het `integration` milieu worden gebaseerd, maar slechts één actieve tak (niet met inbegrip van `integration`).

- **het Staging** - het het opvoeren milieu is voor pre-productie het testen en omvat een gegevensbestand, Webserver, caching, derdediensten, milieuvariabelen, configuraties, en de diensten, zoals Fastly.

- **Productie** - het productiemilieu omvat een drie-knoop, high-availability architectuur voor uw gegevens, de diensten, caching, en opslag. De productie is uw levende, openbare opslagmilieu met milieuvariabelen, configuraties, en derdediensten.

## Ondersteunde software en services

Adobe Commerce op cloudinfrastructuur gebruikt:

- Besturingssysteem: Debian GNU/Linux
- Webserver: Nginx
- Database: MySQL (MariaDB)
- Content Delivery Network (CDN): Fastly CDN

U kunt de volgende services configureren:

- [PHP](../application/php-settings.md)
- [MySQL](../services/mysql.md)
- [Redis](../services/redis.md)
- [RabbitMQ](../services/rabbitmq.md)
- [Elasticsearch](../services/elasticsearch.md)
- [OpenSearch](../services/opensearch.md)

{{elasticsearch-support}}

>[!NOTE]
>
>Zie {de vereisten van het 0} Systeem [&#128279;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html?lang=nl-NL) in de _gids van de Installatie_ voor geadviseerde versies.

De snelste CDN-module wordt gebruikt voor CDN- en caching-services op staging- en productieomgevingen. Zie [&#x200B; vormen de Snelle diensten &#x200B;](../cdn/fastly.md).

Raadpleeg de volgende Adobe Commerce over configuratiebestanden voor de cloud-infrastructuur voor informatie over het configureren van de softwareversies die u in uw implementatie wilt gebruiken:

- [Toepassingsconfiguratie (.magento.app.yaml)](../application/configure-app-yaml.md)
- [Omgevingsconfiguratie (.magento.env.yaml)](../environment/configure-env-yaml.md)
- [Configuratie van routes (routes.yaml)](../routes/routes-yaml.md)
- [Configuratie van services (services.yaml)](../services/services-yaml.md)
