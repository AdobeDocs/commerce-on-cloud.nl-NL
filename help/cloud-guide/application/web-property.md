---
title: Web, eigenschap
description: Zie voorbeelden op hoe te om het Webbezit in het  [!DNL Commerce]  dossier van de toepassingsconfiguratie te vormen.
feature: Cloud, Configuration
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Web, eigenschap

Het `web` bezit bepaalt hoe uw toepassing aan het Web (in HTTP) wordt blootgesteld, bepaalt hoe de Webtoepassing inhoud dient, en controleert hoe de toepassingscontainer aan inkomende verzoeken antwoordt door regels in elke plaats _blok_ te plaatsen. Een blok vertegenwoordigt een absolute weg die met een voorwaartse schuine streep (`/`) leidt.

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

U kunt de configuratie van `locations` verfijnen met de volgende sleutelwaarden voor elk `locations` -blok:

| Kenmerk | Beschrijving |
| :--- | :--- |
| `allow` | Serveer bestanden die niet overeenkomen met de regels. Standaardwaarde = `true` |
| `expires` | Stel het aantal seconden in dat u inhoud in de browser in de cache wilt plaatsen. Met deze toets worden de headers `cache-control` en `expires` ingeschakeld voor statische inhoud. Als deze waarde niet is ingesteld, worden de aanwijzing `expires` en de resulterende kopteksten niet opgenomen wanneer statische inhoudsbestanden worden aangeboden. Een negatieve waarde van 1 (`-1`) resulteert in geen caching en is de standaardwaarde. U kunt de tijdwaarde uitgedrukt in de volgende eenheden: `ms` (milliseconden), `s` (seconden), `m` (minuten), `h` (uren), `d` (dagen), `w` (weken), `M` (maanden, 30d) of `y` (jaren, 365d) |
| `headers` | Stel aangepaste koppen, zoals `X-Frame-Options` , in voor statische inhoud die vanaf deze locatie wordt aangeboden. |
| `index` | Geef een lijst weer van de statische bestanden die aan uw toepassing worden geleverd, zoals het `index.html` -bestand. Deze sleutel verwacht een inzameling. Dit werkt alleen als toegang tot het bestand of de bestanden wordt &quot;toegestaan&quot; door de sleutel `allow` of `rules` voor deze locatie. |
| `rules` | Geef overschrijvingen voor een locatie op. Gebruik een reguliere expressie die overeenkomt met een aanvraag. Als een inkomend verzoek de regel aanpast, dan wordt de regelmatige behandeling van het verzoek met voeten getreden door de sleutels die in de regel worden gebruikt. |
| `passthru` | Stel de URL in die wordt gebruikt voor het geval dat een statisch bestand of PHP-bestand niet wordt gevonden. Doorgaans is deze URL de voorste controller voor uw toepassingen, zoals `/index.php` of `/app.php` . |
| `root` | Stel het pad in ten opzichte van de hoofdmap van de toepassing die op het web wordt weergegeven. De openbare map (locatie &quot;/&quot;) voor een Cloud-project is standaard ingesteld op &quot;pub&quot;. |
| `scripts` | Het laden van scripts op deze locatie toestaan. Stel de waarde in op `true` als u scripts wilt toestaan. |

De standaardconfiguratie staat het volgende toe:

- Vanaf het hoofdpad (`/`) zijn alleen web en media toegankelijk
- Vanuit de paden `~/pub/static` en `~/pub/media` kan elk bestand worden geopend

Het volgende voorbeeld toont de standaardconfiguratie in het `.magento.app.yaml` dossier voor een reeks web-Toegankelijke plaatsen verbonden aan een ingang in het [`mounts` bezit &#x200B;](properties.md#mounts):

```yaml
 # The configuration of app when it is exposed to the web.
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
            root: "pub"
            # The front-controller script to send non-static requests to.
            passthru: "/index.php"
            index:
                - index.php
            expires: -1
            scripts: true
            allow: false
            rules:
                \.(css|js|map|hbs|gif|jpe?g|png|tiff|wbmp|ico|jng|bmp|svgz|midi?|mp?ga|mp2|mp3|m4a|ra|weba|3gpp?|mp4|mpe?g|mpe|ogv|mov|webm|flv|mng|asx|asf|wmv|avi|ogx|swf|jar|ttf|eot|woff|otf|html?)$:
                    allow: true
                ^/sitemap(.*)\.xml$:
                    passthru: "/media/sitemap$1.xml"
        "/media":
            root: "pub/media"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/get.php"
        "/static":
            root: "pub/static"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/front-static.php"
            rules:
                ^/static/version\d+/(?<resource>.*)$:
                    passthru: "/static/$resource"
```

>[!NOTE]
>
>Dit voorbeeld toont de standaardWebconfiguratie voor een project van de Wolk dat wordt gevormd om één enkel domein te steunen. Voor een project dat ondersteuning voor meerdere websites of winkels vereist, moet de `web` -configuratie zo zijn ingesteld dat gedeelde domeinen worden ondersteund. Zie [&#x200B; plaatsen voor gedeelde domeinen &#x200B;](../store/multiple-sites.md#configure-locations-for-shared-domains) vormen.
