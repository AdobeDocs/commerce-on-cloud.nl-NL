---
title: Starter-architectuur
description: Meer informatie over de omgevingen die door de Starter-architectuur worden ondersteund.
feature: Cloud, Paas
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Starter-architectuur

Uw Adobe Commerce op de architectuur van de Aanzet van de wolkeninfrastructuur steunt tot **vier** milieu&#39;s, met inbegrip van a `master` milieu dat de aanvankelijke projectcode, het het Opvoeren milieu, en tot twee integratiemilieu&#39;s bevat.

Alle milieu&#39;s zijn in (Platform als dienst) containers PaaS. Deze containers worden opgesteld binnen hoogst beperkte containers op een net van servers. Deze milieu&#39;s zijn read-only, goedkeurend opgestelde codeveranderingen van takken die van uw lokale werkruimte worden geduwd. Elke omgeving biedt een database en webserver.

U kunt elke gewenste ontwikkelings- en vertakkingsmethode gebruiken. Wanneer u initiële toegang tot uw project krijgt, maakt u een `staging` -omgeving vanuit de `master` -omgeving. Maak vervolgens de `integration` -omgeving door vertakking vanuit `staging` .

## Startomgevingarchitectuur

Het volgende diagram toont de hiërarchische verhoudingen van de milieu&#39;s van de Aanzet.

![&#x200B; High-level mening van het project van de Aanzet &#x200B;](../../assets/starter/architecture.png)

## Productieomgeving

De productieomgeving biedt de broncode voor de implementatie van Adobe Commerce in de Cloud-infrastructuur waarop uw publiek gerichte Single- en Multisite Storefronts worden uitgevoerd. De productieomgeving gebruikt code van de `master` tak om de Webserver, het gegevensbestand, de gevormde diensten, en uw toepassingscode te vormen en toe te laten.

Omdat de `production` -omgeving alleen-lezen is, gebruikt u de `integration` -omgeving om codewijzigingen aan te brengen, implementeert u deze over de architectuur van de `integration` naar `staging` -omgeving en ten slotte naar de `production` -omgeving. Zie [&#x200B; uw opslag &#x200B;](../deploy/staging-production.md) opstellen en [&#x200B; lancering van de Plaats &#x200B;](../launch/overview.md).

Adobe raadt aan om de `staging` -vertakking volledig te testen voordat u naar de `master` -vertakking gaat. Deze wordt in de `production` -omgeving geïmplementeerd.

## Stationele omgeving

Adobe raadt u aan een vertakking met de naam `staging` te maken van `master` . De `staging` -vertakking implementeert code in de testomgeving voor een pre-productieomgeving voor het testen van code, modules en extensies, betaalgateways, verzending, productgegevens en nog veel meer. Dit milieu verstrekt de configuratie voor alle diensten om het productiemilieu met inbegrip van Fastly, New Relic APM, en onderzoek aan te passen.

De extra secties in deze gids verstrekken instructies voor definitieve codeplaatsingen en het testen van productie-vlakke interactie in een veilige het Opvoeren milieu. Voor de beste prestaties en eigenschapstests, repliceer uw gegevensbestand in het Opvoeren milieu.

>[!WARNING]
>
>De Adobe beveelt het testen van elke handels en klanteninteractie in het Opvoeren milieu aan alvorens aan het productiemilieu op te stellen. Zie [&#x200B; uw opslag &#x200B;](../deploy/staging-production.md) opstellen en [&#x200B; plaatsing van de Test &#x200B;](../test/staging-and-production.md).

## Integratieomgeving

Ontwikkelaars gebruiken de `integration` -omgeving voor het ontwikkelen, implementeren en testen van:

- Adobe Commerce-toepassingscode

- Aangepaste code

- Extensies

- Services

**Aanbevolen gebruiksgevallen:**

Integratieomgevingen zijn ontworpen voor beperkte tests en ontwikkeling. U kunt bijvoorbeeld de integratieomgeving gebruiken om de volgende taken uit te voeren:

- Ervoor zorgen dat wijzigingen in processen voor continue integratie (CI) compatibel zijn met de cloud

- Kritieke workflows testen op sleutelpagina&#39;s zoals Home, Categorie, pagina met productdetails (PDP), Afhandeling en Beheer

Voor de beste prestaties in de integratieomgeving volgt u de volgende aanbevolen procedures:

- Beperk de catalogusgrootte - Ter referentie bevat de voorbeeldgegevens ongeveer 2.048 producten. Verklein uw catalogus tot ongeveer 4.000-5.000 producten.
Om het aantal producten in de catalogus te controleren, stel de volgende vraag MySQL in werking:

  ```sql
  select distinct count(entity_id) from catalog_product_entity;
  ```

- Verminder het aantal klantengroepen - Het hebben van teveel klantengroepen kan de indexerende prestaties en algemene prestaties beïnvloeden.

- Gebruik beperken tot een of twee gelijktijdige gebruikers

- Snijtaken uitschakelen en indien nodig handmatig uitvoeren

U kunt tot **twee** actieve milieu&#39;s van de Integratie hebben. U creeert een milieu van de Integratie door een tak van de `staging` tak te creëren. Wanneer u een milieu van de Integratie creeert, past de milieunaam de taknaam aan. Een integratieomgeving bevat een webserver en een database. Het omvat niet alle diensten, bijvoorbeeld Fastly CDN en New Relic zijn niet beschikbaar.

U kunt een onbeperkt aantal inactieve vertakkingen voor codeopslag hebben. Als u een niet-actieve vertakking wilt openen, weergeven en testen, moet u deze activeren

{{enhanced-integration-envs}}

## Productie- en staging-technologiestack

De productie en het opvoeren milieu&#39;s omvatten de volgende technologieën. U kunt deze technologieën aanpassen en configureren via het [`.magento.app.yaml`](../application/configure-app-yaml.md) -bestand.

- Gemakkelijk voor HTTP caching en CDN
- Nginx-webserver die spreekt met PHP-FPM, één instantie met meerdere workers
- Redis-server
- Elasticsearch voor cataloguszoekactie naar Adobe Commerce 2.2 tot 2.4.3-p2
- OpenSearch naar cataloguszoekopdracht voor Adobe Commerce 2.3.7-p3, 2.4.3-p2 en 2.4.4 en hoger
- Egress-filtering (uitgaande firewall)

### Services

Adobe Commerce on cloud Infrastructure biedt momenteel ondersteuning voor de volgende services: PHP, MySQL (MariaDB), Elasticsearch (Adobe Commerce 2.2 tot 2.4.3-p2), OpenSearch (2.3.7-p3, 2.4.3-p2, 2.4.4 en hoger), Redis en [!DNL RabbitMQ].

Elke dienst loopt in een afzonderlijke, veilige container. Containers worden samen in het project beheerd. Sommige services zijn standaard, zoals:

- De router van HTTP (behandeling inkomende verzoeken, maar ook caching en richt opnieuw)

- PHP-toepassingsserver

- Git

- Beveiligde shell (SSH)

### Softwareversies

Adobe Commerce op cloudinfrastructuur gebruikt het Debian GNU/Linux-besturingssysteem en de NGINX-webserver. U kunt deze software niet upgraden, maar u kunt versies voor het volgende configureren:

- [PHP](../application/php-settings.md)

- [MySQL](../services/mysql.md)

- [Redis](../services/redis.md)

- [RabbitMQ](../services/rabbitmq.md)

- [Elasticsearch](../services/elasticsearch.md)

- [OpenSearch](../services/opensearch.md)

In de het opvoeren en productiemilieu&#39;s, gebruikt u snel voor CDN en caching. De recentste versie van de Snelle uitbreiding CDN installeert tijdens de aanvankelijke levering van uw project. U kunt de extensie upgraden voor de nieuwste opgeloste problemen en verbeteringen. Zie [&#x200B; Snelle CDN module voor Magento 2 &#x200B;](https://github.com/fastly/fastly-magento2). Ook, hebt u toegang tot [&#x200B; New Relic &#x200B;](../monitor/account-management.md) voor prestaties controle.

Gebruik de volgende dossiers om de softwareversies te vormen die u in uw implementatie wilt gebruiken.

- [`.magento.app.yaml`](../application/configure-app-yaml.md)

- [&quot;routes.yaml&quot;](../routes/routes-yaml.md)

- [&quot;services.yaml&quot;](../services/services-yaml.md)

### Back-up en noodherstel

U kunt een back-up van uw database en bestandssysteem maken met behulp van [!DNL Cloud Console] of de CLI. Zie [&#x200B; Reservekopiebeheer &#x200B;](../storage/snapshots.md).

## Voorbereiden op ontwikkeling

De volgende werkschema vat het proces samen om uw code te vertakken, te ontwikkelen, en uw opslag op te stellen:

1. De lokale omgeving instellen

1. De vertakking `master` klonen naar uw lokale omgeving

1. Een `staging` vertakking maken vanuit `master`

1. Vertakkingen maken voor ontwikkeling vanuit `staging`

1. Druk code aan Git die bouwt en aan een milieu voor het testen opstelt

Zie de volgende secties voor gedetailleerde instructies en looptraject om uw opslag te ontwikkelen, te testen en op te stellen:

- [Starter-workflow voor ontwikkelen en implementeren](starter-develop-deploy-workflow.md)

- [&#x200B; de ontwikkeling van Docker &#x200B;](../dev-tools/cloud-docker.md) (lokale ontwikkelomgeving die door Docker van de Wolk voor Commerce wordt toegelaten)

- [Vertakkingen beheren](../project/console-branches.md)

- [Je winkel implementeren](../deploy/staging-production.md)

- [Site starten](../launch/overview.md)
