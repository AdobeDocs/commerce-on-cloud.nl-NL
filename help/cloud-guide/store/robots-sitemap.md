---
title: Robots voor site-toewijzing en zoekprogramma's toevoegen
description: Leer hoe u robots voor sites met hyperlinks en zoekprogramma's aan Adobe Commerce kunt toevoegen op cloudinfrastructuur.
feature: Cloud, Configuration, Search, Site Navigation
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# Robots voor site-toewijzing en zoekprogramma&#39;s toevoegen

Een poging om het `sitemap.xml` -bestand te genereren en naar de hoofdmap te schrijven, resulteert in de volgende fout:

```
Please make sure that "/" is writable by the web-server.
```

Met Adobe Commerce op cloudinfrastructuur kunt u alleen naar specifieke mappen schrijven, zoals `var` , `pub/media` , `pub/static` of `app/etc` . Wanneer u het `sitemap.xml` -bestand genereert met het deelvenster Beheer, moet u het `/media/` -pad opgeven.

U hoeft geen `robots.txt` -bestand te genereren omdat `robots.txt` -inhoud op aanvraag wordt gegenereerd en in de database wordt opgeslagen. U kunt de inhoud in uw browser weergeven met de koppeling `<domain.your.project>/robots.txt` of `<domain.your.project>/robots` .

Hiervoor is ECE-Tools versie 2002.0.12 en hoger vereist met een bijgewerkt `.magento.app.yaml` -bestand. Zie een voorbeeld van deze regels in de [ magento-wolkenbewaarplaats ](https://github.com/magento/magento-cloud/blob/master/.magento.app.yaml#L43-L49).

**om een `sitemap.xml` dossier in versie 2.2 en later** te produceren:

1. Open de beheerder.
1. Op het _Op de markt brengen_ menu, klik **Kaart van de Plaats** in de _SEO &amp; sectie van het Onderzoek_.
1. In de _mening van de Kaart van de Plaats_, klik **Sitemap** toevoegen.
1. In de _Nieuwe mening van de Kaart van de Plaats_, ga de volgende waarden in:

   - **filename**:`sitemap.xml`
   - **Weg**:`/media/`

1. Klik **sparen &amp; produceer**. De nieuwe plaatstoewijzing wordt beschikbaar in het _Net van de Kaart van de Plaats_.
1. Klik de weg in de _Verbinding voor de kolom van Google_.

**om inhoud aan het `robots.txt` dossier** toe te voegen:

1. Open de beheerder.
1. Voor het _menu van de Inhoud_, klik **Configuratie** in de _sectie van het Ontwerp_.
1. In de _mening van de Configuratie van het Ontwerp_, geeft de klik **&#x200B;**&#x200B;voor de website in de _kolom van de Actie_ uit.
1. In de _Belangrijkste mening van de Website_, klik **Robots van de Motor van het Onderzoek**.
1. Werk **uit geeft douaneinstructie van robots.txt** gebied uit.
1. Klik **sparen Configuratie**.
1. Controleer het bestand `<domain.your.project>/robots.txt` of de URL `<domain.your.project>/robots` in uw browser.

>[!NOTE]
>
>Als het `<domain.your.project>/robots.txt` dossier a `404 error` produceert, [ legt een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor om het omleiden van `/robots.txt` aan `/media/robots.txt` te verwijderen.

## Herschrijven met VCL-fragment snel

Als u verschillende domeinen hebt en u afzonderlijke site-overzichten nodig hebt, kunt u een VCL maken om naar de juiste sitemap te leiden. Genereer het bestand `sitemap.xml` in het deelvenster Beheer zoals hierboven beschreven en maak vervolgens een aangepast, snel VCL-fragment om het omleiden te beheren. Zie {de fragmenten van 0} Snelle VCL van de Douane &lbrace;[&#128279;](../cdn/fastly-vcl-custom-snippets.md).

>[!NOTE]
>
> U kunt aangepaste VCL-fragmenten uploaden vanuit de beheerinterface of via de snelheids-API. Zie [ de fragmentvoorbeelden en leerprogramma&#39;s van de Douane VCL ](../cdn/fastly-vcl-custom-snippets.md#example-vcl-snippet-code).

### Een VCL-fragment snel gebruiken voor omleiding

Maak een aangepast VCL-fragment om het pad voor `sitemap.xml` naar `/media/sitemap.xml` te herschrijven met de paren `type` en `content` key-value.

```json
{
  "name": "sitemapxml_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; }"
}
```

In het volgende voorbeeld wordt getoond hoe u het pad voor `robots.txt` en `sitemap.xml` to `/media/robots.txt` en `/media/sitemap.xml` herschrijft

```json
{
  "name": "sitemaprobots_rewrite",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path ~ \"^/?sitemap.xml$\" ) { set req.url = \"/media/sitemap.xml\"; } else if (req.url.path ~ \"^/?robots.txt$\") { set req.url = \"/media/robots.txt\";}"
}
```

**om een VCL fragment van het type Fastly te gebruiken voor bepaald domein opnieuw richt**:

Maak een `pub/media/domain_robots.txt` -bestand, waarbij het domein `domain.com` is, en gebruik het volgende VCL-fragment:

```json
{
  "name": "domain_robots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }}"
}
```

Het VCL-fragment routeert `http://domain.com/robots.txt` en geeft het `pub/media/domain_robots.txt` -bestand weer.

Als u een omleiding voor `robots.txt` en `sitemap.xml` in één fragment wilt configureren, maakt u `pub/media/domain_robots.txt` - en `pub/media/domain_sitemap.xml` -bestanden, waarbij het domein `domain.com` is, en gebruikt u het volgende VCL-fragment:

```json
{
  "name": "domain_sitemaprobots",
  "dynamic": "0",
  "type": "recv",
  "priority": "90",
  "content": "if ( req.url.path == \"/robots.txt\" ) { if ( req.http.host ~ \"(domain).com$\" ) { set req.url = \"/media/\" re.group.1 \"_robots.txt\"; }} else if ( req.url.path == \"/sitemap.xml\" ) { if ( req.http.host ~ \"(domain).com$\" ) {  set req.url = \"/media/\" re.group.1 \"_sitemap.xml\"; }}"
}
```

In de `sitemap` admin config, moet u de plaats van het dossier specificeren gebruikend `pub/media/` eerder dan `/`.

### Indexeren via zoekprogramma configureren

Om `robots.txt` aanpassingen in Productie te activeren, moet u **Indexeren door onderzoeksmotoren toelaten voor`<environment-name>`** optie in uw projectmontages is.

![ Gebruik [!DNL Cloud Console] om milieu&#39;s ](../../assets/robots-indexing-by-search-engine.png) te beheren

>[!NOTE]
>
>- Indexering door zoekmachines kan alleen worden ingeschakeld in Productie, maar niet in een van de lagere omgevingen.
>
>- Als u PWA Studio gebruikt en tot uw gevormd `robots.txt` dossier niet kunt toegang hebben, voeg `robots.txt` aan de [ Voorste Lijst van gewenste personen van de Naam ](https://github.com/magento/magento2-upward-connector#front-name-allowlist) bij **Opslag** > Configuratie > **Algemeen** > **Web** > de Configuratie van de PWA van UPWARD toe.
