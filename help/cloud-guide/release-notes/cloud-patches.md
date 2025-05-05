---
title: Cloudpatches voor Commerce
description: Zie een lijst met de meest recente verbeteringen in het pakket met cloudpatches.
recommendations: noDisplay, catalog
last-substantial-update: 2025-05-05T00:00:00Z
exl-id: a4454ebc-72a4-42c1-b591-6237c97fe913
source-git-commit: 0b9717be7d24fa83fe9208f2576508d62cc5594f
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 0%

---

# Cloudpatches voor Commerce

Het ](https://github.com/magento/magento-cloud-patches) pakket van de Patches van de Wolk 1} verstrekt een reeks vereiste flarden die de integratie van alle versies van Adobe Commerce met de milieu&#39;s van de Wolk verbeteren en snelle levering van kritieke moeilijke situaties steunt.[

Het pakket Cloud Patches voor Commerce is afhankelijk van het pakket ECE-Tools en wordt geïnstalleerd en bijgewerkt wanneer u het pakket ECE-Tools installeert of bijwerkt. U kunt Cloud Patches voor Commerce ook gebruiken en beheren als een zelfstandig pakket om patches toe te passen op een Adobe Commerce-project dat zich niet op het Cloud-platform bevindt. In deze releaseopmerkingen worden de meest recente verbeteringen aan dit pakket beschreven.

>[!TIP]
>
>Om ervoor te zorgen dat uw project alle vereiste flarden heeft, werk aan de [ recentste versie van ece-tools ](../dev-tools/update-package.md) bij.

>[!NOTE]
>
>Zie [ flarden ](../development/apply-patches.md) voor instructies op het toepassen van flarden op uw projecten toepassen.

Het pakket `magento/magento-cloud-patches` gebruikt de volgende versiereeks: `<major>.<minor>.<patch>`

<!--Add release notes below-->

## v1.1.7 {#latest}

Releasedatum: 5 mei 2025

- ![ nieuw pictogram ](../../assets/new.svg) **Bijgewerkt flard voor Commerce 2.4.4 aan 2.4.8** - dit is een bijgewerkt flard voor [ CVE-2025-24434 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/increased-execution-time-for-bulk-asynchronous-web-endpoints-post-apsb25-08-security-patch), dat in 1.1.7 <!-- MCLOUD-13619 --> werd vrijgegeven

## v1.1.6

Releasedatum: 24 april 2025

- ![ nieuw pictogram ](../../assets/new.svg) **Bijgewerkt flard voor Commerce 2.4.4 aan 2.4.7** - dit is een bijgewerkt flard voor [ CVE-2025-24434 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/security-update-available-for-adobe-commerce-apsb25-08), dat in 1.1.4 <!-- MCLOUD-13240 --> werd vrijgegeven

## v1.1.5

Releasedatum: 15 april 2025

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegd flard voor B2B 1.5.2** - moeilijke situatie voor de kwestie ACS2E-3833 met B2B module 1.5.2 en MariaDB 10.6 <!-- MCLOUD-13605	-->

## v1.1.4

Releasedatum: 13 februari 2025

- ![ nieuw pictogram ](../../assets/new.svg) **Toegevoegd flard voor Commerce 2.4.4 aan 2.4.7** - Deze updatepatches [ CVE-2025-24434 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/security-update-available-for-adobe-commerce-apsb25-08).<!-- MCLOUD-13240	 - -->

## v1.1.3

Releasedatum: 6 februari 2025

- ![ nieuw pictogram ](../../assets/new.svg) **PHP 8.4** - toegevoegde steun voor PHP 8.4.<!-- MCLOUD-13149	 - -->

## v1.1.2

Releasedatum: 5 november 2024

- ![ fixpictogram ](../../assets/fix.svg) **Toegevoegd flard voor Commerce 2.4.4 aan 2.4.7** - Deze update bevestigt een kritieke [ CVE-2024-45115 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/security-update-available-for-adobe-commerce-apsb24-73) kwetsbaarheid voor Adobe Commerce wanneer het gebruiken van de module B2B.<!-- MCLOUD-12980 - -->

## v1.1.1

Releasedatum: 5 november 2024

- ![ fixpictogram ](../../assets/fix.svg) **Toegevoegd flard voor Commerce 2.4.4 aan 2.4.7** - Deze updatepatches een kritieke [ CVE-2024-34102 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/security-update-available-for-adobe-commerce-apsb24-40-revised-to-include-isolated-patch-for-cve-2024-34102?lang=en) kwetsbaarheid CosmicSting.<!-- MCLOUD-12980 - -->

## v1.1.0

Releasedatum: 7 oktober 2024

- ![ fixpictogram ](../../assets/fix.svg) **Refactored code** - Verwijderde steun van oude PHP versies (7.4, 7.3, 7.2) en verwante bibliotheken.<!-- MCLOUD-9278 - -->
- ](../../assets/fix.svg) **Bevestigingspictogram ![ Bevorderde versie Monolog** - Toegevoegde steun voor monolog 3.6.<!-- MCLOUD-12855 - -->
- ![ fixpictogram ](../../assets/fix.svg) **Reparatie voor de Server van de Toepassing** - lost een bekende kwestie met de Server van de Toepassing van GraphQL op. Specifiek, bevatte `CatalogGraphQl\\Model\\Config\\AttributeReader` in versie 2.4.7 een insect dat tot GraphQL verzoeken kon leiden die reacties terugwinnen op verouderde configuratie van Attributen worden gebaseerd.<!-- ACPT-1876 -->

## v1.0.27

Releasedatum: 21 mei 2024

- **Steun voor PHP 8.3** - Deze flardoplossing verhelpt verenigbaarheidsfouten tussen php 8.3 en de composer pakketversie.

## v1.0.26

Releasedatum: 8 april 2024

- ![ nieuw pictogram ](../../assets/new.svg) **PHP** — Toegevoegde steun voor PHP 8.3.

## v1.0.25

Releasedatum: 16 januari 2024

- **de verbeteringen van het Geheime voorgeheugen** - Dit flard verbetert lay-outgeheim voorgeheugenefficiency, beduidend verminderend geheugengebruik, voor Adobe Commerce versies 2.4.4 en later.<!-- MCLOUD-11514 -->
- {de verbeteringen van de Banen van 0} CRON **- Dit flard bevestigt de kwestie waar de gemiste banen onnodig op de sloten van de kroonbaan voor versies 2.4.4 van Adobe Commerce en later wachten.<!-- MCLOUD-11329 -->**

## v1.0.24

Releasedatum: 15 september 2023

- **de verbetering van Prestaties** - Dit herstelt een kwestie die prestaties beïnvloedt door het aantal tijden te verminderen de zelfde lading van plaatsingsconfiguraties voor Adobe Commerce 2.4.6 aan 2.4.6-p1 <!-- MCLOUD-10604 -->

## v1.0.23

Releasedatum: 31 juli 2023

- **verwijdert het flard MCLOUD-10604** - Dit flard werd verplaatst naar QPT.<!-- MCLOUD-10736 -->

## v1.0.22

Releasedatum: 19 juni 2023

- **Verbeterde tovenaar/output van QPT CLI** - voegde een waarschuwing aan de tovenaar/de output toe QPT CLI die u eraan herinnert om flarddetails en vereisten te verifiëren als er gebiedsdelen zijn.<!-- ACP2E-1963 -->
- **Toegevoegde flarden voor Commerce 2.4.6:**
   - De `regexp cache tag` -validatie is gecorrigeerd. <!-- MCLOUD-10226 -->
   - Verbeterde prestaties door het aantal tijden te verminderen de zelfde lading van plaatsingsconfiguraties.<!-- MCLOUD-10604 -->
- **Toegevoegde flarden voor Commerce 2.3.7 aan 2.4.6** - Vaste een kwestie die een toename door een willekeurige waarde in plaats van een verhoging door 1 voor de `catalog_product_entity_*` lijsten veroorzaakte.<!-- MCLOUD-10032 -->
- **Toegevoegde flarden voor Commerce 2.4.0 aan 2.4.6** - Vaste een fout die dat `The file can't be deleted. Warning!unlink: No such file or directory` verklaart, die voorkwam toen het flushing JS/CSS geheime voorgeheugen van Admin.<!-- MCLOUD-10279 -->

## v1.0.21

Releasedatum: 10 maart 2023

- **Verbeterde steun voor PHP 8.2** - Vaste verenigbaarheidskwesties met bepaalde PHP 8.2.x versies om Commerce 2.4.6 te steunen.

## v1.0.20

Releasedatum: 27 oktober 2022

- **Toegevoegde L2 de verbeteringspatch van het geheime voorgeheugen** - Dit flard lost een kwestie met het spoelen van het lokale geheime voorgeheugen L2 voor versie 2.4.0 en 2.4.1 van Commerce op.<!-- MCLOUD-7845 -->

## v1.0.19

Releasedatum: 13 september 2022

- **Verbeterde steun voor PHP 8.1** - Vaste verenigbaarheidskwesties met bepaalde PHP 8.1.x versies.

## v1.0.18

Releasedatum: 11 augustus 2022

Kritieke patch voor Adobe Commerce 2.4.5:

- **Uitgave met orden die de betalingen van Braintree gebruiken** - Dit flard lost een kritieke kwestie op die beheerders verhindert nieuwe orden of herschikkingen te plaatsen.<!-- MCLOUD-9137 -->

Zie [ Admin kan geen orde tot stand brengen/opnieuw rangschikken wanneer Braintree betaling ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/admin-cant-create-order-reorder-when-braintree-payment-enabled.html) toeliet.

## v1.0.17

Releasedatum: 24 mei 2022

Correctie van beperkingen voor beveiligingspatches in het `patches.json` -bestand.

## v1.0.16

Releasedatum: 31 maart 2022

Kritieke patch voor Adobe Commerce 2.3.3-p1 en latere versies:

De bijgewerkte flarden om a **kritieke** kwetsbaarheid op te lossen die in unauthenticated verre codeuitvoering resulteert.<!-- MCLOUD-8479 -->

Zie [ bulletin van de Veiligheid van Adobe APSB22-12 ](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

Releasedatum: 10 maart 2022

- **Steun PHP 8.1** - Toegevoegde steun voor PHP 8.1 en gelaten vallen steun voor PHP 7.0 en 7.1.
- **Toegevoegd flard voor Adobe Commerce 2.3.3** - Vaste munt die op productpagina toont.

## v1.0.14

Releasedatum: 13 februari 2022

Kritieke patch voor Adobe Commerce 2.3.3-p1 en latere versies:

Toegevoegd een flard om a **kritieke** kwetsbaarheid op te lossen die in unauthenticated verre codeuitvoering resulteert.<!-- MCLOUD-8461 -->

Zie [ bulletin van de Veiligheid van Adobe APSB22-12 ](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

Releasedatum: 25 oktober 2021

- **Monolog van de Update** - werkte de minimumversie bij die voor het `monolog` pakket aan `^2.3` wordt vereist.<!-- ACMP-1263 -->
- **Niet-compatibele PHP methode** - Vaste onverenigbare PHP methode voor de versies 2.4.3 van Adobe Commerce en 2.3.7-p1.<!-- AC-384 -->
- **PHP fout** - Vaste a `PHP error 'Undefined variable: errorMessage' ...` fout die terwijl het proberen om een flard toe te passen voorkwam.<!-- ACP2E-138 -->

## v1.0.12

Releasedatum: 12 augustus 2021

Kritieke patch voor Adobe Commerce 2.4.3 en 2.3.7-p1:

- **Uitgave met API tarief beperkt** - Dit flard verbetert een standaardtariefgrens die Web APIs verhinderde verzoeken met meer dan 20 punten in een serie te verwerken. Deze patch verhoogt de standaardwaarde van de tariefgrens. Zie Adobe Commerce [ 2.4.3 versienota&#39;s ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/adobe-commerce/2-4-3#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

Releasedatum: 29 juli 2021

- **Vaste een kwestie die door B2B Gelaagd navigatiefatch toe te passen** wordt veroorzaakt - voor klanten die de B2B Gelaagde navigatiefatch hebben toegepast, lost deze moeilijke situatie een `Undefined offset` fout op die op de pagina van het Onderzoek na het schakelen van de mening van de Opslag toont.<!--MCLOUD-5287-->

- **Paypal het flard van de Afhandeling** - lost een kwestie van Adobe Commerce 2.3.7 met Uitdrukkelijke PayPal op waar de eerder geplaatste orderprijs wordt getoond.<!--MC-42674-->

- **de categoriessteun van het Reparatie** - Toegevoegde steun voor de categorieën van het verwerkingsflard en oorsprongbronnen die aan de Patches van de Kwaliteit worden toegewezen. De categorieën staan klanten toe om filters en het sorteren te gebruiken om flarden sneller te vinden wanneer het gebruiken van het [ Hulpmiddel van de Patches van de Kwaliteit ](https://github.com/magento/quality-patches) en het hulpmiddel van de Analyse van de Plaats-brede (SWAT). <!--MC-38577-->

## v1.0.10

Releasedatum: 10 mei 2021

- **Verenigbaarheid met Adobe Commerce 2.3.7** - het Opgeloste conflict van composergebiedsdelen voor installatie op Adobe Commerce 2.3.7.<!--MC-42131-->
- **Vaste een kwestie die door een gebundeld flard meerdere keren toe te passen** wordt veroorzaakt - die een gebundeld flard (die andere afgekeurde flarden omvat) meer dan eens toepast kon de inbegrepen afgedekte pakketten terugkeren. Alle pleisters worden nu slechts eenmaal aangebracht. Het proberen om het zelfde pakket opnieuw toe te passen toont een bericht dat de flard reeds is toegepast.<!--MC-41912-->
- **B2B Gelaagd navigatiepatch** - Vaste een andere kwestie die gelaagde navigatie verhinderde alle productopties te tonen wanneer de gebruiker de B2B Gedeelde Catalogus toelaat.<!--MCLOUD-7742-->

## v1.0.9

Releasedatum: 1 februari 2021

- **B2B Gelaagd navigatiepatch** - Vaste de kwestie die gelaagde navigatie verhinderde alle productopties te tonen wanneer B2B Gedeelde Catalogus werd toegelaten.<!--MCLOUD-6923-->
- **Verenigbaarheid met PHP 7.4** - Vaste een wolk-patches compatibiliteitskwestie met PHP 7.4.<!--MCLOUD-7367-->
- **Vervangen flarden worden zichtbaar** - Vaste een wolk-fskwestie waarin de verouderde flarden zichtbaar in de flardlijst na het toepassen van een vervangingsflard worden die de volledige inhoud van het verouderde flard bevat. Dit zou kunnen gebeuren als u een flard toepaste die verscheidene andere flarden combineerde.<!--MC-40626-->
- **Stille mislukkingen wanneer het toepassen van flarden** - Vaste een wolk-fskwestie waarin het `git apply` bevel stil er niet in slaagde om flarden in sommige milieu&#39;s toe te passen.<!--MC-40529-->

## v1.0.8

Releasedatum: 14 oktober 2020

- **de updates van de Verenigbaarheid voor magento/magento-cloud-flarden** - werkte `symfony` en `semver` versiebeperkingen in het `composer.json` dossier voor verenigbaarheid met Adobe Commerce 2.4.1 en recentere versies bij.<!--MCLOUD-7111-->

## v1.0.7

Releasedatum: 14 oktober 2020

- **Redis flarden voor Adobe Commerce 2.3.0 tot 2.3.5, 2.4.0** - werkte de Redis flarden bij om het toevoegen van producten aan een categorie te steunen wanneer het uitvoeren van Niveau 2 geheim voorgeheugen. <!--MCLOUD-6659-->

- **het flard van Braintree VBE** - lost een kwestie op die een fout produceerde toen een Beheerder probeerde om een Rapport van de Regeling van Braintree te bekijken. <!--MCLOUD-6684-->

- De opdracht `ece-patches apply` gebruikt nu de opdracht Unix `patch` om patches toe te passen als Git niet beschikbaar is op het hostsysteem. <!--MCLOUD-7069-->

## v1.0.6

Releasedatum:

- **verstuurt flarden voor Adobe Commerce 2.3.0 - 2.3.4** - optimaliseer mededeling en verbetert prestaties
   - De omvang van netwerkoverdrachten tussen Redis en Adobe Commerce verkleinen
   - Omgevingsfactoren bij laden en schrijven van Redis verhelpen
   - Basiscacheadapter opnieuw schrijven om fouten af te handelen bij het opslaan
   - Vermindering van CPU-verbruik <!--MCLOUD-6139-->

- **bevestigt flarden voor Adobe Commerce 2.3.0 - 2.3.5** - verbeter prestaties en bevestig fouten
   - Verbeter de implementatie van het cachevergrendelen om oneindige vergrendelingen te voorkomen
   - Het huidige vergrendelingsmechanisme verbeteren
   - Ondertekende vergrendelingen implementeren om te voorkomen dat parallelle aanvragen worden ontgrendeld
   - Los de volgende fout op die bij Redis-schrijfbewerking optreedt: `OOM command not allowed when used memory > maxmemory`
   - Verwerking voor onbewerkte cache corrigeren met de tag `cat_p` die wordt uitgevoerd tijdens productupdates <!--MCLOUD-6110-->

- Probleem verholpen dat een fout veroorzaakte bij het toepassen van de vereiste `amzn/amazon-pay-module` -patch op Adobe Commerce voor cloud-infrastructuurprojecten met Adobe Commerce v2.2.6 of 2.3.5, die deze module niet bevatten. Het patchproces slaat nu de `amzn/amazon-pay-module` -patch over als de module niet is geïnstalleerd. <!--MCLOUD-6588-->

## v1.0.5

Releasedatum: 26 juni 2020

- **herstelt prestatiesverbeteringen** - voegt Redis optimaliseringseigenschappen aan versies 2.3.3 en 2.3.4 van Adobe Commerce toe. Deze correcties zijn opgenomen in de Adobe Commerce-versie 2.3.5.<!--MCLOUD-5771-->

- **het logboekenricher van New Relic** - voegt Monolog ProcessorInterface toe die wordt vereist om verbeteringen aan het registreren van New Relic mogelijkheden te steunen die in de Componenten van de Wolk van versie 1.0.4 van Commerce worden geïntroduceerd. Deze patch is vereist voor de implementatie van Adobe Commerce 2.1.x. Als het flard niet wordt toegepast, ontbreekt de bouwstijl tijdens het `di:compile` proces.<!--MCLOUD-6029-->

## v1.0.4

Releasedatum: 12 mei 2020

- **Betaal Amazon checkout** - lost een kwestie met Amazon op betaalwidget die klanten verhinderde om de betalingsmethode op de _Controle &amp; de stap van Betalingen_ tijdens het controleproces te veranderen.<!--MCLOUD-5930-->

- **de vertoning van het Product op Categorie pagina** - lost een kwestie op die producten verhinderde op de categoriepagina in _tonen alle pagina&#39;s_ mening.<!--MCLOUD-5684-->

- **het beeld van de Bouwer van de Pagina uploadt** - lost een de interfacekwestie van de Bouwer van de Pagina op die soms de volgende fout veroorzaakte wanneer het uploaden van beelden aan de beeldgalerij: `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

- **onderdruk onnodige waarschuwingen van de sitemapgeneratie** - voegt een poging opnieuw toe wanneer de fouten tijdens sitemapgeneratie voorkomen en slaat klanten e-mailbericht in gevallen over waar de fouten automatisch kunnen worden teruggekregen.<!--MCLOUD-3025-->

- **de prestatieverbetering van de Plaats** - lost een prestatieskwestie met de `Magento\Framework\App\DeploymentConfig\Reader::load` functie op, die periodiek lange ladingstijden ervoer die plaatsprestaties beïnvloedden. <!--MCLOUD-5650-->

- Bijgewerkte patchtoewijzing voor patches voor betalingsmethoden om de betalingsmodules als doel in te stellen in plaats van het Magento-basispakket (magento/magento2-base), zodat de betalingspatches alleen worden toegepast als de betalingsmodules bestaan.<!--MCLOUD-5666-->

- Bijgewerkte patches voor compatibiliteit met Magento Open Source.<!--MCLOUD-5701-->

## v1.0.3

Releasedatum: 28 april 2020

- Toegevoegde oplossing voor de patch &quot;FPC wordt uitgeschakeld tijdens implementaties&quot; ter ondersteuning van Adobe Commerce 2.3.5.

## v1.0.2

Releasedatum: 27 februari 2020

Deze release bevat de volgende patches en oplossingen voor problemen:

- **de updates van de Verenigbaarheid voor magento/magento-cloud-flarden**

   - De beperkingen `symfony` en `semver` version in het `composer.json` -bestand zijn bijgewerkt vanwege compatibiliteit met Adobe Commerce 2.4 en latere versies. <!--MAGECLOUD-5127-->

   - Bijgewerkte beperkingen in `composer.json` voor compatibiliteit met `ece-tools` 2002.0.22 en latere versies van 2002.0.x.

- **Uitdrukkelijke Controle van PayPal** - Gepubliceerd op 12 februari, 2020, lost dit flard een kwestie op die orden beïnvloedt die met Uitdrukkelijke Betaling worden geplaatst PayPal waar het verzendadres voor de orde een landgebied specificeert dat manueel in het tekstgebied eerder dan geselecteerd van het drop-down menu op de Verzendpagina is ingegaan. Zie de volledige patchbeschrijving op de pagina voor het downloaden van de patch.

- **de plaatsingsmoeilijke situatie van de Toepassing** - voegde een flard toe om een kwestie te bevestigen die het volledige paginacache tijdens het plaatsingsproces onbruikbaar maakte. Deze patch is van toepassing op Adobe Commerce 2.3.2 en latere versies.

- **de parameter van het Werkingsgebied voor Async/Bulk API** - werkte dit flard bij om een syntaxisfout in het `composer.json` dossier te bevestigen. Deze patch geldt voor Magento Open Source 2.3.1 en 2.3.2. Zie de volledige patchbeschrijving op de pagina voor het downloaden van de patch.

## v1.0.1

Releasedatum: 6 februari 2020

We hebben alle Magento Open Source 2.x-patches van de downloadpagina voor software opgenomen in de release magento/magento-cloud-patches v1.0.1. Als u eerder patches naar uw project hebt gekopieerd, verwijdert u deze om conflicten te voorkomen.

Deze release bevat de volgende patches en oplossingen voor problemen:

- **bevestig kroonimplantaties en verbetert kroonvergrendeling**—

   - Hiermee wordt een probleem verholpen waarbij sommige snijtaken niet worden uitgevoerd vanwege een onjuiste statuswaarde in de tabel `cron_schedule` . Nu gebruiken we het Adobe Commerce-vergrendelingsframework om de status van de snijtaak te controleren en bij te werken in plaats van de tabel `cron_schedule` te gebruiken. Cron-taken die met een foutstatus zijn geëindigd, worden opnieuw uitgevoerd tijdens de volgende uitsnijding in plaats van 24 uur te wachten.

   - Voegt a _opnieuw probeert_ verrichting toe om blokkering tijdens updates aan de gegevens in de `cron_schedule` lijst te vermijden.

- **werkte `magento/magento-cloud-patches` bij om alle beschikbare flarden voor Magento Open Source 2.x** te omvatten - werkte het magento/magento-cloud-flardpakket bij om alle Magento Open Source 2.x flarden te omvatten beschikbaar op de pagina van de softwaredownloads. Als u eerder Magento Open Source-patches naar uw Adobe Commerce hebt gekopieerd op een cloudinfrastructuurproject, verwijdert u deze om conflicten te voorkomen.<!--MAGECLOUD-4606-->

- **de cataloguspagineringsmoeilijke situatie van Elasticsearch** - verving de de cataloguspagineringsflard van Elasticsearch die in magento/magento-cloud-patches v1.0 met een effectievere moeilijke situatie wordt geleverd.<!--MAGECLOUD-4847-->

- **de flarden van de Bouwer van de Pagina** - in de flarden van de Wolk voor Commerce 1.0.0, bundelden wij de flarden van de Bouwer van de Pagina om een bekende de verre codeuitvoering van de Bouwer van de Pagina te richten (RCE), met de aanvankelijke moeilijke situatie die op Adobe Commerce 2.3.3 wordt gebaseerd. We hebben deze patches bijgewerkt met een stabielere implementatie op basis van Adobe Commerce 2.3.4. Dit omvat meerdere optimalisaties voor het verhelpen van het probleem.<!--MAGECLOUD-4884-->

  Als u het pakket magento/magento-cloud-patches 1.0.0 hebt, bent u nog steeds beschermd tegen de kwetsbaarheidsproblemen met RCE van Page Builder. Als u aan 1.0.1 of later bijwerkt, hebt u een betere implementatie van de zelfde moeilijke situatie.

## v1.0.0

Releasedatum: 14 november 2019

Dit is de eerste versie van het [`magento/magento-cloud-patches` ](https://github.com/magento/magento-cloud-patches) -pakket. Dit is een nieuwe afhankelijkheid van de `ece-tools` -pakketversie 2002.0.22 of hoger.

Deze release bevat de volgende patches en oplossingen voor problemen:

- **de veiligheidspatches van de Bouwer van de Pagina voor 2.3.1.x en 2.3.2.x versies** - lost een kwestie in de voorproef van de Bouwer van de Pagina op die unauthenticated gebruikers toestaat om tot sommige malplaatjemethodes toegang te hebben die kunnen worden gebruikt om willekeurige codeuitvoering over het netwerk (RCE) teweeg te brengen die in globale informatielekken resulteert. Dit probleem kan zich voordoen bij het gebruik van niet-ondersteunde versies van Page Builder met Adobe Commerce versies 2.3.1 en 2.3.2.<!--MAGECLOUD-4649-->

- **de flarden van MSI** - moeilijke kwesties die indexerende fouten en prestatieskwesties veroorzaakten wanneer het gebruiken van standaardinventarismontages voor het beheren van voorraad.<!--MAGECLOUD-4428-->

- **Achterwaartse Verenigbaarheid van nieuwe Interfaces van de Post** - lost een achterwaartse onverenigbaarheidskwestie op die door de `Magento\Framework\Mail\EmailMessageInterface` PHP interface wordt veroorzaakt die in Adobe Commerce v2.3.3 wordt geïntroduceerd. In het bereik van deze patch zijn de nieuwe `EmailMessageInterface` overervingen van de oude `MessageInterface` en zijn Adobe Commerce-kernmodules weer afhankelijk van `MessageInterface` . <!--MAGECLOUD-4422-->

- **de paginering van de Catalogus werkt niet op Elasticsearch 6.x** - lost een kritieke kwestie met de paginering van het onderzoeksresultaat op die klanten gebruikend Elasticsearch 6.x als motor van de catalogusonderzoek.<!--MAGECLOUD-4448-->
