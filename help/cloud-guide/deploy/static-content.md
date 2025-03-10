---
title: Statische implementatie van inhoud
description: Leer meer over strategieën voor het implementeren van statische inhoud, zoals afbeeldingen, scripts en CSS, op Adobe Commerce op cloud-infrastructuurprojecten.
feature: Cloud, Build, Deploy, SCD
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Statische strategieën voor implementatie van inhoud

De statische plaatsing van de inhoud (SCD) heeft een significante invloed op het proces van de opslagplaatsing dat afhangt van hoeveel te produceren inhoud-zoals beelden, manuscripten, CSS, video&#39;s, thema&#39;s, scènes, en Web-pagina&#39;s-en wanneer om de inhoud te produceren. Bijvoorbeeld, produceert de standaardstrategie statische inhoud tijdens [ stelt fase ](process.md#deploy-phase-deploy-phase) op wanneer de plaats op onderhoudswijze is; nochtans, vergt deze plaatsingsstrategie tijd om de inhoud aan de opgezette `pub/static` folder direct te schrijven. U hebt verschillende opties of strategieën om u te helpen de implementatietijd afhankelijk van uw behoeften te verbeteren.

## JavaScript- en HTML-inhoud optimaliseren

U kunt bundeling en miniatuur gebruiken om geoptimaliseerde JavaScript- en HTML-inhoud te maken tijdens de implementatie van statische inhoud.

### Inhoud minimaliseren

U kunt de ladingstijd SCD tijdens het plaatsingsproces verbeteren als u het kopiëren van de statische meningsdossiers in de `var/view_preprocessed` folder overslaat en _geminimaliseerde_ HTML wanneer gevraagd produceert. U kunt dit activeren door [ SKIP_HTML_MINIFICATION ](../environment/variables-global.md#skiphtmlminification) globale omgevingsvariabele aan `true` in het `.magento.env.yaml` dossier te plaatsen.

>[!NOTE]
>
>Vanaf `ece-tools` package version 2002.0.13, is de standaardwaarde voor de SKIP_HTML_MINIFICATION-variabele ingesteld op `true` .

U kunt **meer** plaatsingstijd en schijfruimte besparen door het aantal onnodige themadossiers te verminderen. U kunt bijvoorbeeld het thema `magento/backend` in het Engels en een aangepast thema in andere talen gebruiken. U kunt deze themamontages met [ vormen SCD_MATRIX ](../environment/variables-deploy.md#scdmatrix) milieuvariabele.

## Een implementatiestrategie kiezen

De strategieën van de plaatsing verschillen gebaseerd op of u verkiest om statische inhoud tijdens de _bouwt_ fase, _op te stellen_ fase, of _op bestelling_. Zoals gezien in de volgende grafiek, is het produceren van statische inhoud tijdens de opstellen fase de minste optimale keus. Zelfs met geminiateerde HTML, moet elk inhoudsbestand naar de gekoppelde `~/pub/static` -map worden gekopieerd. Dit kan lang duren. Het genereren van statische inhoud op aanvraag lijkt de optimale keuze. Als het inhoudsbestand echter niet bestaat in de cache die het op dat moment genereert, wordt het opgevraagd. Hierdoor wordt laadtijd toegevoegd aan de gebruikerservaring. Daarom is het produceren van statische inhoud tijdens de bouwstijlfase de meest optimale.

![ SCD Vergelijking van de Lading ](../../assets/scd-load-times.png)

### Het SCD instellen bij het samenstellen

Het produceren van statische inhoud tijdens de bouwstijlfase met geminiateerde HTML is de optimale configuratie voor [**nul-onderbreking** plaatsingen ](reduce-downtime.md), ook gekend als **ideale staat**. In plaats van bestanden naar een gekoppeld station te kopiëren, maakt dit een koppeling vanuit de map `./init/pub/static` .

Voor het genereren van statische inhoud hebt u toegang tot thema&#39;s en landinstellingen nodig. Adobe Commerce slaat thema&#39;s op in het bestandssysteem, dat toegankelijk is tijdens de constructiefase. Adobe Commerce slaat de landinstellingen echter op in de database. Het gegevensbestand is _niet_ beschikbaar tijdens de bouwstijlfase. Als u statische inhoud wilt genereren tijdens de constructiefase, moet u de opdracht `config:dump` in het `ece-tools` -pakket gebruiken om landinstellingen naar het bestandssysteem te verplaatsen. De landinstellingen worden gelezen en in het `app/etc/config.php` -bestand opgeslagen.

**om uw project te vormen om SCD op bouwstijl** te produceren:

1. Wijzig op uw lokale werkstation de projectmap.
1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Verplaats landinstellingen naar het bestandssysteem en werk vervolgens het [`config.php` bestand ](../development/commerce-version.md#create-a-configphp-file) bij.

1. Het configuratiebestand van `.magento.env.yaml` moet de volgende waarden bevatten:

   - [ SKIP_HTML_MINIFICATION ](../environment/variables-global.md#skip_html_minification) is `true`
   - [ SKIP_SCD ](../environment/variables-build.md#skip_scd) op bouwstijlstadium is `false`
   - [ SCD_STRATEGY ](../environment/variables-build.md#scd_strategy) is `compact`

1. Verifieer configuratie van de [ nawerkingshaak ](../application/hooks-property.md) in het `.magento.app.yaml` dossier.

1. Verifieer uw montages door de [ Slimme tovenaar voor de ideale staat ](smart-wizards.md) in werking te stellen.

   ```bash
   php ./vendor/bin/ece-tools wizard:ideal-state
   ```

### SCD op verzoek instellen

Het genereren van SCD op verzoek is optimaal voor een ontwikkelingsworkflow in de integratieomgeving. Het vermindert plaatsingstijd zodat u uw implementaties kunt snel herzien en integratietests in werking stellen. Laat [ SCD_ON_DEMAND ](../environment/variables-global.md#scdondemand) milieuvariabele in het globale stadium van het `.magento.env.yaml` dossier toe. De variabele SCD_ON_DEMAND negeert alle andere configuraties met betrekking tot SCD en wist bestaande inhoud uit de map `~/pub/static` .

Wanneer het gebruiken van SCD op bestelling strategie, helpt het om het geheime voorgeheugen met pagina&#39;s vooraf te laden u verwacht om, zoals de homepage te verzoeken. Voeg uw lijst van verwachte pagina&#39;s in [ WARM_UP_PAGES ](../environment/variables-post-deploy.md#warmuppages) milieuvariabele in post-stelt stadium van het `.magento.env.yaml` dossier toe.

>[!WARNING]
>
>Gebruik de SCD-strategie op verzoek niet in de productieomgeving.

### SCD wordt overgeslagen

Soms kunt u het genereren van statische inhoud volledig overslaan. U kunt [ SKIP_SCD ](../environment/variables-build.md#skipscd) milieuvariabele in het globale stadium plaatsen om andere configuraties met betrekking tot SCD te negeren. Dit heeft geen invloed op de bestaande inhoud in de map `~/pub/static` .
