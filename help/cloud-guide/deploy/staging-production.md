---
title: Distribueren naar Staging en Productie
description: Leer hoe u uw Adobe Commerce-code voor cloudinfrastructuur kunt implementeren in de Staging- en Productomgevingen voor verdere tests.
feature: Cloud, Console, Deploy, SCD, Storage
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 0%

---

# Distribueren naar Staging en Productie

Het proces voor het opstellen en het gaan leven begint met ontwikkeling, blijft het Opvoeren, en eindigt met het leven in Productie. De Adobe verstrekt een milieu-oplossing van begin tot eind om verenigbare configuraties te verzekeren. Elke milieu steunt directe toegang URL tot de storefront en Admin en toegang SSH voor CLI bevelen.

Wanneer u klaar bent om uw opslag op te stellen, moet u plaatsing en het testen op het Opvoeren milieu voltooien alvorens aan Productie op te stellen. Deze sectie bevat diepgaande instructies en informatie over het proces voor het maken en implementeren, het migreren van gegevens en inhoud en het testen.

>[!TIP]
>
>De Adobe adviseert het creëren van a [&#x200B; steun &#x200B;](../storage/snapshots.md) van het milieu vóór plaatsingen.

Ook, kunt u [&#x200B; plaatsingen van het Spoor met New Relic &#x200B;](../monitor/track-deployments.md) toelaten om plaatsingsgebeurtenissen te controleren en u te helpen prestaties tussen plaatsingen analyseren.

## Startimplementatiestroom

Adobe raadt u aan een `staging` -vertakking van de `master` -vertakking te maken om de ontwikkeling en implementatie van uw Starter-abonnement het beste te ondersteunen. Dan hebt u twee van uw vier actieve milieu&#39;s klaar: `master` voor Productie en `staging` voor Staging.

Voor gedetailleerde informatie van het proces, zie [&#x200B; Begin Ontwikkelen en Werkschema &#x200B;](../architecture/starter-develop-deploy-workflow.md) opstellen.

## Pro-implementatiestroom

Pro wordt geleverd met een grote integratieomgeving met twee actieve vertakkingen, een globale `master` vertakking, Staging en Production vertakkingen. Wanneer u uw project creeert, is de code klaar om zich te vertakken, te ontwikkelen, en te duwen voor de bouw van en het opstellen van uw plaats. Hoewel de integratieomgeving vele vertakkingen kan hebben, hebben het Staging en de Productie slechts één tak voor elk milieu.

Voor gedetailleerde informatie van het proces, zie [&#x200B; Pro Ontwikkelen en Werkschema &#x200B;](../architecture/pro-develop-deploy-workflow.md) opstellen.

## Code implementeren naar fasering

De het Staging milieu verstrekt een bijna-productiemilieu dat een gegevensbestand, Webserver, en alle diensten met inbegrip van Fastly en New Relic omvat. U kunt volledig duwen, samenvoegen, en door [[!DNL Cloud Console]](../project/overview.md) of [&#x200B; Cloud CLI bevelen &#x200B;](../dev-tools/cloud-cli-overview.md) door een eindtoepassing opstellen.

### Code implementeren met de [!DNL Cloud Console]

[!DNL Cloud Console] verstrekt eigenschappen om, code in de milieu&#39;s van de Integratie, het Staging, en van de Productie voor Startpagina en Pro plannen tot stand te brengen te beheren en op te stellen.

**voor Pro projecten, stel de integratietak aan het opvoeren** op:

1. [&#x200B; Login &#x200B;](https://accounts.magento.cloud) aan uw project.
1. Selecteer de `integration` -vertakking.
1. Selecteer de **optie van de Fusie** om aan het Opvoeren op te stellen.

   ![&#x200B; Fusie &#x200B;](../../assets/button-merge.png){width="150"}

1. Voltooi al [&#x200B; het testen &#x200B;](../test/staging-and-production.md) in het milieu van het Staging.
1. Wanneer het Staging klaar is, selecteer de **1&rbrace; optie van de Fusie &lbrace;om aan Productie op te stellen.**

**voor Begin, stel de ontwikkelingstak aan het opvoeren** op:

1. [&#x200B; Login &#x200B;](https://accounts.magento.cloud) aan uw project.
1. Selecteer de voorbereide codevertakking.
1. Selecteer de **optie van de Fusie** om aan het Opvoeren op te stellen.

   ![&#x200B; Fusie &#x200B;](../../assets/button-merge.png){width="150"}

1. Voltooi al [&#x200B; het testen &#x200B;](../test/staging-and-production.md) in het milieu van het Staging.
1. Wanneer het Staging klaar is, selecteer de **1&rbrace; optie van de Fusie &lbrace;om aan Productie (`master`) op te stellen.**

### Code implementeren met de opdrachtregel

De Cloud CLI bevat opdrachten voor het implementeren van code. U hebt SSH en Git toegang tot uw project nodig.

#### Stap 1: Implementeer en test de integratieomgeving

1. Na het registreren in het project, controleer het integratiemilieu:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synchroniseer uw lokale integratieomgeving met de externe omgeving:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Maak een momentopname van de omgeving als back-up:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Werk de code in uw lokale vertakking naar wens bij.

1. Wijzigingen aan de omgeving toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add -A && git commit -m "Commit message" && git push origin <environment-ID>
   ```

1. Volledige sitetests.

#### Stap 2: De veranderingen van de fusie in het Staging en stelt op

1. Bekijk de testomgeving:

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

1. Synchroniseer uw lokale Staging-omgeving met de externe omgeving:

   ```bash
   magento-cloud environment:synchronize <environment-ID>
   ```

1. Maak een momentopname van de omgeving als back-up:

   ```bash
   magento-cloud snapshot: create -e <environment-ID>
   ```

1. Voeg de integratieomgeving samen tot Staging om te implementeren:

   ```bash
   magento-cloud environment:merge <integration-ID>
   ```

1. Volledige sitetests.

#### Stap 3: Distribueren naar productie

1. U kunt een momentopname van uw lokale productieomgeving uitchecken, synchroniseren en maken.

1. Voeg de het Staging milieu aan Productie samen om op te stellen:

   ```bash
   magento-cloud environment:merge <staging-ID>
   ```

1. Volledige sitetests.

## Statische bestanden migreren

[&#x200B; de Statische dossiers &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-operations/implementation-playbook/glossary) worden opgeslagen in `mounts`. Er zijn twee methoden voor het migreren van bestanden van een bronmontagelocatie, zoals uw lokale omgeving, naar een doellocatie. Beide methoden gebruiken het hulpprogramma `rsync` , maar Adobe raadt u aan de CLI van `magento-cloud` te gebruiken om bestanden tussen de lokale en externe omgeving te verplaatsen. En Adobe raadt u aan de methode `rsync` te gebruiken wanneer u bestanden van een externe bron naar een andere externe locatie verplaatst.

### Bestanden migreren met CLI

Met de opdrachten `mount:upload` en `mount:download` CLI kunt u bestanden migreren tussen de lokale en externe omgeving. Beide opdrachten maken gebruik van het hulpprogramma `rsync` , maar de CLI-opdrachten bieden opties en aanwijzingen die zijn afgestemd op de Adobe Commerce op de cloud-infrastructuuromgeving. Bijvoorbeeld, als u het eenvoudige bevel zonder opties gebruikt, vraagt CLI u om te selecteren welke optelling of ophangingen om te uploaden of te downloaden.

```bash
magento-cloud mount:download
```

Monsterrespons:

```
Enter a number to choose a mount to download from:
  [0] app/etc
  [1] pub/static
  [2] var
  [3] pub/media
  [4] All mounts
 > 3

Target directory: ~/pub/media/

Downloading files from the remote mount pub/media to pub/media

Are you sure you want to continue? [Y/n] Y
```

**om dossiers van een lokale `pub/media/` omslag aan de verre `pub/media/` omslag voor het huidige milieu** te uploaden:

```bash
magento-cloud mount:upload --source /path/to/project/pub/media/ --mount pub/media/
```

Monsterrespons:

```
Uploading files from pub/media to the remote mount pub/media

Are you sure you want to continue? [Y/n] Y

  building file list ...   done
  ./
  sample-file.jpeg

  sent 8.43K bytes  received 48 bytes  3.39K bytes/sec
  total size is 154.57K  speedup is 18.23
```

Gebruik de optie `--help` voor de opdrachten `mount:upload` en `mount:download` om meer opties weer te geven. Er is bijvoorbeeld een optie `--delete` om tijdens de migratie andere bestanden te verwijderen.

### Bestanden migreren via synchroniseren

U kunt ook het hulpprogramma `rsync` gebruiken om bestanden te migreren.

```bash
rsync -azvP <source> <destination>
```

Voor deze opdracht worden de volgende opties gebruikt:

- `a`-archive
- `z` bestanden comprimeren tijdens de migratie
- `v`-verbose
- `P` gedeeltelijke voortgang

Zie [&#128279;](https://linux.die.net/man/1/rsync) hulp 0&rbrace; opnieuw synchroniseren.

>[!NOTE]
>
>Om media van ver-aan-verre milieu&#39;s direct over te brengen, moet u de agent van SSH toelaten door:sturen, zie {de begeleiding van 0} GitHub [&#128279;](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

**om statische dossiers van ver-aan-verre milieu&#39;s direct te migreren (snelle benadering)**:

1. Gebruik SSH om u aan te melden bij de bronomgeving. Gebruik de `magento-cloud` CLI niet. Het gebruik van de optie `-A` is belangrijk omdat hiermee het doorsturen van de verbinding met de verificatieagent wordt ingeschakeld.

   >[!TIP]
   >
   >Om de **toegang van SSH** verbinding in uw [!DNL Cloud Console] te vinden, selecteer het milieu en klik **Plaats van de Toegang**.

   ```bash
   ssh -A <environment_ssh_link@ssh.region.magento.cloud>
   ```

1. Gebruik de opdracht `rsync` om de map `pub/media` van uw bronomgeving naar een andere externe omgeving te kopiëren.

   ```bash
   rsync -azvP pub/media/ <destination_environment_ssh_link@ssh.region.magento.cloud>:pub/media/
   ```

1. Meld u aan bij de andere externe omgeving om te controleren of de bestanden correct zijn gemigreerd.

## De database migreren

>[!WARNING]
>
>Het importeren en exporteren van databases kan veel tijd in beslag nemen. Dit kan de prestaties en beschikbaarheid van de site beïnvloeden. Plan de invoer en de uitvoerverrichtingen tijdens off-piekuren om langzame prestaties of stroomonderbrekingen op de plaatsen van de Productie te verhinderen.

>[!BEGINSHADEBOX]

**Vereiste:** Een gegevensbestandstortplaats (zie Stap 3) zou gegevensbestandtrekkers moeten omvatten. Voor het dumpen van hen, bevestig u het [&#x200B; voorrechten van de TRIGGER &#x200B;](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_trigger) hebt.

>[!IMPORTANT]
>
>De gegevensbank van het integratiemilieu is strikt voor ontwikkelingstests en kan gegevens omvatten die u niet in het Opvoeren en Productie wilt migreren.

Voor ononderbroken integratieplaatsingen, adviseert de Adobe **niet** migrerende gegevens van Integratie aan het Opvoeren en de Productie. U kunt testgegevens doorgeven of belangrijke gegevens overschrijven. Om het even welke vitale configuraties worden overgegaan gebruikend het [&#x200B; configuratiedossier &#x200B;](../store/store-settings.md) en `setup:upgrade` bevel tijdens bouwstijl en opstellen.

>[!ENDSHADEBOX]

Adobe **adviseert** migrerend gegevens van Productie in het Opvoeren om uw plaats volledig te testen en in een dichtbij-productiemilieu met alle diensten en montages op te slaan.

>[!NOTE]
>
>Om media van ver-aan-verre milieu&#39;s rechtstreeks over te brengen moet u de agent toelaten door:sturen, zie {de begeleiding van 0} GitHub [&#128279;](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/using-ssh-agent-forwarding).

### Back-up maken van de database

U kunt het beste een back-up van de database maken. De volgende procedure gebruikt de begeleiding van [&#x200B; file het gegevensbestand &#x200B;](../storage/database-dump.md).

**om het gegevensbestand** te dumpen:

1. [&#x200B; SSH van het Gebruik aan login aan het verre milieu &#x200B;](../development/secure-connections.md#use-an-ssh-command) dat het gegevensbestand aan exemplaar bevat.

1. Maak een lijst van de omgevingsverhoudingen en neem nota van de gegevens van de gegevensbestandlogin.

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]))->database);'
   ```

   Voor Pro Staging en Production staat de naam van de database in de variabele `MAGENTO_CLOUD_RELATIONSHIPS` (doorgaans gelijk aan de toepassingsnaam en gebruikersnaam).

1. Maak een back-up van de database. Als u een doelmap voor de DB-dump wilt kiezen, gebruikt u de optie `--dump-directory` .

   Voor Starter-omgevingen en Pro-integratieomgevingen gebruikt u `main` als de naam van de database:

   ```bash
   php vendor/bin/ece-tools db-dump main
   ```

   Snelopties:
   - `--dump-directory=<dir>` - Kies een doelmap voor de databasedumpit
   - `--remove-definers`—Verwijder DEFINITIEVE instructies uit de databasedumpdump

1. Hoewel de ECE-Hulpmiddelen methode de voorkeur heeft, moet een andere methode een dossier van de gegevensbestandstortplaats creëren gebruikend inheems MySQL in formaat GZIP.

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers <database-name> | gzip - > /tmp/database.sql.gz
   ```

   Als u tweefelige authentificatie op het doelmilieu hebt gevormd, is het beter om verwante 2FA lijsten uit te sluiten om het te vermijden opnieuw vormend na gegevensbestandmigratie:

   ```bash
   mysqldump -h <database-host> --user=<database-username> --password=<password> --single-transaction --triggers --ignore-table=<database-name>.tfa_user_config --ignore-table=<database-name>.tfa_country_codes <database-name> | gzip - > /tmp/database.sql.gz
   ```

1. Typ `logout` om de SSH-verbinding te beëindigen.

### De database neerzetten en opnieuw maken

Bij het importeren van gegevens moet u een database neerzetten en maken.

**om het gegevensbestand** te laten vallen en opnieuw te creëren:

1. Vestig een [&#x200B; tunnel van SSH &#x200B;](../development/secure-connections.md#ssh-tunneling) aan het verre milieu.

1. Maak verbinding met de databaseservice.

   ```bash
   mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
   ```

1. Laat de database vallen bij de `MariaDB [main]>` prompt.

   Voor Starter- en Pro-integratie:

   ```shell
   drop database main;
   ```

   Voor productie:

   ```shell
   drop database <cluster-id>;
   ```

   Voor opmaken:

   ```shell
   drop database <cluster-ID_stg>;
   ```

1. Maak de database opnieuw.

   Voor Starter- en Pro-integratie:

   ```shell
   create database main;
   ```

1. De database importeren.

   Invoer voor productie:

   ```shell
   zcat <cluster-ID>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   Importeren voor faseren:

   ```shell
   zcat <cluster-ID_stg>.sql.gz | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | mysql -h 127.0.0.1 -p -u <database-username> <database-name>;
   ```

   Deze opdrachten decomprimeren het databaseddump-bestand, verwijderen de instructies `DEFINER` en importeren de database met de opgegeven referenties.
