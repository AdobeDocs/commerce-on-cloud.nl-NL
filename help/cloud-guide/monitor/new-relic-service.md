---
title: New Relic-service
description: Meer informatie over de New Relic-service die beschikbaar is bij uw Adobe Commerce-project voor cloudinfrastructuur.
feature: Cloud, Observability
last-substantial-update: 2023-09-06T00:00:00Z
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Overzicht van New Relic-services

Alle Adobe Commerce-projecten op cloudinfrastructuur bieden toegang tot de New Relic-service om de prestaties te controleren en gebeurtenissen van de [!DNL Commerce] -toepassing en cloudinfrastructuur te onderzoeken.

De volgende New Relic-functies zijn beschikbaar voor gebruik in Productie- en Staging-omgevingen:

- [ New Relic APM ](#new-relic-apm) (Pro en Starter)
- [ de Infrastructuur van New Relic ](#new-relic-infrastructure) (Pro slechts)
- [ het Beheer van het Logboek van New Relic ](#new-relic-log-management) (Pro slechts)

>[!INFO]
>
>Andere New Relic-functies zijn niet beschikbaar voor Adobe Commerce-projecten.

## NEW RELIC APM

[ New Relic voor het beheer van toepassingsprestaties (APM) ](https://docs.newrelic.com/introduction-apm/) is een product van de softwareanalyse dat u helpt toepassingsinteractie analyseren en verbeteren. New Relic APM is beschikbaar voor alle Adobe Commerce voor cloud-infrastructuurprojecten en biedt de volgende functies:

- **concentreert zich op specifieke transacties** - merk en controleer actief zeer belangrijke klantenacties in uw plaats, zoals het toevoegen aan de kar, het controleren, of het verwerken van een betaling.
- **de vraag van het Gegevensbestand controle** - plaats en controleer gegevensbestandvragen die prestaties beïnvloeden.
- **App Kaart** - bekijk alle toepassingsgebiedsdelen binnen uw plaats, uitbreidingen, en de externe diensten.
- **[!DNL Apdex]scores** - evalueer prestaties en creeer alarm dat kwesties identificeert en u op de hoogte brengt wanneer zij voorkomen, zoals plaatsprestaties die door een flitsverkoop of Webgebeurtenis worden beïnvloed. Zie [ score van de Index ](https://docs.newrelic.com/docs/apm/new-relic-apm/apdex/apdex-measure-user-satisfaction/).
- **Beheerde alarm voor Adobe Commerce** - gebruik dit de waakzame beleid van New Relic om toepassing en infrastructuurprestaties te controleren die op industrie beste praktijken worden gebaseerd. Zie [ prestaties van de Monitor met het Beheerde alarm voor het waakzame beleid van Adobe Commerce ](investigate-performance.md/#monitor-performance-with-managed-alerts).
- **plaatsingen van het Spoor** - de plaatsingsgebeurtenissen van de Monitor en analyseer plaatsingseffect aan algemene prestaties. Zie [ plaatsingen van het Spoor ](track-deployments.md).

Uw Adobe Commerce on cloud-infrastructuurproject bevat de software voor de New Relic APM-service, samen met een licentiecode. U hoeft geen extra software aan te schaffen of te installeren.

## New Relic-infrastructuur

De pro projecten omvatten de [ dienst van de Infrastructuur van New Relic (NRI) ](https://docs.newrelic.com/docs/infrastructure/infrastructure-monitoring/get-started/get-started-infrastructure-monitoring/), die automatisch met de toepassingsgegevens en prestatiesanalyses verbindt om dynamische servercontrole te verstrekken. Deze service is beschikbaar in Pro Production- en Staging-omgevingen.

## New Relic-logbeheer

Alle projecten van de wolkeninfrastructuur omvatten [ het logboekbeheer van New Relic ](log-management.md). De dienst wordt pre-gevormd om alle logboekgegevens van uw het Opvoeren en milieu&#39;s van de Productie samen te voegen en het in een gecentraliseerd logboekbeheersdashboard te tonen.
