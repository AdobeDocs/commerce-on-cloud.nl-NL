---
title: Aanbevolen procedures voor het upgraden van uw project
description: Zie een lijst met aanbevolen procedures voor het upgraden van uw projectbestanden.
feature: Cloud, Best Practices, Upgrade
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Aanbevolen procedures voor het upgraden van uw project

Volg beste praktijken voor bouwstijlen en plaatsing, en gebruik het [ Upgrades en flarden ](../development/commerce-version.md) werkschema om uw toepassing te bevorderen. Gebruik de volgende richtlijnen om uw upgrade en werk na de upgrade te plannen:

- **Steun uw project** - alvorens de Adobe Commerce en om het even welke derde of douaneuitbreidingen te bevorderen, file het gegevensbestand in de milieu&#39;s van de Integratie, het Opvoeren, en van de Productie. Zie [ file het gegevensbestand ](../development/commerce-version.md#project-backup).

- **Controle voor verenigbaarheidskwesties** -

   - Zorg ervoor dat aangepaste thema&#39;s compatibel zijn met de nieuwe Adobe Commerce-versie

   - Nadat u externe en aangepaste extensies hebt bijgewerkt, gebruikt u de opdracht `magento-cloud local:build` om Composer-afhankelijkheden te valideren voordat u deze implementeert.

   - Bekijk de Adobe Commerce-releaseopmerkingen en de uitbreidingsdocumentatie om te controleren of u eventuele oplossingen of configuratiewijzigingen hebt geïmplementeerd die nodig zijn om bekende functionele problemen en fouten met betrekking tot de upgrade van de Adobe Commerce-versie en -extensies te verhelpen.

   - Zorg ervoor dat de geïnstalleerde serviceversies compatibel zijn met de nieuwe Adobe Commerce-versie en werk de services waar nodig bij. Zie [ Diensten ](../services/services-yaml.md).

   - Test uw database om problemen op te lossen die zijn ontstaan door de updates voor de Adobe Commerce-versie en -extensies.

   - Breng de vereiste updates van de specifieke omgevingen aan voordat u deze implementeert in de externe omgeving.

   - Zorg ervoor dat de versie van de zoekservice compatibel is met de PHP-clientversie. Zie [ Elasticsearch van de Opstelling ](../services/elasticsearch.md) of [ Opstelling OpenSearch ](../services/opensearch.md).

- **de gegevensbestandconnectiviteit van de controle en beschikbare opslag in verre milieu&#39;s** -

   - Gebruik SSH aan login aan de verre server en verifieer de verbinding aan het gegevensbestand MySQL. Zie [ verbinden met het gegevensbestand ](../services/mysql.md#connect-to-the-database).

   - Beschikbare opslagruimte in de externe omgeving controleren. Gebruik de opdracht `disk free` om beschikbare schijfruimte in uw cloud-omgeving weer te geven en te beheren. Zie [ schijfruimte beheren ](../storage/manage-disk-space.md).

      - Controleer de grootte van de bijgewerkte database en controleer of er voldoende schijfruimte is toegewezen aan het `services.yaml` -bestand.

      - Maak schijfruimte vrij - Wis de cache en schoonmaak de mappen `/log` en `/tmp` voordat u gaat implementeren.

- **Plan en voer een succesvolle verbetering op lokale en integratiemilieu&#39;s uit, alvorens aan het Opvoeren** - na de verbetering, test uw plaatsing en los om het even welke kwesties op.

- **de code van de Fusie aan het Opvoeren, en dan aan productie** - test en lost om het even welke kwesties in het het Opvoeren milieu op alvorens veranderingen in het milieu van de Productie te duwen.

- **Volledige de verbeteringstaken van het Post** -

   - Gebruik SSH om u aan te melden bij de externe server en controleer het volgende:

      - Controleer de indexeerstatus en herdex naar wens. Zie [ de indexen ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) in de _gids van de Configuratie_ leiden.

      - Controleer de `cron` -logbestanden en de `cron_schedule` -tabel in de Adobe Commerce-database om de uitsnijstatus te controleren en voer de taken voor uitsnijden zo nodig opnieuw uit.
Zie [ het Registreren ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) in de _Gids van de Configuratie_.

   - Voltooi het testen van gebruikersacceptatietests na de upgrade op de testomgeving voor het opslaan en produceren van bestanden en los eventuele problemen op die te maken hebben met upgrades van derden en aangepaste extensies.
