---
source-git-commit: fddcfdb97aede07b2cd6ef12bda6d7998f941951
workflow-type: tm+mt
source-wordcount: '13721'
ht-degree: 0%

---
# magento-cloud (Adobe Commerce op cloudinfrastructuur)

<!-- The template to render with above values -->

**Versie**: 1.47.0

Deze verwijzing bevat 123 opdrachten die beschikbaar zijn via het opdrachtregelprogramma van `magento-cloud` .
De eerste lijst wordt automatisch gegenereerd met de opdracht `magento-cloud list` in Adobe Commerce op de cloud-infrastructuur.

## Algemeen

Deze verwijzing wordt gegenereerd op basis van de toepassingscodebase. Om de inhoud te veranderen, kunt u de broncode voor de overeenkomstige bevelimplementatie in de [ codebase ](https://github.com/magento/magento-cloud-cli) bewaarplaats bijwerken en uw veranderingen voor overzicht voorleggen. Een andere manier is ons _geven terugkoppelt_ (vind de verbinding bij het hogere recht). Voor bijdragerichtsnoeren, zie {de Bijdragen van de Code 0} [.](https://developer.adobe.com/commerce/contributor/guides/code-contributions/)

### Algemene opties

#### `--help`, `-h`

Dit Help-bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten

- Standaard: `false`
- Accepteert geen waarde

#### `--quiet`, `-q`

Alleen de benodigde uitvoer afdrukken; andere berichten en fouten onderdrukken. Dit betekent: geen interactie. In de uitgebreide modus wordt het genegeerd.

- Standaard: `false`
- Accepteert geen waarde

#### `--yes`, `-y`

Antwoord &quot;ja&quot;aan bevestigingsvragen; keur de standaardwaarde voor andere vragen goed; maak interactie onbruikbaar

- Standaard: `false`
- Accepteert geen waarde

#### `--no-interaction`

Stel geen interactieve vragen. Accepteer standaardwaarden. Gelijk aan het gebruik van de omgevingsvariabele: MAGENTO_CLOUD_CLI_NO_INTERACTION=1

- Standaard: `false`
- Accepteert geen waarde


## `clear-cache`

```bash
magento-cloud cc
```

De CLI-cache wissen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `console`

```bash
magento-cloud web [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Het project openen in de console

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--browser`

De browser waarmee de URL moet worden geopend. Stel 0 in voor geen.

- Vereist een waarde

#### `--pipe`

Voer de URL uit die u wilt stopzetten.

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `decode`

```bash
magento-cloud decode [-P|--property PROPERTY] [--] <value>
```

Een gecodeerde tekenreeks decoderen, zoals MAGENTO_CLOUD_VARIABLES

### Argumenten

#### `value`

De te decoderen variabele

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De eigenschap die binnen de variabele moet worden weergegeven

- Vereist een waarde


## `docs`

```bash
magento-cloud docs [--browser BROWSER] [--pipe] [--] [<search>]...
```

De onlinedocumentatie openen

### Argumenten

#### `search`

Zoekterm(en)

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--browser`

De browser waarmee de URL moet worden geopend. Stel 0 in voor geen.

- Vereist een waarde

#### `--pipe`

Voer de URL uit die u wilt stopzetten.

- Standaard: `false`
- Accepteert geen waarde


## `help`

```bash
magento-cloud help [--format FORMAT] [--raw] [--] [<command_name>]
```

Hiermee geeft u Help voor een opdracht weer

```
The help command displays help for a given command:

  magento-cloud help list

You can also output the help in other formats by using the --format option:

  magento-cloud help --format=json list

To display the list of available commands, please use the list command.
```

### Argumenten

#### `command_name`

De opdrachtnaam

- Standaard: `help`

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--format`

De uitvoerindeling (txt, json of md)

- Standaard: `txt`
- Vereist een waarde

#### `--raw`

Help bij de opdracht Uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `list`

```bash
magento-cloud list [--raw] [--format FORMAT] [--all] [--] [<namespace>]
```

Lijsten, opdrachten

```
The list command lists all commands:

  magento-cloud list

You can also display the commands for a specific namespace:

  magento-cloud list project

You can also output the information in other formats by using the --format option:

  magento-cloud list --format=xml

It's also possible to get raw list of commands (useful for embedding command runner):

  magento-cloud list --raw
```

### Argumenten

#### `command`

De uit te voeren opdracht

- Vereist


#### `namespace`

De naamruimtenaam

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--raw`

Naar uitvoer RAW-opdrachtlijst

- Standaard: `false`
- Accepteert geen waarde

#### `--format`

De uitvoerindeling (txt, xml, json of md)

- Standaard: `txt`
- Vereist een waarde

#### `--all`

Alle opdrachten tonen, inclusief verborgen opdrachten

- Standaard: `false`
- Accepteert geen waarde


## `multi`

```bash
magento-cloud multi [-p|--projects PROJECTS] [--continue] [--sort SORT] [--reverse] [--] <cmd> (<cmd>)...
```

Voer een bevel op veelvoudige projecten uit

### Argumenten

#### `cmd`

De uit te voeren opdracht

- Standaard: `[]`
- Vereist

- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--projects`, `-p`

Een lijst met project-id&#39;s, gescheiden door komma&#39;s en/of witruimte

- Vereist een waarde

#### `--continue`

Doorgaan met opdrachten, zelfs als een uitzondering wordt aangetroffen

- Standaard: `false`
- Accepteert geen waarde

#### `--sort`

Een eigenschap waarmee de lijst met projectopties moet worden gesorteerd

- Standaard: `title`
- Vereist een waarde

#### `--reverse`

De volgorde van projectopties omkeren

- Standaard: `false`
- Accepteert geen waarde


## `activity:cancel`

```bash
magento-cloud activity:cancel [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Een activiteit annuleren

### Argumenten

#### `id`

De activiteit-id. Wordt standaard ingesteld op de meest recente annuleerbare activiteit.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--type`, `-t`

Filteren op type (wanneer u een standaardactiviteit selecteert). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken voor het type, bijvoorbeeld &#39;%var%&#39; om activiteiten met betrekking tot variabelen te selecteren.

- Standaard: `[]`
- Vereist een waarde

#### `--exclude-type`, `-x`

Uitsluiten op type (bij het selecteren van een standaardactiviteit). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

#### `--all`, `-a`

Recente activiteiten in alle omgevingen controleren (bij het selecteren van een standaardactiviteit)

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `activity:get`

```bash
magento-cloud activity:get [-P|--property PROPERTY] [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<id>]
```

Gedetailleerde informatie over één activiteit weergeven

### Argumenten

#### `id`

De activiteit-id. Heeft als standaardwaarde de meest recente activiteit.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De eigenschap die moet worden weergegeven

- Vereist een waarde

#### `--type`, `-t`

Filteren op type (wanneer u een standaardactiviteit selecteert). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken voor het type, bijvoorbeeld &#39;%var%&#39; om activiteiten met betrekking tot variabelen te selecteren.

- Standaard: `[]`
- Vereist een waarde

#### `--exclude-type`, `-x`

Uitsluiten op type (bij het selecteren van een standaardactiviteit). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

#### `--state`

Filteren op status (wanneer u een standaardactiviteit selecteert): in_progress, in behandeling, voltooid of geannuleerd. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--result`

Filteren op resultaat (bij het selecteren van een standaardactiviteit): geslaagd of mislukt

- Vereist een waarde

#### `--incomplete`, `-i`

Alleen onvolledige activiteiten opnemen (bij het selecteren van een standaardactiviteit). Dit is een steno voor —state=in_progress,in afwachting

- Standaard: `false`
- Accepteert geen waarde

#### `--all`, `-a`

Recente activiteiten in alle omgevingen controleren (bij het selecteren van een standaardactiviteit)

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `activity:list`

```bash
magento-cloud activities [-t|--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Een lijst met activiteiten voor een omgeving of project ophalen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--type`, `-t`

Filteractiviteiten op type Waarden kunnen worden gesplitst met komma&#39;s (bijvoorbeeld &quot;a,b,c&quot;) en/of witruimte. Het eerste deel van de naam van de activiteit kan worden weggelaten, bijvoorbeeld &#39;cron&#39; kan &#39;environment.cron&#39;-activiteiten selecteren. De tekens % of * kunnen worden gebruikt als jokerteken, bijvoorbeeld &#39;%var%&#39; om activiteiten met betrekking tot variabelen te selecteren.

- Standaard: `[]`
- Vereist een waarde

#### `--exclude-type`, `-x`

Activiteiten uitsluiten op basis van type. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. Het eerste deel van de naam van de activiteit kan worden weggelaten, bijvoorbeeld &#39;cron&#39; kan &#39;environment.cron&#39;-activiteiten uitsluiten. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

#### `--limit`

Beperk het aantal weergegeven resultaten

- Standaard: `10`
- Vereist een waarde

#### `--start`

Alleen activiteiten die vóór deze datum zijn gemaakt, worden vermeld

- Vereist een waarde

#### `--state`

Activiteiten filteren op status: in_progress, in behandeling, voltooid of geannuleerd. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--result`

Activiteiten filteren op resultaat: geslaagd of mislukt

- Vereist een waarde

#### `--incomplete`, `-i`

Alleen onvolledige activiteiten weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--all`, `-a`

Activiteiten weergeven in alle omgevingen

- Standaard: `false`
- Accepteert geen waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id*, created*, description*, progress*, state*, result*, completed, omgevingen, time_build, time_deploy, time_execute, time_wait, type (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `activity:log`

```bash
magento-cloud activity:log [--refresh REFRESH] [-t|--timestamps] [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--state STATE] [--result RESULT] [-i|--incomplete] [-a|--all] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Logboek weergeven voor een activiteit

### Argumenten

#### `id`

De activiteit-id. Heeft als standaardwaarde de meest recente activiteit.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--refresh`

Vernieuwingsinterval voor activiteit (seconden). Stel de waarde in op 0 om vernieuwen uit te schakelen.

- Standaard: `3`
- Vereist een waarde

#### `--timestamps`, `-t`

Een tijdstempel naast elk bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--type`

Filteren op type (wanneer u een standaardactiviteit selecteert). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken voor het type, bijvoorbeeld &#39;%var%&#39; om activiteiten met betrekking tot variabelen te selecteren.

- Standaard: `[]`
- Vereist een waarde

#### `--exclude-type`, `-x`

Uitsluiten op type (bij het selecteren van een standaardactiviteit). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

#### `--state`

Filteren op status (wanneer u een standaardactiviteit selecteert): in_progress, in behandeling, voltooid of geannuleerd. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--result`

Filteren op resultaat (bij het selecteren van een standaardactiviteit): geslaagd of mislukt

- Vereist een waarde

#### `--incomplete`, `-i`

Alleen onvolledige activiteiten opnemen (bij het selecteren van een standaardactiviteit). Dit is een steno voor —state=in_progress,in afwachting

- Standaard: `false`
- Accepteert geen waarde

#### `--all`, `-a`

Recente activiteiten in alle omgevingen controleren (bij het selecteren van een standaardactiviteit)

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `app:config-get`

```bash
magento-cloud app:config-get [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE]
```

De configuratie van een app weergeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

Het configuratiebezit aan mening

- Vereist een waarde

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--identity-file`, `-i`

[ Vervangen optie, niet meer gebruikt ]

- Vereist een waarde


## `app:list`

```bash
magento-cloud apps [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Apps weergeven in het project

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--pipe`

Alleen een lijst met toepassingsnamen uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: naam*, type*, schijf, pad, grootte (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `auth:api-token-login`

```bash
magento-cloud auth:api-token-login
```

Aanmelden bij Magento Cloud met een API-token

```
Use this command to log in to your Magento Cloud account using an API token.

You can create an account at:
    https://business.adobe.com/products/magento/magento-commerce.html

If you have an account, but you do not already have an API token, you can create one here:
    https://accounts.magento.cloud/user/api-tokens

Alternatively, to log in to the CLI with a browser, run:
    magento-cloud auth:browser-login
```

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `auth:browser-login`

```bash
magento-cloud login [-f|--force] [--method METHOD] [--max-age MAX-AGE] [--browser BROWSER] [--pipe]
```

Aanmelden bij Magento Cloud via een browser

```
Use this command to log in to the Magento Cloud CLI using a web browser.

It launches a temporary local website which redirects you to log in if
necessary, and then captures the resulting authorization code.

Your system's default browser will be used. You can override this using the
--browser option.

Alternatively, to log in using an API token (without a browser), run:
magento-cloud auth:api-token-login

To authenticate non-interactively, configure an API token using the
MAGENTO_CLOUD_CLI_TOKEN environment variable.
```

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--force`, `-f`

Meld u opnieuw aan, zelfs als u zich al hebt aangemeld

- Standaard: `false`
- Accepteert geen waarde

#### `--method`

Specifieke verificatiemethode(n) vereisen

- Standaard: `[]`
- Vereist een waarde

#### `--max-age`

De maximumleeftijd (in seconden) van de webverificatiesessie

- Vereist een waarde

#### `--browser`

De browser waarmee de URL moet worden geopend. Stel 0 in voor geen.

- Vereist een waarde

#### `--pipe`

Voer de URL uit die u wilt stopzetten.

- Standaard: `false`
- Accepteert geen waarde


## `auth:info`

```bash
magento-cloud auth:info [--no-auto-login] [-P|--property PROPERTY] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--] [<property>]
```

Geef uw accountgegevens weer

### Argumenten

#### `property`

De accounteigenschap die moet worden weergegeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--no-auto-login`

Hiermee slaat u de automatische aanmelding over. Niets zal output worden als het programma geopend niet, en de uitgangscode zal 0 zijn, veronderstellend geen andere fouten.

- Standaard: `false`
- Accepteert geen waarde

#### `--property`, `-P`

De accounteigenschap die moet worden weergegeven (alternatieve syntaxis)

- Vereist een waarde

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `auth:logout`

```bash
magento-cloud logout [-a|--all] [--other]
```

Afmelden bij Magento Cloud

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--all`, `-a`

Afmelden bij alle lokale sessies

- Standaard: `false`
- Accepteert geen waarde

#### `--other`

Afmelden bij andere lokale sessies

- Standaard: `false`
- Accepteert geen waarde


## `autoscaling:get`

```bash
magento-cloud autoscaling [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Bekijk de configuratie voor automatisch schalen van apps en workers in een omgeving

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: service*, metrische*, direction*, threshold*, duration*, enabled*, instance_count*, cooldown, max_instances, min_instances (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `autoscaling:set`

```bash
magento-cloud autoscaling:set [-s|--service SERVICE] [-m|--metric METRIC] [--enabled ENABLED] [--threshold-up THRESHOLD-UP] [--duration-up DURATION-UP] [--cooldown-up COOLDOWN-UP] [--threshold-down THRESHOLD-DOWN] [--duration-down DURATION-DOWN] [--cooldown-down COOLDOWN-DOWN] [--instances-min INSTANCES-MIN] [--instances-max INSTANCES-MAX] [--dry-run] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

De zelfschaalconfiguratie van apps of workers in een omgeving instellen

```
Configure automatic scaling for apps or workers in an environment.

You can also configure resources statically by running: magento-cloud resources:set
```

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--service`, `-s`

Naam van de app of worker waarmee automatische schaling wordt geconfigureerd voor

- Vereist een waarde

#### `--metric`, `-m`

Naam van metrisch voor het teweegbrengen autoscaling te gebruiken

- Vereist een waarde

#### `--enabled`

Automatisch schalen inschakelen op basis van de opgegeven metrische waarde

- Vereist een waarde

#### `--threshold-up`

Drempel waarboven de service wordt vergroot

- Vereist een waarde

#### `--duration-up`

Duur waarover de metrische waarde wordt afgezet tegen de drempel voor het verhogen van de schaal

- Vereist een waarde

#### `--cooldown-up`

Duur die moet worden gewacht voordat wordt geprobeerd om na een schalingsgebeurtenis verder te schalen

- Vereist een waarde

#### `--threshold-down`

Drempel waaronder de service wordt verkleind

- Vereist een waarde

#### `--duration-down`

Duur waarover metrisch tegen drempel voor het schrapen neer wordt geëvalueerd

- Vereist een waarde

#### `--cooldown-down`

Duur die moet worden gewacht voordat wordt geprobeerd om na een schalingsgebeurtenis verder te schalen

- Vereist een waarde

#### `--instances-min`

Minimumaantal instanties dat wordt verkleind tot

- Vereist een waarde

#### `--instances-max`

Maximumaantal exemplaren dat wordt geschaald tot

- Vereist een waarde

#### `--dry-run`

Wijzigingen weergeven die u wilt aanbrengen, zonder wijzigingen aan te brengen

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `blackfire:setup`

```bash
magento-cloud blackfire:setup [--server_id SERVER_ID] [--server_token SERVER_TOKEN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Blackfire.io-integratie instellen voor het project

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--server_id`

De server-id

- Vereist een waarde

#### `--server_token`

Het servertoken

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `certificate:add`

```bash
magento-cloud certificate:add [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Een SSL-certificaat toevoegen aan het project

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--cert`

Het pad naar het certificaatbestand

- Vereist een waarde

#### `--key`

Het pad naar het persoonlijke sleutelbestand van het certificaat

- Vereist een waarde

#### `--chain`

Het pad naar het certificaatkettingbestand

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `certificate:delete`

```bash
magento-cloud certificate:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <id>
```

Een certificaat verwijderen uit het project

### Argumenten

#### `id`

De certificaat-id (of het begin ervan)

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `certificate:get`

```bash
magento-cloud certificate:get [-P|--property PROPERTY] [--date-fmt DATE-FMT] [-p|--project PROJECT] [--] <id>
```

Een certificaat weergeven

### Argumenten

#### `id`

De certificaat-id (of het begin ervan)

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De certificaateigenschap die moet worden weergegeven

- Vereist een waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `certificate:list`

```bash
magento-cloud certificates [--domain DOMAIN] [--exclude-domain EXCLUDE-DOMAIN] [--issuer ISSUER] [--only-auto] [--no-auto] [--ignore-expiry] [--only-expired] [--no-expired] [--pipe-domains] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Projectcertificaten weergeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--domain`

Filteren op domeinnaam (niet-hoofdlettergevoelige zoekopdracht)

- Vereist een waarde

#### `--exclude-domain`

Certificaten uitsluiten, overeenkomend op domeinnaam (niet-hoofdlettergevoelige zoekopdracht)

- Vereist een waarde

#### `--issuer`

Filteren op uitgever

- Vereist een waarde

#### `--only-auto`

Alleen certificaten met automatische provisioning weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--no-auto`

Alleen handmatig toegevoegde certificaten weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--ignore-expiry`

Verlopen en niet-verlopen certificaten weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--only-expired`

Alleen verlopen certificaten tonen

- Standaard: `false`
- Accepteert geen waarde

#### `--no-expired`

Alleen niet-verlopen certificaten tonen (standaard)

- Standaard: `false`
- Accepteert geen waarde

#### `--pipe-domains`

Retourneer alleen een lijst met domeinnamen die door de certificaten worden gedekt

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: gemaakt, domeinen, verloopt, id, uitgever. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `commit:get`

```bash
magento-cloud commit:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<commit>]
```

Vastleggingsdetails tonen

### Argumenten

#### `commit`

De commit SHA. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunten (^) of tilde (~) accepteren voor bovenliggende bewerkingen.

- Standaard: `HEAD`

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De eigenschap commit die moet worden weergegeven.

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `commit:list`

```bash
magento-cloud commits [--limit LIMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<commit>]
```

Lijstopdrachten

### Argumenten

#### `commit`

De beginstand past SHA toe. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunten (^) of tilde (~) accepteren voor bovenliggende bewerkingen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--limit`

Het aantal verplichtingen dat moet worden weergegeven.

- Standaard: `10`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: auteur, date, sha, summary. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `db:dump`

```bash
magento-cloud db:dump [--schema SCHEMA] [-f|--file FILE] [-d|--directory DIRECTORY] [-z|--gzip] [-t|--timestamp] [-o|--stdout] [--table TABLE] [--exclude-table EXCLUDE-TABLE] [--schema-only] [--charset CHARSET] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP]
```

Creeer een lokale stortplaats van het verre gegevensbestand

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--schema`

Het te dumpen schema. Laat weg om het standaardschema (gewoonlijk &quot;hoofd&quot;) te gebruiken.

- Vereist een waarde

#### `--file`, `-f`

Een aangepaste bestandsnaam voor de dump

- Vereist een waarde

#### `--directory`, `-d`

Een aangepaste map voor de stortplaats

- Vereist een waarde

#### `--gzip`, `-z`

De stortplaats comprimeren met gzip

- Standaard: `false`
- Accepteert geen waarde

#### `--timestamp`, `-t`

Een tijdstempel toevoegen aan de naam van het stortplaatje

- Standaard: `false`
- Accepteert geen waarde

#### `--stdout`, `-o`

Uitvoeren naar STDOUT in plaats van een bestand

- Standaard: `false`
- Accepteert geen waarde

#### `--table`

Op te nemen tabel(len)

- Standaard: `[]`
- Vereist een waarde

#### `--exclude-table`

Uit te sluiten tabel(len)

- Standaard: `[]`
- Vereist een waarde

#### `--schema-only`

Alleen schema&#39;s dumpen, geen gegevens

- Standaard: `false`
- Accepteert geen waarde

#### `--charset`

De tekensetcodering voor de dump

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde


## `db:sql`

```bash
magento-cloud sql [--raw] [--schema SCHEMA] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP] [--] [<query>]
```

SQL uitvoeren op de externe database

### Argumenten

#### `query`

Een SQL-instructie die moet worden uitgevoerd

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--raw`

Onbewerkte, niet-tabelvormige uitvoer produceren

- Standaard: `false`
- Accepteert geen waarde

#### `--schema`

Het te gebruiken schema. Laat weg om het standaardschema (gewoonlijk &quot;hoofd&quot;) te gebruiken. Geef een lege tekenreeks door als u geen schema wilt gebruiken.

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde


## `domain:add`

```bash
magento-cloud domain:add [--cert CERT] [--key KEY] [--chain CHAIN] [--attach ATTACH] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Voeg een nieuw domein aan het project toe. Deze optie is niet beschikbaar voor projecten met een abonnement in Cloud Pro.

### Argumenten

#### `name`

De domeinnaam

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--cert`

Het pad naar een aangepast certificaatbestand

- Vereist een waarde

#### `--key`

Het pad naar de persoonlijke sleutel voor het aangepaste certificaat

- Vereist een waarde

#### `--chain`

Het pad naar het (de) kettingbestand(en) voor het aangepaste certificaat

- Standaard: `[]`
- Vereist een waarde

#### `--attach`

Het productiedomein dat deze vervangt in de routes van het milieu. Vereist voor niet-productieomgevingsdomeinen.

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `domain:delete`

```bash
magento-cloud domain:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Verwijder een domein uit het project. Deze optie is niet beschikbaar voor projecten met een abonnement in Cloud Pro.

### Argumenten

#### `name`

De domeinnaam

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `domain:get`

```bash
magento-cloud domain:get [-P|--property PROPERTY] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<name>]
```

Gedetailleerde informatie voor een domein weergeven. Deze optie is niet beschikbaar voor projecten met een abonnement in Cloud Pro.

### Argumenten

#### `name`

De domeinnaam

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De eigenschap domain die moet worden weergegeven

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `domain:list`

```bash
magento-cloud domains [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Hiermee wordt een lijst met alle domeinen opgehaald. Deze optie is niet beschikbaar voor projecten met een abonnement in Cloud Pro.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: name*, ssl*, created_at*, registered_name, replacement_for, type, updated_at (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `domain:update`

```bash
magento-cloud domain:update [--cert CERT] [--key KEY] [--chain CHAIN] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Een domein bijwerken. Deze optie is niet beschikbaar voor projecten met een abonnement in Cloud Pro.

### Argumenten

#### `name`

De domeinnaam

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--cert`

Het pad naar een aangepast certificaatbestand

- Vereist een waarde

#### `--key`

Het pad naar de persoonlijke sleutel voor het aangepaste certificaat

- Vereist een waarde

#### `--chain`

Het pad naar het (de) kettingbestand(en) voor het aangepaste certificaat

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:activate`

```bash
magento-cloud environment:activate [--parent PARENT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```

Een omgeving activeren

### Argumenten

#### `environment`

Te activeren omgeving(en)

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--parent`

Een bovenliggende omgeving instellen voordat een omgeving wordt geactiveerd

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:branch`

```bash
magento-cloud branch [--title TITLE] [--type TYPE] [--no-clone-parent] [--no-checkout] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>] [<parent>]
```

Een omgeving vertakken

### Argumenten

#### `id`

De id (vertakkingsnaam) van de nieuwe omgeving


#### `parent`

De bovenliggende omgeving van de nieuwe omgeving

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--title`

De titel van de nieuwe omgeving

- Vereist een waarde

#### `--type`

Het type nieuwe omgeving

- Vereist een waarde

#### `--no-clone-parent`

De gegevens van de bovenliggende omgeving niet klonen

- Standaard: `false`
- Accepteert geen waarde

#### `--no-checkout`

De vertakking niet lokaal uitchecken

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:checkout`

```bash
magento-cloud checkout [<id>]
```

Een omgeving controleren

### Argumenten

#### `id`

De id van de omgeving die moet worden uitgecheckt. Bijvoorbeeld: &quot;sprint2&quot;

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `environment:delete`

```bash
magento-cloud environment:delete [--delete-branch] [--no-delete-branch] [--type TYPE] [-t|--only-type ONLY-TYPE] [--exclude EXCLUDE] [--exclude-type EXCLUDE-TYPE] [--inactive] [--status STATUS] [--only-status ONLY-STATUS] [--exclude-status EXCLUDE-STATUS] [--merged] [--allow-delete-parent] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]...
```

Een of meer omgevingen verwijderen

```
When a Magento Cloud environment is deleted, it will become "inactive": it will
exist only as a Git branch, containing code but no services, databases nor
files.

This command allows you to delete environments as well as their Git branches.
```

### Argumenten

#### `environment`

The environment(s) to delete. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--delete-branch`

Git-vertakking(en) verwijderen voor inactieve omgevingen, zonder bevestiging

- Standaard: `false`
- Accepteert geen waarde

#### `--no-delete-branch`

Git-vertakking(en) niet verwijderen (niet-actieve omgevingen)

- Standaard: `false`
- Accepteert geen waarde

#### `--type`

Verwijder alle omgevingen van een type (en voeg deze toe aan andere geselecteerde omgevingen) Waarden kunnen worden gesplitst met komma&#39;s (bijv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--only-type`, `-t`

Alleen verwijderomgevingen van een specifiek type Waarden kunnen worden gesplitst in komma&#39;s (bijvoorbeeld &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--exclude`

Omgeving(en) niet te verwijderen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--exclude-type`

Omgevingstype(n) waarvan de waarden niet mogen worden verwijderd, mogen worden opgesplitst in komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--inactive`

Alle niet-actieve omgevingen verwijderen (toevoegen aan andere geselecteerde omgevingen)

- Standaard: `false`
- Accepteert geen waarde

#### `--status`

Verwijder alle omgevingen van een status (en voeg deze toe aan andere geselecteerde omgevingen) Waarden kunnen worden gesplitst met komma&#39;s (bijv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--only-status`

Alleen verwijderomgevingen van een specifieke statuswaarde kunnen worden gesplitst in komma&#39;s (bijvoorbeeld &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--exclude-status`

Status(en) van omgeving waarvan geen waarden mogen worden verwijderd, kan worden opgesplitst in komma&#39;s (bijvoorbeeld &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--merged`

Alle samengevoegde omgevingen verwijderen (aan geselecteerde omgevingen toevoegen)

- Standaard: `false`
- Accepteert geen waarde

#### `--allow-delete-parent`

Toestaan dat omgevingen met onderliggende items worden verwijderd

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:deploy`

```bash
magento-cloud deploy [-s|--strategy STRATEGY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Geleidelijke wijzigingen van een omgeving implementeren

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--strategy`, `-s`

De implementatiestrategie, de stopstart (standaard, opnieuw opstarten met een stopzetting) of het rollen (geen downtime)

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:deploy:type`

```bash
magento-cloud environment:deploy:type [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<type>]
```

Het implementatietype voor de omgeving weergeven of instellen

```
Choose automatic (the default) if you want your changes to be deployed immediately as they are made.
Choose manual to have changes staged until you trigger a deployment (including changes to code, variables, domains and settings).
```

### Argumenten

#### `type`

Het implementatietype van de omgeving: automatisch of handmatig.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--pipe`

Implementatietype uitvoeren naar stdout

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:http-access`

```bash
magento-cloud httpaccess [--access ACCESS] [--auth AUTH] [--enabled ENABLED] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

De HTTP-toegangsinstellingen voor een omgeving bijwerken

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--access`

De beperking van de toegang in het formaat &quot;toestemming :address&quot;. Gebruik 0 om alle adressen te wissen.

- Standaard: `[]`
- Vereist een waarde

#### `--auth`

De Basisautegeloofsbrieven van HTTP in formaat &quot;gebruikersbenaming :password&quot;. Gebruik 0 om alle gegevens te wissen.

- Standaard: `[]`
- Vereist een waarde

#### `--enabled`

Of toegangsbeheer zou moeten worden toegelaten: 1 om toe te laten, 0 om onbruikbaar te maken

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:info`

```bash
magento-cloud environment:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```

Eigenschappen voor een omgeving lezen of instellen

### Argumenten

#### `property`

De naam van de eigenschap


#### `value`

Een nieuwe waarde voor de eigenschap instellen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:init`

```bash
magento-cloud environment:init [--profile PROFILE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <url>
```

Een omgeving initialiseren vanuit een openbare Git-opslagplaats

### Argumenten

#### `url`

Een URL naar een Git-opslagplaats

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--profile`

De naam van het profiel

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:list`

```bash
magento-cloud environments [-I|--no-inactive] [--status STATUS] [--pipe] [--refresh REFRESH] [--sort SORT] [--reverse] [--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Een lijst met omgevingen ophalen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--no-inactive`, `-I`

Niet-actieve omgevingen tonen

- Standaard: `false`
- Accepteert geen waarde

#### `--status`

Filteromgevingen op status (actief, inactief, vuil, gepauzeerd, verwijderen). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--pipe`

Een eenvoudige lijst met milieu-id&#39;s uitvoeren.

- Standaard: `false`
- Accepteert geen waarde

#### `--refresh`

Of de lijst moet worden vernieuwd.

- Standaard: `1`
- Vereist een waarde

#### `--sort`

Een eigenschap waarop u wilt sorteren

- Standaard: `title`
- Vereist een waarde

#### `--reverse`

Omgekeerde (aflopende) volgorde sorteren

- Standaard: `false`
- Accepteert geen waarde

#### `--type`

Filter de lijst op omgevingstype(n). Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id*, title*, status*, type*, gemaakt, machine_naam, bijgewerkt (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `environment:logs`

```bash
magento-cloud log [--lines LINES] [--tail] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<type>]
```

De logboeken van een omgeving lezen

### Argumenten

#### `type`

Het logtype, bijvoorbeeld &quot;access&quot; of &quot;error&quot;

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--lines`

Het aantal regels dat moet worden weergegeven

- Standaard: `100`
- Vereist een waarde

#### `--tail`

Het logboek continu staart

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--instance`, `-I`

Instantie-id

- Vereist een waarde


## `environment:merge`

```bash
magento-cloud merge [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```

Een omgeving samenvoegen

```
This command will initiate a Git merge of the specified environment into its parent environment.
```

### Argumenten

#### `environment`

De omgeving die moet worden samengevoegd

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:pause`

```bash
magento-cloud environment:pause [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Een omgeving onderbreken

```
Pausing an environment helps to reduce resource consumption and carbon emissions.

The environment will be unavailable until it is resumed. No data will be lost.
```

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:push`

```bash
magento-cloud push [--target TARGET] [-f|--force] [--force-with-lease] [-u|--set-upstream] [--activate] [--parent PARENT] [--type TYPE] [--no-clone-parent] [-W|--no-wait] [--wait] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<source>]
```

Code naar een omgeving duwen

### Argumenten

#### `source`

De Git source ref, bijvoorbeeld een vertakkingsnaam of een commit hash.

- Standaard: `HEAD`

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--target`

De naam van de doelvertakking. Wordt standaard ingesteld op de huidige vertakking.

- Vereist een waarde

#### `--force`, `-f`

Niet-snelle updates toestaan

- Standaard: `false`
- Accepteert geen waarde

#### `--force-with-lease`

Niet-snelle updates toestaan, als de verafgelegen-volgende tak bijgewerkt is

- Standaard: `false`
- Accepteert geen waarde

#### `--set-upstream`, `-u`

Stel de doelomgeving in als de upstream voor de bronvertakking. Dit zal ook het doelproject als ver voor de lokale bewaarplaats plaatsen.

- Standaard: `false`
- Accepteert geen waarde

#### `--activate`

Activeer de omgeving. Gepauzeerde omgevingen worden hervat. Dit zal ervoor zorgen dat de omgeving actief is, ook als er geen veranderingen worden doorgevoerd.

- Standaard: `false`
- Accepteert geen waarde

#### `--parent`

De bovenliggende omgeving instellen (alleen gebruikt met —activate)

- Vereist een waarde

#### `--type`

Het omgevingstype instellen (alleen gebruikt met —activate)

- Vereist een waarde

#### `--no-clone-parent`

De gegevens van de bovenliggende vertakking niet klonen (alleen gebruikt met —activate)

- Standaard: `false`
- Accepteert geen waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `environment:redeploy`

```bash
magento-cloud redeploy [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Een omgeving opnieuw implementeren

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:relationships`

```bash
magento-cloud relationships [-P|--property PROPERTY] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<environment>]
```

Relaties van een omgeving tonen

### Argumenten

#### `environment`

Het milieu

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De relatie-eigenschap die moet worden weergegeven

- Vereist een waarde

#### `--refresh`

Of de relaties moeten worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `environment:resume`

```bash
magento-cloud environment:resume [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait]
```

Een gepauzeerde omgeving hervatten

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:scp`

```bash
magento-cloud scp [-r|--recursive] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<files>]...
```

Bestanden kopiëren van en naar een omgeving met behulp van scp

### Argumenten

#### `files`

Te kopiëren bestanden. Gebruik het voorvoegsel &#39;remote&#39;: om externe locaties te definiëren.

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--recursive`, `-r`

Gehele mappen recursief kopiëren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--instance`, `-I`

Instantie-id

- Vereist een waarde


## `environment:ssh`

```bash
magento-cloud ssh [--pipe] [--all] [-o|--option OPTION] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE] [--] [<cmd>]...
```

SSH in de huidige omgeving

### Argumenten

#### `cmd`

Een opdracht die op de omgeving moet worden uitgevoerd.

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--pipe`

Alleen de SSH-URL uitvoeren.

- Standaard: `false`
- Accepteert geen waarde

#### `--all`

Voer alle SSH-URL&#39;s uit (voor elke app).

- Standaard: `false`
- Accepteert geen waarde

#### `--option`, `-o`

Een extra optie doorgeven aan SSH

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--instance`, `-I`

Instantie-id

- Vereist een waarde


## `environment:synchronize`

```bash
magento-cloud sync [--rebase] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<synchronize>]...
```

De code en/of gegevens van een omgeving synchroniseren vanuit het bovenliggende element

```
This command synchronizes to a child environment from its parent environment.

Synchronizing "code" means there will be a Git merge from the parent to the
child.

Synchronizing "data" means that all files in all services (including
static files, databases, logs, search indices, etc.) will be copied from the
parent to the child.
```

### Argumenten

#### `synchronize`

Wat moet u synchroniseren: &quot;code&quot;, &quot;gegevens&quot; of beide

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--rebase`

Code synchroniseren door opnieuw te baseren in plaats van samen te voegen

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `environment:url`

```bash
magento-cloud url [-1|--primary] [--browser BROWSER] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

De openbare URL&#39;s van een omgeving ophalen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--primary`, `-1`

Retourneert alleen de URL voor de primaire route

- Standaard: `false`
- Accepteert geen waarde

#### `--browser`

De browser waarmee de URL moet worden geopend. Stel 0 in voor geen.

- Vereist een waarde

#### `--pipe`

Voer de URL uit die u wilt stopzetten.

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `environment:xdebug`

```bash
magento-cloud xdebug [--port PORT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Een tunnel openen voor Xdebug in de omgeving

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--port`

De lokale poort

- Standaard: `9000`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--instance`, `-I`

Instantie-id

- Vereist een waarde


## `integration:activity:get`

```bash
magento-cloud integration:activity:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [--] [<integration>] [<activity>]
```

Gedetailleerde informatie weergeven over één integratieactiviteit

### Argumenten

#### `integration`

Een integratie-id. Laat leeg om uit een lijst te kiezen.


#### `activity`

De activiteit-id. Wordt standaard ingesteld op de meest recente integratieactiviteit.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De eigenschap die moet worden weergegeven

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

[ Vervangen optie, niet gebruikt ]

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `integration:activity:list`

```bash
magento-cloud integration:activities [--type TYPE] [-x|--exclude-type EXCLUDE-TYPE] [--limit LIMIT] [--start START] [--state STATE] [--result RESULT] [-i|--incomplete] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<id>]
```

Een lijst met activiteiten voor integratie ophalen

### Argumenten

#### `id`

Een integratie-id. Laat leeg om uit een lijst te kiezen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--type`

Filteractiviteiten op type. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--exclude-type`, `-x`

Activiteiten uitsluiten op basis van type. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte. De tekens % of * kunnen worden gebruikt als jokerteken om typen uit te sluiten.

- Standaard: `[]`
- Vereist een waarde

#### `--limit`

Beperk het aantal weergegeven resultaten

- Standaard: `10`
- Vereist een waarde

#### `--start`

Alleen activiteiten die vóór deze datum zijn gemaakt, worden vermeld

- Vereist een waarde

#### `--state`

Filteractiviteiten op status. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--result`

Activiteiten filteren op resultaat

- Vereist een waarde

#### `--incomplete`, `-i`

Alleen onvolledige activiteiten weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id*, created*, description*, type*, state*, result*, completed, progress, time_build, time_deploy, time_execute, time_wait (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

[ Vervangen optie, niet gebruikt ]

- Vereist een waarde


## `integration:activity:log`

```bash
magento-cloud integration:activity:log [-t|--timestamps] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<integration>] [<activity>]
```

Logboek weergeven voor een integratieactiviteit

### Argumenten

#### `integration`

Een integratie-id. Laat leeg om uit een lijst te kiezen.


#### `activity`

De activiteit-id. Wordt standaard ingesteld op de meest recente integratieactiviteit.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--timestamps`, `-t`

Een tijdstempel naast elk bericht weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

[ Vervangen optie, niet gebruikt ]

- Vereist een waarde


## `integration:add`

```bash
magento-cloud integration:add [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait]
```

Integratie toevoegen aan het project

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--type`

Het integratietype (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhaakje&#39;, &#39;health.email&#39;, &#39;health.pagerduty&#39;, &#39;health.slack&#39;, &#39;health.webhaakje&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;, &#39;otlplplog&#39;)

- Vereist een waarde

#### `--base-url`

De basis-URL van de serverinstallatie

- Vereist een waarde

#### `--bitbucket-url`

De basis-URL van de Bitmap Server-installatie

- Vereist een waarde

#### `--username`

De gebruikersnaam van de Bitmap-server

- Vereist een waarde

#### `--token`

Een verificatie- of toegangstoken voor de integratie

- Vereist een waarde

#### `--key`

Een OAuth-toets voor bitemmers

- Vereist een waarde

#### `--secret`

Een Bitbucket OAuth-consumentengeheim

- Vereist een waarde

#### `--license-key`

De licentiecode voor New Relic Logs

- Vereist een waarde

#### `--server-project`

Het project (bijvoorbeeld &#39;namespace/repo&#39;)

- Vereist een waarde

#### `--repository`

De opslagplaats die moet worden getraceerd (bv. &quot;eigenaar/opslagplaats&quot;)

- Vereist een waarde

#### `--build-merge-requests`

GitLab: samenvoegverzoeken als omgevingen samenstellen

- Standaard: `true`
- Vereist een waarde

#### `--build-pull-requests`

Bouw elk trekkingsverzoek als milieu

- Standaard: `true`
- Vereist een waarde

#### `--build-draft-pull-requests`

Ontwerp-aanroepverzoeken samenstellen

- Standaard: `true`
- Vereist een waarde

#### `--build-pull-requests-post-merge`

Trek verzoeken bouwen die op hun post-fusiestatus worden gebaseerd

- Standaard: `false`
- Vereist een waarde

#### `--build-wip-merge-requests`

GitLab: aanvragen voor WIP-samenvoeging samenstellen

- Standaard: `true`
- Vereist een waarde

#### `--merge-requests-clone-parent-data`

GitLab: gegevens klonen voor samenvoegverzoeken

- Standaard: `true`
- Vereist een waarde

#### `--pull-requests-clone-parent-data`

De gegevens van de bovenliggende omgeving klonen voor pull-aanvragen

- Standaard: `true`
- Vereist een waarde

#### `--resync-pull-requests`

Hersynchroniseer de gegevens van het trekkingsverzoek op elke bouwstijl

- Standaard: `false`
- Vereist een waarde

#### `--fetch-branches`

Alle vertakkingen ophalen van de externe server (als inactieve omgevingen)

- Standaard: `true`
- Vereist een waarde

#### `--prune-branches`

Vertakkingen verwijderen die niet bestaan op de externe server

- Standaard: `true`
- Vereist een waarde

#### `--resources-init`

De bronnen die moeten worden gebruikt bij het initialiseren van een nieuwe service (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Vereist een waarde

#### `--url`

Het URL- of API-eindpunt voor de integratie

- Vereist een waarde

#### `--shared-key`

Webhaak: de gedeelde sleutel voor JWS

- Vereist een waarde

#### `--file`

De naam van een lokaal bestand dat het te uploaden script bevat

- Vereist een waarde

#### `--events`

Een lijst met gebeurtenissen waarop moet worden gereageerd, bijvoorbeeld environment.push

- Standaard: `*`
- Vereist een waarde

#### `--states`

Een lijst met staten waar moet worden opgetreden, bijv. pending, in_progress, complete

- Standaard: `complete`
- Vereist een waarde

#### `--environments`

De milieu-id&#39;s die moeten worden opgenomen

- Standaard: `*`
- Vereist een waarde

#### `--excluded-environments`

De milieu-id&#39;s om uit te sluiten

- Standaard: `[]`
- Vereist een waarde

#### `--from-address`

[ Facultatieve ] Douane van adres voor waakzame e-mails

- Vereist een waarde

#### `--recipients`

E-mailadres(sen) van ontvanger

- Standaard: `[]`
- Vereist een waarde

#### `--channel`

Het Slack-kanaal

- Vereist een waarde

#### `--routing-key`

De PagerDuty-routeringssleutel

- Vereist een waarde

#### `--category`

De Sumo Logic-categorie, gebruikt voor filteren

- Vereist een waarde

#### `--index`

De segmentindex

- Vereist een waarde

#### `--sourcetype`

Het brontype van de Splunk-gebeurtenis

- Vereist een waarde

#### `--protocol`

Vervoersprotocol van Syslog (&quot;tcp&quot;, &quot;udp&quot;, &quot;tls&quot;)

- Standaard: `tls`
- Vereist een waarde

#### `--syslog-host`

Syslog relais/inzamelaargastheer

- Vereist een waarde

#### `--syslog-port`

Syslog relais/inzamelingspoort

- Vereist een waarde

#### `--facility`

Syslog-faciliteit

- Standaard: `1`
- Vereist een waarde

#### `--message-format`

Syslog-berichtindeling (&#39;rfc3164&#39; of &#39;rfc5424&#39;)

- Standaard: `rfc5424`
- Vereist een waarde

#### `--auth-mode`

Verificatiemodus (&#39;prefix&#39; of &#39;gestructureerde_data&#39;)

- Standaard: `prefix`
- Vereist een waarde

#### `--auth-token`

Verificatietoken

- Vereist een waarde

#### `--verify-tls`

Of HTTPS-certificaatverificatie moet worden ingeschakeld (aanbevolen)

- Standaard: `true`
- Vereist een waarde

#### `--header`

HTTP-header(s) voor gebruik in POST-aanvragen. Scheid namen en waarden met een dubbele punt (:).

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `integration:delete`

```bash
magento-cloud integration:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```

Integratie uit een project verwijderen

### Argumenten

#### `id`

De integratie-id. Laat leeg om uit een lijst te kiezen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `integration:get`

```bash
magento-cloud integration:get [-P|--property [PROPERTY]] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<id>]
```

Details van een integratie weergeven

### Argumenten

#### `id`

Een integratie-id. Laat leeg om uit een lijst te kiezen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De integratieeigenschap die moet worden weergegeven

- Accepteert een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `integration:list`

```bash
magento-cloud integrations [-t|--type TYPE] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Een lijst met projectintegratie(s) weergeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--type`, `-t`

Filteren op type

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id, summary, type. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `integration:update`

```bash
magento-cloud integration:update [--type TYPE] [--base-url BASE-URL] [--bitbucket-url BITBUCKET-URL] [--username USERNAME] [--token TOKEN] [--key KEY] [--secret SECRET] [--license-key LICENSE-KEY] [--server-project SERVER-PROJECT] [--repository REPOSITORY] [--build-merge-requests BUILD-MERGE-REQUESTS] [--build-pull-requests BUILD-PULL-REQUESTS] [--build-draft-pull-requests BUILD-DRAFT-PULL-REQUESTS] [--build-pull-requests-post-merge BUILD-PULL-REQUESTS-POST-MERGE] [--build-wip-merge-requests BUILD-WIP-MERGE-REQUESTS] [--merge-requests-clone-parent-data MERGE-REQUESTS-CLONE-PARENT-DATA] [--pull-requests-clone-parent-data PULL-REQUESTS-CLONE-PARENT-DATA] [--resync-pull-requests RESYNC-PULL-REQUESTS] [--fetch-branches FETCH-BRANCHES] [--prune-branches PRUNE-BRANCHES] [--resources-init RESOURCES-INIT] [--url URL] [--shared-key SHARED-KEY] [--file FILE] [--events EVENTS] [--states STATES] [--environments ENVIRONMENTS] [--excluded-environments EXCLUDED-ENVIRONMENTS] [--from-address FROM-ADDRESS] [--recipients RECIPIENTS] [--channel CHANNEL] [--routing-key ROUTING-KEY] [--category CATEGORY] [--index INDEX] [--sourcetype SOURCETYPE] [--protocol PROTOCOL] [--syslog-host SYSLOG-HOST] [--syslog-port SYSLOG-PORT] [--facility FACILITY] [--message-format MESSAGE-FORMAT] [--auth-mode AUTH-MODE] [--auth-token AUTH-TOKEN] [--verify-tls VERIFY-TLS] [--header HEADER] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<id>]
```

Integratie bijwerken

### Argumenten

#### `id`

De id van de bij te werken integratie

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--type`

Het integratietype (&#39;bitbucket&#39;, &#39;bitbucket_server&#39;, &#39;github&#39;, &#39;gitlab&#39;, &#39;webhaakje&#39;, &#39;health.email&#39;, &#39;health.pagerduty&#39;, &#39;health.slack&#39;, &#39;health.webhaakje&#39;, &#39;httplog&#39;, &#39;script&#39;, &#39;newrelic&#39;, &#39;splunk&#39;, &#39;sumologic&#39;, &#39;syslog&#39;, &#39;otlplplog&#39;)

- Vereist een waarde

#### `--base-url`

De basis-URL van de serverinstallatie

- Vereist een waarde

#### `--bitbucket-url`

De basis-URL van de Bitmap Server-installatie

- Vereist een waarde

#### `--username`

De gebruikersnaam van de Bitmap-server

- Vereist een waarde

#### `--token`

Een verificatie- of toegangstoken voor de integratie

- Vereist een waarde

#### `--key`

Een OAuth-toets voor bitemmers

- Vereist een waarde

#### `--secret`

Een Bitbucket OAuth-consumentengeheim

- Vereist een waarde

#### `--license-key`

De licentiecode voor New Relic Logs

- Vereist een waarde

#### `--server-project`

Het project (bijvoorbeeld &#39;namespace/repo&#39;)

- Vereist een waarde

#### `--repository`

De opslagplaats die moet worden getraceerd (bv. &quot;eigenaar/opslagplaats&quot;)

- Vereist een waarde

#### `--build-merge-requests`

GitLab: samenvoegverzoeken als omgevingen samenstellen

- Standaard: `true`
- Vereist een waarde

#### `--build-pull-requests`

Bouw elk trekkingsverzoek als milieu

- Standaard: `true`
- Vereist een waarde

#### `--build-draft-pull-requests`

Ontwerp-aanroepverzoeken samenstellen

- Standaard: `true`
- Vereist een waarde

#### `--build-pull-requests-post-merge`

Trek verzoeken bouwen die op hun post-fusiestatus worden gebaseerd

- Standaard: `false`
- Vereist een waarde

#### `--build-wip-merge-requests`

GitLab: aanvragen voor WIP-samenvoeging samenstellen

- Standaard: `true`
- Vereist een waarde

#### `--merge-requests-clone-parent-data`

GitLab: gegevens klonen voor samenvoegverzoeken

- Standaard: `true`
- Vereist een waarde

#### `--pull-requests-clone-parent-data`

De gegevens van de bovenliggende omgeving klonen voor pull-aanvragen

- Standaard: `true`
- Vereist een waarde

#### `--resync-pull-requests`

Hersynchroniseer de gegevens van het trekkingsverzoek op elke bouwstijl

- Standaard: `false`
- Vereist een waarde

#### `--fetch-branches`

Alle vertakkingen ophalen van de externe server (als inactieve omgevingen)

- Standaard: `true`
- Vereist een waarde

#### `--prune-branches`

Vertakkingen verwijderen die niet bestaan op de externe server

- Standaard: `true`
- Vereist een waarde

#### `--resources-init`

De bronnen die moeten worden gebruikt bij het initialiseren van een nieuwe service (&#39;minimum&#39;, &#39;default&#39;, &#39;manual&#39;, &#39;parent&#39;)

- Vereist een waarde

#### `--url`

Het URL- of API-eindpunt voor de integratie

- Vereist een waarde

#### `--shared-key`

Webhaak: de gedeelde sleutel voor JWS

- Vereist een waarde

#### `--file`

De naam van een lokaal bestand dat het te uploaden script bevat

- Vereist een waarde

#### `--events`

Een lijst met gebeurtenissen waarop moet worden gereageerd, bijvoorbeeld environment.push

- Standaard: `*`
- Vereist een waarde

#### `--states`

Een lijst met staten waar moet worden opgetreden, bijv. pending, in_progress, complete

- Standaard: `complete`
- Vereist een waarde

#### `--environments`

De milieu-id&#39;s die moeten worden opgenomen

- Standaard: `*`
- Vereist een waarde

#### `--excluded-environments`

De milieu-id&#39;s om uit te sluiten

- Standaard: `[]`
- Vereist een waarde

#### `--from-address`

[ Facultatieve ] Douane van adres voor waakzame e-mails

- Vereist een waarde

#### `--recipients`

E-mailadres(sen) van ontvanger

- Standaard: `[]`
- Vereist een waarde

#### `--channel`

Het Slack-kanaal

- Vereist een waarde

#### `--routing-key`

De PagerDuty-routeringssleutel

- Vereist een waarde

#### `--category`

De Sumo Logic-categorie, gebruikt voor filteren

- Vereist een waarde

#### `--index`

De segmentindex

- Vereist een waarde

#### `--sourcetype`

Het brontype van de Splunk-gebeurtenis

- Vereist een waarde

#### `--protocol`

Vervoersprotocol van Syslog (&quot;tcp&quot;, &quot;udp&quot;, &quot;tls&quot;)

- Standaard: `tls`
- Vereist een waarde

#### `--syslog-host`

Syslog relais/inzamelaargastheer

- Vereist een waarde

#### `--syslog-port`

Syslog relais/inzamelingspoort

- Vereist een waarde

#### `--facility`

Syslog-faciliteit

- Standaard: `1`
- Vereist een waarde

#### `--message-format`

Syslog-berichtindeling (&#39;rfc3164&#39; of &#39;rfc5424&#39;)

- Standaard: `rfc5424`
- Vereist een waarde

#### `--auth-mode`

Verificatiemodus (&#39;prefix&#39; of &#39;gestructureerde_data&#39;)

- Standaard: `prefix`
- Vereist een waarde

#### `--auth-token`

Verificatietoken

- Vereist een waarde

#### `--verify-tls`

Of HTTPS-certificaatverificatie moet worden ingeschakeld (aanbevolen)

- Standaard: `true`
- Vereist een waarde

#### `--header`

HTTP-header(s) voor gebruik in POST-aanvragen. Scheid namen en waarden met een dubbele punt (:).

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `integration:validate`

```bash
magento-cloud integration:validate [-p|--project PROJECT] [--] [<id>]
```

Een bestaande integratie valideren

```
This command allows you to check whether an integration is valid.

An exit code of 0 means the integration is valid, while 4 means it is invalid.
Any other exit code indicates an unexpected error.

Integrations are validated automatically on creation and on update. However,
because they involve external resources, it is possible for a valid integration
to become invalid. For example, an access token may be revoked, or an external
repository may be deleted.
```

### Argumenten

#### `id`

Een integratie-id. Laat leeg om uit een lijst te kiezen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `local:build`

```bash
magento-cloud build [-a|--abslinks] [-s|--source SOURCE] [-d|--destination DESTINATION] [-c|--copy] [--clone] [--run-deploy-hooks] [--no-clean] [--no-archive] [--no-backup] [--no-cache] [--no-build-hooks] [--no-deps] [--working-copy] [--concurrency CONCURRENCY] [--lock] [--] [<app>]...
```

Bouw plaatselijk het huidige project

### Argumenten

#### `app`

Toepassingen opgeven die moeten worden gemaakt

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--abslinks`, `-a`

Absolute koppelingen gebruiken

- Standaard: `false`
- Accepteert geen waarde

#### `--source`, `-s`

De bronmap. Wordt standaard ingesteld op de huidige projecthoofdmap.

- Vereist een waarde

#### `--destination`, `-d`

De bestemming, waaraan de webhoofdmap van elke app wordt gekoppeld. Standaard: _www

- Vereist een waarde

#### `--copy`, `-c`

Kopiëren naar een build-directory in plaats van te symboliseren vanaf de bron

- Standaard: `false`
- Accepteert geen waarde

#### `--clone`

Gebruik Git om de huidige HEAD naar de ontwikkelmap te klonen

- Standaard: `false`
- Accepteert geen waarde

#### `--run-deploy-hooks`

Implementatie- en/of post_implementatiehaken uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--no-clean`

Oude builds niet verwijderen

- Standaard: `false`
- Accepteert geen waarde

#### `--no-archive`

Maak of gebruik geen build-archief

- Standaard: `false`
- Accepteert geen waarde

#### `--no-backup`

Maak geen back-up van de vorige build

- Standaard: `false`
- Accepteert geen waarde

#### `--no-cache`

Cache uitschakelen

- Standaard: `false`
- Accepteert geen waarde

#### `--no-build-hooks`

Geen haken voor na het bouwen uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--no-deps`

Installeer geen build-afhankelijkheden lokaal

- Standaard: `false`
- Accepteert geen waarde

#### `--working-copy`

Duwen: gebruik git om een opslagplaats voor elke Drupal-module te klonen in plaats van gewoon een versie te downloaden

- Standaard: `false`
- Accepteert geen waarde

#### `--concurrency`

Duw: stel het aantal gelijktijdige projecten in dat tegelijkertijd wordt verwerkt

- Standaard: `4`
- Vereist een waarde

#### `--lock`

Duw: maak of werk een vergrendelingsbestand bij (alleen beschikbaar met Duw versie 7+)

- Standaard: `false`
- Accepteert geen waarde


## `local:dir`

```bash
magento-cloud dir [<subdir>]
```

De lokale hoofdmap van het project zoeken

### Argumenten

#### `subdir`

De submap die moet worden gevonden (&#39;local&#39;, &#39;web&#39; of &#39;shared&#39;)

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `metrics:all`

```bash
magento-cloud metrics [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Metrische gegevens over CPU, schijf en geheugen weergeven voor een omgeving

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--bytes`, `-B`

Grootte in bytes weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--range`, `-r`

Het tijdbereik. Metriek wordt voor deze duur geladen tot de eindtijd (—to). U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimaal 5 m, maximaal 8 uur of meer (afhankelijk van het project), standaard 10 m.

- Vereist een waarde

#### `--interval`, `-i`

Het tijdinterval. De standaardwaarde is een verdeling van het bereik. U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimaal 1 m.

- Vereist een waarde

#### `--to`

De eindtijd. Tot nu toe is dat standaard het geval.

- Vereist een waarde

#### `--latest`, `-1`

Alleen het laatste enkele gegevenspunt weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--service`, `-s`

Filteren op service- of toepassingsnaam De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

#### `--type`

Filteren op servicetype (indien —service niet opgegeven). De versie is niet vereist. De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: tijdstempel*, service*, cpu_percent*, mem_percent*, disk_percent*, tmp_disk_percent*, cpu_limit, cpu_used, disk_limit, disk_used, inodes_limit, inodes_percent, inodes_used, mem_limit, mem_used, tmp_disk_limit, tmp_disk_used_limit, tmp_inodes_percent, tmp_inodes_used, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `metrics:cpu`

```bash
magento-cloud cpu [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

CPU-gebruik van een omgeving tonen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--range`, `-r`

Het tijdbereik. Metriek wordt voor deze duur geladen tot de eindtijd (—to). U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimaal 5 m, maximaal 8 uur of meer (afhankelijk van het project), standaard 10 m.

- Vereist een waarde

#### `--interval`, `-i`

Het tijdinterval. De standaardwaarde is een verdeling van het bereik. U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimaal 1 m.

- Vereist een waarde

#### `--to`

De eindtijd. Tot nu toe is dat standaard het geval.

- Vereist een waarde

#### `--latest`, `-1`

Alleen het laatste enkele gegevenspunt weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--service`, `-s`

Filteren op service- of toepassingsnaam De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

#### `--type`

Filteren op servicetype (indien —service niet opgegeven). De versie is niet vereist. De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: timestamp*, service*, used*, limit*, percent*, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `metrics:disk-usage`

```bash
magento-cloud disk [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [--tmp] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Schijfgebruik van een omgeving tonen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--bytes`, `-B`

Grootte in bytes weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--range`, `-r`

Het tijdbereik. Metriek wordt voor deze duur geladen tot de eindtijd (—to). U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimaal 5 m, maximaal 8 uur of meer (afhankelijk van het project), standaard 10 m.

- Vereist een waarde

#### `--interval`, `-i`

Het tijdinterval. De standaardwaarde is een verdeling van het bereik. U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimaal 1 m.

- Vereist een waarde

#### `--to`

De eindtijd. Tot nu toe is dat standaard het geval.

- Vereist een waarde

#### `--latest`, `-1`

Alleen het laatste enkele gegevenspunt weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--service`, `-s`

Filteren op service- of toepassingsnaam De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

#### `--type`

Filteren op servicetype (indien —service niet opgegeven). De versie is niet vereist. De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

#### `--tmp`

Het tijdelijke schijfgebruik van het rapport (toont kolommen: timestamp, de dienst, tmp_used, tmp_limit, tmp_percent, tmp_ipercent)

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: timestamp*, service*, used*, limit*, percent*, ipercent*, tmp_percent*, ilimit, used, tmp_ilimit, tmp_ipercent, tmp_iused, tmp_limit, tmp_limit, tmp_used, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `metrics:memory`

```bash
magento-cloud mem [-B|--bytes] [-r|--range RANGE] [-i|--interval INTERVAL] [--to TO] [-1|--latest] [-s|--service SERVICE] [--type TYPE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Geheugengebruik van een omgeving weergeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--bytes`, `-B`

Grootte in bytes weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--range`, `-r`

Het tijdbereik. Metriek wordt voor deze duur geladen tot de eindtijd (—to). U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimaal 5 m, maximaal 8 uur of meer (afhankelijk van het project), standaard 10 m.

- Vereist een waarde

#### `--interval`, `-i`

Het tijdinterval. De standaardwaarde is een verdeling van het bereik. U kunt eenheden opgeven: uren (h), minuten (m) of seconden (s). Minimaal 1 m.

- Vereist een waarde

#### `--to`

De eindtijd. Tot nu toe is dat standaard het geval.

- Vereist een waarde

#### `--latest`, `-1`

Alleen het laatste enkele gegevenspunt weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--service`, `-s`

Filteren op service- of toepassingsnaam De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

#### `--type`

Filteren op servicetype (indien —service niet opgegeven). De versie is niet vereist. De tekens % of * kunnen als jokerteken worden gebruikt.

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: timestamp*, service*, used*, limit*, percent*, type (* = default columns). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `mount:download`

```bash
magento-cloud mount:download [-a|--all] [-m|--mount MOUNT] [--target TARGET] [--source-path] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Bestanden downloaden van een berg, via resynchroniseren

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--all`, `-a`

Downloaden vanaf alle locaties

- Standaard: `false`
- Accepteert geen waarde

#### `--mount`, `-m`

De koppeling (als een pad dat relatief is ten opzichte van de toepassing)

- Vereist een waarde

#### `--target`

De map waarnaar bestanden worden gedownload. Als —all wordt gebruikt, zal de koppelingsweg worden toegevoegd

- Vereist een waarde

#### `--source-path`

Gebruik het bronpad van de koppeling (in plaats van het koppelingspad) als submap van het doel, wanneer —alles wordt gebruikt

- Standaard: `false`
- Accepteert geen waarde

#### `--delete`

Of vreemde bestanden in de doelmap moeten worden verwijderd

- Standaard: `false`
- Accepteert geen waarde

#### `--exclude`

Bestand(en) om uit te sluiten van downloaden (patroon)

- Standaard: `[]`
- Vereist een waarde

#### `--include`

Bestand(en) niet uit te sluiten (patroon)

- Standaard: `[]`
- Vereist een waarde

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--instance`, `-I`

Instantie-id

- Vereist een waarde


## `mount:list`

```bash
magento-cloud mounts [--paths] [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Een lijst met bevestigingen ophalen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--paths`

Alleen de koppelingspaden uitvoeren (één per regel)

- Standaard: `false`
- Accepteert geen waarde

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: definitie, pad. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--instance`, `-I`

Instantie-id

- Vereist een waarde


## `mount:upload`

```bash
magento-cloud mount:upload [--source SOURCE] [-m|--mount MOUNT] [--delete] [--exclude EXCLUDE] [--include INCLUDE] [--refresh] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-I|--instance INSTANCE]
```

Bestanden uploaden naar een koppelingsgebied, via opnieuw synchroniseren

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--source`

Een map met bestanden die moeten worden geüpload

- Vereist een waarde

#### `--mount`, `-m`

De koppeling (als een pad dat relatief is ten opzichte van de toepassing)

- Vereist een waarde

#### `--delete`

Of vreemde bestanden in de telling moeten worden verwijderd

- Standaard: `false`
- Accepteert geen waarde

#### `--exclude`

Bestand(en) om uit te sluiten van uploaden (patroon)

- Standaard: `[]`
- Vereist een waarde

#### `--include`

Bestand(en) niet uit te sluiten (patroon)

- Standaard: `[]`
- Vereist een waarde

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--instance`, `-I`

Instantie-id

- Vereist een waarde


## `operation:list`

```bash
magento-cloud ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Runtimebewerkingen weergeven in een omgeving

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--full`

Beperk de lengte van de opdracht niet tot de weergave. De standaardlimiet is 24 regels.

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: service*, naam*, start*, rol, stop (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `operation:run`

```bash
magento-cloud operation:run [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--worker WORKER] [-W|--no-wait] [--wait] [--] [<operation>]
```

Een bewerking uitvoeren op de omgeving

### Argumenten

#### `operation`

De naam van de bewerking

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--worker`

De naam van een worker

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `project:clear-build-cache`

```bash
magento-cloud project:clear-build-cache [-p|--project PROJECT]
```

De cache voor het samenstellen van projecten wissen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `project:get`

```bash
magento-cloud get [-e|--environment ENVIRONMENT] [--depth DEPTH] [--build] [-p|--project PROJECT] [--] [<project>] [<directory>]
```

Een project lokaal klonen

### Argumenten

#### `project`

Project-id


#### `directory`

De map waarnaar moet worden gekloond. Wordt standaard ingesteld op de projecttitel

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--environment`, `-e`

De milieu-id om te klonen. Wordt standaard ingesteld op de standaardinstelling van het project of de eerste beschikbare omgeving

- Vereist een waarde

#### `--depth`

Een ondiepe kloon maken: het aantal vastleggingen in de geschiedenis beperken

- Vereist een waarde

#### `--build`

Het project na het klonen maken

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `project:info`

```bash
magento-cloud project:info [--refresh] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<property>] [<value>]
```

Eigenschappen voor een project lezen of instellen

### Argumenten

#### `property`

De naam van de eigenschap


#### `value`

Een nieuwe waarde voor de eigenschap instellen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `project:list`

```bash
magento-cloud projects [--pipe] [--region REGION] [--title TITLE] [--my] [--refresh REFRESH] [--sort SORT] [--reverse] [--page PAGE] [-c|--count COUNT] [--format FORMAT] [--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT]
```

Een lijst met alle actieve projecten ophalen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--pipe`

Een eenvoudige lijst met project-id&#39;s uitvoeren. Hiermee schakelt u paginering uit.

- Standaard: `false`
- Accepteert geen waarde

#### `--region`

Filteren op gebied (exact overeenkomend)

- Vereist een waarde

#### `--title`

Filteren op titel (niet-hoofdlettergevoelig zoeken)

- Vereist een waarde

#### `--my`

Alleen de projecten weergeven die u bezit

- Standaard: `false`
- Accepteert geen waarde

#### `--refresh`

Of de lijst moet worden vernieuwd

- Standaard: `1`
- Vereist een waarde

#### `--sort`

Een eigenschap waarop u wilt sorteren

- Standaard: `title`
- Vereist een waarde

#### `--reverse`

Omgekeerde (aflopende) volgorde sorteren

- Standaard: `false`
- Accepteert geen waarde

#### `--page`

Paginanummer Dit laat paginering, ondanks configuratie of —count toe. Genegeerd als —pipe is opgegeven.

- Vereist een waarde

#### `--count`, `-c`

Het aantal projecten dat per pagina moet worden weergegeven. Gebruik 0 om paginering uit te schakelen. Genegeerd als —page is gespecificeerd.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`

Weer te geven kolommen. Beschikbare kolommen: id*, title*, region*, created_at, organisation_id, organisation_label, organisation_name, organisation_type, status (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `project:set-remote`

```bash
magento-cloud set-remote [<project>]
```

Het externe project instellen voor de huidige Git-opslagplaats

### Argumenten

#### `project`

Project-id

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `repo:cat`

```bash
magento-cloud repo:cat [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] <path>
```

Een bestand lezen in de gegevensopslagruimte van het project

### Argumenten

#### `path`

Het pad naar het bestand

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--commit`, `-c`

De commit SHA. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunten (^) of tilde (~) accepteren voor bovenliggende bewerkingen.

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `repo:ls`

```bash
magento-cloud repo:ls [-d|--directories] [-f|--files] [--git-style] [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```

Bestanden weergeven in de gegevensopslagruimte van het project

### Argumenten

#### `path`

Het pad naar een submap

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--directories`, `-d`

Alleen directory&#39;s tonen

- Standaard: `false`
- Accepteert geen waarde

#### `--files`, `-f`

Alleen bestanden tonen

- Standaard: `false`
- Accepteert geen waarde

#### `--git-style`

Stijl, uitvoer vergelijkbaar met &#39;git ls-tree&#39;

- Standaard: `false`
- Accepteert geen waarde

#### `--commit`, `-c`

De commit SHA. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunten (^) of tilde (~) accepteren voor bovenliggende bewerkingen.

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `repo:read`

```bash
magento-cloud read [-c|--commit COMMIT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<path>]
```

Een map of bestand lezen in de projectopslagplaats

### Argumenten

#### `path`

Het pad naar de map of het bestand

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--commit`, `-c`

De commit SHA. Dit kan ook achtervoegsels &quot;HEAD&quot;, en invoegpunten (^) of tilde (~) accepteren voor bovenliggende bewerkingen.

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `resources:build:get`

```bash
magento-cloud build-resources:get [-p|--project PROJECT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Bekijk bouwstijlmiddelen van een project

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: cpu, geheugen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `route:get`

```bash
magento-cloud route:get [--id ID] [-1|--primary] [-P|--property PROPERTY] [--refresh] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-i|--identity-file IDENTITY-FILE] [--] [<route>]
```

Gedetailleerde informatie over een route weergeven

### Argumenten

#### `route`

Originele URL van de route

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--id`

Een route-id om te selecteren

- Vereist een waarde

#### `--primary`, `-1`

Selecteer de primaire route

- Standaard: `false`
- Accepteert geen waarde

#### `--property`, `-P`

De weer te geven eigenschap

- Vereist een waarde

#### `--refresh`

Het geheime voorgeheugen van routes omzeilen

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

[ Vervangen optie, niet meer gebruikt ]

- Vereist een waarde

#### `--identity-file`, `-i`

[ Vervangen optie, niet meer gebruikt ]

- Vereist een waarde


## `route:list`

```bash
magento-cloud routes [--refresh] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--] [<environment>]
```

Alle routes weergeven voor een omgeving

### Argumenten

#### `environment`

De milieu-id

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--refresh`

Het geheime voorgeheugen van routes omzeilen

- Standaard: `false`
- Accepteert geen waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: route*, type*, to*, url (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `self:install`

```bash
magento-cloud self:install [--shell-type SHELL-TYPE]
```

CLI-configuratiebestanden installeren of bijwerken

```
This command automatically installs shell configuration for the Magento Cloud CLI,
adding autocompletion support and handy aliases. Bash and ZSH are supported.
```

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--shell-type`

Het shell-type voor automatisch aanvullen (bash of zsh)

- Vereist een waarde


## `self:update`

```bash
magento-cloud update [--no-major] [--unstable] [--manifest MANIFEST] [--current-version CURRENT-VERSION] [--timeout TIMEOUT]
```

CLI bijwerken naar de nieuwste versie

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--no-major`

Alleen bijwerken tussen kleine versies of patchversies

- Standaard: `false`
- Accepteert geen waarde

#### `--unstable`

Bijwerken naar een nieuwe, instabiele versie, indien beschikbaar

- Standaard: `false`
- Accepteert geen waarde

#### `--manifest`

De locatie van het manifestbestand overschrijven

- Vereist een waarde

#### `--current-version`

De huidige versie overschrijven

- Vereist een waarde

#### `--timeout`

Een time-out voor de versiecontrole

- Standaard: `30`
- Vereist een waarde


## `service:list`

```bash
magento-cloud services [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

De diensten van de lijst in het project

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--pipe`

Alleen een lijst met servicenamen uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: schijf, naam, grootte, type. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `service:mongo:dump`

```bash
magento-cloud mongodump [-c|--collection COLLECTION] [-z|--gzip] [-o|--stdout] [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Een binaire archiefstortplaats maken van gegevens van MongoDB

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--collection`, `-c`

De inzameling aan stortplaats

- Vereist een waarde

#### `--gzip`, `-z`

De stortplaats comprimeren met gzip

- Standaard: `false`
- Accepteert geen waarde

#### `--stdout`, `-o`

Uitvoeren naar STDOUT in plaats van een bestand

- Standaard: `false`
- Accepteert geen waarde

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `service:mongo:export`

```bash
magento-cloud mongoexport [-c|--collection COLLECTION] [--jsonArray] [--type TYPE] [-f|--fields FIELDS] [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Gegevens exporteren uit MongoDB

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--collection`, `-c`

De verzameling die u wilt exporteren

- Vereist een waarde

#### `--jsonArray`

Gegevens exporteren als één JSON-array

- Standaard: `false`
- Accepteert geen waarde

#### `--type`

Het exporttype, bijvoorbeeld &quot;csv&quot;

- Vereist een waarde

#### `--fields`, `-f`

De velden die u wilt exporteren

- Standaard: `[]`
- Vereist een waarde

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `service:mongo:restore`

```bash
magento-cloud mongorestore [-c|--collection COLLECTION] [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Herstel een binaire archiefstortplaats van gegevens in MongoDB

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--collection`, `-c`

De te herstellen verzameling

- Vereist een waarde

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `service:mongo:shell`

```bash
magento-cloud mongo [--eval EVAL] [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

De shell van MongoDB gebruiken

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--eval`

Een JavaScript-fragment aan de shell doorgeven

- Vereist een waarde

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `service:redis-cli`

```bash
magento-cloud redis [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]...
```

Toegang tot de CLI van Redis

### Argumenten

#### `args`

Argumenten om toe te voegen aan de opdracht redis-cli

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `service:valkey-cli`

```bash
magento-cloud valkey [-r|--relationship RELATIONSHIP] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--] [<args>]...
```

Toegang tot de Valkey CLI

### Argumenten

#### `args`

Argumenten die moeten worden toegevoegd aan de opdracht valkey-cli

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `snapshot:create`

```bash
magento-cloud backup [--live] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<environment>]
```

Een opname maken van een omgeving

### Argumenten

#### `environment`

Het milieu

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--live`

Actieve momentopname: stop de omgeving niet. Als deze optie is ingesteld, blijft de omgeving actief en wordt deze opengesteld voor verbindingen tijdens de momentopname. Dit vermindert onderbreking, met het risico om gegevens in een inconsistente staat te steunen.

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `snapshot:delete`

```bash
magento-cloud snapshot:delete [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<id>]
```

Een omgevingsopname verwijderen

### Argumenten

#### `id`

De id van de momentopname. Vereist in niet-interactieve modus.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `snapshot:get`

```bash
magento-cloud snapshot:get [-P|--property PROPERTY] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--date-fmt DATE-FMT] [--] [<id>]
```

Een omgevingsmomentopname weergeven

### Argumenten

#### `id`

De id van de momentopname. Wordt standaard ingesteld op de meest recente.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De eigenschap die moet worden weergegeven.

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde


## `snapshot:list`

```bash
magento-cloud snapshots [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [--date-fmt DATE-FMT] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Beschikbare momentopnamen van een omgeving weergeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `snapshot:restore`

```bash
magento-cloud snapshot:restore [--target TARGET] [--branch-from BRANCH-FROM] [--no-code] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<snapshot>]
```

Een omgevingsmomentopname herstellen

### Argumenten

#### `snapshot`

De id van de momentopname. Wordt standaard ingesteld op de meest recente

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--target`

De omgeving die moet worden hersteld. Wordt standaard ingesteld op de huidige omgeving van de momentopname

- Vereist een waarde

#### `--branch-from`

Als —target nog niet bestaat, specificeert dit de ouder van het nieuwe milieu

- Vereist een waarde

#### `--no-code`

Geen code, alleen gegevens herstellen.

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `source-operation:list`

```bash
magento-cloud source-ops [--full] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Bronbewerkingen in een omgeving weergeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--full`

Beperk de lengte van de opdracht niet tot de weergave. De standaardlimiet is 24 regels.

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: app, command, operation. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `source-operation:run`

```bash
magento-cloud source-operation:run [--variable VARIABLE] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<operation>]
```

Een bronbewerking uitvoeren

### Argumenten

#### `operation`

De naam van de bewerking

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--variable`

Een variabele om tijdens de verrichting, in het formaattype :name=value te plaatsen

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `ssh-cert:load`

```bash
magento-cloud ssh-cert:load [--refresh-only] [--new] [--new-key]
```

Een SSH-certificaat genereren

```
This command checks if a valid SSH certificate is present, and generates a
new one if necessary.

Certificates allow you to make SSH connections without having previously
uploaded a public key. They are more secure than keys and they allow for
other features.

Normally the certificate is loaded automatically during login, or when
making an SSH connection. So this command is seldom needed.

If you want to set up certificates without login and without an SSH-related
command, for example if you are writing a script that uses an API token via
an environment variable, then you would probably want to run this command
explicitly. For unattended scripts, remember to turn off interaction via
--yes or the MAGENTO_CLOUD_CLI_NO_INTERACTION environment variable.
```

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--refresh-only`

Vernieuw slechts het certificaat, indien nodig (schrijf geen SSH config)

- Standaard: `false`
- Accepteert geen waarde

#### `--new`

Vernieuwen van certificaat forceren

- Standaard: `false`
- Accepteert geen waarde

#### `--new-key`

Een nieuw sleutelpaar forceren dat moet worden gegenereerd

- Standaard: `false`
- Accepteert geen waarde


## `ssh-key:add`

```bash
magento-cloud ssh-key:add [--name NAME] [--] [<path>]
```

Een nieuwe SSH-toets toevoegen

```
This command lets you add an SSH key to your account. It can generate a key using OpenSSH.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Argumenten

#### `path`

Het pad naar een bestaande SSH-openbare sleutel

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--name`

Een naam om de sleutel te identificeren

- Vereist een waarde


## `ssh-key:delete`

```bash
magento-cloud ssh-key:delete [<id>]
```

Een SSH-toets verwijderen

```
This command lets you delete SSH keys from your account.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Argumenten

#### `id`

De id van de SSH-toets die moet worden verwijderd

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `ssh-key:list`

```bash
magento-cloud ssh-keys [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Een lijst met SSH-sleutels in uw account ophalen

```
This command lets you list SSH keys in your account.

Notice:
SSH keys are no longer needed by default, as SSH certificates are supported.
Certificates offer more security than keys.

To load or check your SSH certificate, run: magento-cloud ssh-cert:load
```

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: id*, title*, path*, vingerafdruk (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `subscription:info`

```bash
magento-cloud subscription:info [-s|--id ID] [--date-fmt DATE-FMT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [--] [<property>] [<value>]
```

Abonnementseigenschappen lezen of wijzigen

### Argumenten

#### `property`

De naam van de eigenschap


#### `value`

Een nieuwe waarde voor de eigenschap instellen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--id`, `-s`

Abonnement-id

- Vereist een waarde

#### `--date-fmt`

De datumnotatie (als een PHP-datumnotatietekenreeks)

- Standaard: `c`
- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `tunnel:close`

```bash
magento-cloud tunnel:close [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

SSH-tunnels sluiten

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--all`, `-a`

Alle tunnels sluiten

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `tunnel:info`

```bash
magento-cloud tunnel:info [-P|--property PROPERTY] [-c|--encode] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

Relatie-informatie voor SSH-tunnels weergeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

De relatie-eigenschap die moet worden weergegeven

- Vereist een waarde

#### `--encode`, `-c`

Uitvoer als base64-gecodeerde JSON

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `tunnel:list`

```bash
magento-cloud tunnels [-a|--all] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Lijst SSH-tunnels

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--all`, `-a`

Alle tunnels weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: poort*, project*, omgeving*, app*, relatie*, url (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `tunnel:open`

```bash
magento-cloud tunnel:open [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP]
```

SSH-tunnels openen naar de relaties van een app

```
This command opens SSH tunnels to all of the relationships of an application.

Connections can then be made to the application's services as if they were
local, for example a local MySQL client can be used, or the Solr web
administration endpoint can be accessed through a local browser.

This command requires the posix and pcntl PHP extensions (as multiple
background CLI processes are created to keep the SSH tunnels open). The
tunnel:single command can be used on systems without these
extensions.
```

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--gateway-ports`, `-g`

Verre gastheren toestaan om met lokale door:sturen havens te verbinden

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde


## `tunnel:single`

```bash
magento-cloud tunnel:single [--port PORT] [-g|--gateway-ports] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-A|--app APP] [-r|--relationship RELATIONSHIP]
```

Eén SSH-tunnel openen voor een app-relatie

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--port`

De lokale poort

- Vereist een waarde

#### `--gateway-ports`, `-g`

Verre gastheren toestaan om met lokale door:sturen havens te verbinden

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--app`, `-A`

De externe toepassingsnaam

- Vereist een waarde

#### `--relationship`, `-r`

De de dienstverhouding om te gebruiken

- Vereist een waarde


## `user:add`

```bash
magento-cloud user:add [-r|--role ROLE] [--force-invite] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```

Een gebruiker toevoegen aan het project

### Argumenten

#### `email`

Het e-mailadres van de gebruiker

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--role`, `-r`

De projectrol van de gebruiker (&#39;admin&#39; of &#39;viewer&#39;) of de rol van het omgevingstype (bijvoorbeeld &#39;staging :contributor&#39; of &#39;production :viewer&#39;). Als u een gebruiker uit een omgevingstype wilt verwijderen, stelt u de rol in op Geen. De %- of *-tekens kunnen worden gebruikt als een jokerteken voor het omgevingstype, bijvoorbeeld &#39;% :viewer&#39;, om de gebruiker de rol &#39;viewer&#39; te geven op alle typen. De rol kan worden afgekort, bijvoorbeeld &quot;productie :v&quot;.

- Standaard: `[]`
- Vereist een waarde

#### `--force-invite`

Een uitnodiging verzenden, zelfs als er al een is verzonden

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `user:delete`

```bash
magento-cloud user:delete [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] <email>
```

Een gebruiker verwijderen uit het project

### Argumenten

#### `email`

Het e-mailadres van de gebruiker

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `user:get`

```bash
magento-cloud user:get [-l|--level LEVEL] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [-r|--role ROLE] [--] [<email>]
```

Rollen van gebruikers weergeven

### Argumenten

#### `email`

Het e-mailadres van de gebruiker

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--level`, `-l`

Rolniveau (&#39;project&#39; of &#39;milieu&#39;)

- Vereist een waarde

#### `--pipe`

De rol uitvoeren die moet worden stopgezet (nadat eventuele wijzigingen zijn aangebracht)

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde

#### `--role`, `-r`

[ Afgekeurd: gebruik gebruiker :update om de rol(s) van een gebruiker te veranderen ]

- Vereist een waarde


## `user:list`

```bash
magento-cloud users [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT]
```

Projectgebruikers weergeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: email*, name*, role*, id*, allowed_at, update_at (* = standaardkolommen). Het teken &quot;+&quot; kan worden gebruikt als tijdelijke aanduiding voor de standaardkolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde


## `user:update`

```bash
magento-cloud user:update [-r|--role ROLE] [-p|--project PROJECT] [-W|--no-wait] [--wait] [--] [<email>]
```

Gebruikersrol(s) voor een project bijwerken

### Argumenten

#### `email`

Het e-mailadres van de gebruiker

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--role`, `-r`

De projectrol van de gebruiker (&#39;admin&#39; of &#39;viewer&#39;) of de rol van het omgevingstype (bijvoorbeeld &#39;staging :contributor&#39; of &#39;production :viewer&#39;). Als u een gebruiker uit een omgevingstype wilt verwijderen, stelt u de rol in op Geen. De %- of *-tekens kunnen worden gebruikt als een jokerteken voor het omgevingstype, bijvoorbeeld &#39;% :viewer&#39;, om de gebruiker de rol &#39;viewer&#39; te geven op alle typen. De rol kan worden afgekort, bijvoorbeeld &quot;productie :v&quot;.

- Standaard: `[]`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `variable:create`

```bash
magento-cloud variable:create [-u|--update] [-l|--level LEVEL] [--name NAME] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--prefix PREFIX] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] [<name>]
```

Een variabele maken

### Argumenten

#### `name`

De variabelenaam

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--update`, `-u`

De variabele bijwerken als deze al bestaat

- Standaard: `false`
- Accepteert geen waarde

#### `--level`, `-l`

Het niveau waarop de variabele moet worden ingesteld (&#39;project&#39; of &#39;omgeving&#39;)

- Vereist een waarde

#### `--name`

De variabelenaam

- Vereist een waarde

#### `--value`

De waarde van de variabele

- Vereist een waarde

#### `--json`

Geeft aan of de waarde van de variabele JSON-indeling heeft

- Standaard: `false`
- Vereist een waarde

#### `--sensitive`

Of de waarde van de variabele gevoelig is

- Standaard: `false`
- Vereist een waarde

#### `--prefix`

Het voorvoegsel van de variabelenaam dat het type kan bepalen, bijvoorbeeld &#39;env&#39;. Alleen van toepassing als de naam nog geen voorvoegsel bevat. (bijvoorbeeld &quot;none&quot; of &quot;env:&quot;)

- Standaard: `none`
- Vereist een waarde

#### `--enabled`

Of de variabele op het milieu zou moeten worden toegelaten

- Standaard: `true`
- Vereist een waarde

#### `--inheritable`

Of de variabele overerfbaar is door onderliggende omgevingen

- Standaard: `true`
- Vereist een waarde

#### `--visible-build`

Of de variabele zichtbaar zou moeten zijn in bouwstijltijd

- Vereist een waarde

#### `--visible-runtime`

Of de variabele zichtbaar moet zijn bij uitvoering

- Standaard: `true`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `variable:delete`

```bash
magento-cloud variable:delete [-l|--level LEVEL] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Een variabele verwijderen

### Argumenten

#### `name`

De variabelenaam

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--level`, `-l`

Variabel niveau (&#39;project&#39;, &#39;milieu&#39;, &#39;p&#39; of &#39;e&#39;)

- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `variable:get`

```bash
magento-cloud vget [-P|--property PROPERTY] [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--pipe] [--] [<name>]
```

Een variabele weergeven

### Argumenten

#### `name`

De naam van de variabele

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--property`, `-P`

Eén variabele-eigenschap weergeven

- Vereist een waarde

#### `--level`, `-l`

Variabel niveau (&#39;project&#39;, &#39;milieu&#39;, &#39;p&#39; of &#39;e&#39;)

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--pipe`

[ Vervangen optie ] Output de veranderlijke slechts waarde

- Standaard: `false`
- Accepteert geen waarde


## `variable:list`

```bash
magento-cloud variables [-l|--level LEVEL] [--format FORMAT] [-c|--columns COLUMNS] [--no-header] [-p|--project PROJECT] [-e|--environment ENVIRONMENT]
```

Lijstvariabelen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--level`, `-l`

Variabel niveau (&#39;project&#39;, &#39;milieu&#39;, &#39;p&#39; of &#39;e&#39;)

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: is_enabled, level, name, value. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde


## `variable:update`

```bash
magento-cloud variable:update [--allow-no-change] [-l|--level LEVEL] [--value VALUE] [--json JSON] [--sensitive SENSITIVE] [--enabled ENABLED] [--inheritable INHERITABLE] [--visible-build VISIBLE-BUILD] [--visible-runtime VISIBLE-RUNTIME] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [-W|--no-wait] [--wait] [--] <name>
```

Een variabele bijwerken

### Argumenten

#### `name`

De variabelenaam

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--allow-no-change`

Retourneren geslaagd (nulafsluitcode) als er geen wijzigingen zijn opgegeven

- Standaard: `false`
- Accepteert geen waarde

#### `--level`, `-l`

Variabel niveau (&#39;project&#39;, &#39;milieu&#39;, &#39;p&#39; of &#39;e&#39;)

- Vereist een waarde

#### `--value`

De waarde van de variabele

- Vereist een waarde

#### `--json`

Geeft aan of de waarde van de variabele JSON-indeling heeft

- Standaard: `false`
- Vereist een waarde

#### `--sensitive`

Of de waarde van de variabele gevoelig is

- Standaard: `false`
- Vereist een waarde

#### `--enabled`

Of de variabele op het milieu zou moeten worden toegelaten

- Standaard: `true`
- Vereist een waarde

#### `--inheritable`

Of de variabele overerfbaar is door onderliggende omgevingen

- Standaard: `true`
- Vereist een waarde

#### `--visible-build`

Of de variabele zichtbaar zou moeten zijn in bouwstijltijd

- Vereist een waarde

#### `--visible-runtime`

Of de variabele zichtbaar moet zijn bij uitvoering

- Standaard: `true`
- Vereist een waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--no-wait`, `-W`

Wacht niet tot de bewerking is voltooid

- Standaard: `false`
- Accepteert geen waarde

#### `--wait`

Wacht tot de bewerking is voltooid (standaardwaarde)

- Standaard: `false`
- Accepteert geen waarde


## `worker:list`

```bash
magento-cloud workers [--refresh] [--pipe] [-p|--project PROJECT] [-e|--environment ENVIRONMENT] [--format FORMAT] [-c|--columns COLUMNS] [--no-header]
```

Een lijst met alle geïmplementeerde workers ophalen

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--refresh`

Of de cache moet worden vernieuwd

- Standaard: `false`
- Accepteert geen waarde

#### `--pipe`

Alleen een lijst met namen van workers uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--project`, `-p`

De project-id of URL

- Vereist een waarde

#### `--environment`, `-e`

De milieu-id. &quot;.&quot; gebruiken om de standaardomgeving van het project te selecteren.

- Vereist een waarde

#### `--format`

De uitvoerindeling: table, csv, tsv of plain

- Standaard: `table`
- Vereist een waarde

#### `--columns`, `-c`

Weer te geven kolommen. Beschikbare kolommen: opdrachten, naam, type. De tekens % of * kunnen als jokerteken worden gebruikt. Waarden kunnen worden gesplitst met komma&#39;s (bv. &quot;a,b,c&quot;) en/of witruimte.

- Standaard: `[]`
- Vereist een waarde

#### `--no-header`

De tabelkoptekst niet uitvoeren

- Standaard: `false`
- Accepteert geen waarde
