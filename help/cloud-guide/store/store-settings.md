---
title: Beheer van winkelconfiguratie
description: Leer hoe u de configuratie-instellingen van de winkel in alle Adobe Commerce kunt beheren en synchroniseren in omgevingen met cloudinfrastructuren.
feature: Cloud, Configuration, SCD
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 0%

---

# Beheer van winkelconfiguratie

De standaardconfiguraties voor uw opslag worden opgeslagen in een `config.xml` voor de aangewezen module. Wanneer u de instellingen wijzigt in Commerce Admin of de CLI-opdracht `bin/magento config:set` , worden de wijzigingen weerspiegeld in de kerndatabase, met name in de `core_config_data` -tabel. Deze instellingen overschrijven de standaardconfiguraties die in het `config.xml` -bestand zijn opgeslagen.

De montages van de opslag, die naar de configuraties in Admin **verwijzen Slaat** > **Montages** > **de sectie van de Configuratie**, worden opgeslagen in de dossiers van de plaatsingsconfiguratie die op het type van configuratie worden gebaseerd:

- `app/etc/config.php` - configuratie-instellingen voor winkels, websites, modules of extensies, statische optimalisatie van bestanden en systeemwaarden met betrekking tot de implementatie van statische inhoud. Zie de {[&#128279;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-configphp.html) referentie 0} config.php in de _Gids van de Configuratie_.
- `app/etc/env.php` - waarden voor systeem-specifieke met voeten treedt en gevoelige montages die _NIET_ in broncontrole zouden moeten worden opgeslagen. Zie [ env.php verwijzing ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html) in de _Gids van de Configuratie_.

>[!NOTE]
>
>Omdat Adobe Commerce op wolkeninfrastructuur slechts de productie en onderhoudswijzen steunt, is de **Geavanceerde** > **sectie van de Ontwikkelaar** niet toegankelijk in Admin. U moet {de voorrechten van Admin van 0} milieu [&#128279;](../project/user-access.md) hebben om de taken van het configuratiebeheer te voltooien.  U kunt extra montages vormen gebruikend [ milieuvariabelen ](../environment/configure-env-yaml.md).

Het beheer van de configuratie verstrekt een manier om verenigbare opslagmontages over uw milieu&#39;s met minimale onderbreking op te stellen gebruikend de plaatsing van de Pijpleiding. Adobe Commerce op het project van de wolkeninfrastructuur omvat de bouwstijlserver, bouwt en stelt manuscripten, en plaatsingsmilieu&#39;s op die met de [ strategie van de pijpleidingsplaatsing ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) in mening worden ontworpen.

## Configuratieoverschrijvingsschema

Alle systeemconfiguraties worden ingesteld tijdens de bouw- en implementatiefasen volgens het volgende overschrijfschema:

1. Als een omgevingsvariabele bestaat, gebruikt u de aangepaste configuratie en negeert u de standaardconfiguratie.
1. Als een milieuvariabele niet bestaat, gebruik de configuratie van een `MAGENTO_CLOUD_RELATIONSHIPS` naam-waarde paar in het [`.magento.app.yaml` dossier ](../application/configure-app-yaml.md). De standaardconfiguratie negeren.
1. Als een omgevingsvariabele niet bestaat en `MAGENTO_CLOUD_RELATIONSHIPS` geen naam-waardepaar bevat, verwijdert u alle aangepaste configuratie en gebruikt u de waarden uit de standaardconfiguratie.

Samengevat overschrijven omgevingsvariabelen alle andere waarden.

>[!TIP]
>
>Zie [ het beheer van de Configuratie ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/deployment/technical-details.html) in de _gids van de Configuratie_ voor meer over de opheffingsregeling voor pijpleidingsplaatsing.

Als het zelfde plaatsen in veelvoudige plaatsen wordt gevormd, baseert de toepassing zich op de volgende configuratiehiërarchie om te bepalen welke waarde op het milieu van toepassing is:

| Prioriteit | Configuratie <br> Methode | Beschrijving |
| -------- | ------------------------ | ----------- |
| 1 | [!DNL Cloud Console]<br> omgevingsvariabelen | De waarden die van het _lusje van Variabelen_ van milieuconfiguratie in [!DNL Cloud Console] worden toegevoegd. Geef hier waarden op voor gevoelige of omgevingspecifieke configuraties. De hier opgegeven instellingen kunnen niet worden bewerkt via de beheerder. Zie [ de configuratievariabelen van het Milieu ](../project/overview.md#configure-environment). |
| 2 | `.magento.app.yaml` | Waarden toegevoegd in de sectie `variables` van het `.magento.app.yaml` -bestand. Geef hier waarden op voor een consistente configuratie in alle omgevingen. **specificeer geen gevoelige waarden in het `.magento.app.yaml` dossier.** zie [ montages van de Toepassing ](../application/configure-app-yaml.md). |
| 3 | `app/etc/env.php` | Hier opgeslagen configuratiewaarden die specifiek zijn voor het milieu, worden toegevoegd met de opdracht `app:config:dump` . Plaats de systeem-specifieke en gevoelige waarden gebruikend omgevingsvariabelen of CLI. Zie [ Gevoelige gegevens ](#sensitive-data). Het `env.php` dossier is **niet** inbegrepen in broncontrole. |
| 4 | `app/etc/config.php` | Waarden die hier zijn opgeslagen, worden toegevoegd met de opdracht `app:config:dump` . De gedeelde configuratiewaarden worden toegevoegd aan `config.php`. Stel de gedeelde configuratie in via de beheerfunctie of via de CLI. Het `config.php` -bestand wordt opgenomen in het bronbesturingselement. |
| 5 | Database | De waarden die hier worden opgeslagen, worden toegevoegd door configuraties in te stellen in Admin. Configuraties die zijn ingesteld met een van de voorgaande methoden zijn vergrendeld (grijs weergegeven) en kunnen niet worden bewerkt met de beheerfunctie. |
| 6 | `config.xml` | Veel configuraties hebben standaardwaarden die zijn ingesteld in het `config.xml` -bestand voor een module. Als Adobe Commerce geen waarde kan vinden die door een van de voorgaande methoden is ingesteld, wordt de standaardwaarde (indien ingesteld) geretourneerd. |

{style="table-layout:auto"}

## Configuratiedrukschijf

U kunt de volgende opdracht `ece-tools` gebruiken om een `config.php` -bestand te genereren dat alle huidige opslagconfiguraties bevat:

```bash
./vendor/bin/ece-tools config:dump
```

De gegevens &quot;gedumpt&quot;aan het `app/etc/config.php` dossier worden _gesloten_, wat het overeenkomstige gebied in Commerce Admin **read-only** betekent. Het bestand `config.php` bevat alleen de instellingen die u configureert. De standaardwaarden worden niet vergrendeld. Door alleen de waarden te vergrendelen die u bijwerkt, zorgt u ervoor dat alle extensies die worden gebruikt in de omgevingen voor Staging en Productie niet worden verbroken door alleen-lezen configuraties, met name snel.

>[!WARNING]
>
>De opdracht `ece-tools config:dump` haalt geen gedetailleerde configuraties voor modules op, zoals B2B. Als u een uitvoerige configuratiestortplaats nodig hebt, gebruik het `app:config:dump` bevel, maar dit bevel vergrendelt configuratiewaarden in een read-only staat.

### Gevoelige gegevens

Alle gevoelige configuraties worden naar het `app/etc/env.php` -bestand geëxporteerd wanneer u de opdracht `bin/magento app:config:dump` gebruikt. U kunt vertrouwelijke waarden plaatsen gebruikend het CLI bevel: `bin/magento config:sensitive:set`. Zie [ Gevoelige en milieu-specifieke montages ](https://developer.adobe.com/commerce/php/development/configuration/sensitive-environment-settings/) in de _gids van de Uitbreidingen van Commerce PHP_ leren hoe te om configuratiemontages als gevoelig of systeem-specifiek aan te wijzen.

Zie een lijst van [ Gevoelige of systeem-specifieke montages ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/config-reference-sens.html) in de _Gids van de Configuratie_.

### SCD-prestaties

Afhankelijk van de grootte van uw winkel, hebt u mogelijk een groot aantal statische inhoudsbestanden om te implementeren. Normaalgesproken wordt statische inhoud tijdens de implementatiefase geïmplementeerd wanneer de toepassing zich in de onderhoudsmodus bevindt. De meest optimale configuratie moet statische inhoud tijdens de bouwstijlfase produceren. Zie [ Kiezen opstellen strategie ](../deploy/static-content.md).

Als u het Beheer van de Configuratie na het dumpen van de configuraties hebt toegelaten, zou u de variabelen SCD_* van het opstellen stadium aan het bouwstijlstadium moeten bewegen om statische inhoudsgeneratie tijdens de bouwstijlfase behoorlijk toe te laten. Zie [ variabelen van het Milieu ](../environment/configure-env-yaml.md#environment-variables).

**vóór het Beheer van de Configuratie**:

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

**na het toelaten van het Beheer van de Configuratie**:

Verplaats de variabelen SCD_* naar het bouwstijlstadium:

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

>[!NOTE]
>
>Voordat u statische bestanden implementeert, comprimeert de build- en implementatiefase statische inhoud met GZIP. Het comprimeren van statische bestanden verlaagt de serverlading en verbetert de prestaties van de site. Zie [ bouwt opties ](../environment/variables-build.md) om over het aanpassen van of het onbruikbaar maken van dossiercompressie te leren.

## Procedure voor het beheren van uw instellingen

Hieronder ziet u een overzicht op hoog niveau van dit proces:

![ Overzicht van het configuratiebeheer van de Aanzet ](../../assets/starter/configuration-management-flow.png)

**om uw opslag te vormen en een configuratiedossier** te produceren:

1. Voltooi alle configuraties voor uw winkels in Admin voor een van de omgevingen:

   - Starter: een actieve ontwikkelingstak
   - Pro: Een actieve vertakking in de integratieomgeving

   Deze configuraties omvatten niet de daadwerkelijke producten tenzij u van plan bent om het gegevensbestand van dit milieu aan het Opvoeren en de milieu&#39;s van de Productie te dumpen. Doorgaans bevatten ontwikkelingsdatabases niet uw volledige opslaggegevens.

1. Wijzig op uw lokale werkstation de projectmap.

1. Creeer een lokale stortplaats van het verre gegevensbestand.

   ```bash
   magento-cloud db:dump
   ```

1. Wijzigingen in code toevoegen, toewijzen en doorvoeren om een externe omgeving bij te werken.

   ```bash
   git add app/etc/config.php
   ```

   ```bash
   git commit -m "Add system-specific configuration"
   ```

   ```bash
   git push origin <branch-name>
   ```

Nadat de implementatie is voltooid, meldt u zich aan bij de beheerder voor de bijgewerkte omgeving om de instellingen te controleren. Ga door met het samenvoegen van eventuele aanvullende configuraties in de omgevingen Staging en Productie.

### Configuraties bijwerken

Wanneer u de omgeving wijzigt via Beheer en de opdracht opnieuw uitvoert, worden nieuwe configuraties toegevoegd aan de code in het `config.php` -bestand.

>[!WARNING]
>
>Terwijl u het `config.php` dossier in de het Opvoeren en milieu&#39;s van de Productie manueel kunt uitgeven, wordt het **niet** geadviseerd. Het bestand helpt alle configuraties in alle omgevingen consistent te houden. Verwijder het `config.php` -bestand nooit om het opnieuw samen te stellen. Als u het bestand verwijdert, worden mogelijk specifieke configuraties en instellingen verwijderd die vereist zijn voor het samenstellen en implementeren van processen.

### Configuratiebestanden herstellen

Kopieën van de oorspronkelijke `app/etc/env.php` - en `app/etc/config.php` -bestanden zijn gemaakt tijdens het implementatieproces en in dezelfde map opgeslagen. Hieronder ziet u de BAK (back-upbestanden) en PHP (oorspronkelijke bestanden) in dezelfde map `app/etc` :

```
...
config.php.bak
di.xml
env.php.bak
vendor_path.php
config.php
db_schema.xml
env.php
...
```

Oudere configuraties hebben het bestand `app/etc/config.local.php` gebruikt. Zie [ oudere configuraties migreren ](#migrate-older-configurations).

**om configuratiedossiers** te herstellen:

1. Voor uw lokale werkstation, gebruik SSH aan login aan het verre project en het milieu.

   ```bash
   magento-cloud ssh
   ```

1. De locatie en beschikbaarheid van de back-upbestanden controleren.

   ```bash
   ./vendor/bin/ece-tools backup:list
   ```

   Monsterrespons:

   ```
   The list of backup files:
   app/etc/env.php
   app/etc/config.php
   ```

1. Back-upbestanden herstellen.

   ```bash
   ./vendor/bin/ece-tools backup:restore
   ```

### Oudere configuraties migreren

Als u een upgrade uitvoert naar Adobe Commerce op cloudinfrastructuur 2.2 of hoger, kunt u instellingen uit het `config.local.php` -bestand migreren naar het nieuwe `config.php` -bestand. Als de configuratie-instellingen in uw beheerder overeenkomen met de inhoud van het bestand, volgt u de instructies om het `config.php` -bestand te genereren en toe te voegen.

Als deze verschillen, kunt u inhoud uit het `config.local.php` -bestand toevoegen aan uw nieuwe `config.php` -bestand:

1. Volg de instructies om het `config.php` -bestand te genereren.

1. Open het bestand `config.php` en verwijder de laatste regel.

1. Open het `config.local.php` -bestand en kopieer de inhoud.

1. Plak de inhoud in het `config.php` -bestand, sla het bestand op en voeg het toe aan Git.

1. Implementeer in uw omgeving.

U voltooit deze migratie maar één keer. Na de migratie gebruikt u het bestand `config.php` .

### Landinstellingen wijzigen

U kunt uw opslagscènes veranderen zonder een complex configuratieinvoer en uitvoerproces te volgen, _als_ u [ SCD_ON_DEMAND ](../environment/variables-global.md#scd_on_demand) toegelaten hebt. U kunt de landinstellingen bijwerken met de beheerfunctie.

U kunt een andere landinstelling toevoegen aan de omgeving Staging of Production door `SCD_ON_DEMAND` in te schakelen in een integratietak, een bijgewerkt `config.php` -bestand te genereren met de nieuwe landinstellingsinformatie en het configuratiebestand te kopiëren naar de doelomgeving.

>[!WARNING]
>
>Dit proces **beschrijft** de opslagconfiguratie; slechts doe het volgende als de milieu&#39;s de zelfde opslag bevatten.

1. In het integratiemilieu, laat `SCD_ON_DEMAND` variabele toe gebruikend het [`.magento.env.yaml` dossier ](../environment/configure-env-yaml.md).

1. Voeg de vereiste landinstellingen toe met uw beheerder.

1. Gebruik SSH om u aan te melden bij de externe omgeving en het `/app/etc/config.php` -bestand te genereren dat alle landinstellingen bevat.

   ```bash
   ssh <SSH-URL> "./vendor/bin/ece-tools config:dump"
   ```

1. Kopieer het nieuwe configuratiedossier van de verre integratiemilieu aan uw lokale milieufolder.

   ```bash
   rsync <SSH-URL>:app/etc/config.php ./app/etc/config.php
   ```

1. Wijzigingen in code toevoegen, toewijzen en doorvoeren om een externe omgeving bij te werken.
