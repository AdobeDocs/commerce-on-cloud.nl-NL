---
title: Achteruit incompatibele wijzigingen
description: Leer meer over achterwaartse verenigbaarheid wanneer het bevorderen van bestaande projecten van de Wolk.
feature: Cloud, Release Notes
recommendations: noDisplay, catalog
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---

# Achteruit incompatibele wijzigingen

Door wijzigingen die niet compatibel zijn met oudere versies, moet u mogelijk de configuratie en processen van de cloud aanpassen voor bestaande Cloud-projecten wanneer u een upgrade uitvoert naar de nieuwste versie van het `ece-tools` -pakket of andere Cloud Tools Suite voor Commerce-pakketten.

## Wijzigingen in `ece-tools` -pakket

Enkele functionaliteit die eerder in het `ece-tools` -pakket is opgenomen, wordt nu in afzonderlijke pakketten aangeboden. Deze pakketten zijn componentenafhankelijkheden voor `ece-tools`, die automatisch worden geïnstalleerd en bijgewerkt wanneer u bureaubladgereedschappen installeert of bijwerkt.

De nieuwe architectuur zou uw installatie of updateprocessen niet moeten beïnvloeden. Het kan echter zijn dat u bepaalde syntaxis en processen voor opdrachten moet wijzigen wanneer u met uw Adobe Commerce werkt aan een infrastructuurproject voor de cloud. Voor details, herzie de volgende achterwaartse incompatibele veranderingsinformatie en de [&#x200B; de versienota&#39;s van de Reeks van Hulpmiddelen van de Wolk &#x200B;](cloud-tools-suite.md).

### Wijzigingen in de vereisten voor serviceversie

We hebben de minimale PHP-versievereiste gewijzigd van 7.0.x in 7.1.x voor Cloud-projecten die `ece-tools` v2002.1.0 en hoger gebruiken. Als uw milieuconfiguratie PHP 7.0 specificeert, werk de [&#x200B; php configuratie &#x200B;](../application/php-settings.md) in het `.magento.app.yaml` dossier bij.

>[!WARNING]
>
>Vanwege de wijziging in de PHP-versie, ondersteunt `ece-tools` 2002.1.0 alleen Adobe Commerce op cloud-infrastructuurprojecten met Adobe Commerce 2.1.15 of hoger. Als uw project een vroegere versie gebruikt, moet u [&#x200B; bevorderen &#x200B;](../development/commerce-version.md) alvorens u aan `ece-tools` 2002.1.0 bijwerkt.

### Wijzigingen in de configuratie van omgeving

De volgende tabel bevat informatie over omgevingsvariabelen en andere omgevingsconfiguratiebestanden die zijn verwijderd of vervangen in `ece-tools` v2002.1.0.

| Item | Vervanging |
| -------- | ----------- |
| `SCD_EXCLUDE_THEMES` variable | [`SCD_MATRIX`](../environment/variables-build.md#scd_matrix) |
| `STATIC_CONTENT_THREADS` variable | [`SCD_THREADS`](../environment/variables-build.md#scd_threads) |
| `DO_DEPLOY_STATIC_CONTENT` variable | [`SKIP_SCD`](../environment/variables-build.md#skip_scd) |
| `STATIC_CONTENT_SYMLINK` variable | Geen. De build maakt nu altijd een koppeling naar de map met statische inhoud `pub/static` . |
| `build_options.ini` -bestand | Gebruik het bestand [`.magento.env.yaml`](../application/configure-app-yaml.md) om omgevingsvariabelen te configureren voor het beheer van build-and-implementatiehandelingen in al uw omgevingen.<p>Als u een Cloud-omgeving maakt die het `build_options.ini` -bestand bevat, mislukt het samenstellen. |

### Wijzigingen in CLI-opdracht

De volgende lijst vat CLI bevelveranderingen in ECE-Tools v2002.1.0 samen die u zouden kunnen vereisen om bevelen of manuscripten bij te werken.

| Opdracht | Vervanging |
|-------- | ----------- |
| `m2-ece-build` | `vendor/bin/ece-tools build` |
| `m2-ece-deploy` | `vendor/bin/ece-tools deploy` |
| `m2-ece-scd-dump` | `vendor/bin/ece-tools config:dump` |
| `vendor/bin/ece-tools patch` | `vendor/bin/ece-patches apply` |
| `vendor/bin/ece-tools docker:build` | `vendor/bin/ece-docker build:compose` |
| `vendor/bin/ece-tools docker:config:convert` | `vendor/bin/ece-docker  image:generate:php` |

In eerdere versies van ECE-Tools kon u de opdrachten `m2-ece-build` en `m2-ece-deploy` gebruiken om implementatiehaken in het `.magento.app.yaml` -bestand te configureren. Wanneer u de update naar versie 2002.1.0 uitvoert, controleert u de `hooks` -configuratie in het `.magento.app.yaml` -bestand op de verouderde opdrachten en vervangt u deze indien nodig.

## Wijzigingen in cloudpatches

- **verwijdert gedownloade flarden** - het `magento/magento-cloud-patches` pakket bundelt alle flarden beschikbaar van de [&#x200B; software downloadt &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/commerce.html?lang=nl-NL) pagina en past hen automatisch toe wanneer u aan de Wolk opstelt. Om flardconflicten na bevordering aan ECE-Tools 2002.1.0 of later te verhinderen, verwijder om het even welke Adobe-geleverde flarden die u aan uw project manueel downloadde en toevoegde.

- **Bijwerkend het toepassen bevel van flarden** - wij bewogen het bevel voor het toepassen van flarden van de `vendor/bin/ece-tools` folder aan de `vendor/bin/ece-patches` folder. Gebruik het nieuwe pad als u deze opdracht gebruikt om handmatig patches toe te passen.

  > Patches handmatig toepassen

  ```bash
  php ./vendor/bin/ece-patches apply
  ```

## Wijzigingen in Cloud Docker

- **het minimum PHP versievereisten is nu PHP 7.1** - als uw Deken van de Wolk voor de gastheer van Commerce een vroegere versie in werking stelt, bevorder aan PHP v7.1 of later.

- **het Dok van de Wolk voor het bevelveranderingen van Commerce** -

   - **het Bijwerken van het Dok van de Wolk voor de bevelen van Commerce voor Docker bouwt verrichtingen** - wij bewogen het Dok van de Wolk voor de bevelen van Commerce van de `vendor/bin/ece-tools` folder aan de `vendor/bin/ece-docker` folder. Werk uw scripts en opdrachten bij om het nieuwe pad te gebruiken.

     Na de upgrade naar `ece-tools` 2002.1.0 kunt u de volgende opdracht gebruiken om beschikbare `ece-docker` -opdrachten weer te geven.

     ```bash
     php ./vendor/bin/ece-docker list
     ```

   - **Bijwerkend de de docker-samenstelling van de Wolk bevelen** - wij noemden de weg aan het beveldossier van `./bin/docker` aan `./bin/magento-docker` anders. Werk uw scripts en opdrachten bij om het nieuwe pad te gebruiken.

   - **container van de Kroon niet meer inbegrepen in standaardDocker configuratie** - nu, moet u de `--with-cron` optie aan het `ece-docker build:compose` bevel toevoegen om de container van de Kroon in de de omgevingsconfiguratie van het Docker te omvatten. Zie [&#x200B; cron banen &#x200B;](https://developer.adobe.com/commerce/cloud-tools/docker/configure/manage-cron-jobs/) beheren in het _Dok van de Wolk voor Commerce_ gids.

     Scripts die eerder containers met uitsnijdtaken hebben gegenereerd, zijn nu zonder de uitsnijdcontainer.

   - **Gebruikend tijdelijke containers** - in vorige versies, werden de containers die door `bin/magento-docker` bevelverrichtingen werden gecreeerd niet verwijderd, zodat kon u hen voor andere verrichtingen gebruiken. De opdrachten van `magento-docker` verwijderen alle containers die ze maken nadat de opdracht is voltooid.

     Als u een container wilt behouden die is gemaakt door een docker-compositiebewerking, gebruikt u de opdracht `docker-compose run` in plaats van de opdracht `bin/magento-docker` .

   - **Lopend post-opstelt haken** - het `cloud-deploy` bevel niet meer post-opstellings haken in werking. Gebruik de nieuwe opdracht `cloud-post-deploy` om na implementatie hooks uit te voeren nadat u deze hebt geïmplementeerd. Werk uw manuscripten bij om het bevel toe te voegen om haken in werking te stellen post-opstellen.

     ```shell
     bin/magento-docker ece-deploy
     bin/magento-docker ece-post-deploy
     ```

     Als u `docker-compose` -opdrachten rechtstreeks gebruikt, kunt u de opdracht `docker-compose run deploy cloud-post-deploy` ook uitvoeren na de opdracht Implementeren.

- **het Verfrissen van het gegevensbestand** - de container van het Gegevensbestand wordt nu opgeslagen in het `magento-db` blijvende volume van de Docker. Wanneer u de Docker-omgeving vernieuwt, wordt de database niet meer automatisch verwijderd. Indien nodig, gebruik één van de volgende bevelen om het manueel te verwijderen.

   - Verwijder de container van `magento-db` :

     ```bash
     docker volume rm magento-db
     ```

   - Alle bijbehorende volumes verwijderen bij het sluiten van de Docker-containers:

     ```bash
     docker-compose down -v
     ```

- **de montages van de dossiersynchronisatie van de met voeten treden voor archivering en reservedossiers** - Archiveer en reservedossiers met de volgende uitbreidingen zijn niet meer gesynchroniseerd wanneer het gebruiken van docker-synchronisatie of mutageen: SQL, GZ, ZIP, en BZ2. U kunt de standaardbestandssynchronisatie voor deze bestandstypen negeren door de naam van het bestand te wijzigen zodat het eindigt met een andere extensie. Bijvoorbeeld: `synchronize-me.zip-backup`
