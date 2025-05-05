---
title: Cache instellen voor statische bestanden
description: Leer om de opties van de geheim voorgeheugenopslag in het  [!DNL Commerce]  dossier van de toepassingsconfiguratie te plaatsen.
feature: Cloud, Configuration, Cache, SCD
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Cache instellen voor statische bestanden

De cache-TTL (time-to-live) voor uw media en statische bestanden wordt in het configuratiebestand van `.magento.app.yaml` ingesteld met behulp van de `expires` -toets.

>[!NOTE]
>
>Voordat u de productieomgeving bijwerkt, is het belangrijk dat u de wijzigingen in de testomgeving test. [ leg een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voor hulp met het bijwerken van de configuratie op deze milieu&#39;s voor.

1. Geef de TTL-tijd (in seconden) op in de eigenschap [`web` ](web-property.md) van het `.magento.app.yaml` -bestand. U kunt de `expires` -toets toevoegen onder `locations` of onder `"/media"` en `"/static"` .

   Als u wilt voorkomen dat de cache vervalt, gebruikt u het sleutelwaardepaar `expires: -1` . Zie het volgende voorbeeld:

   ```yaml
   # The configuration of app when it is exposed to the web.
   web:
     locations:
       "/media":
         ...
         expires: -1
   
       "/static":
         ...
         expires: -1
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add -A && git commit -m "Set cache TTL for static files" && git push origin <branch-name>
   ```
