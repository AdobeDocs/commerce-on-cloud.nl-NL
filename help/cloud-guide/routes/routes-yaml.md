---
title: Verbindingen vormen
description: Leer hoe u de routes definieert voor binnenkomende HTTPS-aanvragen voor de Adobe Commerce in omgevingen met cloudinfrastructuren.
feature: Cloud, Configuration, Routes
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Verbindingen vormen

Het bestand `routes.yaml` in de map `.magento/routes.yaml` definieert routes voor uw Adobe Commerce op omgevingen voor integratie, staging en productie van cloudinfrastructuur. Routes bepalen hoe de toepassing binnenkomende HTTP- en HTTPS-aanvragen verwerkt.

Het standaard `routes.yaml` dossier specificeert de routesjablonen voor de verwerking van HTTP- verzoeken als HTTPS op projecten die één enkel standaarddomein en op projecten hebben die voor veelvoudige domeinen worden gevormd:

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"
"http://{all}/":
    type: upstream
    upstream: "mymagento:http"
```

Gebruik `magento-cloud` CLI om een lijst van de gevormde routes te bekijken:

```bash
magento-cloud environment:routes

+-------------------+----------+---------------+
| Route             | Type     | To            |
+-------------------+----------+---------------+
| http://{default}/ | upstream | mymagento     |
+-------------------+----------+---------------+
```

## Configuratie-updates voor Pro-omgevingen

{{pro-self-service-warning}}

## Route templates

Het bestand `routes.yaml` is een lijst met sjabloonroutes en hun configuraties. U kunt de volgende placeholders in routesjablonen gebruiken:

- De tijdelijke aanduiding `{default}` vertegenwoordigt de gekwalificeerde domeinnaam die als standaard voor het project is geconfigureerd.

  Bijvoorbeeld een project met het standaarddomein `example.com` en de volgende routesjablonen:

  ```text
  https://www.{default}/
  https://{default}/blog
  ```

  Deze sjablonen verwijzen naar de volgende URL&#39;s in een productieomgeving:

  ```text
  https://www.example.com/
  https://example.com/blog
  ```

- De tijdelijke aanduiding `{all}` vertegenwoordigt alle domeinnamen die voor het project zijn geconfigureerd.

  Bijvoorbeeld een project met `example.com` - en `example1.com` -domeinen met de volgende routesjablonen:

  ```text
  https://www.{all}/
  
  https://{all}/blog
  ```

  Deze malplaatjes lossen aan de volgende routes voor alle domeinen in het project op:

  ```text
  https://www.example.com/
  
  https://www.example1.com/
  
  https://example.com/blog
  
  https://example1.com/blog
  ```

  De tijdelijke aanduiding `{all}` is handig voor projecten die zijn geconfigureerd voor meerdere domeinen. In een niet-productietak, wordt `{all}` vervangen met project identiteitskaart en milieu identiteitskaart voor elk domein.

  Als voor een project geen domeinen zijn geconfigureerd, wat gebruikelijk is tijdens de ontwikkeling, gedraagt de tijdelijke aanduiding `{all}` zich op dezelfde manier als de tijdelijke aanduiding van `{default}` .

Adobe Commerce genereert ook routes voor elke actieve integratieomgeving. Voor integratieomgevingen wordt de tijdelijke aanduiding `{default}` vervangen door de volgende domeinnaam:

```text
[branch]-[per-environment-random-string]-[project-id].[region].magentosite.cloud
```

De `refactorcss` -vertakking voor het `mswy7hzcuhcjw` -project dat wordt gehost in de `us` -cluster heeft bijvoorbeeld het volgende domein:

```text
https://refactorcss-oy3m2pq-mswy7hzcuhcjw.us.magentosite.cloud/
```

>[!NOTE]
>
>Als uw project van de Wolk veelvoudige opslag steunt, volg de instructies van de routeconfiguratie voor [ veelvoudige websites of opslag ](../store/multiple-sites.md).

### Sluitslash

De definities van de route bevatten een het slepen schuine streep om op een omslag of een folder te wijzen; nochtans, kan de zelfde inhoud met of zonder een het slepen schuine streep worden gediend. De volgende URLs lost het zelfde op maar kan als _worden geïnterpreteerd twee verschillende_ URLs:

```text
https://www.example.com/blog/

https://www.example.com/blog
```

>[!TIP]
>
>Het is beste praktijken om een het slepen schuine streep voor folders te gebruiken, maar welke methode u kiest, is het belangrijk om **verenigbaar** te blijven vermijden producerend twee plaatsen.

## Routeprotocollen

Alle omgevingen ondersteunen automatisch HTTP en HTTPS.

- Als de configuratie alleen de HTTP-route opgeeft, worden automatisch HTTPS-routes gemaakt, zodat de site vanuit zowel HTTP als HTTPS kan worden bediend zonder dat omleidingen nodig zijn.

  Bijvoorbeeld, een project met het standaarddomein `example.com` en het volgende routesjabloon:

  ```text
  http://{default}/
  ```

  Deze sjabloon verhelpt naar de volgende URL&#39;s:

  ```text
  http://example.com/
  
  https://example.com/
  ```

- Als de configuratie alleen de HTTPS-route opgeeft, leiden alle HTTP-aanvragen om naar HTTPS.

  Bijvoorbeeld, een project met het standaarddomein `example.com` met het volgende routesjabloon:

  ```text
  https://{default}/
  ```

  Deze sjabloon wordt omgezet naar de volgende URL:

  ```text
  https://example.com/
  ```

  Het verwerkt ook de volgende omleiding:

  `http://example.com/` ==> `https://example.com/`

Geef alle pagina&#39;s weer via TLS. Voor deze configuratie, moet u redirects voor al unencrypted verzoek aan het equivalent TLS vormen gebruikend één van de volgende methodes:

- Wijzig het protocol in HTTPS in het `routes.yaml` -bestand.

  ```yaml
  "https://{default}/":
      type: upstream
      upstream: "mymagento:http"
  "https://{all}/":
      type: upstream
      upstream: "mymagento:http"
  ```

- Voor het Opvoeren en de milieu&#39;s van de Productie, laat [ TLS op Fastly ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/redirect-http-to-https-for-all-pages-on-cloud-force-tls.html?lang=nl-NL) optie van Admin UI toe. Wanneer u deze optie gebruikt, handelt u snel de omleiding naar HTTPS af, zodat u de configuratie `routes.yaml` niet hoeft bij te werken.

## Routopties

Vorm elke route afzonderlijk gebruikend de volgende eigenschappen:

| Eigenschap | Beschrijving |
| ---------------- | ----------- |
| `type: upstream` | Dient een toepassing uit. De eigenschap `upstream` heeft ook een eigenschap die de naam van de toepassing opgeeft (zoals gedefinieerd in `.magento.app.yaml` ) gevolgd door het eindpunt `:http` . |
| `type: redirect` | Omleidt aan een andere route. Deze wordt gevolgd door de eigenschap `to` , die een HTTP-omleiding is naar een andere route die door de sjabloon ervan wordt aangegeven. |
| `cache:` | Controles [ caching voor de route ](caching.md). |
| `redirects:` | De controles [ richten regels ](redirects.md) opnieuw. |
| `ssi:` | Controles toelatend van [ Zijde van de Server omvat ](server-side-includes.md). |

## Eenvoudige routes

In de volgende voorbeelden leidt de routeconfiguratie het apex-domein en het `www` -subdomein naar de `mymagento` -toepassing. Deze route leidt HTTPS- verzoeken niet om.

**Voorbeeld 1:**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: redirect
    to: "http://{default}/"
```

In dit voorbeeld, volgt het verzoek die deze regels verplettert:

- De server reageert rechtstreeks op aanvragen met het volgende URL-patroon:

  ```text
  http://example.com/path
  ```

- De server geeft a _301 opnieuw richt_ voor verzoeken met het volgende patroon URL uit:

  ```text
  http://www.example.com/mypath
  ```

  Deze verzoeken worden bijvoorbeeld omgeleid naar het ex-domein:

  ```text
  http://example.com/mypath
  ```

In het volgende voorbeeld, richt de routeconfiguratie geen URLs van het www domein aan het apex domein. In plaats daarvan, worden de verzoeken gediend van zowel www als apex domein.

**Voorbeeld 2:**

```yaml
"http://{default}/":
    type: upstream
    upstream: "mymagento:http"

"http://www.{default}/":
    type: upstream
    upstream: "mymagento:http"
```

## Jokerroutes

Adobe Commerce op cloudinfrastructuur ondersteunt jokertekenroutes, zodat u meerdere subdomeinen aan dezelfde toepassing kunt toewijzen. Dit werkt voor omleiding en stroomopwaartse routes. U voegt een sterretje (\*) toe aan de route. Met de volgende routes naar bijvoorbeeld dezelfde toepassing:

- `*.example.com`
- `www.example.com`
- `blog.example.com`
- `us.example.com`

Dit werkt als een &#39;catch-all&#39;-domein in een live omgeving.

### Het verpletteren van een niet in kaart gebracht domein

U kunt aan een systeem leiden dat niet aan een domein gebruikend een punt (`.`) in kaart wordt gebracht om subdomain te scheiden.

**Voorbeeld:**

Een project met een vertakking `add-theme` leidt naar de volgende URL:

```text
http://add-theme-projectID.us.magento.com/
```

Als u het volgende routesjabloon definieert:

```text
http://www.{default}/
```

De route lost aan volgende URL op:

```text
http://www.add-theme-projectID.us.magento.com/
```

U kunt elk subdomein invoegen voordat de punt en de route worden omgezet.

**Voorbeeld:**

Bepaal het volgende routesjabloon:

```text
http://*.{default}/
```

Deze sjabloon verhelpt beide volgende URL&#39;s:

```text
http://foo.add-theme-projectID.us.magentosite.cloud/
http://bar.add-theme-projectID.us.magentosite.cloud/
```

U kunt het routepatroon voor niet in kaart gebrachte domeinen bekijken door een verbinding van SSH aan het milieu te vestigen, en `magento-cloud` CLI te gebruiken om van de routes een lijst te maken:

```bash
vendor/bin/ece-tools env:config:show routes

Magento Cloud Routes:
+------------------------------------------+--------------------------------------------------------------+
| Route configuration                      | Value                                                        |
+------------------------------------------+--------------------------------------------------------------+
| http://www.add-theme-projectID.us.magento.com/:                                                         |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https:/{default}/                                            |
+------------------------------------------+--------------------------------------------------------------+
| https://*.add-theme-projectID.us.magentosite.cloud/:                                                    |
+------------------------------------------+--------------------------------------------------------------+
| primary                                  | false                                                        |
| id                                       | null                                                         |
| attributes                               |                                                              |
| type                                     | upstream                                                     |
| to                                       | mymagento                                                    |
| original_url                             | https://*.{default}/                                         |
+------------------------------------------+--------------------------------------------------------------+
```

## Omleiding en caching

Zoals besproken in meer detail in [ richt ](redirects.md) opnieuw, kunt u complexe redirection regels, zoals _gedeeltelijke herleidingen_ beheren, en regels voor route-gebaseerd [ caching ](caching.md) specificeren:

```yaml
https://www.{default}/:
    type: redirect
    to: https://{default}/
https://{default}/:
    cache:
        cookies: [""]
        default_ttl: 0
        enabled: true
        headers:
            - Accept
            - Accept-Language
    ssi:
        enabled: false
    type: upstream
    upstream: mymagento:http
```
