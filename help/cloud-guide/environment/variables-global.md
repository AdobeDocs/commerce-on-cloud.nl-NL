---
title: Algemene variabelen
description: Zie de lijst met omgevingsvariabelen die acties in de Adobe Commerce besturen over het implementatieproces van de cloudinfrastructuur.
feature: Cloud, Configuration, Build, Deploy, Eventing, Logs, SCD
recommendations: noDisplay, catalog
role: Developer
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Algemene variabelen

Globale variabelen beheren acties in elke fase van het [!DNL Commerce] implementatieproces: maken, implementeren en na implementatie. Omdat globale variabelen elke fase beïnvloeden, moet u hen in het `global` stadium van het `.magento.env.yaml` dossier plaatsen:

```yaml
stage:
  global:
    GLOBAL_VARIABLE_NAME: value
```

Voor meer informatie over het aanpassen van het bouwstijl en opstellen proces:

- [Implementatieconfiguratie](configure-env-yaml.md)
- [Implementatieproces](../deploy/process.md)

## `ENABLE_EVENTING`

- **Gebrek** - _niet plaatste_
- **Versie** - Adobe Commerce 2.4.5 en later

Als deze optie is ingesteld op `true` , kunnen gebruikers in de wachtrij met berichten worden uitgevoerd met uitsnijden. Adobe I/O Events for Adobe Commerce gebruikt berichtenrijen om de levering van kritieke gebeurtenissen te versnellen.

Adobe raadt u aan ook de variabele [`CRON_CONSUMERS_RUNNER`](./variables-deploy.md#cron_consumers_runner) toe te voegen aan het `deploy` werkgebied van het `.magento.env.yaml` -bestand met `cron_run` ingesteld op `true` .

In het volgende voorbeeld wordt een volledig geconfigureerde `ENABLE_EVENTING` variabele getoond.

```yaml
stage:
  global:
    ENABLE_EVENTING: true
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      max_messages: 0
      consumers: []
```

## ENABLE_WEBHOOKS

- **Gebrek** - _niet plaatste_
- **Versie** - Adobe Commerce 2.4.4 en later

Als deze optie is ingesteld op `true` , worden Commerce-webhaken ingeschakeld. De webhaak wordt uitgevoerd op een extern eindpunt, zoals een App Builder-runtimeactie of een voorraadbeheersysteem van derden. De [_Gids van Webhooks_ &#x200B;](https://developer.adobe.com/commerce/extensibility/webhooks) beschrijft deze eigenschap in detail.

```yaml
stage:
  global:
    ENABLE_WEBHOOKS: true
```

## `MIN_LOGGING_LEVEL`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Overschrijft het minimale registrerenniveau voor alle outputstromen zonder de code te veranderen, die wanneer het oplossen van problemenproblemen met plaatsing helpt. Bijvoorbeeld, als uw plaatsing ontbreekt, kunt u deze variabele gebruiken om de registrerengranulariteit globaal te verhogen. Zie [&#x200B; niveaus van het Logboek &#x200B;](log-handlers.md#log-levels). De `min_level` -waarde in Logging-handlers overschrijft deze instelling.

```yaml
stage:
  global:
    MIN_LOGGING_LEVEL: debug
```

>[!WARNING]
>
>De instelling voor de variabele `MIN_LOGGING_LEVEL` wijzigt de configuratie op logniveau voor de bestandshandler niet. Deze is standaard ingesteld op `debug` .

## `SCD_ON_DEMAND`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Het genereren van statische inhoud op verzoek van een gebruiker (SCD) inschakelen. Statische inhoud op aanvraag is ideaal voor de ontwikkelings- en testworkflow, omdat hierdoor de implementatietijd afneemt.

Het vooraf laden van de cache met behulp van de [`post_deploy` haak &#x200B;](../application/hooks-property.md) verlaagt de downtime van de site. De opwarming van het geheime voorgeheugen is beschikbaar slechts voor Pro projecten die het Opvoeren en van de Productie milieu&#39;s in [!DNL Cloud Console] bevatten en voor de projecten van de Aanzet. Voeg de omgevingsvariabele `SCD_ON_DEMAND` toe aan het `global` werkgebied in het `.magento.env.yaml` -bestand:

```yaml
stage:
  global:
    SCD_ON_DEMAND: true
```

De variabele `SCD_ON_DEMAND` slaat het SCD in beide fasen over (bouwen en implementeren), wist de mappen `pub/static` en `var/view_preprocessed` en schrijft het volgende naar het `app/etc/env.php` -bestand:

```php?start_inline=1
return array(
   ...
   'static_content_on_demand_in_production' => 1,
   ...
);
```

## `SCD_MAX_EXECUTION_TIME`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.2.0 en later

Staat u toe om de maximale verwachte uitvoeringstijd voor statische inhoudsplaatsing te verhogen.

Door gebrek, plaatst Adobe Commerce de maximum verwachte uitvoering aan 900 seconden, maar in sommige scenario&#39;s zou u meer tijd kunnen nodig hebben om de statische inhoudsplaatsing voor een project van de Wolk te voltooien.

```yaml
stage:
  global:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_NO_PARENT`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.4.2 en later

Stel in op `true` om te voorkomen dat er statische inhoud voor bovenliggende thema&#39;s wordt gegenereerd tijdens de bouw- en implementatiefase. Wanneer deze optie op `true` wordt geplaatst, wordt minder statische inhoud geproduceerd, die uw algemene bouwstijl en plaatsingstijden verbetert.

```yaml
stage:
  global:
    SCD_NO_PARENT: true
```

## `SCD_USE_BALER`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.3.0 en later

[&#x200B; Baler &#x200B;](https://github.com/magento/baler) is een module die uw geproduceerde code van JavaScript aftasten en tot een geoptimaliseerde bundel van JavaScript leidt. Als u de geoptimaliseerde bundel op uw site implementeert, kan het aantal netwerkaanvragen bij het laden van uw site afnemen en de laadtijden van de pagina verbeteren.

Stel dit in op `true` om Baler uit te voeren nadat u statische inhoud hebt geïmplementeerd.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Installeer en configureer de module Baler voordat u deze functie gebruikt. Aangezien Baler zich in alfaversie bevindt, moet u deze optie alleen inschakelen in testomgevingen.

## `SKIP_HTML_MINIFICATION`

- **Gebrek**:
   - `true`—voor `ece-tools` 2002.0.13 en hoger
   - `false`—voor eerdere versies van `ece-tools`
- **Versie** - Adobe Commerce 2.1.4 en later

Hiermee schakelt u het kopiëren van statische weergavebestanden naar de map `<magento_root>/init/` aan het einde van het werkgebied voor het bouwen in of uit. Als deze optie is ingesteld op `true` , worden de bestanden niet gekopieerd en is minificatie van de HTML op aanvraag beschikbaar. Stel deze waarde in op `true` om de downtime te verminderen bij de implementatie in de omgeving voor Staging en Productie.

- **`false`** - Kopieert de `view_preprocessed` map naar de `<magento_root>/init/` -map aan het einde van de constructiefase en herstelt de map in de `<magento_root>/var` -map aan het begin van de implementatiefase.
- **`true`** - laat op bestelling HTML minificatie toe; kopieert _niet_ `<magento_root>var/view_preprocessed` aan de `<magento_root>/init/` folder aan het eind van de bouwstijlfase.

Voeg de omgevingsvariabele `SKIP_HTML_MINIFICATION` toe aan het `global` werkgebied in het `.magento.env.yaml` -bestand:

```yaml
stage:
  global:
    SKIP_HTML_MINIFICATION: true
```

## `X_FRAME_CONFIGURATION`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Gebruik de `X_FRAME_CONFIGURATION` variabele om de [`X-Frame-Options` &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/security/xframe-options.html?lang=nl-NL) kopbalconfiguratie voor uw plaats van Adobe Commerce te veranderen. Deze configuratie bepaalt hoe de browser een pagina in een `<frame>`, `<iframe>` of `<object>` rendert. Gebruik een van de volgende opties:

- `DENY` - De pagina kan niet in een kader worden getoond.
- `SAMEORIGIN`—(De standaard Adobe Commerce-instelling.) De pagina kan alleen worden weergegeven in een kader dat zich op dezelfde oorsprong bevindt als de pagina zelf.

>[!WARNING]
>
>De optie `ALLOW-FROM <uri>` is vervangen omdat deze niet meer wordt ondersteund door browsers die door Adobe Commerce worden ondersteund. Zie [&#x200B; Browser verenigbaarheid &#x200B;](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options#Browser_compatibility).

Voeg de omgevingsvariabele `X_FRAME_CONFIGURATION` toe aan het `global` werkgebied in het `.magento.env.yaml` -bestand:

```yaml
stage:
  global:
    X_FRAME_CONFIGURATION: SAMEORIGIN
```
