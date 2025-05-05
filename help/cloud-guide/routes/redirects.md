---
title: Omleiding
description: Leer hoe u omleidingsregels voor uw Adobe Commerce beheert voor een cloudinfragment.
feature: Cloud, Routes
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Omleiding

Het beheren van omleidingsregels is een algemene vereiste voor webtoepassingen, vooral wanneer u inkomende koppelingen die in de loop der tijd zijn gewijzigd of verwijderd, niet wilt verliezen.

In het volgende voorbeeld ziet u hoe u omleidingsregels voor uw Adobe Commerce kunt beheren voor projecten met cloudinfrastructuur met behulp van het configuratiebestand `routes.yaml` . Als de omleidingsmethodes in dit onderwerp worden besproken niet voor u werken, kunt u caching kopballen gebruiken om het zelfde ding te doen.

{{route-placeholder}}

## Updates voor Pro-omgevingen

{{pro-self-service-warning}}

>[!WARNING]
>
>Voor Adobe Commerce op projecten met cloudinfrastructuur kan het configureren van een groot aantal niet-regex omleidingen en herschrijvingen in het `routes.yaml` -bestand prestatieproblemen veroorzaken. Als het `routes.yaml` -bestand 32 kB of groter is, kunt u de niet-regex omleiden en snel herschrijven. Zie [ de niet-regex van de Offload richt aan Fastly in plaats van Nginx (routes) ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/offload-non-regex-redirects-to-fastly-instead-of-nginx-routes.html?lang=nl-NL) in het _Centrum van de Hulp van Adobe Commerce_.

## Hele-routeomleidingen

Met behulp van omleidingen via volledige route kunt u eenvoudige routes definiëren met behulp van het `routes.yaml` -bestand. U kunt bijvoorbeeld als volgt van een ex-domein naar een `www` -subdomein omleiden:

```yaml
http://{default}/:
    type: redirect
    to: http://www.{default}/
```

## Gedeeltelijke-routeomleidingen

In het bestand `.magento/routes.yaml` kunt u op basis van patroonovereenkomst gedeeltelijke omleidingsregels toevoegen aan bestaande routes:

```yaml
http://{default}/:
    redirects:
        expires: 1d
        paths:
          "/from": { to: "http://example.com/" }
          "/regexp/(.*)/matching": { to: "http://example.com/$1", regexp: true }
```

Gedeeltelijke omleidingen werken met elk type route, inclusief routes die rechtstreeks door de toepassing worden bediend.

Er zijn twee toetsen beschikbaar onder `redirects` :

- **verloopt** - Facultatief, specificeert de hoeveelheid tijd om redirect in browser in cache te plaatsen. Voorbeelden van geldige waarden zijn `3600s` , `1d` , `2w` en `3m` .

- **wegen** - één of meerdere zeer belangrijk-waardeparen die de configuratie voor gedeeltelijk-route omleiden regels specificeren.

  Voor elke omleidingsregel is de sleutel een expressie om aanvraagpaden voor omleiding te filteren. De waarde is een object dat de doelbestemming voor de omleiding en opties voor de verwerking van de omleiding aangeeft.

  Het object value heeft de volgende eigenschappen:

  | Eigenschap | Beschrijving |
  | ---------- | ----------- |
  | `to` | Vereist, een gedeeltelijk absolute weg, URL met protocol en gastheer, of een patroon dat de doelbestemming voor de omleidingsregel specificeert. |
  | `regexp` | Optioneel is de standaardwaarde `false` . Geeft aan of de padsleutel moet worden geïnterpreteerd als een reguliere PCRE-expressie. |
  | `prefix` | Hiermee geeft u aan of de omleiding van toepassing is op zowel het pad als alle onderliggende paden, of alleen op het pad zelf. Wordt standaard ingesteld op `true` . Deze waarde wordt niet ondersteund als `regexp` `true` is. |
  | `append_suffix` | Hiermee bepaalt u of het achtervoegsel wordt overgedragen met de omleiding. Wordt standaard ingesteld op `true` . Deze waarde wordt niet ondersteund als de `regexp` -toets `true` of* is als de `prefix` -toets `false` is. |
  | `code` | Geeft de HTTP-statuscode op. Geldige statuscodes zijn [`301` (Geldig blijvend) ](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2), [`302` ](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3), [`307` ](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8), en [`308` ](https://www.rfc-editor.org/rfc/rfc7238). Wordt standaard ingesteld op `302` . |
  | `expires` | Optioneel: hiermee geeft u aan hoeveel tijd u de omleiding in de browser in de cache wilt plaatsen. De standaardwaarde is de `expires` -waarde die rechtstreeks onder de `redirects` -toets wordt gedefinieerd, maar op dit niveau kunt u de vervaldatum van de cache voor afzonderlijke gedeeltelijke omleidingen perfectioneren. |

## Voorbeelden van gedeeltelijke-routeomleidingen

De volgende voorbeelden laten zien hoe u omleidingen via gedeeltelijke route kunt opgeven in het `routes.yaml` -bestand met behulp van verschillende `paths` -configuratieopties.

### Standaardovereenkomend expressiepatroon

Gebruik het volgende formaat om verzoeken te vormen die van de omleiding op een regelmatige uitdrukking worden gebaseerd.

```yaml
http://{default}/:
    type: upstream
    redirects:
      paths:
        "/regexp/(.*)/match": { to: "http://example.com/$1", regexp: true }
```

Met deze configuratiefilters worden paden aangevraagd op basis van een reguliere expressie en overeenkomstige aanvragen omgeleid naar `https://example.com` . Een aanvraag om `https://example.com/regexp/a/b/c/match` om te leiden naar `https://example.com/a/b/c` .

### Overeenkomende patroon voorvoegsel

Gebruik de volgende indeling om aanvragen voor paden die met een opgegeven voorvoegselpatroon beginnen, om te leiden.

```yaml
http://{default}/:
    type: upstream
    redirects:
      paths:
        "/from": { to: "https://{default}/to", prefix: true }
```

Deze configuratie werkt als volgt:

- Hiermee worden aanvragen die overeenkomen met het patroon `/from` doorgestuurd naar het pad `http://{default}/to` .

- Hiermee worden aanvragen omgeleid die overeenkomen met het patroon `/from/another/path` naar `https://{default}/to/another/path` .

- Als u de eigenschap `prefix` wijzigt in `false` , wordt bij aanvragen die overeenkomen met het patroon `/from` een omleiding geactiveerd, maar aanvragen die overeenkomen met het patroon `/from/another/path` niet.

### Overeenkomende patroon achtervoegsel

Gebruik het volgende formaat om omleidingsverzoeken te vormen die het wegachtervoegsel van het verzoek aan de doelbestemming toevoegen:

```yaml
http://{default}/:
    type: upstream
    redirects:
      paths: "/from": { to: "https://{default}/to", append_suffix: false }
```

Deze configuratie werkt als volgt:

- Hiermee worden aanvragen die overeenkomen met het patroon `/from/path/suffix` doorgestuurd naar het pad `https://{default}/to` .

- Als u de eigenschap `append_suffix` wijzigt in `true` , worden aanvragen die overeenkomen met `/from/path/suffix` doorgestuurd naar het pad `https://{default}/to/path/suffix` .

### Padspecifieke cacheconfiguratie

Gebruik de volgende notatie om de tijd aan te passen om een omleiding van een specifiek pad in de cache op te slaan:

```yaml
http://{default}/:
    type: upstream
    redirects:
    expires: 1d
      paths:
        "/from": { to: "https://example.com/" }
        "/here": { to: "https://example.com/there", expires: "2w" }
```

Deze configuratie werkt als volgt:

- Omleidingen vanaf het eerste pad (`/from`) worden gedurende één dag in cache geplaatst.

- Omleidingen vanaf het tweede pad (`/here`) worden twee weken in cache geplaatst.
