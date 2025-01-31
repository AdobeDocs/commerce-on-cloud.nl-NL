---
title: Variabelen implementeren
description: Zie de lijst met omgevingsvariabelen die acties in de Adobe Commerce op de implementatiefase van de cloudinfrastructuur besturen.
feature: Cloud, Configuration, Cache, Deploy, SCD, Storage, Search
recommendations: noDisplay, catalog
role: Developer
source-git-commit: 0d9d3d64cd0ad4792824992af354653f61e4388d
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 0%

---

# Variabelen implementeren

Het volgende _stelt_ variabelen controleacties in in de opstellen fase op en kan waarden van de [ Globale variabelen ](variables-global.md) erven en met voeten treden. Voeg deze variabelen in het `deploy` werkgebied van het `.magento.env.yaml` -bestand in:

```yaml
stage:
  deploy:
    DEPLOY_VARIABLE_NAME: value
```

Voor meer informatie over het aanpassen van het bouwstijl en opstellen proces:

- [Implementatieconfiguratie](configure-env-yaml.md)
- [Implementatieproces](../deploy/process.md)

## `CACHE_CONFIGURATION`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Configureer Redis-pagina en standaardcaching. Wanneer u de parameter `cm_cache_backend_redis` instelt, moet u de opties `server` , `port` en `database` opgeven.

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          backend: file
        page_cache:
          backend: file
```

{{merge-options}}

In het volgende voorbeeld worden nieuwe waarden samengevoegd met een bestaande configuratie:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          backend_options:
            database: 10
        page_cache:
          backend_options:
            database: 11
```

Het volgende voorbeeld gebruikt [ preload eigenschap ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/redis-pg-cache.html#redis-preload-feature) zoals die in de _gids van de Configuratie_ wordt bepaald:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      _merge: true
      frontend:
        default:
          id_prefix: '061_'
          backend_options:
            preload_keys:
              - '061_EAV_ENTITY_TYPES:hash'
              - '061_GLOBAL_PLUGIN_LIST:hash'
              - '061_DB_IS_UP_TO_DATE:hash'
              - '061_SYSTEM_DEFAULT:hash'
```

Om een douane [ REDIS_BACKEND ](#redis_backend) model (niet alleen van de lijst van gewenste personen) te gebruiken, plaats de `_custom_redis_backend` optie aan `true` om de correcte bevestiging zoals in het volgende voorbeeld toe te laten:

```yaml
stage:
  deploy:
    CACHE_CONFIGURATION:
      frontend:
        default:
          _custom_redis_backend: true
          backend: '\CustomRedisModel'
```

## `CLEAN_STATIC_FILES`

- **Gebrek** - `true`
- **Versie** - Adobe Commerce 2.1.4 en later

Laat of maakt het schoonmaken [ statische inhoudsdossiers ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html) toe onbruikbaar tijdens de bouwstijl wordt geproduceerd of fase opstelt. Gebruik de standaardwaarde _waar_ in ontwikkeling als beste praktijken.

- **`true`** - Hiermee verwijdert u alle bestaande statische inhoud voordat u de bijgewerkte statische inhoud implementeert.
- **`false`** - De implementatie overschrijft alleen bestaande bestanden met statische inhoud als de gegenereerde inhoud een nieuwere versie bevat.

Als u statische inhoud door een afzonderlijk proces wijzigt, plaats de waarde aan _vals_.

```yaml
stage:
  deploy:
    CLEAN_STATIC_FILES: false
```

Het niet opschonen van statische weergavebestanden vóór de implementatie kan problemen veroorzaken als u updates voor bestaande bestanden implementeert zonder de vorige versies te verwijderen. Wegens [ statische dossierreserve ](https://developer.adobe.com/commerce/frontend-core/guide/caching/#clean-static-files-cache) regels, kunnen de reserveverrichtingen het verkeerde dossier tonen als de folder veelvoudige versies van het zelfde dossier bevat.

## `CRON_CONSUMERS_RUNNER`

- **Gebrek**— `cron_run = false`, `max_messages = 1000`
- **Versie** - Adobe Commerce 2.2.0 en later

Gebruik deze omgevingsvariabele om te bevestigen dat de berichtenrijen na een implementatie worden uitgevoerd.

- `cron_run` - Een Booleaanse waarde die de `consumers_runner` cron-taak in- of uitschakelt (standaard = `false`).
- `max_messages` - Een getal dat het maximum aantal berichten opgeeft dat elke consument moet verwerken voordat deze wordt beëindigd (standaardwaarde = `1000` ). U kunt de waarde instellen op `0` om te voorkomen dat de consument wordt beëindigd.
- `consumers` - Een array van tekenreeksen die aangeven welke consumenten moeten worden uitgevoerd. Een lege serie stelt _alle_ consumenten in werking.

- `multiple_processes` - Een getal dat het aantal processen opgeeft dat voor elke consument moet worden genaaid. Ondersteund in Commerce **2.4.4** of groter.

>[!NOTE]
>
>Als u een lijst met berichtenwachtrij `consumers` wilt retourneren, voert u de opdracht `./bin/magento queue:consumers:list` uit in de externe omgeving.

Voorbeeld van een array die specifiek `consumers` en `multiple_processes` voor elke consument wordt uitgevoerd:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers:
        - example_consumer_1
        - example_consumer_2
-     multiple_processes:
        example_consumer_1: 4
        example_consumer_2: 3
```

Voorbeeld van een lege array die alles `consumers` uitvoert:

```yaml
stage:
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 1000
      consumers: []
```

Standaard overschrijft het implementatieproces alle instellingen in het `env.php` -bestand. Zie [ berichtrijen ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/manage-message-queues.html) in de _Gids van de Configuratie van Commerce_ voor op-gebouw Adobe Commerce beheren.

## `CONSUMERS_WAIT_FOR_MAX_MESSAGES`

- **Gebrek** - `false`
- **Versie** - Adobe Commerce 2.2.0 en later

Configureer hoe `consumers` berichten uit de wachtrij met berichten verwerkt door een van de volgende opties te kiezen:

- `false` - `Consumers` proces beschikbare berichten in de rij, sluit de verbinding van TCP, en beëindigt. `Consumers` wacht niet op extra berichten om de rij in te gaan, zelfs als het aantal verwerkte berichten minder dan de `max_messages` waarde is die in `CRON_CONSUMERS_RUNNER` wordt gespecificeerd plaatsingsvariabele.

- `true` - `Consumers` blijft berichten van de berichtrij verwerken tot het maximum aantal berichten (`max_messages`) wordt gespecificeerd in `CRON_CONSUMERS_RUNNER` opstelt variabele alvorens de verbinding van TCP te sluiten en het consumentenproces te beëindigen. Als de wachtrij leeg is voordat `max_messages` wordt bereikt, wacht de consument tot er meer berichten zijn.

>[!WARNING]
>
>Als u workers gebruikt om `consumers` uit te voeren in plaats van een uitsnijdtaak te gebruiken, stelt u deze variabele in op true.

```yaml
stage:
  deploy:
    CONSUMERS_WAIT_FOR_MAX_MESSAGES: false
```

## `CRYPT_KEY`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

>[!WARNING]
>
>Stel de `CRYPT_KEY` -waarde in via [!DNL Cloud Console] in plaats van het `.magento.env.yaml` -bestand om te voorkomen dat de sleutel in de broncodeopslagplaats voor uw omgeving toegankelijk wordt gemaakt. Zie [ plaats milieu en projectvariabelen ](https://experienceleague.adobe.com/docs/commerce-on-cloud/user-guide/project/overview.html#configure-environment).

Wanneer u het gegevensbestand van één milieu aan een andere zonder installatieproces verplaatst, hebt u de overeenkomstige cryptografische informatie nodig. Adobe Commerce gebruikt de waarde van de coderingssleutel die in de [!DNL Cloud Console] is ingesteld als de `crypt/key` -waarde in het `env.php` -bestand.

## `DATABASE_CONFIGURATION`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Als u een gegevensbestand in het [ verhoudingen bezit ](../application/properties.md#relationships) van het `.magento.app.yaml` dossier bepaalde, kunt u uw gegevensbestandverbindingen voor plaatsing aanpassen.

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_value'
```

{{merge-options}}

In het volgende voorbeeld worden nieuwe waarden samengevoegd met een bestaande configuratie:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      some_config: 'some_new_value'
      _merge: true
```

U kunt ook een tabelvoorvoegsel configureren.

>[!WARNING]
>
>Als u de samenvoegoptie niet gebruikt met het tabelvoorvoegsel, moet u standaardverbindingsinstellingen opgeven of kan de implementatie niet worden gevalideerd.

In het volgende voorbeeld wordt het voorvoegsel van de tabel `ece_` gebruikt met standaardverbindingsinstellingen in plaats van de optie `_merge` :

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          username: user
          host: host
          dbname: magento
          password: password
      table_prefix: 'ece_'
```

Voorbeelduitvoer:

```
MariaDB [main]> SHOW TABLES;
+-------------------------------------+
| Tables_in_main                      |
+-------------------------------------+
| ece_admin_passwords                 |
| ece_admin_system_messages           |
| ece_admin_user                      |
| ece_admin_user_session              |
| ece_adminnotification_inbox         |
| ece_amazon_customer                 |
| ece_authorization_rule              |
| ece_cache                           |
| ece_cache_tag                       |
| ece_captcha_log                     |
...
```

## `ELASTICSUITE_CONFIGURATION`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.2.0 en later

Behoudt aangepaste [!DNL Elastic Suite] service-instellingen tussen implementaties en gebruikt deze in de sectie &#39;system/default/glimlach_elasticsuite_core_base_settings&#39; van de hoofdconfiguratie van [!DNL Elastic Suite] . Als het [!DNL Elastic Suite] composer-pakket is geïnstalleerd, wordt het automatisch geconfigureerd.

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      es_client:
        servers: 'remote-host:9200'
      indices_settings:
        number_of_shards: 1
        number_of_replicas: 0
```

>[!NOTE]
>
>Op een Pro Staging/de cluster van de Productie die drie knopen (of drie de dienstknopen op [ Geschaalde Architectuur ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/scaled-architecture#service-tier) heeft, zou `indices_settings` als volgt moeten worden geplaatst:
>
>```yaml
>           indices_settings:
>               number_of_shards: 3
>               number_of_replicas: 2
>```

{{merge-options}}

In het volgende voorbeeld wordt een nieuwe waarde samengevoegd met de bestaande configuratie:

```yaml
stage:
  deploy:
    ELASTICSUITE_CONFIGURATION:
      indices_settings:
        number_of_shards: 3
        number_of_replicas: 2
      _merge: true
```

**Bekende beperkingen**:

- Als u de zoekmachine wijzigt in een ander type dan `elasticsuite` , treedt een implementatiefout op, vergezeld van een geschikte validatiefout
- Het verwijderen van de dienst van de Elasticsearch veroorzaakt een implementatiefout vergezeld van een aangewezen bevestigingsfout

>[!NOTE]
>
>Voor details bij het gebruiken van of het oplossen van problemen de [!DNL Elastic Suite] stop met Adobe Commerce, zie de [[!DNL Elastic Suite]  documentatie ](https://github.com/Smile-SA/elasticsuite).

## `ENABLE_GOOGLE_ANALYTICS`

- **Gebrek** - `false`
- **Versie** - Adobe Commerce 2.1.4 en later

Laat en maakt Googles Analytics toe onbruikbaar wanneer het opstellen aan het Opvoeren en de milieu&#39;s van de Integratie. Googles Analytics gelden standaard alleen voor de productieomgeving. Stel deze waarde in op `true` als u Googles Analytics wilt inschakelen in de omgevingen voor Staging en Integratie.

- **`true`** - Laat Googles Analytics op het Opvoeren en de milieu&#39;s van de Integratie toe.
- **`false`** - Maakt Googles Analytics op het Opvoeren en de milieu&#39;s van de Integratie onbruikbaar.

Voeg de omgevingsvariabele `ENABLE_GOOGLE_ANALYTICS` toe aan het `deploy` werkgebied in het `.magento.env.yaml` -bestand:

```yaml
stage:
  deploy:
    ENABLE_GOOGLE_ANALYTICS: true
```

>[!NOTE]
>
>Het implementatieproces maakt altijd Googles Analytics in productieomgevingen mogelijk.

## `FORCE_UPDATE_URLS`

- **Gebrek** - `true`
- **Versie** - Adobe Commerce 2.1.4 en later

Bij implementatie in een Pro- of Starter-testomgeving vervangt deze variabele Adobe Commerce-basis-URL&#39;s in de database door de project-URL&#39;s die zijn opgegeven door de variabele [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) . Gebruik dit plaatsen om het standaardgedrag van [ met voeten te treden UPDATE_URLS ](#update_urls) veranderlijk opstelt, die wanneer het opstellen aan het Opvoeren of de milieu&#39;s van de Productie wordt genegeerd.

```yaml
stage:
  deploy:
    FORCE_UPDATE_URLS: true
```

## `LOCK_PROVIDER`

- **Gebrek** - `file`
- **Versie** - Adobe Commerce 2.2.5 en later

De vergrendelingsprovider voorkomt het starten van dubbele snijtaken en afdekgroepen. Gebruik de vergrendelingsprovider van `file` in de productieomgeving. De milieu&#39;s van de aanzet en het Pro integratiemilieu gebruiken niet [ MAGENTO_CLOUD_LOCKS_DIR ](variables-cloud.md) variabele, zodat `ece-tools` automatisch de `db` slotleverancier toepast.

```yaml
stage:
  deploy:
    LOCK_PROVIDER: "db"
```

Zie [ vormen het slot ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/lock-provider.html) in _gids_ installeren.

## `MYSQL_USE_SLAVE_CONNECTION`

- **Gebrek** - `false`
- **Versie** - Adobe Commerce 2.1.4 en later

>[!TIP]
>
>De variabele `MYSQL_USE_SLAVE_CONNECTION` wordt alleen ondersteund in Adobe Commerce op omgevingen met Staging- en Production Pro-clusters met cloudinfrastructuur en niet in Starter-projecten.

Adobe Commerce kan meerdere databases asynchroon lezen. Reeks aan `true` om a _read-only_ verbinding aan het gegevensbestand automatisch te gebruiken om read-only verkeer op een niet hoofdknoop te ontvangen. Deze verbinding verbetert prestaties door lading het in evenwicht brengen, omdat slechts één knoop lees-schrijf verkeer behandelt. Stel in op `false` om een bestaande alleen-lezen-verbindingsarray uit het `env.php` -bestand te verwijderen.

```yaml
stage:
  deploy:
    MYSQL_USE_SLAVE_CONNECTION: true
```

Wanneer de variabele `MYSQL_USE_SLAVE_CONNECTION` is ingesteld op `true` , wordt de parameter `synchronous_replication` standaard ingesteld op `true` in het `env.php` -bestand in Pro Staging and Production-omgevingen. Wanneer `MYSQL_USE_SLAVE_CONNECTION` op `false` wordt geplaatst, wordt de `synchronous_replication` parameter niet gevormd.

## `QUEUE_CONFIGURATION`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Gebruik deze omgevingsvariabele om aangepaste AMQP-service-instellingen tussen implementaties te behouden. Als u bijvoorbeeld liever een bestaande berichtwachtrij gebruikt in plaats van dat u de cloudinfrastructuur gebruikt om deze voor u te maken, gebruikt u de omgevingsvariabele `QUEUE_CONFIGURATION` om deze aan te sluiten op uw site:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      amqp:
        host: test.host
        port: 1234
      amqp2:
        host: test.host2
        port: 12345
      mq:
        host: mq.host
        port: 1234
```

{{merge-options}}

In het volgende voorbeeld worden nieuwe waarden samengevoegd met een bestaande configuratie:

```yaml
stage:
  deploy:
    QUEUE_CONFIGURATION:
      _merge: true
      amqp:
        host: changed1.host
        port: 5672
      amqp2:
        host: changed2.host2
        port: 12345
      mq:
        host: changedmq.host
        port: 1234
```

## `REDIS_BACKEND`

- **Gebrek** - `Cm_Cache_Backend_Redis`
- **Versie** - Adobe Commerce 2.3.0 en later

Specificeert de achtergrondmodelconfiguratie voor het geheime voorgeheugen van Redis.

Adobe Commerce versie 2.3.0 en hoger bevat de volgende back-endmodellen:

- `Cm_Cache_Backend_Redis`
- `\Magento\Framework\Cache\Backend\Redis`
- `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache`

Het voorbeeld voor het instellen van `REDIS_BACKEND`

```yaml
stage:
  deploy:
    REDIS_BACKEND: '\Magento\Framework\Cache\Backend\RemoteSynchronizedCache'
```

>[!NOTE]
>
>Als u `\Magento\Framework\Cache\Backend\RemoteSynchronizedCache` als Redis achterste model specificeert om [ L2 geheime voorgeheugen ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html) toe te laten, `ece-tools` produceert automatisch de geheim voorgeheugenconfiguratie. Zie een voorbeeld [ configuratiedossier ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/level-two-cache.html#configuration-example) in de _Gids van de Configuratie van Adobe Commerce_. Om de geproduceerde geheim voorgeheugenconfiguratie met voeten te treden, gebruik [ CACHE_CONFIGURATION ](#cache_configuration) veranderlijk opstelt.

## `REDIS_USE_SLAVE_CONNECTION`

- **Gebrek** - `false`
- **Versie** - Adobe Commerce 2.1.16 en later

>[!WARNING]
>
>Laat __ deze variabele op a [ geschaalde architectuur ](../architecture/scaled-architecture.md) project niet toe. Dit veroorzaakt verbindingsfouten van Redis. Redis-slaven zijn nog steeds actief, maar worden niet gebruikt voor Redis-lezen. Als alternatief raadt de Adobe aan Adobe Commerce 2.3.5 of hoger te gebruiken, een nieuwe Redis-back-endconfiguratie te implementeren en L2-caching voor Redis te implementeren.

>[!TIP]
>
>De variabele `REDIS_USE_SLAVE_CONNECTION` wordt alleen ondersteund in Adobe Commerce op omgevingen met Staging- en Production Pro-clusters met cloudinfrastructuur en niet in Starter-projecten.

Adobe Commerce kan meerdere Redis-instanties asynchroon lezen. Reeks aan `true` om a _read-only_ verbinding aan een Redis instantie automatisch te gebruiken om read-only verkeer op een niet hoofdknoop te ontvangen. Deze verbinding verbetert prestaties door lading het in evenwicht brengen, omdat slechts één knoop lees-schrijf verkeer behandelt. Stel in op `false` om een bestaande alleen-lezen-verbindingsarray uit het `env.php` -bestand te verwijderen.

```yaml
stage:
  deploy:
    REDIS_USE_SLAVE_CONNECTION: true
```

U moet een Redis-service hebben geconfigureerd in het `.magento.app.yaml` -bestand en in het `services.yaml` -bestand.

[ ECE-Hulpmiddelen versie 2002.0.18 ](../release-notes/cloud-release-archive.md#v2002018) en later gebruik meer fout-verdraagzame montages. Als Adobe Commerce geen gegevens van Redis _slave_ instantie kan lezen, dan leest het gegevens van Redis _meester_ instantie.

De read-only verbinding is niet beschikbaar voor gebruik in het integratiemilieu of als u [`CACHE_CONFIGURATION` variabele ](#cache_configuration) gebruikt.

## `RESOURCE_CONFIGURATION`

- **Gebrek** - niet plaats
- **Versie** - Adobe Commerce 2.1.4 en later

Wijst een middelnaam aan een gegevensbestandverbinding toe. Deze configuratie komt overeen met de sectie `resource` van het `env.php` -bestand.

{{merge-options}}

In het volgende voorbeeld worden nieuwe waarden samengevoegd met een bestaande configuratie:

```yaml
stage:
  deploy:
    RESOURCE_CONFIGURATION:
      _merge: true
      default_setup:
        connection: default
```

## `SCD_COMPRESSION_LEVEL`

- **Gebrek** - `4`
- **Versie** - Adobe Commerce 2.1.4 en later

Specificeert welk [ gzip ](https://www.gnu.org/software/gzip) compressieniveau (`0` aan `9`) te gebruiken wanneer het comprimeren van statische inhoud; `0` maakt compressie onbruikbaar.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_LEVEL: 5
```

## `SCD_COMPRESSION_TIMEOUT`

- **Gebrek** - `600`
- **Versie** - Adobe Commerce 2.1.4 en later

Wanneer de tijd die nodig is om de statische elementen te comprimeren, de time-outlimiet voor compressie overschrijdt, wordt het implementatieproces onderbroken. Stel de maximale uitvoeringstijd, in seconden, in voor de opdracht voor het comprimeren van statische inhoud.

```yaml
stage:
  deploy:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_MATRIX`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

U kunt meerdere landinstellingen per thema configureren. Deze aanpassing versnelt het implementatieproces door het aantal onnodige themabestanden te verminderen. Bijvoorbeeld, kunt u het _magento/backend_ thema in het Engels en een douanethema in andere talen opstellen.

In het volgende voorbeeld wordt het thema `Magento/backend` geïmplementeerd met drie landinstellingen:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Ook, kunt u verkiezen om __ geen thema op te stellen:

```yaml
stage:
  deploy:
    SCD_MATRIX:
      "magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.2.0 en later

Staat u toe om de maximale verwachte uitvoeringstijd voor statische inhoudsplaatsing te verhogen.

Door gebrek, plaatst Adobe Commerce de maximum verwachte uitvoering aan 900 seconden, maar in sommige scenario&#39;s zou u meer tijd kunnen nodig hebben om de statische inhoudsplaatsing voor een project van de Wolk te voltooien.

```yaml
stage:
  deploy:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Gebrek** - `false`
- **Versie** - Adobe Commerce 2.4.2 en later

Stel in de implementatiefase `SCD_NO_PARENT: true` zo in dat het genereren van statische inhoud voor bovenliggende thema&#39;s niet plaatsvindt tijdens de implementatiefase. Dit het plaatsen minimaliseert plaatsingstijd en verhindert plaatsonderbreking die kan voorkomen als de statische inhoud tijdens de plaatsing bouwt ontbreekt. Zie [ Statische inhoudsplaatsing ](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SCD_NO_PARENT: true
```

## `SCD_STRATEGY`

- **Gebrek** - `quick`
- **Versie** - Adobe Commerce 2.2.0 en later

Staat u toe om de [ plaatsingsstrategie ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html) voor statische inhoud aan te passen. Zie [ statische meningsdossiers ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html) opstellen.

Gebruik deze opties _slechts_ als u meer dan één scène hebt:

- `standard` - implementeert alle statische weergavebestanden voor alle pakketten.
- `quick` - (_gebrek_) minimaliseert plaatsingstijd.
- `compact` - bespaart schijfruimte op de server. In Adobe Commerce versie 2.2.4 en lager overschrijft deze instelling de waarde voor `scd_threads` met de waarde `1` .

```yaml
stage:
  deploy:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Gebrek** - automatisch
- **Versie** - Adobe Commerce 2.1.4 en later

Plaatst het aantal draden voor statische inhoudsplaatsing. De standaardwaarde wordt ingesteld op basis van het aantal gedetecteerde CPU-thread en de standaardwaarde 4 wordt niet overschreden. Verhoog het aantal draden versnelt de statische plaatsing van inhoud; het verminderen van het aantal draden vertraagt het. U kunt bijvoorbeeld de waarde van de thread instellen:

```yaml
stage:
  deploy:
    SCD_THREADS: 2
```

Om plaatsingstijd verder te verminderen, gebruik [ het Beheer van de Configuratie ](../store/store-settings.md) met het `scd-dump` bevel om statische plaatsing in de bouwstijlfase te bewegen.

## `SEARCH_CONFIGURATION`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Gebruik deze omgevingsvariabele om aangepaste instellingen voor zoekservices tussen implementaties te behouden. Bijvoorbeeld:

Configuratie Elasticsearch:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_hostname: http://elasticsearch.internal
      elasticsearch_server_port: '9200'
      elasticsearch_index_prefix: magento2
      elasticsearch_server_timeout: '15'
```

OpenSearch-configuratie (voor Commerce 2.4.6 en hoger):

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: opensearch
      opensearch_server_hostname: 'http://opensearch.internal'
      opensearch_server_port: '9200'
      opensearch_index_prefix: 'magento2'
      opensearch_server_timeout: '15'
```

{{merge-options}}

In het volgende voorbeeld wordt een nieuwe waarde samengevoegd met de bestaande configuratie:

```yaml
stage:
  deploy:
    SEARCH_CONFIGURATION:
      engine: elasticsearch
      elasticsearch_server_port: '9200'
      _merge: true
```

## `SESSION_CONFIGURATION`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Configureer de Redis-sessieopslag. Vereist de opties `save`, `redis`, `host`, `port` en `database` voor de opslagvariabele van de sessie. Bijvoorbeeld:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      redis:
        bot_first_lifetime: 100
        bot_lifetime: 10001
        database: 0
        disable_locking: 1
        host: redis.internal
        max_concurrency: 10
        max_lifetime: 10001
        min_lifetime: 100
        port: 6379
      save: redis
```

{{merge-options}}

In het volgende voorbeeld wordt een nieuwe waarde samengevoegd met de bestaande configuratie:

```yaml
stage:
  deploy:
    SESSION_CONFIGURATION:
      _merge: true
      redis:
        max_concurrency: 10
```

## `SKIP_SCD`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Stel in op `true` om de implementatie van statische inhoud tijdens de implementatiefase over te slaan.

Voor de opstellen fase, plaats `SKIP_SCD: true` zodat de statische inhoudsbouwstijl niet tijdens de opstellen fase gebeurt. Dit het plaatsen minimaliseert plaatsingstijd en verhindert plaatsonderbreking die kan voorkomen als de statische inhoud tijdens de plaatsing bouwt ontbreekt. Zie [ Statische inhoudsplaatsing ](../deploy/static-content.md).

```yaml
stage:
  deploy:
    SKIP_SCD: true
```

## `UPDATE_URLS`

- **Gebrek** - `true`
- **Versie** - Adobe Commerce 2.1.4 en later

Vervang bij implementatie Adobe Commerce basis-URL&#39;s in de database door het project-URL&#39;s die zijn opgegeven door de variabele [`MAGENTO_CLOUD_ROUTES`](variables-cloud.md) . Deze configuratie is handig voor lokale ontwikkeling, waarbij basis-URL&#39;s zijn ingesteld voor uw lokale omgeving. Wanneer u implementeert in een Cloud-omgeving, worden de URL&#39;s bijgewerkt zodat u toegang hebt tot uw winkel en beheerder met de project-URL&#39;s.

Gebruik de variabele [`FORCE_UPDATE_URLS`](#force_update_urls) als u URL&#39;s moet bijwerken bij de implementatie naar een Pro- of Starter-staging- en productieomgeving.

```yaml
stage:
  deploy:
    UPDATE_URLS: false
```

## `VERBOSE_COMMANDS`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Laat toe of maak [ Symfony ](https://symfony.com/doc/current/console/verbosity.html) onbruikbaar zuivert breedband niveau voor `bin/magento` bevelen CLI die tijdens de plaatsingsfase worden uitgevoerd.

>[!NOTE]
>
>Om VERBOSE_COMMANDS het plaatsen te gebruiken om het detail in beveloutput voor zowel succesvolle als ontbroken `bin/magento` CLI bevelen te controleren, moet u [ MIN_LOGING_LEVEL ](variables-global.md#minlogginglevel) `debug` plaatsen.

Kies het detailniveau in de logboeken:

- `-v`= normale uitvoer
- `-vv`= uitgebreidere uitvoer
- `-vvv` = uitgebreide uitvoer, ideaal voor foutopsporing

```yaml
stage:
  deploy:
    VERBOSE_COMMANDS: "-vv"
```
