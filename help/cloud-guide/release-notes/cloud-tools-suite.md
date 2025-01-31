---
title: Opmerkingen bij de release Cloud Tools Suite
description: Meer informatie over de nieuwste verbeteringen in de Cloud Tools Suite voor Adobe Commerce.
feature: Cloud, Release Notes
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Opmerkingen bij de release voor de Commerce Cloud Tools Suite

Deze release bevat informatie over de meest recente verbeteringen in de Cloud Tools Suite voor Commerce-pakketten die zijn ontworpen om Adobe Commerce-installaties en -upgrades op het Cloud-platform te implementeren en beheren.

| Opmerkingen bij de release | Versie | Beschrijving | Source |
| ----------------- |-----------| ---------------------------------------- | --------------------------- |
| [`ece-tools` package ](ece-tools-package.md) | 2002,2,0 | Een set scripts en tools die zijn ontworpen voor het beheren en implementeren van Cloud-projecten | [`magento/ece-tools`](https://github.com/magento/ece-tools/tree/2002.2.0) |
| [ Haalt de Patches van de Wolk voor Commerce ](cloud-patches.md) | 1.1.0. | Een reeks patches die de integratie van alle Adobe Commerce-versies in de Cloud-omgeving verbeteren. Dit pakket bevat Adobe Commerce-patches en beschikbare hotfixes die worden toegepast wanneer u `ece-tools` gebruikt om | [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches/tree/1.1.0) |
| [ Docker van de Wolk voor Commerce ](cloud-docker.md) | 1.4.0. | Functie- en configuratiebestanden voor Docker-images om Adobe Commerce in een lokale cloudomgeving te implementeren | [`magento/magento-cloud-docker`](https://github.com/magento/magento-cloud-docker/tree/1.0) |
| [ de Componenten van de Wolk van Commerce ](cloud-components.md) | 1.1.0. | Uitgebreide Adobe Commerce-kernfunctionaliteit voor sites die worden geïmplementeerd op de Cloud-infrastructuur | [`magento/magento-cloud-components`](https://github.com/magento/magento-cloud-components/tree/1.1.0) |

Wanneer u een update uitvoert naar ECE-Tools 2002.1.0 of hoger, wordt automatisch een update uitgevoerd naar de nieuwste versies van de andere pakketten. Dit zijn afhankelijkheden voor het `ece-tools` -pakket. Zie [ het metapakket van de Wolk ](../development/overview.md#cloud-metapackage) voor een lijst van gebiedsdelen.

De nieuwe versie van `ece-tools` (2002.2.0) is alleen beschikbaar in PHP versie 8.1 en hoger (8.2, 8.3). Oudere PHP versies zijn afgekeurd (7.4, 7.3, 7.2). U kunt eerdere versies van `ece-tools` gebruiken met oude PHP versies.
