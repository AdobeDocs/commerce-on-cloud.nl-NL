---
title: Het pakket ECE-gereedschappen bijwerken
description: Leer hoe u het pakket ECE-Tools kunt upgraden om te profiteren van de nieuwste oplossingen en functies die op Adobe Commerce op cloudinfrastructuur zijn toegepast.
feature: Cloud, Upgrade
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Het pakket ECE-gereedschappen bijwerken

Een update aan het `ece-tools` pakket werkt ook de andere [&#x200B; Reeks van Hulpmiddelen van de Wolk voor de pakketten van Commerce &#x200B;](../release-notes/cloud-tools-suite.md) bij, die gebiedsdelen voor `ece-tools` zijn. Daarom moet u een versie van Adobe Commerce gebruiken op cloudinfrastructuur die het `ece-tools` -pakket ondersteunt.

{{ece-tools-package}}

**Eerste vereisten**:

- Alvorens u `ece-tools` bijwerkt, herzie de [&#x200B; Reeks van Hulpmiddelen van de Wolk voor de versienota&#39;s van Commerce &#x200B;](../release-notes/cloud-tools-suite.md).
- Als u van `ece-tools` 2002.0.22 of vroeger aan 2002.1.0 bijwerkt, herzie [&#x200B; Achteruit onverenigbare veranderingen &#x200B;](../release-notes/backward-incompatible-changes.md) en breng om het even welke vereiste veranderingen in uw Adobe Commerce op het project van de wolkeninfrastructuur aan.
- Het overzicht [&#x200B; Verbeteringen en Patches &#x200B;](../development/commerce-version.md#upgrade-from-older-versions) om de ECE-Hulpmiddelen versies compatibel met uw Adobe Commerce op het project van de wolkeninfrastructuur te bepalen.

{{upgrade-tip}}

**om het `ece-tools` pakket** bij te werken:

1. Voer op uw lokale werkstation een update uit met Composer.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >Als u niet voorbij `ece-tools` versie 2002.0.8 kunt bijwerken, zie [&#x200B; het project van de Verbetering om ECE-Hulpmiddelen pakket &#x200B;](install-package.md) te gebruiken.

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update magento/ece-tools"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Voeg deze vertakking na testvalidatie samen met de integratievertakking.
