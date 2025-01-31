---
title: Variabelen na implementatie
description: Zie de lijst met omgevingsvariabelen die de acties in de Adobe Commerce na de implementatiefase van de cloudinfrastructuur besturen.
feature: Cloud, Configuration, Cache
recommendations: noDisplay, catalog
role: Developer
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Variabelen na implementatie

Het volgende _post-stelt_ variabelen controleacties in de post-opstelt fase op en kan waarden van de [ Globale variabelen ](variables-global.md) erven en met voeten treden. Voeg deze variabelen in het `post-deploy` werkgebied van het `.magento.env.yaml` -bestand in:

```yaml
stage:
  post-deploy:
    POST-DEPLOY_VARIABLE_NAME: value
```

Voor meer informatie over het aanpassen van het bouwstijl en opstellen proces:

- [Implementatieconfiguratie](configure-env-yaml.md)
- [Implementatieproces](../deploy/process.md)

## `TTFB_TESTED_PAGES`

- **Gebrek**— `[]` (een lege serie)
- **Versie** - Adobe Commerce 2.1.4 en later

Vorm _Tijd aan Eerste Byte_ (TTFB) het testen voor gespecificeerde pagina&#39;s om uw plaatsprestaties te testen. Geef een absolute padverwijzing op, of een URL met protocol en host, voor elke pagina waarvoor de test nodig is.

```yaml
stage:
  post-deploy:
    TTFB_TESTED_PAGES:
       - "index.php"
       - "index.php/customer/account/create"
       - "https://example.com/catalog/some-category"
```

Nadat u de pagina&#39;s specificeert om uw veranderingen te testen en vast te leggen, de _Tijd aan Eerste de testlooppas van de Byte_ tijdens de post-opstellen fase en posten resultaten voor elke weg aan het wolkenlogboek:

```
[2019-06-20 20:42:22] INFO: TTFB test result: 0.313s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/customer/account/create","status":200}
[2019-06-20 20:42:22] INFO: TTFB test result: 0.408s {"url":"https://staging-tkyicst-xkmwgjkwmwfuk.us-4.magentosite.cloud/checkout/cart","status":200}
```

Voor omgeleide wegen, meldt het logboek de weg van het omleidingsdoel in plaats van die in de omgevingsvariabele wordt gevormd. Als u een ongeldig pad opgeeft, wordt in het logbestand een waarschuwingsbericht weergegeven.

## `WARM_UP_CONCURRENCY`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Geef de limiet op voor gelijktijdige verzoeken om tijdens opwarmbewerkingen in het cachegeheugen te verzenden om de serverlading te verminderen. Deze waarde beperkt het aantal parallelle verbindingen en is nuttig voor omgevingsconfiguraties waarbij de `WARM_UP_PAGES` post-implementatievariabele meerdere pagina&#39;s opgeeft voor het vooraf laden van de cache.

```yaml
stage:
  post-deploy:
    WARM_UP_CONCURRENCY: 4
```

## `WARM_UP_PAGES`

- **Gebrek**— `index.php`
- **Versie** - Adobe Commerce 2.1.4 en later

Pas de lijst aan met pagina&#39;s die worden gebruikt om de cache in het `post_deploy` -werkgebied vooraf te laden. U moet de post-opstellen haak vormen. Zie [ haken sectie ](../application/hooks-property.md) van het `.magento.app.yaml` dossier.

- **enige pagina&#39;s** - specificeer één enkele pagina om aan het geheime voorgeheugen toe te voegen. U hoeft de standaard basis-URL niet aan te geven. In het volgende voorbeeld wordt de pagina `BASE_URL/index.php` in cache geplaatst:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - "index.php"
  ```

- **veelvoudige domeinen** - lijst veelvoudige URLs. In het volgende voorbeeld worden pagina&#39;s van twee domeinen in cache opgeslagen:

  ```yaml
  stage:
    post-deploy:
      WARM_UP_PAGES:
        - 'http://example1.com/test'
        - 'http://example2.com/test'
  ```

- **veelvoudige pagina&#39;s** - gebruik het volgende formaat om veelvoudige pagina&#39;s volgens een specifiek regulier uitdrukkingspatroon in het voorgeheugen onder te brengen:

  ```
  <entity_type>:<pattern|url|product_sku>:<store_id|store_code>
  ```

   - `entity_type`: Mogelijke varianten `category` , `cms-page` , `product` , `store-page`
   - `pattern|url|product_sku`: gebruik een `regexp` patroon of een exacte overeenkomst `url` om de URL&#39;s te filteren, of gebruik een asterisk (\*) voor alle pagina&#39;s. ProductSKU gebruiken voor het eenheidstype `product`
   - `store_id|store_code`: Gebruik de id of code van de winkel of een sterretje (\*) voor alle winkels. U kunt meerdere winkel-id&#39;s of -codes doorgeven, gescheiden door `|`

  In het volgende voorbeeld worden op basis van deze criteria in cache geplaatst voor `category` - en `cms-page` -eenheidstypen:
   - alle categoriepagina&#39;s voor opslag met id `1`
   - alle categoriepagina&#39;s voor winkels met code `store1` en `store2`
   - categoriepagina `cars` voor opslaan met code `store_en`
   - cms-pagina `contact` voor alle winkels
   - cms-pagina `contact` voor winkels met id `1` en `2`
   - elke categoriepagina die `car_` bevat en eindigt met `html` voor opslag met ID 2
   - elke categoriepagina die `tires_` bevat voor opslag met code `store_gb`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "category:*:1"
           - "category:*:store1|store2"
           - "category:cars:store_en"
           - "cms-page:contact:*"
           - "cms-page:contact:1|2"
           - "category:|car_.*?\\.html$|:2"
           - "category:|tires_.*|:store_gb"
     ```

  In het volgende voorbeeld wordt het eenheidstype `product` op basis van deze criteria in cache geplaatst:
   - alle producten voor alle opslag (programmatically beperkt tot 100 per opslag om prestatieskwesties te vermijden)
   - alle producten voor opslag `store1`
   - producten met `sku1` voor alle winkels
   - producten met `sku1` voor winkels met code `store1` en `store2`
   - producten met `sku1` , `sku2` en `sku3` voor winkels met code `store1` en `store2`

     ```yaml
     stage:
       post-deploy:
         WARM_UP_PAGES:
           - "product:*:*"
           - "product:*:store1"
           - "product:sku1:*"
           - "product:sku1:store1|store2"
           - "product:sku1|sku2|sku3:store1|store2"
     ```

  In het volgende voorbeeld wordt het eenheidstype `store-page` op basis van deze criteria in cache geplaatst:
   - pagina `/contact-us` voor alle winkels
   - pagina `/contact-us` voor opslag met id `1`
   - pagina `/contact-us` voor winkels met code `code1` en `code2`

  ```yaml
        stage:
          post-deploy:
            WARM_UP_PAGES:
              - "store-page:/contact-us:*"
              - "store-page:/contact-us:1"
              - "store-page:/contact-us:code1|code2"
  ```
