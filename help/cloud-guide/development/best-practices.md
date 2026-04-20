---
title: Aanbevolen procedures voor het upgraden van uw project
description: Zie een lijst met aanbevolen procedures voor het upgraden van uw projectbestanden.
feature: Cloud, Best Practices, Upgrade
exl-id: 64f92739-9170-4cbf-90ef-aab6593a37ca
source-git-commit: 31494a956babaf15320d0ffa86fcba9e845d53a1
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# Aanbevolen procedures voor het upgraden van uw project

Volg beste praktijken voor bouwstijlen en plaatsing, en gebruik het [&#x200B; Upgrades en flarden &#x200B;](../development/commerce-version.md) werkschema om uw toepassing te bevorderen. Gebruik de volgende richtlijnen om uw upgrade en werk na de upgrade te plannen:

- **Steun uw project** - alvorens de Adobe Commerce en om het even welke derde of douaneuitbreidingen te bevorderen, file het gegevensbestand in de milieu&#39;s van de Integratie, het Opvoeren, en van de Productie. Zie [&#x200B; file het gegevensbestand &#x200B;](../development/commerce-version.md#project-backup).

- **Controle voor verenigbaarheidskwesties** -

   - Zorg ervoor dat aangepaste thema&#39;s compatibel zijn met de nieuwe Adobe Commerce-versie

   - Na de bevordering van derde en douaneversies, gebruik het `magento-cloud local:build` bevel om de gebiedsdelen van de Componist te bevestigen alvorens op te stellen, en in werking te stellen het [&#x200B; Hulpmiddel van de Verenigbaarheid van de Verbetering &#x200B;](#use-the-upgrade-compatibility-tool) om code-vlakke onverenigbaarheden tussen uw huidige en doelversies te identificeren. Dan gebruik het [&#x200B; Hulpmiddel van de Verenigbaarheid van de Verbetering &#x200B;](https://fluffyjaws.adobe.com/#use-the-upgrade-compatibility-tool) om code-vlakke onverenigbaarheden te identificeren en voorrang te geven alvorens aan Integratie, het Opvoeren, of Productie op te stellen.

   - Bekijk de Adobe Commerce-releaseopmerkingen en de uitbreidingsdocumentatie om te controleren of u eventuele oplossingen of configuratiewijzigingen hebt geïmplementeerd die nodig zijn om bekende functionele problemen en fouten met betrekking tot de upgrade van de Adobe Commerce-versie en -extensies te verhelpen.

   - Zorg ervoor dat de geïnstalleerde serviceversies compatibel zijn met de nieuwe Adobe Commerce-versie en werk de services waar nodig bij. Zie [&#x200B; Diensten &#x200B;](../services/services-yaml.md).

   - Test uw database om problemen op te lossen die zijn ontstaan door de updates voor de Adobe Commerce-versie en -extensies.

   - Breng de vereiste updates van de specifieke omgevingen aan voordat u deze implementeert in de externe omgeving.

   - Zorg ervoor dat de versie van de zoekservice compatibel is met de PHP-clientversie. Zie [&#x200B; Opstelling Elasticsearch &#x200B;](../services/elasticsearch.md) of [&#x200B; Opstelling OpenSearch &#x200B;](../services/opensearch.md).

- **de gegevensbestandconnectiviteit van de controle en beschikbare opslag in verre milieu&#39;s** -

   - Gebruik SSH aan login aan de verre server en verifieer de verbinding aan het gegevensbestand MySQL. Zie [&#x200B; verbinden met het gegevensbestand &#x200B;](../services/mysql.md#connect-to-the-database).

   - Beschikbare opslagruimte in de externe omgeving controleren. Gebruik de opdracht `disk free` om beschikbare schijfruimte in uw cloud-omgeving weer te geven en te beheren. Zie [&#x200B; schijfruimte beheren &#x200B;](../storage/manage-disk-space.md).

      - Controleer de grootte van de bijgewerkte database en controleer of er voldoende schijfruimte is toegewezen aan het `services.yaml` -bestand.

      - Maak schijfruimte vrij - Wis de cache en schoonmaak de mappen `/log` en `/tmp` voordat u gaat implementeren.

- **Plan en voer een succesvolle verbetering op lokale en integratiemilieu&#39;s uit, alvorens aan het Opvoeren** - na de verbetering, test uw plaatsing en los om het even welke kwesties op.

- **de code van de Fusie aan het Opvoeren, en dan aan productie** - test en lost om het even welke kwesties in het het Opvoeren milieu op alvorens veranderingen in het milieu van de Productie te duwen.

- **Volledige de verbeteringstaken van het Post** -

   - Gebruik SSH om u aan te melden bij de externe server en controleer het volgende:

      - Controleer de indexeerstatus en herdex naar wens. Zie [&#x200B; de indexen &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/manage-indexers.html) in de _gids van de Configuratie_ leiden.

      - Controleer de `cron` -logbestanden en de `cron_schedule` -tabel in de Adobe Commerce-database om de uitsnijstatus te controleren en voer de taken voor uitsnijden zo nodig opnieuw uit.
Zie [&#x200B; het Registreren &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html#logging) in de _Gids van de Configuratie_.

   - Voltooi het testen van gebruikersacceptatietests na de upgrade op de testomgeving voor het opslaan en produceren van bestanden en los eventuele problemen op die te maken hebben met upgrades van derden en aangepaste extensies.

## Het gereedschap Compatibiliteit bijwerken gebruiken

Voer het Hulpmiddel van de Verenigbaarheid van de Verbetering (UCT) als deel van uw pre-verbeteringsanalyse uit om het werkingsgebied en het effect van een verbetering te begrijpen.

- UCT vergelijkt uw huidige instantie met een Adobe Commerce-doelversie, waarbij een lijst met kritieke problemen, fouten en waarschuwingen wordt geretourneerd die moeten worden verholpen voordat de upgrade wordt uitgevoerd.
- Gebruik `--coming-version (-c)` om te vergelijken met uw geplande doelversie en `--ignore-current-version-compatibility-issues` om alleen de nadruk te leggen op nieuwe problemen die door de upgrade zijn geïntroduceerd.
- Behandel het rapport van UCT HTML als input aan uw verbeteringscontrolelijst naast uitbreidingsverenigbaarheid, de dienstversies, en gegevensbestandcontroles.

Voor opstelling en gebruiksdetails, zie:

- [Overzicht van het gereedschap Compatibiliteit bijwerken](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/overview)
- [Voer het gereedschap Compatibiliteit bijwerken uit](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/use-upgrade-compatibility-tool/run)

Voor verkopers van de Wolk die het hulpmiddel van de Analyse van de Plaats gebruiken, kunt u UCT van het dashboard ook teweegbrengen en het rapport van HTML direct van widget downloaden. Zie het [&#x200B; plaats-brede Hulpmiddel van de Analyse &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/upgrade-guide/upgrade-compatibility-tool/use-upgrade-compatibility-tool/integrate-analysis-tool) integreren.
