---
title: Foutberichten voor het pakket ECE-Tools
description: Zie een lijst met foutcodes en berichten die tijdens de Adobe Commerce kunnen optreden bij het ontwikkelen, implementeren en implementeren van processen in de cloud-infrastructuur.
recommendations: noDisplay
role: Developer
exl-id: e240c268-b171-44e9-9fa4-f0e91b0d9899
source-git-commit: 350cfea06f036f0787b330e6e40c5af46a30f5ad
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Foutberichten voor ECE-Tools

Deze naslaggids voor foutberichten bevat informatie voor het oplossen van fouten die kunnen optreden tijdens de Adobe Commerce voor het ontwikkelen, implementeren en implementeren van processen in de cloud-infrastructuur.

Alle kritieke foutmeldingen en waarschuwingsfoutmeldingen die tijdens de implementatie optreden, worden zowel naar de `var/log/cloud.log` - als `/var/log/cloud.error.log` -bestanden geschreven. Het logbestand van de cloud-fout bevat alleen fouten van de laatste implementatie. Een leeg bestand geeft aan dat de implementatie zonder fouten is gelukt.

In het `cloud.error.log` -bestand wordt elk item opgemaakt als een JSON-tekenreeks, zodat het gemakkelijker kan worden geparseerd:

```json
{"errorCode":1006,"stage":"build","step":"validate-config","suggestion":"No stores/website/locales found in config.php\n  To speed up the deploy process do the following:\n  1. Using SSH, log in to your Magento Cloud account\n  2. Run \"php ./vendor/bin/ece-tools config:dump\"\n  3. Using SCP, copy the app/etc/config.php file to your local repository\n  4. Add, commit, and push your changes to the app/etc/config.php file","title":"The configured state is not ideal","type":"warning"}
```

Foutberichten worden gecategoriseerd door een van de implementatiefasen: maken, implementeren en na implementatie. Elke sectie bevat een lijst met bijbehorende fouten met de volgende informatie voor elke fout:

- **code van de Fout**: Adobe Commerce-Toegewezen herkenningsteken voor het foutenbericht
- **Stadium**: Wijst erop of de fout tijdens de bouwstijl voorkwam, opstelt, of post-opstelt stadium
- **Stap**: Wijst op de stap in het plaatsingsscenario dat de fout kan terugkeren. Als de _kolom van de Stap_ leeg is, is de fout een algemene fout die door veelvoudige stappen, of tijdens preprocessing verrichtingen kan zijn teruggekeerd. Zie [ op scenario-Gebaseerde plaatsing ](../deploy/scenario-based.md) voor meer informatie over de bouw, opstellen, en post-opstelt stappen.
- **Suggestie**: Verstrekt begeleiding om de fout problemen op te lossen en op te lossen
- **Titel (de beschrijving van de Fout)**: Een beschrijving die de oorzaak van de fout samenvat
- **Type**: Wijst erop of de fout een kritieke fout of een waarschuwing is

{{$include /help/_includes/automated/ece-tools-error-codes.md}}
