---
title: Cloud Docker-pakket
description: Zie een lijst met de meest recente verbeteringen in het Cloud Docker-pakket.
feature: Cloud, Docker, Release Notes
recommendations: noDisplay, catalog
last-substantial-update: 2024-10-07T00:00:00Z
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 0%

---

# Cloud Docker-pakket

Het pakket [`magento/magento-cloud-docker` ](https://github.com/magento/magento-cloud-docker) biedt functionaliteit en Docker-afbeeldingen om Adobe Commerce te implementeren in een lokale Cloud-omgeving. Deze versienota&#39;s beschrijven de recentste verbeteringen aan dit pakket, dat een component van [ de Reeks van Hulpmiddelen van de Wolk voor Commerce ](cloud-tools-suite.md) is.

Het pakket `magento/magento-cloud-docker` gebruikt de volgende versiereeks: `<major>.<minor>.<patch>`

De opmerkingen bij de release omvatten:

- ![ nieuw pictogram ](../../assets/new.svg) Nieuwe eigenschappen
- ](../../assets/fix.svg) Bevestigingspictogram van 0} moeilijke situatie en verbeteringen![

<!--Add release notes below-->

## v1.4.0 {#latest}

Releasedatum: 7 oktober 2024

- ![ fixpictogram ](../../assets/fix.svg) **Refactored code** - Verwijderde steun van oude PHP versies (7.4, 7.3, 7.2) en verwante bibliotheken en beelden.

## v1.3.7

Releasedatum: 8 april 2024

- ![ nieuw pictogram ](../../assets/new.svg) **PHP** — Toegevoegde steun voor PHP 8.3 en PHP 8.3 beelden.
- ![ nieuw pictogram ](../../assets/new.svg) **Nginx** — Toegevoegde beeld nginx v. 1.24.
- ![ nieuw pictogram ](../../assets/new.svg) **OpenSearch** - Toegevoegde beeld OpenSearch v. 2.12, 1.3.
- ![ nieuw pictogram ](../../assets/new.svg) **Composer** - bijgewerkte versie Composer aan 2.2.23.

## v1.3.6

Releasedatum: 31 juli 2023

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde nieuwe de dienstversie** - OpenSearch 2.5.
- ![ nieuw pictogram ](../../assets/new.svg) **laat het geheime voorgeheugen van de Composer** toe - nu kunt u de configuratie van het Dok uitbreiden om Composer duidelijk geheime voorgeheugen toe te laten wanneer het beginnen van de container van het Dok. Zie [ de configuratie van het Dok ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/extend-docker-configuration/) in het _Dok van de Wolk voor Commerce_ gids uitbreiden.

## v1.3.5

Releasedatum: 10 maart 2023

- ![ nieuw pictogram ](../../assets/new.svg) **ionCube** - voegde de IonCube uitbreiding voor PHP 8.1 beeld toe.
- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde nieuwe de dienstversies** - OpenSearch 2.3 en 2.4, PHP 8.2, Varnish 7.1.1.
- ![ nieuw pictogram ](../../assets/new.svg) **Verbeterde steun voor PHP 8.2** - Vaste verenigbaarheidskwesties met bepaalde PHP 8.2.x versies om Commerce 2.4.6 te steunen.
- ](../../assets/fix.svg) **de kwestie-Vaste kwesties van de 2} componist van de moeilijke situatie ![ {** die na het bijwerken van de versie Composer binnen de containers van de Docker voorkwamen.

## v1.3.4

Releasedatum: 27 oktober 2022

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde nieuwe beelden Varnish** - Toegevoegde beelden voor Varnish 6.5, 7.0, en 7.1.<!-- MCLOUD-7879 -->

## v1.3.3

Releasedatum: 13 september 2022

- ![ nieuw pictogram ](../../assets/new.svg) **Apple M1 (ARM64) steun** - Toegevoegde veranderingen in de beelden van het Dok om steun voor Apple M1 (ARM64) architectuur toe te laten.<!-- MCLOUD-7989-2 MCLOUD-7989 -->
- ![ fixpictogram ](../../assets/fix.svg) **Brievenbus** - Vaste een kwestie waar de dienst van de Brievenbus e-mails niet tijdens ontwikkelaarwijze vangstde.<!-- MCLOUD-8643 -->
- ![ fixpictogram ](../../assets/fix.svg) **init-docker.sh** - Vaste de recensies validator van de dienstversies in het `init-docker.sh` manuscript.<!-- MCLOUD-8765 -->

## v1.3.2

Releasedatum: 31 maart 2022

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde Elasticsearch 7.10 beeld**<!-- MCLOUD-8548 -->

## v1.3.1

Releasedatum: 10 maart 2022

- ![ nieuw pictogram ](../../assets/new.svg) **Steun PHP 8.1** - toegevoegde steun voor PHP 8.1.
- ![ nieuw pictogram ](../../assets/new.svg) **OpenSearch** - Toegevoegde beelden van versies OpenSearch 1.1 en 1.2.
- ![ nieuw pictogram ](../../assets/new.svg) **Composer 2.1** - plaats composer 2.1.x door gebrek in PHP 8.x beelden.
- ![ nieuw pictogram ](../../assets/new.svg) **PHP beeldverbeteringen** -

   - PHP 8.1-afbeeldingen toegevoegd
   - Bijgewerkte versie xDebug 3.1.2
   - Bijgewerkt xmlrpc 1.0.0RC3

- ](../../assets/fix.svg) **Elasticsearch &amp; verbeteringen OpenSearch** - Verbeteringen in Elasticsearch en Dockerfiles OpenSearch; verwijder Elasticsearch 5.2 beeld.![
- ![ fixpictogram ](../../assets/fix.svg) **Natriumuitbreiding** - Toegelaten de `sodium` uitbreiding door gebrek in alle PHP beelden.
- ](../../assets/fix.svg) **het geheime voorgeheugenvolume van de Composer** - Vaste weg voor het geheim voorgeheugenvolume van Composer om in het voorgeheugen ondergebrachte Composer pakketten te hebben.![
- ![ fixpictogram ](../../assets/fix.svg) **de beperking van het Geheugen in nginx** - Vaste beperking van geheugen in NGINX beeld.

## v1.3.0

Releasedatum: 25 oktober 2021

- ![ fixpictogram ](../../assets/fix.svg) **verbetert het werkschema van de wijze van de Ontwikkelaar** - eerder, moest u de wijze in de bouwstijl specificeren en stappen opstellen. De optie `--mode` in de stap `build` bepaalt nu de modus in de latere stap `deploy` . Het instellen van de modus na de implementatie is niet meer vereist. Zie {de wijze van de 0} Ontwikkelaar ](https://developer.adobe.com/commerce/cloud-tools/docker/deploy/developer-mode/).<!-- ACMP-1086 -->[
- ![ fixpictogram ](../../assets/fix.svg) **Verbeteringen voor read-only filesystem** - <!-- ACMP-1106 -->
   - Probleem verhelpen met een PHP-container voor e-mailconfiguratie.
   - Kan omgevingsvariabelen gebruiken in INI-bestanden.
   - Zorg ervoor dat voor PHP-ingangspunten geen schrijfmachtiging nodig is.
- ![ fixpictogram ](../../assets/fix.svg) **Knoop van de Update** - werk de gebundelde versie van de Knoop bij; wanneer het installeren van Knoop in PHP-CLI beelden, gebruikt het nu de huidige versie LTS.<!-- ACMP-1539 -->
- ![ herstellingspictogram ](../../assets/fix.svg) **Symfony van de Update** - werkte de gebiedsdelen van Symfony config bij om compatibel te zijn met Adobe Commerce 2.4.4.<!-- ACMP-1533 -->

## v1.2.4

Releasedatum: 29 juli 2021

- ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe `Zookeeper` container** - toegevoegd a [ container van de Zookeeper ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#zookeeper-container) om slotleveranciersconfiguratie voor projecten te beheren die niet aan Adobe Commerce op de infrastructuur van de Wolk worden opgesteld.<!--MCLOUD-8000-->

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde steun voor Composer 2.0.** - Toegevoegde Composer versie 2.0 aan het de configuratiedossier van Composer om verbeteringen van Composer 1.0 te steunen die eind-van-leven nadert.<!--MCLOUD-8003-->

## v1.2.3

Releasedatum: 14 juni 2021

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde PHP 8.0** - Bijgewerkt PHP aan versie 8.0, toestaand u uit alle nieuwe eigenschappen en optimalisaties PHP 8.0 omvat.<!--MCLOUD-7941-->
- ![ nieuw pictogram ](../../assets/new.svg) **bijgewerkt aan Varnish 6.6 en Elasticsearch 7.11.2** - de volgende verbindingen verstrekken versieinformatie over [ Vernis Geheime voorgeheugen 6.6 ](https://varnish-cache.org/releases/rel6.6.0.html#rel6-6-0) en Elasticsearch 7.11.2.<!--MCLOUD-7921-->
- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde `ioncube` uitbreiding voor PHP beeld 7.4** - de `ioncube` uitbreiding is opnieuw toegevoegd aan PHP beeld 7.4 na aanvankelijk uitgesloten van PHP 7.3 aan PHP verbetering 7.4. *[Voorgelegd door mattskr ](https://github.com/magento/magento-cloud-docker/pull/314).*<!--PR #314-->
- ![ nieuw pictogram ](../../assets/new.svg) **voegde een optie van de dossiersynchronisatie toe:`manual-native`** - de `manual-native` optie van de dossiersynchronisatie verstrekt handcontrole over synchronisatie, die de beste prestaties voor de milieu&#39;s van macOS en van Vensters verstrekt. Lees over het gebruiken van de `manual-native` optie op [ wijze van de Ontwikkelaar ](https://developer.adobe.com/commerce/cloud-tools/docker/deploy/developer-mode/) en [ het Synchroniseren van gegevens in een ontwikkelaarmilieu van de Docker ](https://developer.adobe.com/commerce/cloud-tools/docker/setup/synchronize-data/#file-synchronization-options).<!--MCLOUD-7977-->
- ![ nieuw pictogram ](../../assets/new.svg) **Verwijderde volume schrappingen van `up` en `down` bevelen** - de `--volume` optie werd verwijderd uit `bin/magento-docker up` en `bin/magento-docker down` bevelen, die door het nieuwe `bin/magento-docker init` bevel met een waarschuwing van het gegevensverlies worden vervangen. Door deze wijziging voorkomt u dat gegevens per ongeluk verloren gaan. *[Voorgelegd door joeshelton-wagento ](https://github.com/magento/magento-cloud-docker/pull/319).*<!--PR #319-->
- ![ fixpictogram ](../../assets/fix.svg) **bijgewerkte `CN` waarde voor het geproduceerde certificaat** - Verwijderde de geharde `CN` waarde uit Dockerfile. Deze waarde leidde tot een certificaatfout (`NET::ERR_CERT_INVALID`) die `--host` optie voor het `ece-docker build:compose` bevel om veroorzaakte te worden genegeerd.<!--MCLOUD-7934-->

## v1.2.2

Releasedatum: 20 april 2021

- ![ nieuw pictogram ](../../assets/new.svg) **Bijgewerkt `host.docker.internal` om platform onafhankelijk te zijn** - u kunt zelfde Docker nu creëren stelt manuscripten voor Ubuntu, Vensters, en macOS samen. Het gebruik van Xdebug op Ubuntu vereist niet langer een afzonderlijke omgevingsvariabele. [ Repareren die door Vitol van Igor ](https://github.com/magento/magento-cloud-docker/pull/299) wordt voorgelegd.<!--Issue #298-->
- ![ nieuw pictogram ](../../assets/new.svg) **Bijgewerkt init-docker.sh** - voegde het `mounts` voorwerp aan de `MAGENTO_CLOUD_APPLICATION` omgevingsvariabele toe. [ Reparatie die door Chiranjeevi ](https://github.com/magento/magento-cloud-docker/pull/299) wordt voorgelegd.<!--Issue #299-->
- ![ nieuw pictogram ](../../assets/new.svg) **Bijgewerkt init-docker.sh** - werkte het `init-docker.sh` manuscript met PHP 7.4 en de versies van Docker 1.2.1 van de Wolk bij. [ Repareren die door Adarsh Manickam ](https://github.com/magento/magento-cloud-docker/pull/300) wordt voorgelegd.<!--Issue #300-->
- ![ nieuw pictogram ](../../assets/new.svg) **Natrium toegelaten door gebrek** - Toegelaten de `sodium` PHP uitbreiding door gebrek binnen de beelden van de Docker van PHP.<!--MCLOUD-7548-->
- ![ nieuw pictogram ](../../assets/new.svg) **`custom-registry`optie** - toegevoegd a `--custom-registry` optie aan `php ./vendor/bin/ece-docker build:compose` bevel voor het gebruiken van uw eigen beeldregistratie.<!--MCLOUD-7476-->

  ```bash
  ./vendor/bin/ece-docker build:compose --custom-registry=my-registry.example.com
  ```

- ![ nieuw pictogram ](../../assets/new.svg) **Verwijderde oude versies van de Elasticsearch** - Verwijderde versies van de Elasticsearch 1.7 en 2.4 uit de beelden van de Elasticsearch.<!--MCLOUD-7504-->
- ![ nieuw pictogram ](../../assets/new.svg) **auto-produceert NGINX certificaten** - Verwijderde de bestaande certificaten uit het beeld NGINX. De NGINX-certificaten worden nu automatisch gegenereerd bij elke nieuwe implementatie voor verbeterde beveiliging.<!--MCLOUD-7396-->
- ![ fixpictogram ](../../assets/fix.svg) **Toegelaten`opcache.validate_timestamps`** - Toegelaten `opcache.validate_timestamps` PHP plaatsend door gebrek op ontwikkelaarwijze. Het toelaten van deze het plaatsen verholpen de kwestie waar de veranderingen in het filesystem niet in Docker werden erkend.<!--MCLOUD-7466-->
- ![ bevestigen pictogram ](../../assets/fix.svg) **Vast`build:custom:compose`** - Vaste het `build:custom:compose` bevel om een fout te werpen wanneer de dossiers niet tijdens het bouwstijlproces kunnen worden beschreven. Door een fout te genereren voorkomt u situaties waarin `docker-compose up` de verkeerde bestanden zou kunnen gebruiken. <!--MCLOUD-7457-->
- ](../../assets/fix.svg) Vast **het pictogram van de moeilijke situatie `--sync_engine="native"` optie** - Vaste de kwestie waar op productiemodus (`--mode="production"`), de `--sync_engine="native"` optie geen ingangen voor lokale omslagen in het `docker.composer.yml` dossier zou creëren.<!--MCLOUD-7254-->![
- ![ herstellingspictogram ](../../assets/fix.svg) **Vaste de bevestigingsfouten van de de dienstversie** - Toegevoegde de dienstversies voor [!DNL RabbitMQ], Elasticsearch, en andere diensten aan het `type` bezit in de `MAGENTO_CLOUD_RELATIONSHIP` variabele. Het toevoegen van deze versies aan de `relationships` variabele herstelde de bevestigingsfouten die tijdens plaatsingsfase voorkwamen.<!--MCLOUD-7572-->

## v1.2.1

Releasedatum: 21 december 2020

- ![ nieuw pictogram ](../../assets/new.svg) **NGINX bevelopties** - toegevoegd bouwt bevelopties om het aantal NGINX `worker_processes` en NGINX `worker_connections` voor de diensten van TLS en van het Web te veranderen. De parameter `worker_process` behoudt de mogelijkheid om de waarde in te stellen op `auto` . Voorbeelden: <!--MCLOUD-7259-->

  ```bash
  ./vendor/bin/ece-docker build:compose --nginx-worker-processes=2
  ./vendor/bin/ece-docker build:compose --nginx-worker-connections=2048
  ```

- ![ nieuw pictogram ](../../assets/new.svg) **TLS beveloptie** - Toegevoegd bouwt beveloptie om een configuratie zonder de dienst van TLS tot stand te brengen. Voorbeeld: <!--MCLOUD-7259-->

  ```bash
  ./vendor/bin/ece-docker build:compose --no-tls
  ```

- ![ nieuw pictogram ](../../assets/new.svg) **NGINX geheugenconsumptie** - verminderde het geheugen dat door het NGINX proces voor de diensten van TLS en van het Web wordt verbruikt.<!--MCLOUD-7259-->

- ![ nieuw pictogram ](../../assets/new.svg) **Blackfire** - Gehandicapte Blackfire PHP uitbreiding door gebrek in het beeld van het Dok van de Wolk.

- ![ fixpictogram ](../../assets/fix.svg) **PHP-FPM container** - Vaste PHP-FPM de controle van de containergezondheid door `WEB_PORT` van `80` te veranderen in `8080`.<!--MCLOUD-7232-->

- ![ fixpictogram ](../../assets/fix.svg) **Ongeldig volume noemend** - Vaste een fout met ongeldig volume noemend op ontwikkelaarwijze.<!--MCLOUD-7442-->

- ![ fixpictogram ](../../assets/fix.svg) **NGINX stroomopwaartse haven** - werkte het beeld van de NSE 1.19 van de Docker aan gebruikshaven 8080 bij om een oneindige lijn te vermijden. [ Repareren die door Adarsh Manickam ](https://github.com/magento/magento-cloud-docker/pull/296) wordt voorgelegd.<!--Issue 295-->

## v1.2.0

Releasedatum: 9 november 2020

- ![ nieuwe pictogram ](../../assets/new.svg) **de updates van de Container—**

   - ![ nieuw pictogram ](../../assets/new.svg) **PHP-FPM container** - toegevoegde steun voor de gnupg PHP uitbreiding. [ Repareren die door G Arvind van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/210) wordt voorgelegd.<!--MCLOUD-5981-->

   - ![ fixpictogram ](../../assets/fix.svg) **container van het Gegevensbestand** - Vaste de gezondheidscontrole van de gegevensbestandcontainer door het vereiste gegevensbestandwachtwoord aan het bevel van de gezondheidscontrole toe te voegen.<!--MCLOUD-7122-->

   - ![ nieuw pictogram ](../../assets/new.svg) **container van de Elasticsearch**

      - Toegevoegde steun voor Elasticsearch 7.9 voor verenigbaarheid met de aanstaande versies van Adobe Commerce.<!--MCLOUD-7190-->

      - **Elasticsearch plug-in configuratie** - Toegevoegde steun om de configuratieinformatie van de Elasticsearch plug-in van het `services.yaml` dossier te gebruiken om het `docker-compose.yaml` dossier voor een Dok van de Wolk voor het milieu van Commerce te produceren. Zie [ de stoppen van de Elasticsearch ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#elasticsearch-plugins).<!--MCLOUD-2789-->

      - **de insteekmodule van de Elasticsearch steun** - toegevoegde steun voor de volgende Elasticsearch stop-ins: `analysis-icu`, `analysis-phonetic`, `analysis-stempel`, en `analysis-nori`. De plug-ins `analysis-icu` en `analysis-phonetic` worden standaard geïnstalleerd. U kunt de plug-ins `analysis-stempel` en `analysis-nori` naar wens toevoegen of verwijderen. <!--MCLOUD-2789-->

   - ![ nieuw pictogram ](../../assets/new.svg) **CLI container**

      - **de bevelen van de Looppas binnen de containers van PHP van de Doopvaring** - nu kunt u CLI van het Dok van de Wolk gebruiken om bevelen binnen containers PHP in uw milieu van het Dok in werking te stellen zonder het moeten PHP op de gastheer installeren. Met de volgende opdracht bouwt u bijvoorbeeld de configuratie: `./bin/magento-docker php 7.3 vendor/bin/ece-docker build:compose` . Zie [ CLI van het Docker van de Wolk ](https://developer.adobe.com/commerce/cloud-tools/docker/quick-reference/#cloud-docker-cli). [ Repareren die door G Arvind van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/209) wordt voorgelegd.<!--MCLOUD-5982-->

      - OpenSSH-client toegevoegd aan PHP CLI containers. Nu, kunt u ssh-agent gebruiken die voor Composer door:sturen als het `composer.json` dossier privé gothandelen bevat die een ssh cliënt vereisen om Composer bevelen te gebruiken.<!--MCLOUD-6008-->

   - ![ fixpictogram ](../../assets/fix.svg) **container TLS** - nu, is de [ container TLS ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#tls-container) gebaseerd op het `https://hub.docker.com/r/magento/magento-cloud-docker-nginx` beeld van het Dok in plaats van het beeld CentOS. Deze wijziging verhelpt problemen die fouten veroorzaakten bij het verzenden van HTTPS-aanvragen tussen containers in de Cloud Docker-omgeving.<!--MCLOUD-6469-->

   - ![ nieuw pictogram ](../../assets/new.svg) **container van de Test** - voegde een testcontainer voor toepassing het testen toe, en voegde de `--with-test` optie aan het Dokker `build:compose` bevel toe om de container slechts tot stand te brengen wanneer het testen in het milieu van de Dokker. Zie [ toepassing het testen ](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/).<!--MCLOUD-6394-->

   - ![ nieuw pictogram ](../../assets/new.svg) **FPM-XDEBUG container**

      - ![ nieuw pictogram ](../../assets/new.svg) **vorm Xdebug op Linux** - voegde de `--set-docker-host` optie aan het `ece-docker build:compose` bevel toe om de `host.docker.internal` waarde in de container te vormen Xdebug. Deze optie is vereist als u Xdebug wilt gebruiken op Linux-systemen. Zie [ Xdebug voor Docker ](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/) vormen.<!--MCLOUD-6430-->

      - ![ fixpictogram ](../../assets/fix.svg) Vaste de Xdebug veranderlijke configuratie voor het BINNENPUNT van de Dok om `uninitialized "with_xdebug" variable` fouten in de logboeken op te lossen. [ Fix die door Florent Olivaud ](https://github.com/magento/magento-cloud-docker/pull/218) wordt voorgelegd <!--MCLOUD-6043-->

- ![ nieuw pictogram ](../../assets/new.svg) **de configuratieveranderingen van de Docker**

   - **configuratie MailHog** - nu kunt u de volgende `ece-docker build:compose` bevelopties gebruiken om MailHog onbruikbaar te maken en havens te specificeren: `--no-mailhog`, `--mailhog-http-port`, en `--mailhog-smtp-port`. Zie [ Opstelling e-mail ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/#set-up-email).<!--MCLOUD-6898, MCLOUD-6660-->

   - Voor Cloud Docker voor Commerce 1.2.0 en hoger biedt Adobe nu Docker-afbeeldingen voor elke patchversie en de Docker-configuratiegenerator maakt de Docker-configuratie met een opgegeven patchversie in plaats van de nieuwste versie. Eerder, bouwde de configuratiegenerator van de Dokker de configuratie gebruikend de recentste flardversie die Cloud Docker voor milieu&#39;s kon breken Commerce die gebruikend een vroegere versie werden gebouwd.<!--MCLOUD-7093-->

   - **specificeer douanebeelden en versies in de configuratie van het Dok van de douaneWolk** - bijgewerkt het `build:custom:compose` bevel met opties om douanebeelden en versies te specificeren wanneer het produceren van een douaneDocker stelt configuratiedossier samen (`docker-compose.yaml`). Zie [ bouwt een douaneDocker stelt configuratie ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/custom-docker-compose/) samen. <!--MCLOUD-7089-->

   - Bijgewerkt de de gastheerconfiguratie van de Docker om haven 443 bloot te stellen om toegang tot Adobe Commerce (`https://magento2.docker`) van alle containers toe te laten CLI. U kunt de standaardpoort wijzigen door de optie `--tls-port` toe te voegen wanneer u het Docker-configuratiebestand genereert.<!--MCLOUD-6806-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die het Kloud Docker voor Commerce veroorzaakte om te ontbreken als het `app/etc/env.php` dossier bestaat.<!--MCLOUD-6732-->

- ![ herstellingspictogram ](../../assets/fix.svg) werkte bouwstijlconfiguratie bij om genoemde volumes met regelmatige volumes te vervangen om kwesties te verhinderen wanneer het opstellen van het Dok van de Wolk voor Commerce op Linux of Subsystem van Vensters voor Linux (WSL2).<!--MCLOUD-6732-->

- ![ fixpictogram ](../../assets/fix.svg) werkte het Dok van de Wolk voor functionele tests van Commerce bij om Composer 2.0 te steunen.<!--MCLOUD-7183-->

## v1.1.2

Releasedatum: 9 september 2020

- ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde steun voor Elasticsearch 7.7 <!--MCLOUD-6219-->

## v1.1.1

Releasedatum: 5 augustus 2020

- ![ fixpictogram ](../../assets/fix.svg) **Bijgewerkte e-mailconfiguratie** - Bijgewerkt het standaardDocker van de Wolk voor de configuratie van Commerce om de dienst te steunen MailHog in plaats van het gebruiken van SendMail. Zie [ Opstelling e-mail ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/#set-up-email).<!--MCLOUD-5624-->

- ![ fixpictogram ](../../assets/fix.svg) herstelde de bibliotheek van PS aan de de omgevingsconfiguratie van het Dok van de Wolk om `ps:  command not found` fouten te bevestigen.<!--MCLOUD-6621-->

- ![ herstellingspictogram ](../../assets/fix.svg) werkte standaarddocker van de Wolk voor de configuratie van Commerce bij om automatische steun van de volumes van de gegevensbestandingang en MariaDB te verwijderen om `Cannot create container for service db` fouten te bevestigen die wanneer het beginnen van uw milieu van de Dok van de Wolk kunnen voorkomen.

  Nu kunt u de Cloud Docker-omgeving zo configureren dat de databasemappen worden gekoppeld door de volgende opties toe te voegen aan de opdracht `ece-docker build:compose` : `--with-entry-point` en `with-mariadb-conf` . Zie [ de configuratieopties van de Dienst ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/#service-configuration-options).<!--MCLOUD-6424-->

- ![ nieuwe pictogram ](../../assets/new.svg) **CLI bevelupdates**

| Handeling | Opdracht |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| Voeg een ingangspunt aan de gegevensbestandcontainer toe om het gegevensbestand van steun te herstellen | `./vendor/bin/ece-docker build:compose --db --with-entrypoint` |
| Een MariaDB-configuratievolume toevoegen | `./vendor/bin/ece-docker build:compose --db --mariadb-conf` |

## v1.1.0

Releasedatum: 25 juni 2020

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde steun voor de gespleten oplossing van de gegevensbestandprestaties** - nu kunt u een opslag vormen en opstellen gebruikend de Gesplitste oplossing van de gegevensbestandprestaties in het milieu van het Dok van de Wolk.<!--MCLOUD-3740-->

- ![ nieuw pictogram ](../../assets/new.svg) **Steun voor Adobe Commerce en plaatsing van de Magento Open Source** - nu kunt u het Dok van de Wolk voor Commerce gebruiken om een lokale ontwikkelomgeving voor projecten op te stellen die niet op Adobe Commerce op wolkeninfrastructuur worden ontvangen.<!--MCLOUD-5667-->

- ![ nieuw pictogram ](../../assets/new.svg) **Blackfire.io steun** - Toegevoegde steun om de {](https://developer.adobe.com/commerce/cloud-tools/docker/test/blackfire/) uitbreiding 4} Blackfire.io voor geautomatiseerde prestaties te gebruiken testend. [ [ Reparatie die door Adarsh Manickam van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/202) wordt voorgelegd <!--MCLOUD-5857-->

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Container**

   - **vernis** - nu vervaagt is het standaardgeheime voorgeheugen wanneer u Adobe Commerce in een milieu van het Dok van de Wolk gebruikend een gesteunde versie van het de toepassingsmalplaatje van de Wolk opstelt. Zie [ Vierige container ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#varnish-container).<!--MCLOUD-2634-->

   - De optie `--no-varnish` is toegevoegd om de installatie van Varnish-services over te slaan wanneer u het configuratiebestand van Cloud Docker genereert.<!--MCLOUD-2634-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Gegevensbestand**

      - De ondersteuning voor de MySQL-database is toegevoegd. Nu kunt u de Cloud Docker-omgeving configureren met MariaDB of MySQL. Zie [ de configuratieopties van de Dienst ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/#service-configuration-options).<!--MCLOUD-5691-->

      - Toegevoegd de capaciteit om de verhogings en compensatiemontages voor gegevensbestandreplicatie te plaatsen wanneer u het Docker samenstelt dossier produceert. Zie [ de containers van de Dienst ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/#service-containers).<!--MCLOUD-5735-->

   - ![ nieuw pictogram ](../../assets/new.svg) **PHP-FPM**

      - Toegevoegde steun voor PHP 7.4. [ Fix die door Mohanela Murugan van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/198) wordt voorgelegd <!--MCLOUD-198-->

      - Mogelijkheid toegevoegd om een `php.ini` -bestand in de hoofdprojectmap te kopiëren naar de Cloud Docker-omgeving en aangepaste PHP-instellingen toe te passen op de PHP-FPM- en CLI-containers. Zie [ PHP montages ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#customize-php-settings) aanpassen. [ Repareren die door Mathew Beane van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/130) wordt voorgelegd.<!--MCLOUD-6012-->

      - Er is een containerhealth check toegevoegd. [ Reparatie die door de Sampath van de Visant van de Technologie van de Zilker ](https://github.com/magento/magento-cloud-docker/pull/188) wordt voorgelegd.<!--MCLOUD-5752-->

   - ![ fixpictogram ](../../assets/fix.svg) **Node.js** - werkte de standaardversie Node.js van versie 8 aan versie 10 bij om veiligheid te verbeteren. Node.js versie 8 is afgekeurd en niet meer bijgewerkt met insectenmoeilijke situaties of veiligheidspatches. [ Reparatie die door Mohan Elamurugan van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/183) wordt voorgelegd.<!--MCLOUD-5586-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Elasticsearch**

      - Toegevoegde steun voor Elasticsearch 6.8, 7.2, 7.5, en 7.6.<!--MCLOUD-4050, MCLOUD-5855,MCLOUD-5860-->

      - Toegevoegd de capaciteit om de [ de containerconfiguratie van de Elasticsearch ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#elasticsearch-container) aan te passen wanneer u het Docker samenstelt configuratiedossier produceert.<!--MCLOUD-3059-->

      - De optie `--no-es` is toegevoegd aan de opties voor serviceconfiguratie voor het genereren van het configuratiebestand Docker Compose. Gebruik deze optie om de containerinstallatie van de Elasticsearch over te slaan en in plaats daarvan MySQL-zoekopdracht te gebruiken. Deze optie wordt slechts gesteund voor versies 2.3.5 van Adobe Commerce en vroeger.<!--MCLOUD-3766-->

   - ![ nieuw pictogram ](../../assets/new.svg) **FPM-XDEBUG container** - voegde een optie van de de dienstconfiguratie toe om Xdebug voor het zuiveren PHP in uw milieu van het Dok van de Wolk te installeren en te vormen. Zie [ Xdebug ](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/) vormen.<!--MCLOUD-4098-->

- ![ nieuw pictogram ](../../assets/new.svg) **de configuratieveranderingen van de Docker**

   - Toegevoegde gezondheidscontroles voor PHP-FPM, Redis, Elasticsearch, en MySQL de dienstcontainers van de Dok.<!--MCLOUD-3335 and MCLOUD-5856-->

   - Veranderde standaardwijze van de dossiersynchronisatie in `native` op de wijze van de Ontwikkelaar.<!--MCLOUD-3890 -->

   - Versieinformatie toegevoegd aan de generieke afbeelding van de de dienstcontainer van de Docker wanneer het produceren van het `docker-compose.yml` dossier.<!--MCLOUD-3878-->

   - Verbeterde capaciteit om grote reacties van de stroomopwaartse container te behandelen PHP-FPM door de `fastcgi_buffers` waarde voor de server van Nginx te verhogen.<!--MCLOUD-5980-->

   - Verbeterde synchronisatieprestaties voor bestanden met mutagene verbindingen door een tweede synchronisatiesessie toe te voegen om bestanden in de map `vendor` te synchroniseren. Deze wijziging voorkomt dat mutageen vastzit tijdens het synchronisatieproces van het bestand. [ Repareren die door Mathew Beane van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/127) wordt voorgelegd.<!--MCLOUD-6010-->

   - ![ nieuwe pictogram ](../../assets/new.svg) **CLI bevelupdates**

| Handeling | Opdracht |
| -------- | --------------- |
| Redis-cache wissen | `bin/magento-docker flush-redis` |
| Varnish-cache wissen | `bin/magento-docker flush-varnish` |
| De standaardinstallatie van Varnish overslaan | `.vendor/bin/ece-docker build:compose --no-varnish`<!--MCLOUD-2634--> |
| [ pas Elasticsearch opties ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#elasticsearch-container) aan | `.vendor/bin/ece-docker build:compose --es-env-var`<!--MCLOUD-3059--> |
| [ verwijdert de configuratie van de Elasticsearch ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#elasticsearch-container) | `.vendor/bin/ece-docker build:compose --no-es`<!--MCLOUD-3766--> |
| DB-container configureren met MySQL versie 5.6 of 5.7 | `./vendor/bin/ece-docker build:compose --db <mysql-version-number> --db-image mysql`<!--MCLOUD-5691--> |
| Aangepaste basis-URL opgeven | `./vendor/bin/ece-docker build:compose --host=<hostname> --port=<port-number>`<!--MCLOUD-3063--> |
| [ voeg container voor configuratie Xdebug ](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/) toe | `.vendor/bin/ece-docker build:compose --mode developer --sync-engine native --with-xdebug`<!--MCLOUD-4098--> |

- ![ fixpictogram ](../../assets/fix.svg) Vaste de configuratie van mutagene dossiersynchronisatie om mutageen te verhinderen stapelzittingen te creëren. [ Repareren die door Mathew Beane van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/127) wordt voorgelegd.<!--MCLOUD-6010-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een configuratiekwestie die syntaxisfouten in Docker veroorzaakte stelt logboek samen wanneer het beginnen van de PHP-FPM container. [ Repareren die door Mathew Beane van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/129) wordt voorgelegd <!--MCLOUD-3958-->

- ![ het pictogram van de moeilijke situatie ](../../assets/fix.svg) Vaste de fouten van het volumenconflict die soms voorkwamen wanneer het gebruiken van de veelvoudige milieu&#39;s van het Dok. [ Reparatie die door G Arvind van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/168) wordt voorgelegd.

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die het `ece-docker build:compose` bevel veroorzaakte om te ontbreken als de configuratie Blackfire.io omvatte. [ Repareren die door G Arvind van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/199) wordt voorgelegd. <!--MCLOUD-5797-->

- ![ herstellingspictogram ](../../assets/fix.svg) werkte PHP CLI beeldconfiguratie bij om uit-van-geheugenfouten te verhinderen die voorkwamen wanneer het installeren van veelvoudige pakketten gebruikend de Dekker van de Wolk voor Commerce. [ Reparatie die door Mohan Elamurugan van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/197) wordt voorgelegd.* <!--MCLOUD-5818-->

- ![ fixpictogram ](../../assets/fix.svg) Toegevoegde steun voor veelvoudige gebruikers MySQL in het milieu van het Dok van de Wolk. In eerdere versies is de bewerking `build:compose` mislukt als in het `magento.app.yaml` -bestand meerdere databasegebruikers zijn opgegeven. [ Repareren die door G Arvind van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/181) wordt voorgelegd.<!--MCLOUD-5670-->

- ![ fixpictogram ](../../assets/fix.svg) Verwijderd `rsyslog` uit het Dok van de Wolk voor de containers van Commerce PHP om verenigbaarheidskwesties op te lossen die waarschuwingsberichten tijdens plaatsing veroorzaakten. Cloud Docker gebruikt het hulpprogramma rsyslog niet.<!--MCLOUD-6173-->

## v1.0.0

Releasedatum: 5 februari 2020

- ![ nieuw pictogram ](../../assets/new.svg) **creeerde een afzonderlijk pakket om`Cloud Docker for Commerce`** te leveren - Verplaatst de broncode om het Dok van de Wolk voor Commerce van de `ece-tools` bewaarplaats aan de [ nieuwe `magento-cloud-docker` bewaarplaats ](https://github.com/magento/magento-cloud-docker) te leveren om codekwaliteit te handhaven en onafhankelijke versies te verstrekken. Het nieuwe pakket is afhankelijk van ECE-Tools v2002.1.0 en hoger.

  Wanneer u bureaubladgereedschappen bijwerkt, werkt u het pakket `magento/magento-cloud-docker` ook bij naar versie 1.0.0. Als u Docker van de Wolk voor Commerce met een vroegere `ece-tools` versie (2002.0.x) gebruikte, herzie [ achterwaartse onverenigbaarheden ](backward-incompatible-changes.md) en werk uw project als manuscripten, bevelen, en processen zoals nodig bij.

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde versioning aan de beelden van de Dok** - u moet nu het `magento/magento-cloud-docker` pakket bijwerken om de bijgewerkte beelden te krijgen.<!--MAGECLOUD-4737-->

- ![ nieuw pictogram ](../../assets/new.svg) **de updates van de Container**—

   - ![ nieuw pictogram ](../../assets/new.svg) **PHP-FPM container** -

      - ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde steun Node.js** - werkte het beeld PHP-FPM bij om knoop, npm, en de grot-cli mogelijkheden binnen de PHP container te steunen.<!--MAGECLOUD-3953-->

      - ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde steun voor [ ionCube ](https://www.ioncube.com/)** - werkte de standaardconfiguratie van Docker bij om IonCube in het lokale de ontwikkelingsmilieu van de Dok te steunen.<!--MAGECLOUD-4354-->

   - ![ nieuw pictogram ](../../assets/new.svg) **container van het Web** -

      - ![ nieuw pictogram ](../../assets/new.svg) **pas NGINX configuratie** toe - voegde het vermogen toe om een douane `nginx.conf` dossier aan het Dok van de Wolk voor het milieu van Commerce op te zetten. Zie {de container van 0} Web ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#web-container).<!--MAGECLOUD-4204-->[

      - ![ nieuw pictogram ](../../assets/new.svg) **Auto-geproduceerde NGINX certificaten** - het de configuratiedossier van de Docker omvat nu de configuratie om NGINX certificaten voor de container van het Web auto-te produceren.<!--MAGECLOUD-4258-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Nieuwe container van Selenium** - Toegevoegd a [ container van Selenium ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#selenium-container) om de toepassing van Adobe Commerce te steunen die het Magento het Functionele Testen Kader (MFTF) testen.<!--MAGECLOUD-4040-->

   - ![ nieuw pictogram ](../../assets/new.svg) **[!DNL RabbitMQ]versiessteun** - werkte de [!DNL RabbitMQ] containerconfiguratie bij om [!DNL RabbitMQ] versie 3.8 te steunen.<!--MAGECLOUD-4674-->

   - ![ bevestigen pictogram ](../../assets/fix.svg) **Persistent gegevensbestandcontainer** - het `magento-db: /var/lib/mysql` gegevensbestandvolume blijft nu na u tegenhouden en verwijdert de configuratie van de Dokker en herstelt wanneer u de configuratie van de Dokker opnieuw begint. Nu moet u het databasevolume handmatig verwijderen. Zie [ containers van het Gegevensbestand ].<!--MAGECLOUD-3978-->

   - ![ nieuw pictogram ](../../assets/new.svg) **container TLS** -

      - ![ nieuw pictogram ](../../assets/new.svg) **werkte het beeld van de containerbasis bij om officieel beeld** te gebruiken - het [ de container van TLS van de Wolk ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#tls-container) beeld is nu gebaseerd op het officiële `debian:jessie` beeld van het Docker.—<!--MAGECLOUD-4163-->

      - ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegde steun voor de [ Gevonden Volgorde van de Beëindiging TLS]** - het [ Pond configuratiedossier ](https://github.com/magento/magento-cloud-docker/blob/1.0/images/tls/) voegt de volgende variabelen toe ENV om de configuratie van de Dok voor de container aan te passen TLS:

         - **`TimeOut`** - Stelt de time-outwaarde voor Tijd in op Eerste byte (TTFB). De standaardwaarde is 300 seconden.

         - **`RewriteLocation`** - Hiermee wordt bepaald of de proxy Pond de locatie standaard herschrijft naar de aanvraag-URL. Wordt standaard ingesteld op `0` om te voorkomen dat bij het herschrijven de omleiding naar externe websites, zoals een externe SSO-site, wordt verbroken. [ Repareren die door Sorin wordt voorgelegd Suiker ](https://github.com/magento/magento-cloud-docker/pull/37) <!--MAGECLOUD-4061-->

      - ![ nieuw pictogram ](../../assets/new.svg) verhoogde de onderbrekingswaarde in de de containerconfiguratie van TLS van 15 tot 300 seconden. [ Repareren die door Mathew Beane van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/78) wordt voorgelegd <!--MAGECLOUD-4460-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Varnish container** -

      - ![ nieuw pictogram ](../../assets/new.svg) **werkte het beeld van de containerbasis bij om officieel beeld** te gebruiken - de [ container van de Vlek van de Wolk ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service/#varnish-container) is nu gebaseerd op het officiële `centos` beeld van het Docker.<!--MAGECLOUD-4163-->

      - ![ nieuw pictogram ](../../assets/new.svg) **Verbeterde standaardonderbrekingsconfiguratie** - toegevoegd `.first_byte_timeout` en `.between_bytes_timeout` configuratie aan de container van de Varnish. Beide time-outwaarden zijn standaard ingesteld op `300s` (5 minuten). [ Repareren die door Mathew Beane van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/78) wordt voorgelegd <!--MAGECLOUD-4460-->

      - ![ herstellingspictogram ](../../assets/fix.svg) **Skip Varnish tijdens zittingen Xdebug** - werkte de de containerconfiguratie van de Varnish bij om `pass` op ontvangen verzoeken terug te keren wanneer Xdebug wordt toegelaten. In vorige versies kon u geen Xdebug gebruiken als Varnish in de Docker-omgeving was opgenomen. [ Repareren die door Mathew Beane van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/111) wordt voorgelegd.<!--MAGECLOUD-4873-->

- ![ nieuw pictogram ](../../assets/new.svg) **de configuratieveranderingen van de Docker**—

   - ![ nieuw pictogram ](../../assets/new.svg) **beheert steunen en volumes voor uw project** - toegevoegd de capaciteit om steunen en volumes te beheren wanneer het lanceren van een milieu van de Dok voor lokale ontwikkeling. Zie [ het Delen van projectgegevens ].<!--MAGECLOUD-3248-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Steun voor de wijze van de netwerkbrug** - Toegevoegde steun voor de wijze van de netwerkbrug om verbindingen tussen de containers van de Dok over het lokale netwerk toe te laten.<!--MAGECLOUD-4165-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Uitsnijdcontainer gehandicapt door gebrek** - om prestaties te verbeteren, wordt de container van het Gewas niet meer gevormd door gebrek wanneer u het milieu van de Docker bouwt. Met de optie `--with-cron` in de constructieopdracht Docker kunt u een container voor uitsnijden aan uw omgeving toevoegen. Zie [ het Leiden kroonbanen ](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/).<!--MAGECLOUD-5181-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Einde synchroniserend grote reservedossiers** - Toegevoegde de stortplaatsen van DB en archiefdossiers-ZIP, SQL, GZ, en BZ2-aan de uitsluitingslijst in `dist/docker-sync.yml` en `dist/mutagen.sh` dossiers. Het synchroniseren van grote dossiers (>1 GB) kan een periode van inactiviteit veroorzaken en de reservedossiers vereisen normaal geen synchronisatie aangezien u hen kunt regenereren.<!--MAGECLOUD-3979-->

- ![ nieuw pictogram ](../../assets/new.svg) **de veranderingen van het Bevel** -

   - ![ herstellingspictogram ](../../assets/fix.svg) hernoemde het `./bin/docker` dossier aan `./bin/magento-docker` om een kwestie te bevestigen die sommige milieu&#39;s van het Docker aan onderbreking veroorzaakte omdat het `./bin/docker` dossier bestaande binaire dossiers van het Docker beschrijft. Dit is a [ achteruit onverenigbare verandering ](backward-incompatible-changes.md) die updates aan uw manuscripten en bevelen vereist.<!-- MAGECLOUD-4038 -->

   - ![ nieuw pictogram ](../../assets/new.svg) **voegde een optie van de de dienstconfiguratie toe om de gegevensbestandhaven aan de gastheer** bloot te stellen - gebruik de `--expose-db-port= [Fix submitted by Adarsh Manickam from Zilker Technology](https://github.com/magento/magento-cloud-docker/pull/101).<PORT>` optie om de gegevensbestandhaven aan de gastheer bloot te stellen wanneer het bouwen van het `docker-compose.yml` dossier: `bin/ece-docker build:compose --expose-db-port=<PORT>`<!--MAGECLOUD-4454-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Nieuw post-stelt bevel** op - eerder, post-stelt haken die in het `.magento.app.yaml` dossier worden bepaald automatisch in werking nadat u Adobe Commerce aan een container van het Dok van de Wolk gebruikend het `cloud-deploy` bevel opstelde. Nu moet u een aparte opdracht `cloud-post-deploy` geven om de koppelingen na de implementatie uit te voeren. Zie de bijgewerkte lanceringsinstructies voor [ ontwikkelaar ](https://developer.adobe.com/commerce/cloud-tools/docker/deploy/developer-mode/) en [ productie ](https://developer.adobe.com/commerce/cloud-tools/docker/deploy/production-mode/) wijze.<!--MAGECLOUD-3996-->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde de `--rm` optie aan `./bin/magento-docker` bevelen voor de bouwstijl toe en stel containers op. Dit verwijdert de container nadat de taak volledig is.<!--MAGECLOUD-4205-->

   - ![ nieuw pictogram ](../../assets/new.svg) **Updates aan `build:compose` bevel**—

      - ![ nieuw pictogram ](../../assets/new.svg) voegde de `--sync-engine="native"` optie aan het `docker-build` bevel toe om dossiersynchronisatie onbruikbaar te maken wanneer u het Docker samenstelt configuratiedossier op ontwikkelaarwijze produceert. Gebruik deze optie bij het ontwikkelen op Linux-systemen, waarvoor geen bestandssynchronisatie is vereist voor lokale Docker-ontwikkeling. Zie [ Synchroniserend gegevens in het milieu van de Dokker ](https://developer.adobe.com/commerce/cloud-tools/docker/setup/synchronize-data/).<!--MCLOUD-3231, MCLOUD-3890-->

   - ![ nieuw pictogram ](../../assets/new.svg) veranderde standaarddossiersynchronisatie die van `docker-sync` aan `native` werd geplaatst. [ Repareren die door Mathew Beane van de Technologie van Zilker ](https://github.com/magento/magento-cloud-docker/pull/124) wordt voorgelegd.<!--MAGECLOUD-5066-->

- ![ nieuw pictogram ](../../assets/new.svg) **de verbeteringen van de Bevestiging** -

   - ![ nieuw pictogram ](../../assets/new.svg) Toegevoegde bevestiging aan het plaatsingsproces voor lokale de ontwikkelomgevingen van de Docker om te verifiëren dat de het omgevingsconfiguratie van de Wolk de encryptiesleutel omvat die wordt vereist om het gegevensbestand te decrypteren. Nu, krijgt u een foutenmelding in het logboek als de milieuconfiguratie geen waarde voor de encryptiesleutel specificeert.<!--MAGECLOUD-4423-->

   - ![ nieuw pictogram ](../../assets/new.svg) voegde een controle van de containergezondheid aan de dienst van de Elasticsearch toe om ervoor te zorgen dat de dienst klaar is alvorens met bouwstijl voort te gaan en verwerking op te stellen. Als de gezondheidscontrole een fout terugkeert, begint de container automatisch opnieuw.<!--MAGECLOUD-4456-->
