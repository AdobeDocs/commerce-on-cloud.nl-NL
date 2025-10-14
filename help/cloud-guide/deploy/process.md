---
title: Implementatieproces
description: Leer hoe implementatie werkt voor Adobe Commerce op cloud-infrastructuurprojecten.
feature: Cloud, Build, Deploy, SCD
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Implementatieproces

Het plaatsingsproces begint wanneer u een fusie, duw, of synchronisatie van uw milieu uitvoert, of wanneer u a [&#x200B; handherplaatsing &#x200B;](../dev-tools/cloud-cli-overview.md#redeploy-the-environment) teweegbrengt. Het implementatieproces neemt tijd in beslag, maar er zijn manieren om de implementatie te optimaliseren die afhankelijk zijn van het feit of u een livesite ontwikkelt en test of ermee werkt. Met name, kunt u de [&#x200B; statische inhoudsplaatsing &#x200B;](static-content.md) controleren.

Er zijn drie, verschillende fasen van het plaatsingsproces: bouw, stel, en post-opstellen op. Elke fase voert specifieke acties met beperkte middelen uit:

## ![&#x200B; bouwt fase &#x200B;](../../assets/status-build.png) bouwt fase

De _bouwstijl_ assembleert containers voor de diensten die in de configuratiedossiers worden bepaald, installeert gebiedsdelen die op het `composer.lock` dossier worden gebaseerd, en stelt de bouwstijlhaken in werking die in het `.magento.app.yaml` dossier worden bepaald. Zonder de capaciteit om met om het even welke diensten te verbinden of tot het gegevensbestand toegang te hebben, hangt de bouwstijlfase van de middelen af die tot het milieu worden beperkt.

## ![&#x200B; opstellen fase &#x200B;](../../assets/status-deploy.png) opstellen fase

_stelt_ fase op plaatsen een tijdelijke greep op inkomende verzoeken en overgangen de plaats in [&#x200B; onderhoudswijze &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html?lang=nl-NL) op. In de implementatiefase worden de nieuwe containers gebruikt en worden, nadat het bestandssysteem is gekoppeld, netwerkverbindingen geopend, de services geactiveerd die zijn gedefinieerd in de sectie `relationships` van het `.magento.app.yaml` -bestand en worden de implementatiehaken uitgevoerd die zijn gedefinieerd in het `.magento.app.yaml` -bestand. Alles is _leest slechts_, behalve folders die in het `.magento.app.yaml` dossier worden bepaald. Door gebrek, omvat het [`mounts` bezit &#x200B;](../application/properties.md#mounts) de volgende folders:

- `app/etc` - bevat de configuratiebestanden `env.php` en `config.php`
- `pub/media` - bevat alle mediagegevens, zoals producten of categorieën
- `pub/static`—bevat gegenereerde statische bestanden
- `var` - bevat tijdelijke bestanden die tijdens runtime zijn gemaakt

Alle andere mappen hebben alleen-lezen machtigingen. De nieuwe plaats wordt actief aan het eind van de opstellen fase aangezien het uit onderhoudswijze overgaat en de tijdelijke greep op inkomende verzoeken vrijgeeft.

Tijdens de implementatiefase worden kopieën van de configuratiebestanden voor de implementatie van `app/etc/config.php` en `app/etc/env.php` opgeslagen met de BAK-extensie. Zie [&#x200B; montages van de Opslag &#x200B;](../store/store-settings.md#restore-configuration-files) om over het herstellen van deze dossiers te leren.

## ![&#x200B; post-opstellen fase &#x200B;](../../assets/status-post-deploy.png) post-opstellen fase

De _post-stel_ fase in werking stelt de haken post-stelt die in het `.magento.app.yaml` dossier worden bepaald. Het uitvoeren van om het even welke actie op deze fase kan plaatsprestaties beïnvloeden; nochtans, kunt u [&#x200B; gebruiken WARM_UP_PAGES &#x200B;](../environment/variables-post-deploy.md#warmuppages) milieuvariabele om het geheime voorgeheugen te bevolken.

## ![&#x200B; verifieer staat &#x200B;](../../assets/status-verify.png) configuraties verifieert

U kunt de optimale configuratie voor de staat van uw project testen door de [&#x200B; Slimme tovenaars &#x200B;](smart-wizards.md) in werking te stellen.

>[!NOTE]
>
>Met `ece-tools` 2002.1.0 en hoger kunt u de op scenario&#39;s gebaseerde implementatiefunctie gebruiken om de build-, implementatie- en postimplementatieprocessen voor uw Adobe Commerce aan te passen in het infrastructuurproject in de cloud. Zie [&#x200B; op scenario-Gebaseerde plaatsing &#x200B;](scenario-based.md).
