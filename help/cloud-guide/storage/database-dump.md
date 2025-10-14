---
title: Back-up maken van de database
description: Leer hoe u met ECE-tools een back-up kunt maken van de database voor een Adobe Commerce on cloud-infrastructuurproject.
feature: Cloud, Iaas, Storage
exl-id: 351f7691-3153-4b8a-83af-8b8895b93d98
source-git-commit: 3a3b0cd6e28f3e6ed3521a86f7c7c8868be0cf83
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Back-up maken van de database

U kunt een kopie van uw database maken met de opdracht `ece-tools db-dump` zonder alle omgevingsgegevens van services en montage vast te leggen. Met deze opdracht maakt u standaard back-ups in de map `app/var/` voor alle databaseverbindingen die in de omgevingsconfiguratie zijn opgegeven. De de stortplaatsverrichting van DB schakelt de toepassing aan onderhoudswijze, houdt de processen van de consumentenrij tegen, en maakt cron banen onbruikbaar alvorens de stortplaats begint.

Overweeg de volgende richtlijnen voor stortplaats van DB:

- Voor productieomgevingen raadt Adobe aan de databasedumportbewerkingen tijdens niet-piekuren uit te voeren om de onderbreking van de service die optreedt wanneer de site in de onderhoudsmodus staat, tot een minimum te beperken.
- Als een fout tijdens de stortplaatsverrichting voorkomt, schrapt het bevel het stortplaatsdossier om schijfruimte te besparen. Bekijk de logboeken voor details (`var/log/cloud.log`).
- Voor Pro de milieu&#39;s van de Productie, dumpt dit bevel slechts van _één_ van de drie high-availability knopen, zodat zouden de productiegegevens die aan een verschillende knoop tijdens de stortplaats worden geschreven niet kunnen worden gekopieerd. De opdracht genereert een `var/dbdump.lock` -bestand om te voorkomen dat de opdracht op meer dan één knooppunt wordt uitgevoerd.
- Voor een steun van alle milieudiensten, adviseert Adobe creërend a [&#x200B; steun &#x200B;](snapshots.md).

U kunt verkiezen aan file veelvoudige gegevensbestanden door de gegevensbestandnamen aan het bevel toe te voegen. In het volgende voorbeeld wordt een back-up gemaakt van twee databases: `main` en `sales` :

```bash
php vendor/bin/ece-tools db-dump main sales
```

Gebruik de opdracht `php vendor/bin/ece-tools db-dump --help` voor meer opties:

- `--dump-directory=<dir>` - Kies een doelmap voor de databasedumpdump. **kies geen openbare Webfolders zoals `pub/media` of`pub/static`**.
- `--remove-definers` - verwijder DEFINER-instructies van de database-dump.

**om een gegevensbestandstortplaats in het het Opvoeren of milieu van de Productie te creëren**:

1. [&#x200B; SSH van het Gebruik aan login of creeer een tunnel om met het verre milieu &#x200B;](../development/secure-connections.md) te verbinden die het gegevensbestand aan exemplaar bevat.

1. Maak een lijst van de omgevingsverhoudingen en neem nota van de gegevens van de gegevensbestandlogin.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

1. Maak een back-up van de database. Als u een doelmap voor de DB-dump wilt kiezen, gebruikt u de optie `--dump-directory` .

   >[!WARNING]
   >
   >Als u een doelmap opgeeft, kiest u geen openbare webmappen zoals `pub/media` of `pub/static` .

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
   [2020-01-28 16:38:10] INFO: Finished DB dump for main database, it can be found here: /app/qxmtlseakof6y/var/dump-main-1580229490.sql.gz
   [2020-01-28 16:38:10] INFO: Backup completed.
   [2020-01-28 16:38:11] NOTICE: Maintenance mode is disabled.
   ```

1. Met de opdracht `db-dump` maakt u een `dump-<timestamp>.sql.gz` -archiefbestand in de externe projectmap.

>[!TIP]
>
>Als u deze gegevens aan een specifiek milieu wilt duwen, zie [&#x200B; gegevens en statische dossiers migreren &#x200B;](../deploy/staging-production.md#migrate-static-files).
