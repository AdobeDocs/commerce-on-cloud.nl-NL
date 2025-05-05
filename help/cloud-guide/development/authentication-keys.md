---
title: Verificatietoetsen
description: Leer hoe u verificatietoetsen toepast op een ontwikkelingsproject in Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Security
topic: Security
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Verificatietoetsen

U moet een verificatietoets hebben om toegang te krijgen tot de Adobe Commerce-opslagplaats en om installatie- en updateopdrachten voor uw Adobe Commerce in te schakelen voor het infrastructuurproject in de cloud. Er zijn twee methoden om de autorisatiegegevens van de Composer op te geven.

- **authentificatiedossier** - een dossier dat uw 2&rbrace; autorisatiereferenties van Adobe Commerce [&#128279;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) in uw Adobe Commerce op de folder van de de wortelfolder van de wolkeninfrastructuur bevat.
- **milieu veranderlijk** - een milieu variabele aan opstellingsauthentificatietoetsen in uw Adobe Commerce op het project van de wolkeninfrastructuur om toevallige blootstelling te verhinderen.

>[!BEGINSHADEBOX]

**nota van de Veiligheid**

De Adobe adviseert gebruikend de [ milieu veranderlijke ](#composer-auth-environment-variable) methode met uw wolkenproject om toevallige blootstelling van uw vergunningsgeloofsbrieven te verhinderen.

De methode voor het verificatiebestand is ideaal als u Cloud Docker voor Commerce gebruikt als lokaal ontwikkelingsprogramma, maar zorg ervoor dat u het `auth.json` -bestand niet uploadt naar een openbare Git-opslagplaats. U kunt het `auth.json` dossier aan het [`.gitignore` dossier ](../project/file-structure.md#ignoring-files) toevoegen.

>[!ENDSHADEBOX]

## Verificatiebestand

**om een `auth.json` dossier** tot stand te brengen:

1. Als u geen `auth.json` dossier in uw folder van de projectwortel hebt, creeer één.

   - Maak met een teksteditor een `auth.json` -bestand in de hoofdmap van het project.
   - Kopieer de inhoud van de [ steekproef `auth.json` ](https://github.com/magento/magento2/blob/2.3/auth.json.sample) in het nieuwe `auth.json` dossier.

1. Vervang `<public-key>` en `<private-key>` door uw Adobe Commerce-verificatiereferenties.

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Sla de wijzigingen op en sluit de teksteditor af.

## Omgevingsvariabele van composer

De volgende methode is de beste manier om onbedoelde blootstelling van gevoelige gegevens in een openbare Git-opslagplaats te voorkomen.

**om authentificatietoetsen toe te voegen gebruikend een omgevingsvariabele**:

1. Klik in _[!DNL Cloud Console]_&#x200B;op het configuratiepictogram rechts van de projectnavigatie.

   ![ vorm project ](../../assets/icon-configure.png){width="36"}

1. In de _lijst van de Montages van het Project_, klik **[!UICONTROL Variables]**.

1. Klik op **[!UICONTROL Create variable]**.

1. Typ `env:COMPOSER_AUTH` in het veld **[!UICONTROL Variable name]** .

1. Op het _gebied van de Waarde_, voeg het volgende toe en vervang `<public-key>` en `<private-key>` met uw de authentificatiegeloofsbrieven van Adobe Commerce:

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Selecteer **[!UICONTROL Available during buildtime]** en hef de selectie van **[!UICONTROL Available during runtime]** op.

1. Klik op **[!UICONTROL Create variable]**.

1. Verwijder het `auth.json` -bestand uit elke omgeving.
