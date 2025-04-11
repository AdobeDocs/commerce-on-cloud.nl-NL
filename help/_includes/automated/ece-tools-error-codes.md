---
source-git-commit: 350cfea06f036f0787b330e6e40c5af46a30f5ad
workflow-type: tm+mt
source-wordcount: '2554'
ht-degree: 4%

---
# ECE-gereedschappen, foutcodes

<!--Note: The error code tables in this file are auto-generated from source code. To request changes to error code descriptions or suggestions, submit a GitHub issue to the magento/ece-tools repository.-->

## Kritieke fouten

Kritieke fouten wijzen op een probleem met Commerce op de projectconfiguratie van de wolkeninfrastructuur die plaatsingsmislukking veroorzaakt, bijvoorbeeld onjuiste, niet gestaafde, of ontbrekende configuratie voor vereiste montages. Voordat u kunt implementeren, moet u de configuratie bijwerken om deze fouten op te lossen.

### Werkgebied bouwen

| Foutcode | Stap maken | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 2 |  | Kan niet schrijven naar het `./app/etc/env.php` -bestand | Implementatiescript kan geen vereiste wijzigingen aanbrengen in het `/app/etc/env.php` -bestand. Controleer de bestandssysteemmachtigingen. |
| 3 |  | Configuration is not defined in the `schema.yaml` file | Configuration is not defined in the `./vendor/magento/ece-tools/config/schema.yaml` file. Controleer of de naam van de configuratievariabele correct en bepaald is. |
| 4 |  | Kan het bestand `.magento.env.yaml` niet parseren | Het `./.magento.env.yaml` bestandsformaat is ongeldig. Gebruik een YAML-parser om de syntaxis te controleren en eventuele fouten op te lossen. |
| 5 |  | Kan het `.magento.env.yaml` bestand niet lezen | Kan het `./.magento.env.yaml` bestand niet lezen. Controleer de bestandsmachtigingen. |
| 6 |  | Kan het `.schema.yaml` bestand niet lezen | Kan het `./vendor/magento/ece-tools/config/magento.env.yaml` bestand niet lezen. Controleer de bestandsrechten en implementeer opnieuw (`magento-cloud environment:redeploy`). |
| 7 | Refresh-modules | Kan niet schrijven naar het `./app/etc/config.php` -bestand | Het implementatiescript kan geen vereiste wijzigingen aanbrengen in het `/app/etc/config.php` -bestand. Controleer de bestandssysteemmachtigingen. |
| 8 | validate-config | Kan het `composer.json` -bestand niet lezen | Kan het `./composer.json` -bestand niet lezen. Controleer de bestandsmachtigingen. |
| 9 | validate-config | De sectie Automatisch laden van het bestand `composer.json` ontbreekt | De sectie Required `autoload` ontbreekt in het `composer.json` -bestand. Vergelijk de sectie Automatisch laden met het `composer.json` -bestand in de Cloud-sjabloon en voeg de ontbrekende configuratie toe. |
| 10 | validate-config | Het bestand `.magento.env.yaml` bevat een optie die niet in het schema is gedeclareerd of een optie die is geconfigureerd met een ongeldige waarde of een ongeldig werkgebied | Het bestand `./.magento.env.yaml` bevat een ongeldige configuratie. Controleer het foutenlogboek voor gedetailleerde informatie. |
| 11 | verfrissingsmodules | Opdracht is mislukt: `/bin/magento module:enable --all` | Voer `composer update` lokaal uit. Vervolgens legt u het bijgewerkte `composer.lock` -bestand vast en drukt u erop. Raadpleeg ook `cloud.log` voor meer informatie. Voeg de optie `VERBOSE_COMMANDS: '-vvv'` toe aan het `.magento.env.yaml` -bestand voor meer gedetailleerde uitvoer van opdrachten. |
| 12 | toepassen-patches | Kan patch niet toepassen |  |
| 13 | set-report-dir-nesting-level | Kan niet schrijven naar het bestand `/pub/errors/local.xml` |  |
| 14 | kopiëren-voorbeeld-gegevens | Kan voorbeeldgegevensbestanden niet kopiëren |  |
| 15 | compile-di | Opdracht is mislukt: `/bin/magento setup:di:compile` | Raadpleeg `cloud.log` voor meer informatie. Voeg `VERBOSE_COMMANDS: '-vvv'` toe aan `.magento.env.yaml` voor meer gedetailleerde opdrachtuitvoer. |
| 16 | dump-autoload | Opdracht is mislukt: `composer dump-autoload` | De opdracht `composer dump-autoload` is mislukt. Raadpleeg `cloud.log` voor meer informatie. |
| 17 | renbaan | Het uitvoeren van de opdracht `Baler` voor JavaScript-bundeling is mislukt | Controleer de `SCD_USE_BALER` omgevingsvariabele om te controleren of de Baler-module is geconfigureerd en ingeschakeld voor JS-bundeling. Stel `SCD_USE_BALER: false` in als u de module Baler niet nodig hebt. |
| 18 | compress-static-content | Vereist hulpprogramma niet gevonden (timeout, bash) |  |
| 19 | implementatie-statische inhoud | Opdracht `/bin/magento setup:static-content:deploy` mislukt | Kijk op de `cloud.log` voor meer informatie. Voeg de `VERBOSE_COMMANDS: '-vvv'` optie toe aan het `.magento.env.yaml` bestand voor een meer gedetailleerde opdrachtuitvoer. |
| 20 | comprimeren-statische-inhoud | Statische inhoudscompressie is mislukt | Raadpleeg `cloud.log` voor meer informatie. |
| 21 | Back-upgegevens: statische inhoud | Kan statische inhoud niet naar de `init` map kopiëren | Kijk op de `cloud.log` voor meer informatie. |
| 22 | back-upgegevens: schrijfbare dirs | Kan sommige beschrijfbare mappen niet kopiëren naar de map `init` . | Kan beschrijfbare mappen niet naar de map `./init` kopiëren. Controleer de bestandssysteemmachtigingen. |
| 23 |  | Kan geen logboekobject maken |  |
| 24 | back-upgegevens: statische inhoud | Kan de map `./init/pub/static/` niet opschonen | Kan de map `./init/pub/static` niet opschonen. Controleer de bestandssysteemmachtigingen. |
| 25 |  | Kan het Composer-pakket niet vinden | Als u de Adobe Commerce-toepassingsversie rechtstreeks hebt geïnstalleerd vanuit de GitHub-opslagplaats, controleert u of de `DEPLOYED_MAGENTO_VERSION_FROM_GIT` -omgevingsvariabele is geconfigureerd. |
| 26 | validate-config | Magento Braintree-moduleconfiguratie verwijderen die niet meer wordt ondersteund in Adobe Commerce en Magento Open Source 2.4 en latere versies. | Ondersteuning voor de Braintree-module is niet meer inbegrepen bij Magento 2.4.0 en hoger. Verwijder de variabele CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL uit de sectie variables van het `.magento.app.yaml` bestand. Gebruik in plaats daarvan een officiële extensie van de Commerce Marketplace voor Braintree-betalingsondersteuning. |

### Werkgebied implementeren

| Foutcode | Stap implementeren | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 101 | vooraf implementeren: cache | Onjuiste cacheconfiguratie (ontbrekende poort of host) | De vereiste parameters `server` of `port` ontbreken in de cacheconfiguratie. Raadpleeg `cloud.log` voor meer informatie. |
| 102 |  | Kan niet schrijven naar het `./app/etc/env.php` -bestand | Implementatiescript kan geen vereiste wijzigingen aanbrengen in het `/app/etc/env.php` -bestand. Controleer de bestandssysteemmachtigingen. |
| 103 |  | Configuration is not defined in the `schema.yaml` file | Configuration is not defined in the `./vendor/magento/ece-tools/config/schema.yaml` file. Controleer of de naam van de configuratievariabele correct is en of deze is gedefinieerd. |
| 104 |  | Kan het bestand `.magento.env.yaml` niet parseren | Configuration is not defined in the `./vendor/magento/ece-tools/config/schema.yaml` file. Controleer of de naam van de configuratievariabele correct is en of deze is gedefinieerd. |
| 105 |  | Kan het bestand `.magento.env.yaml` niet lezen | Kan het `./.magento.env.yaml` -bestand niet lezen. Controleer de bestandsmachtigingen. |
| 106 |  | Kan het bestand `.schema.yaml` niet lezen |  |
| 107 | vooraf implementeren: clean-redis-cache | Kan de Redis-cache niet opschonen | Kan de Redis-cache niet opschonen. Controleer of de cachemonfiguratie van Redis correct is en of de service Redis beschikbaar is. Zie [ Redis de dienst van de Opstelling ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/service/redis). |
| 140 | Vooraf implementeren: clean-valkey-cache | Kan de Valkey-cache niet opschonen | Kan de Valkey-cache niet opschonen. Controleer of de Valkey-cacheconfiguratie correct is en of de Valkey-service beschikbaar is. Zie [Valkey-service](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/service/valkey) instellen. |
| 108 | pre-implementatie: set-production-mode | Opdracht `/bin/magento maintenance:enable` mislukt | Raadpleeg `cloud.log` voor meer informatie. Voeg de optie `VERBOSE_COMMANDS: '-vvv'` toe aan het `.magento.env.yaml` -bestand voor meer gedetailleerde uitvoer van opdrachten. |
| 109 | validate-config | Onjuiste databaseconfiguratie | Controleer of de `DATABASE_CONFIGURATION` omgevingsvariabele correct is geconfigureerd. |
| 110 | validate-config | Onjuiste sessieconfiguratie | Controleer of de omgevingsvariabele `SESSION_CONFIGURATION` correct is geconfigureerd. De configuratie moet ten minste de parameter `save` bevatten. |
| 111 | validate-config | Onjuiste zoekconfiguratie | Controleer of de omgevingsvariabele `SEARCH_CONFIGURATION` correct is geconfigureerd. De configuratie moet ten minste de parameter `engine` bevatten. |
| 112 | validate-config | Onjuiste bronconfiguratie | Controleer of de omgevingsvariabele `RESOURCE_CONFIGURATION` correct is geconfigureerd. De configuratie moet ten minste `connection` parameter bevatten. |
| 113 | validate-config:elasticsuite-integriteit | ElasticSuite is geïnstalleerd, maar de Elasticsearch-service is niet beschikbaar | Controleer of de omgevingsvariabele `SEARCH_CONFIGURATION` correct is geconfigureerd en of de Elasticsearch-service beschikbaar is. |
| 114 | validate-config:elasticsuite-integriteit | ElasticSuite is geïnstalleerd, maar er wordt een andere zoekmachine gebruikt | ElasticSuite is geïnstalleerd, maar een andere zoekmachine is geconfigureerd. Werk de omgevingsvariabele `SEARCH_CONFIGURATION` bij om Elasticsearch in te schakelen en controleer de configuratie van de Elasticsearch-service in het `services.yaml` -bestand. |
| 115 |  | Uitvoering van databasequery mislukt |  |
| 116 | install-update: setup | Opdracht `/bin/magento setup:install` mislukt | Raadpleeg `cloud.log` en `install_upgrade.log` voor meer informatie. Voeg de optie `VERBOSE_COMMANDS: '-vvv'` toe aan het `.magento.env.yaml` -bestand voor meer gedetailleerde uitvoer van opdrachten. |
| 117 | install-update: config-import | Opdracht `app:config:import` mislukt | Raadpleeg `cloud.log` voor meer informatie. Voeg de optie `VERBOSE_COMMANDS: '-vvv'` toe aan het `.magento.env.yaml` -bestand voor meer gedetailleerde uitvoer van opdrachten. |
| 118 |  | Vereist hulpprogramma niet gevonden (timeout, bash) |  |
| 119 | install-update: implementatie-static-content | Opdracht `/bin/magento setup:static-content:deploy` mislukt | Raadpleeg `cloud.log` voor meer informatie. Voeg de optie `VERBOSE_COMMANDS: '-vvv'` toe aan het `.magento.env.yaml` -bestand voor meer gedetailleerde uitvoer van opdrachten. |
| 120 | compress-static-content | Statische inhoudscompressie is mislukt | Raadpleeg `cloud.log` voor meer informatie. |
| 121 | implementeren-statische inhoud:genereren | Kan de geïmplementeerde versie niet bijwerken | Kan het `./pub/static/deployed_version.txt` -bestand niet bijwerken. Controleer de bestandssysteemmachtigingen. |
| 122 | zuiver-statische inhoud | Kan bestanden met statische inhoud niet opschonen |  |
| 123 | install-update: split-db | Opdracht `/bin/magento setup:db-schema:split` mislukt | Raadpleeg `cloud.log` voor meer informatie. Voeg de optie `VERBOSE_COMMANDS: '-vvv'` toe aan het `.magento.env.yaml` -bestand voor meer gedetailleerde uitvoer van opdrachten. |
| 124 | onbewerkt | Kan de map `var/view_preprocessed` niet opschonen | Kan de `./var/view_preprocessed` map niet opschonen. Controleer de bestandssysteemmachtigingen. |
| 125 | install-update: reset-password | Kan het `/var/credentials_email.txt` -bestand niet bijwerken | Kan het `/var/credentials_email.txt` -bestand niet bijwerken. Controleer de bestandssysteemmachtigingen. |
| 126 | install-update: update | Opdracht `/bin/magento setup:upgrade` mislukt | Raadpleeg `cloud.log` en `install_upgrade.log` voor meer informatie. Voeg de optie `VERBOSE_COMMANDS: '-vvv'` toe aan het `.magento.env.yaml` -bestand voor meer gedetailleerde uitvoer van opdrachten. |
| 127 | schone cache | Opdracht `/bin/magento cache:flush` mislukt | Raadpleeg `cloud.log` voor meer informatie. Voeg de optie `VERBOSE_COMMANDS: '-vvv'` toe aan het `.magento.env.yaml` -bestand voor meer gedetailleerde uitvoer van opdrachten. |
| 128 | uit-onderhoud-modus | Opdracht `/bin/magento maintenance:disable` mislukt | Raadpleeg `cloud.log` voor meer informatie. Voeg `VERBOSE_COMMANDS: '-vvv'` toe aan `.magento.env.yaml` voor meer gedetailleerde opdrachtuitvoer. |
| 129 | install-update: reset-password | Kan de sjabloon voor opnieuw instellen van wachtwoord niet lezen |  |
| 130 | install-update: cache_type | Opdracht is mislukt: `php ./bin/magento cache:enable` | Opdracht `php ./bin/magento cache:enable` wordt alleen uitgevoerd wanneer Adobe Commerce is geïnstalleerd, maar het `./app/etc/env.php` -bestand is niet aanwezig of leeg aan het begin van de implementatie. Raadpleeg `cloud.log` voor meer informatie. Voeg `VERBOSE_COMMANDS: '-vvv'` toe aan `.magento.env.yaml` voor meer gedetailleerde opdrachtuitvoer. |
| 131 | installeren-bijwerken | De waarde van de sleutel `crypt/key` bestaat niet in het `./app/etc/env.php` -bestand of de omgevingsvariabele van de cloud`CRYPT_KEY` | Deze fout treedt op als het `./app/etc/env.php` -bestand niet aanwezig is wanneer de Adobe Commerce-implementatie begint of als de `crypt/key` -waarde ongedefinieerd is. Als u de database uit een andere omgeving hebt gemigreerd, haalt u de waarde van de cryptsleutel uit die omgeving op. Dan, voeg de waarde aan [ CRYPT_KEY ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure/env/stage/variables-deploy#crypt_key) de variabele van het wolkenmilieu in uw huidig milieu toe. Zie [ de encryptiesleutel van Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/overview#gather-credentials). Als u per ongeluk het `./app/etc/env.php` -bestand hebt verwijderd, gebruikt u de volgende opdracht om het bestand te herstellen van de back-upbestanden die zijn gemaakt op basis van een vorige implementatie: `./vendor/bin/ece-tools backup:restore` CLI-opdracht.&quot; |
| 132 |  | Kan geen verbinding maken met de Elasticsearch-service | Controleren op geldige Elasticsearch-referenties en controleren of de service wordt uitgevoerd |
| 137 |  | Kan geen verbinding maken met de OpenSearch-service | Controleren op geldige OpenSearch-referenties en controleren of de service wordt uitgevoerd |
| 133 | validate-config | Magento Braintree-moduleconfiguratie verwijderen die niet meer wordt ondersteund in Adobe Commerce of Magento Open Source 2.4 en latere versies. | Ondersteuning voor de Braintree-module is niet meer inbegrepen bij Adobe Commerce of Magento Open Source 2.4.0 en hoger. Verwijder de variabele CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL uit de sectie variables van het `.magento.app.yaml` bestand. Gebruik voor Braintree-ondersteuning een officiële Braintree Payments-extensie van de Commerce Marketplace. |
| 134 | validate-config | Adobe Commerce en Magento Open Source 2.4.0 vereisen dat de Elasticsearch-service wordt geïnstalleerd | Elasticsearch-service installeren |
| 138 | validate-config | Adobe Commerce en Magento Open Source 2.4.4 vereisen dat de OpenSearch- of Elasticsearch-service wordt geïnstalleerd | OpenSearch-service installeren |
| 135 | validate-config | Het zoekprogramma moet op Elasticsearch for Adobe Commerce en Magento Open Source zijn ingesteld >= 2.4.0 | Controleer de variabele SEARCH_CONFIGURATION op de optie `engine` . Als het wordt gevormd, verwijder de optie, of plaats de waarde aan &quot;elasticsearch&quot;. |
| 136 | validate-config | Splitste database is verwijderd vanaf Adobe Commerce en Magento Open Source 2.5.0. | Als u een gesplitste database gebruikt, moet u terugkeren naar of migreren naar één database of een alternatieve benadering gebruiken. |
| 139 | validate-config | Onjuiste zoekfunctie | Deze Adobe Commerce- of Magento Open Source-versie biedt geen ondersteuning voor OpenSearch. Gebruik versies 2.3.7-p3, 2.4.3-p2 of hoger |

### Positie na implementatie

| Foutcode | Stap na implementatie | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 201 | is-implementatie-mislukt | Werkgebied implementeren is mislukt |  |
| 202 |  | Het bestand `./app/etc/env.php` is niet beschrijfbaar | Implementatiescript kan geen vereiste wijzigingen aanbrengen in het `/app/etc/env.php` -bestand. Controleer de bestandssysteemmachtigingen. |
| 203 |  | Configuration is not defined in the `schema.yaml` file | Configuration is not defined in the `./vendor/magento/ece-tools/config/schema.yaml` file. Controleer of de naam van de configuratievariabele correct is en of deze is gedefinieerd. |
| 204 |  | Kan het bestand `.magento.env.yaml` niet parseren | De bestandsindeling `./.magento.env.yaml` is ongeldig. Gebruik een parser YAML om de syntaxis te controleren en om het even welke fouten te bevestigen. |
| 205 |  | Kan het bestand `.magento.env.yaml` niet lezen | Controleer de bestandsmachtigingen. |
| 206 |  | Kan het bestand `.schema.yaml` niet lezen |  |
| 207 | opwarmen | Voorladen van enkele opwarmpagina&#39;s is mislukt |  |
| 208 | time-to-firs-byte | Kan tijd naar eerste byte (TTFB) niet testen |  |
| 227 | schone cache | Opdracht `/bin/magento cache:flush` mislukt | Raadpleeg `cloud.log` voor meer informatie. Voeg `VERBOSE_COMMANDS: '-vvv'` toe aan `.magento.env.yaml` voor meer gedetailleerde opdrachtuitvoer. |

### Algemeen

| Foutcode | Algemene stap | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 243 |  | Configuration is not defined in the `schema.yaml` file | Controleer of de naam van de configuratievariabele correct is en of deze is gedefinieerd. |
| 244 |  | Kan het bestand `.magento.env.yaml` niet parseren | De bestandsindeling `./.magento.env.yaml` is ongeldig. Gebruik een parser YAML om de syntaxis te controleren en om het even welke fouten te bevestigen. |
| 245 |  | Kan het bestand `.magento.env.yaml` niet lezen | Kan het `./.magento.env.yaml` -bestand niet lezen. Controleer de bestandsmachtigingen. |
| 246 |  | Kan het bestand `.schema.yaml` niet lezen |  |
| 247 |  | Kan geen module voor gebeurtenissen genereren | Raadpleeg `cloud.log` voor meer informatie. |
| 248 |  | Kan een module voor gebeurtenissen niet inschakelen | Raadpleeg `cloud.log` voor meer informatie. |
| 249 |  | Kan de module AdobeCommerceWebhoogins niet genereren | Raadpleeg `cloud.log` voor meer informatie. |
| 250 |  | Kan de module AdobeCommerceWebhoogins niet inschakelen | Raadpleeg `cloud.log` voor meer informatie. |

## Waarschuwingsfouten

Waarschuwingsfouten geven een probleem aan met de Commerce op de projectconfiguratie van de cloud-infrastructuur, zoals onjuiste, vervangen, niet-ondersteunde of ontbrekende configuratie-instellingen voor optionele functies die de sitebewerking kunnen beïnvloeden. Hoewel een waarschuwing geen plaatsingsmislukking veroorzaakt, zou u waarschuwingsberichten moeten herzien en de configuratie bijwerken om hen op te lossen.

### Werkgebied bouwen

| Foutcode | Stap maken | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 1001 | validate-config | Bestand app/etc/config.php bestaat niet |  |
| 1002 | validate-config | De ./build_options.ini-bestand wordt niet meer ondersteund |  |
| 1003 | validate-config | De modulesectie mist van het gedeelde configdossier |  |
| 1004 | validate-config | De configuratie is niet compatibel met deze versie van Magento |  |
| 1005 | validate-config | SCD-opties genegeerd |  |
| 1006 | validate-config | De geconfigureerde status is niet ideaal |  |
| 1007 | renbaan | Baler JS-bundeling kan niet worden gebruikt |  |

### Werkgebied implementeren

| Foutcode | Stap implementeren | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 2001 | vooraf implementeren:cache | Het geheime voorgeheugen wordt gevormd voor de dienst Redis die niet beschikbaar is. Configuratie wordt genegeerd. |  |
| 2032 | vooraf implementeren:cache | Het geheime voorgeheugen wordt gevormd voor de dienst Valkey die niet beschikbaar is. Configuratie wordt genegeerd. |  |
| 2002 | validate-config | De geconfigureerde status is niet ideaal |  |
| 2003 | validate-config | De geneste niveauwaarde van de folder voor fout het melden is niet gevormd |  |
| 2004 | validate-config | Ongeldige configuratie in de ./pub/errors/local.xml. |  |
| 2005 | validate-config | Beheerdersgegevens worden alleen gebruikt om een beheerdersgebruiker te maken tijdens de eerste installatie. Eventuele wijzigingen in beheerdersgegevens worden genegeerd tijdens het upgradeproces. | Na de eerste installatie kunt u de beheergegevens uit de configuratie verwijderen. |
| 2006 | validate-config | Admin-gebruiker is niet gemaakt omdat e-mail met beheerder niet is ingesteld | Na de installatie kunt u handmatig een beheerder maken: gebruik SSH om verbinding te maken met uw omgeving. Voer vervolgens de opdracht `bin/magento admin:user:create` uit. |
| 2007 | validate-config | PHP-versie bijwerken naar aanbevolen versie |  |
| 2008 | validate-config | Solr-ondersteuning is afgekeurd in Adobe Commerce en Magento Open Source 2.1. |  |
| 2009 | validate-config | Solr wordt niet meer ondersteund door Adobe Commerce en Magento Open Source 2.2 of hoger. |  |
| 2010 | validate-config | De dienst van Elasticsearch wordt geïnstalleerd bij de infrastructuurlaag, maar het wordt niet gebruikt als onderzoeksmotor. | U kunt overwegen de Elasticsearch-service uit de infrastructuurlaag te verwijderen om het gebruik van bronnen te optimaliseren. |
| 2011 | validate-config | Elasticsearch-serviceversie op de infrastructuurlaag is niet compatibel met de huidige versie van de elasticsearch/elasticsearch module die door uw Adobe Commerce-toepassing wordt gebruikt. |  |
| 2012 | validate-config | De huidige configuratie is niet compatibel met deze versie van Adobe Commerce |  |
| 2013 | validate-config | SCD opties genegeerd omdat het plaatsingsproces niet op de bouwstijlfase werd in werking gesteld |  |
| 2014 | validate-config | De configuratie bevat vervangen variabelen of waarden |  |
| 2015 | validate-config | Omgevingsconfiguratie is niet geldig |  |
| 2016 | validate-config | Kan JSON-typeconfiguratie niet decoderen |  |
| 2017 | validate-config | De huidige configuratie is niet compatibel met deze versie van Adobe Commerce |  |
| 2018 | validate-config | Sommige services zijn overgegaan tot EOL |  |
| 2019 | validate-config | De MySQL optie van de onderzoeksconfiguratie is verouderd | Gebruik in plaats hiervan Elasticsearch. |
| 2029 | validate-config | Splitste database is vervangen in de Adobe Commerce en Magento Open Source 2.4.2 en wordt verwijderd in 2.5. | Als u een gesplitste database gebruikt, moet u beginnen met het plannen om terug te keren naar of te migreren naar één database of een alternatieve benadering gebruiken. |
| 2020 | installeren-bijwerken | Adobe Commerce-installatie is voltooid, maar het configuratiebestand van `app/etc/env.php` ontbreekt of is leeg. | De vereiste gegevens worden teruggezet vanuit omgevingsconfiguraties en vanuit het bestand .magento.env.yaml. |
| 2021 | install-update:db-connection | Voor gesplitste databases die aangepaste verbindingen gebruiken |  |
| 2022 | install-update:db-connection | U bent veranderd in een gegevensbestandconfiguratie die niet compatibel met de slave verbinding is. |  |
| 2023 | install-update:split-db | Het inschakelen van een gesplitste database wordt overgeslagen. |  |
| 2024 | install-update:split-db | De SPLIT_DB-variabele mist de configuratie voor gesplitste verbindingstypen. |  |
| 2025 | install-update:split-db | Verbinding met slave niet ingesteld. |  |
| 2026 | vooraf implementeren:herschrijfbare dirs | Kan sommige gegevens die tijdens de constructiefase zijn gegenereerd, niet terugzetten naar de gekoppelde directory&#39;s | Raadpleeg `cloud.log` voor meer informatie. |
| 2027 | validate-config:image-mode-variable | Modus value for MAGE_MODE environment variable not supported | Verwijder de MAGE_MODE omgevingsvariabele, of verander zijn waarde in &quot;productie&quot;. Adobe Commerce op cloud-infrastructuur ondersteunt alleen de modus &quot;productie&quot;. |
| 2028 | externe opslag | Externe opslag kan niet worden ingeschakeld. | Verifieer externe opslagreferenties. |
| 2030 | validate-config | Elasticsearch- en OpenSearch-services zijn beide geïnstalleerd op de infrastructuurlaag. Adobe Commerce en Magento Open Source 2.4.4 en hoger gebruiken standaard OpenSearch | U kunt overwegen de Elasticsearch- of OpenSearch-service uit de infrastructuurlaag te verwijderen om het gebruik van bronnen te optimaliseren. |

### Positie na implementatie

| Foutcode | Stap na implementatie | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 3001 | validate-config | Foutopsporingsregistratie is ingeschakeld in Adobe Commerce | Als u schijfruimte wilt besparen, moet u foutopsporingslogboekregistratie niet inschakelen voor uw productieomgevingen. |
| 3002 | opwarmen | OpslagURL&#39;s kunnen niet worden opgehaald |  |
| 3003 | opwarmen | Kan URL winkel niet ophalen |  |
| 3004 | back-up | Kan geen back-upbestanden maken |  |

### Algemeen

| Foutcode | Algemene stap | Foutbeschrijving (titel) | Voorgestelde actie |
| - | - | - | - |
| 4001 |  | Het aantal systeemprocessors kan niet worden opgehaald: |  |
