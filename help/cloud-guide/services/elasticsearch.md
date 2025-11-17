---
title: Elasticsearch-service instellen
description: Leer hoe u de Elasticsearch-service voor Adobe Commerce kunt inschakelen voor cloudinfrastructuur.
feature: Cloud, Search, Services
exl-id: 238b9ed5-ce73-428f-9459-35de8573d5d8
source-git-commit: ef22e7b305c20148f4ee4b2c0e64e2114bf229b5
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---

# Elasticsearch-service instellen

[ Elasticsearch ](https://www.elastic.co) is een open-bronproduct dat u toelaat om gegevens uit om het even welke bron, om het even welk formaat, en onderzoek en visualiseer het in echt - tijd te nemen.

{{elasticsearch-support}}

Voor versie 2.4.4 van Adobe Commerce en recenter, zie [ de dienst van OpenSearch van de Opstelling ](opensearch.md).

- Elasticsearch voert snelle en geavanceerde zoekopdrachten uit op producten in de productcatalogus
- Elasticsearch Analyzers ondersteunen meerdere talen
- Ondersteunt stopwoorden en synoniemen
- Indexering heeft geen invloed op klanten totdat de herindexering is voltooid

>[!TIP]
>
>Adobe raadt u aan Elasticsearch altijd in te stellen voor uw Adobe Commerce-infrastructuurproject in de cloud, zelfs als u een zoekprogramma van derden voor uw Adobe Commerce-toepassing wilt configureren. Het instellen van Elasticsearch biedt een fallback-optie voor het geval dat het zoekprogramma van derden mislukt.

{{service-instruction}}

**om Elasticsearch** toe te laten:

1. Voor Starter-projecten voegt u de service `elasticsearch` toe aan het `.magento/services.yaml` -bestand met de Elasticsearch-versie en toegewezen schijfruimte in MB.

   ```yaml
   elasticsearch:
       type: elasticsearch:<version>
       disk: 1024
   ```

   Voor Pro-projecten moet u een Adobe Commerce Support-ticket indienen om de Elasticsearch-versie te wijzigen in de omgeving voor Staging en Productie.

1. Stel de eigenschap `relationships` in het `.magento.app.yaml` -bestand in.

   ```yaml
   relationships:
       elasticsearch: "elasticsearch:elasticsearch"
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable Elasticsearch" && git push origin <branch-name>
   ```

   Voor informatie over hoe deze veranderingen uw milieu&#39;s beïnvloeden, zie [ Diensten ](services-yaml.md).

1. Nadat het plaatsingsproces voltooit, gebruik SSH aan login aan het verre milieu.

   ```bash
   magento-cloud ssh
   ```

1. Indexeer de zoekindex van de catalogus opnieuw.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Maak de cache leeg.

   ```bash
   bin/magento cache:clean
   ```

{{service-change-tip}}

## Compatibiliteit met Elasticsearch-software

Wanneer u uw Adobe Commerce op het project van de wolkeninfrastructuur installeert of bevordert, controleert altijd verenigbaarheid tussen de de dienstversie van Elasticsearch en [ Elasticsearch PHP ](https://github.com/elastic/elasticsearch-php) cliënt voor Adobe Commerce.

- **eerste opstelling** - bevestig dat de versie van Elasticsearch die in het `services.yaml` dossier wordt gespecificeerd compatibel is met de cliënt van Elasticsearch PHP die voor Adobe Commerce wordt gevormd.

- **verbetering van het Project** - verifieer dat de cliënt van Elasticsearch PHP in de nieuwe toepassingsversie compatibel is met de de dienstversie van Elasticsearch die op de wolkeninfrastructuur wordt geïnstalleerd.

Serviceversie en compatibiliteitsondersteuning voor Adobe Commerce op cloudinfrastructuur worden bepaald door versies die worden geïmplementeerd op de cloudinfrastructuur en verschillen soms van versies die worden ondersteund door Adobe Commerce-implementaties op locatie. Zie [ versies van de Dienst ](services-yaml.md#service-versions).

**om de softwareverenigbaarheid van Elasticsearch te controleren**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Geef de Elasticsearch-gegevens voor de actieve omgeving weer.

   ```bash
   magento-cloud relationships --property=elasticsearch
   ```

1. U kunt SSH ook gebruiken om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Controleer de Composer-pakketversie op `elasticsearch/elasticsearch` .

   ```bash
   composer show elasticsearch/elasticsearch
   ```

   Controleer in het antwoord de geïnstalleerde versie in de eigenschap `versions` .

   ```
   name     : elasticsearch/elasticsearch
   descrip. : PHP Client for Elasticsearch
   keywords : client, elasticsearch, search
   versions : * v7.17.1
   type     : library
   license  : Apache License 2.0 (Apache-2.0) (OSI approved) https://spdx.org/licenses/Apache-2.0.html#licenseText
   license  : GNU Lesser General Public License v2.1 only (LGPL-2.1-only) (OSI approved) https://spdx.org/licenses/LGPL-2.1-only.html#licenseText
   homepage :
   source   : [git] git@github.com:elastic/elasticsearch-php.git f1b8918f411b837ce5f6325e829a73518fd50367
   dist     : [zip] https://api.github.com/repos/elastic/elasticsearch-php/zipball/f1b8918f411b837ce5f6325e829a73518fd50367 f1b8918f411b837ce5f6325e829a73518fd50367
   path     : ~/vendor/elasticsearch/elasticsearch
   names    : elasticsearch/elasticsearch
   ```

   U kunt ook de Elasticsearch PHP client version vinden in het `composer.lock` bestand in de root directory van de omgeving.

1. Haal de gegevens van de Elasticsearch-serviceverbinding op de opdrachtregel op.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   In de reactie, vind het IP adres voor het de diensteindpunt van Elasticsearch:

   ```
   | elasticsearch:                                                                                                  |
   +------------------------------------------+----------------------------------------------------------------------+
   | username                                 | null                                                                 |
   | scheme                                   | http                                                                 |
   | service                                  | elasticsearch                                                        |
   | fragment                                 | null                                                                 |
   | ip                                       | 169.254.220.11                                                       |
   | hostname                                 | dzggu33f75wi3sd24lgwtoupxm.elasticsearch.service._.magentosite.cloud |
   | public                                   | false                                                                |
   | cluster                                  | fo3qdoxtla4j4-master-7rqtwti                                         |
   | host                                     | elasticsearch.internal                                               |
   | rel                                      | elasticsearch                                                        |
   | query                                    |                                                                      |
   | path                                     | null                                                                 |
   | password                                 | null                                                                 |
   | type                                     | elasticsearch:6.5                                                    |
   | port                                     | 9200                                                                 |
   +------------------------------------------+----------------------------------------------------------------------+
   ```

1. Haal de geïnstalleerde Elasticsearch-service `version:number` op van het eindpunt van de service.

   ```bash
   curl -XGET <elasticsearch-service-endpoint-ip-address>:9200/
   ```

   ```json
   {
      "name" : "-AqGi9D",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "_yze6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "number" : "6.5.4",
        "build_flavor" : "default",
        "build_type" : "deb",
        "build_hash" : "82a8aa7",
        "build_date" : "2019-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "7.5.0",
        "minimum_wire_compatibility_version" : "5.6.0",
        "minimum_index_compatibility_version" : "5.0.0"
   },
   "  tagline" : "You Know, for Search"
   }
   ```

1. Controleer de versiecompatibiliteit tussen de Elasticsearch service en de PHP client.

   Als de versies incompatibel zijn, voert u een van de volgende updates uit in uw omgevingsconfiguratie:

   - Wijzig de Elasticsearch PHP client in een versie die compatibel is met de Elasticsearch service version.

     ```bash
     composer require "elasticsearch/elasticsearch:~<version>"
     ```

   - Wijzig de Elasticsearch-serviceversie in het `services.yaml` -bestand in een versie die compatibel is met de Elasticsearch PHP-client.

     {{pro-update-service}}

## De Elasticsearch-service opnieuw starten

Als u de [ dienst van Elasticsearch ](https://www.elastic.co) moet opnieuw beginnen, moet u de steun van Adobe Commerce contacteren.

## Aanvullende zoekconfiguratie

- Standaard wordt de zoekconfiguratie voor Cloud-omgevingen telkens opnieuw gegenereerd wanneer u deze implementeert. Met de implementatievariabele van `SEARCH_CONFIGURATION` kunt u aangepaste zoekinstellingen tussen implementaties behouden. Zie [ variabelen opstellen ](../environment/variables-deploy.md#search_configuration).

- Nadat u de Elasticsearch-service voor uw project hebt ingesteld, gebruikt u de beheerinterface om de Elasticsearch-verbinding te testen en Elasticsearch-instellingen voor Adobe Commerce aan te passen.

### Plug-ins voor Elasticsearch toevoegen

U kunt desgewenst plug-ins voor Elasticsearch toevoegen door de sectie `configuration:plugins` toe te voegen aan de Elasticsearch-service in het `.magento/services.yaml` -bestand. Met de volgende code worden bijvoorbeeld de insteekmodules voor ICU-analyse en Fonetische analyse ingeschakeld.

```yaml
elasticsearch:
    type: elasticsearch:<service-version>
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Als u de Elastic Suite derdestop gebruikt, moet u [ het `ece-tools` pakket ](../dev-tools/update-package.md) aan versie 2002.0.19 of later bijwerken.
Als u Elastic Suite instelt, voegt u de configuratie-instellingen toe aan de implementatievariabele van `ELASTICSUITE_CONFIGURATION` . Deze configuratie bewaart de montages over plaatsingen.

### Plug-ins voor Elasticsearch verwijderen

Als u de insteekmodules verwijdert uit `elasticsearch:` in `.magento/services.yaml` , worden deze niet zoals u zou verwachten verwijderd of uitgeschakeld. U moet de Elasticsearch-gegevens opnieuw indexeren. Dit gedrag is opzettelijk bedoeld om mogelijk verlies of beschadiging van gegevens te voorkomen die afhankelijk zijn van deze plug-ins.

**om de insteekmodules van Elasticsearch te verwijderen**:

1. Verwijder de Elasticsearch-insteekmodules uit uw `.magento/services.yaml` -bestand.
1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove Elasticsearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Leg de `.magento/services.yaml` -wijzigingen vast in uw Cloud-repo.
1. Indexeer de zoekindex van de catalogus opnieuw.

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Maak de cache leeg.

   ```bash
   bin/magento cache:clean
   ```

>[!TIP]
>
>Voor details bij het gebruiken van of het oplossen van problemen van de Insteekmodule Elastic Suite met Adobe Commerce, zie de [ documentatie van de Elastic Suite ](https://github.com/Smile-SA/elasticsuite).

