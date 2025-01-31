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

Het plaatsingsproces begint wanneer u een fusie, duw, of synchronisatie van uw milieu uitvoert, of wanneer u a [ handherplaatsing ](../dev-tools/cloud-cli-overview.md#redeploy-the-environment) teweegbrengt. Het implementatieproces neemt tijd in beslag, maar er zijn manieren om de implementatie te optimaliseren die afhankelijk zijn van het feit of u een livesite ontwikkelt en test of ermee werkt. Met name, kunt u de [ statische inhoudsplaatsing ](static-content.md) controleren.

Er zijn drie, verschillende fasen van het plaatsingsproces: bouw, stel, en post-opstellen op. Elke fase voert specifieke acties met beperkte middelen uit:

## ![ bouwt fase ](../../assets/status-build.png) bouwt fase

De _bouwstijl_ assembleert containers voor de diensten die in de configuratiedossiers worden bepaald, installeert gebiedsdelen die op het `composer.lock` dossier worden gebaseerd, en stelt de bouwstijlhaken in werking die in het `.magento.app.yaml` dossier worden bepaald. Zonder de capaciteit om met om het even welke diensten te verbinden of tot het gegevensbestand toegang te hebben, hangt de bouwstijlfase van de middelen af die tot het milieu worden beperkt.

## ![ opstellen fase ](../../assets/status-deploy.png) opstellen fase

_stelt_ fase op plaatsen een tijdelijke greep op inkomende verzoeken en overgangen de plaats in [ onderhoudswijze ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html) op. In de implementatiefase worden de nieuwe containers gebruikt en worden, nadat het bestandssysteem is gekoppeld, netwerkverbindingen geopend, de services geactiveerd die zijn gedefinieerd in de sectie `relationships` van het `.magento.app.yaml` -bestand en worden de implementatiehaken uitgevoerd die zijn gedefinieerd in het `.magento.app.yaml` -bestand. Alles is _leest slechts_, behalve folders die in het `.magento.app.yaml` dossier worden bepaald. Door gebrek, omvat het [`mounts` bezit ](../application/properties.md#mounts) de volgende folders:

- `app/etc` - bevat de configuratiebestanden `env.php` en `config.php`
- `pub/media` - bevat alle mediagegevens, zoals producten of categorieën
- `pub/static`—bevat gegenereerde statische bestanden
- `var` - bevat tijdelijke bestanden die tijdens runtime zijn gemaakt

Alle andere mappen hebben alleen-lezen machtigingen. De nieuwe plaats wordt actief aan het eind van de opstellen fase aangezien het uit onderhoudswijze overgaat en de tijdelijke greep op inkomende verzoeken vrijgeeft.

Tijdens de implementatiefase worden kopieën van de configuratiebestanden voor de implementatie van `app/etc/config.php` en `app/etc/env.php` opgeslagen met de BAK-extensie. Zie [ montages van de Opslag ](../store/store-settings.md#restore-configuration-files) om over het herstellen van deze dossiers te leren.

## ![ post-opstellen fase ](../../assets/status-post-deploy.png) post-opstellen fase

De _post-stel_ fase in werking stelt de haken post-stelt die in het `.magento.app.yaml` dossier worden bepaald. Het uitvoeren van om het even welke actie op deze fase kan plaatsprestaties beïnvloeden; nochtans, kunt u [ gebruiken WARM_UP_PAGES ](../environment/variables-post-deploy.md#warmuppages) milieuvariabele om het geheime voorgeheugen te bevolken.

## ![ verifieer staat ](../../assets/status-verify.png) configuraties verifieert

U kunt de optimale configuratie voor de staat van uw project testen door de [ Slimme tovenaars ](smart-wizards.md) in werking te stellen.

>[!NOTE]
>
>Met `ece-tools` 2002.1.0 en hoger kunt u de op scenario&#39;s gebaseerde implementatiefunctie gebruiken om de build-, implementatie- en postimplementatieprocessen voor uw Adobe Commerce aan te passen in het infrastructuurproject in de cloud. Zie [ op scenario-Gebaseerde plaatsing ](scenario-based.md).
