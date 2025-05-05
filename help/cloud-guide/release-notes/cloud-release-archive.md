---
title: Archief met releaseopmerkingen voor ece-tools
description: Meer informatie over gearchiveerde verbeteringen voor ece-tools.
hide: true
hidefromtoc: true
recommendations: noDisplay, noCatalog
source-git-commit: 0d9d3d64cd0ad4792824992af354653f61e4388d
workflow-type: tm+mt
source-wordcount: '7147'
ht-degree: 0%

---

# Archief met releaseopmerkingen voor ece-tools

>[!NOTE]
>
>Deze releaseopmerkingen bevatten informatie en updates voor `ece-tools` v2002.0.22 en hoger. Zie [ de nota&#39;s van de Versie voor de Reeks van Hulpmiddelen van de Wolk ](cloud-tools-suite.md) om de recentste updates voor `ece-tools` en andere pakketten van de Wolk te krijgen.

## v2002.0.22

In de release `ece-tools` 2002.0.22 wordt de structuur van het `ece-tools` -pakket gewijzigd, zodat de release van `Adobe Commerce on cloud infrastructure` -patches wordt losgekoppeld van de release ECE-Tools. Vanaf deze release worden patches en kritieke oplossingen geleverd met het [`magento/magento-cloud-patches` ](https://github.com/magento/magento-cloud-patches) -pakket. Dit is een nieuwe afhankelijkheid van het `ece-tools` -pakket. We hebben deze wijzigingen aangebracht om de complexiteit te verminderen bij het plannen van releaseupdates en het werken met bijdragen van de gemeenschap.

- ![ nieuw pictogram ](../../assets/new.svg) **Veranderingen in het pakket ECE-Tools**

   - ![ nieuw pictogram ](../../assets/new.svg) Verplaatst de flarden van Adobe Commerce van het `ece-tools` pakket naar een nieuw [`magento/magento-cloud-patches` ](https://github.com/magento/magento-cloud-patches) composer pakket.

   - ![ nieuw pictogram ](../../assets/new.svg) werkte het `composer.json` dossier voor het `ece-tools` pakket bij om een gebiedsdeel voor het `magento/magento-cloud-patches` v1.0.0 pakket toe te voegen.

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die het `ece-tools` patchproces veroorzaakte om te breken wanneer het toepassen van flardreeksen bovenop veiligheid-slechts versies, die met versie 2.3.2-p2 en later beginnen. Deze kwestie werd geïntroduceerd door de nieuwe versieringsregeling die voor [ wordt goedgekeurd veiligheid-slechts flarden ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/security-patches/overview).<!--MAGECLOUD-4661-->

- ![ herstellingspictogram ](../../assets/fix.svg) **Patches en kritieke moeilijke situaties** - werk uw milieu&#39;s van de Wolk met `ece-tools` versie 2002.0.22 bij om de volgende flarden en kritieke moeilijke situaties toe te passen. Deze patches worden opgenomen in het pakket `magento/magento-cloud-patches` v1.0.0.

   - ![&#128279;](../../assets/fix.svg) **de veiligheidspatches van de Bouwer van de Steek van 0&rbrace; moeilijke situatie &lbrace;voor 2.3.1.x en 2.3.2.x versies** - lost een kwestie in de voorproef van de Bouwer van de Pagina op die ongeautoriseerde gebruikers toestaat om tot sommige malplaatjemethodes toegang te hebben die kunnen worden gebruikt om willekeurige codeuitvoering over het netwerk (RCE) te teweegbrengen die in globale informatielekken.  Dit probleem kan zich voordoen bij het gebruik van niet-ondersteunde versies van Page Builder met Adobe Commerce versies 2.3.1 en 2.3.2.<!--MAGECLOUD-4649-->

   - &rbrack;(../../assets/fix.svg) **de flarden MSI van 0&rbrace; fixepictogram** - moeilijke situaties die indexerende fouten en prestatieskwesties veroorzaakten wanneer het gebruiken van standaardinventarismontages voor het beheren van voorraad.<!--MAGECLOUD-4428-->!&lbrack;

   - ![ fixpictogram ](../../assets/fix.svg) **Achterwaartse Verenigbaarheid van nieuwe Interfaces van de Post** - lost een achterwaartse onverenigbaarheidskwestie op die door de `Magento\Framework\Mail\EmailMessageInterface` PHP interface wordt veroorzaakt die in Adobe Commerce v2.3.3 wordt geïntroduceerd. In het bereik van deze patch zijn de nieuwe `EmailMessageInterface` overervingen van de oude `MessageInterface` en zijn Adobe Commerce-kernmodules weer afhankelijk van `MessageInterface` . <!--MAGECLOUD-4422-->

   - &rbrack;(../../assets/fix.svg) **de paginering van de Catalogus van 0&rbrace; bevestigt pictogram &lbrace;niet aan Elasticsearch 6.x** - lost een kritieke kwestie met de paginering van het onderzoeksresultaat op die klanten gebruikend Elasticsearch 6.x als motor van het catalogusonderzoek.<!--MAGECLOUD-4448-->!&lbrack;

## v2002.0.21

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Dokker** -

   - ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe Beelden van de Docker** - gesteund door versies 2.3.3 en later <!-- MAGECLOUD-3345 -->

      - PHP versie 7.3.<!-- MAGECLOUD-4017 -->

      - Varnish Cache 6.2.0 <!-- MAGECLOUD-4017 -->

   - ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun om de configuratie van de douanehaak toe te passen die in `.magento.app.yaml` in het milieu van het Dok wordt gespecificeerd. Eerder, steunde het milieu van de Dokker slechts de standaardhakenconfiguratie.<!-- MAGECLOUD-3505-->

   - ![ de nieuwe pictogrammen ](../../assets/new.svg) de dossiers van ENV van de Dokker worden niet meer geproduceerd tijdens de Bouwstijl van het Dock, en het `docker:config:convert` bevel wordt afgekeurd. De bijbehorende gegevens worden nu opgeslagen in het `docker-compose.yml` -bestand. <!-- MAGECLOUD-3816-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Bijgewerkt PHP beeld** - Toegevoegde Node.js aan het PHP beeld van de Dakker om knoop, npm, en knijpmachine mogelijkheden te steunen.<!-- MAGECLOUD-3953 -->

- ![ nieuwe pictogram ](../../assets/new.svg) **veranderlijke updates van het Milieu** -

   - ![ nieuw pictogram ](../../assets/new.svg) voegde **LOCK_PROVIDER** variabele op om de slotleverancier te vormen die de lancering van dubbele kroonbanen en gewassengroepen verhindert. Zie de veranderlijke beschrijving in [ variabelen ](../environment/variables-deploy.md#lock_provider) onderwerp opstellen.<!-- MAGECLOUD-4052 -->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde de **CONSUMERS_WAIT_FOR_MAX_MESSAGES** omgevingsvariabele toe om te vormen hoe de consumenten berichten van de berichtrij verwerken wanneer het gebruiken van de `CRON_CONSUMERS_RUNNER` milieuvariabele om banen te beheren. Zie de veranderlijke beschrijving in [ variabelen ](../environment/variables-deploy.md#consumers_wait_for_max_messages) onderwerp opstellen.<!-- MAGECLOUD-4071 -->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die de fouten van de gegevensbestandblokkering kan veroorzaken wanneer de `consumers_runner` bouwbaanbegin veelvoudige instanties van de zelfde consument op verschillende knopen. Nu, als u [**CRON_CONSUMERS_RUNNER**](../environment/variables-deploy.md#cron_consumers_runner) hebt toegelaten stel variabele in uw milieu op, gebruikt de `consumers_runner` baan de `single-thread` optie om één geval van elke consument op slechts één knoop te beginnen.<!-- MAGECLOUD-3913 -->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) functionaliteit beïnvloedde die een standaard opslag URL gebruikt. Nu, als het `config:show:default-url` bevel geen basis URL kan halen, dan wordt URL van de variabele MAGENTO_CLOUD_ROUTES gebruikt.<!-- MAGECLOUD-3866 -->

- ![ nieuw pictogram ](../../assets/new.svg) werkte de registrereninformatie bij die door het `module:refresh` bevel werd teruggekeerd. Nu, kunt u een gedetailleerde lijst van toegelaten modules in het `cloud.log` dossier zien.<!-- MAGECLOUD-2514 -->

- ![ nieuw pictogram ](../../assets/new.svg) Verbeterde bevestiging en waarschuwingsberichten van de versiecompatibiliteit voor verenigbaarheidskwesties tussen de versie van Adobe Commerce en de geïnstalleerde diensten, zoals Elasticsearch, [!DNL RabbitMQ], Redis, en OB.<!-- MAGECLOUD-3535 -->

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor versie 3.8 RabitMQ.<!-- MAGECLOUD-4674-->

- ![ nieuw pictogram ](../../assets/new.svg) Bijgewerkte interactieve bevestigingen voor de dienstverenigbaarheid om op gesteunde versies voor nieuwe versies van Adobe Commerce 2.3.3 en 2.2.10 te wijzen. Zie {de vereisten van het 0} Systeem &rbrack;(https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements) in de _gids van de Installatie_ voor geadviseerde versies.<!-- MAGECLOUD-4018 -->&lbrack;

- ![ bevestig pictogram ](../../assets/fix.svg) verbeterde het logboekbericht teruggekeerd wanneer het proces van het baanbeheer van de cron in opstellen fase probeert om een hulpbaan te stoppen die reeds heeft gebeëindigd om te verduidelijken dat deze kwestie geen fout is. Veranderde het logboekniveau van `INFO` in `DEBUG`.<!-- MAGECLOUD-3653-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie wanneer het runnen van het `setup:upgrade` bevel dat het plaatsingsproces niet onderbreekt wanneer een mislukking tijdens de `app:config:import` taak voorkwam.<!-- MAGECLOUD-3806 -->

- ![ nieuw pictogram ](../../assets/new.svg) veranderde het standaardlogboekniveau voor de dossiermanager aan `debug` om de hoeveelheid detail in het logboek te verminderen dat in [!DNL Cloud Console] wordt getoond, terwijl nog het verstrekken van gedetailleerde informatie voor het zuiveren.<!-- MAGECLOUD-3871 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die een fout met statische inhoudsplaatsing tijdens bouwstijl veroorzaakte. Na een installatie en `ece-tools` config-dump is een fout opgetreden als er geen landinstelling is opgegeven voor de beheerder gebruiker in het `config.php` -bestand. Er staat nu een standaardlandinstelling voor de gebruiker van de beheerder in het `config.php` -bestand. <!-- MAGECLOUD-3957 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een `Undefined index error` dat voorkomt wanneer een `magento-cloud` bevel CLI in een milieu ontbreekt dat niet met een veilige URL (https) wordt gevormd. Nu gebruikt het ECE-Tools-pakket de basis-URL (http) als de beveiligde URL niet beschikbaar is.<!-- MAGECLOUD-4009 -->

## v2002.0.20

- ![ nieuw pictogram ](../../assets/new.svg) **de Updates van de Docker** -

   - ![ nieuw pictogram ](../../assets/new.svg) U kunt functioneel het testen nu uitvoeren gebruikend het `ece-tools` pakket in het milieu van het Dok. Zie [ toepassing het testen ](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/).<!-- MAGECLOUD-3129/3684 -->

   - ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor het vormen PHP modules gebruikend het `.magento.app.yaml` dossier. Om het even welke [ PHP Uitbreidingen die in het `.magento.app.yaml` dossier ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/app/php-settings#enable-extensions) worden gespecificeerd worden beschikbaar in de containers PHP van de Dokker.<!-- MAGECLOUD-3357 -->

   - ![ nieuw pictogram ](../../assets/new.svg) Er zijn nieuwe bevelen beschikbaar om de ervaring van de het bevellijn van het Docker te verbeteren. Zie de [`bin/magento-docker` sectie van de verwijzing van de Dokker ](https://developer.adobe.com/commerce/cloud-tools/docker/quick-reference/#cloud-docker-cli).<!-- MAGECLOUD-3569 -->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde de capaciteit toe om Mutagen.io te gebruiken om dossiers tijdens ontwikkeling tussen de lokale gastheer en Docker te synchroniseren.<!-- MAGECLOUD-3559 -->

   - ![ fixpictogram ](../../assets/fix.svg) Correcteerde de standaardweg wanneer het gebruiken van het milieu van de Dok. Nu, wanneer u SSH aan login aan de container van het Dok gebruikt, bent u bij de projectwortel in de `/app` folder, zoals verwacht.<!-- MAGECLOUD-3582 -->

   - ![ fixpictogram ](../../assets/fix.svg) werkte de bibliotheek van Natrium van versie 1.0.11 aan versie 1.0.18 bij, en werkte de Natriumuitbreiding PHP bij.<!-- MAGECLOUD-3832 -->

     >[!WARNING]
     >
     >Adobe Commerce op klanten van de wolkeninfrastructuur moet [ een kaartje van de Steun van Adobe Commerce ](https://support.magento.com/hc/en-us/articles/360000913794#submit-ticket) voorleggen om het bibliotheekpakket op ProProductie en het Opvoeren milieu&#39;s te bevorderen voorafgaand aan bevordering aan Adobe Commerce 2.3.2. U kunt momenteel geen upgrade uitvoeren van Starter-omgevingen naar Adobe Commerce 2.3.2.

   - ![ fixpictogram ](../../assets/fix.svg) voegde `analysis-icu` en de `analysis-phonetic` Elasticsearch stop- ins aan alle beelden van het Dok toe.<!-- MAGECLOUD-3446 -->

   - ![ fixpictogram ](../../assets/fix.svg) Verbeterde bevestigingen: Wanneer het gebruiken van opties voor het `docker:build` bevel, moet u een waarde verstrekken wanneer het gebruiken van een optie. Voeg ook validatie toe voor de Node-versie wanneer u de opdracht `docker:build run` gebruikt. <!-- MAGECLOUD-3486 & MAGECLOUD-3678 -->

- ![ nieuw pictogram ](../../assets/new.svg) **veranderlijke updates van het Milieu** -

   - ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor de prefixen van de gegevensbestandlijst gebruikend [ DATABASE_CONFIGURATION milieuvariabele ](../environment/variables-deploy.md#database_configuration).<!-- MAGECLOUD-2901 -->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde **FORCE_UPDATE_URLS** variabele op om basis URLs bij te werken wanneer het opstellen aan Pro en de productie en het opvoeren van de Starter milieu&#39;s. Zie de definitie in [ variabelen ](../environment/variables-deploy.md#force_update_urls) inhoud opstellen.<!-- MAGECLOUD-3602 -->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde **TTFB_TESTED_PAGES** toe post-stel variabele om _Tijd aan Eerste de paginatietests van de Byte_ te vormen om toepassingsprestaties op plaatsen te controleren die aan de infrastructuur van de Wolk worden opgesteld. Zie de veranderlijke beschrijving in [ post-opstelt variabelen ](../environment/variables-post-deploy.md).<!-- MAGECLOUD-3643 -->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie met multi-threaded SCD, die willekeurige mislukkingen in statische inhoudsplaatsing veroorzaakte. De alternerende actie impliceerde het plaatsen van **SCD_THREADS** variabele aan `1`. U kunt nu het aantal verhogen wanneer dat nodig is. Zie de definities in [ variabelen ](../environment/variables-deploy.md#scd_threads) opstellen en [ variabelen ](../environment/variables-build.md#scd_threads) bouwen.<!-- MAGECLOUD-3611 -->

   - ![ herstellingspictogram ](../../assets/fix.svg) U kunt **WARM_UP_PAGES** omgevingsvariabele vormen om enige pagina&#39;s, veelvoudige domeinen, en veelvoudige pagina&#39;s in het voorgeheugen onder te brengen. Zie de uitgebreide definitie in [ post-opstelt variabelen ](../environment/variables-post-deploy.md#warm_up_pages) inhoud.<!-- MAGECLOUD-3258 -->

- ![ fixpictogram ](../../assets/fix.svg) voegde het `pub/static/.htaccess` dossier aan de uitsluitingslijst toe. [ Fix die door Björn Kraus van PHOENIX MEDIA GmbH ](https://github.com/magento/ece-tools/pull/455) wordt voorgelegd.<!-- MAGECLOUD-3545/Github#455 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een fout wanneer alle bevestigingsberichten als `Critical` werden getoond als minstens één kritieke niveauvalidator een fout terugkeerde.<!-- MAGECLOUD-3178 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die een plaatsingsmislukking veroorzaakte als basis URL niet in het gegevensbestand bestond.<!-- MAGECLOUD-3075 -->

- ![ nieuw pictogram ](../../assets/new.svg) voegde een nieuw **`env:config:show`bevel** aan het `ece-tools` pakket toe dat de omgevingsdiensten, routes, of variabelen toont. Zie [ Diensten, routes, en variabelen ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/ece-tools/package-overview#services-routes-and-variables). [ Eigenschap die door Vladimir Kerkhoff ](https://github.com/magento/ece-tools/pull/486) wordt voorgelegd.<!-- MAGECLOUD-3451 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die een kritieke fout wanneer het proberen om Adobe Commerce 2.2.6 te installeren of vroeger met `ece-tools` ontwikkelden na shell refactoring veroorzaakte.<!-- MAGECLOUD-3665 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die Adobe Commerce 2.1.x en 2.2.x installaties veroorzaakte om met een waarschuwing te ontbreken over het gebruiken van een verouderde versie van Koolstof.<!-- MAGECLOUD-3704 -->

- ![ fixpictogram ](../../assets/fix.svg) verlaagde het `cloud.log` logboekniveau voor shell output van `info` aan `debug`.<!-- MAGECLOUD-3277 -->

- ![ fixpictogram ](../../assets/fix.svg) voegde de `--remove-definers (-d)` optie aan het `ece-tools db-dump` bevel toe om definities uit het stortplaatsdossier te verwijderen.<!-- MAGECLOUD-3510 -->

## v2002.0.19

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die het `env.php` dossier tijdens opstelt, resulterend in een verlies van douaneconfiguraties. Deze update zorgt ervoor dat Adobe Commerce op de cloudinfrastructuur het `env.php` -bestand bij elke implementatie bijwerkt, terwijl aangepaste configuraties behouden blijven. <!-- MAGECLOUD-3668 -->

## v2002.0.18

- ![ nieuw pictogram ](../../assets/new.svg) **de Updates van de Docker** -

   - ![ nieuw pictogram ](../../assets/new.svg) nu, steunt het milieu van de Dokker de kanonconfiguratie die in het [ wordt bepaald krons bezit van het.magento.app.yaml- dossier ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/app/properties/crons-property).<!-- MAGECLOUD-3150 -->

   - ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe Container van de Docker** - Toegevoegd a [ TLS de container van de beëindigingsvolmacht ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#varnish-container) om de Varnish SSL beëindiging over HTTPS te vergemakkelijken.<!-- MAGECLOUD-2890 -->

   - ![ nieuw pictogram ](../../assets/new.svg) **Nieuw Beeld van de Docker** - voegde een beeld Node.js toe om Gulp en andere mogelijkheden, zoals het Testen van de Eenheid JS van Jasmine te steunen JS.<!-- MAGECLOUD-3345 -->

   - ![ nieuw pictogram ](../../assets/new.svg) **Docker bouwt wijzen** - nu kunt u verkiezen om het milieu van de Docker op [ wijze van de Productie of wijze van de Ontwikkelaar ](https://developer.adobe.com/commerce/cloud-tools/docker/deploy/#launch-mode) te lanceren. De wijze van de ontwikkelaar steunt actieve ontwikkeling met volledige, schrijfbare filesystem toestemmingen.<!-- MAGECLOUD-3152/3511 -->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die de opstelling van de Docker veroorzaakte om met a `Name or service not known` fout te ontbreken als het geheime voorgeheugen voor de dienst wordt gevormd die niet beschikbaar is. Nu, kunt u de dienst uit het [`.magento/services.yaml` dossier ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/service/services-yaml) verwijderen. De de configuratiegenerator van de Dokker werkt de dienst in het `docker/config.php.dist` dossier automatisch bij.<!-- MAGECLOUD-3369 -->

   - ![ nieuw pictogram ](../../assets/new.svg) toegevoegde interactieve bevestigingen voor de dienstverenigbaarheid. Nu, als een gevraagde dienst met de versie van Adobe Commerce of andere diensten onverenigbaar is, veroorzaakt de _interactieve wijze_ de gebruiker met een bericht en een keus om verder te gaan. Zie de [ versies van de Dienst ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/#service-containers) beschikbaar voor Docker. Gebruik de optie `-n` om de interactiviteit voor CICD-doeleinden over te slaan.<!-- MAGECLOUD-3251 -->

   - ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie met Docker stelt `db-dump` bevel samen dat bestaande dumps wist.<!-- MAGECLOUD-3366 -->

   - ![ fixpictogram ](../../assets/fix.svg) Vloedigde een kwestie die Redis `session`, `default`, en `page_cache` geheim voorgeheugenopslag aan zelfde gegevensbestand identiteitskaart <!-- MAGECLOUD-3172 --> toewees.

- ![ nieuw pictogram ](../../assets/new.svg) **veranderlijke updates van het Milieu** -

   - ![ nieuw pictogram ](../../assets/new.svg) de nieuwe **ELASTICSUITE \_CONFIGURATION** milieuvariabele behoudt uw aangepaste de dienstmontages tussen plaatsingen. Zie de definitie in [ variabelen ](../environment/variables-deploy.md#elasticsuite_configuration) inhoud opstellen.<!-- MAGECLOUD-3205 -->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde **SCD_MAX_EXECUTION_TIMEOUT** milieuvariabele toe zodat kunt u de tijd verhogen om de statische inhoudsplaatsing van het `.magento.env.yaml` dossier te voltooien. Zie de definitie in [ variabelen ](../environment/variables-deploy.md#scd_max_execution_time) opstellen, [ variabelen ](../environment/variables-build.md#scd_max_execution_time) bouwen, en [ globale variabelen ](../environment/variables-global.md#scd_max_execution_time).<!-- MAGECLOUD-2822 -->

      - ![ nieuw pictogram ](../../assets/new.svg) voegde de **MAGENTO_CLOUD_LOCKS_DIR** milieuvariabele toe om de weg aan het koppelingspunt voor de slotleverancier op de wolkeninfrastructuur te vormen. De vergrendelingsprovider voorkomt het starten van dubbele snijtaken en afdekgroepen. Deze variabele wordt ondersteund op Adobe Commerce versie 2.2.5 en hoger en automatisch geconfigureerd. Zie de definitie in [ variabelen van de Wolk ](../environment/variables-cloud.md).<!-- MAGECLOUD-3135 -->

      - ![ fixpictogram ](../../assets/fix.svg) veranderde **SCD_THREADS** milieu veranderlijke standaardwaarden om de optimale waarde automatisch te bepalen die op de ontdekte de draadtelling van CPU wordt gebaseerd. Zie de bijgewerkte definities in [ variabelen ](../environment/variables-deploy.md#scd_threads) opstellen en [ variabelen ](../environment/variables-build.md#scd_threads) bouwen.<!-- MAGECLOUD-3382 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie met een flard voor het Mechanisme van de Isolatie van OB dat een fout toen het bevorderen aan Adobe Commerce op versie 2002.0.16 van de wolkeninfrastructuur veroorzaakte.<!-- MAGECLOUD-3383 -->

- ![ fixpictogram ](../../assets/fix.svg) voegde een flard toe die _de Grafieken van het Beeld van Google_ met _beeld-Grafieken_ vervangt. Zie het DevBlog artikel [ afschrijving en update van de Grafieken van het Beeld van Google voor M1 ](https://community.magento.com/t5/Magento-DevBlog/Google-Image-Charts-deprecation-and-update-for-M1/ba-p/125006).<!-- MAGECLOUD-3456 -->

- ![ fixpictogram ](../../assets/fix.svg) Toegevoegde bevestiging voor de [ variabele SEARCH_CONFIGURATION ](../environment/variables-deploy.md#search_configuration). Implementatie mislukt als de optie &#39;engine&#39; niet is ingesteld en `_merge` niet is vereist.<!-- MAGECLOUD-3470 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die gevoelige gegevens nadat een uitzondering voorkomt blootstelde. Nu wordt de gevoelige informatie geschikt gemaskeerd.<!-- MAGECLOUD-3525 -->

- ![ fixpictogram ](../../assets/fix.svg) verbeterde de fout-verdraagzame montages van het pakket van de Magento Open Source. Als Adobe Commerce geen gegevens kan lezen van de instantie Redis `slave` , wordt een waarde gelezen van de instantie Redis `master` . Zie [ REDIS_USE_SLAVE_CONNECTION ](../environment/variables-deploy.md#redis_use_slave_connection).<!-- MAGECLOUD-2899 -->

## v2002.0.17

>[!NOTE]
>
>De `ece-tools` versie 2002.0.17 bevat een belangrijke beveiligingspatch. Zie [ Middelen van de Tech: De Patches van de Magento Open Source ](https://magento.com/tech-resources/download#download2288).

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Dienst** - gesteund door de volgende versies van Adobe Commerce: 2.2.8 en later 2.2.x, 2.3.1 en later 2.3.x

   - Toegevoegde steun voor versie 6.x van de Elasticsearch.<!-- MAGECLOUD-3196 -->

   - Toegevoegde ondersteuning voor Redis versie 5.0.

- ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe beelden van het Dock** - voegde de volgende diensten aan het Docker toe bouwt:

   - Elasticsearch 6.5 <!-- MAGECLOUD-3196 -->

   - Redis 5.0 <!-- MAGECLOUD-3223 -->

- ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe milieu variabele** - eerder, was er een hard-gecodeerde onderbreking voor compressie SCD. Nu kunt u de compressieonderbreking vormen SCD gebruikend **SCD_COMPRESSION_TIMEOUT** milieuvariabele. Zie de definities in [ variabelen bouwen ](../environment/variables-build.md#scd_compression_timeout) en [ variabelen ](../environment/variables-deploy.md#scd_compression_timeout) inhoud opstellen.<!-- MAGECLOUD-2870 -->

- ![ fixpictogram ](../../assets/fix.svg) voegde de `--use-rewrites` optie aan toe installeert bevel zodat het Webserver herschrijft voor geproduceerde verbindingen in de storefront en toegang Admin om veiligheid en klantenervaring te verbeteren.<!-- MAGECLOUD-3246 -->

- ![ fixpictogram ](../../assets/fix.svg) Toegevoegde timestamps aan het `var/log/install_upgrade.log` dossier zodat het data voor installatie en verbeteringsgebeurtenissen toont.<!-- MAGECLOUD-2895 -->

## v2002.0.16

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Dokker** -

   - Nu, is de standaarddienstconfiguratie die in het milieu van de Dokker wordt geproduceerd het zelfde als de standaardconfiguratie in het malplaatje van de Wolk.<!-- MAGECLOUD-3025 -->

   - U kunt post van uw milieu van de Dokker verzenden gebruikend de `sendmail` dienst.<!-- MAGECLOUD-2907 -->

   - Toegevoegd de capaciteit om [ Xdebug ](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/) te vormen om in het milieu van het Dok van de Wolk te zuiveren.<!-- MAGECLOUD-2891 -->

   - Probleem verholpen met webservicerechten tijdens het genereren van het `docker-compose.yml` -bestand. <!-- MAGECLOUD-2883 -->

- ![ nieuw pictogram ](../../assets/new.svg) **verbetering van de Verbetering** - Toegevoegde bevestiging om te bevestigen dat het `autoload` bezit in het `composer.json` dossier vereiste configuratieveranderingen bevat alvorens aan Adobe Commerce v2.3 te bevorderen. Zie [ versie van de Verbetering ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/upgrade/commerce-version).<!-- MAGECLOUD-2392 -->

- ![ nieuw pictogram ](../../assets/new.svg) het compressieproces in het opstellen van statische inhoud omvat nu alle activa-nefast geproduceerd of aangepast-en komt tijdens de bouwstijlfase bij het begin van de [`build:transfer` sectie ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/app/properties/hooks-property) voor. Eerder was het compressieproces vóór het toepassen van aangepaste minificatie en bundeling van statische elementen. [ Fix die door Rafael Garcia Lepper van Tryzens Limited ](https://github.com/magento/ece-tools/pull/413) wordt voorgelegd.<!-- MAGECLOUD-3104 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een fout van de gegevensbestandverbinding die tijdens plaatsing onmiddellijk na het vormen van een extra gegevensbestand en de dienstverhouding voorkwam. Bovendien verhelpt deze oplossing een probleem dat zich heeft voorgedaan tijdens het configuratieproces van Commerce Reporting for Starter. Voor de Starter, is deze verbetering &quot;moet&quot;hebben voor het gebruiken van de Rapportering van Commerce.<!-- MAGECLOUD-3035 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een bevestigingskwestie met de gegevensbestandconfiguratie die het opstellen proces om veroorzaakte te ontbreken.<!-- MAGECLOUD-3003 -->

- ![ fixpictogram ](../../assets/fix.svg) werkte de beperking met de aangewezen versie van het `symfony/yaml` pakket bij om met [ PHP constanten ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/env/configure-env-yaml#php-constants) te gebruiken. Constante het ontleden werkt niet wanneer het gebruiken van een `symfony/yaml` pakketversie vroeger dan 3.2. [ Repareren die door Vladimir Kerkhoff ](https://github.com/magento/ece-tools/pull/404) wordt voorgelegd.<!-- MAGECLOUD-2956 -->

- ![ nieuw pictogram ](../../assets/new.svg) **de configuratiecontrole van het Milieu** - Toegevoegde bevestiging om de PHP versie te controleren en gebruikers te waarschuwen als zij niet de recentste geadviseerde versie gebruiken.<!--MAGECLOUD-2903-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie met het verwerken van misvormde variabelen JSON. Nu, als een variabele JSON een syntaxisfout veroorzaakt, verschijnt een waarschuwing in het `cloud.log` dossier en de plaatsing blijft gebruikend de standaardvariabele.<!-- MAGECLOUD-2851 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een verbindingsfout die tijdens plaatsing onmiddellijk na het onbruikbaar maken van de dienst Redis voorkwam.<!-- MAGECLOUD-2747 -->

- ![ nieuw pictogram ](../../assets/new.svg) **het Registreren verandert** - bijgewerkt het [ logboekniveau ](../environment/log-handlers.md#log-levels) van `Info` aan `Notice` voor het volgende bouwt en stelt procesgebeurtenissen op:<!--MAGECLOUD-2925-->

   - Begin en einde van het proces om geïnstalleerde modules in `composer.json` te combineren met gedeelde configuratie-instellingen in het `app/etc/config.php` -bestand

   - Begin en eind van het configuratiebevestigingsproces

   - Begin en einde van het `setup:di:compile` -proces voor het genereren van klassen

- ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe omgevingsvariabelen** -

   - **[RESOURCE_CONFIGURATION stelt veranderlijk](../environment/variables-deploy.md#resource_configuration)** op - gebruik deze variabele om een middelnaam aan een gegevensbestandverbinding in kaart te brengen.<!-- MAGECLOUD-3026 & MAGECLOUD-2963-->

   - **[X_FRAME_CONFIGURATION globale variabele](../environment/variables-global.md#x_frame_configuration)** - gebruik deze variabele om de `X-Frame-Options` kopbalconfiguratie voor het teruggeven van een pagina van Adobe Commerce in a `<frame>`, `<iframe>`, of `<object>` te veranderen.<!-- MAGECLOUD-3048 -->

- ![&#128279;](../../assets/fix.svg) **veranderlijke updates van het Milieu 1&rbrace; fixpictogram** - veranderde de volgende milieuvariabelen:

   - **[WARM_UP_PAGES](../environment/variables-post-deploy.md)** - voegde het vermogen toe om het geheime voorgeheugen voor gespecificeerde pagina&#39;s op alle domeinen vooraf te laden die voor een opslag van Adobe Commerce worden bepaald. Eerder, als uw plaats met veelvoudige domeinen werd gevormd, kon het post-opstellen proces niet het geheime voorgeheugen voor de gespecificeerde pagina&#39;s op niet standaarddomeinen vooraf laden en de volgende fout in het post-opstellen logboek terugkeren: `ERROR: Warming up failed: <uri>`<!-- MAGECLOUD-2466 -->

   - **SCD_COMPRESSION_LEVEL** - werkte de documentatie en het steekproef `.magento.env.yaml` dossier met de correcte standaardwaarden voor SCD compressieniveau bij. Zie de definities in [ variabelen bouwen ](../environment/variables-build.md#scd_compression_level) en [ variabelen ](../environment/variables-deploy.md#scd_compression_level) inhoud opstellen.<!-- MAGECLOUD-2823 -->

   - **SCD_EXCLUDE_THEMES** - Deze omgevingsvariabele wordt afgekeurd. Gebruik [ SCD_MATRIX ](../environment/variables-build.md#scd_matrix) om themeconfiguratie te controleren.<!--MAGECLOUD-2882-->

   - **SCD \_MATRIX** - Vaste het bevestigingsproces om een probleem te verhinderen dat voorkwam wanneer SCD_MATRIX een themawaarde negeerde die verschillende karaktergevallen bevatte. Zie de definities in [ variabelen bouwen ](../environment/variables-build.md#scd_matrix) en [ variabelen ](../environment/variables-deploy.md#scd_matrix) inhoud opstellen.<!-- MAGECLOUD-2904 -->

   - **ADMIN variabelen** - <!-- MAGECLOUD-2573/MAGECLOUD-2848 -->

      - Verbeterde beveiliging bij het beheren van referenties voor de Admin-gebruiker met omgevingsvariabelen. U kunt de ADMIN_EMAIL, ADMIN_USERNAME, en ADMIN_PASSWORD milieuvariabelen niet meer gebruiken om admin geloofsbrieven tijdens verbeteringen met voeten te treden. Als u niet tot het Admin paneel kunt toegang hebben, gebruik _vergeten wachtwoordeigenschap_ of het `admin:user:create` bevel CLI om een nieuwe admin gebruiker tot stand te brengen. Zie [ Toegang tot uw Admin paneel ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/onboarding#admin).

      - ADMIN_EMAIL is niet meer vereist wanneer u patches upgradet of toepast.

## v2002.0.15

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Dokker** -

   - Nu gebruikt de generator van de Dokker de diensten die in `.magento.app.yaml` worden gespecificeerd en `.magento/services.yaml` configuratiedossiers wanneer [ bouwend uw milieu van de Dokker ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/). U kunt een verschillende de dienstversie kiezen gebruikend bouwstijlparameters.<!-- MAGECLOUD-2888 -->

   - Toegevoegde PHP 7.2 beeld-Toegevoegde steun voor PHP 7.2 in het Dok van de Wolk; werkte de [ configuratie van het Docker van de Lancering ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/) bij om de `docker:build --php` optie te omvatten om de versie van PHP compatibel met uw versie van Adobe Commerce te specificeren.<!-- MAGECLOUD-2799 -->

   - Toegevoegde container van het a [ Gewas ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/cli/#cron-container) die op het PHP-CLI beeld wordt gebaseerd.<!-- MAGECLOUD-2565 -->

   - De volgende services zijn toegevoegd aan de Docker-build:

      - [!DNL RabbitMQ] 3.5 en 3.7 <!-- MAGECLOUD-2567 & 2889-->

      - Elasticsearch 1.7, 2.4, en 5.2 <!-- MAGECLOUD-2569 & 2887 -->

      - Redis 3.2 en 4.0 <!-- MAGECLOUD-2886 -->

- ![ nieuw pictogram ](../../assets/new.svg) **vormt met PHP constanten** - Toegevoegde steun voor [ PHP constanten ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/env/configure-env-yaml#php-constants) in het `.magento.env.yaml` configuratiedossier.<!-- MAGECLOUD- 2575 -->

- ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe milieu variabele** - door gebrek, slechts heeft het milieu van de Productie toegelaten Googles Analytics. U kunt Googles Analytics op de het Opvoeren en milieu&#39;s van de Integratie toelaten gebruikend [ ENABLE_GOOGLE_ANALYTICS omgevingsvariabele ](../environment/variables-deploy.md#enable_google_analytics).<!--MAGECLOUD-2879-->

- ![ bevestig pictogram ](../../assets/fix.svg) een kwestie die aangepaste kroonconfiguraties van het `env.php` dossier na een herplaatsing verwijderde. Aangepaste uitsnijdconfiguraties blijven nu veilig in het `env.php` -bestand staan. <!-- MAGECLOUD-2923 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste inconsistenties in de berichten en [ logboekniveaus ](../environment/log-handlers.md#log-levels) voor bouw, stel, en post-opstelt fasen op. Verhoogde het beginnen en beëindigende niveaus van het logboekbericht van **info** aan **bericht** voor alle fasen en subfasen. Toegevoegde begin en beëindigende logboekberichten, waar aangewezen.<!-- MAGECLOUD-2919 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die gewassenprocessen impliceerde die het begin van de post-opstellen fase, toen gevormd verhinderden. Nu, als u de post-opstellen toegelaten haak hebt, worden de kroonprocessen opnieuw toegelaten aan het begin van de post-opstellen fase.<!-- MAGECLOUD-2862 -->

- ![ fixpictogram ](../../assets/fix.svg) loste een kwestie op die een succesvolle installatie van Adobe Commerce verhinderde toen het specificeren van een configuratie van het douanegegevensbestand. Eerder, gebruikte het installatieproces de gegevensbestandconfiguratie van de [ variabele MAGENTO_CLOUD_RELATIONSHIP ](../environment/variables-cloud.md) zelfs als u aangepaste verbindingsinformatie in [ DATABASE_CONFIGURATION milieuvariabele ](../environment/variables-deploy.md#database_configuration) aangewezen.<!--MAGECLOUD-2736-->

- ![ fixpictogram ](../../assets/fix.svg) corrigeerde het `config:dump` bevel zodat het elke websitescène in de `system` sectie van het `config.php` dossier omvat.<!--MAGECLOUD-2740-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die in _opwarmings_ fouten tijdens de post-opstellings fase resulteerde door de bronURL verwijzing te verbeteren.<!--MAGECLOUD-2797-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die dossiers incorrect tijdens het `setup:di:compile` proces produceerde, die de module van het Betalen van Amazon beïnvloedde.<!--MAGECLOUD-2850-->

## v2002.0.14

- ![ nieuw pictogram ](../../assets/new.svg) **verifieer Ideale Staat** - de `ideal-state` tovenaar verifieert nu de huidige configuratie tijdens elke plaatsing en verstrekt duidelijke instructies voor het bijwerken van de configuratie om een snellere, nul-onderbreking plaatsing te bereiken.<!--MAGECLOUD-2372-->

- ![ fixpictogram ](../../assets/fix.svg) **PCI Naleving** - werkte de overseinenprotocollen voor Adobe Commerce op wolkeninfrastructuur bij om versie 1.2 van de Veiligheid van de Laag van het Vervoer (TLS) te vereisen wanneer het verbinden met de diensten van het derdenoverseinen. Als u een berichtservice gebruikt die geen ondersteuning biedt voor TLS versie 1.2, moet u een upgrade uitvoeren op uw service. Anders wordt het volgende foutbericht weergegeven wanneer uw Adobe Commerce-toepassing verbinding probeert te maken met de berichtserver om een e-mail te verzenden: `Unable to connect via TLS`. <!--MAGECLOUD-2521-->

- ![ nieuw pictogram ](../../assets/new.svg) **de verbetering van de Plaatsing** - Toegevoegde bevestiging om klanten te waarschuwen als een het Opvoeren of milieu van de Productie `dev` heeft, `debug`, of `debug_logging` toegelaten opties om prestatieskwesties te verhinderen die door bovenmatige registrerenactiviteit worden veroorzaakt.<!--MAGECLOUD-2517-->

- ![&#128279;](../../assets/fix.svg) **moeilijke situaties van de Plaatsing 0&rbrace; fixpictogram** -

   - Nu wordt de onderhoudswijze toegelaten bij het begin van de opstellen fase en gehandicapt aan het eind. Als de plaatsing ontbreekt, blijft de plaats op onderhoudswijze tot de plaatsingskwesties worden opgelost. Eerder, keerde de plaats aan productiemodus terug zelfs als de plaatsing ontbrak.<!--MAGECLOUD-2603-->

      - Herwerkte de controles van de plaatsingsfasbevestiging om het foutenniveau voor de volgende plaatsingskwesties van `CRITICAL` aan `WARNING` te verlagen zodat de plaatsing voltooit. Deze problemen hebben er eerder toe geleid dat de implementatie is mislukt.

      - De configuratie van het milieu bevat onjuiste waarden voor opstelling of wolkenvariabelen.

   - De versie van de Elasticsearch op de cloudinfrastructuur is niet compatibel met de versie van de elasticsearch/elasticsearch module die door Adobe Commerce wordt ondersteund op de cloudinfrastructuur. Zie het [ het oplossen van problemenartikel van de Elasticsearch ](https://support.magento.com/hc/en-us/articles/360015758471-Deployment-fails-or-interrupts-with-cloud-log-error-Elasticsearch-version-is-not-compatible-with-current-version-of-magento) in de Kennisbank van de Steun van Adobe Commerce.<!--MAGECLOUD-2600-->

   - Probleem verholpen met de gedeelde configuratie-instellingen in het `app/etc/config.php` -bestand dat `recursion detected` fouten tijdens de implementatie veroorzaakte. <!--MAGECLOUD-2173-->

- ![ het pictogram van de moeilijke situatie ](../../assets/fix.svg) **op elkaar betrekking hebbende moeilijke situaties**—

   - Oplossing een bouwsteen die kwestie die banen verhinderde te lopen als u een gewassenfrequentie buiten het gebrek (1 minuut) specificeert.<!--MAGECLOUD-2602-->

   - Probleem verholpen in de implementatiefase die ervoor zorgde dat cron-taken tijdens de implementatie konden worden uitgevoerd, wat databasestlokken en andere kritieke problemen kan veroorzaken. Nu, worden alle kroonbanen tegengehouden alvorens de opstellen fase begint en opnieuw begonnen nadat de plaatsing voltooit.&lt;!—MAGECLOUD—2537—>

   - Oplossing voor de werkstroom voor uitsnijden in versie 2.2.x om bevroren uitsnijdtaken te ontgrendelen zodat deze kunnen worden gestopt voordat de implementatie wordt gestart. Eerder, veroorzaakte een bevroren kroonbaan de plaatsing om te stagneren.<!--MAGECLOUD-2501-->

- ![ fixpictogram ](../../assets/fix.svg) veranderde het formaat van het `config.php` dossier dat door het `vendor/bin/ece-tools config:dump` bevel wordt geproduceerd om korte seriesyntaxis en 4-ruimteinspringing te gebruiken om aan de coderingsnormen van Adobe Commerce te voldoen.<!--MAGECLOUD-2527-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een plaatsingsfout die voorkomt wanneer `.magento.env.yaml` `{{ base_url }}` en `{{ unsecure_base_url }}` placeholders voor Webconfiguraties in plaats van de standaardURL configuratie voor een Adobe Commerce op het project van de wolkeninfrastructuur bevat./<!--MAGECLOUD-2607-->

## v2002.0.13

- ![ nieuw pictogram ](../../assets/new.svg) **laat nul-onderbreking plaatsing** toe - nu Adobe Commerce op de rijen van de wolkeninfrastructuur verzoeken met vereiste gegevensbestandveranderingen tijdens plaatsing en past de veranderingen toe zodra de plaatsing voltooit. Verzoeken kunnen maximaal 5 minuten worden bewaard om ervoor te zorgen dat geen sessies verloren gaan. Zie [ Statische opties van de inhoudsplaatsing om plaatsing onderbreking op Wolk ](https://support.magento.com/hc/en-us/articles/360004861194-Static-content-deployment-options-to-reduce-deployment-downtime-on-Cloud) te verminderen.<!--MAGECLOUD-2169-->

- ![ nieuw pictogram ](../../assets/new.svg) **Samenstellen van de Teller voor wolk** - maakte de volgende verbeteringen in de [ opstelling en de configuratieproces van de Dokker ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/):

   - Toegevoegd een bevel— `docker:config:convert` om PHP configuratiedossiers in formaat om te zetten Docker ENV om omgevingsconfiguratie te vereenvoudigen. Nu kopieert u de PHP-configuratiebestanden naar de Docker-map en zet u ze om in Docker ENV-bestanden. Zie [ Docker van de Lancering ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/).<!--MAGECLOUD-2359-->

   - Het installatieproces van Adobe Commerce on cloud Infrastructure ondersteunt nu de implementatie op zowel read-only- als read-write-bestandssystemen om het Cloud-bestandssysteem beter te emuleren. Zie [ Docker ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/) vormen.&lt;!—MAGECLOUD—2357—>

   - **Redis de dienststeun** - voegde een beeld Redis toe, dat aan een container van het Dok wordt opgesteld en automatisch wordt gevormd om met uw installatie van het Docker te werken.&lt;!—MAGECLOUD—2442—>

   - Nu hebt u het vermogen van de stortplaats van DB wanneer het gebruiken van de Dok van de Wolk [ gegevensbestandcontainer ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#database-container). Ook, kunt u dossiers &rbrack;(https://developer.adobe.com/commerce/cloud-tools/docker/containers/#sharing-data-between-host-machine-and-container) tussen een gastheermachine en een container delen gebruikend de `docker/mnt` folder.<!-- MAGECLOUD-2577 -->&lbrack;

   - **de dienststeun van Varnish** - voegde een beeld van Varnish toe, dat automatisch aan een container van de Dok wordt opgesteld. Na plaatsing, kunt u Varnish na de beste praktijken van Adobe Commerce manueel vormen. Zie [ vormen en gebruiken Vierkant ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cache/varnish/config-varnish).&lt;!—MAGECLOUD—2358—>

   - Toegang tot de site beveiligen—Toegevoegde SSL-ondersteuning voor toegang tot uw Adobe Commerce-winkel en het deelvenster Beheer.&lt;!—MAGECLOUD—2360—>

- ![ fixpictogram ](../../assets/fix.svg) **Verbeterde Adobe Commerce op de uitbreidingssteun van de wolkeninfrastructuur** - Gedowngraded de minimumversievereiste voor het guzzlehttp/guzzle pakket in Adobe Commerce op het dossier van de wolkeninfrastructuur [ composer.json ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/overview) aan versie 6.2 zodat het `ece-tools` pakket met meer uitbreidingen compatibel is.<!--MAGECLOUD-2205-->

- ![ nieuw pictogram ](../../assets/new.svg) **pas douaneveranderingen in uw toepassing van Adobe Commerce tijdens bouwstijlfase** toe - wij verdelen de bouwstijlfase in twee afzonderlijke processen zodat u haken kunt gebruiken om douaneveranderingen op de geproduceerde statische inhoud toe te passen alvorens de toepassing voor plaatsing te verpakken. _bouwt:produceert_ proces produceert code, past flarden toe, en produceert statische inhoud. _bouwt voort:overdracht_ proces brengt de geproduceerde code en statische inhoud aan de definitieve bestemming over. Zie [ de haken van de Toepassing ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/app/properties/hooks-property).<!--MAGECLOUD-2363-->

- ![&#128279;](../../assets/fix.svg) **de configuratiecontroles van het Milieu 1&rbrace;  bevestigen pictogram** - Verbeterde bevestiging van de milieuconfiguratie om klanten over versionverenigbaarheden en configuratiefouten te waarschuwen alvorens Adobe Commerce op wolkeninfrastructuur te bouwen en op te stellen.

   - Toegevoegde versie-specifieke bevestiging om niet gestaafde of verouderde omgevingsvariabelen en waarden te identificeren.<!--MAGECLOUD-2183-->

   - Er is een compatibiliteitscontrole voor Elasticsearch toegevoegd om gebruikers te waarschuwen voor problemen met de configuratie van Elasticsearch. De implementatie mislukt nu als de versie van de service Elasticsearch op de server niet compatibel is met Adobe Commerce. Eerder, slaagde de plaatsing zelfs als de versie van de Elasticsearch incompatibel was, die de kwesties van de productcatalogus na plaatsplaatsing veroorzaakte.<!--MAGECLOUD-2389-->

     U kunt de onverenigbaarheid oplossen door [ een kaartje van de Steun ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/deploy/best-practices) voor te leggen om Elasticsearch aan een compatibele versie te bevorderen, of de configuratie van Adobe Commerce te veranderen om een compatibele versie van de cliënt van Elasticsearch te specificeren PHP.

      - Voor Adobe Commerce versie 2.1.x tot 2.2.2, bevorder Elasticsearch aan versie 2.4.

      - Voer voor Adobe Commerce versie 2.2.3 en hoger een upgrade uit naar Elasticsearch 5.2.

      - Als u Elasticsearch 1.x of 2.x hebt en geen upgrade wilt uitvoeren, moet u de vereiste versie van de Adobe Commerce Elasticsearch PHP-client in composer.json bijwerken naar `"elasticsearch/elasticsearch": "~2.0"` .

   - Verbeterde validatie van omgevingsvariabelen om configuratie-instellingen te identificeren die conflicten kunnen veroorzaken tijdens de fasen build, implementatie en implementatie na implementatie. Bijvoorbeeld, toont een waarschuwingsbericht tijdens installatie en verbeteringsproces als het globale plaatsen voor statische inhoudsplaatsing met montages op bouwt of opstelt fase in conflict is.<!--MAGECLOUD-2156-->

- ![&#128279;](../../assets/fix.svg) **veranderlijke updates van het Milieu 1&rbrace; fixpictogram** - veranderde de volgende milieuvariabelen:

   - **[SKIP_HTML_MINIFICATION globale variabele](../environment/variables-global.md#skip_html_minification)** - veranderde de standaardwaarde in `true` om op bestelling de inhoudminificatie van de HTML toe te laten, die onderbreking wanneer het opstellen aan het Opvoeren en de milieu&#39;s van de Productie minimaliseert. Deze configuratie wordt vereist voor nul-onderbreking plaatsingen.<!--MAGECLOUD-2435-->

   - **[CLEAN_STATIC_FILES stelt veranderlijk](../environment/variables-deploy.md#clean_static_files)** op - toegevoegd het vermogen om het schone statische die dossierverwerking voor statische inhoud te beheren tijdens de bouwstijlfase wordt geproduceerd die op CLEAN_STATIC_FILES milieu veranderlijke het plaatsen wordt gebaseerd. Eerder, werden de statische inhoudsdossiers die tijdens de bouwstijlfase werden geproduceerd altijd schoongemaakt.<!--MAGECLOUD-1506-->

- ![&#128279;](../../assets/fix.svg) **Logging** - van het de fixpictogram van 0&rbrace; &lbrace;&lbrace;om de volgende veranderingen aan te brengen om logboekberichten te verbeteren en logboekgrootte te verminderen:

   - De de mislukkingslogboekingangen van de plaatsing omvatten nu de beveloutput van de verrichtingen die de mislukkingen veroorzaken zelfs als uw milieuconfiguratie niet zuivert niveau registreren specificeert. Zie [`MIN_LOGGING_LEVEL`](../environment/variables-global.md#min_logging_level).<!--MAGECLOUD-2489-->

   - Het toegevoegde registreren voor plaatsingsmislukkingen die voorkomen wanneer de geproduceerde die fabrieken door sommige uitbreidingen worden vereist kan niet correct worden geproduceerd omdat het dossiersysteem in een read-only staat is.<!--MAGECLOUD-2209-->

   - Verminderde opstellen logboekgrootte en de vaste opmaakkwesties die door opstellingsbevelen worden veroorzaakt die de interactieve vooruitgangsbar gebruiken.<!--MAGECLOUD-2402-->

   - Elimineerde onnodige breedheid en werkte de prioritaire niveaus voor sommige logboekverklaringen bij.<!--MAGECLOUD-2227-->

- ![ het pictogram van de moeilijke situatie ](../../assets/fix.svg) **Cron-Specifieke moeilijke situaties**—

   - Veranderde de standaard montages van de baanconfiguratie van de cron voor geschiedenisleven van 3d (4320 min) aan 1h (60 min) om prestatieskwesties en plaatsingsmislukkingen te verhinderen die kunnen voorkomen wanneer de kroonrij te snel vult.<!--MAGECLOUD-2427-->

   - Verbeterde het cron proces van het baanbeheer tijdens de opstellen fase om gegevensbestandsloten en andere kritieke kwesties te verhinderen. Nu, stoppen alle kroonbanen tijdens de opstellen fase en nieuw begin nadat de plaatsing voltooit.<!--MAGECLOUD-2445-->

   - Probleem verholpen met het vergrendelingsmechanisme voor het plannen van consumenten die worden gestart door cron-taken in Adobe Commerce versie 2.2.0 en hoger om te voorkomen dat cron-taken dubbele consumenten op de markt brengen.<!--MAGECLOUD-2464-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie met het [ statische proces van de inhoudscompressie ](../environment/variables-intro.md) (`gzip`) dat `not overwritten` en `no such file or directory` fouten veroorzaakte wanneer het van verwijzingen voorzien van naar het samengeperste dossier tijdens het plaatsingsproces.<!-- MAGECLOUD-2182-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die het `php ./vendor/bin/ece-tools config:dump` bevel verhinderde overtollige secties uit het `config.php` dossier tijdens het stortplaatsproces te verwijderen als de opslagscène niet wordt gespecificeerd. Nu kunt u uw configuratiebestanden eenvoudig tussen omgevingen verplaatsen. Nadat u de update naar `ece-tools` v2002.0.13 hebt uitgevoerd, kunt u oudere `config.php` -bestanden opnieuw genereren met de verbeterde opdracht `config:dump` . Zie [ beheer van de Configuratie voor opslagmontages ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/store-settings).<!--MAGECLOUD-2444-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die een fout tijdens opstelt fase veroorzaakte als de routeconfiguratie in het `.magento/routes.yaml` dossier van een [ apex ](https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp/) domein aan a `www` domein opnieuw richt.<!--MAGECLOUD-2556-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie met de `_merge` optie voor de [`SEARCH_CONFIGURATION`](../environment/variables-deploy.md#search_configuration) variabele die onjuiste fusieresultaten veroorzaakte als u niet de `engine` parameter in het bijgewerkte `.magento.env.yaml` configuratiedossier omvat. Nu, beschrijft de fusieverrichting correct slechts de waarden u in bijgewerkte `.magento.env.yaml` specificeert zonder u te vereisen om de `engine` parameter te plaatsen. <!--MAGECLOUD-2520-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een Redis configuratiekwestie die verkeerd zittingssluiten voor Adobe Commerce op versie 2.2.1 van de wolkeninfrastructuur en recenter toeliet, die langzame prestaties en onderbrekingen kan veroorzaken. Sessievergrendeling is nu standaard uitgeschakeld. Het probleem is veroorzaakt door een wijziging in het standaardgedrag van de parameter `disable_locking` die is geïntroduceerd in versie 1.3.4 van het Redis-sessiehandlerpakket. Zie [ colinmolenhour/php-redis-session-abstract pakket ](https://github.com/colinmollenhour/php-redis-session-abstract).<!-- MAGECLOUD-2515-->

## v2002.0.12

- ![ nieuw pictogram ](../../assets/new.svg) **Samenstellen van het Dock voor Wolk** - toegevoegd een bevel - `docker:build` - om a [ Docker te produceren stelt ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/) configuratie van de 7&rbrace; bewaarplaats van de Wolk samen.<!-- MAGECLOUD-2250 -->`ece-tools`

- ![ nieuw pictogram ](../../assets/new.svg) **de Plaatsen van de Verandering** - nu kunt u opslagscène zonder het uitvoeren en het invoeren configuratieproces veranderen. Terwijl de toepassing in Productie is en SCD_ON_DEMAND wordt toegelaten, zijn de opslag en admin scèneopties beschikbaar.<!-- MAGECLOUD-2019 -->

- ![ nieuw pictogram ](../../assets/new.svg) <!-- MAGECLOU-1998 -->**kaart van de Plaats en Robots** - creeerde a [ werkschema ](../store/robots-sitemap.md) om een `robots.txt` dossier toe te voegen en een `sitemap.xml` dossier voor één enkele domeinconfiguratie te produceren zonder een verandering in de infrastructuur te vereisen.

- ![ nieuw pictogram ](../../assets/new.svg) **Tovenaar** - toegevoegd twee [ tovenaars ](../deploy/smart-wizards.md) om u met de configuratie van de Wolk te helpen:<!-- MAGECLOUD-1910 -->

   - `ideal-state` - vorm de ideale staat voor minimale plaatsingsonderbreking

   - `master-slave` - load balancing voor database en Redis configureren

- ![ nieuw pictogram ](../../assets/new.svg) **Module verfrist zich** - voegde een bevel van de Wolk toe - `module:refresh` - om modules toe te laten die of niet uitdrukkelijk toegelaten werden, gelijkend op de manier dat het automatisch tijdens een bouwstijl wordt gedaan.<!-- MAGECLOUD-1521 -->

- ![ nieuw pictogram ](../../assets/new.svg) voegde de capaciteit toe om configuratie voor de diensten samen te voegen of te beschrijven gebruikend de `_merge` optie in [ CACHE ](../environment/variables-deploy.md#cache_configuration), [ SESSIE ](../environment/variables-deploy.md#session_configuration), [ WACHTRIJ ](../environment/variables-deploy.md#queue_configuration), en [ ZOEKEN ](../environment/variables-deploy.md#search_configuration) configuraties.<!-- MAGECLOUD-2105 -->

- ![ nieuw pictogram ](../../assets/new.svg) **het steekproefdossier van de Configuratie van het Milieu** - wij hebben een `.magento.env.yaml` steekproefdossier aan het ECE-Hulppakket toegevoegd dat een gedetailleerde beschrijving en mogelijke waarden voor elke milieuvariabele omvat.<!-- MAGECLOUD-1908 -->

   - We hebben ook een uitgebreide validatie toegevoegd voor de `.magento.env.yaml` -configuratie die fouten in het implementatieproces voorkomt die worden veroorzaakt door onverwachte waarden. Wanneer een fout optreedt, ontvangt u nu een gedetailleerd foutbericht dat begint met: `Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:`<!-- MAGECLOUD-1907 -->

- ![ nieuw pictogram ](../../assets/new.svg) voegde de volgende [**variabelen van het Milieu**](../environment/variables-intro.md) toe:

   - Nu kunt u veelvoudige scènes voor elk thema bepalen gebruikend nieuwe [ SCD_MATRIX ](../environment/variables-deploy.md#scd_matrix) omgevingsvariabele, die de hoeveelheid op te stellen themadossiers vermindert.<!-- MAGECLOUD-1501 -->

   - Toegevoegd [ DATABASE_CONFIGURATION ](../environment/variables-deploy.md#database_configuration) milieuvariabele om uw gegevensbestandverbindingen voor plaatsing aan te passen.<!-- MAGECLOUD-2047 -->

   - De nieuwe {&rbrack;(../environment/variables-global.md#min_logging_level) variabele 0} MIN_LOGGING_LEVEL treedt het minimumregistrerenniveau voor alle outputstromen met voeten zonder veranderingen in de code aan te brengen.<!-- MAGECLOUD-2129 -->&lbrack;

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die onderbreking tussen opstelt en post-opstelt fase veroorzaakte. Nu, begint de post-opstellen fase _onmiddellijk_ na de opstellen faseeinden.

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die niet de succesvolle cron banen, die met `status = success`, van het programma schoonmaakte.<!-- MAGECLOUD-2268 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie met de `post_deploy` haak die het geheime voorgeheugen in opstelde fase in plaats van post-opstelt fase van het project ontruimde.<!-- MAGECLOUD-2113 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie wanneer het gebruiken van SCD met veelvoudige scènes, die het zelfde `js-translation.json` dossier voor elke scène produceerde.<!-- MAGECLOUD-2034 -->

- ![ fixpictogram ](../../assets/fix.svg) optimaliseerde het `db:dump` bevel in het `ece-tools` pakket om het sluiten van lijsten te vermijden en snelheid te verhogen.<!-- MAGECLOUD-2033 -->

## v2002.0.11

>[!NOTE]
>
>Voor compatibiliteit met versie 2.2.4 is ECE-Tools versie 2002.0.11 vereist.

- ![ nieuw pictogram ](../../assets/new.svg) **Vormend read-only verbindingen aan niet-hoofdknopen** - Deze versie voegt de capaciteit toe om een read-only verbinding aan een niet-hoofdknoop te vormen om read-only verkeer (voor [ MariaDB ](../environment/variables-deploy.md#mysql_use_slave_connection)) te ontvangen.<!--MAGECLOUD-143 -->[ Redis ](../environment/variables-deploy.md#redis_use_slave_connection) en voor <!--MAGECLOUD-143 -->

- ![ nieuw pictogram ](../../assets/new.svg) **Tovenaar van de Configuratie** - voegde een tovenaar toe helpen uw configuratie voor statische inhoudsplaatsing verifiëren. Zie [ Slimme tovenaars ](../deploy/smart-wizards.md).<!--MAGECLOUD-1910 -->

- ![ nieuw pictogram ](../../assets/new.svg) **steun van de Console van het Symfony** - Toegevoegde steun voor Console 4 van het Symfony met Adobe Commerce 2.3.<!-- MAGECLOUD-1966 -->

- ![ fixpictogram ](../../assets/fix.svg) **Gewas die optimalisaties** plannen - verbeterde het rijbeheer en verbeterde registreren om met het zuiveren van op elkaar betrekking hebbende kwesties te helpen.<!-- MAGECLOUD-1607 -->

- ![ bevestigt pictogram ](../../assets/fix.svg) de bevestiging van de Plaatsing ontbreekt als een `ADMIN_EMAIL` of `ADMIN_USERNAME` waarde het zelfde als een bestaande beheerderrekening is.<!-- MAGECLOUD-1221 -->

- ![ fixpictogram ](../../assets/fix.svg) Verwijderde SOLR steun voor 2.2.x versies. 2.1.x de versies behouden de capaciteit om SOLR toe te laten.<!-- MAGECLOUD-1282 -->

- ![ fixpictogram ](../../assets/fix.svg) De eerste installatie van de het Opvoeren &amp; milieu&#39;s van de Productie van een PRO project omvat nu verschillende indexvoorvoegsels voor Elasticsearch om mogelijke conflicten te verhinderen terwijl het identificeren van verslagen die tot elk milieu behoren.<!-- MAGECLOUD-1489 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die de bouwstijlfase voor erfenisarchitectuur tijdens statische inhoudsplaatsing onderbrak.<!-- MAGECLOUD-2021 -->

- ![ fixpictogram ](../../assets/fix.svg) **Cron-Specifieke Verbeteringen** - herwerkte de cron implementatie:<!-- MAGECLOUD-1607 -->

   - Probleem verholpen waarbij de wachtrij voor uitsnijden snel werd gevuld. Nu worden de achterhaalde kroonbanen op een betrouwbaardere manier gewist.

   - Herorganiseerde de opeenvolging van kroonbanen zodat alle banen in afzonderlijke draden vóór de algemene groep lanceren.

   - Verbeterde logboekregistratie om u beter te helpen bij het opsporen van fouten in uitsnijdingen.

   - **NOTA** - Deze versie richt vele op elkaar betrekking hebbende kwesties. Als u momenteel sommige op elkaar betrekking hebbende flarden in _m2-hotfixes_ gebruikt, verwijder hen.

- ![&#128279;](../../assets/fix.svg) **SCD-Specifieke verbeteringen** van het 0&rbrace; fixpictogram &lbrace;

   - U kunt `VERBOSE_COMMANDS` en `SCD_COMPRESSION_LEVEL` milieuvariabelen tijdens zowel _gebruiken bouwt_ en de_ploy fasen.<!-- MAGECLOUD-1819 -->

   - Probleem verholpen waarbij implementatie mislukte met een willekeurige fout bij het tegenkomen van een onverwachte waarde voor de omgevingsvariabele `SCD_COMPRESSION_LEVEL` . Verbeterde configuratievalidering voor betekenisvolle meldingen. Zie [`SCD_COMPRESSION_LEVEL`](../environment/variables-build.md#scd_compression_level) voor acceptabele waarden. <!-- MAGECLOUD-2043 -->

   - Vaste het gedrag van de `SCD_COMPRESSION_LEVEL` stroom van de omgevingsvariabele zodat werken de met voeten treedt zoals verwacht.<!-- MAGECLOUD-2044 -->

   - Vaste een kwestie die de configuratie van de `SCD_THREADS` omgevingsvariabele in het `.magento.env.yaml` dossier _verhinderde_ stadium opstelt.<!-- MAGECLOUD-2046 -->

## v2002.0.10

- ![ nieuw pictogram ](../../assets/new.svg) **Statische Plaatsing van de Inhoud (SCD)** - er is een nieuw, alternatief plaatsingsproces om statische inhoud te produceren wanneer gevraagd (op bestelling). Dit vermindert onderbreking en verbetert geheim voorgeheugenbehandeling door de meest kritieke activa te produceren.<!-- MAGECLOUD-1285 -->

   - **Nieuwe milieu veranderlijk** - voegde de `SCD_ON_DEMAND` globale milieuvariabele toe om statische inhoud te produceren wanneer gevraagd.<!-- MAGECLOUD-1738 -->

   - **post-opstellings haak** - Toegevoegde a `post_deploy` haak voor het `.magento.app.yaml` dossier dat het geheime voorgeheugen ontruimt en (oorlogen) het geheime voorgeheugen _vooraf laadt nadat_ de container begint goedkeurend verbindingen. Het is beschikbaar slechts voor Pro projecten die het Opvoeren en van de Productie milieu&#39;s in [!DNL Cloud Console] bevatten en voor de projecten van de Aanzet. Hoewel niet vereist, werkt dit in combinatie met de `SCD_ON_DEMAND` omgevingsvariabele.<!-- MAGECLOUD-1788 -->

- ![ nieuw pictogram ](../../assets/new.svg) **Optimalisering** - Geoptimaliseerd het bewegen of het kopiëren van dossiers tijdens plaatsing om plaatsingssnelheid te verbeteren en ladingen op het dossiersysteem te verminderen.<!-- MAGECLOUD-1842 -->

- ![ nieuw pictogram ](../../assets/new.svg) **Logging van de Plaatsing** - voegde de capaciteit toe om de managers van het Logboek van het Logboek van Syslog en van het Graylog Uitgebreide (GELF) voor uitvoerlogboeken tijdens het plaatsingsproces toe te laten. Zie [ het Registreren managers ](../environment/log-handlers.md).<!-- MAGECLOUD-1751 -->

- ![ nieuw pictogram ](../../assets/new.svg) voegde de volgende [**variabelen van het Milieu**](../environment/variables-intro.md) toe:

   - `CRYPT_KEY` - Verstrek een cryptografische sleutel aan een ander milieu wanneer het bewegen van een gegevensbestand.<!-- MAGECLOUD-1556 -->

   - `SKIP_HTML_MINIFICATION` - _Globale_ milieu variabele die het kopiëren van de statische meningsdossiers in de `var/view_preprocessed` folder overslaat en geminificeerde HTML wanneer gevraagd produceert.<!-- MAGECLOUD-1621 and MAGECLOUD-1736-->

   - `SCD_ON_DEMAND` - _Globale_ milieu variabele om statische inhoud te produceren wanneer gevraagd.<!-- MAGECLOUD-1738 -->

   - `WARM_UP_PAGES` - U kunt de pagina&#39;s weergeven die u wilt gebruiken om de cache vooraf te laden. Beschikbaar in nieuwe [ post-opstelt variabelen ](../environment/variables-post-deploy.md).

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die een plaatselijk toegepast flard impliceerde die de plaatsing op een instantie breekt. Nu, ECE-Hulpmiddelen kunnen ontdekken dat een flard is toegepast.<!-- MAGECLOUD-982 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een conflict tussen het bundelen van JavaScript en functionaliteit GZIP. Nu werken deze eigenschappen correct samen.<!-- MAGECLOUD-1735 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die ECE-Tools CLI bevelen om veroorzaakte te ontbreken wanneer het gebruiken van vroegere PHP 7.0.x versies.<!-- MAGECLOUD-1744 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die statische inhoudsplaatsing met de compacte strategie in veelvoudige draden verhinderde.<!-- MAGECLOUD-1822 -->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een Redis zittingsvergrendelingskwestie die een Admin login vertraging veroorzaakte. Ook, is de moeilijke situatie beschikbaar voor 2.1.x.<!-- MAGECLOUD-1853 -->

## v2002.0.9

>[!NOTE]
>
>U moet [ Adobe Commerce op het metapakket van de wolkeninfrastructuur ](../dev-tools/install-package.md#update-the-metapackage) bevorderen om dit en alle toekomstige updates te krijgen.

- ![ nieuw pictogram ](../../assets/new.svg) **knoop-hulpmiddelen** - het `ece-tools` pakket steunt nu Adobe Commerce 2.1.x.<!-- MAGECLOUD-1086 -->

- ![ nieuw pictogram ](../../assets/new.svg) **herstelt configuratie** - u kan nu [ Redis ](../environment/variables-deploy.md#cache_configuration) pagina en standaardgeheime voorgeheugen en Redis zittingsopslag vormen gebruikend een omgevingsvariabele.<!-- MAGECLOUD-1552 -->

- ![ nieuw pictogram ](../../assets/new.svg) **Onderzoek, AMQP, en Redis de dienstverbeteringen** - wij verenigden de stroom van de de dienstconfiguratie zodat het zich nu de zelfde manier voor alle diensten gedraagt. Het handmatig bewerken van het `env.php` -bestand om services te configureren, wordt niet meer ondersteund. U moet omgevingsvariabelen of het `.magento.env.yaml` -bestand gebruiken. <!-- MAGECLOUD-1437 -->

- ![&#128279;](../../assets/fix.svg) **de variabelen van het Milieu 1&rbrace; bevestigen** -

   - Het gebruik van `env:STATIC_CONTENT_THREADS` is vervangen en wordt in een toekomstige versie verwijderd. Gebruik [ SCD_THREADS ](../environment/variables-deploy.md#scd_threads) in plaats daarvan.<!-- MAGECLOUD-1507 -->

   - De omgevingsvariabele `STATIC_CONTENT_EXCLUDE_THEMES` is vervangen. U moet in plaats hiervan de omgevingsvariabele `SCD_EXCLUDE_THEMES` gebruiken. <!-- MAGECLOUD-1640 -->

- ![ fixpictogram ](../../assets/fix.svg) **het Registreren** - wij vereenvoudigden het registreren rond ingebouwde het patchen verrichtingen.<!-- MAGECLOUD-1674 -->

- ![ fixpictogram ](../../assets/fix.svg) wij verwijderden `developer` wijzessteun en de `APPLICATION_MODE` omgevingsvariabele omdat zij onverwacht gedrag veroorzaakten.<!-- MAGECLOUD-1615 -->

- ![ fixpictogram ](../../assets/fix.svg) wij vervingen een kwestie die de statische mislukkingen van de inhoudsplaatsing met betrekking tot Redis veroorzaakte. Nu, multi-threaded statische de looppas van de inhoudsplaatsing zoals ontworpen.<!-- MAGECLOUD-1630 -->

- ![ fixpictogram ](../../assets/fix.svg) wij vervingen een kwestie die gebruikers voorhield om wijzigingen aan configuratiegebieden in Admin op te slaan, die als gevoelig na het runnen van het `app:config:dump` bevel worden gemerkt.<!-- MAGECLOUD-1175 -->

- ![ fixpictogram ](../../assets/fix.svg) wij toegevoegde steun voor een vroegere versie van `symfony/yaml` om conflicten met sommige pakketten te bevestigen, die nog niet compatibel met de recentste versie zijn.<!-- MAGECLOUD-1674 -->

## v2002.0.8

>[!NOTE]
>
>We hebben `vendor/magento/ece-patches` in deze release samengevoegd met `vendor/magento/ece-tools` . U hoeft het `vendor/magento/ece-patches` -pakket niet meer afzonderlijk bij te werken.

**Nieuwe eigenschappen:**

- **Verbeterd registreren**<!-- MAGECLOUD-1253 -MAGECLOUD-1495 -->
   - Wij verbeterden logboekoverseinen om betere verklaringen te verstrekken wanneer de bouwstijl of het proces opstelt een milieuvariabele met voeten treedt.
   - U kunt nu de voortgang van de installatie en upgrade in real-time bekijken. Tik op het bestand `install_update.log` om de voortgang weer te geven. Bijvoorbeeld:

     ```bash
     tail -f var/log/install_upgrade.log
     ```

- **Nieuw kroonbevel** - u kunt specifieke vastgezette kroonbanen in plaats van het tegenhouden van en het opnieuw lanceren van allen met het [`cron:unlock` nu ontgrendelen ](https://support.magento.com/hc/en-us/articles/360033099451) bevel. Niet beschikbaar in 2.1.<!-- MAGECLOUD-1367 -->

- **Verenigd configuratiedossier** - u kunt bouwt en stadia nu vormen gebruikend a [`.magento.env.yaml` ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/env/configure-env-yaml) dossier.<!-- MAGECLOUD-1369 -->

- **de configuratiedossiers van de Steun** - Het plaatsingsproces leidt nu automatisch tot een steun van de `app/etc/env.php` en `app/etc/config.php` configuratiedossiers na plaatsing. Wij hebben ook a [ nieuw CLI bevel ](https://support.magento.com/hc/en-us/articles/360033182871) toegevoegd om deze configuratiedossiers van een steun te herstellen.<!-- MAGECLOUD-1372 -->

- **de bevestigingsfouten van het Oplossen van problemen** - wij veranderden het bevel u moet gebruiken om bevestigingsfouten op te lossen wanneer `config.php` niet genoeg gegevens voor statische inhoudsplaatsing bevat. Eerder werd u door het foutbericht opgedragen `bin/magento app:config:dump` uit te voeren. Nu moet u `php ./vendor/bin/ece-tools config:dump` uitvoeren.<!-- MAGECLOUD-1491 -->

- **Nieuwe milieu variabelen** - u kan milieu variabelen nu gebruiken om het onderzoek van de douane [&#128279;](../environment/variables-deploy.md#search_configuration) en [ op AMQP-Gebaseerde ](../environment/variables-deploy.md#queue_configuration) diensten met uw plaats te verbinden.<!-- MAGECLOUD-1410 -->

- We hebben intelligente patching geïmplementeerd. Nu past het pakket patches toe die niet op Adobe Commerce zijn gebaseerd op de versie van de cloudinfrastructuur, maar op de versie van het patchpakket.<!--MAGECLOUD-1090-->

**Opgeloste kwesties:**

- We hebben een logboekprobleem verholpen dat fouten veroorzaakt.<!-- MAGECLOUD-1162 -->

- We hebben een probleem opgelost dat time-outuitzonderingen veroorzaakte tijdens het uitvoeren van implementaties in de interactieve modus.<!-- MAGECLOUD-1389 -->

- We hebben een probleem opgelost dat fouten veroorzaakte bij het gebruik van de compacte strategie voor het genereren van statische inhoud. Niet beschikbaar in 2.1.<!-- MAGECLOUD-1446 MAGECLOUD-1485-->

- Wij hebben een kwestie opgelost die het plaatsingsmanuscript verhinderde het opvoeren en productiemilieu&#39;s behoorlijk te identificeren.<!-- MAGECLOUD-1493 -->

- We hebben een probleem verholpen dat ervoor zorgde dat netwerkproblemen de databaseverbindingen onderbreken en fouten veroorzaken tijdens de installatie en het upgradeproces.<!-- MAGECLOUD-1520 -->

- We hebben een probleem verholpen waardoor u de configuratiebestanden niet meer dan één keer met `app:config:dump` kunt exporteren. Niet beschikbaar in 2.1.<!--  MAGECLOUD-1567  -->

- Wij bevestigden een Redis zitting _vergrendelings_ kwestie die een _Admin_ login vertraging veroorzaakte. Niet beschikbaar in 2.1.<!--  MAGECLOUD-1582  -->

- Wij verholpen een implementatiekwestie met betrekking tot versioning die een conflict met andere op composer-Gebaseerde het filtreren modules veroorzaakte.<!-- MAGECLOUD-1450 -->

- We hebben een probleem verholpen dat tijdens het importeren problemen met het PHP-geheugen veroorzaakte.<!-- MAGECLOUD-1310 -->

- Verwijderd patch; bug in `colinmollenhour/credis` v1.6 wordt gecorrigeerd om ondersteuning voor Adobe Commerce op cloudinfrastructuur 2.2.1 mogelijk te maken. Niet beschikbaar in 2.1.<!-- MAGECLOUD-1033 -->

## v2002.0.7

**Opgeloste kwesties:**

- We hebben `var/view_preprocessed` symlinking verwijderd om een probleem op te lossen dat tot minificatieconflicten van JavaScript leidde. <!-- MAGECLOUD-1454 -->

## v2002.0.6

**Opgeloste kwesties:**

- We hebben een probleem verholpen dat `gzip` fouten veroorzaakte wanneer een bestand- of mapnaam spaties bevat.<!-- MAGECLOUD-1413 -->

- We hebben een probleem opgelost dat ervoor zorgde dat implementatiescripts niet naar behoren konden herkennen en moduleafhankelijkheden konden inschakelen.<!-- MAGECLOUD-1424 -->

## v2002.0.5

**Nieuwe eigenschappen:**

- **vorm een cron consument met een milieu veranderlijk** - u kunt cron consumenten nu vormen gebruikend de nieuwe `CRON_CONSUMERS_RUNNER` milieuvariabele.

- **het aftasten van de Configuratie** - wij aftasten nu voor kritieke componenten tijdens het bouwstijl/stelt proces op en houdt het proces tegen als het aftasten ontbreekt, die onnodige onderbreking wegens de plaats die op onderhoudswijze wordt verhinderd.

- **bouwt/stelt berichten** op - wij hebben een configuratiedossier toegevoegd dat u aan [ opstellings Slack en/of e-mailberichten ](../environment/set-up-notifications.md) voor bouwt/stelt acties in al uw milieu&#39;s kunt gebruiken.

- **Statische inhoudscompressie** - wij persen nu statische inhoud gebruikend [ gzip ](https://www.gnu.org/software/gzip/) tijdens de bouwstijl en stellen fasen op. Deze compressie, in combinatie met een snelle compressie, helpt uw winkel te verkleinen en de implementatiesnelheid te verhogen. Indien noodzakelijk, kunt u compressie onbruikbaar maken gebruikend a [ bouwt optie ](../environment/variables-build.md) of [ veranderlijk ](../environment/variables-deploy.md) opstelt. Raadpleeg de volgende onderwerpen voor meer informatie:

   - [Omgevingsvariabelen van de toepassing](../application/variables-property.md)

   - [Statische prestaties voor implementatie van inhoud](../deploy/static-content.md)

   - [ proces van de Plaatsing ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/deploy/best-practices)

- **beheer van de Configuratie** - wij nu auto-produceren een `app/etc/config.php` dossier in uw bewaarplaats van het Git tijdens de bouwstijlfase als het niet reeds bestaat. Het automatisch gegenereerde bestand bevat alleen een lijst met modules en extensies. Als het bestand al bestaat, gaat de constructiefase verder als normaal. Als u [ Beheer van de Configuratie ](../store/store-settings.md) in een recentere tijd volgt, werken de bevelen het dossier bij zonder extra stappen te vereisen. Verwijs naar [ proces van de Plaatsing ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/deploy/best-practices) voor meer informatie.

- **dumps van het Gegevensbestand** - wij hebben a `magento/ece-tools` CLI bevel voor het creëren van gegevensbestanddumps in alle milieu&#39;s toegevoegd. Voor de milieu&#39;s van de Productie van het Pro-plan, laat dit bevel slechts dumpen van één van drie high-availability knopen, zodat kunnen de productiegegevens die aan een verschillende knoop tijdens de stortplaats worden geschreven niet worden gekopieerd. Wij adviseren het zetten van de toepassing op onderhoudswijze alvorens een gegevensbestandstortplaats in de milieu&#39;s van de Productie te doen. Zie [ Reservekopiebeheer ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/storage/snapshots) voor meer informatie.

- **opgeheven het intervalbeperkingen van de Kroon** - het standaardkantelinterval voor alle milieu&#39;s die in de us-3, eu-3, en ap-3 gebieden worden voorzien is 1 minuut. Het standaardinterval voor uitsnijden in alle andere gebieden is 5 minuten voor Pro-integratieomgevingen en 1 minuut voor Pro Staging- en Productieomgevingen. Als u uw bestaande uitsnijdtaken wilt wijzigen, bewerkt u de instellingen in `.magento.app.yaml` of maakt u een ondersteuningsticket voor productie-/parkeeromgevingen. Verwijs naar [ de banen van de opstelling cron ](../application/crons-property.md#set-up-cron-jobs) voor meer informatie.

**Opgeloste kwesties:**

- We hebben een probleem verholpen dat lange implementatietijden veroorzaakte als gevolg van het implementatieproces dat de `cache-clean` -bewerking aanroept vóór de implementatie van statische inhoud.<!-- MAGECLOUD-1327 -->

- Wij verholpen een kwestie die fouten tijdens de statische stap van de inhoudsgeneratie van plaatsing op de milieu&#39;s van de Productie veroorzaakte.<!-- MAGECLOUD-1322 -->

- We hebben een probleem verholpen waardoor sommige `magento/ece-tools` -opdrachten uitvoer niet konden vastleggen naar `stderr` . <!-- MAGECLOUD-1264 -->

- We hebben een probleem opgelost waardoor basis-URL-waarden in `env.php` niet kunnen worden bijgewerkt in vertakte vertakkingen. <!-- MAGECLOUD-1242 -->

- We hebben een probleem verholpen waardoor de opdracht `magento setup:install` een onbeveiligd voorvoegsel (`http://` ) toevoegde om basis-URL&#39;s te beveiligen.<!-- MAGECLOUD-1171 -->

- We hebben een probleem verholpen dat patchfouten verhinderde implementatiefouten te veroorzaken.<!-- MAGECLOUD-1170 -->

- We hebben een probleem verholpen waardoor `ece-tools` de uitvoering niet kan stoppen en een uitzondering kan genereren als er geen patches kunnen worden toegepast.<!-- MAGECLOUD-1152 -->

- We hebben een probleem verholpen dat fouten veroorzaakte bij het laden van de opslagruimte nadat het minieren van HTML in de beheerfunctie was ingeschakeld.<!-- MAGECLOUD-1138 -->

## v2002.0.4

**Opgeloste kwesties:**

- U kunt [ manueel terugstellen vastgelopen kroonbanen ](https://support.magento.com/hc/en-us/articles/360033099451) gebruikend een CLI bevel in alle milieu&#39;s via de toegang van SSH. Het plaatsingsproces stelt automatisch cron banen terug.<!-- MAGECLOUD-1355 -->

## v2002.0.3

**Opgeloste kwesties:**

- We hebben een probleem opgelost dat ertoe leidde dat pagina&#39;s uitvielen omdat Redis te lang duurde om te lezen/schrijven. U kunt de parameter `disable_locking` nu gebruiken in Redis-configuraties om dit probleem te voorkomen. <!-- MAGECLOUD-1311 -->

## v2002.0.2

**Opgeloste kwesties:**

- Het [!DNL RabbitMQ] configuratieproces verkrijgt nu automatisch alle vereiste parameters.<!-- MAGECLOUD-1246 -->

## v2002.0.1

**Nieuwe eigenschappen:**

- Adobe Commerce op wolkeninfrastructuur steunt nu werkingsgebied en [ statische strategieën van de inhoudsplaatsing ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy). De parameter `–s` is toegevoegd met de standaardinstelling `quick` voor de strategie voor de implementatie van statische inhoud. U kunt het milieu veranderlijke [ SCD_STRATEGY ](../environment/variables-deploy.md) gebruiken om deze strategieën met uw te passen en acties op te stellen en op te stellen. Deze variabele ondersteunt de opties `standard` , `quick` of `compact` . Als u `compact` selecteert, overschrijven we de `STATIC_CONTENT_THREADS` waarde met `1` , wat de implementatie kan vertragen, vooral in productieomgevingen. Niet beschikbaar in 2.1.<!--- MAGECLOUD-1057 -->

- We hebben een logbestand voor omgevingen gemaakt om acties vast te leggen en te compileren en implementeren. Het `var/log/cloud.log` -bestand bevindt zich in de hoofdmap van de toepassing. <!--- MAGECLOUD-1014 & MAGECLOUD-1023 -->

**Opgeloste kwesties:**

- Verfijnde het `ece-tools` pakket om het met Adobe Commerce op wolkeninfrastructuur 2.2.0 en hoger compatibel te maken.<!-- MAGECLOUD-919 & MAGECLOUD-1030 -->

- We hebben een probleem opgelost dat `ece-tools` ervan weerhield de uitvoering te stoppen en een uitzondering te genereren als er geen patches kunnen worden toegepast.<!-- MAGECLOUD-1186 -->

- We hebben een probleem opgelost dat ervoor zorgde dat uitzonderingen werden gegenereerd wanneer de compilatie van de injectie van afhankelijkheid (di) tijdens builds wordt overgeslagen.<!-- MAGECLOUD-1047 & MAGECLOUD-1049 -->

- We hebben een probleem verholpen waardoor aangepaste Redis-configuraties in het `env.php` -bestand werden overschreven tijdens het implementatieproces.<!-- MAGECLOUD-1019 -->

- We hebben een probleem verholpen dat zorgt voor omleiding als gevolg van een uitgeschakelde functie voor veilig beheer.<!-- MAGECLOUD-1020 -->

## v2002.0.0

>[!WARNING]
>
>Dit pakket is niet meer compatibel met andere versies van Adobe Commerce op wolkeninfrastructuur en **zou niet** moeten worden gebruikt.

### Eerste release

Eerste release van `ece-tools` voor Adobe Commerce op cloudinfrastructuur 2.2.0.
