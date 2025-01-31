---
title: Logbestanden weergeven en beheren
description: Begrijp de typen logbestanden die beschikbaar zijn in de cloudinfrastructuur en waar u ze kunt vinden.
last-substantial-update: 2023-05-23T00:00:00Z
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Logbestanden weergeven en beheren

De logboeken voor Adobe Commerce op de projecten van de wolkeninfrastructuur zijn nuttig voor het oplossen van problemenproblemen met betrekking tot [ bouwen en stellen haken ](../application/hooks-property.md), de wolkendiensten, en de toepassing van Adobe Commerce op.

U kunt de logboeken van het dossiersysteem, [!DNL Cloud Console], en `magento-cloud` CLI bekijken.

- **het systeem van het Dossier** - de `/var/log` systeemfolder bevat logboeken voor alle milieu&#39;s. De map `var/log/` bevat toepassingsspecifieke logs die uniek zijn voor een bepaalde omgeving. Deze mappen worden niet gedeeld tussen knooppunten in een cluster. In Pro Productie en het Staging milieu&#39;s, moet u de logboeken op elke knoop controleren.

- **[!DNL Cloud Console]** - u kunt zien bouwen, opstellen, en post-stelt logboekinformatie in het milieu _berichten_ lijst op.

- **Cloud CLI** - u kunt lokale milieulogboeken bekijken gebruikend het `magento-cloud log` bevel of verre milieu logboeken gebruikend het `magento-cloud ssh` bevel.

## Loglocaties

Systeemlogboeken worden opgeslagen op de volgende locaties:

- Integratie: `/var/log/<log-name>.log`
- Pro Staging: `/var/log/platform/<project-ID>_stg/<log-name>.log`
- Pro Production: `/var/log/platform/<project-ID>/<log-name>.log`

De waarde van `<project-ID>` is afhankelijk van het project en of de omgeving Staging of Production is. Met bijvoorbeeld een project-id `yw1unoukjcawe` is de gebruiker van de omgeving Staging `yw1unoukjcawe_stg` en de gebruiker van de productieomgeving `yw1unoukjcawe` .

In dat voorbeeld is het implementatielogbestand: `/var/log/platform/yw1unoukjcawe_stg/deploy.log`

### Logboeken voor externe omgevingen weergeven

De meeste logboeken omvatten gebeurtenissen die in het verre milieu voorkomen. Voor Pro, zijn er veelvoudige knopen en elke knoop heeft unieke logboeken. Gebruik het volgende om een lijst van alle gastheren te zien:

```bash
magento-cloud ssh -p <project-ID> -e <environment-ID> --all
```

Monsterrespons:

```
1.ent-project-environment-id@ssh.region.magento.cloud
2.ent-project-environment-id@ssh.region.magento.cloud
3.ent-project-environment-id@ssh.region.magento.cloud
```

**om een lijst van verre milieu logboeken** te bekijken:

```bash
magento-cloud ssh -e <environment-ID> "ls var/log"
```

Voorbeeld voor Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "ls var/log | grep error"
```

**om een ver logboek** te bekijken:

```bash
magento-cloud ssh -e <environment-ID> "cat var/log/cron.log"
```

Voorbeeld voor Pro:

```bash
ssh 1.ent-project-environment-id@ssh.region.magento.cloud "cat var/log/cron.log"
```

>[!TIP]
>
>Voor Pro Staging- en Pro Production-omgevingen zijn automatische logrotatie, compressie en verwijdering ingeschakeld voor logbestanden met een vaste bestandsnaam. Elk logboekbestandstype heeft een roterend patroon en een levensduur.
>Meer informatie over de logrotatie en de levensduur van gecomprimeerde logbestanden in de omgeving vindt u in: `/etc/logrotate.conf` en `/etc/logrotate.d/<various>` .
>Voor Pro het Opvoeren en de Pro milieu&#39;s van de Productie, moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voorleggen om voor veranderingen in de configuratie van de logboekomwenteling te vragen.

>[!TIP]
>
>Logrotatie kan niet worden geconfigureerd in Pro-integratieomgevingen.
>Voor ProIntegratie, moet u een douaneoplossing/manuscript uitvoeren en [ vormt uw kruin ](../application/crons-property.md) om het manuscript in werking te stellen zoals nodig.

>[!NOTE]
>
>Starter-projectomgevingen hebben geen logrotatie.

## Logboeken samenstellen en implementeren

Nadat u wijzigingen in uw omgeving hebt aangebracht, kunt u de logboekregistratie bekijken vanaf elke haak in het `var/log/cloud.log` -bestand. Het logboek bevat begin en eindeberichten voor elke haak. In het volgende voorbeeld, zijn de berichten &quot;`Starting post-deploy.`&quot;en &quot;`Post-deploy is complete.`&quot;

Controleer de tijdstempels op logboekingangen, verifieer, en bepaal de plaats van de logboeken voor een specifieke plaatsing. Hieronder ziet u een beknopt voorbeeld van loguitvoer die u kunt gebruiken voor het oplossen van problemen:

```
Re-deploying environment project-integration-ID
  Executing post deploy hook for service `mymagento`
    [2019-01-03 19:44:11] NOTICE: Starting post-deploy.
    [2019-01-03 19:44:11] INFO: Validating configuration
    [2019-01-03 19:44:11] INFO: End of validation
    [2019-01-03 19:44:11] INFO: Enable cron
    [2019-01-03 19:44:11] INFO: Create backup of important files.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/env.php.bak for /app/app/etc/env.php was created.
    [2019-01-03 19:44:11] INFO: Backup /app/app/etc/config.php.bak for /app/app/etc/config.php was created.
    [2019-01-03 19:44:11] INFO: php ./bin/magento cache:flush --ansi --no-interaction
    [2019-01-03 19:44:32] INFO: Warming up failed: http://integration-id-project.us.magentosite.cloud/
    [2019-01-03 19:44:32] NOTICE: Post-deploy is complete.
```

>[!TIP]
>
>Wanneer u uw milieu van de Wolk vormt, kunt u opstelling [ op logboek-gebaseerde Slack en e-mailberichten ](../environment/set-up-notifications.md) voor bouwt en stelt acties op.

De volgende logboeken hebben een gemeenschappelijke plaats voor alle projecten van de Wolk:

- **Logboek van de Plaatsing**: `var/log/cloud.log`
- **laatste logboek van de plaatsingsfout**: `var/log/cloud.error.log`
- **zuivert logboek**: `var/log/debug.log`
- **Logboek van de Uitzondering**: `var/log/exception.log`
- **Logboek van het Systeem**: `var/log/system.log`
- **Logboek van de Steun**: `var/log/support_report.log`
- **Rapporten**: `var/report/`

Hoewel het `cloud.log` dossier terugkoppelt van elk stadium van het plaatsingsproces bevat, zijn de logboeken die door de op te stellen haak worden gecreeerd uniek aan elke milieu. Het milieu-specifieke opstellen logboek is in de volgende folders:

- **Begin en Pro integratie**: `/var/log/deploy.log`
- **Pro het Staging**: `/var/log/platform/<project-ID>_stg/deploy.log`
- **Proproductie**: `/var/log/platform/<project-ID>/deploy.log`

### Logbestand implementeren

Het logboek voor elke plaatsing schakelt aan het specifieke `deploy.log` dossier aaneen. Het volgende voorbeeld drukt het opstellen logboek van het huidige milieu in de terminal af:

```bash
magento-cloud log -e <environment-ID> deploy
```

Monsterrespons:

```
Reading log file projectID-branchname-ID--mymagento@ssh.zone.magento.cloud:/var/log/'deploy.log'

[2023-04-24 18:58:03.080678] Launching command 'b'php ./vendor/bin/ece-tools run scenario/deploy.xml\n''.

[2023-04-24T18:58:04.129888+00:00] INFO: Starting scenario(s): scenario/deploy.xml (magento/ece-tools version: 2002.1.14, magento/magento2-base version: 2.4.6)
[2023-04-24T18:58:04.364714+00:00] NOTICE: Starting pre-deploy.
...
```

{{scd-timing-warning}}

### Foutlogboek

Fout- en waarschuwingsberichten die tijdens het implementatieproces worden gegenereerd, worden zowel naar de `var/log/cloud.log` - als naar de `var/log/cloud.error.log` -bestanden geschreven. Het logbestand met fouten in de cloud bevat alleen fouten en waarschuwingen van de meest recente implementatie. Een leeg bestand geeft aan dat de implementatie zonder fouten is gelukt.

U kunt het logboekdossier bekijken gebruikend [ Cloud CLI SSH ](#view-remote-environment-logs), of u kunt ECE-Hulpmiddelen gebruiken om de fouten met suggesties te tonen:

```bash
magento-cloud ssh -e <environment-ID> "./vendor/bin/ece-tools error:show"
```

Monsterrespons:

```
errorCode: 1001
stage: build
step: validate-config
suggestion: Please run the following commands:
1. bin/magento module:enable --all
2. git add -f app/etc/config.php
3. git commit -m 'Adding config.php'
4. git push
title: File app/etc/config.php does not exist
type: warning
---------------

errorCode: 1006
stage: build
step: validate-config
suggestion: Your application does not have the "post_deploy" hook enabled.
  In order to minimize downtime, add the following to ".magento.app.yaml":
  hooks:
      post_deploy: |
          php ./vendor/bin/ece-tools run scenario/post-deploy.xml
title: The configured state is not ideal
type: warning
```

De meeste foutberichten bevatten een beschrijving en voorgestelde actie. Gebruik de [ het berichtverwijzing van de Fout voor ECE-Hulpmiddelen ](../dev-tools/error-reference.md) om de foutencode voor verdere begeleiding op te zoeken. Voor verdere begeleiding, gebruik de [ de plaatsingsprobleemoplosser van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html).

## Toepassingslogboeken

Toepassingslogboeken zijn net als logboeken voor implementatie uniek voor elke omgeving:

| Logbestand | Starter en Pro-integratie | Beschrijving |
| ------------------- | --------------------------- | ------------------------------------------------- |
| **Deploy logboek** | `/var/log/deploy.log` | De activiteit van [ stelt haak ](../application/hooks-property.md) op. |
| **Logboek van de post-opstellen** | `/var/log/post_deploy.log` | De activiteit van [ post-stelt haak ](../application/hooks-property.md) op. |
| **het logboek van het Gewas** | `/var/log/cron.log` | Uitvoer van snijtaken. |
| **Nginx toegangslogboek** | `/var/log/access.log` | Bij Nginx-start worden HTTP-fouten gegenereerd voor ontbrekende mappen en uitgesloten bestandstypen. |
| **Nginx foutenlogboek** | `/var/log/error.log` | Opstartberichten die nuttig zijn voor foutopsporing in configuratiefouten die aan Nginx zijn gekoppeld. |
| **PHP toegangslogboek** | `/var/log/php.access.log` | Verzoeken aan de PHP service. |
| **PHP FPM logboek** | `/var/log/app.log` | |

Voor Pro Staging- en productieomgevingen zijn de logbestanden Implementeren, Post-implementeren en Uitsnijden alleen beschikbaar op het eerste knooppunt in de cluster:

| Logbestand | Pro Staging | Pro Production |
| ------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **Deploy logboek** | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>_stg/deploy.log` | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>/deploy.log` |
| **Logboek van de post-opstellen** | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>_stg/post_deploy.log` | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>/post_deploy.log` |
| **het logboek van het Gewas** | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>_stg/cron.log` | Alleen eerste knooppunt:<br>`/var/log/platform/<project-ID>/cron.log` |
| **Nginx toegangslogboek** | `/var/log/platform/<project-ID>_stg/access.log` | `/var/log/platform/<project-ID>/access.log` |
| **Nginx foutenlogboek** | `/var/log/platform/<project-ID>_stg/error.log` | `/var/log/platform/<project-ID>/error.log` |
| **PHP toegangslogboek** | `/var/log/platform/<project-ID>_stg/php.access.log` | `/var/log/platform/<project-ID>/php.access.log` |
| **PHP FPM logboek** | `/var/log/platform/<project-ID>_stg/php5-fpm.log` | `/var/log/platform/<project-ID>/php5-fpm.log` |

### Gearchiveerde logbestanden

De toepassingslogboeken worden samengeperst en één keer per dag gearchiveerd en voor **30 dagen** gehouden. De gecomprimeerde logbestanden krijgen een naam met een unieke id die overeenkomt met de naam `Number of Days Ago + 1` . In Pro-productieomgevingen wordt bijvoorbeeld een PHP-toegangslogboek voor 21 dagen in het verleden opgeslagen en als volgt benoemd:

```
/var/log/platform/<project-ID>/php.access.log.22.gz
```

De gearchiveerde logboekdossiers worden altijd opgeslagen in de folder waar het originele dossier vóór compressie werd gevestigd.

>[!NOTE]
>
>**stelt** en **op:stellen** logboekdossiers op worden niet geroteerd en gearchiveerd. De volledige plaatsingsgeschiedenis wordt geschreven binnen die logboekdossiers.

## Servicelogboeken

Omdat elke dienst in een afzonderlijke container loopt, zijn de de dienstlogboeken niet beschikbaar in het integratiemilieu. Adobe Commerce on cloud Infrastructure biedt alleen toegang tot de webservercontainer in de integratieomgeving. De volgende locaties van het servicelogboek zijn bestemd voor de Pro Production- en Staging-omgevingen:

- **Redis logboek**: `/var/log/platform/<project-ID>_stg/redis-server-<project-ID>_stg.log`
- **logboek van de Elasticsearch**: `/var/log/elasticsearch/elasticsearch.log`
- **logboek van de huisvuilinzameling van Java**: `/var/log/elasticsearch/gc.log`
- **het logboek van de Post**: `/var/log/mail.log`
- **MySQL foutenlogboek**: `/var/log/mysql/mysql-error.log`
- **MySQL langzaam logboek**: `/var/log/mysql/mysql-slow.log`
- **het logboek van RabbitMQ**: `/var/log/rabbitmq/rabbit@host1.log`

De logboeken van de dienst worden gearchiveerd en voor verschillende periodes, afhankelijk van het logboektype bewaard. In MySQL-logboeken is bijvoorbeeld de kortste levensduur verwijderd na zeven dagen.

>[!TIP]
>
>De bestandslocaties van logbestanden in de geschaalde architectuur zijn afhankelijk van het type knooppunt. Zie {de plaatsen van het 0} Logboek in het Schaalde architectuur ](../architecture/scaled-architecture.md#log-locations) onderwerp.[

## Loggegevens voor Pro Production en Staging

Voor ProProductie en het Opvoeren milieu&#39;s, gebruik [ New Relic logboekbeheer ](../monitor/log-management.md) geïntegreerd met uw project om samengevoegde logboekgegevens van alle logboeken te beheren verbonden aan uw Adobe Commerce op het project van de wolkeninfrastructuur.

De New Relic Logs-toepassing biedt een gecentraliseerd logbeheerdashboard om Adobe Commerce problemen op te lossen en te controleren in productieomgevingen en testomgevingen voor cloudinfrastructuur. Het dashboard verleent ook toegang tot logboekgegevens voor de Snelle diensten van CDN, van de Optimalisering van het Beeld, en van de de toepassingsfirewall van het Web (WAF). Zie {de diensten van 0} New Relic ](../monitor/new-relic-service.md).[
