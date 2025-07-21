---
title: OpenSearch-service instellen
description: Leer hoe u de OpenSearch-service voor Adobe Commerce kunt inschakelen voor cloudinfrastructuur.
feature: Cloud, Search, Services
exl-id: e704ab2a-2f6b-480b-9b36-1e97c406e873
source-git-commit: 1f965749e59e3c48be2d8e04ac58683234e7b685
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---

# OpenSearch-service instellen

De [ OpenSearch ](https://www.opensearch.org) dienst is een open-bron vork van Elasticsearch 7.10.2, na de vergunningsveranderingen voor Elasticsearch. Zie het [ Project OpenSource ](https://github.com/opensearch-project) in GitHub.

{{elasticsearch-support}}

Met OpenSearch kunt u gegevens van elke bron, elke indeling en in real-time zoeken en visualiseren.

- Snel en geavanceerd zoeken naar producten in de productcatalogus
- OpenSearch Analyzers ondersteunen meerdere talen
- Ondersteunt stopwoorden en synoniemen
- Indexering heeft geen invloed op klanten totdat de herindexering is voltooid

{{service-instruction}}

>[!TIP]
>
>Adobe raadt u aan om altijd OpenSearch voor uw Adobe Commerce in te stellen op het infrastructuurproject voor de cloud, zelfs als u een zoekprogramma van derden voor uw Adobe Commerce-toepassing wilt configureren. Het instellen van OpenSearch biedt een fallback-optie als het zoekgereedschap van derden mislukt.

**om OpenSearch** toe te laten:

1. Voor integratieomgevingen voegt u de service `opensearch` toe aan het `.magento/services.yaml` -bestand met de juiste versie en toegewezen schijfruimte in MB. In dit geval is versie 2 geschikt. De secundaire versie is niet vereist.

   ```yaml
   opensearch:
       type: opensearch:2
       disk: 1024
   ```

   Voor Pro projecten, moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voorleggen om de versie OpenSearch in de het Opvoeren en milieu&#39;s van de Productie te veranderen.

1. Stel de eigenschap `relationships` in het `.magento.app.yaml` -bestand in of controleer deze.

   ```yaml
   relationships:
       opensearch: "opensearch:opensearch"
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable OpenSearch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   Voor informatie over hoe deze veranderingen uw milieu&#39;s beïnvloeden, zie [ de diensten ](services-yaml.md) vormen.

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

## Compatibiliteit met OpenSearch-software

Wanneer u uw Adobe Commerce op het project van de wolkeninfrastructuur installeert of bevordert, controleert altijd verenigbaarheid tussen de OpenSearch de dienstversie en [ OpenSearch PHP ](https://github.com/opensearch-project/opensearch-php) cliënt voor Adobe Commerce.

- **eerste opstelling** - bevestig dat de versie OpenSearch die in het `services.yaml` dossier wordt gespecificeerd compatibel is met de cliënt OpenSearch PHP die voor Adobe Commerce wordt gevormd.

- **verbetering van het Project** - verifieer dat de cliënt OpenSearch PHP in de nieuwe toepassingsversie compatibel is met de OpenSearch de dienstversie die op de wolkeninfrastructuur wordt geïnstalleerd.

De versie van de dienst en verenigbaarheidssteun wordt bepaald door versies die op de infrastructuur van de Wolk worden getest en worden opgesteld, en verschillen soms van versies die door Adobe Commerce op-gebouw plaatsingen worden gesteund. Zie {de vereisten van het 0} Systeem [ in de ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html?lang=nl-NL) Gids van de Installatie _voor een lijst van gesteunde versies._

**om de softwareverenigbaarheid te verifiëren OpenSearch**:

1. Wijzig op uw lokale werkstation de projectmap.

1. De OpenSearch-details voor de actieve omgeving weergeven.

   ```bash
   magento-cloud relationships --property=opensearch
   ```

1. U kunt SSH ook gebruiken om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Haal de verbindingsgegevens van de OpenSearch-service op.

   ```bash
   vendor/bin/ece-tools env:config:show services
   ```

   In de reactie, vind het IP adres en de haven voor het de diensteindpunt van OpenSearch:

   ```
   +------------------------------------------+--------------------------------------------------------+
   | opensearch:                                                                                       |
   +------------------------------------------+--------------------------------------------------------+
   | username                                 | null                                                   |
   | scheme                                   | http                                                   |
   | service                                  | opensearch                                             |
   | fragment                                 | null                                                   |
   | ip                                       | 169.254.220.11                                         |
   | hostname                                 | hostf75wi3sd24l.opensearch.service._.magentosite.cloud |
   | port                                     | 9200                                                   |
   | cluster                                  | projectID-develop-4ranwui                              |
   | host                                     | opensearch.internal                                    |
   | rel                                      | opensearch                                             |
   | path                                     | null                                                   |
   | query                                    |                                                        |
   | password                                 | null                                                   |
   | type                                     | opensearch:2                                           |
   | public                                   | false                                                  |
   | host_mapped                              | false                                                  |
   ```

1. Haal de geïnstalleerde OpenSearch-service `version:number` op van het eindpunt van de service.

   ```bash
   curl -XGET <opensearch-service-endpoint-ip-address>:9200
   ```

   ```json
   {
      "name" : "opensearch.0",
      "cluster_name" : "opensearch",
      "cluster_uuid" : "_yzaae6-ywSEW1MaAF8ZPWyQ",
      "version" : {
        "distribution" : "opensearch",
        "number" : "2.5.0",
        "build_type" : "deb",
        "build_hash" : "aaaaaaa",
        "build_date" : "2023-01-23T12:07:18.760675Z",
        "build_snapshot" : false,
        "lucene_version" : "9.4.2",
        "minimum_wire_compatibility_version" : "7.10.0",
        "minimum_index_compatibility_version" : "7.0.0"
   },
   "tagline" : "The OpenSearch Project: https://opensearch.org/"
   }
   ```

{{pro-update-service}}

## De OpenSearch-service opnieuw starten

Als u de OpenSearch-service opnieuw wilt starten, moet u contact opnemen met de ondersteuning van Adobe Commerce.

## Aanvullende zoekconfiguratie

- Standaard wordt de zoekconfiguratie voor Cloud-omgevingen telkens opnieuw gegenereerd wanneer u deze implementeert. Met de implementatievariabele van `SEARCH_CONFIGURATION` kunt u aangepaste zoekinstellingen tussen implementaties behouden. Zie [ variabelen opstellen ](../environment/variables-deploy.md#search_configuration).

- Nadat u de OpenSearch-service voor uw project hebt ingesteld, gebruikt u de beheerinterface om de OpenSearch-verbinding te testen en de OpenSearch-instellingen voor Adobe Commerce aan te passen.

### Plug-ins toevoegen voor OpenSearch

U kunt desgewenst plug-ins voor OpenSearch toevoegen door de sectie `configuration:plugins` toe te voegen aan de OpenSearch-service in het `.magento/services.yaml` -bestand. Met de volgende code worden bijvoorbeeld de insteekmodules voor ICU-analyse en Fonetische analyse ingeschakeld.

>[!NOTE]
>
>Dit geldt alleen voor integratie- en starteromgevingen. Om plugins in een Pro het Opvoeren of cluster van de Productie te installeren, [ voorlegt een steunverzoek ](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-case).


```yaml
opensearch:
    type: opensearch:2
    disk: 1024
    configuration:
        plugins:
            - analysis-icu
            - analysis-phonetic
```

Zie het [ Project OpenSearch ](https://github.com/opensearch-project) voor meer informatie over stoppen.

### Insteekmodules voor OpenSearch verwijderen

Het verwijderen van de insteekmoduleingangen uit de `opensearch:` sectie van het `.magento/services.yaml` dossier **&#x200B;**&#x200B;schrapt of maakt de dienst niet onbruikbaar. Als u de service volledig wilt uitschakelen, moet u de OpenSearch-gegevens opnieuw indexeren nadat u de plug-ins uit het `.magento/services.yaml` -bestand hebt verwijderd. Dit ontwerp voorkomt mogelijk gegevensverlies of -beschadiging die afhankelijk is van deze plug-ins.


**om stopSearch te verwijderen**:

>[!NOTE]
>
>Deze wijziging geldt alleen voor integratie- en starteromgevingen. U zult een steunkaartje [ moeten voorleggen om de stop in een Pro Staging of cluster van de Productie te verwijderen.](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-case)

1. Verwijder de items van de OpenSearch-insteekmodule uit het `.magento/services.yaml` -bestand.
1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Remove OpenSearch plugin"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Leg de `.magento/services.yaml` -wijzigingen vast in uw cloudopslagplaats.
1. Wijzig de index van het Onderzoek van de Catalogus (alle milieu&#39;s: Integratie, Starter, Pro het Opvoeren en clusters van de Productie).

   ```bash
   bin/magento indexer:reindex catalogsearch_fulltext
   ```

1. Maak de cache leeg.

   ```bash
   bin/magento cache:clean
   ```
