---
title: Slimme wizards
description: Leer hoe u slimme wizards gebruikt om te beoordelen of uw Adobe Commerce on cloud Infrastructure-project de best practices voor implementatie volgt.
feature: Cloud, Build, Deploy, SCD
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Slimme wizards

De slimme wizards kunnen u helpen bepalen of uw configuratie van de Wolk beste praktijken volgt. De beschikbare tovenaars helpen bij de volgende configuraties:

- Ideale status voor minimale uitvaltijd van implementatie
- Configuratie voor taakverdeling voor database en Redis
- De statische Plaatsing van de Inhoud (SCD) voor op bestelling, bouwt stadium, of stelt stadium op

Elk van de slimme tovenaarsbevelen verstrekt een controlerespons en, indien van toepassing, een aanbeveling voor de juiste configuratie.

| Opdracht | Beschrijving |
| ------- | ------------|
| `wizard:ideal-state` | Controleer dat SCD op het _bouwt_ stadium is, is de `SKIP_HTML_MINIFICATION` variabele `true`, en de post_implementatiehaak die in het milieu van de Wolk wordt gevormd. Niet voor gebruik in de lokale ontwikkelomgeving. |
| `wizard:master-slave` | Controleer of de variabele `REDIS_USE_SLAVE_CONNECTION` en de variabele `MYSQL_USE_SLAVE_CONNECTION` `true` zijn. |
| `wizard:scd-on-demand` | Controleer of de globale omgevingsvariabele `SCD_ON_DEMAND` `true` is. |
| `wizard:scd-on-build` | Controleer dat de `SCD_ON_DEMAND` globale milieuvariabele `false` is en de `SKIP_SCD` omgevingsvariabele `false` voor het _bouwt_ stadium is. Hiermee wordt gecontroleerd of het `config.php` -bestand informatie bevat voor winkels, opslaggroepen en websites. |
| `wizard:scd-on-deploy` | Controleer dat de `SCD_ON_DEMAND` globale milieuvariabele `false` is en de `SKIP_SCD` omgevingsvariabele `false` voor __ stadium opstelt. Verifieert dat het `config.php` dossier _NIET_ de lijst van opslag, opslaggroepen, en websites met verwante informatie bevat. |

Als voorbeeld, kunt u verifiëren dat uw configuratie behoorlijk SCD op bestelling eigenschap toelaat:

```bash
./vendor/bin/ece-tools wizard:scd-on-demand
```

Een geslaagde configuratie retourneert:

```
SCD on-demand is enabled
```

Een mislukte configuratie retourneert:

```
SCD on-demand is disabled
```

## Een ideale configuratie controleren

De _ideale_ configuratie voor uw project van de Wolk helpt om plaatsing onderbreking te minimaliseren door het geheime voorgeheugen te verwarmen en statische inhoud te produceren wanneer gevraagd door de gebruiker. Deze tovenaar loopt automatisch tijdens het plaatsingsproces. Als uw Wolk niet voor deze _ideale staat_ wordt gevormd, dan ontvangt u een bericht gelijkend op het volgende:

```
- SCD on build is not configured
- Post-deploy hook is not configured
- Skip HTML minification is disabled

Ideal state is not configured
```

Gebaseerd op de output, moet u de volgende correcties in uw configuratie aanbrengen:

1. Schakel de minificatievariabele HTML overslaan in.

   > .magento.env.yaml

   ```yaml
   stage:
     global:
       SKIP_HTML_MINIFICATION: true
   ```

1. Vorm de post-opstellen haak.

   > .magento.app.yaml

   ```yaml
       post_deploy: |
           php ./vendor/bin/ece-tools post-deploy
   ```

1. Duw uw code verandert en stel de test opnieuw in werking. Wanneer uw configuratie __ ideaal is, ontvangt u het volgende bericht.

   ```
   Ideal state is configured
   ```
