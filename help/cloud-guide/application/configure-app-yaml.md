---
title: Implementatie van toepassingen configureren
description: Leer hoe te om de eigenschappen in het dossier van de toepassingsconfiguratie te vormen die de manier controleren  [!DNL Commerce]  toepassing bouwt en aan het milieu van de Wolk opstelt.
feature: Cloud, Configuration, Build, Deploy
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Implementatie van toepassingen configureren

Het bestand `.magento.app.yaml` bepaalt de manier waarop uw toepassing wordt gemaakt en geïmplementeerd. Hoewel Adobe Commerce op cloudinfrastructuur meerdere toepassingen per project ondersteunt, heeft een project doorgaans één toepassing met het `.magento.app.yaml` -bestand aan de basis van de opslagplaats.

`.magento.app.yaml` heeft vele standaardwaarden, zie [ een steekproef `.magento.app.yaml` dossier ](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml). Controleer altijd `.magento.app.yaml` voor uw geïnstalleerde versie. Dit bestand kan in Adobe Commerce verschillen in versies van de cloudinfrastructuur.

Gebruik het bestand `.magento.app.yaml` om de volgende configuratiewaarden te definiëren:

- [ Eigenschappen ](properties.md) - bepaal bezitswaarden voor toepassingsinstantie.
- [ het bezit van Variabelen ](variables-property.md) - de milieuvariabelen van het Overzicht die voor de [!DNL Commerce] toepassingsversie worden vereist.
- [ PHP montages ](php-settings.md) - vorm runtime PHP opties.
- [ plaats Geheime voorgeheugen voor Statische Dossiers ](set-cache.md) - plaats geheim voorgeheugen TTL voor uw media en statische dossiers.

>[!NOTE]
>
>Het `.magento.app.yaml` -bestand wordt lokaal of in de it-opslagplaats beheerd. De configuratie wordt slechts gelezen voor het doel van de plaatsing en bouwt proces en wordt verwijderd nadat de plaatsing is voltooid, zodat zult u het niet op de server vinden.
