---
title: Hooks, eigenschap
description: Zie voorbeelden op hoe te om het hooks bezit in het  [!DNL Commerce]  dossier van de toepassingsconfiguratie te vormen.
feature: Cloud, Configuration, Build, Deploy
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Hooks, eigenschap

Gebruik de sectie `hooks` om shell-opdrachten uit te voeren tijdens de fasen build, implementatie en post-implementatie:

- **`build`** - voer bevelen _uit alvorens_ uw toepassing verpakken. De diensten, zoals het gegevensbestand of Redis, zijn niet beschikbaar aangezien de toepassing nog niet is opgesteld. Voeg douanebevelen _vóór_ het gebrek `php ./vendor/bin/ece-tools` bevel toe zodat de douane-geproduceerde inhoud aan de plaatsingsfase verdergaat.

- **`deploy`** - voer bevelen _na_ het verpakken uit en het opstellen van uw toepassing. U kunt tot andere diensten op dit punt toegang hebben. Aangezien het standaard `php ./vendor/bin/ece-tools` bevel de `app/etc` folder aan de correcte plaats kopieert, moet u douanebevelen _toevoegen na_ het opstellen bevel om douanebevelen van het ontbreken te verhinderen.

- **`post_deploy`** - voer bevelen _uit na_ het opstellen van uw toepassing en _nadat_ de container begint goedkeurend verbindingen. Met de `post_deploy` -haak wordt de cache gewist en wordt de cache voorgeladen (verdraaiingen). U kunt de lijst van pagina&#39;s aanpassen gebruikend de `WARM_UP_PAGES` variabele in [ post-opstelt stadium ](../environment/variables-post-deploy.md). Hoewel niet vereist, werkt dit in combinatie met de omgevingsvariabele `SCD_ON_DEMAND` .

In het volgende voorbeeld wordt de standaardconfiguratie in het `.magento.app.yaml` -bestand getoond. Voeg CLI bevelen onder `build` toe, `deploy`, of `post_deploy` secties _vóór_ het `ece-tools` bevel:

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        composer install
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    # We run deploy hook after your application has been deployed and started.
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    # We run post deploy hook to clean and warm the cache. Available with ECE-Tools 2002.0.10.
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

Bovendien kunt u de constructiefase verder aanpassen met de opdrachten `generate` en `transfer` om aanvullende handelingen uit te voeren wanneer u specifiek code maakt of bestanden verplaatst.

```yaml
hooks:
    # We run build hooks before your application has been packaged.
    build: |
        set -e
        php ./vendor/bin/ece-tools build:generate
        # php /path/to/your/script
        php ./vendor/bin/ece-tools build:transfer
```

- `set -e` - de haken mislukken op het eerste ontbroken bevel, in plaats van het definitieve ontbroken bevel.
- `build:generate` - past flarden toe, bevestigt configuratie, produceert DI, en produceert statische inhoud als SCD voor bouwstijlfase wordt toegelaten.
- `build:transfer` - hiermee worden gegenereerde code en statische inhoud overgedragen naar de uiteindelijke bestemming.

De opdrachten worden uitgevoerd vanuit de toepassingsmap (`/app`). U kunt de opdracht `cd` gebruiken om de map te wijzigen. De haken mislukken als het definitieve bevel daarin ontbreekt. Om ervoor te zorgen dat deze mislukken bij de eerste mislukte opdracht, voegt u `set -e` toe aan het begin van de haak.

**om de dossiers van de Klasse te compileren gebruikend grot**:

```yaml
dependencies:
    ruby:
        sass: "3.4.7"
    nodejs:
        grunt-cli: "~0.1.13"

hooks:
    build: |
        cd public/profiles/project_name/themes/custom/theme_name
        npm install
        grunt
        cd
        php ./vendor/bin/ece-tools build
```

Compileer de dossiers van de Klasse gebruikend `grunt` vóór statische inhoudsplaatsing, die tijdens de bouwstijl gebeurt. Plaats de opdracht `grunt` vóór de opdracht `build` .

{{scenarios}}
