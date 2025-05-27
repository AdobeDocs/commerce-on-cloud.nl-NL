---
title: Valkey-service instellen
description: Leer hoe u Valkey instelt en optimaliseert als back-end cacheoplossing voor Adobe Commerce op Cloud Infrastructure.
feature: Cloud, Cache, Services
exl-id: f8933e0d-a308-4c75-8547-cb26ab6df947
source-git-commit: 242582ea61d0d93725a7f43f2ca834db9e1a7c29
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Valkey-service instellen

[ Valkey ](https://valkey.io) is een facultatieve, achterste geheim voorgeheugenoplossing die `Zend Framework Zend_Cache_Backend_File` vervangt, die Adobe Commerce door gebrek gebruikt.

Zie [ Valkey ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/valkey/config-valkey.html?lang=nl-NL){target="_blank"} in de _gids van de Configuratie_ vormen.

{{service-instruction}}

**om Valkey** toe te laten:

1. Voeg de vereiste naam en het vereiste type aan het `.magento/services.yaml` dossier toe.

   ```yaml
   cache:
       type: valkey:<version>
   ```

   Als u uw eigen Valkey-configuratie wilt opgeven, voegt u een `core_config` -sleutel toe in het `.magento/services.yaml` -bestand:

   ```yaml
   cache:
       type: valkey:8.0
   ```

1. Configureer de relaties in het `.magento.app.yaml` -bestand.

   ```yaml
   relationships:
       valkey: "cache:valkey"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml && git commit -m "Enable valkey service" && git push origin <branch-name>
   ```

1. [ verifieer de de dienstverhoudingen ](services-yaml.md#service-relationships).

{{service-change-tip}}

## Het gebruiken van Valkey CLI

Ervan uitgaande dat de Valkey-relatie `valkey` heet, kunt u deze openen met het gereedschap `valkey-cli` .

1. Gebruik SSH om verbinding te maken met de integratieomgeving met Valkey geïnstalleerd en geconfigureerd.

1. Open een tunnel SSH aan een gastheer.

   ```bash
   valkey-cli -h valkey.internal
   ```

## Geïnstalleerde Valkey-versie ophalen

Gebruik de volgende opdracht om de Valkey-versie op een integratieomgeving te installeren:

```bash
valkey-cli -h valkey.internal info | grep version
```

Reactie:

```
valkey_version:8.0.1
gcc_version:12.2.0
```

### Valkey op Pro-fasering en -productie

Gebruik de opdracht `valkey-server` om de Valkey-versie op een testomgeving of productieomgeving te installeren:

```bash
valkey-server -v
```

```bash
Valkey server v=8.0.1 ...
```

Gebruik het volgende bevel om de Valkey-configuratie te installeren op een Pro Staging- of Productieomgeving:

```bash
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
```

Reactie:

```json
"valkey" : [
    {
        "cluster" : "project-master-abc0003",
        "epoch" : 0,
        "fragment" : null,
        "host" : "valkeycache.internal",
        "host_mapped" : false,
        "hostname" : "oblahblahblahblahe.cache.service._.magentosite.cloud",
        "instance_ips" : [
        "123.456.789.012"
        ],
        "ip" : "123.456.789.012",
        "password" : null,
        "path" : null,
        "port" : 6379,
        "public" : false,
        "query" : {},
        "rel" : "valkey",
        "scheme" : "valkey",
        "service" : "cache",
        "type" : "valkey:8.0",
        "username" : null
    }
]
```
