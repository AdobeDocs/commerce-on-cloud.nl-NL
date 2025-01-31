---
title: Upgradeproject voor gebruik van ECE-tools
description: Leer hoe u een upgrade uitvoert van uw Adobe Commerce op een cloud-infrastructuurproject, zodat u het pakket ECE-Tools kunt gebruiken en de nieuwste oplossingen en functies kunt benutten.
feature: Cloud, Install
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Upgradeproject voor gebruik van het pakket ECE-Tools

Adobe heeft de pakketten `magento/magento-cloud-configuration` en `magento/ece-patches` vervangen door het pakket `ece-tools` , dat veel cloudprocessen vereenvoudigt. Als u een oudere Adobe Commerce op het project van de wolkeninfrastructuur gebruikt dat _niet_ het `ece-tools` pakket bevat, dan moet u een eenmalig, manueel _verbetering_ proces aan uw project uitvoeren.

>[!WARNING]
>
>Als uw project het `ece-tools` -pakket bevat, kunt u de volgende upgrade overslaan. Als u wilt controleren, haalt u de [!DNL Commerce] -versie op met de opdracht `php vendor/bin/ece-tools -V` in de lokale hoofdmap van het project.

Voor dit upgradeproces van het project moet u de versiebeperking `magento/magento-cloud-metapackage` bijwerken in het `composer.json` -bestand in de hoofdmap. Met deze beperking kunnen updates voor Adobe Commerce worden uitgevoerd op metapakketten voor cloudinfrastructuur, zoals het verwijderen van verouderde pakketten, zonder dat de huidige Adobe Commerce-versie wordt bijgewerkt.

{{upgrade-tip}}

## Vervangen pakketten verwijderen

Voordat u een upgrade uitvoert voor het gebruik van het `ece-tools` -pakket, controleert u het `composer.lock` -bestand op de volgende verouderde pakketten:

- `magento/magento-cloud-configuration`
- `magento/ece-patches`

## Het pakket metapakketten bijwerken

Voor elke Adobe Commerce-versie is een andere beperking vereist op basis van het volgende:

```
>=current_version <next_version
```

- Geef bij `current_version` de Adobe Commerce-versie op die u wilt installeren.
- Geef bij `next_version` de volgende patchversie op na de waarde die is opgegeven in `current_version` .

Als u Adobe Commerce `2.3.5-p2` wilt installeren, stelt u `current_version` in op `2.3.5` en `next_version` op `2.3.6` . Met de restrictie `">=2.3.5 <2.3.6"` wordt het meest recente beschikbare pakket voor 2.3.5 geïnstalleerd.

U kunt de recentste metapakketbeperking in het [`magento-cloud` malplaatje ](https://github.com/magento/magento-cloud/blob/master/composer.json) altijd vinden.

In het volgende voorbeeld wordt een beperking voor het Adobe Commerce-pakket voor de infrastructuur van de cloud geplaatst in elke versie die hoger is dan of gelijk is aan de huidige versie 2.4.7 en lager is dan de volgende versie 2.4.8:

```json
"require": {
    "magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
},
```

## Het project upgraden

Als u uw project wilt upgraden voor gebruik van het `ece-tools` -pakket, moet u het metapakket en de `.magento.app.yaml` hooks-eigenschappen bijwerken en een Composer-update uitvoeren.

**om project te bevorderen om knoop-hulpmiddelen** te gebruiken:

1. Werk de `magento/magento-cloud-metapackage` version-restrictie in het `composer.json` -bestand bij.

   ```bash
   composer require "magento/magento-cloud-metapackage":">=2.4.7 <2.4.8" --no-update
   ```

1. Werk het metapakket bij.

   ```bash
   composer update magento/magento-cloud-metapackage
   ```

1. Wijzig de haakbevelen in het `magento.app.yaml` dossier.

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Controle voor en verwijder de [ afgekeurde pakketten ](#remove-deprecated-packages). De vervangen pakketten kunnen een geslaagde upgrade verhinderen.

   ```bash
   composer remove magento/magento-cloud-configuration
   ```

   ```bash
   composer remove magento/ece-patches
   ```

1. Het kan nodig zijn om het `ece-tools` -pakket bij te werken.

   ```bash
   composer update magento/ece-tools
   ```

1. Voeg de codewijzigingen toe en wijs deze toe. In dit voorbeeld zijn de volgende bestanden bijgewerkt:

   ```
   .magento.app.yaml
   composer.json
   composer.lock
   ```

1. Duw de codeveranderingen in de verre server en voeg deze tak met de `integration` tak samen.

   ```bash
   git push origin <branch-name>
   ```
