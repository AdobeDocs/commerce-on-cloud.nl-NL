---
source-git-commit: 11d0e86ad4633d9c4232474b9921ed491f285969
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---
# Gereedschappen

**Versie**: 2002.2.8

Deze verwijzing bevat 34 opdrachten die beschikbaar zijn via het opdrachtregelprogramma van `ece-tools` .
De eerste lijst wordt automatisch gegenereerd met de opdracht `ece-tools list` in Adobe Commerce op de cloud-infrastructuur.

## Algemeen

Deze verwijzing wordt gegenereerd op basis van de toepassingscodebase. Om de inhoud te veranderen, _geef ons terugkoppelen_ (vind de verbinding bij het hogere recht). Voor bijdragerichtsnoeren, zie {de Bijdragen van de Code 0} [.](https://developer.adobe.com/commerce/contributor/guides/code-contributions/)

### Algemene opties

#### `--help`, `-h`

Help weergeven voor de opgegeven opdracht. Wanneer geen bevel vertoningshulp voor het lijstbevel wordt gegeven

- Standaard: `false`
- Accepteert geen waarde

#### `--silent`

Geen bericht uitvoeren

- Standaard: `false`
- Accepteert geen waarde

#### `--quiet`, `-q`

Alleen fouten worden weergegeven. Alle andere uitvoer wordt onderdrukt

- Standaard: `false`
- Accepteert geen waarde

#### `--verbose`, `-v|-vv|-vvv`

Verhoog de breedheid van berichten: 1 voor normale output, 2 voor meer uitgebreide output en 3 voor zuivert

- Standaard: `false`
- Accepteert geen waarde

#### `--version`, `-V`

Deze toepassingsversie weergeven

- Standaard: `false`
- Accepteert geen waarde

#### `--ansi`

ANSI-uitvoer forceren (of uitschakelen —no-ansi)

- Accepteert geen waarde

#### `--no-ansi`

De optie &quot;—ansi&quot; negeren

- Accepteert geen waarde

#### `--no-interaction`, `-n`

Geen interactieve vraag stellen

- Standaard: `false`
- Accepteert geen waarde


## `_complete`

```bash
ece-tools _complete [-s|--shell SHELL] [-i|--input INPUT] [-c|--current CURRENT] [-a|--api-version API-VERSION] [-S|--symfony SYMFONY]
```

Interne opdracht voor suggesties voor shell-voltooiing

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--shell`, `-s`

Het schelpdiertype (&quot;bash&quot;, &quot;fish&quot;, &quot;zsh&quot;)

- Vereist een waarde

#### `--input`, `-i`

Een array van invoertokens (bv. COMP_WORDS of argv)

- Standaard: `[]`
- Vereist een waarde

#### `--current`, `-c`

De index van de &quot;input&quot;-array waarin de cursor zich bevindt (bijvoorbeeld COMP_CWORD)

- Vereist een waarde

#### `--api-version`, `-a`

De API-versie van het voltooiingsscript

- Vereist een waarde

#### `--symfony`, `-S`

verouderd

- Vereist een waarde


## `build`

```bash
ece-tools build
```

Builds-toepassing.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `completion`

```bash
ece-tools completion [--debug] [--] [<shell>]
```

Het shell-voltooiingsscript dumpen

```
The completion command dumps the shell completion script required
to use shell autocompletion (currently, bash, fish, zsh completion are supported).

Static installation
-------------------

Dump the script to a global completion file and restart your shell:

    bin/ece-tools completion  | sudo tee /etc/bash_completion.d/ece-tools

Or dump the script to a local file and source it:

    bin/ece-tools completion  > completion.sh

    # source the file whenever you use the project
    source completion.sh

    # or add this line at the end of your "~/.bashrc" file:
    source /path/to/completion.sh

Dynamic installation
--------------------

Add this to the end of your shell configuration file (e.g. "~/.bashrc"):

    eval "$(/var/jenkins/workspace/gendocs-ece-tools-cli/bin/ece-tools completion )"
```

### Argumenten

#### `shell`

Het shell type (bijvoorbeeld &quot;bash&quot;), de waarde van &quot;$SHELL&quot; env var zal worden gebruikt als dit niet wordt gegeven

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--debug`

Tik op het logbestand voor foutopsporing bij voltooien

- Standaard: `false`
- Accepteert geen waarde


## `db-dump`

```bash
ece-tools db-dump [-d|--remove-definers] [-a|--dump-directory DUMP-DIRECTORY] [--] [<databases>...]
```

Maakt databaseback-ups.

### Argumenten

#### `databases`

Databases voor back-up. Beschikbare Waarden: [ belangrijkste citaatverkoop ]. Als de argumentwaarde niet wordt gespecificeerd, zullen de gegevensbestandsteunen worden gecreeerd gebruikend de geloofsbrieven die in `MAGENTO_CLOUD_RELATIONSHIP` worden opgeslagen omgevingsvariabele of/en het `stage.deploy.DATABASE_CONFIGURATION` bezit van het .magento.env.yaml configuratiedossier.

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--remove-definers`, `-d`

Verwijder definities uit de gegevensbestandstortplaats

- Standaard: `false`
- Accepteert geen waarde

#### `--dump-directory`, `-a`

Alternatieve directory gebruiken voor opslaan van dump

- Vereist een waarde


## `deploy`

```bash
ece-tools deploy
```

Implementeert de toepassing.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `help`

```bash
ece-tools help [--format FORMAT] [--raw] [--] [<command_name>]
```

Help weergeven voor een opdracht

```
The help command displays help for a given command:

  bin/ece-tools help list

You can also output the help in other formats by using the --format option:

  bin/ece-tools help --format=xml list

To display the list of available commands, please use the list command.
```

### Argumenten

#### `command_name`

De opdrachtnaam

- Standaard: `help`

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--format`

De uitvoerindeling (txt, xml, json of md)

- Standaard: `txt`
- Vereist een waarde

#### `--raw`

Help bij de opdracht Uitvoeren

- Standaard: `false`
- Accepteert geen waarde


## `list`

```bash
ece-tools list [--raw] [--format FORMAT] [--short] [--] [<namespace>]
```

Lijstopdrachten

```
The list command lists all commands:

  bin/ece-tools list

You can also display the commands for a specific namespace:

  bin/ece-tools list test

You can also output the information in other formats by using the --format option:

  bin/ece-tools list --format=xml

It's also possible to get raw list of commands (useful for embedding command runner):

  bin/ece-tools list --raw
```

### Argumenten

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

#### `--short`

Om het beschrijven van de argumenten van bevelen over te slaan

- Standaard: `false`
- Accepteert geen waarde


## `patch`

```bash
ece-tools patch
```

Hiermee past u aangepaste patches toe.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `post-deploy`

```bash
ece-tools post-deploy
```

Voert uit na plaatsingsverrichtingen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `run`

```bash
ece-tools run <scenario>...
```

Voer scenario(s) uit.

### Argumenten

#### `scenario`

Scenario(s)

- Standaard: `[]`
- Vereist

- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `backup:list`

```bash
ece-tools backup:list
```

Hiermee geeft u de lijst met back-upbestanden weer.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `backup:restore`

```bash
ece-tools backup:restore [-f|--force] [--file [FILE]]
```

Belangrijke configuratiebestanden herstellen. De steun van de looppas :list om de lijst van reservedossiers te tonen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--force`, `-f`

Bestaande bestanden overschrijven tijdens het herstellen van een back-up

- Standaard: `false`
- Accepteert geen waarde

#### `--file`

Een specifiek pad voor bestandsherstel

- Accepteert een waarde


## `build:generate`

```bash
ece-tools build:generate
```

Hiermee worden alle benodigde bestanden gegenereerd voor het samenstellen van het werkgebied.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `build:transfer`

```bash
ece-tools build:transfer
```

Gegenereerde bestanden worden overgebracht naar de init-map.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `cloud:config:create`

```bash
ece-tools cloud:config:create <configuration>
```

Maakt een `.magento.env.yaml` -bestand met de opgegeven configuratie van variabelen voor samenstellen, implementeren en achteraf implementeren. Hiermee overschrijft u een bestaand `.magento.env.yaml` -bestand.

### Argumenten

#### `configuration`

Configuratie in JSON-indeling

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `cloud:config:update`

```bash
ece-tools cloud:config:update <configuration>
```

Werkt het bestaande `.magento.env.yaml` dossier met de gespecificeerde configuratie bij. Maakt een `.magento.env.yaml` -bestand als dit niet bestaat.

### Argumenten

#### `configuration`

Configuratie in JSON-indeling

- Vereist

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `cloud:config:validate`

```bash
ece-tools cloud:config:validate
```

Valideert het configuratiebestand `.magento.env.yaml`

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `config:dump`

```bash
ece-tools config:dumpdump
```

Vorm van de pomp voor statische inhoudsplaatsing.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `cron:disable`

```bash
ece-tools cron:disable
```

Alle Magento-snijprocessen uitschakelen en alle actieve processen beëindigen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `cron:enable`

```bash
ece-tools cron:enable
```

Hiermee schakelt u Magento-snijprocessen in.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `cron:kill`

```bash
ece-tools cron:kill
```

Beëindigt alle Magento-snijprocessen.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `cron:unlock`

```bash
ece-tools cron:unlock [--job-code [JOB-CODE]]
```

Ontgrendel de banen van de kroon die in &quot;lopende&quot;staat bleven.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--job-code`

Taakcode uitsnijden die moet worden ontgrendeld.

- Standaard: `[]`
- Accepteert meerdere waarden


## `dev:generate:schema-error`

```bash
ece-tools dev:generate:schema-error
```

Genereert het bestand dist/error-codes.md uit het bestand schema.error.yaml.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `dev:git:update-composer`

```bash
ece-tools dev:git:update-composer
```

Werkt composer bij voor implementatie vanuit de it.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `env:config:show`

```bash
ece-tools env:config:show [<variable>...]
```

Gecodeerde omgevingsvariabelen voor cloudconfiguratie weergeven.

### Argumenten

#### `variable`

Te tonen omgevingsvariabelen, mogelijke opties: services, routes, variabelen

- Standaard: `[]`
- Array

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `error:show`

```bash
ece-tools error:show [-j|--json] [--] [<error-code>]
```

Hier wordt informatie weergegeven over fout-id of informatie over alle fouten van de laatste implementatie.

### Argumenten

#### `error-code`

Foutcode: als er geen informatie over de opdrachtweergave wordt doorgegeven over alle fouten van de laatste implementatie

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).

#### `--json`, `-j`

Wordt gebruikt voor het ophalen van resultaten in de JSON-indeling

- Standaard: `false`
- Accepteert geen waarde


## `module:refresh`

```bash
ece-tools module:refresh
```

Verfrist de configuratie om nieuw toegevoegde modules toe te laten.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `schema:generate`

```bash
ece-tools schema:generate
```

Genereert het schema *.dist-bestand.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `wizard:ideal-state`

```bash
ece-tools wizard:ideal-state
```

Verifieert ideale staat van configuratie.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `wizard:master-slave`

```bash
ece-tools wizard:master-slave
```

Verifieert master-slave configuratie.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `wizard:scd-on-build`

```bash
ece-tools wizard:scd-on-build
```

Verifieert SCD bij bouwstijlconfiguratie.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `wizard:scd-on-demand`

```bash
ece-tools wizard:scd-on-demand
```

Verifieert SCD op bestelling configuratie.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `wizard:scd-on-deploy`

```bash
ece-tools wizard:scd-on-deploy
```

Verifieert SCD bij opstellen configuratie.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).


## `wizard:split-db-state`

```bash
ece-tools wizard:split-db-state
```

Controleert de mogelijkheid om DB te splitsen en of DB al gesplitst was of niet.

### Opties

Voor globale opties, zie [ Globale opties ](#global-options).
