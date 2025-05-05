---
title: '[!DNL ECE-Tools] Pakket maken'
description: Leer over het  [!DNL ECE-Tools]  pakket en hoe het helpt om Adobe Commerce te beheren en op te stellen.
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# ECE-gereedschapspakket

Het [!DNL ECE-Tools] -pakket is een set scripts en gereedschappen die zijn ontworpen voor het beheren en implementeren van de [!DNL Commerce] -toepassing. Het `ece-tools` -pakket vereenvoudigt veel processen, zoals het beheren van uitsnijdtaken, het controleren van de projectconfiguratie en het toepassen van patches voor Adoben en hotfixes. U kunt bekijken en tot de [ open-bron  [!DNL ECE-Tools]  codebewaarplaats op GitHub ][ece-repo] bijdragen.

{{ece-tools-package}}

Het `ece-tools` -pakket is compatibel met Adobe Commerce (vanaf versie 2.1.4) en bevat scripts en Adobe Commerce voor opdrachten in de cloud-infrastructuur die zijn ontworpen om u te helpen uw code te beheren en automatisch uw projecten te maken en implementeren.

In het volgende voorbeeld worden de beschikbare `ece-tools` opdrachten weergegeven:

```bash
php ./vendor/bin/ece-tools list
```

## Samenstellen en implementeren

Het `ece-tools` -pakket bevat opdrachten voor het uitvoeren van bewerkingen voor de fasen van het maken, implementeren en na implementatie van het starten van uw Adobe Commerce op een cloudinframetoepassing. De opdracht `php ./vendor/bin/ece-tools build` begint bijvoorbeeld het bouwproces van de toepassing.

Door gebrek, zijn deze `ece-tools` bevelen in het [ hooks bezit ](../application/hooks-property.md) van het `.magento.app.yaml` configuratiedossier.

## Docker-configuratiegenerator

Het `ece-tools` pakket omvat een gebiedsdeel voor het [ magento/magento-cloud-docker ] pakket, dat functionaliteit en configuratiedossiers voor de beelden van Docker verstrekt om een de ontwikkelomgeving van het Docker voor Adobe Commerce op wolkeninfrastructuur te lanceren. U kunt Cloud Docker voor Commerce ook als een zelfstandig pakket uitvoeren. Zie {de ontwikkeling van 0} Docker [&#128279;](../dev-tools/cloud-docker.md).

## Services, routes en variabelen

U kunt het `ece-tools` pakket gebruiken om gedetailleerde informatie over Base64-Gecodeerde [ variabelen van de Wolk te tonen ](../environment/variables-cloud.md) die in om het even welk milieu van de Wolk worden gebruikt. Het volgende bevel toont alle diensten, routes, en variabelen.

```bash
php ./vendor/bin/ece-tools env:config:show
```

Als u een specifieke set gegevens wilt weergeven, gebruikt u de volgende indeling:

```bash
php ./vendor/bin/ece-tools env:config:show <option>
```

- `services` - Geeft de relatiegegevens weer van de `MAGENTO_CLOUD_RELATIONSHIPS` omgevingsvariabele, gedefinieerd in het `services.yaml` -bestand.
- `routes` - Toont de gevormde routes voor het project gebruikend de `MAGENTO_CLOUD_ROUTES` omgevingsvariabele.
- `variables` - Toont de gevormde variabelen voor het project gebruikend de `MAGENTO_CLOUD_VARIABLES` omgevingsvariabele.

Voorbeelduitvoer voor de optie `services` :

```
Magento Cloud Services:
+-----------------------------------+----------------------------------+
| Service Configuration             | Value                            |
+-----------------------------------+----------------------------------+
| database:                                                            |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| password                          | <password>                       |
| port                              | 3306                             |
+-----------------------------------+----------------------------------+
| opensearch:                                                          |
+-----------------------------------+----------------------------------+
| host                              | 127.0.0.1                        |
| port                              | 9200                             |
...
```

## Omgevingsconfiguratie controleren

Er is een reeks verificatiebevelen beschikbaar helpen de configuratie van uw project evalueren. Zie [ Slimme tovenaars ](../deploy/smart-wizards.md) in _plaatsing_ sectie voor een gedetailleerde beschrijving van elk tovenaarsbevel optimaliseren. De opdracht `wizard:ideal-state` wordt automatisch uitgevoerd tijdens de constructiefase. Om de ideale staat van uw project te verifiëren:

```bash
php ./vendor/bin/ece-tools wizard:ideal-state
```

>[!NOTE]
>
>U moet de opdracht `wizard:ideal-state` uitvoeren in de externe cloud-omgeving. De opdracht retourneert altijd de fout `The configured state is not ideal` wanneer deze wordt uitgevoerd in de lokale ontwikkelomgeving.

Voorbeelduitvoer:

```
Ideal state is configured
```

Zie [ de nota&#39;s van de Versie voor kind-hulpmiddelen ](../release-notes/cloud-tools-suite.md).

## Patches voor Adoben en aangepaste patches

Het `ece-tools` pakket omvat een gebiedsdeel voor het [ magento/magento-cloud-flarden ] pakket, dat Adobe flarden en hete moeilijke situaties levert die de integratie van alle versies van Adobe Commerce met de milieu&#39;s van de Wolk verbeteren en snelle levering van kritieke moeilijke situaties steunt. De &quot;levert ook aangepaste patches die u toevoegt aan uw Adobe Commerce op het project voor cloudinfrastructuur. Zie [ flarden ](../development/apply-patches.md) toepassen.

<!-- link definitions -->

[ece-repo]: https://github.com/magento/ece-tools
[magento/magento-cloud-docker]: https://github.com/magento/magento-cloud-docker
[magento/magento-cloud-patches]: https://github.com/magento/magento-cloud-patches
