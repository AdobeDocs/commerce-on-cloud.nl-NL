---
title: Aangepaste VCL voor het blokkeren van aanvragen
description: Blok inkomende verzoeken door IP adres gebruikend een lijst van het Toegangsbeheer van Edge (ACL) met een fragment van douaneVCL.
feature: Cloud, Configuration, Security
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Aangepaste VCL voor het blokkeren van aanvragen

U kunt de Fastly CDN module voor Magento 2 gebruiken om Edge ACL met een lijst van IP adressen tot stand te brengen die u wilt blokkeren. Vervolgens kunt u die lijst gebruiken met een VCL-fragment om binnenkomende aanvragen te blokkeren. De code controleert het IP adres van het inkomende verzoek. Als het een IP adres aanpast inbegrepen in ACL lijst, blokkeert snel het verzoek om tot uw plaats toegang te hebben en keert a `403 Forbidden error` terug. Alle andere client-IP-adressen hebben toegang.

**Eerste vereisten:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Lijst met client-IP-adressen die moeten worden geblokkeerd

## Edge ACL maken voor het blokkeren van client IP-adressen

U creeert Edge ACL om de lijst van IP te bepalen adressen aan blok. Na het creëren van ACL, kunt u het in een fragment van douaneVCL gebruiken om toegang tot uw het Opvoeren of plaats van de Productie te beheren.

Beheer toegang voor zowel het Opvoeren als de plaatsen van de Productie door Edge ACL met de zelfde naam in beide milieu&#39;s te creëren. De VCL-fragmentcode is van toepassing op beide omgevingen.

1. Meld u aan bij de beheerder.
1. Navigeer aan **Opslag** > Montages > **Configuratie** > **Geavanceerd** > **Systeem** > **Volledige het Geheime voorgeheugen van de Pagina** > **Gemakkelijke Configuratie**.
1. Breid **ACL van Edge** sectie uit.
1. Klik **toevoegen ACL** om een lijst tot stand te brengen. In dit voorbeeld geeft u de lijst &quot;lijst van gewezen personen&quot; een naam.
1. Voer IP-adreswaarden in de lijst in. Alle client-IP-adressen die aan deze lijst worden toegevoegd, worden geblokkeerd en hebben geen toegang tot de site.
1. Naar keuze, selecteer **GeNegeerde** checkbox indien nodig.

U verwijst Edge ACL door naam in uw VCL fragmentcode.

## De aangepaste VCL voor de lijst van gewezen personen maken

>[!NOTE]
>
>In dit voorbeeld ziet u hoe u geavanceerde gebruikers een VCL-codefragment kunt maken om aangepaste blokkeringsregels te configureren voor het uploaden naar de Fastly-service. U kunt een lijst van gewezen personen of een lijst van gewenste personen vormen die op land van Adobe Commerce wordt gebaseerd Admin gebruikend de [ Blokkerende ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) eigenschap beschikbaar in Fastly CDN voor Magento 2 module.

Nadat u Edge ACL bepaalt, kunt u het gebruiken om het fragment tot stand te brengen VCL om toegang tot de IP adressen te blokkeren die in ACL worden gespecificeerd. U kunt hetzelfde VCL-fragment gebruiken in zowel de testomgeving als de productieomgeving, maar u moet het fragment afzonderlijk uploaden naar elke omgeving.

De volgende het fragmentcode van douaneVCL (formaat JSON) toont de logica om inkomende verzoeken met een cliëntIP adres te blokkeren dat een adres in lijst van gewezen personen ACL aanpast.

```json
{
  "name": "blocklist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.ip ~ blocklist) { error 403 \"Forbidden\"; }"
}
```

Voordat u een op dit voorbeeld gebaseerd fragment maakt, controleert u de waarden om te bepalen of u wijzigingen wilt aanbrengen:

- `name`: naam voor het VCL-fragment. In dit voorbeeld hebben we de naam `blocklist` gebruikt.

- `priority`: hiermee wordt bepaald wanneer het VCL-fragment wordt uitgevoerd. De prioriteit is `5` om onmiddellijk in werking te stellen en te controleren of een Admin- verzoek uit een toegestaan IP adres komt. Het fragment loopt vóór om het even welk standaard Magento VCL fragmenten (`magentomodule_*`) toegewezen een prioriteit van 50. Stel de prioriteit voor elk aangepast fragment in op een waarde hoger of lager dan 50, afhankelijk van het tijdstip waarop het fragment moet worden uitgevoerd. Fragmenten met een lagere prioriteit worden eerst uitgevoerd.

- `type` - Geeft het type VCL-fragment op dat de locatie van het fragment in de gegenereerde VCL-code bepaalt. In dit voorbeeld gebruiken we `recv` , dat de VCL-code in de `vcl_recv` -subroutine invoegt, onder de vaste plaat VCL en boven alle objecten. Zie de [ Snelle VCL fragmentverwijzing ](https://docs.fastly.com/api/config#api-section-snippet) voor de lijst van fragmenttypes.

- `content`: Het fragment van VCL-code dat moet worden uitgevoerd, dat het client-IP-adres controleert. Als IP in ACL van Edge is, wordt het geblokkeerd van toegang met een `403 Forbidden` fout voor de volledige website. Alle andere client-IP-adressen hebben toegang.

Na het herzien van en het bijwerken van de code voor uw milieu, gebruik één van beiden van de volgende methodes om het fragment van douaneVCL aan uw Fastly de dienstconfiguratie toe te voegen:

- [ voeg het fragment van douaneVCL van Admin ](#add-the-custom-vcl-snippet) toe. Deze methode wordt aanbevolen als u toegang kunt krijgen tot de beheerder. (Vereist [ Snelle versie 1.2.58 ](fastly-configuration.md#upgrade-fastly-module) of later.)

- Sparen het JSON codevoorbeeld aan een dossier (bijvoorbeeld, `blocklist.json`) en [ uploadt het gebruikend Fastly API ](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Gebruik deze methode als u geen toegang hebt tot de beheerder.

## Het aangepaste VCL-fragment toevoegen

{{admin-login-step}}

1. Klik **Opslag** > Montages > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Breid **Volledige het Geheime voorgeheugen van de Pagina** > **Snelle Configuratie** uit > **de Fragmenten van VCL van de Douane**.

1. Klik **creëren het Fragment van de Douane**.

1. Voeg de waarden van het VCL-fragment toe:

   - **Naam** — `blocklist`

   - **Type** — `recv`

   - **Prioriteit** — `5`

   - Voeg de **VCL** fragmentinhoud toe:

     ```conf
     if ( client.ip ~ blocklist) { error 403 "Forbidden"; }
     ```

1. Klik **creëren** om het VCL fragmentdossier met het naampatroon `type_priority_name.vcl` te produceren, bijvoorbeeld `recv_5_blocklist.vcl`

1. Na de pagina herlaadt, uploadt de klik **VCL aan Fastly** in de *Snelle sectie van de Configuratie* om het dossier aan de Snelle de dienstconfiguratie toe te voegen.

1. Na uploads, vernieuw het geheime voorgeheugen volgens het bericht bij de bovenkant van de pagina.

Hiermee wordt de bijgewerkte versie van de VCL-code snel gevalideerd tijdens het uploadproces. Als de validatie mislukt, bewerkt u het aangepaste VCL-fragment om het probleem op te lossen. Vervolgens uploadt u de VCL opnieuw.

## Aanvullende VCL-voorbeelden voor het blokkeren van aanvragen

De volgende voorbeelden tonen hoe te om verzoeken te blokkeren gebruikend gealigneerde voorwaardenverklaringen in plaats van een ACL lijst.

>[!WARNING]
>
>In deze voorbeelden is de VCL-code opgemaakt als een JSON-payload die naar een bestand kan worden opgeslagen en in een Fastly API-aanvraag kan worden verzonden. U kunt het [ fragment VCL van Admin ](#add-the-custom-vcl-snippet) voorleggen, of als koord JSON gebruikend Snelle API. Als u validatiefouten wilt voorkomen wanneer u de snelheids-API gebruikt met een JSON-tekenreeks, moet u een backslash gebruiken om speciale tekens te verwijderen.

>[!NOTE]
>Als u het VCL-fragment vanuit Beheer verzendt, haalt u de afzonderlijke waarden uit de VCL-voorbeeldcode en voert u deze in de desbetreffende velden in. Bijvoorbeeld:
>- Naam: `<name of the VCL>`
>- Dynamisch: `<0/1>`
>- Type: `<type>`
>- Prioriteit: `<priority>`
>- Inhoud: `<content>`

Zie [ Gebruikend dynamische fragmenten VCL ](https://docs.fastly.com/vcl/vcl-snippets/) in de Fastly documentatie VCL.

### VCL-codevoorbeeld: blokcode per land

In dit voorbeeld wordt de ISO 3166-1-landcode van twee tekens gebruikt voor het land dat aan het IP-adres is gekoppeld.

```json
{
  "name": "blockbycountrycode",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( client.geo.country_code == \"HK\" ) { error 405 \"Not allowed\";}"
}
```

>[!NOTE]
>
>In plaats van het gebruiken van een fragment van douaneVCL, kunt u de Snelle [&#128279;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BLOCKING.md) eigenschap van het Blokkeren  in Adobe Commerce op beheerder van de wolkeninfrastructuur gebruiken om het blokkeren door landcode of een lijst van landcodes te vormen.

### Voorbeeld van VCL-code: Blok door aanvraagheader van HTTP-gebruikersagent

```json
{
  "name": "blockbyuseragent",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( req.http.User-Agent ~ \"(UCBrowser|MQQBrowser|LieBaoFast|Mb2345Browser)\" ) {error 405 \"Not allowed\";}"
}
```

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
