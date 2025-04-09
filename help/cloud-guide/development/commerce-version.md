---
title: Commerce-versie upgraden
description: Leer hoe u de Adobe Commerce-versie kunt upgraden in het cloud-infrastructuurproject.
feature: Cloud, Upgrade
exl-id: 0cc070cf-ab25-4269-b18c-b2680b895c17
source-git-commit: 1cea1cdebf3aba2a1b43f305a61ca6b55e3b9d08
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 0%

---

# Commerce-versie upgraden

U kunt de Adobe Commerce-codebasis upgraden naar een nieuwere versie. Alvorens uw project te bevorderen, herzie de [ vereisten van het Systeem ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in de _gids van de Installatie_ voor de recentste vereisten van de softwareversie.

Afhankelijk van uw projectconfiguratie, kunnen uw verbeteringstaken het volgende omvatten:

- Werk services bij, zoals MariaDB (MySQL), OpenSearch, RabbitMQ en Redis, voor compatibiliteit met nieuwe Adobe Commerce-versies.
- Converteer een ouder configuratiebeheerbestand.
- Werk het `.magento.app.yaml` bestand bij met nieuwe instellingen voor hooks en omgevingsvariabelen.
- Voer een upgrade uit van externe extensies naar de nieuwste ondersteunde versie.
- Werk het `.gitignore` bestand bij.

{{upgrade-tip}}

{{pro-update-service}}

## Upgrade uitvoeren vanaf oudere versies

Als u met een verbetering van een versie van Commerce ouder dan 2.1 begint, kunnen sommige beperkingen in de codebasis van Adobe Commerce uw capaciteit beïnvloeden om __ aan een specifieke ECE-Hulpmiddelen versie of aan _verbetering_ aan de volgende gesteunde versie van Commerce bij te werken. Gebruik de volgende tabel om het beste pad te bepalen:

| Huidige versie | Upgradepad |
| ----------------- | ------------ |
| 2.1.3 en eerdere versies | Upgrade Adobe Commerce naar versie 2.1.4 of hoger voordat u verder gaat. Voer vervolgens een [eenmalige upgrade uit om ECE-Tools](../dev-tools/install-package.md) te installeren. |
| 2.1.4 - 2.1.14 | [ Update ECE-Hulpmiddelen ](../dev-tools/update-package.md) pakket.<br> zie versienota&#39;s voor [ 2002.0.9 ](../release-notes/cloud-release-archive.md#v200209) en recentere versies 2002.0.x. |
| 2.1.15 - 2.1.16 | [ Update ECE-Hulpmiddelen ](../dev-tools/update-package.md) pakket.<br> zie versienota&#39;s voor [ 2002.0.9 ](../release-notes/cloud-release-archive.md#v200209) en later. |
| 2.2.x en hoger | [ Update ECE-Hulpmiddelen ](../dev-tools/update-package.md) pakket.<br> zie versienota&#39;s voor [ 2002.0.8 ](../release-notes/cloud-release-archive.md#v200208) en later. |

{style="table-layout:auto"}

{{ece-tools-package}}

## Configuratiebeheer

Oudere versies van Adobe Commerce, zoals 2.1.4 of hoger tot 2.2.x of hoger, hebben een `config.local.php` -bestand gebruikt voor configuratiebeheer. Adobe Commerce versie 2.2.0 en hoger gebruiken het `config.php` -bestand, dat precies hetzelfde werkt als het `config.local.php` -bestand, maar dat andere configuratie-instellingen heeft, waaronder een lijst met de ingeschakelde modules en aanvullende configuratieopties.

Wanneer u een upgrade uitvoert vanaf een oudere versie, moet u het `config.local.php` -bestand migreren om het nieuwere `config.php` -bestand te kunnen gebruiken. Gebruik de volgende stappen om een back-up van het configuratiebestand te maken en een bestand te maken.

**Een tijdelijk `config.php` bestand** maken:

1. Maak een kopie van het `config.local.php` -bestand en noem het `config.php` .

1. Voeg dit bestand toe aan de map `app/etc` van uw project.

1. Voeg het bestand toe en wijs het toe aan uw vertakking.

1. Verplaats het bestand naar de integratietak.

1. Ga door met het upgradeproces.

>[!WARNING]
>
>Na de upgrade kunt u het `config.php` -bestand verwijderen en een nieuw, volledig bestand genereren. U kunt dit bestand alleen deze keer verwijderen om het te vervangen. Nadat u een nieuw, volledig `config.php` bestand hebt gegenereerd, kunt u het bestand niet verwijderen om een nieuw bestand te genereren. Zie [Configuratiebeheer en implementatie van](../store/store-settings.md) pijplijnen.

### Afhankelijkheden van de Zend Framework-componist controleren

Wanneer u een upgrade uitvoert van **2.2.x** naar 2.3.x of hoger, controleert u of de Zend Framework-afhankelijkheden zijn toegevoegd aan de `autoload` eigenschap van het `composer.json` bestand om Laminas te ondersteunen. Deze plugin ondersteunt nieuwe vereisten voor het Zend Framework, dat is gemigreerd naar het Laminas-project. Zie [ Migratie van Kader van Zend aan het Project van Laminas ](https://community.magento.com/t5/Magento-DevBlog/Migration-of-Zend-Framework-to-the-Laminas-Project/ba-p/443251) op _Magento DevBlog_.

**om de `auto-load:psr-4` configuratie** te controleren:

1. Wijzig op uw lokale werkstation de projectmap.

1. Ontdek je integratietak.

1. Open het `composer.json` -bestand in een teksteditor.

1. Controleer de sectie `autoload:psr-4` voor de Zend plugin manager implementatie voor controlemechanismeafhankelijkheid.

   ```json
    "autoload": {
       "psr-4": {
          "Magento\\Framework\\": "lib/internal/Magento/Framework/",
          "Magento\\Setup\\": "setup/src/Magento/Setup/",
          "Magento\\": "app/code/Magento/",
          "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
       },
   }
   ```

1. Als de Zend-afhankelijkheid ontbreekt, werkt u het `composer.json` bestand bij:

   - Voeg de volgende regel toe aan de `autoload:psr-4` sectie.

     ```json
     "Zend\\Mvc\\Controller\\": "setup/src/Zend/Mvc/Controller/"
     ```

   - Werk de projectgebiedsdelen bij.

     ```bash
     composer update
     ```

   - Wijzigingen in code toevoegen, vastleggen en doorvoeren.

     ```bash
     git add -A
     ```

     ```bash
     git commit -m "Add Zend plugin manager implementation for controllers dependency for Laminas support"
     ```

     ```bash
     git push origin <branch-name>
     ```

   - Voeg de wijzigingen in de Staging-omgeving en vervolgens in Production samen.

## Configuratiebestanden

Voordat u de toepassing kunt upgraden, moet u de projectconfiguratiebestanden bijwerken om rekening te houden met wijzigingen in de standaardconfiguratie-instellingen voor Adobe Commerce op de cloudinfrastructuur of de toepassing. De recentste gebreken kunnen in de [ magento-cloud bewaarplaats GitHub ](https://github.com/magento/magento-cloud) worden gevonden.

### .magento.app.yaml

Controleer altijd de waarden in het [ .magento.app.yaml ](../application/configure-app-yaml.md) dossier voor uw geïnstalleerde versie, omdat het de manier controleert uw toepassing bouwt en aan de wolkeninfrastructuur opstelt. Het volgende voorbeeld is voor versie 2.4.8 en gebruikt Composer 2.8.4. Het `build: flavor:` bezit wordt niet gebruikt voor Composer 2.x; zie [ Installerend en gebruikend Composer 2 ](../application/properties.md#installing-and-using-composer-2).

**Het bestand** bijwerken`.magento.app.yaml`:

1. Wijzig op uw lokale werkstation de projectmap.

1. Open en bewerk het `magento.app.yaml` -bestand.

1. Werk de PHP-opties bij.

   ```yaml
   type: php:8.4
   
   build:
       flavor: none
   dependencies:
       php:
           composer/composer: '2.8.4'
   ```

1. Wijzig de opdrachten `hooks` property `build` en `deploy` .

   ```yaml
   hooks:
       # We run build hooks before your application has been packaged.
       build: |
           set -e
           composer install
           php ./vendor/bin/ece-tools run scenario/build/generate.xml
           php ./vendor/bin/ece-tools run scenario/build/transfer.xml
       # We run deploy hook after your application has been deployed and started.
       deploy: |
           php ./vendor/bin/ece-tools run scenario/deploy.xml
       # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
       post_deploy: |
           php ./vendor/bin/ece-tools run scenario/post-deploy.xml
   ```

1. Voeg de volgende omgevingsvariabelen toe aan het einde van het bestand.

   Voor Adobe Commerce 2.2.x tot en met 2.3.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

   Voor Adobe Commerce 2.4.x-

   ```yaml
   variables:
       env:
           CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
           CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
   ```

1. Sla het bestand op. Breng nog geen wijzigingen aan in de externe omgeving.

1. Ga door met het upgradeproces.

### composer.json

Voordat u een upgrade uitvoert, moet u altijd controleren of de afhankelijkheden in het `composer.json` bestand compatibel zijn met de Adobe Commerce-versie.

**om het `composer.json` dossier voor versie 2.4.4 van Adobe Commerce en later bij te werken**:

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

## Projectback-up

We raden u aan een back-up van uw project te maken voordat u een upgrade uitvoert. Gebruik de volgende stappen om een back-up te maken van uw integratie-, faserings- en productieomgevingen.

**Een back-up maken van de database en code** van uw integratieomgeving:

1. Maak een lokale back-up van de externe database.

   ```bash
   magento-cloud db:dump
   ```

   >[!NOTE]
   >
   >Het `magento-cloud db:dump` bevel stelt het [ mysqldump ](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) bevel met de `--single-transaction` vlag in werking, die u aan file uw gegevensbestand zonder de lijsten te sluiten toestaat.

1. Maak een back-up van code en media.

   ```bash
   php bin/magento setup:backup --code [--media]
   ```

   U kunt `[--media]` ook weglaten als u een groot aantal statische bestanden hebt die al in bronbeheer staan.

**aan file uw het Staging of milieu gegevensbestand van de Productie alvorens** op te stellen:

1. Gebruik SSH om u aan te melden bij de externe omgeving.

1. Creeer a [ gegevensbestandstortplaats ](../storage/database-dump.md). Als u een doelmap voor de DB-dump wilt kiezen, gebruikt u de optie `--dump-directory` .

   ```bash
   vendor/bin/ece-tools db-dump
   ```

   Met de dump-bewerking maakt u een `dump-<timestamp>.sql.gz` archiefbestand in uw externe projectmap. Zie [ file gegevensbestand ](../storage/database-dump.md).

## Toepassingsupgrade

Herzie de [ informatie van de de dienstversies ](../services/services-yaml.md#service-versions) voor de recentste vereisten van de softwareversie alvorens uw toepassing te bevorderen.

**De versie van de applicatie upgraden**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Plaats de verbeteringsversie gebruikend de [ syntaxis van de versiebeperking ](overview.md#cloud-metapackage).

   ```bash
   composer require "magento/magento-cloud-metapackage":">=CURRENT_VERSION <NEXT_VERSION" --no-update
   ```

   >[!NOTE]
   >
   >U moet de syntaxis van de versiebeperking gebruiken om het `ece-tools` -pakket bij te werken. U kunt de versiebeperking in het `composer.json` dossier voor de versie van het [ toepassingsmalplaatje ](https://github.com/magento/magento-cloud/blob/master/composer.json) vinden u voor de verbetering gebruikt.

1. Werk het project bij.

   ```bash
   composer update
   ```

1. Bekijk de patches die momenteel worden toegepast:

   - Als er om het even welke die flarden in de `m2-hotfixes` folder worden geïnstalleerd zijn, [ voorlegt een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-case) en het werk met de Steun van Adobe Commerce om te verifiëren welke flarden nog op de nieuwe versie kunnen worden toegepast. Verwijder de niet-toepasselijke patch(es) uit de map `m2-hotfixes` .

   - Als er om het even welke [ Patches van de Kwaliteit ] in het `.magento.env.yaml` dossier worden toegepast, verifieer of zij nog op de nieuwe versie kunnen worden toegepast. Verwijder de niet-toepasselijke patch(es) uit de sectie `QUALITY_PATCHES` van het `.magento.env.yaml` -bestand.

   **Methode 1**: [ verifieer de toepasselijke versies in de de versienota&#39;s van de Patches van de Kwaliteit ](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/quality-patches-tool/release-notes)

   **Methode 2**: [ de beschikbare flarden van de Mening en status ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/upgrade/apply-patches#view-available-patches-and-status)

   **Methode 3**: [ Onderzoek naar flarden ](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=en)


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

1. Controleer de upgrade in uw integratie-, stagage- of productieomgeving door met SSH in te loggen en de versie te controleren.

   ```bash
   php bin/magento --version
   ```

### Een bestand config.php maken

Zoals vermeld in [ beheer van de Configuratie ](#configuration-management), na bevordering, moet u een bijgewerkt `config.php` dossier creëren. Voltooi eventuele aanvullende configuratiewijzigingen via de beheerfunctie in uw integratieomgeving.

**om een systeem-specifiek configuratiedossier** tot stand te brengen:

1. Gebruik vanaf de terminal een SSH-opdracht om het `/app/etc/config.php` -bestand voor de omgeving te genereren.

   ```bash
   ssh <SSH-URL> "<Command>"
   ```

   Als u bijvoorbeeld voor Pro de instructie `scd-dump` wilt uitvoeren op de `integration` -vertakking:

   ```bash
   ssh <project-id-integration>@ssh.us.magentosite.cloud "php vendor/bin/ece-tools config:dump"
   ```

1. Breng het `config.php` -bestand via `rsync` of `scp` over naar uw lokale werkstations. U kunt dit bestand alleen lokaal aan de vertakking toevoegen.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
   ```

   Dit genereert een bijgewerkt `/app/etc/config.php` bestand met een modulelijst en configuratie-instellingen.

>[!WARNING]
>
>Voor een upgrade verwijdert u het bestand `config.php` . Zodra dit dossier aan uw code wordt toegevoegd, zou u **niet** het moeten schrappen. Als u instellingen moet verwijderen of bewerken, bewerkt u het bestand handmatig.

### Extensies upgraden

Bekijk de extensie- en modulepagina&#39;s van derden in Marketplace of andere bedrijfssites en controleer de ondersteuning voor Adobe Commerce en Adobe Commerce op cloudinfrastructuur. Als u extensies en modules van derden moet bijwerken, raadt Adobe aan te werken in een nieuwe integratietak met uw extensies uitgeschakeld.

**om uw uitbreidingen** te verifiëren en te bevorderen:

1. Maak een vertakking op uw lokale werkstation.

1. Schakel de extensies desgewenst uit.

1. Indien beschikbaar, downloadextensies voor upgrades.

1. Installeer de upgrade zoals wordt beschreven in de documentatie van derden.

1. Schakel de extensie in en test deze.

1. Voeg de wijzigingen aan de externe code toe, wijs deze aan en duw erop.

1. Push naar en test in uw integratieomgeving.

1. Ga naar de testomgeving om te testen in een pre-productieomgeving.

Adobe adviseert sterk bevordering uw milieu van de Productie _vóór_ met inbegrip van de promotieuitbreidingen in uw proces van de plaatslancering.

>[!NOTE]
>
>Wanneer u uw toepassingsversie bevordert, werkt het verbeteringsproces aan de recentste versie van de [ Snelle CDN module ](../cdn/fastly.md#fastly-cdn-module-for-magento-2) automatisch bij.

## Upgrade problemen oplossen

Als de upgrade is mislukt, ontvangt u een foutbericht in de browser waarin wordt aangegeven dat u geen toegang hebt tot uw winkel of het deelvenster Beheer:

```
There has been an error processing your request
Exception printing is disabled by default for security reasons.
  Error log record number: <error-number>
```

**om de fout** op te lossen:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om in te loggen op de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Open het `./app/var/report/<error number>` bestand.

1. [Onderzoek de logboeken](../test/log-locations.md) en bepaal de oorzaak van het probleem.

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A && git commit -m "Fixed deployment failure" && git push origin <branch-name>
   ```
