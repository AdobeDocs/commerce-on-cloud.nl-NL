---
title: Crons, eigenschap
description: Zie voorbeelden op hoe te om het bezit "crons"in het  [!DNL Commerce]  dossier van de toepassingsconfiguratie te vormen.
feature: Cloud, Configuration
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Crons, eigenschap

Adobe Commerce gebruikt de eigenschap `crons` om herhalende activiteiten te plannen. Het is ideaal voor het plannen van een specifieke taak om op bepaalde tijden van de dag te lopen. Vanwege de aard van alleen-lezen omgevingen kan slechts één snijtaak tegelijk op de webinstantie voor Adobe Commerce worden uitgevoerd voor cloudinfrastructuurprojecten. Het is aan te raden om taken die al lang worden uitgevoerd, op te splitsen in kleinere taken in een wachtrij. Alternatief, kunt u a [ arbeidersinstantie ](workers-property.md) bouwen.

De Adobe adviseert dat u `crons` als [ eigenaar van het dossiersysteem ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html?lang=nl-NL) in werking stelt. Voer _niet_ in `crons` zoals `root` of als gebruiker van de Webserver.

Deze configuratie is anders dan plaatsingen in het gebouw van Adobe Commerce, die veelvoudige standaard kantelbanen hebben. Zie [ cron banen ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html?lang=nl-NL) in de _gids van de Configuratie_ vormen.

## Uitsnijdtaken instellen

De eigenschap `crons` beschrijft processen die op een schema worden geactiveerd. Voor elke taak zijn een naam en de volgende opties vereist:

- `spec` - De expressie voor uitsnijden die wordt gebruikt voor planning.
- `cmd` - De opdracht die moet worden uitgevoerd op `start` en `stop` .
- `shutdown_timeout` - (_Facultatief_) als een kroonbaan wordt geannuleerd, is dit het aantal seconden waarna een signaal SIGKILL wordt verzonden om de baan of het proces tegen te houden. De standaardwaarde is 10 seconden.
- `timeout` - (_Facultatief_) de maximumhoeveelheid tijd een kroonbaan kan vóór onderbreking lopen. De standaardwaarde is 86400 seconden (24 uur).

Standaard heeft elk Commerce-wolkenproject de volgende standaardconfiguratie `crons` in het `.magento.app.yaml` -bestand:

```yaml
crons:
    cronrun:
        spec: "* * * * *"
        cmd: "php bin/magento cron:run"
```

Als uw project aangepaste uitsnijdtaken vereist, kunt u deze toevoegen aan de standaardconfiguratie `crons` . Zie [ bouwt een kroonbaan ](#build-a-cron-job).

### `crontab`

Adobe Commerce heeft alleen aan Pro-projecten een configuratieoptie voor automatische bakens toegevoegd ter ondersteuning van de zelfbedieningsconfiguratie `crons` in de omgevingen Staging en Production. Als deze optie is ingeschakeld, kunt u met `crontab` de configuratie van de uitsnede controleren. Dit is _niet_ beschikbaar met de projecten van de Aanzet.

Hoewel u `crontab` kunt gebruiken om de configuratie van Pro-projecten te controleren, gebruikt Adobe Commerce `crontab` niet om taken voor uitsnijden uit te voeren voor sites die worden geïmplementeerd in de cloud-infrastructuur.

**aan overzicht cron configuratie op Pro milieu&#39;s**:

1. Het gebruik [ SSH ](../development/secure-connections.md#use-an-ssh-command) aan login aan het verre milieu.

1. Vermeld de geplande uitsnijdprocessen.

   ```shell
   crontab -l
   ```

   >[!NOTE]
   >
   >Als het `crontab -l` bevel een `Command not found` fout (in Pro het Opvoeren en milieu&#39;s van de Productie slechts) terugkeert, moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voorleggen om de auto-crons zelfbedieningsconfiguratieoptie op uw project toe te laten.

In het volgende voorbeeld wordt de `crontab` -uitvoer getoond voor een omgeving die alleen de standaard `crons` -configuratie heeft:

```
username@hostname:~$ crontab -l
# Crontab is managed by the system, attempts to edit it directly will fail.
SHELL=/etc/platform/6fck2obu3244c/cron-run
MAILTO=""

# m h  dom mon dow  job_name

* * * * *           cronrun
```

## Een uitsnijdtaak maken

Een uitsnijdtaak bevat de planning- en tijdspecificatie en de opdracht die op de geplande tijd moet worden uitgevoerd. Voor Starter-omgevingen en Pro `integration`-omgevingen bedraagt het minimale interval één keer per vijf minuten. Voor Pro het Staging en van de Productie milieu&#39;s, is het minimuminterval eens per minuut. In Adobe Commerce op de cloud-infrastructuur voegt u aangepaste uitsnijdtaken toe aan het `.magento.app.yaml` -bestand in de `crons` -sectie. De algemene indeling is `spec` voor planning en `cmd` voor het opgeven van de opdracht of het aangepaste script dat moet worden uitgevoerd.

### Specificatie

Adobe Commerce gebruikt een expressie van vijf waarden voor een `crons` specificatie (spec): `* * * * *`

1. Minuut (0 tot en met 59) Voor alle Starter- en Pro-omgevingen is de minimale frequentie die wordt ondersteund voor taken voor cron vijf minuten. Mogelijk moet u instellingen configureren in uw beheerder.
2. Uur (0 tot en met 23)
3. Dag van de maand (1 tot en met 31)
4. Maand (1 tot en met 12)
5. Dag van de week (0 tot en met 6) (zondag tot en met zaterdag; 7 is ook zondag op sommige systemen)

Enkele voorbeelden:

- `00 */3 * * *` wordt elke drie uur uitgevoerd op de eerste minuut (12:00, 3:00, 6:00 uur)
- `20 */8 * * *` wordt om de 8 uur uitgevoerd op minuut 20 (12:20, 8:20, 4:20)
- `00 00 * * *` wordt eenmaal per dag om middernacht uitgevoerd
- `00 * * * 1` wordt één keer per week uitgevoerd op maandag om middernacht.

>[!NOTE]
>
>De `crons` tijd die in het `.magento.app.yaml` -bestand wordt opgegeven, is gebaseerd op de tijdzone van de server, niet op de tijdzone die is opgegeven in de configuratiewaarden van de opslagruimte in de database.

Wanneer het bepalen van het plannen, overweeg de tijd het neemt om de taak te voltooien. Als u bijvoorbeeld om de drie uur een taak uitvoert en de taak 40 minuten duurt, kunt u overwegen de geplande tijd te wijzigen.

### Opdracht

In `cmd` wordt de opdracht of het aangepaste script opgegeven die moet worden uitgevoerd. Het formaat van het bevelmanuscript kan het volgende omvatten:

```text
<path-to-php-binary> <project-dir>/<script-command>
```

Bijvoorbeeld:

```yaml
crons:
    spec: "00 */8 * * *"
    cmd: "/usr/bin/php /app/abc123edf890/bin/magento export:start catalog_category_product"
```

In dit voorbeeld is `<path-to-php-binary>` `/usr/bin/php` . De installatiemap, die de project-id bevat, is `/app/abc123edf890/bin/magento` en de scripthandeling is `export:start catalog_category_product` .

### Aangepaste uitsnijdtaken toevoegen aan uw project

Op het Adobe Commerce-platform voor cloudinfrastructuur kunt u aanpassingen toevoegen aan de sectie `crons` van het [`.magento.app.yaml`](../application/configure-app-yaml.md) -bestand.

>[!NOTE]
>
>Voor Starter-omgevingen en Pro `integration`-omgevingen bedraagt het minimale interval één keer per vijf minuten. Voor Pro het Staging en van de Productie milieu&#39;s, is het minimuminterval eens per minuut. U kunt geen frequentere intervallen dan de standaardminimumintervallen vormen.

Voor de Pro projecten van Adobe Commerce, moet de [ auto-bakens eigenschap ](#set-up-cron-jobs) op uw project worden toegelaten alvorens u de banen van de douanecurn aan het Opvoeren en van de Productie milieu&#39;s kunt toevoegen gebruikend het `.magento.app.yaml` dossier. Als deze eigenschap niet wordt toegelaten, [ voorlegt een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) om auto-bakens toe te laten.

**om de banen van de douanecurn** toe te voegen:

1. Bewerk het bestand `.magento.app.yaml` in de map Adobe Commerce `/app` in uw lokale ontwikkelomgeving.

1. Voeg in de sectie `crons` de aanpassing toe in de volgende indeling:

   ```yaml
   crons:
       <cron_name_1>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
       <cron_name_2>:
           spec: "<schedule_time>"
           cmd: "<schedule_command>"
   ```

   In het volgende voorbeeld exporteert de `productcatalog` -taak de productcatalogus elke acht uur, 20 minuten na het uur.

   ```yaml
   crons:
       magento:
           spec: '* * * * *'
           cmd: 'php bin/magento cron:run'
       productcatalog:
           spec: '20 */8 * * *'
           cmd: 'bin/magento export:start catalog_product_category'
   ```

1. Wijzigingen in code toevoegen, vastleggen en doorvoeren.

   ```bash
   git add .magento.app.yaml && git commit -m "cron config updates" && git push origin <branch-name>
   ```

### Snijtaken bijwerken

Als u een aangepaste taak wilt toevoegen, verwijderen of bijwerken, wijzigt u de configuratie in de sectie `crons` van het `.magento.app.yaml` -bestand. Vervolgens test u de updates in de externe `integration` -omgeving voordat u de wijzigingen doorvoert in de Staging- en Productieomgeving.

## Snijtaken uitschakelen

U kunt snijtaken handmatig uitschakelen voordat u onderhoudstaken uitvoert, zoals opnieuw indexeren of het cachegeheugen schoonmaken om prestatieproblemen te voorkomen. U kunt de `ece-tools` CLI-opdracht `cron:disable` gebruiken om alle uitsnijdtaken uit te schakelen en actieve uitsnijdprocessen te stoppen.

**om kroonbanen** onbruikbaar te maken:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Hiermee schakelt u uitsnijdtaken uit en stopt u actieve uitsnijdprocessen.

   ```shell
   ./vendor/bin/ece-tools cron:disable
   ```

1. Nadat u alle vereiste onderhoudstaken hebt uitgevoerd, dient u de uitsnijdtaken opnieuw in te schakelen.

   ```shell
   ./vendor/bin/ece-tools cron:enable
   ```

## Problemen met uitsnijdtaken oplossen

Adobe heeft het Adobe Commerce-pakket voor cloudinfrastructuur bijgewerkt om de verwerking van cron op het Adobe Commerce-platform voor cloudinfrastructuur te optimaliseren en om problemen met betrekking tot cloudinfrastructuur op te lossen. Als u problemen ondervindt met de verwerking van bijsnijden, controleert u of uw project de meest actuele versie van het `ece-tools` -pakket gebruikt. Zie [ Update ECE-Hulpmiddelen ](../dev-tools/update-package.md).

U kunt de gegevens van de cron-verwerking bekijken in de logbestanden op toepassingsniveau voor elke omgeving. Zie [ Logboeken van de Toepassing ](../test/log-locations.md#application-logs).

Raadpleeg de volgende Adobe Commerce Support-artikelen voor hulp bij het oplossen van problemen met betrekking tot andere toepassingen:

- [ de taken van het de taakslot van het Gewas taken van andere groepen ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-tasks-lock-tasks-from-other-groups.html?lang=nl-NL)

- [ het Terugstellen van geplakt kroonbanen manueel op de wolk ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/reset-stuck-magento-cron-jobs-manually-on-cloud.html?lang=nl-NL)
