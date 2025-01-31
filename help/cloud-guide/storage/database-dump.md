---
title: Back-up maken van de database
description: Leer hoe u met ECE-tools een back-up kunt maken van de database voor een Adobe Commerce on cloud-infrastructuurproject.
feature: Cloud, Iaas, Storage
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Back-up maken van de database

U kunt een kopie van uw database maken met de opdracht `ece-tools db-dump` zonder alle omgevingsgegevens van services en montage vast te leggen. Met deze opdracht maakt u standaard back-ups in de map `/app/var/dump-main` voor alle databaseverbindingen die in de omgevingsconfiguratie zijn opgegeven. De de stortplaatsverrichting van DB schakelt de toepassing aan onderhoudswijze, houdt de processen van de consumentenrij tegen, en maakt cron banen onbruikbaar alvorens de stortplaats begint.

Overweeg de volgende richtlijnen voor stortplaats van DB:

- Voor Productomgevingen, adviseert de Adobe de verrichtingen van de gegevensbestandstortplaats tijdens off-peak uren te voltooien om de dienstverstoringen te minimaliseren die voorkomen wanneer de plaats op onderhoudswijze is.
- Als een fout tijdens de stortplaatsverrichting voorkomt, schrapt het bevel het stortplaatsdossier om schijfruimte te besparen. Bekijk de logboeken voor details (`var/log/cloud.log`).
- Voor Pro de milieu&#39;s van de Productie, dumpt dit bevel slechts van _één_ van de drie high-availability knopen, zodat zouden de productiegegevens die aan een verschillende knoop tijdens de stortplaats worden geschreven niet kunnen worden gekopieerd. De opdracht genereert een `var/dbdump.lock` -bestand om te voorkomen dat de opdracht op meer dan één knooppunt wordt uitgevoerd.
- Voor een steun van alle milieudiensten, adviseert de Adobe creërend a [ steun ](snapshots.md).

U kunt verkiezen aan file veelvoudige gegevensbestanden door de gegevensbestandnamen aan het bevel toe te voegen. In het volgende voorbeeld wordt een back-up gemaakt van twee databases: `main` en `sales` :

```bash
php vendor/bin/ece-tools db-dump main sales
```

Gebruik de opdracht `php vendor/bin/ece-tools db-dump --help` voor meer opties:

- `--dump-directory=<dir>` - Kies een doelmap voor de databasedumpit
- `--remove-definers`—Verwijder DEFINITIEVE instructies uit de databasedumpdump

**om een gegevensbestandstortplaats in het het Opvoeren of milieu van de Productie te creëren**:

1. [ SSH van het Gebruik aan login of creeer een tunnel om met het verre milieu ](../development/secure-connections.md) te verbinden die het gegevensbestand aan exemplaar bevat.

1. Maak een lijst van de omgevingsverhoudingen en neem nota van de gegevens van de gegevensbestandlogin.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Maak een back-up van de database. Als u een doelmap voor de DB-dump wilt kiezen, gebruikt u de optie `--dump-directory` .

   ```bash
   php vendor/bin/ece-tools db-dump -- main
   ```

   Monsterrespons:

   ```
   The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
   Your site will not receive any traffic until the operation completes.
   Do you wish to proceed with this process? (y/N)? y
   2020-01-28 16:38:08] INFO: Starting backup.
   [2020-01-28 16:38:08] NOTICE: Enabling Maintenance mode
   [2020-01-28 16:38:10] INFO: Trying to kill running cron jobs and consumers processes
   [2020-01-28 16:38:10] INFO: Running Magento cron and consumers processes were not found.
   [2020-01-28 16:38:10] INFO: Waiting for lock on db dump.
   [2020-01-28 16:38:10] INFO: Start creation DB dump for main database...
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /tmp/qxmtlseakof6y/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

1. Met de opdracht `db-dump` maakt u een `dump-<timestamp>.sql.gz` -archiefbestand in de externe projectmap.

>[!TIP]
>
>Als u deze gegevens aan een specifiek milieu wilt duwen, zie [ gegevens en statische dossiers migreren ](../deploy/staging-production.md#migrate-static-files).
