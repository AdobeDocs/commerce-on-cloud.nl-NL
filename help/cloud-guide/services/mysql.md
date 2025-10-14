---
title: MySQL-service instellen
description: Leer hoe u de MySQL-service beheert voor permanente gegevensopslag met Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Services, Storage
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# MySQL-service instellen

De `mysql` dienst verstrekt blijvende gegevensopslag die op [&#x200B; wordt gebaseerd MariaDB &#x200B;](https://mariadb.com/) versies 10.2 tot 10.4, ondersteunend de [&#x200B; XtraDB &#x200B;](https://docs.percona.com/percona-xtradb-cluster/8.0/index.html) opslagmotor en heropgezette eigenschappen van MySQL 5.6 en 5.7.

Het opnieuw indexeren op MariaDB 10.4 neemt meer tijd in vergelijking met andere versies MariaDB of MySQL. Zie [&#x200B; Indexers &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html?lang=nl-NL#indexers) in de _Beste praktijken van Prestaties_ gids.

>[!WARNING]
>
>Wees voorzichtig wanneer het bevorderen van MariaDB van versie 10.1 tot 10.2. MariaDB 10.1 is de laatste versie die _XtraDB_ als opslagmotor steunt. MariaDB 10.2 gebruikt _InnoDB_ voor de opslagmotor. Nadat u van 10.1 aan 10.2 bevordert, kunt u niet de verandering terugdraaien. Adobe Commerce ondersteunt beide opslagengines. U moet echter wel de extensies en andere systemen controleren die door uw project worden gebruikt om te controleren of deze compatibel zijn met MariaDB 10.2. Zie [&#x200B; Incompatibele Veranderingen tussen 10.1 en 10.2 &#x200B;](https://mariadb.com/kb/en/upgrading-from-mariadb-101-to-mariadb-102/#incompatible-changes-between-101-and-102).

{{service-instruction}}

**om MySQL** toe te laten:

1. Voeg de vereiste naam, het type en de schijfwaarde (in MB) toe aan het `.magento/services.yaml` -bestand.

   ```yaml
   mysql:
       type: mysql:<version>
       disk: 5120
   ```

   >[!TIP]
   >
   >MySQL-fouten, zoals `PDO Exception: MySQL server has gone away` , kunnen optreden als er onvoldoende schijfruimte is. Controleer of u voldoende schijfruimte hebt toegewezen aan de service in het [`.magento/services.yaml`](services-yaml.md#disk) -bestand.

1. Configureer de relaties in het `.magento.app.yaml` -bestand.

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable mysql service" && git push origin <branch-name>
   ```

1. [&#x200B; verifieer de de dienstverhoudingen &#x200B;](services-yaml.md#service-relationships).

{{service-change-tip}}

## MySQL-database configureren

U hebt de volgende opties wanneer het vormen van het gegevensbestand MySQL:

- **`schemas`** - Een schema definieert een database. Het standaardschema is de `main` -database.
- **`endpoints`** - Elk eindpunt vertegenwoordigt een referentie met specifieke bevoegdheden. Het standaardeindpunt is `mysql` , dat `admin` toegang heeft tot de `main` -database.
- **`properties`** - De eigenschappen worden gebruikt om extra gegevensbestandconfiguraties te bepalen.

Hieronder volgt een eenvoudige voorbeeldconfiguratie in het `.magento/services.yaml` -bestand:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

`properties` in het bovenstaande voorbeeld wijzigt de standaard `optimizer` montages zoals [&#x200B; geadviseerd in de gids van Beste praktijken van Prestaties &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/configuration.html?lang=nl-NL#indexers).

**MariaDB configuratieopties**:

| Opties | Beschrijving | Standaardwaarde |
| -------------------- | --------------------------------------------------- | ------------------ |
| `default_charset` | De standaardtekenset. | utf8mb4 |
| `default_collation` | De standaardsortering. | utf8mb4_unicode_ci |
| `max_allowed_packet` | Maximale grootte voor pakketten, in MB. Bereik `1` tot `100` . | 16 |
| `optimizer_switch` | Stel waarden in voor de functie voor query-optimalisatie. Zie {de documentatie van 0} MariaDB [&#128279;](https://mariadb.com/kb/en/server-system-variables/#optimizer_switch). | |
| `optimizer_use_condition_selectivity` | Selecteer de statistieken die door optimizer worden gebruikt. Bereik `1` tot `5` . Zie {de documentatie van 0} MariaDB [&#128279;](https://mariadb.com/kb/en/server-system-variables/#optimizer_use_condition_selectivity). | 4 voor 10.4 en hoger |

### Meerdere databasegebruikers instellen

U kunt desgewenst meerdere gebruikers instellen met verschillende machtigingen voor toegang tot de `main` -database.

Standaard is er één eindpunt met de naam `mysql` dat beheerderstoegang tot de database heeft. Als u meerdere databasegebruikers wilt instellen, moet u meerdere eindpunten in het `services.yaml` -bestand definiëren en de relaties in het `.magento.app.yaml` -bestand declareren. Voor Pro het Opvoeren en de milieu&#39;s van de Productie, [&#x200B; voorleggen een kaartje van de Steun van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) om de extra gebruiker te verzoeken.

Gebruik een geneste array om de eindpunten voor specifieke gebruikerstoegang te definiëren. Elk eindpunt kan toegang tot één of meerdere schema&#39;s (gegevensbestanden) en verschillende niveaus van toestemming op elk aanwijzen.

De geldige machtigingsniveaus zijn:

- `ro`: alleen SELECT-query&#39;s zijn toegestaan.
- `rw`: query&#39;s SELECT en query&#39;s INSERT, UPDATE en DELETE zijn toegestaan.
- `admin`: Alle vragen zijn toegestaan, met inbegrip van vragen DDL (CREATE LIJST, DROP LIJST, en meer).

Bijvoorbeeld:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
    configuration:
        schemas:
            - main
        endpoints:
            admin:
                default_schema: main
                privileges:
                    main: admin
            reporter:
                privileges:
                    main: ro
            importer:
                privileges:
                    main: rw
        properties:
            optimizer_switch: "rowid_filter=off"
            optimizer_use_condition_selectivity: 1
```

In het vorige voorbeeld biedt het eindpunt `admin` beheerderniveau toegang tot de database `main` , biedt het eindpunt `reporter` alleen-lezen toegang en het eindpunt `importer` biedt alleen-lezen toegang, wat betekent:

- De gebruiker van `admin` heeft volledige controle over de database.
- De gebruiker `reporter` heeft alleen SELECT-rechten.
- De gebruiker van `importer` heeft SELECT, INSERT, UPDATE, en DELETE voorrechten.

Voeg de eindpunten die in het bovenstaande voorbeeld worden gedefinieerd, toe aan de eigenschap `relationships` van het `.magento.app.yaml` -bestand. Bijvoorbeeld:

```yaml
relationships:
    database: "mysql:admin"
    databasereporter: "mysql:reporter"
    databaseimporter: "mysql:importer"
```

>[!NOTE]
>
>Als u één gebruiker MySQL vormt, kunt u niet het [`DEFINER` &#x200B;](https://dev.mysql.com/doc/refman/8.0/en/show-grants.html) toegangsbeheermechanisme voor opgeslagen procedures en meningen gebruiken.

## Verbinding maken met de database

Als u rechtstreeks toegang wilt krijgen tot de MariaDB-database, moet u een SSH gebruiken om u aan te melden bij de externe Cloud-omgeving en verbinding te maken met de database.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Haal de MySQL login geloofsbrieven van de `database` en `type` eigenschappen in de [$MAGENTO_CLOUD_RELATIONSHIPS &#x200B;](../application/properties.md#relationships) variabele terug.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   In de reactie, vind de informatie MySQL. Bijvoorbeeld:

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

1. Maak verbinding met de database.

   - Gebruik voor Starter de volgende opdracht:

     ```bash
     mysql -h database.internal -u <username>
     ```

   - Gebruik voor Pro de volgende opdracht met hostnaam, poortnummer, gebruikersnaam en wachtwoord uit de variabele `$MAGENTO_CLOUD_RELATIONSHIPS` .

     ```bash
     mysql -h <hostname> -P <number> -u <username> -p'<password>'
     ```

>[!TIP]
>
>Met de opdracht `magento-cloud db:sql` kunt u verbinding maken met de externe database en SQL-opdrachten uitvoeren.

## Verbinding maken met secundaire database

>[!IMPORTANT]
>
>Deze functie is alleen beschikbaar voor Pro Production- en Staging-clusters.

Soms, moet u met het secundaire gegevensbestand verbinden om gegevensbestandprestaties te verbeteren of gegevensbestand het sluiten kwesties op te lossen. Als deze configuratie vereist is, gebruikt u `"port" : 3304` om de verbinding tot stand te brengen. Zie [&#x200B; Beste praktijken om het MySQL slave verbindings &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration.html?lang=nl-NL) onderwerp in de _gids van de Beste praktijken van de Implementatie_ te vormen.

## Problemen oplossen

Raadpleeg de volgende Adobe Commerce Support-artikelen voor hulp bij het oplossen van MySQL-problemen:

- [&#x200B; die langzame vragen controleert en MySQL &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/checking-slow-queries-and-processes-mysql.html?lang=nl-NL) verwerkt
- [&#x200B; creeer gegevensbestandstortplaats op Wolk &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud.html?lang=nl-NL)
- [&#x200B; het oplossen van problemen van het Hulpmiddel van de Migratie van Gegevens &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-migration-tool-troubleshooting.html?lang=nl-NL)
- [&#x200B; verbetering van Adobe Commerce: compact aan dynamische lijsten 2.2.x, 2.3.x aan 2.4.x &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/maintenance/commerce-235-upgrade-prerequisites-mariadb.html?lang=nl-NL)
