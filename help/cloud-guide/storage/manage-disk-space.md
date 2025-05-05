---
title: Schijfruimte beheren
description: Leer hoe u schijfruimte beheert met behulp van de opdrachtregelinterface.
feature: Cloud, Storage
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# Schijfruimte beheren

U kunt de totale opslagcapaciteit voor uw project van de Wolk in uw Adobe Commerce op het contract van de wolkeninfrastructuur en op uw [ rekeningspagina ](https://accounts.magento.cloud/user) vinden. Elke projectkaart in uw rekening toont het aantal _milieu&#39;s_, de _opslag_ capaciteit in GB, en het aantal _gebruikers_. U kunt ook de volgende Cloud-opdracht gebruiken:

```bash
magento-cloud subscription:info | grep storage
```

Monsterrespons:

```
| storage              | 51200
```

Wanneer een Pro-productie- of -testomgeving 95% van de opslagcapaciteit bereikt of overschrijdt, wordt met het hulpprogramma voor bewaking van de cloudinfrastructuur een supportwaarschuwing weergegeven waarin u op de hoogte wordt gesteld van een automatische toename van de opslagcapaciteit.

Voorbeeldmelding:

>[!BEGINSHADEBOX]

_&quot;Onze controle heeft dossieropslag op uw cluster (project-id-milieu) ontdekt bijna volledig. Het schijfgebruik bevindt zich momenteel op kritieke gebruiksniveaus met nog geen 1 GiB. Het volume van de gedeelde opslag wordt momenteel verhoogd van 60 GiB tot 70 GiB om uw diensten in gebruik te houden. Gelieve te nemen een blik bij de productie en het opvoeren van dossiergebruik om te zien of kunt u wat ruimte ontruimen.&quot;_

>[!ENDSHADEBOX]

>[!TIP]
>
>U wordt aangeraden regelmatig uw opslagcapaciteit te controleren en deze goed onder de 90% te houden om deze automatische verhogingen te voorkomen. Als deze eenmaal zijn toegewezen, kan de opslagverhoging voor Pro-opslag en -productie niet worden teruggedraaid.

## Integratieomgeving controleren

U kunt het gebruik van schijfruimte voor uw integratieomgeving controleren met behulp van `magento-cloud` CLI.

**om het benaderende gebruik van de schijfruimte te controleren**:

```bash
magento-cloud db:size
```

Monsterrespons:

```
Checking database service mysql...

+----------------+-----------------+--------+
| Allocated disk | Estimated usage | % used |
+----------------+-----------------+--------+
| 2.0 GiB        | 193.3 MiB       | ~ 9%   |
+----------------+-----------------+--------+
```

Alle bevestigingen delen een schijf. Met de CLI `magento-cloud` kunt u het gebruik van schijfruimte voor montage controleren.

**om het benaderende gebruik van de schijfruimte voor steunen** te controleren:

```bash
magento-cloud mount:size
```

Monsterrespons:

```
Checking disk usage for all mounts on <project>-<environment>-mymagento@ssh.us.magento.cloud...

+------------+-----------+---------+-----------+-----------+--------+
| Mount(s)   | Size(s)   | Disk    | Used      | Available | % Used |
+------------+-----------+---------+-----------+-----------+--------+
| app/etc    | 184 KiB   | 1.9 GiB | 481.3 MiB | 1.4 GiB   | 24.7%  |
| pub/media  | 128 KiB   |         |           |           |        |
| pub/static | 158.2 MiB |         |           |           |        |
| var        | 316.7 MiB |         |           |           |        |
+------------+-----------+---------+-----------+-----------+--------+
```

## Specifieke clusters controleren

Voor Pro Staging- en productieomgevingen kunt u het gebruik van schijfruimte in elke omgeving controleren met de opdracht `disk free` , die de hoeveelheid schijfruimte rapporteert die door het bestandssysteem wordt gebruikt. U moet SSH gebruiken aan login aan een verre milieu.

```bash
df -h
```

Met de optie `-h` wordt het rapport weergegeven in een leesbare indeling (KB, MB of GB).

In de volgende voorbeeldreactie geeft de koppeling `/data/exports` de schijfruimte voor media weer en geeft de koppeling `/data/mysql/` schijfruimte voor de database weer:

```
Filesystem                                    Size  Used Avail Use% Mounted on
udev                                           16G     0   16G   0% /dev
tmpfs                                         3.2G  9.1M  3.2G   1% /run
/dev/xvda1                                     59G  8.9G   48G  16% /
tmpfs                                          16G   36K   16G   1% /dev/shm
tmpfs                                         5.0M     0  5.0M   0% /run/lock
tmpfs                                          16G     0   16G   0% /sys/fs/cgroup
/dev/xvdj                                     9.8G  2.3G  7.6G  23% /data/mysql
/dev/xvdi                                     9.8G  491M  9.3G   5% /data/exports
192.168.5.5:/shared                           9.8G  591M  9.3G   6% /mnt/shared
/dev/loop0                                     91M   91M     0 100% /app/project
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
192.168.5.5:/shared/project/app/etc     9.8G  591M  9.3G   6% /app/project/app/etc
192.168.5.5:/shared/project/pub/media   9.8G  591M  9.3G   6% /app/project/pub/media
192.168.5.5:/shared/project/pub/static  9.8G  591M  9.3G   6% /app/project/pub/static
```

U kunt de reactie beperken door een map op te geven. Bijvoorbeeld:

```bash
df -h var/
```

Monsterrespons:

```
Filesystem                                    Size  Used Avail Use% Mounted on
192.168.5.5:/shared/project/var         9.8G  591M  9.3G   6% /app/project/var
```

## Schijfruimte toewijzen

Twee [ configuratiedossiers ](../environment/overview.md) controleren de toewijzing van schijfruimte in de milieu&#39;s van de Wolk: het `.magento.app.yaml` dossier en het `.magento/services.yaml` dossier. Elk bestand bevat de eigenschap `disk` , die de waarde van de schijfgrootte in MB voor de respectievelijke configuratie definieert. U kunt de toewijzing van schijfruimte alleen wijzigen in Pro-integratie- en Starter-omgevingen.

>[!IMPORTANT]
>
>Voor ProProductie en het Opvoeren milieu&#39;s, moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voorleggen om de toewijzing van de schijfruimte te veranderen. Een grootteverhoging van de milieu&#39;s van de Proproductie en van het Staging kan slechts met bepaalde intervallen voorkomen, zodat, afhankelijk van uw huidig gebruik van de schijfruimte, de steun zou kunnen adviseren om schijftoewijzing met een minimum van 10 GB te verhogen. Als deze eenmaal zijn toegewezen, kan de opslagverhoging voor Pro-opslag en -productie niet worden teruggedraaid. Opslag kan niet opnieuw worden toegewezen of herverdeeld tussen bronnen. Als u meer opslagruimte voor bestanden wilt toevoegen, verkleint u de schijfruimte die aan MySQL is toegewezen.

### Schijfruimte van toepassing

Het `.magento.app.yaml` dossier controleert de [ blijvende schijfruimte ](../application/properties.md#disk) beschikbaar aan de toepassing.

**om schijfruimte voor uw toepassing** te verhogen:

1. Open het configuratiebestand van `.magento.app.yaml` in uw lokale ontwikkelomgeving.

1. Stel een nieuwe waarde in voor de eigenschap `disk` (in MB).

   ```yaml
   disk: <value-mb>
   ```

1. Sla de wijzigingen op in het bestand.

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento.app.yaml && git commit -m "Increase disk space for application" && git push origin <branch-name>
   ```

   De wijzigingen worden van kracht nadat u het bijgewerkte YAML-bestand naar de externe omgeving hebt geduwd.

### Schijfruimte van service

Het bestand `.magento/services.yaml` bestuurt de schijfruimte die beschikbaar is voor elke service, zoals MySQL en Redis.

**om schijfruimte voor de dienst** te verhogen:

1. Open het configuratiebestand van `.magento/services.yaml` in uw lokale ontwikkelomgeving.

1. Voeg een service toe of zoek een service in het bestand. Zie [ meer over het vormen van de diensten ](../services/services-yaml.md).

1. Stel een nieuwe waarde in voor de eigenschap disk (in MB).

   ```yaml
   <name>:
       type: <service-name>:<service-version>
       disk: <value-mb>
   ```

1. Sla de wijzigingen op in het bestand.

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml && git commit -m "Increase disk space for service" && git push origin <branch-name>
   ```

   De wijzigingen worden van kracht nadat u het bijgewerkte YAML-bestand naar de externe omgeving hebt geduwd.

## Schijfruimte van monitor

In een Pro Production-omgeving kunt u de schijfruimte en andere prestatie-indicatoren controleren aan de hand van de Beheerde waarschuwingen voor het Adobe Commerce-waarschuwingsbeleid voor New Relic. Voor details, zie [ prestaties van de Monitor met Beheerde Alarm ](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts). Voor verdere begeleiding, zie [ Beste praktijken om de kwesties van gegevensbestandprestaties ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/resolve-database-performance-issues.html?lang=nl-NL) op te lossen.

## Geen ruimte meer over

De buildcache kan na verloop van tijd groter worden. Als u een waarschuwing ontvangt met de status `No space left on device` , probeert u de cache voor samenstellen te wissen en opnieuw te implementeren:

```bash
magento-cloud project:clear-build-cache
```
