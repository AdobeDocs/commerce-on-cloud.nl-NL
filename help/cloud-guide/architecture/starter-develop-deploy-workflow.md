---
title: Starter-projectworkflow
description: Leer hoe u de workflows voor Starter-ontwikkeling en -implementatie kunt gebruiken.
feature: Cloud, Paas
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 0%

---

# Starter-projectworkflow

De Adobe Commerce on cloud-infrastructuur omvat één Git-opslagplaats met een `master` -vertakking voor de productieomgeving die kan worden vertakt om een testomgeving en meerdere integratieomgevingen te creëren voor test- en ontwikkelingswerk. U kunt maximaal vier actieve omgevingen hebben, waaronder een `master` -omgeving voor uw productieserver. Zie [ architectuur van de Aanzet ](starter-architecture.md) voor een overzicht.

Volg voor uw omgevingen de [!UICONTROL Development > Staging > Production] -workflow om uw site te ontwikkelen en te implementeren.

- **het milieu van de Productie (levende plaats)** - verstrekt een volledig productiemilieu met alle diensten die worden gebouwd en van de code op de `master` tak worden opgesteld.
- **het Staging milieu** - verstrekt een volledig het opvoeren milieu dat het productiemilieu met alle diensten aanpast die worden gebouwd en van a `staging` tak worden opgesteld die u door het klonen van `master` creeert.
- **milieu&#39;s van de Integratie** - verstrekt tot twee actieve ontwikkelomgevingen die u van de `staging` tak creeert. De `integration` -omgeving biedt geen ondersteuning voor services van derden zoals Fastly en New Relic.

Voor uw takken, kunt u om het even welke ontwikkelingsmethodologie volgen. U kunt bijvoorbeeld een gangbare methode volgen, zoals scrum, om vertakkingen te maken voor elke sprint.

Vanuit elke sprint kunt u vertakkingen maken voor elk gebruikersartikel. Alle verhalen worden testbaar. U kunt voortdurend samenvoegen tot de verftak en die vertakking doorlopend valideren. Wanneer de sprint eindigt, kunt u de sprinttak aan `master` samenvoegen om alle sprintveranderingen in productie op te stellen zonder het moeten een het testen knelpunt behandelen.

## Ontwikkelingsworkflow

De ontwikkeling en de plaatsing op de plannen van de Aanzet beginnen met uw aanvankelijke project. U maakt uw project met de &quot;lege site&quot;, een Adobe Commerce on cloud-infrastructuursjablooncode met een volledig voorbereide winkel. Hiermee maakt u een `master` -vertakking met een kopie van de code uit de productieomgeving.

De ontwikkelingsworkflow omvat het volgende:

- [ Kloon en tak ](#clone-and-branch) van `master` om `staging` en ontwikkelingstakken tot stand te brengen
- [ ontwikkelt code ](#develop-code) en installeert uitbreidingen plaatselijk in een ontwikkelingstak, met inbegrip van [!DNL Composer] updates
- [ vorm ](#configure-store) uw opslag en uitbreidingsmontages
- [ produceer configuratie ](#generate-configuration-management-files) beheersdossiers
- [ duw code ](#push-code-and-test) en configuratie om aan de `staging` en `production` milieu&#39;s te bouwen en op te stellen

![ ontwikkelt en stelt werkschema ](../../assets/starter/workflow.png) op

U hebt ook een paar optionele stappen om u te helpen uw code en uw opslaggegevens te ontwikkelen en te testen:

- [ installeer steekproefgegevens ](#optional-install-sample-data) aan uw opslag
- [ de gegevens van de productieopslag van de Trek ](#optional-pull-production-data) neer aan milieu&#39;s

Dit proces veronderstelt dat u opstelling uw [ lokale ontwikkelaarswerkruimte ](../development/overview.md) hebt.

### Klonen en vertakking

Voor een nieuw Starter Plan-project is een `master` -vertakking uit de Adobe Commerce gekloond op de Git-opslagplaats voor cloudinfrastructuur. Als u vertakking wilt starten en wilt werken met code, kloont u de `master` -vertakking naar uw lokale omgeving.

De indeling van de opdracht Git-kloon is:

```bash
git fetch origin
```

```bash
git pull origin <environment-ID>
```

De eerste keer dat u in vertakkingen voor uw Starter-project begint te werken, maakt u een `staging` -vertakking. Dit leidt tot een codetak die de `master` tak aanpast die aan een het Opvoeren milieu aan testconfiguratie en codeveranderingen alvorens aan het productiemilieu opstelt.

Maak vervolgens vertakkingen vanuit `staging` om code te ontwikkelen, extensies toe te voegen en integratie van derden te configureren. Telkens wanneer u douanecode ontwikkelt, voeg uitbreidingen toe, integreer met de derdedienst, werk in een ontwikkelingstak die van de `staging` tak wordt gecreeerd. U hebt vier actieve integratieomgevingen beschikbaar. Wanneer u een actieve vertakking duwt, stelt één van deze integratiemilieu&#39;s automatisch uw code aan test op.

De indeling van de opdracht voor de Git-vertakking is:

```bash
git checkout <branch-name>
```

De indeling van de opdracht Cloud CLI `branch` is:

```bash
magento-cloud environment:branch <environment-name> <parent-environment-ID>
```

![ Tak van Stramien ](../../assets/starter/branching.png)

### Code ontwikkelen

Met de basisvertakking van Adobe Commerce op code voor de cloud-infrastructuur kunt u extensies installeren, aangepaste code ontwikkelen, thema&#39;s toevoegen en nog veel meer.

Gebruik een vertakkende strategie met uw ontwikkelingswerk. Het gebruik van één vertakking om al uw werk in één keer uit te voeren kan het testen bemoeilijken. U kunt bijvoorbeeld de methoden voor continue integratie en sprint volgen om te werken:

- Voeg een paar uitbreidingen toe en vorm hen met uw eerste tak
- Druk deze code, test en fusie aan het Staging toen Productie
- Configureer uw services volledig in `services.yaml` en voeg een thema toe
- Druk deze code, test en fusie aan het Staging toen Productie
- Integreren met een service van derden
- Druk deze code, test en fusie aan het Staging toen Productie

Totdat uw winkel volledig is gebouwd, geconfigureerd en klaar is om te worden gestart. Maar blijf lezing, zijn er vele opties voor uw opslag en codeconfiguratie.

>[!NOTE]
>
>Voer nog geen configuraties in uw lokale werkstation uit.

![ duw code van lokale ](../../assets/starter/push-code.png)

### Winkel configureren

Wanneer u klaar bent om uw winkel te configureren, drukt u op al uw code naar de `integration` -omgeving. Configureer uw opslaginstellingen vanuit de beheerfunctie voor de integratieomgeving, niet in uw lokale omgeving. U kunt URL vinden door **plaats van de Toegang** in [!DNL Cloud Console] te klikken

Raadpleeg de documentatie voor Adobe Commerce en de geïnstalleerde extensies voor de beste informatie over configuraties. Hier volgen enkele koppelingen en ideeën die u helpen om aan de slag te gaan:

- [ Beste praktijken voor opslagconfiguratie ](../store/best-practices.md) voor specifieke beste praktijken in de wolk
- [ Basisconfiguratie ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/store-details) voor opslag admin toegang, naam, talen, valuta, branding, plaatsen, opslagmeningen en meer
- [ Thema ](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/content-menu#design-features) voor uw blik en gevoel van de plaats en opslag met inbegrip van CSS en lay-outs
- [ configuratie van het Systeem ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) voor rollen, hulpmiddelen, berichten, en uw encryptiesleutel voor uw gegevensbestand
- Instellingen voor extensies gebruiken in de documentatie

Buiten enkel opslagmontages, kunt u veelvoudige plaatsen en opslag, de gevormde diensten, en meer verder vormen. Zie [ uw opslag ](../store/overview.md) vormen.

### Configuratiebeheerbestanden genereren

Als u vertrouwd bent met Adobe Commerce, kunt u zich zorgen maken over hoe te om uw configuratiemontages van uw gegevensbestand in ontwikkeling aan de het opvoeren en productiemilieu&#39;s te krijgen. Eerder, moest u al uw configuratiemontages neer op papier of aan een dossier kopiëren, en dan manueel de montages toepassen op andere milieu&#39;s. Of u hebt uw database mogelijk gedumpt en deze gegevens naar een andere omgeving geduwd.

Adobe Commerce op wolkeninfrastructuur verstrekt een reeks twee [ bevelen van het Beheer van de Configuratie ](../store/store-settings.md) die configuratiemontages van uw milieu in een dossier uitvoeren. Deze bevelen zijn slechts beschikbaar voor **Adobe Commerce op wolkeninfrastructuur 2.2 en later**.

- `php .vendor/bin/ece-tools config:dump` - Exporteert alleen de configuratie-instellingen die u hebt ingevoerd of gewijzigd op basis van standaardinstellingen in een configuratiebestand. _geadviseerd_.
- `php bin/magento app:config:dump` - Exporteert elke configuratie-instelling, inclusief gewijzigd en standaard, naar een configuratiebestand.

Het gegenereerde bestand is `app/etc/config.php` .

Genereer het bestand in de integratieomgeving waarin u Adobe Commerce hebt geconfigureerd. Stap door het proces om het dossier te produceren, het toe te voegen aan uw tak, en het op te stellen.

**Belangrijke nota&#39;s** op het Beheer van de Configuratie:

- Elke configuratie-instelling die is opgenomen in het bestand dat is gegenereerd via de opdracht `app:config:dump` , is vergrendeld voor bewerking of alleen-lezen in de geïmplementeerde omgeving. Dit is een van de redenen waarom de Adobe het gebruik van de opdracht `.vendor/bin/ece-tools config:dump` aanbeveelt.

  U installeert bijvoorbeeld een module voor Snel in uw ontwikkelomgeving. U kunt deze module in het opvoeren en productiemilieu slechts vormen. Als u de opdracht `.vendor/bin/ece-tools config:dump` gebruikt, blijven deze standaardvelden bewerkbaar wanneer u uw ontwikkelingswijzigingen implementeert in de omgeving van Staging en Productie.

- Het gegenereerde bestand kan lang zijn, afhankelijk van de grootte van uw implementatie. De opdracht `.vendor/bin/ece-tools config:dump` genereert een kleiner bestand dan het bestand dat met de opdracht `app:config:dump` wordt gegenereerd.

Als u Adobe Commerce versie 2.2 of hoger gebruikt, bieden de opdrachten voor configuratiebeheer een extra functie om vertrouwelijke gegevens te beschermen, zoals referenties van sandboxen voor een PayPal-module. Tijdens het uitvoerproces, worden om het even welke waarden die gevoelige gegevens bevatten uitgevoerd naar afzonderlijk configuratiedossier— `env.php` in de `app/etc/` folder. Dit bestand blijft in uw lokale omgeving en wordt niet gekopieerd wanneer u de code naar een andere vertakking verplaatst. U kunt ook omgevingsvariabelen maken met CLI-opdrachten in alle Adobe Commerce-versies van cloudinfrastructuur.

![ de variabelen van het Milieu produceren ](../../assets/starter/env-variables.png)

Zie [ Beheer van de Configuratie ](../store/store-settings.md).

### Pushcode en test

Op dit punt, zou u een ontwikkelde codetak met een configuratiedossier (`config.local.php` of `config.php`) klaar moeten hebben om te testen.

Telkens als u code van uw lokale milieu duwt, bouwt een reeks en stelt manuscripten in werking in werking. Deze manuscripten produceren nieuwe code en stellen het aan het verre milieu op. Bijvoorbeeld, als u een ontwikkelingstak van uw lokale milieu aan de verre tak duwt, werkt een passende milieu de diensten, code, en statische inhoud bij.

U hebt rechtstreeks toegang tot deze omgeving via een winkel-URL, een Admin-URL en een SSH. Deze milieu&#39;s omvatten een Webserver, gegevensbestand, en de gevormde diensten. Als u klaar bent, kunt u beginnen met het implementeren en testen in de testomgeving.

Voor meer informatie, zie [ het werkschema van de Plaatsing ](#deployment-workflow).

### Optioneel: voorbeeldgegevens installeren

Als u voorbeeldgegevens nodig hebt bij het ontwikkelen van uw winkel, kunt u voorbeeldgegevens installeren. Deze gegevens simuleren een actieve opslag, met inbegrip van klanten, producten, en andere gegevens. Deze voorbeeldgegevens werken het best met een &quot;lege site&quot; Adobe Commerce op de sjablooninstallatie van de cloudinfrastructuur wanneer u uw project maakt. U kunt het beste de voorbeeldgegevens verwijderen voordat u live gaat. Zie [ facultatieve steekproefgegevens installeren ](../test/sample-data.md).

![ installeer facultatieve steekproefgegevens ](../../assets/starter/sample-data.png)

### Optioneel: volledige productiegegevens

Voeg al uw producten, catalogi, site-inhoud enzovoort rechtstreeks toe aan de `production` -omgeving. Door deze gegevens toe te voegen aan de productieomgeving, kunt u bijgewerkte prijzen, coupons, voorraad, verkoopmededelingen, informatie over toekomstig aanbod en meer voor uw klanten verstrekken. Deze gegevens omvatten geen uitbreidingsconfiguraties, die u in uw lokale ontwikkelingstak vormt.

Als u functies ontwikkelt, extensies toevoegt en thema&#39;s ontwerpt, is het handig om echte gegevens te gebruiken. Op elk ogenblik, kunt u een gegevensbestandstortplaats [&#128279;](../storage/database-dump.md) van het productiemilieu tot stand brengen en duwen dat aan uw het Opvoeren en integratiemilieu&#39;s zonodig.

Productiegegevens exporteren als testgegevens voor gebruik in staging- en integratieomgevingen:

- [ stel de bevelen van de steunnut ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) CLI (geadviseerd) in werking wanneer het uitvoeren van een beschermde steun van klant en opslaggegevens gebruikend uw de encryptiesleutel van Adobe Commerce

- [ het hulpmiddel van de Inzameling van Gegevens ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/support#data-collector) om gegevens te produceren en uit te voeren

Om dit gegeven te migreren, zie [ en stel statische dossiers en gegevens ](../deploy/staging-production.md#migrate-static-files) op.

![ Trek en ontsmet productiegegevens ](../../assets/starter/data-code-process.png)

>[!NOTE]
>
>Voordat u de gegevens naar een andere omgeving verplaatst, moet u overwegen de gegevens te ontsmetten. U hebt een paar opties met inbegrip van [ gebruikend steunnut ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/run-support-utilities.html) of het ontwikkelen van een manuscript om klantengegevens te schrobben.

>[!WARNING]
>
>Verplaats een database niet van een integratie- of testomgeving naar een productieomgeving. Als u, de gegevens van de integratie of het opvoeren milieu uw levende productiegegevens, met inbegrip van verkoop, orden, nieuwe en bijgewerkte klanten, en meer overschrijft.

## Implementatieworkflow

Zoals beschreven in de architectuurinformatie, wordt Adobe Commerce op cloudinfrastructuur aangestuurd door Git. Adobe Commerce implementeren op cloudinfrastructuur maakt deel uit van uw Git-pushprocessen voor vertakkingen.

Wanneer u vertakte code van uw lokale milieu aan de verre tak duwt, begint een reeks bouwstijl en stelt manuscripten op.

Scripts maken:

- De site in de doelomgeving blijft actief tijdens een build

- Adobe Commerce controleren en uitvoeren op patches en hotfixes voor cloudinfrastructuur

- Compileer uw code met een bouwstijl en stel logboek op

- Controleren op configuratiebeheer als de implementatie van statische inhoud tijdens deze fase plaatsvindt

- Een witruimte maken of gebruiken als ongewijzigde code voor een sneller proces

- Alle back-endservices en -toepassingen aanbieden

Scripts implementeren:

- Zet uw site in de modus Onderhoud op de doelomgeving

- Statische inhoud implementeren als deze niet is voltooid tijdens de build

- Adobe Commerce installeren of bijwerken op cloudinfrastructuur

- Vorm het verpletteren voor verkeer

Wanneer uw winkel volledig is voltooid, kunt u online terugkeren, live, met al uw bijgewerkte code en configuraties.

Zie [ proces van de Plaatsing ](../deploy/process.md).

### Naar testfase duwen en testen

Duw uw code altijd in herhalingen aan het `staging` milieu voor volledige het testen. De eerste keer u dit milieu gebruikt, moet u een paar diensten, met inbegrip van [ snel ](/help/cloud-guide/cdn/fastly.md) en [ New Relic ](../monitor/new-relic-service.md) vormen. Configureer ook betaalgateways, verzendingen, meldingen en andere essentiële services met sandbox- of testgegevens.

Staging is een omgeving vóór de productie die alle services en instellingen zo dicht mogelijk bij de productie biedt. Test grondig elke dienst, verifieer uw prestaties testende hulpmiddelen, voer het testen van UAT als beheerder en als klant uit, tot u uw opslag klaar voor productie voelt.

Zie [ uw opslag ](../deploy/staging-production.md) opstellen.

### Verschuiven naar productie

Wanneer u naar de `master` -vertakking drukt, gaat u door naar de `production` -omgeving. Voltooi configuratie- en testactiviteiten in de productieomgeving, net als in de testomgeving, met één belangrijk verschil. Gebruik in de productieomgeving live referenties voor configuratie en testen. Wanneer u uw site start, kunnen klanten hun aankopen voltooien en kunnen beheerders de live winkel beheren.

Zie [ uw opslag ](../deploy/staging-production.md) opstellen.

### Site starten

Er is een duidelijke doorloop om met uw site te gaan wonen. Nadat u deze stappen hebt uitgevoerd, kan uw winkel producten in uw aangepaste thema meteen verkopen.

Zie [ lancering van de Plaats ](../launch/overview.md).

## Continue integratie

Na uw vertakkings en ontwikkelingsmethodologieën, kunt u nieuwe eigenschappen gemakkelijk ontwikkelen, veranderingen vormen, en uitbreidingen toevoegen om updates onophoudelijk te ontwikkelen en op te stellen.

Alle omgevingen met cloudinfrastructuren ondersteunen continue integratie voor constante updates. Deze workflow biedt ondersteuning voor releases die meerdere keren per dag of volgens een vast tijdschema worden uitgevoerd.

- Ontwikkeltakken maken met toekomstige functies en wijzigingen

- De code in uw `integration` -omgeving testen

- Implementeren en testen in `staging` -omgeving

- Distribueren naar de `production` -omgeving
