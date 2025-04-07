---
title: Opmerkingen bij de release ECE-Tools
description: Zie een lijst met de meest recente verbeteringen in het pakket ECE-Tools.
recommendations: noDisplay, catalog
last-substantial-update: 2024-04-03T00:00:00Z
exl-id: 3cbfe698-d75d-4a16-877a-52c214595344
source-git-commit: 3d5c84890f48a26938b42783b591b876fd2a2fd1
workflow-type: tm+mt
source-wordcount: '3059'
ht-degree: 0%

---

# Opmerkingen bij de release ECE-Tools

Het [ kind-hulpmiddelen ](https://github.com/magento/ece-tools) pakket is een reeks manuscripten en hulpmiddelen die worden ontworpen om de projecten van de Wolk te beheren en op te stellen. Deze versienota&#39;s beschrijven de recentste verbeteringen aan dit pakket, dat deel van de [ Reeks van Hulpmiddelen van de Wolk voor Commerce ](cloud-tools-suite.md) uitmaakt.

>[!NOTE]
>
>Zie [ Verbetering ECE-Hulpmiddelen ](../dev-tools/update-package.md) voor informatie over het bijwerken aan de recentste versie van het `ece-tools` pakket.

Het pakket `ece-tools` gebruikt de volgende versiesequentie voor releases: `200<major>.<minor>.<patch>`

De opmerkingen bij de release omvatten:

- ![ nieuw pictogram ](../../assets/new.svg) Nieuwe eigenschappen
- ](../../assets/fix.svg) Bevestigingspictogram van 0} moeilijke situatie en verbeteringen![

<!--Add release notes below-->

## v2002.2.2 {#latest}

Releasedatum: 3 april 2025

- ![ nieuw pictogram ](../../assets/new.svg) **Valkey** - toegevoegde steun voor de nieuwe dienst (Valkey), die een vervanging voor Redis is.<!-- MCLOUD-13455	 - -->
- ![ fixpictogram ](../../assets/fix.svg) **Openssearch2 voor 2.4.4/2.4.5** - toegevoegde steun voor `opensearch2` in de versies van Adobe Commerce 2.4.4/2.4.5. <!-- MCLOUD-13493	 - -->

## v2002.2.1

Releasedatum: 6 februari 2024

- ![ nieuw pictogram ](../../assets/new.svg) **PHP 8.4** - toegevoegde steun voor PHP 8.4.<!-- MCLOUD-13145	 - -->
- ![ fixpictogram ](../../assets/fix.svg) **Validator voor Openssearch** - Vaste validator die een misleidend bericht over de verkeerde versie van de dienst produceerde.<!-- MCLOUD-13184	 - -->


## v2002.2.0

Releasedatum: 7 oktober 2024

- ![ nieuw pictogram ](../../assets/new.svg) **MariaDB 11.4**-Toegevoegde steun van MariaDB 11.4.
- ![ fixpictogram ](../../assets/fix.svg) **Refactored code** - Verwijderde steun van oude PHP versies 7.4, 7.3, 7.2 en verwante bibliotheken.<!-- MCLOUD-9278 -->
- ](../../assets/fix.svg) **Bevestigingspictogram ![ Bevorderde versie Monolog** - Toegevoegde steun voor monolog 3.6.<!-- MCLOUD-12855 -->
- ![ fixpictogram ](../../assets/fix.svg) **Validator voor RabbitMQ, MariaDB, en PHP** - Vaste validator die een misleidend bericht over de verkeerde versie van de dienst produceerde.

## v2002.1.19

Releasedatum: 21 mei 2024

- ![ nieuw pictogram ](../../assets/new.svg) **Lua** - Toegevoegde optie useLua voor CACHE_CONFIGURATION.
- ![ fixpictogram ](../../assets/fix.svg) **Validator** - bijgewerkte validators voor nieuwe versies van Redis en RabbitMQ.

## v2002.1.18

Releasedatum: 8 april 2024

- ![ nieuw pictogram ](../../assets/new.svg) **PHP** — Toegevoegde steun voor PHP 8.3.
- ![ fixpictogram ](../../assets/fix.svg) **Validator** - Bijgewerkte validator EOL.

## v2002.1.17

Releasedatum: 16 januari 2024

- ![ fixpictogram ](../../assets/fix.svg) **Validator voor Elasticsearch &amp; OpenSearch** - Vaste validator die een misleidend bericht produceerde om de onderzoeksdienst te installeren wanneer LiveSearch wordt toegelaten.<!-- MCLOUD-10167 -->
- ](../../assets/fix.svg) **de waarschuwing van de Plaatsing 1} ![ fixpictogram** - Vaste een kwestie die in plaatsingswaarschuwingen over niet-lege omslagen resulteerde.<!-- MCLOUD-8958 -->

## v2002.1.16

Releasedatum: 16 oktober 2023

- ![ nieuw pictogram ](../../assets/new.svg) **ENABLE_WEBHOOKS globale milieu veranderlijk** - toegevoegd [ ENABLE_WEBHOOKS ](../environment/variables-global.md#enable_webhooks) globale variabele voor gebruik met de websites van Commerce om met een extern eindpunt, zoals runtime van App Builder actie of een systeem van het derdeninventarisbeheer te verbinden.

## v2002.1.15

Releasedatum: 31 juli 2023

- ![ herstellingspictogram ](../../assets/fix.svg) **de codes van de Fout** - bijgewerkt het schema van de foutencode en de generator van het foutencodedocument.
- ](../../assets/fix.svg) **Bevestigingspictogram ![ bevestigt Validator voor douane Redis model** - Bijgewerkt validator voor douane Redis achterste modellen. [ zie het voorbeeld voor geheim voorgeheugenconfiguratie ](../environment/variables-deploy.md#cache_configuration).
- ![ fixpictogram ](../../assets/fix.svg) **Validator voor RabbitMQ** - Toegevoegde steun voor RabbitMQ 3.11
- ![ fixpictogram ](../../assets/fix.svg) **Vaste de verkeerde verbinding** - Vaste de verkeerde verbinding aan de onboarding documentatie in het welkome e-mailmalplaatje.

## v2002.1.14

Releasedatum: 10 maart 2023

- ![ nieuw pictogram ](../../assets/new.svg) **PHP** - toegevoegde steun voor PHP 8.2.
- ![ nieuw pictogram ](../../assets/new.svg) **Validators voor de Diensten** - Bijgewerkte validators voor Commerce 2.4.6 vereiste diensten: MariaDB 10.6, Redis 7.0, PHP 8.2, OpenSearch 2.x, en RabbitMQ 3.9.
- ![ herstellingspictogram ](../../assets/fix.svg) **knoop-hulpmiddelen db-stortplaats** - Vaste een kwestie die de `db-dump` verrichting veroorzaakte om voortijdig te stoppen.

## v2002.1.13

Releasedatum: 27 oktober 2022

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde steun voor Adobe I/O Events voor Adobe Commerce**. De ontwikkelaars van de uitbreiding kunnen het [ Adobe I/O Events ](https://developer.adobe.com/events/docs/) kader nu gebruiken om de gebeurtenisinformatie van Commerce van de instanties van de Wolk naar hun toepassingen te verzenden die voor [ App Builder van Adobe ](https://developer.adobe.com/app-builder/docs/overview/) worden geschreven. Adobe I/O Events for Adobe Commerce is in de Voorproef van de Partner.<!-- CEXT-932 -->
- ![ nieuw pictogram ](../../assets/new.svg) **Validator voor configuratie OPcache** - voegde een validator toe om de configuratie OPcache voor uitgesloten wegen te controleren.<!-- MCLOUD-9485 -->
- ![ fixpictogram ](../../assets/fix.svg) **Vaste een kwestie met het geheim voorgeheugenconfiguratie van GraphQL** - nu ECE-Hulpmiddelen houdt de GraphQL `id_salt` waarde in `cache` configuratie in het `app/etc/env.php` dossier.<!-- MCLOUD-9486 -->

## v2002.1.12

Releasedatum: 13 september 2022

- ![ nieuw pictogram ](../../assets/new.svg) **laat`synchronous_replication`** toe - ECE-hulpmiddelen reeksen `synchronous_replication=>true` in het `app/etc/env.php` dossier wanneer `MYSQL_USE_SLAVE_CONNECTION` wordt toegelaten. Deze configuratie heeft alleen invloed op Commerce 2.4.6+. Zie de `MYSQL_USE_SLAVE_CONNECTION` veranderlijke beschrijving in [ stelt variabelen ](../environment/variables-deploy.md#mysql_use_slave_connection) op.<!-- MCLOUD-9142 -->
- ![ nieuw pictogram ](../../assets/new.svg) **OpenSearch** - toegevoegde functionaliteit om de `opensearch` motor voor volgende versie 2.4.6 van Adobe Commerce te vormen en te plaatsen. Zie [ de dienst van OpenSearch van de Opstelling ](../services/opensearch.md).<!-- MCLOUD-9236 -->

## v2002.1.11

Releasedatum: 4 augustus 2022

- ![ herstellingspictogram ](../../assets/fix.svg) **Validator ElasticSuite en OpenSearch** - Vaste ElasticSuite integriteitscontrole validatorkwestie wanneer OpenSearch geïnstalleerd is.<!-- MCLOUD-8767 -->
- ![ fixpictogram ](../../assets/fix.svg) **de types van Terugkeer voor opstellen bevelen** - Vaste terugkeertypes voor opstellen bevelen.<!-- AC-3208 -->
- ![ het pictogram van de moeilijke situatie ](../../assets/fix.svg) **[!DNL RabbitMQ]kwestie met nieuwe installatie van Commerce 2.4.5** - Vaste [!DNL RabbitMQ] neerstortingskwestie op nieuwe Commerce 2.4.5. installatie.<!-- MCLOUD-9059 -->

## v2002.1.10

Releasedatum: 31 maart 2022

- ![ fixpictogram ](../../assets/fix.svg) **Elasticsearch 7.10** - Bijgewerkte validators om versie 7.10 van Elasticsearch te steunen.<!-- MCLOUD-8548 -->

## v2002.1.9

Releasedatum: 10 maart 2022

- ![ nieuw pictogram ](../../assets/new.svg) **OpenSearch** - Toegevoegde steun voor OpenSearch voor versies 2.4.4 van Adobe Commerce, 2.4.3-p2, en 2.3.7-p3.<!-- MCLOUD-8296 -->
- ![ nieuw pictogram ](../../assets/new.svg) **PHP** - toegevoegde steun voor PHP 8.1.
- ![ herstellingspictogram ](../../assets/fix.svg) **symfony/proces** - voegde de verenigbaarheid met symfony/proces ^5.3 toe.<!-- MCLOUD-8283 -->

- ![ nieuw pictogram ](../../assets/new.svg) **Verbruiks veelvoudige processen** - toegevoegd a `multiple_processes` optie zodat u het aantal processen kunt specificeren om voor elke consument te kweken. Zie de `CRON_CONSUMERS_RUNNER` veranderlijke beschrijving in [ stelt variabelen ](../environment/variables-deploy.md#cron_consumers_runner) op.<!-- MCLOUD-8295 -->
- ![ nieuw pictogram ](../../assets/new.svg) **regeling OpenSearch en volledige gastheerweg** - voegde de capaciteit toe om een regeling van Elasticsearch en volledige gastheerweg te vormen.
- ![ fixpictogram ](../../assets/fix.svg) **AWS S3** - veranderde de methode van AWS S3 enablement.
- ![ fixpictogram ](../../assets/fix.svg) **Fix driver_options reader** - Toegevoegde het lezen driver_options configuratie voor de verbinding van DB van het `env.php` dossier door `ece-tools` voor validators.<!-- MCLOUD-8420 -->

## v2002.1.8

Releasedatum: 25 oktober 2021

- ![ nieuw pictogram ](../../assets/new.svg) **Alternatieve stortplaats** - toegevoegd de `--dump-directory` optie zodat u een doelfolder voor een stortplaats van DB kunt kiezen. Nu is `/app/var/dump-main` de standaarddoelmap voor een DB-dump. Zie [ Reservekopiebeheer: Dump uw gegevensbestand ](../storage/database-dump.md)<!-- MCLOUD-8063 -->
- ![ fixpictogram ](../../assets/fix.svg) **Update Monolog** - werkte de minimumversie bij die voor het `monolog` pakket aan `^2.3` wordt vereist.<!-- ACMP-1263 -->
- ![ herstellingspictogram ](../../assets/fix.svg) **Symfony van de Update** - werkte de gebiedsdelen van het Symfonie bij om met Adobe Commerce 2.4.4 compatibel te zijn.<!-- ACMP-1533 -->
- ![ herstellingspictogram ](../../assets/fix.svg) **Eigenschap/los autoload** op - Vaste een kwestie wanneer het opstellen aan een integratiemilieu en het zien van de `CRITICAL: [9] Required configuration is missed in autoload section of composer.json file.` fout.<!-- https://github.com/magento/ece-tools/pull/799 -->

## v2002.1.7

Releasedatum: 29 juli 2021

**de updates van de Configuratie**—

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor Composer 2.0.<!--MCLOUD-8003-->

- ![ fixpictogram ](../../assets/fix.svg) **werkte composer vereisten voor`symphony/console`** bij - werkte de ECE-Hulpmiddelen `composer.json` versievereisten voor het `symphony/console` pakket bij om een kwestie te bevestigen die `di:compile` bevelen veroorzaakte om met de volgende fout te ontbreken: `Incompatible argument type: Required type: int. Actual type: string`<!--MC-42919-->

- ![ fixpictogram ](../../assets/fix.svg) werkte de eind-van-leven softwarecontroles (`eol.yaml`) bij om Elasticsearch 7.9.x te omvatten.<!--MCLOUD-7938-->

## v2002.1.6

Releasedatum: 20 april 2021

- ![ nieuw pictogram ](../../assets/new.svg) **opnieuw afgeeft authentificatiegeloofsbrieven** - Toegevoegd de capaciteit om Redis vergunningsgeloofsbrieven van het `relationships` bezit tijdens op te stellen fase te lezen.<!--MCLOUD-7694-->

- ![ nieuw pictogram ](../../assets/new.svg) **de vergunningsgeloofsbrieven van Elasticsearch** - voegde de capaciteit toe om de vergunningsgeloofsbrieven van Elasticsearch van het `relationships` bezit tijdens op te stellen fase te lezen.<!--MCLOUD-7695-->

- ![ nieuw pictogram ](../../assets/new.svg) **Dedicated de dienst van de zittingsopslag** - toegevoegd `redis-session` als tweede optie voor zittingsopslag. U kunt de `redis-session` dienst gebruiken om zittingsinformatie op te slaan en de `redis` dienst voor geheim voorgeheugen te gebruiken om betere prestaties te verstrekken.<!--MCLOUD-7698-->

- ![ nieuw pictogram ](../../assets/new.svg) **Afgekeurde SPLIT_DB- berichten** - Toegevoegde validatorwaarschuwing en kritieke berichten voor de afgekeurde `SPLIT_DB` optie voor Adobe Commerce 2.4.2 en zijn verwijdering in Adobe Commerce 2.5.0.<!--MCLOUD-7806-->

- ![ fixpictogram ](../../assets/fix.svg) **versie van Elasticsearch van verhoudingen** - Vaste de bevestiging van de Dienst om de correcte versie van Elasticsearch van de `relationships` eigenschappen in de Server van de Wolk en integratiemilieu&#39;s terug te winnen.<!--MCLOUD-7572-->

- ![ herstellingspictogram ](../../assets/fix.svg) **Flexibele havenbevestiging** - kan nu de haven in een verbinding van het douanegeheime voorgeheugen van `server` URL bevestigen. U kunt bijvoorbeeld als volgt uw poortnummer aan de URL van de server toevoegen: `server: 'tcp://rfs-store-simple-page-cache:26379'` . Hiermee voorkomt u validatiefouten waarbij de optie `port` ontbreekt of onjuist is.<!--MCLOUD-7722-->

- ![ fixpictogram ](../../assets/fix.svg) **Bevorderend aan Adobe Commerce 2.4.2** - Vaste de kwestie die gebruikers vereiste om `bin/magento setup:upgrade` manueel in werking te stellen om hun plaatsen na bevordering aan Adobe Commerce 2.4.2 operationeel te maken.<!--MCLOUD-7776-->

## v2002.1.5

Releasedatum: 1 februari 2021

- ![ nieuw pictogram ](../../assets/new.svg) **Verre opslag** - voegde de `REMOTE_STORAGE` milieuvariabele toe om de Projecten van de Wolk voor verre opslag van media dossiers toe te laten gebruikend de opslagdienst, zoals AWS S3. Deze configuratieoptie maakt deel uit van het pakket ECE-Tools, maar wordt niet ondersteund door Adobe Commerce op cloudinfrastructuur.<!--MCLOUD-7153-->

- ![ nieuw pictogram ](../../assets/new.svg) **Nieuw `cloud:config:validate` bevel** - toegevoegd bevel `php vendor/bin/ece-tools cloud:config:validate` om de `.magento.env.yaml` configuratie te bevestigen alvorens veranderingen in het verre milieu van de Wolk te duwen.<!--MCLOUD-7120-->

- ![ nieuw pictogram ](../../assets/new.svg) **Flushing het opcache** - toegevoegde steun voor de `opcache.enable_cli` PHP optie om OPCache te spoelen alvorens de op te stellen haak in werking te stellen. Deze configuratie stelt de geheim voorgeheugenconfiguratie terug om ervoor te zorgen dat de huidige configuratiemontages op elke plaatsing worden toegepast.<!--MCLOUD-7015-->

- ![ nieuw pictogram ](../../assets/new.svg) **Bevestiging van OB Aurora** - werkte de bevestiging van de gegevensbestanddienst bij zodat het met het gegevensbestand van Aurora compatibel is.<!--MCLOUD-7269-->

- ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe SCD_NO_PARENT milieu variabele** - voegde de `SCD_NO_PARENT` milieuvariabele (voor Adobe Commerce >=2.4.2) toe om de generatie van statische inhoud voor ouderthema&#39;s te beheren.<!--MCLOUD-7284-->

- ![ bevestig pictogram ](../../assets/fix.svg) **de grenzen en de bevelen van het Geheugen** - Vaste een kwestie waar `php vendor/bin/ece-tools` bevelen niet zouden werken als de grootte van het `cloud.log` dossier PHP memory_limit overschreed. In plaats van het volledige `cloud.log` bestand in het geheugen te lezen, lezen we nu alleen een kleinere subset van gegevens uit het logbestand. <!--MCLOUD-7275--><!--MCLOUD-7400-->

- ![ het pictogram van de moeilijke situatie ](../../assets/fix.svg) **de gegevensbestandverbindingen van de Douane** - Vaste a `.magento.env.yaml` configuratiekwestie waarin de verbindingen van het douanegegevensbestand die voor `DATABASE_CONFIGURATION` werden bepaald niet werden gebruikt. De verbindingsinstellingen zijn niet toegevoegd aan `app/etc/env.php` . <!--MCLOUD-7426-->

- ](../../assets/fix.svg) **Lege foutenlogboeken** - Vaste een kwestie die plaatsingen veroorzaakte om te ontbreken als `cloud.error.log` leeg was.<!--MCLOUD-7296-->![

- ![ fixpictogram ](../../assets/fix.svg) **MariaDB 10.3 bevestiging** - Vaste bevestiging van MariaDB 10.3 voor Adobe Commerce 2.3.6-p1.<!--MCLOUD-7416-->

- ![ fixpictogram ](../../assets/fix.svg) **Geheime voorgeheugen:flush registreren** - Verbeterde logboekingangen om op het begin en de beëindiging van de `cache:flush` stap te wijzen.<!--MCLOUD-7503-->

## v2002.1.4

Releasedatum: 19 november 2020

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die plaatsingsmislukking veroorzaakte wanneer de onderzoeksmotor die in de `SEARCH_CONFIGURATION` milieuvariabele wordt gespecificeerd een waarde buiten `elasticsearch` is.<!--MCLOUD-7283-->

## v2002.1.3

Releasedatum: 9 november 2020

**de updates van de Infrastructuur**—

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde ECE-Hulpmiddelen steun voor de read-only `pub/static` folder wanneer de statische inhoud wordt geplaatst om in het bouwstijlstadium op te stellen.<!--MC-37699-->

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor Elasticsearch 7.9 en Redis 6 voor verenigbaarheid met de aanstaande versies van Adobe Commerce.<!--MCLOUD-7191-->

- ![ fixpictogram ](../../assets/fix.svg) werkte ECE-Hulpmiddelen `composer.json` bij om een vereiste gebiedsdeel voor het Hulpmiddel van de Patches van de Kwaliteit toe te voegen. Dit verhelpt een cirkelafhankelijkheid die tussen de ECE-Hulpmiddelen en magento-cloud-flarden pakketten bestond.<!--MCLOUD-6910-->

**Bevestiging en logboekverbeteringen**—

- ![ nieuw pictogram ](../../assets/new.svg) toegevoegde onderzoek-motor bevestiging om ervoor te zorgen dat `elasticsearch` voor Adobe Commerce op wolkeninfrastructuur 2.4 en later wordt geplaatst. Als de bevestiging ontbreekt, wordt de plaatsing tegengehouden met een kritiek foutenbericht dat oplossingen voor de kwestie voorstelt. Zie [ Kritieke Fouten, opstellen stadium ](../dev-tools/error-reference.md#deploy-stage).<!--MCLOUD-6937-->

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde bevestiging van Elasticsearch om de verenigbaarheid tussen de de dienstversie van Elasticsearch en de versie van Adobe Commerce te controleren.<!--MCLOUD-7193-->

- ![ nieuw pictogram ](../../assets/new.svg) werkte het de verenigbaarheidsfoutenmelding van Elasticsearch bij om de versies van Elasticsearch te tonen die met de module van Adobe Commerce Elasticsearch compatibel zijn. Het foutbericht bevat nu de specifieke Elasticsearch-versies die in uw Cloud-infrastructuur moeten worden geïnstalleerd, zodat deze compatibel zijn met de Elasticsearch-module die door uw versie van Adobe Commerce wordt gebruikt. Zie {de Fouten van de 0} Waarschuwing, opstellen stadium ](../dev-tools/error-reference.md#deploy-stage-1).<!--MCLOUD-6698-->[

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde waarschuwingsfouten `2026` en `2027` voor ongeldige `MAGE_MODE` milieu veranderlijke het plaatsen. De enige geldige waarde is `production` . Vóór deze correctie kan `MAGE_MODE` zonder implementatiefouten op `developer` worden ingesteld, alleen om later fouten te veroorzaken bij het schrijven naar alleen-lezen bestanden. Zie [ de Fouten van de Waarschuwing ](../dev-tools/error-reference.md#warning-errors).<!--MCLOUD-6708-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste bevestiging voor Redis, RabbitMQ, en de diensten MySQL om ervoor te zorgen dat deze versies met de versie van Adobe Commerce compatibel zijn. Geldige versies van deze services worden nu naar de map `cloud.log` geschreven. <!--MCLOUD-7098-->

- ![ fixpictogram ](../../assets/fix.svg) werkte `cloud.log` bij om de gezamenlijke verzoekgrens te omvatten om verzoeken tijdens geheim voorgeheugenwarmte te verzenden. Deze waarde wordt gevormd in [ WARM_UP_CONCURRENCY ](../environment/variables-post-deploy.md#warm_up_concurrency) post-opstellen variabele.<!--MCLOUD-5563-->

**CLI bevelupdates**—

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde CLI bevelen (`cloud:config:create` en `cloud:config:update`) om het `.magento.env.yaml` dossier met een configuratie tot stand te brengen en bij te werken die één of meerdere bouwstijl, opstellen, en post-opstelt variabelen kunnen omvatten. Zie [ configuratiedossier van CLI ](../environment/configure-env-yaml.md#create-configuration-file-from-cli) creëren.<!--MCLOUD-7072-->

**veranderlijke updates van het Milieu**—

- ![ nieuw pictogram ](../../assets/new.svg) voegde [ SKIP_COMPOSER_DUMP_AUTOLOAD ](../environment/variables-build.md#skip_composer_dump_autoload) bouwstijlvariabele toe. Als u de variabele instelt op `true` , wordt de opdracht `composer dump-autoload` niet uitgevoerd tijdens een Cloud Docker voor Commerce-installatie. De variabele is alleen relevant voor Cloud Docker voor Commerce-containers met beschrijfbare bestandssystemen (gemaakt voor testen en ontwikkelen met `./vendor/bin/ece-docker build:compose --with-test`). Bij dergelijke installaties voorkomt het overslaan van de opdracht `composer dump-autoload` fouten bij het uitvoeren van andere opdrachten die proberen toegang te krijgen tot bestanden uit een verwijderde `generated` -map. <!--MCLOUD-6939-->

## v2002.1.2

Releasedatum: 5 augustus 2020

**Bevestiging en logboekverbeteringen**—

- ![ nieuw pictogram ](../../assets/new.svg) voegde het `schema.error.yaml` dossier toe dat alle fout en waarschuwingsberichten omvat die tijdens de bouwstijl kunnen voorkomen, opstellen, en post-opstellen proces samen met suggesties om de fouten op te lossen. De informatie in dit dossier is ook beschikbaar in de _Gids van de Wolk voor Commerce_. Zie [ de berichtverwijzing van de Fout voor Griekenland-hulpmiddelen ](../dev-tools/error-reference.md).<!--MCLOUD-5878-->

- ![ nieuw pictogram ](../../assets/new.svg) veranderde het foutenlogboek van de Wolk (`/var/log/cloud.error.log`) ingangen in formaat JSON om het logboek gemakkelijker te maken programmatically te ontleden.<!--MCLOUD-5879-->

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde extra foutencontroles om te bouwen, op te stellen, en na-stelt verwerking en betere bestaande controles op:

   - Foutcode 2026—Kan sommige gegevens die tijdens de constructiefase zijn gegenereerd, niet herstellen naar de gekoppelde mappen

   - Foutcode 3004—Kan geen back-upbestanden maken

   - Foutcode 102—Aanvullende controles toegevoegd voor problemen die optreden wanneer het `env.php` -bestand niet beschrijfbaar is <!--MCLOUD-6221-->

- ![ nieuw pictogram ](../../assets/new.svg) voegde **QUALITY_PATCHES** milieuvariabele toe om één of meerdere kwaliteitspatches te specificeren tijdens het plaatsingsproces van toepassing te zijn. Zie [ variabelen bouwen ](../environment/variables-build.md#quality_patches).<!--MCLOUD-6375-->

## v2002.1.1

Releasedatum: 25 juni 2020

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Infrastructuur**—

   - ![ nieuw pictogram ](../../assets/new.svg) **het Registreren verbeteringen** - verbeterd logboek-volgend vermogen door uitgangscodes toe te wijzen om fouten kritisch op te stellen en de uitgangscodes in foutenmeldingen en logboekgebeurtenissen bloot te stellen. Zie [ de berichtverwijzing van de Fout voor Griekenland-hulpmiddelen ](../dev-tools/error-reference.md).<!-- MCLOUD-5637, 5531-->

   - ![ nieuw pictogram ](../../assets/new.svg) verbeterde het proces voor gegevensbestanddumps (`vendor/bin/ece-tools db-dump`) en bijgewerkte logboekberichten om te verduidelijken dat de verrichting van de gegevensbestandstortplaats de toepassing aan onderhoudswijze schakelt, de processen van de consumentenrij tegenhoudt, en snijbanen onbruikbaar maakt alvorens de stortplaats begint.<!--MCLOUD-5324, MCLOUD-2062-->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie om ervoor te zorgen dat het project URL correct wanneer het opstellen aan het Opvoeren en de milieu&#39;s van de Productie wordt bijgewerkt. Nu, `ece-tools` gebruikt URL voor de route met het `primary:true` attribuut dat in de configuratie van de projectroute wordt geplaatst. Zie [ variabelen opstellen ](../environment/variables-deploy.md#update_urls).<!--MCLOUD-5883-->

   - ![ fixpictogram ](../../assets/fix.svg) werkte het `generate.xml` werkschema van het bouwstijlscenario voor het toepassen van flarden bij. Patches moeten eerder worden toegepast om Adobe Commerce bij te werken om problemen op te lossen die ertoe kunnen leiden dat de stappen `di:compile` en `module:refresh` mislukken. <!--MCLOUD-5941-->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie in het installatieproces dat verkeerd de `Crypt key missing` fout terugkeert. De `crypt/key` -waarde wordt automatisch tijdens de installatie gegenereerd. <!--MCLOUD-6120-->

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Dienst**—

   - ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor PHP 7.4 en MariaDB 10.4.<!--MAGECLOUD-2957, MCLOUD-4144-->

- ![ nieuw pictogram ](../../assets/new.svg) **veranderlijke updates van het Milieu** -

   - ![ nieuw pictogram ](../../assets/new.svg) voegde **SCD_USE_BALER** variabele toe om de module van de Baller voor JavaScript die tijdens Adobe Commerce bundelt op het de bouwproces van de wolkeninfrastructuur toe te laten. Zie de veranderlijke beschrijving in [ bouwt variabelen ](../environment/variables-build.md#scd_use_baler).<!-- MCLOUD-3456, MCLOUD-3457-->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde **REDIS_BACKEND** milieuvariabele toe om Redis achterste model voor Redis geheime voorgeheugen voor Adobe Commerce 2.3.5 of later te vormen. Zie de veranderlijke beschrijving in [ variabelen ](../environment/variables-deploy.md#redis_backend) opstellen.<!--MCLOUD-5721, MCLOUD-5865-->

- ![ nieuw pictogram ](../../assets/new.svg) **CLI bevelupdates**—

   - ![ nieuw pictogram ](../../assets/new.svg) werkte de volgende bevelen CLI met een optie voor meer gedetailleerd registreren bij:

      - `app:config:dump`
      - `app:config:import`
      - `module:enable`

     Het registrerenniveau voor elke vraag wordt bepaald door de configuratie van [`VERBOSE_COMMANDS`](../environment/variables-build.md#verbose_commands) variabele in het `.magento.env.yaml` dossier.<!--MCLOUD-3503-->

- ![ nieuw pictogram ](../../assets/new.svg) **de verbeteringen van de Bevestiging** -

   - ![ nieuw pictogram ](../../assets/new.svg) **Elasticsearch 7.x verenigbaarheidscontroles** - bijgewerkte bevestiging van Elasticsearch voor Elasticsearch 7.x de controles van de softwareverenigbaarheid.<!--MCLOUD-5542-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Bijgewerkte de dienstversie en de bevestigingscontroles EOL** - bijgewerkte bevestiging om geïnstalleerde de dienstversies tegen Adobe Commerce 2.4 te controleren.<!--MCLOUD-6144-->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een bevestigingskwestie zodat het volgende post-opstelt waarschuwingsbericht toont slechts als de `post-deploy` hakconfiguratie van het `.magento.app.yaml` dossier mist:

     ```text
     Your application does not have the "post_deploy" hook enabled.
     ```

     <!--MCLOUD-4077-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde bevestiging voor de gebiedsdelen van het Kader van Zend** - Toegevoegde componentengebiedsbevestiging voor het Kader van Zend dat aan het project van Laminas is gemigreerd. Als de vereiste gebiedsdelen ontbreken, toont het volgende foutenbericht tijdens het bouwstijlproces.

     ```text
     Required configuration is missing from the autoload section of the composer.json file.
     Add ("Laminas\Mvc\Controller\Zend\": "setupsrc/ Zend/Mvc/Controller/") to
     the `autoload -> psr-4` section. Then, re-run the "composer update" command locally, and
     commit the updated composer.json and composer.lock files.
     ```

     Zie [ verifiëren de gebiedsdelen van het Kader van Zend ](../development/commerce-version.md#verify-zend-framework-composer-dependencies).<!--MCLOUD-4094-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde bevestiging voor `env.php` dossier en gegevens** - toegevoegde controles voor het `env.php` dossier en gegevens tijdens installeren en verbeteringsproces.<!--MCLOUD-5991-->

      - Als het `env.php` -bestand ontbreekt in de installatie en de `crypt/key` -waarde niet is opgegeven in het `.magento.app.yaml` -bestand, mislukt de implementatie met de volgende melding:

        ```text
        The crypt/key key value does not exist in the ./app/etc/env.php file or the CRYPT_KEY cloud environment variable``Missing crypt key for upgrading Magento`.
        ```

      - Als de installatie het `env.php` -bestand niet bevat of als de configuratie slechts één cachetype bevat, wordt de opdracht `cron:enable` uitgevoerd tijdens het upgradeproces om het bestand met alles te herstellen `cache_types` . Het volgende bericht wordt toegevoegd aan het logboek:

        ```text
        Magento state indicated as installed but configuration file app/etc/env.php was empty or did not exist.
        Required data will be restored from environment configurations and from the .magento.env.yaml file.
        ```

## v2002.1.0

Releasedatum: 6 februari 2020

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Infrastructuur**—

   - ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegd afzonderlijk pakket voor het Dok van de Wolk voor Commerce** - ontkoppelde het pakket van de Dok van het `ece-tools` pakket om codekwaliteit te handhaven en onafhankelijke versies te verstrekken. De updates en de moeilijke situaties met betrekking tot `ece-tools` worden geleid van de [ magento-cloud-docker ](https://github.com/magento/magento-cloud-docker) bewaarplaats GitHub.<!--MAGECLOUD-2927-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Bijgewerkt het patchen mogelijkheden** - Bewegd de het patchen functionaliteit van het ECE-Hulpmiddel pakket aan een afzonderlijk [ magento-cloud-patches ](https://github.com/magento/magento-cloud-patches) pakket. Tijdens de implementatie gebruikt `ece-tools` het nieuwe pakket om patches toe te passen. Zie [ de versienota&#39;s van de flarden van de Wolk ](cloud-patches.md).<!--MAGECLOUD-4567-->

   - ![ nieuw pictogram ](../../assets/new.svg) **werkte Vereisten Composer** bij - werkte het `composer.json` dossier voor Adobe Commerce op wolkeninfrastructuur met een gebiedsdeel voor het `magento/magento-cloud-docker` pakket bij. `ece-tools` bevat nu afhankelijkheden voor alle pakketten in de [`Cloud Tools Suite for Commerce`](cloud-tools-suite.md) . Deze pakketten worden automatisch geïnstalleerd en bijgewerkt wanneer u `ece-tools` installeert of bijwerkt.

- ![ nieuw pictogram ](../../assets/new.svg) **Steun voor op scenario-gebaseerde plaatsingen** - <!--MAGECLOUD-4101-->

   - ![ nieuw pictogram ](../../assets/new.svg) nu kunt u de bouwstijl aanpassen, processen opstellen en post-opstellen gebruikend de configuratiedossiers van XML om de standaardconfiguratie met voeten te treden of aan te passen.

   - ![ nieuw pictogram ](../../assets/new.svg) **veranderde de `hooks` configuratie in`.magento.app.yaml`** - wij hebben het `hooks` configuratieformaat bijgewerkt om op scenario-gebaseerde plaatsingen te steunen. De oudere indeling van de eerdere release ECE-Tools 2002.0.x wordt nog steeds ondersteund. Nochtans, moet u aan het nieuwe formaat bijwerken om de op scenario-gebaseerde plaatsingseigenschap te gebruiken. Zie [ op scenario-Gebaseerde plaatsingen ](../deploy/scenario-based.md#add-scenarios-using-build-and-deploy-hooks).

>[!NOTE]
>
>Alvorens aan ECE-Hulpmiddelen versie 2002.1.0 bij te werken, herzie [ achterwaarts   incompatibele veranderingen ](backward-incompatible-changes.md) om over veranderingen te leren die u zouden kunnen vereisen   Adobe Commerce bijwerken over projectconfiguratie of -processen voor cloudinfrastructuur.

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Dienst**—

   - ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor PHP 7.3.<!--MAGECLOUD-4022-->

   - ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor RabbitMQ 3.8.<!--MAGECLOUD-4674-->

   - ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde bevestiging om geïnstalleerde de dienstversies tegen de datum EOL voor elke dienst te controleren. Nu, ontvangen de klanten een bericht als een de dienstversie binnen drie maanden na de datum EOL is, en een waarschuwing als de datum EOL in het verleden is.<!--MAGECLOUD-4076-->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een de configuratiekwestie van Elasticsearch om ervoor te zorgen dat de correcte montages van Elasticsearch in alle milieu&#39;s worden gevormd.<!--MAGECLOUD-4474-->

>[!NOTE]
>
>Zie [ versies van de Dienst ](../services/services-yaml.md#service-versions) voor een lijst van de diensten die in Adobe Commerce op wolkeninfrastructuur en hun versiecompatibiliteit met het malplaatje van de Wolk worden gebruikt.

- ![ nieuw pictogram ](../../assets/new.svg) **veranderlijke updates van het Milieu** -

   - ![ nieuw pictogram ](../../assets/new.svg) Uitgebreide de functionaliteit van de `WARM_UP_PAGES` omgevingsvariabele om geheim voorladen voor specifieke productpagina&#39;s te steunen. Zie de uitgebreide definitie in het [ post-opstelt variabelen ](../environment/variables-post-deploy.md#warm_up_pages) onderwerp.<!--MAGECLOUD-4444-->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde de `ERROR_REPORT_DIR_NESTING_LEVEL` milieuvariabele toe om het gegevensbeheer van foutenrapporten in de `<magento_root>/var/report/` folder te vereenvoudigen. Zie de veranderlijke beschrijving in het [ bouwt variabelen ](../environment/variables-build.md#error_report_dir_nesting_level) onderwerp.

   - ![ fixpictogram ](../../assets/fix.svg) Verwijderde `SCD_EXCLUDE_THEMES`, `STATIC_CONTENT_THREADS`, `DO_DEPLOY_STATIC_CONTENT`, en `STATIC_CONTENT_SYMLINK` milieuvariabelen. Zie [ Achteruit onverenigbare veranderingen ](backward-incompatible-changes.md#environment-configuration-changes).<!--MAGECLOUD-4407, MAGECLOUD-3873-->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie in het Elastic de configuratieproces van de Reeks zodat de standaardconfiguratie zoals verwacht wordt beschreven wanneer u `ELASTICSUITE_CONFIGURATION` vorm veranderlijk zonder de `_merge` optie opstelt.<!--MAGECLOUD-4388-->

- ![ nieuw pictogram ](../../assets/new.svg) **CLI bevelupdates**—

   - ![ nieuw pictogram ](../../assets/new.svg) **Nieuw kruin bevel** - u kunt cron verwerking in uw Adobe Commerce op het milieu van de wolkeninfrastructuur nu manueel beheren gebruikend `cron:disable` en `cron:enable` bevelen. Gebruik de opdracht Uitschakelen om alle actieve snijprocessen te stoppen en alle snijtaken uit te schakelen. Gebruik de opdracht Inschakelen om de taken voor uitsnijden weer in te schakelen wanneer u klaar bent. Zie [ cron banen ](../application/crons-property.md#disable-cron-jobs) onbruikbaar maken.

   - ![ nieuw pictogram ](../../assets/new.svg) **Verbeterde fout die** rapporteert - toegevoegd beter registreren voor CLI bevelmislukkingen die tijdens ECE-Hulpmiddelen verwerking voorkomen.<!--MAGECLOUD-4849-->

   - ![ nieuw pictogram ](../../assets/new.svg) **verwijdert afgekeurde bouwstijlbevelen** - Verwijderde de volgende bouwstijlbevelen: `m2-ece-build`, `m2-ece-deploy`, `m2-ece-scd-dump`, en anders genoemd `ece-tools docker` bevelen aan `ece-docker`. Zie [ Achteruit onverenigbaar veranderingen ](backward-incompatible-changes.md)<!--MAGECLOUD-4392-->

- ![ nieuw pictogram ](../../assets/new.svg) Verwijderde het afgekeurde `build_options.ini` dossier en toegevoegde bevestiging om te ontbreken bouwt als het dossier bestaat. Gebruik het [ .magento.env.yaml ](../environment/configure-env-yaml.md) dossier om bouwstijlopties te vormen.

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die het bouwstijlproces veroorzaakte om te ontbreken wanneer het `config.php` dossier leeg is.<!--MAGECLOUD-4127-->

## 2002,0,23

Releasedatum: 27 februari 2020

- ![ fixpictogram ](../../assets/fix.svg) Vaste een verenigbaarheidskwestie met `ece-tools` 2002.0.x versies die op bestelling statische inhoudsgeneratie verhinderden met succes op productiemodus te voltooien.

## Oudere releases

Zie het [ archief van de versienota&#39;s ](cloud-release-archive.md) voor versie 2002.0.22 en vroeger.
