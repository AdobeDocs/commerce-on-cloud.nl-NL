---
title: Omgeving herstellen
description: Leer hoe u de Adobe Commerce-toepassing kunt verwijderen uit een cloudinfrastructuurproject en een omgeving kunt herstellen in een stabiele toestand.
role: Developer
topic: Development
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Omgeving herstellen

Als u kwesties in het integratiemilieu ontmoet en geen a [ geldige steun ](../storage/snapshots.md) hebt, of het milieu aan een lege plaats zou willen terugstellen, kunt u uw milieu herstellen/terugstellen gebruikend één van de volgende methodes:

- De code in de Git-vertakking herstellen of herstellen
- De toepassing [!DNL Commerce] verwijderen
- Herplaatsing forceren
- De database handmatig opnieuw instellen

{{stuck-deployment-tip}}

## De Git-vertakking opnieuw instellen

Als u de Git-vertakking opnieuw instelt, wordt de code in het verleden teruggezet naar een stabiele status.

**om uw tak** terug te stellen:

1. Wijzig op uw lokale werkstation de projectmap.

1. Bekijk de Git commit geschiedenis. Gebruik `--oneline` om afgekorte komma&#39;s op één regel weer te geven:

   ```bash
   git log --oneline
   ```

   Monsterrespons:

   ```
   6bf9f45 (HEAD -> master, magento/master, magento/develop, magento/HEAD, develop) Create composer.lock
   34d7434 2.4.6 upgrade
   b69803c Update composer.lock
   c1bca24 Add sample data
   ec604c3 Update magento/ece-tools
   ...
   ```

1. Kies een commit hash die de laatst bekende stabiele staat van uw code vertegenwoordigt.

   Als u de oorspronkelijke geïnitialiseerde status van de vertakking wilt herstellen, zoekt u eerst naar de instelling waarmee de vertakking is gemaakt. Met `--reverse` kunt u de historie in omgekeerde chronologische volgorde weergeven.

1. Met de optie voor het opnieuw instellen van de vaste waarden kunt u de vertakking herstellen. Wees voorzichtig met het gebruik van deze opdracht omdat alle wijzigingen worden verwijderd sinds de gekozen toewijzen.

   ```bash
   git reset --hard <commit>
   ```

1. Duw uw veranderingen om een herplaatsing teweeg te brengen, die Adobe Commerce opnieuw installeert.

   ```bash
   git push --force <origin> <branch>
   ```

## Commerce verwijderen

Als u de [!DNL Commerce] -toepassing verwijdert, wordt de oorspronkelijke toestand van de omgeving hersteld door de database te herstellen, de implementatieconfiguratie te verwijderen en de submappen van `var/` te wissen. Deze richtlijn stelt ook uw git tak aan een vroegere stabiele staat terug. Als u geen recente back-up hebt, maar de externe omgeving wel kunt openen met behulp van SSH, voert u de volgende stappen uit om uw omgeving te herstellen:

- Configuratiebeheer uitschakelen
- Adobe Commerce verwijderen
- De grijsvertakking herstellen

Als u de Adobe Commerce-software verwijdert, wordt de database neergezet en hersteld, wordt de implementatieconfiguratie verwijderd en worden de submappen van `var/` gewist. Het is belangrijk om [ beheer van de Configuratie ](../store/store-settings.md) onbruikbaar te maken zodat het niet automatisch de vorige configuratiemontages tijdens de volgende plaatsing toepast. Controleer of de map `app/etc/` het bestand `config.php` niet bevat.

**om de software van Adobe Commerce** te desinstalleren:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Verwijder het configuratiebestand.
   - Voor Adobe Commerce 2.2 en hoger:

     ```bash
     rm app/etc/config.php
     ```

   - Voor Adobe Commerce 2.1:

     ```bash
     rm app/etc/config.local.php
     ```

1. Verwijder de Adobe Commerce-toepassing.

   ```bash
   php bin/magento setup:uninstall -n
   ```

1. Bevestig dat Adobe Commerce is verwijderd.

   Het volgende bericht wordt weergegeven om te bevestigen dat het verwijderen is gelukt:

   ```
   [SUCCESS]: Magento uninstallation complete.
   ```

1. Wis de submappen `var/` .

   ```bash
   rm -rf var/*
   ```

1. Afmelden.

>[!TIP]
>
>Optioneel is het een goede gewoonte om bouwcaches schoon te maken.
>
>```bash
>magento-cloud project:clear-build-cache
>```

## Herplaatsing forceren

Als u hebt geprobeerd om Adobe Commerce te verwijderen en uw implementatie blijft mislukken, kunt u proberen om handmatig een herimplementatie te forceren.

```bash
git commit --allow-empty -m "<message>" && git push <origin> <branch>
```

## De database opnieuw instellen

Als u hebt geprobeerd om Adobe Commerce te verwijderen en de opdracht is mislukt of niet kan worden voltooid, kunt u de database handmatig opnieuw instellen.

**om het gegevensbestand** terug te stellen:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Maak verbinding met de database.

   ```bash
   mysql -h database.internal
   ```

1. Zet de `main` -database neer.

   ```shell
   drop database main;
   ```

1. Maak een lege `main` -database.

   ```shell
   create database main;
   ```

1. Verwijder de volgende configuratiebestanden.

   - `config.php`
   - `config.php.bak`
   - `env.php`
   - `env.php.bak`

1. Log uit en activeer een herplaatsing.

   ```bash
   magento-cloud environment:redeploy
   ```

{{redeploy-warning}}
