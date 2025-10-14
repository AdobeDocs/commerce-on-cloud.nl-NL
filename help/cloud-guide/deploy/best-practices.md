---
title: Aanbevolen werkwijzen voor implementatie
description: Ontdek best practices voor de implementatie van Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Deploy, Best Practices
source-git-commit: 0d9d3d64cd0ad4792824992af354653f61e4388d
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---

# Aanbevolen werkwijzen voor implementatie

Scripts maken en implementeren die worden geactiveerd wanneer u code samenvoegt in een externe omgeving. Deze manuscripten gebruiken milieu [&#x200B; configuratiedossiers &#x200B;](../environment/overview.md) en toepassingscode aan voorziening wolkeninfrastructuur met aangewezen gegevens en de diensten. Deze scripts worden ook gebruikt om de Adobe Commerce-toepassing, services van derden en aangepaste extensies in de cloud te installeren of bij te werken.

Het bouwstijl en opstellen proces is lichtjes verschillend voor elk plan:

- **de plannen van de Aanzet** - voor het integratiemilieu, bouwt elke actieve tak en stelt aan een volledig milieu voor toegang en het testen op. Test de code na het samenvoegen tot de `staging` -vertakking volledig. Als u uw site wilt starten, drukt u op `staging` naar `master` om deze te implementeren in de productieomgeving. U hebt volledige toegang tot alle takken door [!DNL Cloud Console] en CLI bevelen.

- **Pro plannen** - voor het integratiemilieu, bouwt elke actieve tak en stelt aan een volledig milieu voor toegang en het testen op. Voeg uw code samen met de `integration` -vertakking voordat u deze samenvoegt tot de omgevingen voor Staging en Productie. U kunt samenvoegen met de instellingen voor Staging en Productie met behulp van de opdrachten [!DNL Cloud Console] of SSH en `magento-cloud` CLI.

## Het proces volgen

U kunt bouw volgen en acties in echt - tijd opstellen gebruikend de terminal of [!DNL Cloud Console] berichten van de Status— `in-progress`, `pending`, `success`, of `failed` - vertoning tijdens het plaatsingsproces. U kunt details in de logboekdossiers bekijken. Zie [&#x200B; Logboeken van de Mening &#x200B;](../test/log-locations.md).

Als u externe bewaarplaatsen GitHub gebruikt, toont het logboek van verrichtingen niet in de zitting GitHub. U kunt echter wel de activiteit in de interface voor de externe gegevensopslagruimte en de [!DNL Cloud Console] volgen. Zie [&#x200B; Integraties &#x200B;](../integrations/overview.md).

>[!NOTE]
>
>In integratieomgevingen kunt u de implementatielogboeken niet weergeven vanuit de [!DNL Cloud Console] . Deze functie is alleen beschikbaar voor Productie- en Staging-omgevingen. Nochtans, kunt u logboeken voor elke fase van de plaatsing in om het even welk milieu bekijken gebruikend [&#x200B; bouw en stel &#x200B;](../test/log-locations.md#build-and-deploy-logs) logboeken op. Voor het oplossen van problemeninformatie, zie de [&#x200B; foutenverwijzing van de Plaatsing &#x200B;](../dev-tools/error-reference.md).

U kunt [&#x200B; plaatsingen van het Spoor met New Relic &#x200B;](../monitor/track-deployments.md) toelaten om plaatsingsgebeurtenissen te controleren en prestaties tussen plaatsingen te analyseren.

## Aanbevolen werkwijzen voor builds en implementatie

Bekijk deze best practices en overwegingen voor uw implementatieproces:

- **zorg ervoor dat u de huidigste versie van het `ece-tools` pakket** in werking stelt

  Zie &lbrace;de nota&#39;s van de Versie voor ECE-Hulpmiddelen [&#128279;](../release-notes/ece-tools-package.md).

- **volg het bouwstijl en stel proces** op

  Zorg ervoor dat u de juiste code in elke omgeving hebt om te voorkomen dat configuraties worden overschreven wanneer u code samenvoegt tussen omgevingen. Bijvoorbeeld, om configuratieveranderingen op alle milieu&#39;s toe te passen, wijzig en test de veranderingen in het lokale milieu alvorens aan het verre integratiemilieu op te stellen. Dan, stel en test de veranderingen in het het Opvoeren milieu op alvorens aan Productie op te stellen. Wanneer u van één milieu aan een andere samenvoegt, beschrijft de plaatsing al code in het milieu, behalve milieu-specifieke configuratie en montages.

- **Gebruik de zelfde variabelen over milieu&#39;s**

  De waarden voor deze variabelen kunnen in verschillende omgevingen verschillen, maar meestal hebt u in elke omgeving dezelfde variabelen nodig. Zie [&#x200B; beheer van de Configuratie voor opslagmontages &#x200B;](../store/store-settings.md).

- **houd gevoelige configuratiewaarden en gegevens in milieu-specifieke variabelen**

  Deze waarden zijn onder andere variabelen die zijn opgegeven met de CLI van de cloud, de [!DNL Cloud Console] , of die zijn toegevoegd aan het `env.php` -bestand. Zie [&#x200B; Variabele niveaus &#x200B;](../environment/variable-levels.md).

- **zorg ervoor dat al code in de milieu tak** beschikbaar is

  Verwijzen naar code van andere takken, zoals een privé tak, kan problemen tijdens het bouwstijl veroorzaken en proces opstellen. Als u bijvoorbeeld naar een thema van een privé-vertakking verwijst, is het thema niet toegankelijk en kan het niet worden samengesteld met de toepassingscode.

- **voegt uitbreidingen, integratie, en code in herhaalde takken** toe

  Breng lokale wijzigingen aan en test deze. Druk vervolgens op `integration` en op `staging` en `production` . Test en los problemen in elke omgeving op voordat u de updates samenvoegt tot de volgende omgeving. Sommige uitbreidingen en integratie moeten in een specifieke orde wegens gebiedsdelen worden toegelaten en worden gevormd. Door het toevoegen en testen in groepen kunt u uw ontwikkelings- en implementatieproces veel eenvoudiger maken en bepalen waar zich problemen voordoen.

- **verifieer de dienstversies en verhoudingen en de capaciteit om** te verbinden

  Controleer welke services beschikbaar zijn voor uw toepassing en zorg ervoor dat u de meest actuele, compatibele versie gebruikt. Zie &lbrace;de verhoudingen van de Dienst [&#128279;](../services/services-yaml.md#service-relationships) en [&#x200B; vereisten van het Systeem &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html?lang=nl-NL) in de _gids van de Installatie_ voor geadviseerde versies.

- **Test plaatselijk en in het integratiemilieu alvorens aan het Opvoeren en Productie** op te stellen

  Identificeer en los kwesties in uw lokale en integratiemilieu&#39;s op om uitgebreide onderbreking te verhinderen wanneer u aan het Opvoeren van Staging en Productiemilieu&#39;s opstelt.

  >[!TIP]
  >
  >Er zijn [&#x200B; slimme tovenaar &#x200B;](../deploy/smart-wizards.md) bevelen die u kunt gebruiken om te verifiëren dat uw configuratie van het wolkenproject beste praktijken voor bouwstijl en plaatsingsconfiguratie volgt, met inbegrip van de statische strategie van de inhoudsplaatsing (SCD).

- **na het voltooien van het testen in lokale en integratiemilieu&#39;s, stel en test in het het Opvoeren milieu** op

  Zie [&#x200B; het Opvoeren en het Testen van de Productie &#x200B;](../test/staging-and-production.md).

- **het omgevingsconfiguratie van de Productie van de Controle**

  Voordat u gaat implementeren in Productie, moet u de volgende taken uitvoeren:

   - Zorg ervoor dat u met alle drie knopen in het milieu van de Productie kunt verbinden gebruikend [&#x200B; SSH &#x200B;](../development/secure-connections.md).

   - Verifieer dat de Indexers aan _Update op Programma_ worden geplaatst. Zie [&#x200B; Indexerende wijzen &#x200B;](https://developer.adobe.com/commerce/php/development/components/indexing/) in de _Gids van de Ontwikkelaar van de Uitbreiding_.

   - Bereid het milieu door om het even welke milieu-specifieke variabelen in de code van de Productie voor te werken, de beschikbaarheid en verenigbaarheid van de dienst te verifiëren, en om het even welke andere vereiste configuratieveranderingen aan te brengen.

- **Monitor het opstellen proces**

  Herzie de berichten van de plaatsingsstatus en verminder kwesties zoals nodig. Herzie de Logboeken van de Wolk [&#128279;](../test/log-locations.md#) voor gedetailleerde logboekberichten.

## Vijf fasen van integratie bouwen en plaatsing

De volgende fasen komen in uw lokale ontwikkelomgeving en integratieomgeving voor. Voor Pro plannen, wordt de code niet opgesteld aan de het Staging of milieu&#39;s van de Productie in deze aanvankelijke fasen.

### Fase 1: Validatie van code en configuratie

Wanneer u aanvankelijk opstelling een project, [&#x200B; het malplaatje van de wolkeninfrastructuur &#x200B;](https://github.com/magento/magento-cloud) een basis voor de codedossiers verstrekt. Deze codereeks wordt gekloond aan uw project als `master` tak.

- **voor Startpagina** - `master` tak is uw milieu van de Productie.
- **voor Pro** - `master` begint als oorsprongstak voor het integratiemilieu.

Maak een vertakking vanuit `master` voor uw aangepaste code, extensies en modules en integratie van derden. Er is een externe integratieomgeving voor het testen van uw code in de cloud.

Wanneer u uw code van uw lokale werkruimte aan de verre bewaarplaats duwt, voltooit een reeks controles en codebevestigingen alvorens manuscripten te bouwen en op te stellen beginnen. De ingebouwde server van de Git bevestigt wat u duwt en veranderingen aanbrengt. Bijvoorbeeld, als u de dienst OpenSearch toevoegt, verifieert de ingebouwde server van het Git dat de topologie van uw cluster dienovereenkomstig wordt gewijzigd.

Als een configuratiebestand een syntaxisfout bevat, wijst de Git-server de push af. Zie [&#x200B; Beschermend Blok &#x200B;](../development/protective-block.md).

In deze fase wordt ook `composer install` uitgevoerd om afhankelijkheden op te halen.

### Fase 2: Genereren

>[!NOTE]
>
>Tijdens de bouwstijlfase, is de plaats niet op onderhoudswijze en als de fouten of de kwesties voorkomen niet neer worden gebracht. Het bouwt slechts de code die sinds vorige bouwt is veranderd.

Deze fase bouwt de codebase en voert haken in de `build` sectie van `.magento.app.yaml` uit. De standaardbuild-haak is de opdracht `php ./vendor/bin/ece-tools` en voert het volgende uit:

- Past patches toe in `vendor/magento/ece-patches` en optionele, projectspecifieke patches in `m2-hotfixes`
- Regenereert code en de [&#x200B; configuratie van de gebiedsdeelinjectie &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-operations/implementation-playbook/glossary) (namelijk de `generated/` folder, die `generated/code` en `generated/metapackage` omvat) gebruikend `bin/magento setup:di:compile`.
- Controleert of het [`app/etc/config.php`](../store/store-settings.md) -bestand in de codebase bestaat. Adobe Commerce genereert dit bestand automatisch als het tijdens de constructiefase niet wordt gedetecteerd en bevat een lijst met modules en extensies. Als het bestaat, gaat de bouwstijlfase als normaal verder, comprimeert statische dossiers gebruikend GZIP, en stelt op, die onderbreking in de plaatsingsfase vermindert. Verwijs naar [&#x200B; bouwt opties &#x200B;](../environment/variables-build.md) om over het aanpassen van of het onbruikbaar maken van dossiercompressie te leren.

>[!WARNING]
>
>Op dit punt, is de cluster niet gecreeerd, zodat probeer niet om met een gegevensbestand te verbinden of veronderstel dat er een actief daemon proces is.

Nadat de toepassing bouwt, wordt het opgezet op a **read-only dossiersysteem**. U kunt specifieke koppelpunten vormen die zullen worden gelezen/schrijven. U kunt geen FTP aan de server en modules toevoegen. In plaats daarvan moet u code aan uw lokale opslagplaats toevoegen en `git push` uitvoeren, die bouwt en het milieu opstelt. Voor de projectstructuur, zie [&#x200B; de Lokale structuur van de projectfolder &#x200B;](../project/file-structure.md).

### Fase 3: De witruimte voorbereiden

Het resultaat van de bouwstijlfase is een read-only dossiersysteem dat als a _schuine streep_ wordt bedoeld. In deze fase wordt een archief gemaakt en wordt de witruimte permanent opgeslagen. De volgende keer dat u code indrukt, wordt de witruimte uit het archief gebruikt als de service niet is gewijzigd.

- Maakt continue integratie sneller opbouwen door ongewijzigde code opnieuw te gebruiken
- Als de code verandert, werkt de schuine streep voor volgende bouwstijl aan hergebruik bij
- Staat voor onmiddellijk het terugkeren van een plaatsing toe, indien nodig
- Bevat statische bestanden als het `app/etc/config.php` -bestand bestaat in de codebase

De schuine streep omvat alle dossiers en omslagen **exclusief de volgende** in `magento.app.yaml` gevormde steunen:

- `"var": "shared:files/var"`
- `"app/etc": "shared:files/etc"`
- `"pub/media": "shared:files/media"`
- `"pub/static": "shared:files/static"`

### Fase 4: Slakken en cluster implementeren

Uw toepassingen en alle [&#x200B; achterste &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-operations/implementation-playbook/glossary) de dienstvoorziening als volgt:

- Elke service in een container koppelen, zoals een webserver, OpenSearch, [!DNL RabbitMQ]
- Hiermee wordt het lees-schrijfbestandssysteem gemonteerd (op een opslagraster met hoge beschikbaarheid)
- Vormt het netwerk zodat kunnen de diensten &quot;zien&quot;elkaar (en slechts elkaar)

>[!NOTE]
>
>Breng uw veranderingen in een tak van de Plaats aan nadat al bouwt en plaatsing voltooit en opnieuw duw. Alle systemen van het milieudossier zijn _read-only_. Een alleen-lezen systeem garandeert deterministische implementaties en verbetert de beveiliging van uw site aanzienlijk, omdat geen enkel proces naar het bestandssysteem kan schrijven. Het werkt ook om ervoor te zorgen dat uw code in de milieu&#39;s van de Integratie, het Opvoeren, en van de Productie identiek is.

### Fase 5: implementatiehaken

>[!NOTE]
>
>In deze fase wordt de toepassing van [!DNL Commerce] in de onderhoudsmodus gezet totdat de implementatie is voltooid.

De laatste stap stelt een plaatsingsmanuscript in werking, dat u kunt gebruiken om gegevens in ontwikkelomgevingen, duidelijke geheime voorgeheugens, en vraagexterne ononderbroken-integratiegereedschappen anoniem te maken. Wanneer dit manuscript loopt, hebt u toegang tot alle diensten in uw milieu, zoals Redis.

Als het `app/etc/config.php` -bestand niet bestaat in de codebase, worden statische bestanden gecomprimeerd met `gzip` en geïmplementeerd tijdens deze fase, waardoor de implementatiefase en het siteonderhoud langer worden.

>[!NOTE]
>
>Verwijs naar [&#x200B; opstelt variabelen &#x200B;](../environment/variables-deploy.md) om over het aanpassen van of het onbruikbaar maken van dossiercompressie te leren.

Er zijn twee implementatiehaken. De `pre-deploy.php` haak voltooit noodzakelijke schoonmaak en terugwinning van middelen en code die in de bouwstijlhaak wordt geproduceerd. Met de `php ./vendor/bin/ece-tools deploy` -haak wordt een reeks opdrachten en scripts uitgevoerd:

- Als Adobe Commerce **niet geïnstalleerd** is, installeert het met `bin/magento setup:install`, werkt de plaatsingsconfiguratie, `app/etc/env.php`, en het gegevensbestand voor uw gespecificeerde milieu, zoals Redis en website URLs bij. **Belangrijk:** toen u de [&#x200B; Eerste plaatsing &#x200B;](https://experienceleague.adobe.com/docs/commerce-on-cloud/user-guide/launch/overview.html?lang=nl-NL) tijdens opstelling voltooide, werd Adobe Commerce geïnstalleerd en over alle milieu&#39;s opgesteld.

- Als Adobe Commerce **&#x200B;**&#x200B;geïnstalleerd is, voer om het even welke noodzakelijke verbeteringen uit. Het plaatsingsmanuscript stelt `bin/magento setup:upgrade` in werking om het gegevensbestandschema en de gegevens (die na uitbreiding of kerncode updates noodzakelijk is) bij te werken, en werkt ook de plaatsingsconfiguratie, `app/etc/env.php`, en het gegevensbestand voor uw milieu bij. Tot slot wist het plaatsingsmanuscript het geheime voorgeheugen van Adobe Commerce.

- Het script genereert optioneel statische webinhoud met de opdracht `magento setup:static-content:deploy` .

- Gebruikt werkingsgebied (`-s` vlag in bouwstijlmanuscripten) met het gebrek dat van `quick` voor de statische strategie van de inhoudsplaatsing plaatst. U kunt de strategie aanpassen met de omgevingsvariabele [`SCD_STRATEGY`](../environment/variables-deploy.md#scd_strategy) . Voor details op deze opties en eigenschappen, zie [&#x200B; Statische strategieën van de dossierplaatsing &#x200B;](../deploy/static-content.md) en de `-s` vlag voor [&#x200B; Statische meningsdossiers &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/static-view/static-view-file-deployment.html?lang=nl-NL) opstellen.

>[!NOTE]
>
>In het implementatiescript worden de waarden gebruikt die door configuratiebestanden in de map `.magento` zijn gedefinieerd. Vervolgens verwijdert het script de map en de inhoud ervan. Dit heeft geen invloed op uw lokale ontwikkelomgeving.

### Post-plaatsing: vorm het verpletteren

Terwijl de plaatsing loopt, stopt het proces inkomend verkeer op het ingangspunt voor 60 seconden en past het verpletteren aan zodat uw Webverkeer bij uw pas gecreëerde cluster aankomt.

Bij een geslaagde implementatie wordt de onderhoudsmodus verwijderd, zodat normale toegang mogelijk is en worden back-upbestanden (BAK-bestanden) gemaakt voor de `app/etc/env.php` - en `app/etc/config.php` -configuratiebestanden.

Laat statische inhoudsgeneratie toe gebruikend de `SCD_ON_DEMAND` variabele en vorm [`post_deploy` haak &#x200B;](../application/hooks-property.md) zodat het het geheime voorgeheugen ontruimt en (oorlogen) het geheime voorgeheugen _na_ de container begint goedkeurend verbindingen en _tijdens_ normaal, inkomend verkeer.

Om logboeken te herzien bouwen en op te stellen, zie [&#x200B; Logboeken van de Mening &#x200B;](../test/log-locations.md#view-and-manage-logs).
