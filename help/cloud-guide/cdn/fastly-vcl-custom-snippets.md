---
title: Aan de slag met aangepaste VCL-fragmenten
description: Leer over het gebruiken van de codefragmenten van de Taal van de Controle van de Varnish om de Fastly de dienstconfiguratie voor Adobe Commerce aan te passen.
feature: Cloud, Configuration, Services
exl-id: 90f0bea6-4365-4657-94e9-92a0fd1145fd
source-git-commit: a51946f65ccd606cde6fbb4278f625a49ae42dad
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 0%

---

# Aan de slag met aangepaste VCL

Steunt snel een aangepaste versie van de Taal van de Configuratie van de Varnish (VCL) om de Snelle de dienstconfiguratie aan uw vereisten aan te passen.

Aangepaste VCL-fragmenten zijn blokken VCL-logica die zijn toegevoegd aan de actieve VCL-versie die is geüpload naar uw Adobe Commerce-site. Een aangepast VCL-fragment wijzigt hoe services die snel in cache worden geplaatst, reageren op aanvraagverkeer. U kunt bijvoorbeeld een aangepast VCL-fragment toevoegen om alleen aanvraagverkeer vanaf opgegeven IP-adressen van de client toe te staan. U kunt ook een fragment maken om het verkeer te blokkeren van websites die bekend staan om het verzenden van spam naar uw Adobe Commerce-sites.

Aangepaste VCL-fragmenten - gegenereerd, gecompileerd en verzonden naar alle caches met een snelheid - laden en activeren zonder serverdowntime.

>[!NOTE]
>
>Alvorens douanecode VCL, randwoordenboeken, en ACLs aan uw Fastly moduleconfiguratie toe te voegen, verifieer dat de Fastly caching dienst met de standaardconfiguratie werkt. Zie [ vormen de Snelle diensten ](fastly-configuration.md).

Snelle ondersteuning voor twee typen aangepaste VCL-fragmenten:

- [ Regelmatige fragmenten ](https://docs.fastly.com/en/guides/about-vcl-snippets) - de regelmatige fragmenten van VCL van de Douane worden gecodeerd voor specifieke versies VCL. U kunt gewone VCL-fragmenten maken, wijzigen en implementeren via de API voor beheerders of snelkoppelingen.

- [ Dynamische fragmenten ](https://docs.fastly.com/en/guides/using-dynamic-vcl-snippets) - VCL fragmenten die gebruikend Fastly API worden gecreeerd. U kunt dynamische fragmenten wijzigen en opstellen zonder het moeten de Fastly versie VCL voor uw dienst bijwerken.

Wij adviseren gebruikend de fragmenten van douaneVCL met de Woordenboeken van Edge en de Lijsten van het Toegangsbeheer (ACL) om gegevens op te slaan die in uw douanecode worden gebruikt.

- [**het woordenboek van Edge** ](https://docs.fastly.com/guides/edge-dictionaries/about-edge-dictionaries) - slaat gegevens als zeer belangrijk-waardeparen in een woordenboekcontainer op die van de fragmenten van douaneVCL kan worden van verwijzingen voorzien

- [**ACL van Edge** ](https://docs.fastly.com/guides/access-control-lists/about-acls) - slaat de cliëntIP adresgegevens op die de toegangsbeheerlijst voor blok bepalen of regels toestaan die gebruikend de fragmenten van douaneVCL worden uitgevoerd

De woordenboeken en ACL gegevens worden opgesteld aan de Fastly Edge knopen die over netwerkgebieden toegankelijk zijn. Ook, kunnen de gegevens dynamisch over het netwerk worden bijgewerkt zonder u te vereisen om de code VCL voor uw het opvoeren of productiemilieu opnieuw op te stellen.

>[!NOTE]
>
>U kunt de fragmenten van douaneVCL aan een het Opvoeren of milieu van de Productie slechts toevoegen als u [ de Snelle diensten ](fastly-configuration.md) voor dat milieu hebt gevormd.

## Zelfstudie

Deze zelfstudie en voorbeelden demonstreren het gebruik van gewone aangepaste VCL-fragmenten met Edge-woordenboeken en Edge ACL&#39;s om de Fastly-serviceconfiguratie voor Adobe Commerce aan te passen. Raadpleeg de documentatie bij Snelheid voor meer informatie:

- [ Gids om snel VCL ](https://docs.fastly.com/guides/vcl/guide-to-vcl) - Informatie over de Fastly Varnish implementatie, de Snelle uitbreidingen van VCL, en middelen voor het leren van meer over Varnish en VCL.
- [ VCL verwijzing 1&rbrace; - Gedetailleerde programmeringsverwijzing snel om douaneVCL en de fragmenten van douaneVCL te ontwikkelen en problemen op te lossen.](https://docs.fastly.com/guides/vcl/)

U kunt aangepaste VCL-fragmenten maken en beheren via Adobe Commerce Admin of met de snelheids-API:

- [ Admin van Adobe Commerce ](#manage-custom-vcl-from-admin) - wij adviseren gebruikend Adobe Commerce Admin om de fragmenten van douaneVCL te beheren omdat het het proces automatiseert om, de veranderingen VCL in de de dienstconfiguratie van de Fastly te bevestigen te uploaden en toe te passen. Bovendien kunt u de aangepaste VCL-fragmenten die aan de Fastly-serviceconfiguratie zijn toegevoegd, weergeven en bewerken via de beheerfunctie.

- [ snel API ](#manage-vcl-using-the-api) - als u tot Admin niet kunt toegang hebben, gebruik snel API om de fragmenten van douaneVCL te beheren. Gebruik bijvoorbeeld de API om de Fastly-serviceconfiguratie problemen op te lossen wanneer de site uitvalt, of om een aangepast VCL-fragment toe te voegen. Bovendien kunnen sommige bewerkingen alleen met de API worden voltooid. U moet de API bijvoorbeeld gebruiken om een oudere VCL-versie te reactiveren of om alle VCL-fragmenten in een opgegeven VCL-versie weer te geven. Zie [ API snelle verwijzing voor fragmenten VCL ](#api-quick-reference-for-vcl-snippets).

### Voorbeeld-VCL-fragmentcode

In het volgende voorbeeld wordt het aangepaste VCL-fragment (JSON-indeling) getoond dat verkeer filtert op IP-adres van client:

```json
{
  "service_id": "FASTLY_SERVICE_ID",
  "version": "{Editable Version #}",
  "name": "apply_acl",
  "priority": "100",
  "dynamic": "1",
  "type": "hit",
  "content": "if ((client.ip ~ {ACLNAME}) && !req.http.Fastly-FF){ error 403; }"
}
```

>[!WARNING]
>
>In dit voorbeeld is de VCL-code geformatteerd als een JSON-payload die naar een bestand kan worden opgeslagen en in een Fastly API-aanvraag kan worden verzonden. Als u JSON-validatiefouten wilt voorkomen bij het verzenden van het fragment als JSON voor een API-aanvraag, gebruikt u een backslash om speciale tekens in de code te verwijderen. Zie [ Gebruikend dynamische fragmenten VCL ](https://docs.fastly.com/vcl/vcl-snippets/) in de Fastly documentatie VCL. Als u het VCL-fragment vanuit Beheer verzendt, hoeft u geen speciale tekens te verwijderen.

De logica VCL in het `content` gebied voert de volgende acties uit:

- Controleert het inkomende IP adres, `client.ip` op elke aanvraag

- Blokkeert om het even welk verzoek met een IP adres inbegrepen in *ACLNAME* rand ACL, die a `403 Forbidden` fout terugkeert

De volgende lijst verstrekt details over zeer belangrijke gegevens voor de fragmenten van douaneVCL. Voor een meer gedetailleerde verwijzing, zie de [ VCL fragmenten ](https://docs.fastly.com/api/config#api-section-snippet) verwijzing in de Snelle documentatie.

| Waarde | Beschrijving |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `API_KEY` | De API-sleutel voor toegang tot uw snelaccount. Zie [ geloofsbrieven ](fastly-configuration.md) krijgen. |
| `active` | Actieve status van een fragment of versie. Retourneert `true` of `false` . Indien waar (true), wordt het fragment of de versie gebruikt. Een actief fragment klonen met het versienummer ervan. |
| `content` | Het fragment van VCL-code dat moet worden uitgevoerd. Snelheid biedt geen ondersteuning voor alle VCL-taalfuncties. Bovendien beschikt Fastly over aangepaste functionaliteit voor extensies. Voor details over gesteunde eigenschappen, zie de [ VCL programmeringsverwijzing van de Snelle VCL ](https://docs.fastly.com/vcl/reference/). |
| `dynamic` | Dynamische status van een fragment. Keert `false` voor [ regelmatige fragmenten ](https://docs.fastly.com/en/guides/about-vcl-snippets) inbegrepen in versioned VCL voor de Snelle de dienstconfiguratie terug. Keert `true` voor a [ dynamisch fragment ](https://docs.fastly.com/vcl/vcl-snippets/using-dynamic-vcl-snippets/) terug dat kan worden gewijzigd en worden opgesteld zonder een nieuwe versie te vereisen VCL. |
| `number` | VCL-versienummer waar het fragment wordt opgenomen. Gebruikt snel *Bewerkbare Versie #* in hun voorbeeldwaarden. Als u aangepaste fragmenten uit de API toevoegt, neemt u het versienummer op in de API-aanvraag. Als u aangepaste VCL toevoegt via de beheerfunctie, is de versie beschikbaar voor u. |
| `priority` | Numerieke waarde van `1` tot `100` die opgeeft wanneer de aangepaste VCL-fragmentcode wordt uitgevoerd. Fragmenten met lagere prioriteitswaarden worden eerst uitgevoerd. Als deze waarde niet wordt opgegeven, wordt de standaardwaarde `priority` gebruikt.`100`<p>Elk aangepast VCL-fragment met een prioriteitswaarde van `5` wordt direct uitgevoerd. Dit is het meest geschikt voor VCL-code die aanvraag routering implementeert (blok en lijsten van gewenste personen en omleidingen). Prioriteit `100` is het meest geschikt voor het overschrijven van standaard VCL-fragmentcode.<p>Alle [ standaardVCL fragmenten ](fastly-configuration.md#upload-vcl-snippets) inbegrepen in de Magento-Fastly module hebben `priority=50`.<ul><li>Wijs een hoge prioriteit toe zoals `100` om aangepaste VCL-code na alle andere VCL-functies uit te voeren en de standaard VCL-code te overschrijven.</li></ul> |
| `service_id` | De snelste service-id voor een specifieke omgeving voor Staging of Productie. Deze identiteitskaart wordt toegewezen wanneer uw project aan Adobe Commerce op de de dienstrekening van de wolkeninfrastructuur [ wordt toegevoegd Fastly ](fastly.md#fastly-service-account-and-credentials). |
| `type` | Geeft de locatie op voor het invoegen van het gegenereerde fragment, zoals `init` (boven subroutines) en `recv` (binnen subroutines). Voor details, zie de Snelle [ VCL fragmenten ](https://docs.fastly.com/api/config#api-section-snippet) verwijzing. |

## Aangepaste VCL beheren vanuit beheerder

U kunt [ de fragmenten van douaneVCL ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md) van de *Snelle Configuratie* toevoegen > *de sectie van de Fragmenten van de Douane VCL* in Admin.

![ beheer de fragmenten van douaneVCL ](../../assets/cdn/fastly-edit-snippets.png)

De *de fragmenten van de Douane VCL* mening toont slechts fragmenten die door Admin zijn toegevoegd. Als de fragmenten gebruikend Fastly API worden toegevoegd, gebruik API om hen [ te beheren ](#manage-vcl-using-the-api).

De volgende voorbeelden laten zien hoe u aangepaste VCL-fragmenten maakt en beheert vanuit de beheerfunctie en hoe u snel Edge-modules en Edge-woordenboeken kunt gebruiken:

- [Aanvragen voor een CMS-backend routeren](fastly-vcl-wordpress.md)
- [Blokverwijzingsspam](fastly-vcl-badreferer.md)
- [Blokverwijzingsspam](fastly-vcl-badreferer.md)
- [Aangepaste VCL voor IP-lijst van gewenste personen](fastly-vcl-allowlist.md)
- [Aangepaste VCL voor IP-lijst van gewezen personen](fastly-vcl-blocking.md)
- [Snelcache omzeilen](fastly-vcl-bypass-to-origin.md)

## Fragmenten die niet kunnen worden weergegeven of gewijzigd in Commerce Admin

Sommige fragmenten kunt u niet rechtstreeks in Commerce Admin weergeven of wijzigen. Bijvoorbeeld, [ dynamische fragmenten ](https://docs.fastly.com/en/guides/using-dynamic-vcl-snippets). In de sectie van de Fragmenten van de Douane VCL, zult u geen fragmenten zien die door het team van de Steun van de Wolk direct aan het [ Fastly beheersdashboard ](fastly.md#fastly-service-account-and-credentials) werden toegevoegd.


**om de fragmenten waar te nemen die door het team van de Steun van de Wolk worden toegevoegd:**

1. Ga naar de **sectie van Hulpmiddelen**.

1. Klik **Lijst alle versies** naast _de Geschiedenis van de Versie_.

1. Klik het oogpictogram naast de toepasselijke Versie van VCL om de bestaande fragmenten te bekijken.


## VCL beheren met de API

De volgende analyse toont u hoe te om regelmatige VCL fragmentdossiers tot stand te brengen en hen toe te voegen aan uw Snelle de dienstconfiguratie gebruikend Snelle API. U kunt de fragmenten van de *terminal* toepassing tot stand brengen en beheren. U hebt geen SSH-verbinding in een specifieke omgeving nodig.

**Eerste vereisten:**

- Configureer uw Adobe Commerce op de cloud-infrastructuur voor snelle services. Zie [ Opstelling snel ](fastly-configuration.md).

- [ krijgt snel API geloofsbrieven ](fastly-configuration.md) om verzoeken aan Fastly voor authentiek te verklaren API. Zorg ervoor dat u de geloofsbrieven voor het correcte milieu krijgt: het Opvoeren of de Productie.

- Sla snel de dienstgeloofsbrieven van de sparen als basisomgevingsvariabelen die u in cURL bevelen kunt gebruiken:

  ```bash
  export FASTLY_SERVICE_ID=<Service-ID>
  ```

  ```bash
  export FASTLY_API_TOKEN=<API-Token>
  ```

  De geëxporteerde omgevingsvariabelen zijn alleen beschikbaar in de huidige basissessie en gaan verloren wanneer u de terminal sluit. U kunt variabelen opnieuw definiëren door een nieuwe waarde te exporteren. U kunt als volgt de lijst met geëxporteerde variabelen weergeven die betrekking hebben op Snelheid:

  ```bash
  export | grep FASTLY
  ```

## VCL-fragmenten toevoegen

Deze zelfstudie bevat de basisstappen voor het toevoegen van aangepaste fragmenten met de snelheids-API.

>[!NOTE]
>
>Leren hoe te om de fragmenten van douaneVCL van Adobe Commerce te beheren Admin, zie [ VCL van Adobe Commerce beheren Admin ](#manage-custom-vcl-from-admin).


**Eerste vereisten**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

### Stap 1: Zoek de actieve VCL-versie

Gebruik de Fastly API [ krijgt versie ](https://docs.fastly.com/api/config#version_dfde9093f4eb0aa2497bbfd1d9415987) verrichting om het actieve VCL versieaantal te krijgen:

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/active
```

In het JSON-antwoord noteert u het actieve VCL-versienummer dat in de `number` -toets wordt geretourneerd, bijvoorbeeld `"number": 99` . U hebt het versienummer nodig wanneer u de VCL kloont om te bewerken.

```json
{
  "testing": false,
  "locked": true,
  "number": 99,
  "active": true,
  "service_id": "872zhjyxhto5SIRb3GAE0",
  "staging": false,
  "created_at": "2019-01-29T22:38:53Z",
  "deleted_at": null,
  "comment": "Magento Module uploaded VCL",
  "updated_at": "2019-01-29T22:39:06Z",
  "deployed": false
}
```

Sla het actieve versienummer op in een basisomgevingsvariabele voor gebruik in volgende API-aanvragen:

```bash
export FASTLY_VERSION_ACTIVE=<Version>
```

### Stap 2: De actieve VCL-versie en alle fragmenten klonen

Voordat u aangepaste VCL-fragmenten kunt toevoegen of wijzigen, moet u een kopie van de actieve VCL-versie maken voor bewerking. Gebruik de Fastly API [ kloonverrichting ](https://docs.fastly.com/api/config#version_7f4937d0663a27fbb765820d4c76c709):

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION_ACTIVE/clone -X PUT
```

In de reactie JSON, wordt het versieaantal verhoogd, en de *actieve* zeer belangrijke waarde is `false`. U kunt de nieuwe, inactieve versie van VCL plaatselijk wijzigen.

```json
{
  "testing": false,
  "locked": false,
  "number": 100,
  "active": false,
  "service_id": "vW2bLFWhhto5SIRb3GAE0",
  "staging": false,
  "created_at": "2019-01-29T22:38:53Z",
  "deleted_at": null,
  "comment": "Magento Module uploaded VCL",
  "updated_at": "2019-01-29T22:39:06Z",
  "deployed": false
}
```

Sla het nieuwe versienummer op in een basisomgevingsvariabele voor gebruik in volgende opdrachten:

```bash
export FASTLY_EDIT_VERSION=<Version>
```

### Stap 3: Een aangepast VCL-fragment maken

Maak en sla uw aangepaste VCL-code op in een JSON-bestand met de volgende inhoud en indeling:

```json
{
  "name": "<name>",
  "dynamic": "0",
  "type": "<type>",
  "priority": "100",
  "content": "<code all in one line>"
}
```

De volgende waarden zijn beschikbaar:

- `name` - Naam voor het fragment VCL.

- `dynamic` - wijst erop als dit a [ regelmatig fragment ](https://docs.fastly.com/en/guides/about-vcl-snippets) of a [ dynamisch fragment ](https://docs.fastly.com/guides/vcl-snippets/using-dynamic-vcl-snippets) is.

- `type` - Geeft de locatie op voor het invoegen van het gegenereerde fragment, zoals `init` (boven subroutines) en `recv` (binnen subroutines). Zie [ VCL fragmentobjecten ](https://docs.fastly.com/api/config#snippet) voor informatie over deze waarden snel.

- `priority` - Een waarde van `1` tot `100` die bepaalt wanneer de aangepaste VCL-fragmentcode wordt uitgevoerd. Aangepaste VCL-fragmenten met lagere waarden worden eerst uitgevoerd.

  Alle standaard VCL-code uit de Fastly VCL-module heeft de waarde `priority` `50` . Als u wilt dat een actie het laatst plaatsvindt of dat de standaard VCL-code wordt genegeerd, gebruikt u een hoger getal, zoals `100` . Als u aangepaste VCL-fragmentcode direct wilt uitvoeren, stelt u de prioriteit in op een lagere waarde, zoals `5` .

- `content` - Het fragment van VCL-code dat op één regel wordt uitgevoerd, zonder regeleinden. Zie [ het fragment van douaneVCL van het Voorbeeld ](#example-vcl-snippet-code).

### Stap 4: voeg VCL-fragment toe aan de snelconfiguratie

Gebruik snel API [ creeert fragment ](https://docs.fastly.com/api/config#snippet_41e0e11c662d4d56adada215e707f30d) verrichting om het fragment van douaneVCL aan de versie toe te voegen VCL.

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/snippet -H 'Content-Type: application/json' -X POST --data @<filename.json>
```

`<filename.json>` is de naam van het bestand dat u in de vorige stap hebt voorbereid. Herhaal deze opdracht voor elk VCL-fragment.

Als u een `500 Internal Server Error` reactie van de Fastly-service ontvangt, controleert u de syntaxis van het JSON-bestand om te controleren of u een geldig bestand uploadt.

### Stap 5: Valideer en activeer aangepaste VCL-fragmenten

Nadat u een aangepast VCL-fragment hebt toegevoegd, wordt het fragment snel ingevoegd in de VCL-versie die u bewerkt. Als u wijzigingen wilt toepassen, voert u de volgende stappen uit om de VCL-fragmentcode te valideren en de VCL-versie te activeren.

1. Gebruik snel API [ bevestigt VCL versie ](https://docs.fastly.com/api/config#version_97f8cf7bfd5dc2e5ea1933d94dc5a9a6) verrichting om de bijgewerkte code te verifiëren VCL.

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/validate
   ```

   Als de Fastly-API een fout retourneert, verhelpt u het probleem en valideert u de bijgewerkte VCL-versie opnieuw.

1. Gebruik snel API [ activeer ](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) verrichting om de nieuwe versie te activeren VCL.

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/activate -X PUT
   ```


## Snelle API-referentie voor VCL-fragmenten

In deze API-aanvraagvoorbeelden worden geëxporteerde omgevingsvariabelen gebruikt om de referenties te leveren die u snel wilt verifiëren. Voor details op deze bevelen, zie [ Snelle API verwijzing ](https://docs.fastly.com/api/config#vcl).

>[!NOTE]
>
>Gebruik deze opdrachten om fragmenten te beheren die u met de snelheids-API hebt toegevoegd. Als u fragmenten van Admin toevoegde, zie [ VCL fragmenten beheren gebruikend Admin ](#manage-vcl-using-the-api).

- **krijgt actief VCL versieaantal**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/active
  ```

- **Lijst alle regelmatige fragmenten VCL in bijlage aan de dienst**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet
  ```

- **herzie een individueel fragment**

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name>
  ```

  De `<snippet_name>` is de naam van een fragment, zoals `my_regular_snippet` .

- **werk een fragment** bij

  Wijzig het [ voorbereide JSON- dossier ](#step-3-create-a-custom-vcl-snippet) en verzend het volgende verzoek:

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name> -H 'Content-Type: application/json' -X PUT --data @<filename.json>
  ```

- **Schrap een individueel fragment VCL**

  Hiermee wordt een lijst met fragmenten opgehaald en wordt de volgende opdracht `curl` met de specifieke fragmentnaam gebruikt om te verwijderen:

  ```bash
  curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name> -X DELETE
  ```

- **Overschrijf waarden in het [ gebrek VCL code ](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets)**

  Maak een fragment met bijgewerkte waarden en wijs een prioriteit van `100` toe.
