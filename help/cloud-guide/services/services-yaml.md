---
title: Services configureren
description: Leer hoe u services die door Adobe Commerce worden gebruikt op cloudinfrastructuur configureert.
feature: Cloud, Configuration, Services
exl-id: ddf44b7c-e4ae-48f0-97a9-a219e6012492
source-git-commit: 5fc2082ca2aae8a1466821075c01ce756ba382cc
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# Services configureren

In het bestand `services.yaml` worden de services gedefinieerd die door Adobe Commerce worden ondersteund en gebruikt op cloudinfrastructuur, zoals MySQL, Redis en Elasticsearch of OpenSearch. U hoeft zich niet in te schrijven op externe serviceproviders.

>[!NOTE]
>
>Het bestand `.magento/services.yaml` wordt lokaal beheerd in de map `.magento` van uw project. De configuratie wordt betreden tijdens het bouwstijlproces om de vereiste de dienstversies in het integratiemilieu slechts te bepalen, en wordt verwijderd zodra de plaatsing is voltooid, zodat zult u hen niet op de server vinden.


Het plaatsingsmanuscript gebruikt de configuratiedossiers in de `.magento` folder aan voorziening het milieu met de gevormde diensten. Een service wordt beschikbaar voor uw toepassing als deze wordt opgenomen in de eigenschap [`relationships`](../application/properties.md#relationships) van het `.magento.app.yaml` -bestand. Het `services.yaml` dossier bevat het _type_ en _schijf_ waarden. Het type van dienst bepaalt de dienst _naam_ en _versie_.

Het veranderen van een de dienstconfiguratie veroorzaakt een plaatsing aan voorziening het milieu met de bijgewerkte diensten, die de volgende milieu&#39;s beïnvloedt:

- Alle starteromgevingen, inclusief productie `master`
- Pro-integratieomgevingen

{{pro-update-service}}

## Standaard en ondersteunde services

De cloudinfrastructuur ondersteunt en implementeert de volgende services:

- [ActiveMQ](activemq.md)
- [MySQL](mysql.md)
- [Redis](redis.md)
- [KonijnMQ](rabbitmq.md)
- [Elasticsearch](elasticsearch.md)
- [OpenSearch](opensearch.md)

U kunt standaardversies en schijfwaarden in het huidige, [ standaard `services.yaml` dossier ](https://github.com/magento/magento-cloud/blob/master/.magento/services.yaml) bekijken. In het volgende voorbeeld worden de services `mysql` , `redis` , `opensearch` of `elasticsearch` , `rabbitmq` en `activemq-artemis` getoond die in het configuratiebestand `services.yaml` zijn gedefinieerd:

```yaml
mysql:
    type: mysql:10.4
    disk: 5120

redis:
    type: redis:6.2

opensearch:
    type: opensearch:2  # minor version not required; uses latest
    disk: 1024

rabbitmq:
    type: rabbitmq:3.9
    disk: 1024

activemq-artemis:
    type: activemq-artemis:2.42
    disk: 1024
```

## Servicewaarden

U moet de service-id en de configuratie van het servicetype opgeven `type: <name>:<version>` . Als de service blijvende opslag gebruikt, moet u een schijfwaarde opgeven.

Gebruik de volgende indeling:

```yaml
<service-id>:
    type: <name>:<version>
    disk: <value-MB>
```

### `service-id`

De `service-id` -waarde identificeert de service in het project. U kunt alleen alfanumerieke tekens in kleine letters gebruiken: `a` tot `z` en `0` tot `9` , zoals `redis` .

Deze _dienst-identiteitskaart_ waarde wordt gebruikt in het [`relationships`](../application/properties.md#relationships) bezit van het `.magento.app.yaml` configuratiedossier:

```yaml
relationships:
    redis: "<name>:redis"
```

U kunt meerdere instanties van elk servicetype een naam geven. U kunt bijvoorbeeld meerdere Redis-exemplaren gebruiken, een voor een sessie en een voor een cache.

```yaml
redis:
    type: redis:<version>

redis2:
    type: redis:<version>
```

Het anders noemen van de dienst in het `services.yaml` dossier **verwijdert permanent** het volgende:

- De bestaande service voordat u een service met de nieuwe naam maakt die u opgeeft.
- Alle bestaande gegevens voor de service worden verwijderd. Adobe adviseert sterk dat u [ steun uw milieu van de Aanzet ](../storage/snapshots.md) alvorens u de naam van een bestaande dienst verandert.

### `type`

De `type` -waarde geeft de servicenaam en -versie op. Bijvoorbeeld:

```yaml
mysql:
    type: mysql:10.4
```

### `disk`

De `disk` -waarde geeft de grootte aan van de permanente schijfopslag (in MB) die aan de service moet worden toegewezen. De diensten die blijvende opslag, zoals MySQL gebruiken, moeten een schijfwaarde verstrekken. Voor services die geheugen gebruiken in plaats van permanente opslag, zoals Redis, is geen schijfwaarde vereist.

```yaml
mysql:
    type: mysql:10.4
    disk: 5120
```

Het huidige standaard opslagbedrag per project is 5 GB of 512 0MB. U kunt dit bedrag tussen uw toepassing en elk van zijn diensten verdelen.

## Servicerelaties

In Adobe Commerce op de projecten van de wolkeninfrastructuur, de dienst [ verhoudingen ](../application/properties.md#relationships) die in het `.magento.app.yaml` dossier worden gevormd bepalen welke diensten aan uw toepassing beschikbaar zijn.

U kunt de configuratiegegevens voor alle de dienstverhoudingen van de [`$MAGENTO_CLOUD_RELATIONSHIPS`](../environment/variables-cloud.md) omgevingsvariabele terugwinnen. De configuratiegegevens omvatten de de dienstnaam, type, en versie samen met om het even welke vereiste verbindingsdetails zoals havenaantal en login geloofsbrieven.

**om verhoudingen in lokaal milieu** te verifiëren:

1. Geef in uw lokale omgeving de relaties voor de actieve omgeving weer.

   ```bash
   magento-cloud relationships
   ```

1. Bevestig de `service` en `type` in het antwoord. De reactie verstrekt verbindingsinformatie, zoals het IP adres en havenaantal.

   >Afkorting van monsterrespons

   ```yaml
   redis:
       -
   ...
           type: 'redis:7.0'
           port: 6379
   elasticsearch:
       -
   ...
           type: 'opensearch:2'
           port: 9200
   database:
       -
   ...
           type: 'mysql:10.6'
           port: 3306
   ```

**om verhoudingen in verre milieu&#39;s** te verifiëren:

1. Gebruik SSH om u aan te melden bij de externe omgeving.

1. Maak een lijst van de gegevens van de relatieconfiguratie voor alle diensten die in het milieu worden gevormd.

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   U kunt ook de volgende opdracht `ece-tools` gebruiken om relaties weer te geven:

   ```bash
   php ./vendor/bin/ece-tools env:config:show services
   ```

1. Bevestig de `service` en `type` in het antwoord. De reactie verstrekt verbindingsinformatie, zoals het IP adres en havenaantal en om het even welke vereiste gebruikersbenaming en wachtwoordgeloofsbrieven.

## Serviceversies

Serviceversie en compatibiliteitsondersteuning voor Adobe Commerce op cloudinfrastructuur worden bepaald door versies die worden geïmplementeerd en getest op de cloudinfrastructuur en verschillen soms van versies die worden ondersteund door Adobe Commerce-implementaties op locatie. Zie {de vereisten van het 0} Systeem [ in de ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) gids van de Installatie _voor een lijst van derdesoftwaregebiedsdelen die Adobe met specifieke versies van Adobe Commerce en van Magento Open Source heeft getest._

### Software EOL-controles

Tijdens het implementatieproces controleert het `ece-tools` -pakket de geïnstalleerde serviceversies op de einddatums (EOL) voor elke service.

- Als een de dienstversie binnen drie maanden na de datum EOL is, toont een bericht in het opstellen logboek.
- Als de datum EOL in het verleden is, toont een waarschuwingsbericht.

Om de veiligheid van de opslag te handhaven, werk geïnstalleerde softwareversies bij alvorens zij EOL bereiken. U kunt de data EOL in het [ dossier van 0} controleren-hulpmiddelen `eol.yaml`.](https://github.com/magento/ece-tools/blob/develop/config/eol.yaml)

### Migreren naar OpenSearch

{{elasticsearch-support}}

Voor versie 2.4.4 van Adobe Commerce en recenter, zie [ de dienst van OpenSearch van de Opstelling ](opensearch.md).

## Serviceversie wijzigen

U kunt de versie van de geïnstalleerde service upgraden voor compatibiliteit met de Adobe Commerce-versie die in uw cloud-omgeving is geïmplementeerd.

U kunt de de dienstversie voor een geïnstalleerde dienst niet direct degraderen. U kunt echter wel een service met de vereiste versie maken. Zie [ de dienstversie van de Verlaag ](#downgrade-version).

### Installatieversie van de service upgraden

U kunt de geïnstalleerde de dienstversie bevorderen door de de dienstconfiguratie in het `services.yaml` dossier bij te werken.

1. Wijzig de [`type`](#type) -waarde voor de service in het `.magento/services.yaml` -bestand:

   > Oorspronkelijke servicedefinitie

   ```yaml
   mysql:
       type: mysql:10.3
       disk: 2048
   ```

   > Bijgewerkte servicedefinitie

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml
   ```

   ```bash
   git commit -m "Upgrade MySQL from MariaDB 10.3 to 10.4."
   ```

   ```bash
   git push origin <branch-name>
   ```

### Downgrade

U kunt een geïnstalleerde service niet rechtstreeks downgraden. U hebt twee opties:

1. Wijzig de naam van een bestaande service met de nieuwe versie, waardoor de bestaande service en gegevens worden verwijderd en er een nieuwe wordt toegevoegd.

1. Creeer de dienst en sla de gegevens van de bestaande dienst op.

Wanneer u de serviceversie wijzigt, moet u de serviceconfiguratie in het `services.yaml` -bestand bijwerken en de relaties in het `.magento.app.yaml` -bestand bijwerken.

**om een de dienstversie te degraderen door de bestaande dienst** anders te noemen:

1. Wijzig de naam van de bestaande service in het `.magento/services.yaml` -bestand en wijzig de versie.

   >[!WARNING]
   >
   >Als u de naam van een bestaande service wijzigt, wordt deze vervangen en worden alle gegevens verwijderd. Als u de gegevens wilt behouden, maakt u een service in plaats van de naam van de bestaande service te wijzigen.

   Bijvoorbeeld, om de versie MariaDB voor de _mysql_ dienst van versie 10.4 tot 10.3 te degraderen, verander de bestaande _dienst-identiteitskaart_ en _type_ configuratie.

   > Oorspronkelijke `services.yaml` definitie

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   ```

   > Nieuwe definitie `services.yaml`

   ```yaml
   mysql2:
        type: mysql:10.3
        disk: 5120
   ```

1. Werk de relaties in het `.magento.app.yaml` -bestand bij.

   > Oorspronkelijke `.magento.app.yaml` configuratie

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Bijgewerkte `.magento.app.yaml` configuratie

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

**om de dienst te degraderen door de dienst** te creëren:

1. Voeg een de dienstdefinitie aan het `services.yaml` dossier voor uw project met de gedowngraded versiespecificatie toe. Zie _mysql2_ in het volgende voorbeeld:

   > services.yaml

   ```yaml
   mysql:
       type: mysql:10.4
       disk: 5120
   mysql2:
       type: mysql:10.3
       disk: 5120
   ```

1. Wijzig de relatieconfiguratie in het `.magento.app.yaml` dossier om de nieuwe dienst te gebruiken.

   > Oorspronkelijke `.magento.app.yaml` configuratie

   ```yaml
   relationships:
       database: "mysql:mysql"
   ```

   > Nieuwe `.magento.app.yaml` configuratie

   ```yaml
   relationships:
       database: "mysql2:mysql"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.
