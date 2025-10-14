---
title: Omgeving configureren
description: Leer hoe u ontwikkelings- en implementatieacties in alle Commerce kunt configureren in omgevingen met cloudinfrastructuren, waaronder Pro Staging en Production, met behulp van omgevingsvariabelen.
feature: Cloud, Build, Configuration, Deploy, SCD
role: Developer
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Omgevingsvariabelen voor implementatie configureren

Het bestand van `.magento.env.yaml` gebruikt omgevingsvariabelen om het beheer van het maken en implementeren van acties in al uw omgevingen te centraliseren, inclusief Pro Staging en Production. Om unieke acties in elke milieu te vormen, moet u dit dossier in elke milieu wijzigen.

>[!TIP]
>
>YAML-bestanden zijn hoofdlettergevoelig en staan geen tabs toe. Wees voorzichtig met het gebruik van consistente inspringing in het `.magento.env.yaml` -bestand, anders werkt de configuratie mogelijk niet naar behoren. De voorbeelden in de documentatie en in het steekproefdossier gebruiken _twee-ruimte_ inspringing. Gebruik de [&#x200B; knoop-hulpmiddelen bevestigen bevel &#x200B;](#validate-configuration-file) om uw configuratie te controleren.

## Bestandsstructuur

Het bestand `.magento.env.yaml` bevat twee secties: `stage` en `log` . De `stage` sectie controleert acties die tijdens de fasen van het [&#x200B; de plaatsingsproces van de Wolk &#x200B;](../deploy/process.md) voorkomen.

- `stage` - Gebruik de sectie Werkgebied om bepaalde acties voor de volgende stadia van plaatsing te bepalen:
   - `global` - Beheert acties in zowel de bouw, opstelling, als post-opstelt fasen. U kunt deze montages in bouwstijl met voeten treden, opstelt, en post-opstelt secties.
   - `build` - Beheert acties in de bouwstijlfase slechts. Als u geen montages in deze sectie specificeert, gebruikt de bouwstijlfase montages van de globale sectie.
   - `deploy` - Beheert acties in de opstellen slechts fase. Als u geen montages in deze sectie specificeert, de plaatsingsfase gebruikt montages van de globale sectie.
   - `post-deploy` - de acties van Controles _na_ het opstellen van uw toepassing en _nadat_ de container begint goedkeurend verbindingen.
- `log` - gebruik de logboeksectie om [&#x200B; berichten &#x200B;](set-up-notifications.md), met inbegrip van berichttypes en niveau van detail te vormen.
   - `slack` - Vorm een bericht om naar een Slack te verzenden allebei.
   - `email` - Configureer een e-mail om deze naar een of meer e-mailontvangers te verzenden.
   - [&#x200B; logboekmanagers &#x200B;](log-handlers.md) - vorm hardware en softwaretoepassingsberichten die naar een verre registrerenserver worden verzonden.

### Omgevingsvariabelen

Het `ece-tools` pakket plaatst waarden in het `env.php` dossier dat op waarden van [&#x200B; variabelen van de Wolk &#x200B;](variables-cloud.md) wordt gebaseerd, variabelen die in [!DNL Cloud Console] worden geplaatst, en het `.magento.env.yaml` configuratiedossier. De omgevingsvariabelen in het `.magento.env.yaml` -bestand passen de Cloud-omgeving aan door de bestaande Commerce-configuratie te overschrijven. Als een standaardwaarde `Not Set` is, dan neemt het `ece-tools` pakket **NO** actie en gebruikt het [!DNL Commerce] gebrek of de waarde van de configuratie MAGENTO_CLOUD_RELATIONSHIPS. Als de standaardwaarde is ingesteld, wordt die standaardwaarde ingesteld door het `ece-tools` -pakket.

De volgende onderwerpen bevatten gedetailleerde definities, zoals of een standaardwaarde is ingesteld of niet, van alle variabelen die u in het `.magento.env.yaml` -bestand kunt gebruiken:

- [&#x200B; Globaal &#x200B;](variables-global.md) - variabelen controleacties in elke fase: bouw, stel, en post-opstellen op
- [&#x200B; bouwt &#x200B;](variables-build.md)-variabelen controle bouwt acties
- [&#x200B; stelt &#x200B;](variables-deploy.md) op:stellen-variabelen de controle acties op
- [&#x200B; post-opstellen &#x200B;](variables-post-deploy.md) - variabelen controleacties na opstellen

### Configuratiebestand maken van CLI

U kunt een `.magento.env.yaml` -configuratiebestand voor een Cloud-omgeving genereren met behulp van de volgende `ece-tools` -opdrachten.

>Maakt een configuratiebestand

```bash
php ./vendor/bin/ece-tools cloud:config:create `<configuration-json>`
```

>Waarden bijwerken in het configuratiebestand

```bash
php ./vendor/bin/ece-tools cloud:config:update `<configuration-json>`
```

Voor beide opdrachten is één argument vereist: een array in JSON-indeling die een waarde opgeeft voor ten minste één variabele voor build, implementatie of implementatie na implementatie. Met de volgende opdracht stelt u bijvoorbeeld waarden in voor de variabelen `SCD_THREADS` en `CLEAN_STATIC_FILES` :

```bash
php vendor/bin/ece-tools cloud:config:create '{"stage":{"build":{"SCD_THREADS":5}, "deploy":{"CLEAN_STATIC_FILES":false}}}'
```

En maakt een `.magento.env.yaml` -bestand met de volgende instellingen:

```yaml
stage:
  build:
    SCD_THREADS: 5
  deploy:
    CLEAN_STATIC_FILES: false
```

U kunt de opdracht `cloud:config:update` gebruiken om het nieuwe bestand bij te werken. Met de volgende opdracht wijzigt u bijvoorbeeld de waarde `SCD_THREADS` en voegt u de configuratie `SCD_COMPRESSION_TIMEOUT` toe:

```bash
php vendor/bin/ece-tools cloud:config:update '{"stage":{"build":{"SCD_THREADS":3, "SCD_COMPRESSION_TIMEOUT":1000}}}'
```

Het bijgewerkte bestand bevat de volgende configuratie:

```yaml
stage:
  build:
    SCD_THREADS: 3
    SCD_COMPRESSION_TIMEOUT: 1000
  deploy:
    CLEAN_STATIC_FILES: false
```

### Configuratiebestand valideren

Gebruik de volgende opdracht `ece-tools` om het configuratiebestand van `.magento.env.yaml` te valideren voordat u wijzigingen aanbrengt in de externe cloud-omgeving.

```bash
php ./vendor/bin/ece-tools cloud:config:validate
```

De volgende voorbeeldreactie bevat een lijst met te corrigeren items:

```
Environment configuration is not valid. Correct the following items in your .magento.env.yaml file:
The SCD_THREADS variable contains an invalid value of type string. Use the following type: integer.
The SCD_STRATEGY variable contains an invalid value fast. Use one of the available value options: compact, quick, standard.
The NOT_EXIST_OPTION variable is not allowed in configuration.
```

## PHP-constanten

U kunt PHP-constanten gebruiken in `.magento.env.yaml` -bestandsdefinities in plaats van hard-coderingswaarden. In het volgende voorbeeld wordt de `driver_options` gedefinieerd met behulp van een PHP-constante:

```yaml
stage:
  deploy:
    DATABASE_CONFIGURATION:
      connection:
        default:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
        indexer:
          driver_options:
            !php/const:\PDO::MYSQL_ATTR_LOCAL_INFILE : 1
      _merge: true
```

>[!WARNING]
>
>Constante parsering werkt niet wanneer u een pakketversie van `symfony/yaml` gebruikt die ouder is dan 3.2.

## Foutafhandeling

Wanneer een fout optreedt als gevolg van een onverwachte waarde in het configuratiebestand van `.magento.env.yaml` , ontvangt u een foutbericht. In het volgende foutbericht wordt bijvoorbeeld een lijst met voorgestelde wijzigingen in elk item met een onverwachte waarde weergegeven, waarbij soms geldige opties worden geboden:

```
- Environment configuration is not valid. Please correct .magento.env.yaml file with next suggestions:
  Item CRON_CONSUMERS_RUNNER is not supposed to be in stage build. Please move it to one of possible stages: global, deploy
  Item SKIP_SCD has unexpected type string. Please use one of next types: boolean
  Item VERBOSE_COMMANDS has unexpected type boolean. Please use one of next types: string
  Item SKIP_HTML_MINIFICATION has unexpected type string. Please use one of next types: boolean
  Item CRON_CONSUMERS_RUNNER has unexpected type boolean. Please use one of next types: array
  Item VAR_WARM_UP_PAGES is not allowed in configuration.
  Item WARM_UP_PAGES has unexpected type string. Please use one of next types: array
```

Breng de gewenste correcties aan, wijs deze toe en duw op de wijzigingen. Als u geen foutbericht ontvangt, slagen de wijzigingen in het configuratiebestand voor de validatie.

## Optimalisatie van configuratiebeheer

Als u het Beheer van de Configuratie na het dumpen van de configuraties hebt toegelaten, zou u de variabelen SCD_* van opstellen aan het bouwstijlstadium moeten bewegen. Zie [&#x200B; Statische strategieën van de inhoudsplaatsing &#x200B;](../deploy/static-content.md).

>Voor configuratiebeheer:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
    REDIS_USE_SLAVE_CONNECTION: 1
```

>Na het toelaten van het Beheer van de Configuratie, verplaats de variabelen SCD_* naar het bouwstijlstadium:

```yaml
  deploy:
    CRON_CONSUMERS_RUNNER:
      cron_run: true
      consumers: []
    REDIS_USE_SLAVE_CONNECTION: 1
  build:
    SCD_STRATEGY: compact
    SCD_MATRIX:
      ...
```
