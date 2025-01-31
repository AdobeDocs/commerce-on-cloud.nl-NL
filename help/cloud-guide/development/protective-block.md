---
title: Beschermend blok
description: Leer meer over de beschermende blokfunctie van Adobe Commerce op cloudinfrastructuur en hoe deze werkt om uw site te beschermen tegen bekende beveiligingsproblemen.
feature: Cloud, Configuration, Security
topic: Security
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Beschermend blok

Adobe Commerce on cloud Infrastructure heeft een beschermende blokkeringsfunctie die onder bepaalde omstandigheden de toegang beperkt tot websites met beveiligingsproblemen. Deze gedeeltelijke het blokkeren methode verhindert exploitatie van bekende veiligheidskwetsbaarheid. Verouderde software bevat vaak explosies, dus het is belangrijk om tegen deze explosies te beschermen door de toegang tot deze sites gedeeltelijk te blokkeren.

## Hoe het beschermende blok werkt

Adobe Commerce onderhoudt een database met handtekeningen van bekende beveiligingsproblemen in opensource-software die doorgaans wordt geïmplementeerd op cloudinfrastructuur. De veiligheidscontrole analyseert slechts bekende kwetsbaarheid in open-bronprojecten; het kan geen aanpassingen onderzoeken u schrijft.

Beveiligingsscan:

- Wanneer u nieuwe code op Git drukt
- Wanneer nieuwe kwetsbaarheden aan het gegevensbestand worden toegevoegd

Als in uw toepassing een kritieke kwetsbaarheid wordt gedetecteerd, wordt de Git-push afgewezen.

Er zijn twee typen blokken die worden uitgevoerd:

1. **Volledig blok** - voor ontwikkelingswebsites. Het foutbericht dat `git push` begeleidt, bevat gedetailleerde informatie over de kwetsbaarheid.

1. **Gedeeltelijk blok** - voor productiewebsites, die de plaats toestaat om hoofdzakelijk online te blijven. Afhankelijk van de aard van de kwetsbaarheid, kunnen delen van een verzoek, zoals een vraagkoord, koekjes, of om het even welke extra kopballen, uit GET verzoeken worden verwijderd. Alle andere verzoeken kunnen volledig worden geblokkeerd, zoals het aanmelden, het verzenden van formulieren of het afrekenen van producten.

Het deblokkeren wordt geautomatiseerd bij het oplossen van het veiligheidsrisico. Het blok wordt verwijderd kort nadat u een beveiligingsupgrade hebt uitgevoerd waarmee de kwetsbaarheid wordt verwijderd.

## Weigeren van het beschermende blok

Het beschermende blok is er om u te beschermen tegen bekende kwetsbaarheden in de software die u Adobe Commerce op cloudinfrastructuur implementeert.

U kunt de optie Weigeren echter toevoegen aan [`.magento.app.yaml`](../application/configure-app-yaml.md) door het volgende toe te voegen:

```yaml
   preflight:
      enabled: false
```

U kunt een specifieke controle expliciet uitschakelen, bijvoorbeeld:

```yaml
   preflight:
      enabled: true
      ignore_rules: [ "drupal:SA-CORE-2014-005" ]
```
