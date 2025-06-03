---
title: Cloud Components voor Commerce
description: Zie een lijst met de meest recente verbeteringen in het pakket met Cloud Components.
recommendations: noDisplay, catalog
exl-id: 34aec593-e2ea-4060-a6b9-6f4cb95a11c0
source-git-commit: dcf71ffbdafae46e6a02735c090c33a8fe248bc6
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Cloud Components voor Commerce

Het [&#128279;](https://github.com/magento/magento-cloud-components) pakket van de Componenten van de Wolk  verstrekt uitgebreide de kernfunctionaliteit van Adobe Commerce voor plaatsen die op de infrastructuur van de Wolk worden opgesteld. Dit pakket is afhankelijk van het pakket ECE-Tools. Deze versienota&#39;s beschrijven de recentste verbeteringen aan dit pakket, dat een component van [ de Reeks van Hulpmiddelen van de Wolk voor Commerce ](cloud-tools-suite.md) is.

Het pakket `magento/magento-cloud-components` gebruikt de volgende versiereeks: `<major>.<minor>.<patch>`

De opmerkingen bij de release omvatten:

- ![ nieuw pictogram ](../../assets/new.svg) Nieuwe eigenschappen
- ![&#128279;](../../assets/fix.svg) Bevestigingspictogram van 0&rbrace; moeilijke situatie en verbeteringen

<!--Add release notes below-->

## v1.1.2 {#latest}

Releasedatum: 3 juni 2025

- &rbrack;(../../assets/fix.svg) **Verbeterde verenigbaarheid met 2.4.8** - Bijgewerkte derdebibliotheken voor betere verenigbaarheid met 2.4.8 <!-- MCLOUD-13707	 - -->!&lbrack;

## v1.1.1

Releasedatum: 6 februari 2025

- ![ nieuw pictogram ](../../assets/new.svg) **PHP 8.4** - toegevoegde steun voor PHP 8.4.<!-- MCLOUD-13148	 - -->
- ![ fixpictogram ](../../assets/fix.svg) **Repareren voor geheim voorgeheugen warm-omhoog** - Vaste een kwestie met categorie URLs tijdens geheim voorgeheugenopwarming.<!-- MCLOUD-12454 - -->


## v1.1.0

Releasedatum: 7 oktober 2024

- ![ fixpictogram ](../../assets/fix.svg) **Refactored code** - Verwijderde steun van oude PHP versies 7.4, 7.3, 7.2 en verwante bibliotheken.<!-- MCLOUD-9278 - -->
- ![&#128279;](../../assets/fix.svg) **Bevestigingspictogram  Bevorderde versie Monolog** - Toegevoegde steun voor monolog 3.6.<!-- MCLOUD-12855 - -->

## v1.0.14

Releasedatum: 8 april 2024

- ![ nieuw pictogram ](../../assets/new.svg) **PHP** - toegevoegde steun voor PHP 8.3.

## v1.0.13

Releasedatum: 10 maart 2023

- ![ nieuw pictogram ](../../assets/new.svg) **Verbeterde steun voor PHP 8.2** - Vaste verenigbaarheidskwesties met bepaalde PHP 8.2.x versies om Commerce 2.4.6 te steunen.

## v1.0.12

Releasedatum: 13 september 2022

- ![ herstellingspictogram ](../../assets/fix.svg) **Fouten op warmte** - Vaste een kwestie die aan [ warmte ](../environment/variables-post-deploy.md#warm_up_pages) probeerde toen de paginazichtbaarheid aan [**niet Zichtbaar individueel** ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-attributes-product#simple-product-csv-file-structure) in Admin wordt geplaatst, resulterend in `ERROR: Warming up failed: <link to page>` fouten in het plaatsingslogboek.<!-- MCLOUD-9134 -->

## v1.0.11

Releasedatum: 4 augustus 2022

- ![ fixpictogram ](../../assets/fix.svg) **Toegevoegde Steun voor Symfony 5.4 verenigbaarheid** - Vast voor verenigbaarheid met Symfony 5.4.<!-- AC-3550 -->

## v1.0.10

Releasedatum: 10 maart 2022

- ![ nieuw pictogram ](../../assets/new.svg) **Steun PHP 8.1** - Toegevoegde steun voor PHP 8.1 en gelaten vallen steun voor PHP 7.1.

## v1.0.9

Releasedatum: 25 oktober 2021

- ![ fixpictogram ](../../assets/fix.svg) **Update Monolog** - werkte de minimumversie bij die voor het `monolog` pakket aan `^2.3` wordt vereist.<!-- ACMP-1263 -->

## v1.0.8

Releasedatum: 29 juli 2021

- ![ herstellingspictogram ](../../assets/fix.svg) **Verwijderde het slepen schuine strepen van auto-geproduceerde URLs** - Verwijderde de het slepen schuine strepen van Categorie Pagina URLs die tijdens geheim voorgeheugen warm wordt geproduceerd.<!--MCLOUD-7192-->

## v1.0.7

Releasedatum: 9 september 2020

- ![ nieuw pictogram ](../../assets/new.svg) **het Registreren verbeteringen** - verklein de grootte van het `cache.log` dossier om prestaties te verbeteren.<!--MCLOUD-6859-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een typefout in de waarden van de geheim voorgeheugenconfiguratie die het `php bin/magento cache:evict` CLI bevel om veroorzaakte te ontbreken.

## v1.0.6

Releasedatum: 5 augustus 2020

- ![ nieuw pictogram ](../../assets/new.svg) **verbetert Redis prestaties** - toegevoegd het `./bin/magento cache:evict` bevel om verlopen sleutels te verwijderen Redis, die Redis geheugengebruik vermindert om prestaties te verbeteren.<!--MCLOUD-6023-->

- ![ fixpictogram ](../../assets/fix.svg) Verwijderde steun voor *Logboeken van New Relic in Context* om een prestatieskwestie te bevestigen.<!--MCLOUD-6422-->

## v1.0.5

Releasedatum: 25 juni 2020

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die in magento/magento-wolk-componenten versie 1.0.4 werd geïntroduceerd die de leeglopings geheim voorgeheugenverrichting om tijdens de opstellen fase veroorzaakte te ontbreken, die het plaatsingsproces onderbreekt.

## v1.0.4

Releasedatum: 25 juni 2020

- ![ nieuw pictogram ](../../assets/new.svg) **Geïmplementeerde Logboeken van New Relic in Context** - De logboeken van de Toepassing die door Adobe Commerce nu vertoning in sporen binnen New Relic worden geproduceerd om het oplossen van problemenmogelijkheden te verbeteren.<!--MCLOUD-6029-->

- ![ nieuw pictogram ](../../assets/new.svg) **Verbeterd registreren** - Toegevoegd registreren om geheim voorgeheugenongeldigverklaring en volledige herindexgebeurtenissen te volgen.<!--MCLOUD-6157-->

## v1.0.3

Releasedatum: 27 februari 2020

- ![ fixpictogram ](../../assets/fix.svg) Vaste een verenigbaarheidskwestie om `ece-tools` 2002.0.x- versies te steunen die oudere PHP versies gebruiken.

## v1.0.2

Releasedatum: 6 februari 2020

- ![ nieuw pictogram ](../../assets/new.svg) Uitgebreide de functionaliteit van de `WARM_UP_PAGES` omgevingsvariabele om geheim voorladen voor specifieke productpagina&#39;s te steunen. Zie [ post-stel variabelen ](../environment/variables-post-deploy.md#warm_up_pages) onderwerp voor een gedetailleerde eigenschapbeschrijving op.<!--MAGECLOUD-4444-->

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie waar een ongeldige opslag URL de post-opstellingshaak veroorzaakt om te ontbreken wanneer het gebruiken van de `WARM_UP_PAGES` functionaliteit om het geheime voorgeheugen te bevolken. Deze kwestie kwam slechts voor wanneer URL herschrijft werd onbruikbaar gemaakt.<!-- MAGECLOUD-4094 -->

## v1.0.1

Releasedatum: 23 juli 2019

- ![ fixpictogram ](../../assets/fix.svg) Vaste een kwestie die [**WARM_UP_PAGES**](../environment/variables-post-deploy.md#warm_up_pages) functionaliteit beïnvloedde die een standaard opslag URL gebruikt. Nu, als het `config:show:default-url` bevel geen basis URL kan halen, dan wordt URL van de variabele MAGENTO_CLOUD_ROUTES gebruikt.<!-- MAGECLOUD-3866 -->

## v1.0.0

Releasedatum: 12 juni 2019

Dit is de eerste versie van het pakket [`magento/magento-cloud-components` ](https://github.com/magento/magento-cloud-components) . Dit is een nieuwe afhankelijkheid voor pakketversie 2002.0.20 en hoger van `ece-tools` .

- ![ nieuw pictogram ](../../assets/new.svg) voegde het vermogen toe om regex patronen te gebruiken om de **WAM_UP_PAGES** omgevingsvariabele te vormen om enige pagina&#39;s, veelvoudige domeinen, en veelvoudige pagina&#39;s in het voorgeheugen onder te brengen. Zie [ variabelen van de post-opstellen ](../environment/variables-post-deploy.md#warm_up_pages).<!--MAGECLOUD-3258-->
