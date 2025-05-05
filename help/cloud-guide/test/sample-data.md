---
title: Voorbeeldgegevens
description: Leer hoe u voorbeeldgegevens met Adobe Commerce installeert op cloudinfrastructuur.
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# Voorbeeldgegevens

Als u voorbeeldgegevens nodig hebt bij het ontwikkelen van uw winkel, kunt u voorbeeldgegevens installeren. Deze gegevens simuleren een actieve Adobe Commerce-winkel met klanten, producten en andere gegevens. Deze voorbeeldgegevens werken het best met een nieuwe Adobe Commerce op de sjablooninstallatie van de cloudinfrastructuur.

U kunt het beste voorbeeldgegevens installeren in ontwikkelings- en integratieomgevingen. Als u steekproefgegevens in het Opvoeren of de Productie gebruikt, dan moet u [&#128279;](#reset-or-uninstall-sample-data) de informatie en de producten verwijderen alvorens levend te gaan.

## Voorbeeldgegevens installeren

Voorbeeldgegevens installeren:

1. Wijzig op uw lokale werkstation de projectmap.

1. Voer in de hoofdmap de volgende opdracht in om voorbeeldgegevens toe te voegen:

   ```bash
   ./bin/magento sampledata:deploy
   ```

1. Wacht tot componenten zijn bijgewerkt.

1. Leg de wijzigingen vast en duw deze:

   ```bash
   git add -A && git commit -m "Install sample data"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Wacht op het project om op te stellen.

1. Controleer of de installatie is gelukt door naar de winkelpagina in de integratieomgeving te gaan. U kunt de URL-koppeling naar de winkel vinden via [!DNL Cloud Console] .

1. Maak een momentopname van uw omgeving:

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

U kunt uw ontwikkeling testen met live-gegevens!

## Voorbeeldgegevens opnieuw instellen of verwijderen

U kunt de voorbeeldgegevens opnieuw instellen of verwijderen volgens dezelfde procedure als voor de installatie van de voorbeeldgegevens:

- Voorbeeldgegevens verwijderen: `./bin/magento sampledata:remove`
- Voorbeeldgegevens opnieuw instellen: `./bin/magento sampledata:reset`
