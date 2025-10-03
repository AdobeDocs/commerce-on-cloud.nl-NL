---
title: Commerce-versie upgraden
description: Leer hoe u de Adobe Commerce-versie kunt upgraden in de cloud-infrastructuuromgeving.
feature: Cloud, Upgrade
exl-id: 0cc070cf-ab25-4269-b18c-b2680b895c17
source-git-commit: 7f9aac358effdf200b59678098e6a1635612301b
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Commerce-versie upgraden

U kunt de Adobe Commerce-codebasis upgraden naar een nieuwere versie. Alvorens het milieu te bevorderen, herzie de [&#x200B; vereisten van het Systeem &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in de _gids van de Installatie_ voor de recentste vereisten van de softwareversie.

Afhankelijk van het milieutype (Ontwikkeling, het Opvoeren, of de Productie), kunnen uw verbeteringstaken het volgende omvatten:

- Werk het `.magento/services.yaml` -bestand bij met nieuwe versies voor MariaDB (MySQL), OpenSearch, RabbitMQ en Redis voor compatibiliteit met nieuwe Adobe Commerce-versies.
- Werk het `.magento.app.yaml` dossier met nieuwe montages voor haken en omgevingsvariabelen bij.
- Voer een upgrade uit van externe extensies naar de nieuwste ondersteunde versie.

{{upgrade-tip}}

{{pro-update-service}}

## Configuratiebestanden

Voordat u de toepassing kunt upgraden, moet u de projectconfiguratiebestanden bijwerken om rekening te houden met wijzigingen in de standaardconfiguratie-instellingen voor Adobe Commerce op de cloudinfrastructuur of de toepassing. De recentste gebreken kunnen in de [&#x200B; magento-cloud bewaarplaats GitHub &#x200B;](https://github.com/magento/magento-cloud) worden gevonden.

### composer.json

Controleer voordat u de upgrade uitvoert of de afhankelijkheden in het `composer.json` -bestand compatibel zijn met de Adobe Commerce-versie.

U kunt als volgt het `composer.json` -bestand voor Adobe Commerce versie 2.4.4 en hoger** bijwerken:

1. Voeg het volgende `allow-plugins` toe aan de sectie `config` :

   ```json
   "config": {
      "allow-plugins": {
         "dealerdirect/phpcodesniffer-composer-installer": true,
         "laminas/laminas-dependency-plugin": true,
         "magento/*": true
      }
   },
   ```

1. Voeg de volgende plug-in toe aan de sectie `require` :

   ```json
   "require": {
       "magento/composer-root-update-plugin": "^2.0.3"
   },
   ```

1. Voeg de volgende component toe aan de sectie `extra:component_paths` :

   ```json
   "extra": {
      "component_paths": {
         "tinymce/tinymce": "lib/web/tiny_mce_5"
      },
   },
   ```

1. Sla het bestand op. Wijzig de vertakking nog niet en duw er nog niet op.

1. Ga door met het upgradeproces.

## Omgevingsback-up

We raden u aan een back-up van de instantie te maken voordat u de upgrade uitvoert. Gebruik de volgende stappen om een back-up te maken van uw integratie-, staging- en productieomgevingen.

**aan file uw gegevensbestand van het integratiemilieu en code**:

1. Maak een lokale back-up van de externe database.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >Het `magento-cloud db:dump` bevel stelt het [&#x200B; mysqldump &#x200B;](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) bevel met de `--single-transaction` vlag in werking, die u aan file uw gegevensbestand zonder de lijsten te sluiten toestaat.

1. Maak een back-up van code en media.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   U kunt `[--media]` ook weglaten als u een groot aantal statische bestanden hebt die al in bronbeheer staan.

**aan file uw het Staging of milieu gegevensbestand van de Productie alvorens** op te stellen:

1. Gebruik SSH om u aan te melden bij de externe omgeving.

1. Creeer a [&#x200B; gegevensbestandstortplaats &#x200B;](../storage/database-dump.md). Als u een doelmap voor de DB-dump wilt kiezen, gebruikt u de optie `--dump-directory` .

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   Met de dump-bewerking maakt u een `dump-<timestamp>.sql.gz` archiefbestand in uw externe projectmap. Zie [&#x200B; file gegevensbestand &#x200B;](../storage/database-dump.md).

## Toepassingsupgrade

Herzie de [&#x200B; informatie van de de dienstversies &#x200B;](../services/services-yaml.md#service-versions) voor de recentste vereisten van de softwareversie alvorens uw toepassing te bevorderen.

**om de toepassingsversie** te bevorderen:

1. Wijzig op uw lokale werkstation de projectmap.

1. Plaats de [&#x200B; versiebeperking &#x200B;](overview.md#cloud-metapackage) voor de versie van de doelverbetering. Deze stap is alleen nodig als de doelversie zich buiten de bestaande beperking bevindt.

   ```bash
   composer require-commerce "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >U moet de syntaxis van de versiebeperking gebruiken om het `ece-tools` -pakket bij te werken. U kunt de versiebeperking in het `composer.json` dossier voor de versie van het [&#x200B; toepassingsmalplaatje &#x200B;](https://github.com/magento/magento-cloud/blob/master/composer.json) vinden u voor de verbetering gebruikt.

1. Werk uw `composer.json` -bestand bij met de belangrijkste Commerce-upgradeversie.

   ```bash
   composer require-commerce magento/product-enterprise-edition 2.4.8 --no-update
   ```

1. Als u B2B gebruikt, werk uw `composer.json` dossier met de [&#x200B; gesteunde versie &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability#adobe-authored-extensions) voor Commerce bij.

   ```bash
   composer require-commerce magento/extension-b2b 1.5.2 --no-update
   ```

1. Projectafhankelijkheden bijwerken.

   ```bash
   composer update
   ```

1. Bekijk de patches die momenteel worden toegepast:

   - Als er om het even welke die flarden in de `m2-hotfixes` folder worden geïnstalleerd zijn, [&#x200B; voorlegt een kaartje van de Steun van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-case) en het werk met de Steun van Adobe Commerce om te verifiëren welke flarden nog op de nieuwe versie kunnen worden toegepast. Verwijder de niet-toepasselijke patch(es) uit de map `m2-hotfixes` .

   - Als er om het even welke [ Patches van de Kwaliteit ] in het `.magento.env.yaml` dossier worden toegepast, verifieer of zij nog op de nieuwe versie kunnen worden toegepast. Verwijder de niet-toepasselijke patch(es) uit de sectie `QUALITY_PATCHES` van het `.magento.env.yaml` -bestand.

   **Methode 1**: [&#x200B; verifieer de toepasselijke versies in de de versienota&#39;s van de Patches van de Kwaliteit &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/release-notes)

   **Methode 2**: [&#x200B; de beschikbare flarden van de Mening en status &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/upgrade/apply-patches#view-available-patches-and-status)

   **Methode 3**: [&#x200B; Onderzoek naar flarden &#x200B;](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=en)


1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Upgrade"
   ```

   ```bash
   git push origin <branch-name>
   ```

   `git add -A` is vereist om alle gewijzigde bestanden toe te voegen aan bronbesturing vanwege de manier waarop Composer basispakketten marshals. Zowel `composer install` als `composer update` marshal dossiers van het basispakket (`magento/magento2-base` en `magento/magento2-ee-base`) in de pakketwortel.

   De bestanden die Composer marshals hebben, horen bij de nieuwe versie van Adobe Commerce, om de verouderde versie van dezelfde bestanden te overschrijven. Op dit moment is het rangschikken in Adobe Commerce uitgeschakeld, dus u moet de gemarcheerde bestanden toevoegen aan bronbesturing.

1. Wacht tot de implementatie is voltooid.

1. Verifieer de verbetering in uw Integratie, het Staging, of milieu van de Productie door SSH te gebruiken om login en de versie te controleren.

   ```bash
   php bin/magento --version
   ```

### Extensies upgraden

Bekijk de extensie- en modulepagina&#39;s van derden in Marketplace of andere bedrijfssites en controleer de ondersteuning voor Adobe Commerce en Adobe Commerce op cloudinfrastructuur. Als u extensies en modules van derden moet bijwerken, raadt Adobe aan te werken in een nieuwe integratietak met uw extensies uitgeschakeld.

**om uw uitbreidingen** te verifiëren en te bevorderen:

1. Maak een vertakking op uw lokale werkstation.

1. Schakel de extensies desgewenst uit.

1. Indien beschikbaar, downloadextensies voor upgrades.

1. Installeer de upgrade zoals wordt beschreven in de documentatie van derden.

1. Schakel de extensie in en test deze.

1. Voeg de wijzigingen aan de externe code toe, wijs deze aan en duw erop.

1. Zet uw integratieomgeving aan en test deze.

1. Druk op de testomgeving om te testen in een pre-productieomgeving.

Adobe adviseert sterk bevordering uw milieu van de Productie _vóór_ met inbegrip van de promotieuitbreidingen in uw proces van de plaatslancering.

>[!NOTE]
>
>Wanneer u uw toepassingsversie bevordert, werkt het verbeteringsproces aan de recentste versie van de [&#x200B; Snelle CDN module &#x200B;](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automatisch bij.

## Upgrade problemen oplossen

Als de upgrade is mislukt, ontvangt u een foutbericht in de browser waarin wordt aangegeven dat u geen toegang hebt tot uw winkel of het deelvenster Beheer:

```
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**om de fout** op te lossen:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Open het `./app/var/report/<error number>` -bestand.

1. [&#x200B; onderzoek de logboeken &#x200B;](../test/log-locations.md) en bepaal de bron van de kwestie.

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
