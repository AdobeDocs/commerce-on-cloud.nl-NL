---
title: Redis-service instellen
description: Leer hoe u Redis kunt instellen en optimaliseren als back-end cacheoplossing voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Cache, Services
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Redis-service instellen

[ Redis ](https://redis.io) is een facultatieve, achterste geheim voorgeheugenoplossing die Zend Framework Zend_Cache_Backend_File vervangt, die Adobe Commerce door gebrek gebruikt.

Zie [ vormen Redis ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html?lang=nl-NL) in de _gids van de Configuratie_.

{{service-instruction}}

**Redis** toelaten:

1. Voeg de vereiste naam en het vereiste type aan het `.magento/services.yaml` dossier toe.

   ```yaml
   myredis:
       type: redis:<version>
   ```

   Als u uw eigen Redis-configuratie wilt opgeven, voegt u een `core_config` -toets toe in het `.magento/services.yaml` -bestand:

   ```yaml
   cache:
       type: redis:<version>
   ```

1. Configureer de relaties in het `.magento.app.yaml` -bestand.

   ```yaml
   runtime:
       extensions:
           - redis
   
   relationships:
       redis: "redis:redis"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable redis service" && git push origin <branch-name>
   ```

1. [ verifieer de de dienstverhoudingen ](services-yaml.md#service-relationships).

{{service-change-tip}}

## Het gebruik van Redis CLI

Ervan uitgaande dat de Redis-relatie de naam `redis` heeft, kunt u deze openen met het gereedschap `redis-cli` .

1. Gebruik SSH om verbinding te maken met de integratieomgeving met Redis geïnstalleerd en geconfigureerd.

1. Open een tunnel SSH aan een gastheer.

   ```bash
   redis-cli -h redis.internal
   ```

## De geïnstalleerde versie van Redis ophalen

Gebruik de volgende opdracht om de Redis-versie op een integratieomgeving te installeren:

```bash
redis-cli -h redis.internal info | grep version
```

Monsterrespons:

```
redis_version:7.0.5
gcc_version:8.3.0
```

### Redis op Pro-ophaling en -productie

Als u de versie Redis wilt installeren in een omgeving voor Staging of Productie, gebruikt u de opdracht `redis-server` :

```bash
redis-server -v
```

```
Redis server v=7.0.5 ...
```

Gebruik het volgende bevel om de configuratie te krijgen Redis die op een Pro het Staging of milieu van de Productie wordt geïnstalleerd:

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Monsterrespons:

```json
"redis" : [
    {
        "cluster" : "project-master-123abc4",
        "fragment" : null,
        "host" : "redis.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.redis.service._.magentosite.cloud",
        "ip" : "169.254.10.10",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "redis",
        "scheme" : "redis",
        "service" : "redis",
        "type" : "redis:7.0.5",
        "username" : null
    }
]
```

## Problemen met Redis oplossen

Raadpleeg de volgende Adobe Commerce Support-artikelen voor hulp bij het oplossen van problemen met Redis:

- [ herstelt de login van Admin van de Uitgiftevertraging of controle ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html?lang=nl-NL)
- [ Uitgebreide Redis geheim voorgeheugenimplementatie Adobe Commerce 2.3.5+ ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/planning/redis-service-configuration.html?lang=nl-NL)
- [ Beheerde alarm op Adobe Commerce: Redis alarm van de geheugenwaarschuwing ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html?lang=nl-NL)
- [ Beheerd alarm op Adobe Commerce: Redis geheugen kritieke alarm ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html?lang=nl-NL)
