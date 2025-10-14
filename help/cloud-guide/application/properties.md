---
title: Eigenschappen
description: Gebruik de bezitslijst als verwijzing wanneer configuratie de  [!DNL Commerce]  toepassing voor bouwt en aan de wolkeninfrastructuur opstelt.
feature: Cloud, Configuration, Build, Deploy, Roles/Permissions, Storage
exl-id: 32bd1f64-43d6-48a3-84b7-bea22f125bb0
source-git-commit: 1cea1cdebf3aba2a1b43f305a61ca6b55e3b9d08
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Eigenschappen voor toepassingsconfiguratie

Het bestand `.magento.app.yaml` gebruikt eigenschappen voor het beheer van de omgevingsondersteuning voor de toepassing [!DNL Commerce] .

| Naam | Beschrijving | Standaard | Vereist |
| ------ | --------------------------------- | ------- | -------- |
| [`access`](#access) | Gebruikersrollen aanpassen | — | Nee |
| [`crons`](crons-property.md) | Specificaties bijwerken en uitsnijdtaken plannen | — | Nee |
| [`dependencies`](#dependencies) | Aanvullende afhankelijkheden inschakelen | `php:composer/composer: '2.2.4'` | Nee |
| [`disk`](#disk) | De grootte van de vaste schijf definiëren | `5120` | Ja |
| [`firewall`](firewall-property.md) | (Alleen Starter) Uitgaand verkeer besturen | — | Nee |
| [`hooks`](hooks-property.md) | Pas shellbevelen voor de bouw, opstellen, en post-opstellen fasen aan | — | Nee |
| [`mounts`](#mounts) | Paden instellen | Paden:<ul><li>`"var": "shared:files/var"`</li><li>`"app/etc": "shared:files/etc"`</li><li>`"pub/media": "shared:files/media"`</li><li>`"pub/static": "shared:files/static"`</li></ul> | Nee |
| [`name`](#name) | De toepassingsnaam definiëren | `mymagento` | Ja |
| [`relationships`](#relationships) | Kaartservices | Services:<ul><li>`database: "mysql:mysql"`</li><li>`redis: "redis:redis"`</li><li>`opensearch: "opensearch:opensearch"`</li></ul> | Nee |
| [`runtime`](#runtime) | De runtime-eigenschap omvat extensies die door de [!DNL Commerce] -toepassing worden vereist. | Extensies:<ul><li>`xsl`</li><li>`newrelic`</li><li>`sodium`</li></ul> | Ja |
| [`type`](#type-and-build) | De basiscontainerafbeelding instellen | `php:8.3` | Ja |
| [`variables`](variables-property.md) | Een omgevingsvariabele toepassen voor een specifieke Commerce-versie | — | Nee |
| [`web`](web-property.md) | Externe verzoeken afhandelen | — | Ja |
| [`workers`](workers-property.md) | Externe verzoeken afhandelen | — | Ja, als de webeigenschap niet wordt gebruikt |

{style="table-layout:auto"}

## `name`

De eigenschap `name` biedt de toepassingsnaam die in het [`routes.yaml`](../routes/routes-yaml.md) -bestand wordt gebruikt om de HTTP-upstream te definiëren (standaard `mymagento:http` ). Als de waarde van `name` bijvoorbeeld `app` is, moet u `app:http` in het upstreamveld gebruiken.

>[!WARNING]
>
>Wijzig de naam van de toepassing niet nadat deze is geïmplementeerd. Dit leidt tot gegevensverlies.

## `type` en `build`

De eigenschappen `type` en `build` bevatten informatie over de basiscontainerafbeelding voor het samenstellen en uitvoeren van het project.

De ondersteunde `type` taal is PHP. Geef de PHP-versie als volgt op:

```yaml
type: php:<version>
```

De eigenschap `build` bepaalt wat er standaard gebeurt bij het bouwen van het project. In `flavor` wordt een standaardset bouwtaken opgegeven die moet worden uitgevoerd. In het volgende voorbeeld wordt de standaardconfiguratie voor `type` en `build` from `magento-cloud/.magento.app.yaml` getoond:

```yaml
# The toolstack used to build the application.
type: php:8.4
build:
    flavor: none

dependencies:
    php:
        composer/composer: '2.7.2'
```

### Composer 2 installeren en gebruiken

De eigenschap `build: flavor:` wordt niet gebruikt voor Composer 2.x. Daarom moet u Composer handmatig installeren tijdens de constructiefase. Als u Composer 2.x wilt installeren en gebruiken in uw Starter- en Pro-projecten, moet u drie wijzigingen aanbrengen in de `.magento.app.yaml` -configuratie:

1. Verwijder `composer` als `build: flavor:` en voeg `none` toe. Door deze wijziging wordt voorkomen dat Cloud de standaardversie 1.x van Composer gebruikt voor het uitvoeren van ontwikkeltaken.
1. Voeg `composer/composer: '^2.0'` toe als een `php` -afhankelijkheid voor het installeren van Composer 2.x.
1. Voeg `composer` bouwtaken aan een `build` haak toe om bouwstijltaken in werking te stellen gebruikend Composer 2.x.

Gebruik de volgende configuratiefragmenten in uw eigen `.magento.app.yaml` configuratie:

```yaml
# 1. Change flavor to none.
build:
    flavor: none

# 2. Add Composer ^2.0 as a php dependency.
dependencies:
    php:
        composer/composer: '^2.0'

# 3. Add a build hook to run the build tasks using Composer 2.x.
hooks:
    build: |
        set -e
        composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
```

Zie [&#x200B; Vereiste pakketten &#x200B;](../development/overview.md#required-packages) voor meer informatie over Composer.

## `dependencies`

Specificeer gebiedsdelen die uw toepassing tijdens het bouwstijlproces zou kunnen vereisen.

Adobe Commerce ondersteunt afhankelijkheden voor de volgende talen:

- PHP
- Ruby
- Node.js

Deze afhankelijkheden zijn onafhankelijk van de uiteindelijke afhankelijkheden van uw toepassing en zijn beschikbaar in de `PATH` , tijdens het ontwikkelproces en in de runtimeomgeving van uw toepassing.

U kunt die gebiedsdelen als volgt specificeren:

```yaml
ruby:
   sass: "~3.4"
nodejs:
   grunt-cli: "~0.3"
```

## `runtime`

Gebruik deze optie om de PHP-configuratie tijdens runtime te wijzigen, bijvoorbeeld om extensies in te schakelen. De volgende extensies zijn vereist:

```yaml
runtime:
    extensions:
        - xsl
        - newrelic
        - sodium
```

Zie [&#x200B; PHP montages &#x200B;](php-settings.md) voor details over het toelaten van uitbreidingen.

## `disk`

Definieert de persistente schijfgrootte van de toepassing in MB.

```yaml
disk: 5120
```

De minimale aanbevolen schijfgrootte is 256 MB. Als u de fout `UserError: Error building the project: Disk size may not be smaller than 128MB`ziet, vergroot u de grootte naar 256 MB.

>[!NOTE]
>
>Voor Pro het Opvoeren en van de Productie milieu&#39;s, moet u [&#x200B; een kaartje van de Steun van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voorleggen om de `mounts` en `disk` configuratie voor uw toepassing bij te werken. Wanneer u het ticket verzendt, geeft u de vereiste configuratiewijzigingen aan en neemt u een bijgewerkte versie van het `.magento.app.yaml` -bestand op.
>
>Het is niet mogelijk om de schijfopslag in Staging of Productie tijdelijk te verhogen; dit proces is niet omkeerbaar.

## `relationships`

Definieert de servicetoewijzing in de toepassing.

De relatie `name` is beschikbaar voor de toepassing in de omgevingsvariabele `MAGENTO_CLOUD_RELATIONSHIPS` . De `<service-name>:<endpoint-name>` -relatie wordt toegewezen aan de naam en typewaarden die zijn gedefinieerd in het `.magento/services.yaml` -bestand.

```yaml
relationships:
    <name>: "<service-name>:<endpoint-name>"
```

Hieronder ziet u een voorbeeld van de standaardrelaties:

```yaml
relationships:
    database: "mysql:mysql"
    redis: "redis:redis"
    opensearch: "opensearch:opensearch"
    rabbitmq: "rabbitmq:rabbitmq"
```

Zie [&#128279;](../services/services-yaml.md) de Diensten van 0&rbrace; &lbrace;voor een volledige lijst van momenteel gesteunde de diensttypes en eindpunten.

## `mounts`

Een object waarvan de sleutels paden zijn die relatief zijn ten opzichte van de hoofdmap van de toepassing. De koppeling is een beschrijfbaar gebied op de schijf voor bestanden. Hieronder volgt een standaardlijst met toewijzingen die in het `magento.app.yaml` -bestand worden geconfigureerd met de syntaxis van `volume_id[/subpath]` :

```yaml
 # The mounts that will be performed when the package is deployed.
mounts:
    "var": "shared:files/var"
    "app/etc": "shared:files/etc"
    "pub/media": "shared:files/media"
    "pub/static": "shared:files/static"
```

De indeling voor het toevoegen van de hoeveelheid aan deze lijst is als volgt:

```bash
"/public/sites/default/files": "shared:files/files"
```

- `shared` - Deel een volume tussen uw toepassingen binnen een omgeving.
- `disk` - Hiermee definieert u de grootte die beschikbaar is voor het gedeelde volume.

>[!NOTE]
>
>Voor Pro het Opvoeren en van de Productie milieu&#39;s, moet u [&#x200B; een kaartje van de Steun van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voorleggen om de `mounts` en `disk` configuratie voor uw toepassing bij te werken. Wanneer u het ticket verzendt, geeft u de vereiste configuratiewijzigingen aan en neemt u een bijgewerkte versie van het `.magento.app.yaml` -bestand op.

U kunt het koppelingsweb toegankelijk maken door het toe te voegen aan het [`web`](web-property.md) -blok met locaties.

>[!WARNING]
>
>Wijzig niet het `subpath` -gedeelte van de montagenaam als uw site gegevens bevat. Deze waarde is de unieke id voor het `files` -gebied. Als u deze naam wijzigt, gaan alle sitegegevens verloren die op de oude locatie zijn opgeslagen.

## `access`

De eigenschap `access` geeft een minimale gebruikersrolniveau aan dat SSH-toegang tot de omgevingen wordt toegestaan. De beschikbare gebruikersrollen zijn:

- `admin` - kan montages veranderen en acties in het milieu uitvoeren; heeft _contribuant_ en _kijker_ rechten.
- `contributor` - kan code aan dit milieu duwen en zich van het milieu vertakken; heeft _kijker_ rechten.
- `viewer` - Kan alleen de omgeving weergeven.

De standaardgebruikersrol is `contributor`, die de toegang van SSH van gebruikers met slechts _kijker_ rechten beperkt. U kunt de gebruikersrol in `viewer` veranderen om de toegang van SSH voor gebruikers met slechts _kijker_ rechten toe te staan:

```yaml
access:
    ssh: viewer
```
