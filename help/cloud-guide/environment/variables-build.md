---
title: Variabelen samenstellen
description: Zie de lijst met omgevingsvariabelen die acties in de Adobe Commerce besturen over de bouwfase van de cloudinfrastructuur.
feature: Cloud, Configuration, Build, SCD, Upgrade
recommendations: noDisplay, catalog
role: Developer
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Variabelen samenstellen

Het volgende _bouwt_ variabelen controleacties in de bouwstijlfase en kan waarden van de [&#x200B; Globale variabelen &#x200B;](variables-global.md) erven en met voeten treden. Voeg deze variabelen in het `build` werkgebied van het `.magento.env.yaml` -bestand in:

```yaml
stage:
  build:
    BUILD_VARIABLE_NAME: value
```

Voor meer informatie over het aanpassen van het bouwstijl en opstellen proces:

- [Implementatieconfiguratie](configure-env-yaml.md)
- [Implementatieproces](../deploy/process.md)

De volgende variabelen zijn verwijderd uit v2.2:

- `skip_di_clearing`
- `skip_di_compilation`

## `ERROR_REPORT_DIR_NESTING_LEVEL`

- **Gebrek** - `1`
- **Versie** - Adobe Commerce 2.1.4 en later

Stel het nestniveau van directory&#39;s in voor het opslaan van foutrapportbestanden om te voorkomen dat de rapportmap wordt gevuld met tienduizenden bestanden, wat het moeilijk kan maken om de gegevens te beheren en te bekijken. Deze instelling is standaard ingesteld op `1` . Doorgaans hoeft u de standaardwaarde alleen te wijzigen als u problemen hebt met het beheren van bestanden met foutrapporten in de map `<magento_root>/var/report/` .

```yaml
stage:
  build:
    ERROR_REPORT_DIR_NESTING_LEVEL: 2
```

## `QUALITY_PATCHES`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Geef een lijst met Adobe Commerce-kwaliteitspatches op die u tijdens de implementatie wilt toepassen.

```yaml
stage:
  build:
    QUALITY_PATCHES: [ ]
```

In het volgende voorbeeld worden drie patches opgegeven die tijdens de implementatie moeten worden toegepast.

```yaml
stage:
  build:
    QUALITY_PATCHES:
      - MC-31387
      - MDVA-4567
      - MC-456345
```

Zie [&#x200B; flarden &#x200B;](../development/apply-patches.md) toepassen.

## `SCD_COMPRESSION_LEVEL`

- **Gebrek** - `6`
- **Versie** - Adobe Commerce 2.1.4 en later

Specificeert welk [&#x200B; gzip &#x200B;](https://www.gnu.org/software/gzip) compressieniveau (`0` aan `9`) te gebruiken wanneer het comprimeren van statische inhoud; `0` maakt compressie onbruikbaar.

```yaml
stage:
  build:
    SCD_COMPRESSION_LEVEL: 4
```

## `SCD_COMPRESSION_TIMEOUT`

- **Gebrek** - `600`
- **Versie** - Adobe Commerce 2.1.4 en later

Wanneer de tijd die nodig is om de statische elementen te comprimeren, de time-outlimiet voor compressie overschrijdt, wordt het implementatieproces onderbroken. Stel de maximale uitvoeringstijd, in seconden, in voor de opdracht voor het comprimeren van statische inhoud.

```yaml
stage:
  build:
    SCD_COMPRESSION_TIMEOUT: 800
```

## `SCD_NO_PARENT`

- **Gebrek** - `false`
- **Versie** - Adobe Commerce 2.4.2 en later

Stel in op `true` om te voorkomen dat tijdens de constructiefase statische inhoud voor bovenliggende thema&#39;s wordt gegenereerd.

Stel `SCD_NO_PARENT: false` in tijdens de constructiefase, zodat het genereren van statische inhoud voor de bovenliggende thema&#39;s geen invloed heeft op de implementatie van de site of onnodige downtime veroorzaakt. Zie [&#x200B; Statische inhoudsplaatsing &#x200B;](../deploy/static-content.md).

```yaml
stage:
  build:
    SCD_NO_PARENT: false
```

## `SCD_MATRIX`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

U kunt meerdere landinstellingen per thema configureren. Deze aanpassing helpt het bouwstijlproces te versnellen door het aantal onnodige themadossiers te verminderen. Bijvoorbeeld, kunt u het _magento/backend_ thema in het Engels en een douanethema in andere talen bouwen.

In het volgende voorbeeld wordt het thema `Magento/backend` gemaakt met drie landinstellingen:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

In het volgende voorbeeld worden drie thema&#39;s met drie landinstellingen samengesteld:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/blank":
        language:
          - en_US
          - fr_FR
          - af_ZA
      "Magento/luma":
        language:
          - en_US
          - fr_FR
          - af_ZA
```

Of, kunt u verkiezen om __ geen thema op te stellen:

```yaml
stage:
  build:
    SCD_MATRIX:
      "Magento/backend": [ ]
```

## `SCD_MAX_EXECUTION_TIME`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.2.0 en later

Staat u toe om de maximale verwachte uitvoeringstijd voor statische inhoudsplaatsing te verhogen.

Standaard stelt Adobe Commerce op de cloudinfrastructuur de maximale verwachte uitvoering in op 900 seconden, maar in sommige scenario&#39;s hebt u wellicht meer tijd nodig om de implementatie van statische inhoud voor een Cloud-project te voltooien.

```yaml
stage:
  build:
    SCD_MAX_EXECUTION_TIME: 3600
```

{{scd-timing-warning}}

## `SCD_STRATEGY`

- **Gebrek** - `quick`
- **Versie** - Adobe Commerce 2.2.0 en later

Pas de [&#x200B; plaatsingsstrategie &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-strategy.html?lang=nl-NL) voor statische inhoud aan. Zie [&#x200B; statische meningsdossiers &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html?lang=nl-NL) opstellen.

Gebruik deze opties _slechts_ als u meer dan één scène hebt:

- `standard` - implementeert alle statische weergavebestanden voor alle pakketten.
- `quick` - (_gebrek_) minimaliseert plaatsingstijd.
- `compact` - bespaart schijfruimte op de server. In Adobe Commerce versie 2.2.4 en lager overschrijft deze instelling de waarde voor `scd_threads` met de waarde `1` .

```yaml
stage:
  build:
    SCD_STRATEGY: "compact"
```

## `SCD_THREADS`

- **Gebrek** - automatisch
- **Versie** - Adobe Commerce 2.1.4 en later

Plaatst het aantal draden voor statische inhoudsplaatsing. De standaardwaarde wordt ingesteld op basis van het aantal gedetecteerde CPU-thread en de standaardwaarde 4 wordt niet overschreden. Verhoog het aantal draden versnelt de statische plaatsing van inhoud; het verminderen van het aantal draden vertraagt het. U kunt bijvoorbeeld de waarde van de thread instellen:

```yaml
stage:
  build:
    SCD_THREADS: 2
```

Om plaatsingstijd verder te verminderen, gebruik [&#x200B; het Beheer van de Configuratie &#x200B;](../store/store-settings.md) met het `scd-dump` bevel om statische plaatsing in de bouwstijlfase te bewegen.

## `SCD_USE_BALER`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.3.0 en later

[&#x200B; Baler &#x200B;](https://github.com/magento/baler) scant uw geproduceerde code van JavaScript en leidt tot een geoptimaliseerde bundel van JavaScript. Als u de geoptimaliseerde bundel op uw site implementeert, kan het aantal netwerkaanvragen bij het laden van uw site afnemen en de laadtijden van de pagina verbeteren.

Stel dit in op `true` om Baler uit te voeren nadat u statische inhoud hebt geïmplementeerd.

```yaml
stage:
  build:
    SCD_USE_BALER: true
```

>[!NOTE]
>
>Omdat Baler in alpha- versie is, is het niet raadzaam om het in de milieu&#39;s van de Productie te gebruiken.

## `SKIP_COMPOSER_DUMP_AUTOLOAD`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Stel in op `true` om de opdracht `composer dump-autoload` over te slaan tijdens de installatie van Cloud Docker. Deze variabele is alleen relevant voor Cloud Docker-containers met schrijfbare bestandssystemen. In dergelijke gevallen voorkomt het overslaan van de opdracht fouten van andere opdrachten die toegang proberen te krijgen tot code vanuit de verwijderde `generated` -map.

Wanneer Adobe Commerce `composer dump-autoload` uitvoert, worden automatisch bestanden gemaakt met koppelingen naar gegenereerde klassen in de map `generated` . Dit is geen probleem in productieomgevingen met alleen-lezen bestandssystemen. Voor installaties van Cloud Docker met schrijfbare bestandssystemen (die alleen zijn gemaakt voor testen en ontwikkelen met `./vendor/bin/ece-docker build:compose --with-test` ) kunt u de opdracht `bin/magento -n setup:upgrade` uitvoeren zonder de optie `--keep-generated` , waarmee de map `generated` wordt verwijderd. Als de map wordt verwijderd, mislukt de opdracht `composer dump-autoload` omdat de opdracht automatisch laden koppelingen bevat naar bestanden in de verwijderde map.

```yaml
stage:
  build:
    SKIP_COMPOSER_DUMP_AUTOLOAD: true
```

## `SKIP_SCD`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Stel in op `true` om de implementatie van statische inhoud tijdens de constructiefase over te slaan.

Als u reeds statische inhoud tijdens de bouwstijlfase met [&#x200B; Beheer van de Configuratie &#x200B;](../store/store-settings.md) opstelt, kunt u statische inhoudsplaatsing voor een snelle bouwstijltest overslaan.

Voor de bouwstijlfase, plaats `SKIP_SCD: false` zodat de statische inhoudsbouw tijdens de bouwstijlfase voorkomt waar het proces plaatsplaatsing niet beïnvloedt of onnodige plaatsonderbreking veroorzaakt. Zie [&#x200B; Statische inhoudsplaatsing &#x200B;](../deploy/static-content.md).

```yaml
stage:
  build:
    SKIP_SCD: false
```

## `VERBOSE_COMMANDS`

- **Gebrek** - _niet plaats_
- **Versie** - Adobe Commerce 2.1.4 en later

Laat toe of maak [&#x200B; Symfony &#x200B;](https://symfony.com/doc/current/console/verbosity.html) onbruikbaar zuivert breedband niveau voor `bin/magento` bevelen CLI die tijdens de plaatsingsfase worden uitgevoerd.

>[!NOTE]
>
>Om VERBOSE_COMMANDS te gebruiken om het detail in beveloutput voor zowel succesvolle als ontbroken `bin/magento` CLI bevelen te controleren, moet u [&#x200B; MIN_LOGING_LEVEL &#x200B;](variables-global.md#minlogginglevel) `debug` plaatsen.

Kies het detailniveau in de logboeken:

- `-v`= normale uitvoer
- `-vv`= uitgebreidere uitvoer
- `-vvv` = uitgebreide uitvoer, ideaal voor foutopsporing

```yaml
stage:
  build:
    VERBOSE_COMMANDS: "-vv"
```
