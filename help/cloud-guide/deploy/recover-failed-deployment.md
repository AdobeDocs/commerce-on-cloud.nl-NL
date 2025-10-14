---
title: Herstellen van componentfout
description: Leer hoe u kunt herstellen als een component niet correct wordt geïmplementeerd in Adobe Commerce op de cloudinfrastructuur.
feature: Cloud, Deploy
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Herstellen van componentfout

Dit onderwerp bespreekt hoe te terug te krijgen als een component er niet in slaagt behoorlijk op te stellen. De typische voorbeelden omvatten componenten die gebiedsdelen hebben die niet door uw verre milieu, zoals incompatibele PHP versies worden voldaan.

U kunt op de volgende manieren herstellen van een mislukte implementatie:

- [Een back-up herstellen](../storage/snapshots.md#restore-a-snapshot)
- Project en code van vorige wijzigingen opschonen en opnieuw implementeren

## Reinigen, verwijderen en opnieuw implementeren

Om van de vorige plaatsing schoon te maken, identificeer de component die werd toegevoegd of bijgewerkt en verwijder dan het. Meld u eerst aan bij de externe omgeving en wis de inhoud van de map `var` handmatig. Verwijder vervolgens de component uit het `composer.json` -bestand en implementeer de omgeving opnieuw.

**om de `var` folders** schoon te maken:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Wis de mappen `var` .

   ```shell
   rm -rf var/*
   ```

1. Afmelden.

**om de component** te verwijderen:

1. Wijzig op uw lokale werkstation de projectmap.

1. Wis de cache.

   ```bash
   composer clear-cache
   ```

1. Verwijder de component uit het `composer.json` -bestand.

   ```bash
   composer remove <component-name>:<version>
   ```

   Als het volgende bericht wordt weergegeven, hoeft u niets meer te doen:

   ```
   Package "<name>:<version>" listed for update is not installed. Ignoring.
   ```

1. Wacht terwijl de gebiedsdelen worden bijgewerkt.

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "<message>"
   ```

   ```bash
   git push origin <environment-ID>
   ```

{{redeploy-warning}}

Zie meer over het herstellen van een milieu zonder een steun in [&#x200B; herstellen een milieu &#x200B;](../development/restore-environment.md).

{{stuck-deployment-tip}}
