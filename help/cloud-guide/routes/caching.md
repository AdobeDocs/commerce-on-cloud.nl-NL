---
title: Caching
description: Leer hoe u caching inschakelt voor uw Adobe Commerce in omgevingen met cloudinfrastructuren.
feature: Cloud, Cache, Routes
exl-id: e73c36d6-9a58-45c0-9220-86074c1f46f0
source-git-commit: a1ed2818cbaf5adf8b673df0ee9b9218e6f700a2
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Caching

U kunt caching in uw het projectmilieu van de wolkeninfrastructuur toelaten. Als u caching uitschakelt, dient Adobe Commerce de bestanden rechtstreeks.

{{route-placeholder}}

## Opslaan in cache instellen

Schakel caching voor uw toepassing in door cachemegels in het `.magento/routes.yaml` -bestand als volgt te configureren:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
        headers: [ "Accept", "Accept-Language", "X-Language-Locale" ]
        cookies: ["*"]
        default_ttl: 60
```

## Route-based caching

Schakel fijnkorrelige caching in door caching-regels voor verschillende routes afzonderlijk in te stellen, zoals in het volgende voorbeeld wordt getoond:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true

http://{default}/path/:
    type: upstream
    upstream: php:php
    cache:
        enabled: false

http://{default}/path/more/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
```

In het voorgaande voorbeeld worden de volgende routes in cache opgeslagen:

- `http://{default}/`
- `http://{default}/path/more/`
- `http://{default}/path/more/etc/`

En de volgende routes zijn **niet** caching:

- `http://{default}/path/`
- `http://{default}/path/etc/`

>[!NOTE]
>
>De regelmatige uitdrukkingen in routes worden **niet** gesteund.

## Cacheduur

De cacheduur wordt bepaald door de headerwaarde van `Cache-Control` response. Als er geen `Cache-Control` header in het antwoord staat, wordt de `default_ttl` -toets gebruikt.

## Cachesleutel

Om te beslissen hoe u een reactie in de cache plaatst, bouwt Adobe Commerce een cachemoets die afhankelijk is van verschillende factoren en slaat het de reactie op die aan deze toets is gekoppeld. Wanneer een verzoek met de zelfde geheim voorgeheugensleutel komt, wordt de reactie opnieuw gebruikt. Zijn doel is gelijkaardig aan de HTTP [`Vary` kopbal &#x200B;](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

Met de parameters `headers` en `cookies` -toetsen kunt u deze cachemoets wijzigen.

De standaardwaarde voor deze toetsen is als volgt:

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## Cachekenmerken

### `enabled`

Wanneer reeks aan `true`, laat het geheime voorgeheugen voor deze route toe. Wanneer ingesteld op `false`, schakelt u de cache voor deze route uit.

### `headers`

Definieert op welke waarden de cachetoets moet afhangen.

Als de `headers` -toets bijvoorbeeld als volgt is:

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

Vervolgens plaatst Adobe Commerce een andere reactie in cache voor elke waarde van de `Accept` HTTP-header.

### `cookies`

De sleutel `cookies` bepaalt op welke waarden de geheim voorgeheugensleutel moet afhangen.

Bijvoorbeeld:

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

De cachemoets is afhankelijk van de waarde van het `value` -cookie in de aanvraag.

Er is een speciaal geval als de `cookies` -toets de `["*"]` -waarde heeft. Deze waarde betekent dat een aanvraag met een cookie de cache overslaat. Dit is de standaardwaarde.

>[!NOTE]
>
>U kunt geen jokertekens gebruiken in de naam van het cookie. Gebruik of een nauwkeurige koekjesnaam of gelijke alle koekjes met een asterisk (`*`). Bijvoorbeeld, `SESS*` of `~SESS` zijn momenteel **niet** geldige waarden.

Cookies hebben de volgende beperkingen:

- Er is een vastgestelde maximum van **50 koekjes** in het systeem. Anders genereert de toepassing een `Unable to send the cookie. Maximum number of cookies would be exceeded` -uitzondering. Om het aantal koekjes aan 200 te verhogen, pas het [&#x200B; MDVA-12304 flard &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/tools/quality-patches-tool/release-notes.html?lang=nl-NL) toe gebruikend het [&#x200B; Hulpmiddel van de Patches van de Kwaliteit &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-learn/tutorials/tools/quality-patch-tool).
- Een maximumkoekjesgrootte is **4096 bytes**. Anders genereert de toepassing een `Unable to send the cookie. Size of '%name' is %size bytes` -uitzondering.

### `default_ttl`

Als de reactie geen `Cache-Control` koptekst heeft, wordt de `default_ttl` -toets gebruikt om de duur van de cache in seconden te definiëren. De standaardwaarde is `0` , wat betekent dat er niets in de cache wordt opgeslagen.
