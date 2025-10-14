---
title: Extensies beheren
description: Leer extensies installeren en beheren in Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Extensions, Upgrade
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Extensies beheren

U kunt uw de toepassingsmogelijkheden van Adobe Commerce uitbreiden door een uitbreiding van de [&#x200B; Commerce Marketplace &#x200B;](https://marketplace.magento.com) toe te voegen. U kunt bijvoorbeeld een thema toevoegen om de vormgeving van uw winkel te wijzigen of u kunt een taalpakket toevoegen om uw winkel en Admin te lokaliseren.

>[!NOTE]
>
>Om installatiekwesties te voorkomen, moeten alle aankopen van Marketplace worden voltooid met dezelfde account (MAGEID) als die eigenaar is van het cloudproject.

## Composernaam van een extensie

Hoewel deze sectie bespreekt hoe te om de naam Composer en de versie van een uitbreiding van Commerce Marketplace te krijgen, kunt u de naam en de versie van _om het even welke_ module in het dossier Composer van de module vinden. Open het bestand `composer.json` in een teksteditor en noteer de waarden `"name"` en `"version"` .

**om de naam Composer van een module van de Commerce Marketplace** te krijgen:

1. Login aan [&#x200B; Commerce Marketplace &#x200B;](https://marketplace.magento.com) met de gebruikersbenaming en het wachtwoord u gebruikte om de component te kopen.

1. In de hogere juiste hoek, klik uw gebruikersbenaming en selecteer **Mijn Profiel**.

   ![&#x200B; heb toegang tot uw rekening van de Marketplace &#x200B;](../../assets/marketplace/my-profile.png)

1. Op de _Mijn pagina van de Rekening_, klik **Mijn Aankopen**.

   ![&#x200B; de aankoopgeschiedenis van de Marketplace &#x200B;](../../assets/marketplace/my-purchases.png)

1. Voor _Mijn Aankopen_ pagina, selecteer een module die u kocht en **Technische Details** klikt.

1. Klik **Exemplaar** om [!UICONTROL Component name] aan het klembord te kopiëren.

1. Open een tekstverwerker en plak de componentnaam en voeg een dubbele punt (`:`) toe.

1. In **Technische Details**, klik **Exemplaar** om [!UICONTROL Component version] aan het klembord te kopiëren.

1. Voeg in de teksteditor het versienummer toe aan de componentnaam na de dubbele punt. Bijvoorbeeld:

   ```text
   extension-name/magento2:1.0.1
   ```

## Een extensie installeren

Adobe raadt u aan in een ontwikkelingsvertakking te werken wanneer u een extensie toevoegt aan uw implementatie. Wanneer het installeren van een uitbreiding, wordt de uitbreidingsnaam (`<VendorName>_<ComponentName>`) automatisch opgenomen in het [`app/etc/config.php` &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/deployment-files.html?lang=nl-NL) dossier. U hoeft het bestand niet rechtstreeks te bewerken.

**om een uitbreiding** te installeren:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak of check een ontwikkelingsvertakking uit. Zie [&#x200B; vertakkend &#x200B;](../development/cli-branches.md).

1. Voeg de extensie met de naam en versie van de Composer toe aan de sectie `require` van het `composer.json` -bestand.

   ```bash
   composer require <extension-name>:<version> --no-update
   ```

1. Werk de projectgebiedsdelen bij.

   ```bash
   composer update
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Install <extension-name>"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!WARNING]
   >
   >Wanneer u een extensie installeert, moet u het `composer.lock` -bestand opnemen wanneer u codewijzigingen doorvoert in de externe omgeving. De opdracht `composer install` leest het `composer.lock` -bestand om de gedefinieerde afhankelijkheden in de externe omgeving in te schakelen.

1. Nadat de build en implementatie is voltooid, gebruikt u een SSH om u aan te melden bij de externe omgeving en om de geïnstalleerde extensie te controleren.

   ```bash
   bin/magento module:status <extension-name>
   ```

   Een extensienaam gebruikt de indeling: `<VendorName>_<ComponentName>` .

   Monsterrespons:

   ```
   Module is enabled
   ```

   Als u plaatsingsfouten ontmoet, zie [&#x200B; mislukking van de uitbreidingsplaatsing &#x200B;](../deploy/recover-failed-deployment.md).

## Extensies beheren

Wanneer u een uitbreiding gebruikend Composer toevoegt, laat het plaatsingsproces automatisch de uitbreiding toe. Als u reeds de uitbreiding hebt geïnstalleerd, kunt u de uitbreiding toelaten of onbruikbaar maken gebruikend CLI. Gebruik de volgende indeling wanneer u extensies beheert: `<VendorName>_<ComponentName>`

Schakel een extensie nooit in of uit wanneer u bent aangemeld bij de externe omgevingen.

**om een uitbreiding** toe te laten of onbruikbaar te maken:

1. Wijzig op uw lokale werkstation de projectmap.

1. Een module in- of uitschakelen. Met de opdracht `module` werkt u het `config.php` -bestand bij met de gevraagde status van de module.

   >Een module inschakelen.

   ```bash
   bin/magento module:enable <module-name>
   ```

   >Een module uitschakelen.

   ```bash
   bin/magento module:disable <module-name>
   ```

1. Als u een module hebt ingeschakeld, gebruikt u `ece-tools` om de configuratie te vernieuwen.

   ```bash
   ./vendor/bin/ece-tools module:refresh
   ```

1. Controleer de status van een module.

   ```bash
   bin/magento module:status <module-name>
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Disable <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

## Een extensie upgraden

Voordat u verdergaat, hebt u de naam en de versie van de Composer nodig voor de extensie. Controleer ook of de extensie compatibel is met uw project en de Adobe Commerce-versie. Met name, [&#x200B; controleer de vereiste PHP versie &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html?lang=nl-NL) alvorens u begint.

**om een uitbreiding** bij te werken:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak of check een ontwikkelingsvertakking uit. Zie [&#x200B; vertakkend &#x200B;](../development/cli-branches.md).

1. Open het `composer.json` -bestand in een teksteditor.

1. Zoek de extensie en werk de versie bij.

1. Sla de wijzigingen op en sluit de teksteditor af.

1. Werk de projectgebiedsdelen bij.

   ```bash
   composer update
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update <extension-name>"
   ```

   ```bash
   git push origin <branch-names>
   ```

Als u fouten ontmoet, zie [&#x200B; Herstel van componentenmislukking &#x200B;](../deploy/recover-failed-deployment.md). Meer over het gebruiken van uitbreidingen met Adobe Commerce leren, zie [&#x200B; Uitbreidingen &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/extensions.html?lang=nl-NL) in de _Gids Admin_.
