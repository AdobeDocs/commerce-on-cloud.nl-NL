---
title: Patches toepassen
description: Leer hoe u patches in de Adobe Commerce kunt toepassen op een cloudinfrastructuurproject.
feature: Cloud, Upgrade
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Patches toepassen

[&#x200B; de Patches van de Wolk voor Commerce &#x200B;](https://github.com/magento/magento-cloud-patches) en het [&#x200B; Hulpmiddel van de Patches van de Kwaliteit &#x200B;](https://github.com/magento/quality-patches) leveren flarden aan uw geïnstalleerde toepassing van Adobe Commerce.

- Het Cloud Patches for Commerce-pakket biedt vereiste patches met kritieke oplossingen
- De flarden van de kwaliteit leveren facultatieve, low-impact kwaliteitsmoeilijke situaties als [&#x200B; individuele flarden &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/versioning-policy.html?lang=nl-NL#individual-patch) die achterwaartse onverenigbare veranderingen niet bevatten

Zie [&#x200B; Beschikbare Patches &#x200B;](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=nl-NL) in de _Gids van de Hulpmiddelen van de Verrichtingen van Commerce_ om een volledige lijst van vrijgegeven flarden te herzien.

Beide pakketten verbeteren de integratie van alle Adobe Commerce-versies met Cloud-omgevingen en ondersteunen snelle levering van kritieke, optionele en aangepaste oplossingen. U kunt deze pakketten gebruiken om algemene informatie over alle afzonderlijke patches die beschikbaar zijn voor Commerce toe te passen, terug te draaien en weer te geven.

>[!TIP]
>
>U kunt het [&#x200B; Hulpmiddel van de Patches van de Kwaliteit &#x200B;](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=nl-NL) en de Patches van de Wolk voor Commerce als stand-alone pakketten voor Magento Open Source en de projecten van Adobe Commerce gebruiken. We raden u aan het gereedschap Kwaliteitspatches te gebruiken voor niet-cloud-projecten.

Wanneer u wijzigingen in de externe omgeving implementeert, gebruikt het `ece-tools` -pakket `magento/magento-cloud-patches` en `magento/quality-patches` om te controleren op in behandeling zijnde patches en past het deze automatisch toe in de volgende volgorde:

1. Pas alle vereiste Commerce-patches toe die zijn opgenomen in het pakket Cloud Patches voor Commerce.
1. Geselecteerde optionele Commerce-patches toepassen die zijn opgenomen in het gereedschap Kwaliteitspatches.
1. Pas aangepaste patches toe in de map `/m2-hotfixes` in alfabetische volgorde op flardnaam.

>[!NOTE]
>
>Wanneer u het `ece-tools` -pakket of het Cloud Patches for Commerce-pakket bijwerkt, worden de meest recente vereiste patches toegepast wanneer u uw project de volgende keer implementeert. U kunt de patches ook direct implementeren met de `ece-patches apply` CLI-opdracht en de Cloud-omgeving opnieuw implementeren. U kunt niet [&#x200B; vereiste flarden &#x200B;](https://github.com/magento/magento-cloud-patches/tree/develop/patches) tijdens het plaatsingsproces overslaan.

## Vereisten

{{upgrade-tip}}

Het gereedschap Kwaliteitspatches is afhankelijk van de cloudpatches voor Commerce en het `ece-tools` -pakket. Om de recentste flarden toe te passen, moet u [&#x200B; de recentste geïnstalleerde versie van ECE-Hulpmiddelen &#x200B;](../dev-tools/update-package.md) hebben. De minimaal vereiste versie van ECE-Tools is 2002.1.2.

## Beschikbare patches en status weergeven

U kunt als volgt de lijst met beschikbare afzonderlijke patches weergeven:

```bash
php ./vendor/bin/ece-patches status
```

Monsterrespons:

```
More detailed information about patches you can find on https://support.magento.com/
╔════════════════╤═════════════════════════════════════════════════╤══════════╤═════════════╤═════════════════════════════════╗
║ Id             │ Title                                           │ Type     │ Status      │ Details                         ║
╠════════════════╪═════════════════════════════════════════════════╪══════════╪═════════════╪═════════════════════════════════╣
║ MAGECLOUD-5069 │ FPC is getting disabled during deployments      │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-page-cache    ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5650    │ Hold deployment config after reading from file  │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5684    │ Pagination Not working - product_list_limit=all │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-elasticsearch ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-65837       │ Fix load balancer issue                         │Deprecated│ Applied     │ Recommended replacement: MC-1   ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ BUNDLE-2554    │ Set Payment info bug                            │ Required │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - amzn/amazon-pay-module       ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-1           │ Fixes issue 1                                   │ Optional │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-2           │ Fixes issue 2                                   │ Optional │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-3           │ Fixes issue 3                                   │ Optional │ Not applied │ Required patches:               ║
║                │                                                 │          │             │  - MC-2                         ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ N/A            │ ../m2-hotfixes/MDVA_custom__2.3.5_ce.patch      │ Custom   │ N/A         │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-framework     ║
╚════════════════╧═════════════════════════════════════════════════╧══════════╧═════════════╧═════════════════════════════════╝
Magento 2 Enterprise Edition, version 2.3.5.0
```

De statustabel bevat de volgende soorten informatie:

- **Type**:
   - `Optional` - Alle patches van het gereedschap Kwaliteitspatches en het pakket Cloudepatches zijn optioneel voor installatie van Adobe Commerce en Magento Open Source. Voor Adobe Commerce op cloud-infrastructuur zijn alle patches optioneel.
   - `Required` - Alle patches uit het pakket Cloud Patches voor Commerce zijn vereist voor klanten van de cloud.
   - `Deprecated` - De afzonderlijke patch is gemarkeerd als afgekeurd en we raden u aan de patch terug te draaien als u deze hebt toegepast. Nadat u een vervangen patch hebt hersteld, wordt deze niet meer weergegeven in de statustabel.
   - `Custom` - Alle patches uit de map &#39;m2-hotfixes&#39;.

- **Status**:
   - `Applied` - De patch is toegepast.
   - `Not applied` - De patch is niet toegepast.
   - `N/A` - De status van de patch kan niet worden gedefinieerd vanwege conflicten.

- **Details**:
   - `Affected components` - De lijst van beïnvloede modules.
   - `Required patches` - De lijst met vereiste patches (afhankelijkheden).
   - `Recommended replacement` - De patch die een aanbevolen vervanging voor een vervangen patch is.

## Een patch toepassen in een lokale omgeving

U kunt patches handmatig toepassen in een lokale omgeving en ze testen voordat u ze implementeert.

**om individuele flarden in een lokale ontwikkelomgeving toe te passen**:

1. Voeg de variabele &#39;QUALITY_PATCH&#39; toe aan het bestand `.magento.env.yaml` en maak een lijst met de vereiste patches eronder.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

1. Pas de patches toe vanuit de projecthoofdmap.

   ```bash
   php ./vendor/bin/ece-patches apply
   ```

   Met de opdracht `ece-patches apply` past u patches in de volgende volgorde toe:
   - Vereiste patches
   - Optionele afzonderlijke patches
   - Aangepaste patches uit de map `/m2-hotfixes`

1. Wis de cache.

   ```bash
   php ./bin/magento cache:clean
   ```

1. Test de patches en breng de benodigde wijzigingen aan in aangepaste patches.

## Een patch toepassen in een externe omgeving

>[!WARNING]
>
>We raden u ten zeerste aan om alle patches in een integratie- of testomgeving te testen voordat u deze implementeert in de productieomgeving.

**om flarden in een ver milieu** toe te passen:

1. Voeg de variabele `QUALITY_PATCHES` toe aan het `.magento.env.yaml` -bestand en geef een overzicht van de vereiste patches eronder.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

   >[!NOTE]
   >
   >Nadat u de upgrade naar een nieuwe versie van Adobe Commerce hebt uitgevoerd, moet u de patches opnieuw toepassen als de patches niet in de nieuwe versie zijn opgenomen.

1. Voeg het bijgewerkte `.magento.env.yaml` -bestand toe, wijs het toe en duw erop.

   ```bash
   git add .magento.env.yaml
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

## Een aangepaste patch toepassen

Wanneer u opstelt, past ECE-Tools alle patches voor Adoben en aangepaste patches toe die u toevoegt aan de map `/m2-hotfixes` in de hoofdmap van het project.

>[!NOTE]
>
>Alle namen van patchbestanden moeten eindigen met de extensie `.patch` .

**om een douaneflard op een milieu van de Wolk toe te passen en te testen**:

1. Maak in de hoofdmap van het project een map met de naam `m2-hotfixes` als deze niet bestaat

   ```bash
   mkdir m2-hotfixes
   ```

1. Kopieer het patchbestand naar de map `/m2-hotfixes` .

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Zorg ervoor dat u alle pleisters test in een pre-productieomgeving. Voor Adobe Commerce op cloudinfrastructuur kunt u vertakkingen maken met de opdracht `magento-cloud environment:branch <branch-name>` CLI.

## Een aangepaste patch herstellen

Een eerder toegepaste aangepaste patch herstellen of verwijderen:

1. Verwijder het patchbestand uit de map `/m2-hotfixes` .

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Revert patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Zorg ervoor dat u test in een pre-productieomgeving. Voor Adobe Commerce op cloudinfrastructuur kunt u vertakkingen maken met de opdracht `magento-cloud environment:branch <branch-name>` CLI.

## Patches toepassen op een niet-cloud-project

Gebruik het [&#x200B; Hulpmiddel van de Patches van de Kwaliteit &#x200B;](https://github.com/magento/quality-patches) voor Magento Open Source en de projecten van Adobe Commerce.

## Een patch herstellen in een lokale omgeving

U kunt alle eerder toegepaste patches in een lokale ontwikkelomgeving herstellen met de CLI van `ece-patches` .

Alle toegepaste patches herstellen:

```bash
php ./vendor/bin/ece-patches revert
```

Met deze opdracht worden alle patches in de volgende volgorde teruggezet:

- Keert alle toegepaste douaneflarden van /m2-hotfixes folder om.
- Hiermee worden alle toegepaste optionele afzonderlijke patches omgekeerd.
- Hiermee herstelt u alle toegepaste vereiste patches.

## Logboekregistratie

Met het gereedschap Kwaliteitspatches registreert u alle bewerkingen in het `<Project_root>/var/log/patch.log` -bestand.
