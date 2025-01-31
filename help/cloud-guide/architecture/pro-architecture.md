---
title: Pro-architectuur
description: Leer meer over de omgevingen die worden ondersteund door de Pro-architectuur.
feature: Cloud, Auto Scaling, Iaas, Paas, Storage
topic: Architecture
source-git-commit: 0d9d3d64cd0ad4792824992af354653f61e4388d
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 0%

---

# Pro-architectuur

Uw Adobe Commerce on cloud Infrastructure Pro-architectuur ondersteunt meerdere omgevingen die u kunt gebruiken om uw winkel te ontwikkelen, te testen en te starten.

- **Meester** - verstrekt a `master` tak die aan Platform als de dienstcontainers (PaaS) wordt opgesteld.
- **Integratie** - verstrekt één enkele `integration` tak voor ontwikkeling, hoewel u één extra tak kunt tot stand brengen. Dit staat voor maximaal twee _actieve_ takken toe die aan Platform als de dienstcontainers (PaaS) worden opgesteld.
- **het Opvoeren** - verstrekt één enkele `staging` tak die aan specifieke Infrastructuur als de dienstcontainers (IaaS) wordt opgesteld.
- **Productie** - verstrekt één enkele `production` tak die aan specifieke Infrastructuur als de dienstcontainers (IaaS) wordt opgesteld.

De volgende tabel geeft een overzicht van de verschillen tussen omgevingen:

|                                        | INTEGRATIE | STAGING | PRODUCTIE |
| -------------------------------------- | ----------- | ----------------- | -------------------- |
| Ondersteunt het instellingenbeheer in de [!DNL Cloud Console] | Ja | Beperkt | Beperkt |
| Ondersteunt meerdere takken | Ja | Nee (alleen Staging) | Nee (alleen productie) |
| Gebruikt YAML-bestanden voor configuratie | Ja | Nee | Nee |
| Wordt uitgevoerd op toegewezen IaaS-hardware | Nee | Ja | Ja |
| Inclusief snel CDN | Nee | Ja | Ja |
| Inclusief New Relic-service | Nee | APM | APM + NRI |
| Automatische back-ups | Nee | Ja | Ja |

>[!NOTE]
>
>Adobe biedt het hulpprogramma Cloud Docker voor Commerce voor het implementeren naar een lokale Cloud Docker-omgeving zodat u Adobe Commerce-projecten kunt ontwikkelen en testen. Zie {de ontwikkeling van 0} Docker ](../dev-tools/cloud-docker.md).[

## Omgevingsarchitectuur

Uw project is één Git-opslagplaats met drie belangrijke omgevingsvertakkingen: `integration`, `staging` en `production` . Het volgende diagram toont de hiërarchische verhouding van Pro milieu&#39;s:

![ mening op hoog niveau van Pro milieuarchitectuur ](../../assets/pro-branch-architecture.png)

### Hoofdomgeving

Bij Pro-projecten biedt de `master` -vertakking een actieve PaaS-omgeving met uw productieomgeving. Duw altijd een exemplaar van de productiecode aan het `master` milieu zodat u het productiemilieu kunt zuiveren zonder de diensten te onderbreken.

**beveats:**

- Creëer **** geen tak die op de `master` tak wordt gebaseerd. Gebruik de integratieomgeving om actieve vertakkingen voor ontwikkeling te maken.

- Gebruik de `master` -omgeving niet voor ontwikkelings-, UAT- of prestatietests

### Integratieomgeving

De integratieomgeving wordt uitgevoerd in een Linux-container (LXC) op een raster met servers die PaaS wordt genoemd. Elke omgeving bevat een webserver en database waarmee u uw site kunt testen. Zie [ Regionale IP Adressen ](../project/regional-ip-addresses.md) voor een lijst van AWS en Azure IP adressen.

**Aanbevolen gebruiksgevallen:**

De milieu&#39;s van de integratie worden ontworpen voor beperkte test en ontwikkeling alvorens veranderingen in het opvoeren en productiemilieu&#39;s te bewegen. U kunt bijvoorbeeld de integratieomgeving gebruiken om de volgende taken uit te voeren:

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

**beveats:**

- Snelle CDN- en New Relic-services zijn niet toegankelijk in een integratieomgeving

- De architectuur van het integratiemilieu past niet de Staging en architectuur van de Productie aan

- Gebruik de `integration` -omgeving niet voor het testen van de ontwikkeling, het testen van de prestaties of het testen van de gebruikersacceptatie (UAT)

- Gebruik de `integration` -omgeving niet om B2B voor Adobe Commerce-functionaliteit te testen

- U kunt de database niet terugzetten in de integratieomgeving vanuit de databaseproductie of -staging

{{enhanced-integration-envs}}

### Stationele omgeving

De testomgeving biedt een omgeving voor bijna-productie om uw site te testen. Deze omgeving, die wordt gehost op toegewezen IaaS-hardware, omvat alle services, zoals Fastly CDN, New Relic APM en zoeken.

**Aanbevolen gebruiksgevallen:**

De omgeving komt overeen met de productiearchitectuur en is ontworpen voor UAT, inhoudstaging en definitieve revisie voordat de functies naar de `production` -omgeving worden verplaatst. U kunt bijvoorbeeld de `staging` -omgeving gebruiken om de volgende taken uit te voeren:

- Regressietest aan de hand van productiegegevens

- Prestaties testen met snelle caching ingeschakeld

- Nieuwe builds testen in plaats van patching in Production

- UAT testen voor nieuwe builds

- Test B2B voor Adobe Commerce

- De configuratie van de uitsnede aanpassen en de taken voor uitsnijden testen

Zie [ het werkschema van de Plaatsing ](pro-develop-deploy-workflow.md#deployment-workflow) en [ plaatsing van de Test ](../test/staging-and-production.md).

**beveats:**

- Na het lanceren van de productielocatie, gebruik het het opvoeren milieu hoofdzakelijk om flarden voor productie-kritieke insectenmoeilijke situaties te testen.

- U kunt geen vertakking maken van de `staging` -vertakking. In plaats daarvan verandert de code van de `integration` -vertakking in de `staging` -vertakking.

{{second-staging}}

### Productieomgeving

De productieomgeving voert uw openbare, naar wens enkelvoudige en multisite winkels uit. Deze omgeving wordt uitgevoerd op toegewezen IaaS-hardware met redundante knooppunten met hoge beschikbaarheid voor continue toegang en failover-beveiliging voor uw klanten. Het productiemilieu omvat alle diensten in het opvoeren milieu, plus de [ dienst van de Infrastructuur van New Relic (NRI) ](../monitor/new-relic-service.md#new-relic-infrastructure), die automatisch met de toepassingsgegevens en prestatiesanalyses verbindt om dynamische servercontrole te verstrekken.

**Beveat:**

U kunt geen vertakking maken van de `production` -vertakking. In plaats daarvan verandert de code van de `staging` -vertakking in de `production` -vertakking.

### Stapel productietechnologie

De productieomgeving heeft drie virtuele machines (VM&#39;s) achter een Elastic Load Balancer die wordt beheerd door een HAProxy per VM. Elke VM bevat de volgende technologieën:

- **snel CDN** - HTTP caching en CDN

- **NGINX** - Webserver die PHP-FPM gebruikt, één instantie met veelvoudige arbeiders

- **GlusterFS** - dossierserver voor het beheren van alle statische dossierplaatsingen en synchronisatie met vier foldersteunen:

   - `var`
   - `pub/media`
   - `pub/static`
   - `app/etc`

- **herstelt** - één server per VM met slechts één actief en andere twee als replica&#39;s

- **Elasticsearch** - onderzoek naar Adobe Commerce op wolkeninfrastructuur 2.2 aan 2.4.3-p2

- **OpenSearch** - onderzoek naar Adobe Commerce op wolkeninfrastructuur 2.3.7-p3, 2.4.3-p2, 2.4.4 en later

- **Galera** - gegevensbestandcluster met één gegevensbestand MariaDB MySQL per knoop met auto-verhogen het plaatsen van drie voor unieke identiteitskaarts over elk gegevensbestand

De volgende afbeelding toont de technologieën die in de productieomgeving worden gebruikt:

![ de technologiestapel van de Productie ](../../assets/az-stack-diagram.png)

## Redundante hardware

Eerder dan het in werking stellen van een traditioneel, actief-passief `master` of een primair-secundaire opstelling, stelt Adobe Commerce op wolkeninfrastructuur a _overtollige architectuur_ in werking waar alle drie instanties lezen en schrijven goedkeuren. Deze architectuur biedt geen onderbreking wanneer het schrapen aan en verstrekt gewaarborgde transactionele integriteit.

Vanwege de unieke, redundante hardware kan Adobe drie gatewayservers leveren. De meeste externe diensten laten u toe om veelvoudige IP adressen aan een lijst van gewenste personen toe te voegen, zodat heeft meer dan één vast IP adres geen probleem is. De drie gateways wijzen aan de drie servers in uw cluster van het productiemilieu toe en behouden statische IP adressen. Het is volledig overtollig en hoogst beschikbaar op elk niveau:

- DNS
- Content Delivery Network (CDN)
- Elastic Load balancer (ELB)
- Drieservercluster bestaande uit alle Adobe Commerce-services, inclusief de database en webserver

## Back-up en noodherstel

Adobe Commerce op cloudinfrastructuur maakt gebruik van een architectuur met hoge beschikbaarheid die elk Pro-project repliceert op drie aparte AWS- of Azure-beschikbaarheidszones, elke zone met een afzonderlijk datacenter. Naast deze overtolligheid, ontvangen de Pro het opvoeren en productiemilieu&#39;s regelmatige, levende steunen die voor gebruik in gevallen van _catastrofale mislukking_ worden ontworpen.

**Automatische steunen** omvatten blijvende gegevens van alle lopende diensten, zoals het gegevensbestand MySQL en dossiers die op de opgezette volumes worden opgeslagen. De back-ups worden opgeslagen in gecodeerde EBS (Elastic Block Storage) in hetzelfde gebied als de productieomgeving. De automatische steunen zijn niet openbaar toegankelijk omdat zij in een afzonderlijk systeem worden opgeslagen.

>[!NOTE]
>
>De opgezette volumes omvatten slechts/verwijzen naar de [ beschrijfbare steunen ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/app/properties/properties#mounts) en zullen niet al uw `app/` folder omvatten. Zoals voor de andere dossiers, worden zij gecreeerd/geproduceerd door [ bouwt en plaatsingsproces ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/pro-develop-deploy-workflow#deployment-workflow), en u zult ook uw bewaarplaats van het Git voor resterende dossiers moeten controleren.

{{pro-backups}}

U kunt a **handsteun** van het gegevensbestand voor uw het Opvoeren en milieu&#39;s van de Productie tot stand brengen gebruikend bevelen CLI. Zie [ file het gegevensbestand ](../storage/database-dump.md). Voor `integration` -omgevingen raadt de Adobe aan een back-up te maken als eerste stap nadat ze uw Adobe Commerce hebben benaderd voor een cloud-infrastructuurproject en voordat ze belangrijke wijzigingen aanbrengen. Zie [ Reservekopiebeheer ](../storage/snapshots.md).

### Doelstelling herstelpunt

Neem contact op met de Customer Success Manager van de Adobe voor meer informatie over de tijd die het herstelpunt nodig heeft om de laatste back-up te maken. De frequentie van back-ups is afhankelijk van het back-upschema van uw abonnement en het volume van de wijzigingen dat naar de opslagservice moet worden geschreven.

### Retentiebeleid

Met Adobe blijven automatische back-ups behouden volgens het volgende beleid voor gegevensopslag:

| Tijdsperiode | Retoucheringsbeleid voor back-up |
| ------------------ | ----------------------- |
| Dag 1 tot en met 3 | Eén back-up per uur |
| Dagen 4 tot en met 7 | Eén back-up per dag |
| Week 2 tot en met 6 | Eén back-up per week |
| Week 8 tot en met 12 | Eén back-up per twee weken |
| Maand 3 tot en met 5 | Eén back-up per maand |

Dit beleid kan afhankelijk van uw plan van de wolkeninfrastructuur variëren.

### Doelstelling hersteltijd

RTO is afhankelijk van de grootte van de opslag. Grote EBS-volumes hebben meer tijd nodig om te herstellen. De hersteltijden kunnen variëren, afhankelijk van de grootte van de database. Neem voor meer informatie contact op met de Customer Success Manager van de Adobe.

## Schalen in Pro-clusters

Het Pro cluster rangschikken en _verwerkt_ configuraties afhankelijk van de gekozen wolkenleverancier (AWS, Azure), gebied, en de dienstgebiedsdelen. De de wolkeninfrastructuur van de Adobe kan Pro clusters schrapen om verkeersverwachtingen en de dienstvereisten aan te passen aangezien de vraag verandert.

De overtollige architectuur laat de Adobe wolkeninfrastructuur toe om zonder onderbreking te verhogen. Bij upscaling roteert elk van de drie instanties om de capaciteit te upgraden zonder dat dit invloed heeft op de sitebewerking. U kunt bijvoorbeeld extra webservers toevoegen aan een bestaande cluster als de beperking zich op PHP-niveau bevindt in plaats van op databaseniveau. Dit verstrekt _horizontaal schrapen_ om het verticale schrapen aan te vullen die door extra CPUs op het gegevensbestandniveau wordt verstrekt. Zie [ Schaalde architectuur ](scaled-architecture.md).

Als u een significante toename van verkeer voor een gebeurtenis of een andere reden verwacht, kunt u om een tijdelijke verhoging van capaciteit verzoeken. Zie [ hoe te om een tijdelijke upsize ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html) in het _Centrum van de Hulp van Commerce_ te verzoeken.
