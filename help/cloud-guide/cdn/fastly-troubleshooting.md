---
title: Snelle probleemoplossing
description: Leer hoe u de snelste CDN-module en -services voor Adobe Commerce kunt oplossen en beheren.
feature: Cloud, Configuration, Cache, Services
exl-id: 69954ef9-9ece-411e-934e-814a56542290
source-git-commit: f496a4a96936558e6808b3ce74eac32dfdb9db19
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%

---

# Snelle probleemoplossing

Gebruik de volgende informatie om de Fastly CDN module voor Magento 2 in uw Adobe Commerce op het projectmilieu van de wolkeninfrastructuur problemen op te lossen en te beheren. U kunt bijvoorbeeld de headerwaarden van reacties en het gedrag van caching onderzoeken om problemen met services en prestaties snel op te lossen.

Op ProProductie en het Staging milieu&#39;s, kunt u [&#x200B; logboeken van New Relic &#x200B;](../monitor/log-management.md) gebruiken om snel CDN en het logboekgegevens van WAF te bekijken en te analyseren om fouten en prestatiesproblemen problemen op te lossen.

>[!NOTE]
>
>Voor informatie over vestiging en het vormen van Fastly, zie [&#x200B; Opstelling Fastly &#x200B;](fastly.md).

## Service-id snel zoeken

U hebt de snelste service-id nodig om snel vanaf de beheerder te configureren of snel API-aanvragen voor geavanceerde snelle configuratie en probleemoplossing in te dienen.

Als Fastly in uw projectmilieu wordt toegelaten, kunt u de dienstidentiteitskaart van Admin krijgen. Zie [&#x200B; krijgen de Snelle geloofsbrieven &#x200B;](fastly-configuration.md#get-fastly-credentials).

Ontwikkelaars en gevorderde VCL-gebruikers kunnen aangepaste VCL gebruiken om de service-id op te halen met behulp van de snelvariabele `req.service_id` . U kunt bijvoorbeeld de instructie `req.service_id` toevoegen aan de aangepaste logboekinstructie in uw VCL om de waarde van de service-id vast te leggen:

```json
log {"syslog"} req.service_id {" my_logging_endpoint_name :: "}
```

U kunt dezelfde VCL gebruiken voor productie- en testomgevingen. Zie [`vcl_log` &#x200B;](https://www.fastly.com/documentation/reference/vcl/subroutines/log/) in de _Snelle Documentatie_.

## Problemen met de prestaties, leegmaken en cache van de site

Gebruik de volgende lijst om problemen met betrekking tot de Fastly-serviceconfiguratie voor uw Adobe Commerce in de cloud-infrastructuur te identificeren en op te lossen.

- **het menu van de Opslag toont of werkt niet** - u zou een verbinding of een tijdelijke verbinding rechtstreeks aan de oorsprongserver in plaats van het gebruiken van levende plaats URL kunnen gebruiken, of u gebruikte `-H "host:URL"` in het bevel van a [&#x200B; cURL &#x200B;](#check-live-site-through-fastly). Als u Fastly naar de oorspronkelijke server overslaat, werkt het hoofdmenu niet en worden onjuiste kopteksten weergegeven die caching op de browserzijde toestaan.

- **De hoogste navigatie werkt niet** - de hoogste navigatie baseert zich op de Zijde van Edge omvat (ESI) verwerking die wordt toegelaten wanneer u het gebrek van Magento snel VCL fragmenten uploadt. Als de navigatie niet werkt, [&#x200B; uploadt de Fastly VCL &#x200B;](fastly-configuration.md#upload-vcl-to-fastly) en controleert de plaats opnieuw.

- **Geo-location/GeoIP werkt niet** - de standaard fragmenten van Magento snel VCL voegen de landcode aan URL toe. Als de landcode niet werkt, [&#x200B; uploadt de Fastly VCL &#x200B;](fastly-configuration.md#upload-vcl-to-fastly) en controleert de plaats opnieuw.

- **de Pagina&#39;s zijn niet caching** - door gebrek, leidt de Fastly geen pagina&#39;s met de `Set-Cookies` kopbal in het voorgeheugen op. Adobe Commerce stelt cookies zelfs in op cacheable pages (TTL > 0). De standaard Magento Fastly VCL verwijdert deze cookies op cacheable pagina&#39;s. Als de pagina&#39;s niet in het voorgeheugen onderbrengen, [&#x200B; uploadt de Fastly VCL &#x200B;](fastly-configuration.md#upload-vcl-to-fastly) en controleert de plaats opnieuw.

  Deze kwestie kan ook voorkomen als een paginablok in een malplaatje uncacheable duidelijk is. In dat geval, wordt het probleem zeer waarschijnlijk veroorzaakt door een derdemodule of een uitbreiding die de kopballen van Adobe Commerce blokkeren of verwijderen. Om de kwestie op te lossen, zie [&#x200B; x-Geheime voorgeheugen slechts MISS, geen HIT &#x200B;](#x-cache-contains-only-miss-no-hit) bevat.

- **zuivert verzoeken ontbreken** - keert snel de volgende fout terug wanneer u een zuiveringsverzoek voorlegt:

  ```text
  The purge request was not processed successfully.
  ```

  Dit probleem kan worden veroorzaakt door een van de volgende problemen:

   - Ongeldige Fastly geloofsbrieven in de Fastly de dienstconfiguratie voor de Adobe Commerce op het projectmilieu van de wolkeninfrastructuur
   - Ongeldige code in een aangepast VCL-fragment

  Om de kwestie op te lossen, zie [&#x200B; Fout die het geheime voorgeheugen van de Fout op Cloud &#x200B;](https://support.magento.com/hc/en-us/articles/115001853194-Error-purging-Fastly-cache-on-Cloud-The-purge-request-was-not-processed-successfully-) in het Centrum van de Hulp van Adobe Commerce leegmaakt.

## 503 fouten van snel

Als er snel 503 time-outfouten worden geretourneerd, controleert u de foutlogboeken en de 503-foutpagina om de hoofdoorzaak te identificeren.

>[!NOTE]
>
>Als de onderbreking wanneer het runnen van bulkverrichtingen voorkomt, kunt u [&#x200B; de Snelle onderbreking voor Admin &#x200B;](fastly-custom-cache-configuration.md#extend-fastly-timeout) uitbreiden.

Als u een fout 503 ontvangt, controleer het van de de milieufout van de Productie of het Staging milieu en php toegangslogboek om de kwestie problemen op te lossen.

**om de foutenlogboeken** te controleren:

- [Foutlogboek](../test/log-locations.md#application-logs)

  ```text
  /var/log/platform/<project-ID>/error.log
  ```

  Dit logbestand bevat eventuele fouten van de toepassing of PHP-engine, bijvoorbeeld `memory_limit` - of `max_execution_time exceeded` -fouten. Als u geen Fastly verwante fouten vindt, controleer het PHP toegangslogboek.

- PHP-toegangslogboek

  ```text
  /var/log/platform/<project-ID>/php.access.log
  ```

  Zoek in het logbestand naar HTTP 200-reacties op de URL die de fout 503 heeft geretourneerd. Als u het antwoord van 200 vindt, betekent dit dat Adobe Commerce de pagina zonder fouten heeft geretourneerd. Dit geeft aan dat de kwestie mogelijk is opgetreden na het interval dat de `first_byte_timeout` -waarde overschrijdt die is ingesteld in de Fastly-serviceconfiguratie.

Wanneer er een fout van 503 optreedt, wordt de reden snel geretourneerd op de fout- en onderhoudspagina. U zou niet de reden kunnen zien als u code voor de pagina van de a [&#x200B; douanereactie &#x200B;](fastly-custom-response.md) toevoegde. Als u de redencode op de standaardfoutpagina wilt weergeven, kunt u de HTML-code voor de aangepaste foutpagina verwijderen.

**om de Fastly 503 foutenpagina** te controleren:

{{admin-login-step}}

1. Klik **Slaat** op > **Montages** > **Configuratie** > **Geavanceerd** > **Systeem**.

1. In de juiste ruit, breid **Volledig Geheime voorgeheugen van de Pagina** uit.

1. In de **Snelle sectie van de Configuratie**, breid **de Synthetische Pagina&#39;s van de Douane uit** aangezien het volgende cijfer toont.

   ![&#x200B; Douane 503 foutenpagina &#x200B;](../../assets/cdn/fastly-custom-synthetic-pages-edit-html.png)

1. Klik **Reeks HTML**.

1. Verwijder de aangepaste code. U kunt de sjabloon opslaan in een tekstprogramma en deze later weer toevoegen.

1. Klik **uploaden** om uw updates naar Fastly te verzenden.

1. Klik **sparen Config** bij de bovenkant van de pagina.

1. Open de URL die de fout 503 heeft veroorzaakt. Retourneert snel een foutpagina met de reden zoals in het volgende voorbeeld wordt getoond.

   ![&#x200B; Snelle fout &#x200B;](../../assets/cdn/fastly-503-example.png)

## Apex- en subdomeinen die al zijn gekoppeld aan een snelaccount

Als het apex-domein en de subdomeinen voor uw Adobe Commerce on cloud-infrastructuurproject al zijn gekoppeld aan een bestaand Fastly-account met een toegewezen Service-id, kunt u pas starten wanneer u de Fastly-configuratie bijwerkt:

- Werk de apex- en subdomeinconfiguratie bij op de bestaande Fastly-account. Zie [&#x200B; Veelvoudige Snelle rekeningen en toegewezen domeinen &#x200B;](fastly.md#multiple-fastly-accounts-and-assigned-domains).

- [&#x200B; laat en vormt snel &#x200B;](fastly-configuration.md#enable-fastly-caching) toe en voltooit de [&#x200B; DNS configuratie &#x200B;](../launch/checklist.md#update-dns-configuration-with-production-settings)

## Verifieer of zuivert de Snelle diensten

U kunt problemen met de prestaties of caching oplossen voor een Adobe Commerce op een cloudinfrastructuursite door site-URL&#39;s te testen en de headerwaarden te bekijken die in het antwoord worden geretourneerd.

### Live site snel controleren

Gebruik de snelheids-API om de `Fastly-Magento-VCL-Uploaded` - en `X-Cache` -antwoordheaders te controleren die door uw livesite worden geretourneerd.

Snelle API-aanvragen worden doorgegeven via de snelheidsuitbreiding om een antwoord te krijgen van uw oorspronkelijke servers. Als de reactie onjuiste kopballen terugkeert, test direct de [&#x200B; oorsprongservers &#x200B;](#bypass-fastly-cache-to-check-adobe-commerce-sites).

**om de reactiekopballen** te controleren:

1. Gebruik in een terminal de volgende `curl` opdracht om de URL van uw livesite te testen:

   ```bash
   curl https://<live URL> -vo /dev/null -H Fastly-Debug:1
   ```

   Als u geen statische route hebt geplaatst of de DNS configuratie voor de domeinen op uw levende plaats voltooid, gebruik de `--resolve` vlag, die DNS naamresolutie overslaat.

   ```bash
   curl -svo /dev/null --resolve '<your_hostname>:443:<IP-address-of-cache-node>' <https-URL>
   ```

   >[!NOTE]
   >
   >Als u deze opdracht met de optie `--resolve` wilt gebruiken, moet u TLS hebben ingeschakeld met Fastly via een SSL/TLS-certificaat en moet u het IP-adres van het cacheknooppunt zoeken.

1. In de reactie, verifieer de [&#x200B; kopballen &#x200B;](#check-cache-hit-and-miss-response-headers) om ervoor te zorgen dat de Fastly werkt. De volgende unieke kopteksten worden weergegeven in het antwoord:

   ```http
   < Fastly-Magento-VCL-Uploaded: 1.2.222
   < X-Cache: HIT, MISS
   ```

Zie de volgende informatie als de kopteksten niet de juiste waarden hebben:

- [VCL-upload controleren](#fastly-vcl-has-not-been-uploaded)

- [X-cache bevat alleen MISS, geen HIT](#x-cache-contains-only-miss-no-hit)

### Snelcache omzeilen om Adobe Commerce-sites te controleren

Als de Fastly dienst onjuiste kopballen terugkeert, kunt u een fragment tot stand brengen VCL dat u toestaat om verzoeken te verzenden die de Fastly geheime voorgeheugen overslaan. Zie [&#x200B; snel geheime voorgeheugen van de Bekeerling &#x200B;](fastly-vcl-bypass-to-origin.md).

Nadat u het VCL-fragment hebt toegevoegd, gebruikt u cURL-opdrachten om vanaf het opgegeven IP-adres aanvragen bij de oorspronkelijke server in te dienen. Controleer vervolgens de reacties op fouten.

### HIT- en MISS-responsheaders voor cache controleren

Controleer of de geretourneerde reactie de volgende informatie bevat:

- Bevat de header `X-Magento-Tags`

- De waarde van de header `Fastly-Module-Enabled` is `Yes` of het versienummer van de Fastly for CDN Magento 2-module die in de projectomgeving is geïnstalleerd

- [&#x200B; cache-Controle: max-age &#x200B;](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) is groter dan 0

- [&#x200B; Pragma &#x200B;](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.32) het plaatsen is `cache`

In het volgende fragment uit de uitvoer van de opdracht cURL worden de juiste waarden voor de headers `Pragma` , `X-Magento-Tags` en `Fastly-Module-Enabled` weergegeven:

```
* STATE: INIT => CONNECT handle 0x600057800; line 1402 (connection #-5000)
* Rebuilt URL to: https://www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud/
* Added connection 0. The cache now contains 1 members
* Trying 192.0.2.31...
* STATE: CONNECT => WAITCONNECT handle 0x600057800; line 1455 (connection #0)

% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud (54.229.163.31) port 443 (#0)

* STATE: WAITCONNECT => SENDPROTOCONNECT handle 0x600057800; line 1562 (connection #0)
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* ALPN, offering h2

... portion omitted for brevity ...

< Set-Cookie: mage-messages=%5B%5D; expires=Wed, 22-Nov-2017 17:39:58 GMT; Max-Age=31536000; path=/
< Pragma: cache
< Expires: Wed, 23 Nov 2016 17:39:56 GMT
< Cache-Control: max-age=86400, public, s-maxage=86400, stale-if-error=5, stale-while-revalidate=5
< X-Magento-Tags: cb_welcome_popup store cb cb_store_info_mobile cb_header_promotional_bar cb_store_info cb_discount-promo-bar cpg_2 cb_83 cb_81 cb_84 cb_85 cb_86 cb_87 cb_88 cb_89 p5646 catalog_product p5915 p6040 p6197 p6227 p7095 p6109 p6122 p6331 p7592 p7651 p7690
< Fastly-Module-Enabled: yes
< Strict-Transport-Security: max-age=31536000
    < Content-Security-Policy: upgrade-insecure-requests
    < X-Content-Type-Options: nosniff
    < X-XSS-Protection: 1; mode=block
    < X-Frame-Options: SAMEORIGIN
    < X-Platform-Server: i-dff64b52
    <
    * STATE: PERFORM => DONE handle 0x600057800; line 1955 (connection #0)
    * multi_done
      0     0    0     0    0     0      0      0 --:--:--  0:00:02 --:--:--     0
    * Connection #0 to host www.mymagento.biz.c.sv7gVom4qrpek.ent.magento.cloud left intact
```

>[!NOTE]
>
>Voor gedetailleerde informatie over klappen en missen, zie [&#x200B; Begrip van de kopballen van het geheime voorgeheugen HIT en van MISS met de beschermde diensten &#x200B;](https://docs.fastly.com/guides/performance-tuning/understanding-cache-hit-and-miss-headers-with-shielded-services) in de Fastly documentatie.

### Fouten in responsheaders oplossen

Deze sectie bevat suggesties voor het oplossen van fouten die worden geretourneerd wanneer responsheaders worden gecontroleerd met de snelheids-API.

#### Module Snelheid is niet ingeschakeld

Als de Fastly module niet (`Fastly-Module-Enabled: no`) wordt toegelaten of als de kopbal mist, [&#x200B; gebruik SSH aan login &#x200B;](../development/secure-connections.md#connect-to-a-remote-environment) aan het project. Voer vervolgens de volgende opdracht uit om de status van de module te controleren.

```bash
php bin/magento module:status Fastly_Cdn
```

Gebaseerd op de teruggekeerde status, gebruik de volgende instructies om de Fastly configuratie bij te werken.

- `Module does not exist` - als de module niet [&#x200B; bestaat installeer en vorm &#x200B;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/INSTALLATION.md) de FastlyCDN Module voor Magento 2 in een integratietak. Nadat de installatie is voltooid, schakelt u de module in en configureert u deze. Zie [&#x200B; Opstelling snel &#x200B;](fastly-configuration.md).

- `Module is disabled` - Als de module Snelheid is uitgeschakeld, werkt u de omgevingsconfiguratie op een `integration` -vertakking in uw lokale omgeving bij om deze in te schakelen. Druk vervolgens op de wijzigingen in Staging en Production. Zie [&#x200B; uitbreidingen &#x200B;](../store/extensions.md#install-an-extension) beheren.

  Als u [&#x200B; Beheer van de Configuratie &#x200B;](../store/store-settings.md#configure-store) gebruikt, controleer de Fastly CDN modulestatus in het `app/etc/config.php` configuratiedossier alvorens u veranderingen in de Productie of het Opvoeren milieu duwt.

  Als de module niet is ingeschakeld (`Fastly_CDN => 0`) in het `config.php` -bestand, verwijdert u het bestand en voert u de volgende opdracht uit om `config.php` bij te werken met de meest recente configuratie-instellingen.

  ```bash
  bin/magento magento-cloud:scd-dump
  ```

#### VCL is niet snel geüpload

Als Fastly VCL niet is geupload (`Fastly-Magento-VCL-Uploaded`: `false`), gebruik *uploadt VCL* optie in Admin om het te uploaden. Zie [&#x200B; snel VCL fragmenten &#x200B;](fastly-configuration.md#upload-vcl-to-fastly) uploaden.

#### X-cache bevat alleen MISS, geen HIT

Als de header `X-Cache` `HIT` (`HIT, HIT` of `HIT, MISS` ) bevat, geeft dit aan dat de inhoud in de cache snel wordt geretourneerd.

Als de `X-Cache` header `MISS, MISS` is en niet `HIT` bevat, voert u de opdracht `curl` opnieuw uit om ervoor te zorgen dat de pagina niet onlangs uit de cache is verwijderd.

Als u het zelfde resultaat krijgt, gebruik [`curl` bevelen &#x200B;](#check-live-site-through-fastly) en verifieer de [&#x200B; reactiekopballen &#x200B;](#check-cache-hit-and-miss-response-headers):

- `Pragma` is `cache`
- `X-Magento-Tags` exists
- `Cache-Control: max-age` is groter dan 0

Als het probleem zich blijft voordoen, worden deze headers waarschijnlijk opnieuw ingesteld door een andere extensie. Herhaal de volgende procedure in de het Staging milieu door alle uitbreidingen onbruikbaar te maken en elk opnieuw toe te laten om te bepalen welke uitbreiding de kopballen opnieuw instelt. Nadat u de extensie hebt geïdentificeerd die het probleem veroorzaakt, moet u deze uitschakelen in de productieomgeving.

**om een uitbreidingen te identificeren die reactiekopballen terugstelt:**

{{admin-login-step}}

1. Navigeer aan **Slaat** > **Montages** > **Configuratie** > **Geavanceerd** > **Geavanceerd**.

1. In *maak de sectie van de Output van Modules* in de juiste ruit onbruikbaar, vind elk van uw uitbreidingen en maak hen onbruikbaar.

1. Klik **sparen Config**.

1. Klik **Systeem** > **Hulpmiddelen** > **het Beheer van het Geheime voorgeheugen**.

1. Klik **het Geheime voorgeheugen van Magento van de Duw**.

1. Voer de volgende stappen uit voor elke extensie die mogelijk problemen veroorzaakt met snelkopteksten:

   - Schakel één extensie tegelijk in, sla de configuratie op en verwijder de Adobe Commerce-cache.

   - Voer de [`curl` bevelen &#x200B;](#check-live-site-through-fastly) in werking om de [&#x200B; reactiekopballen &#x200B;](#check-cache-hit-and-miss-response-headers) te verifiëren.

   Herhaal dit proces voor elke extensie. Als de headers voor snelle reactie niet meer worden weergegeven, hebt u de extensie geïdentificeerd die problemen met Snelheid veroorzaakt.

Nadat u de extensie hebt geïdentificeerd die de sneltoetsen opnieuw instelt, neemt u contact op met de ontwikkelaar van de extensie voor verdere ondersteuning. We kunnen geen correcties of updates opgeven om extensies van derden te laten werken met snel cachegeheugen.

## Snelconfiguratie terugdraaien

Als de de fragmentupdates van douaneVCL of andere Fastly configuratieveranderingen een Adobe Commerce op de plaats van de wolkeninfrastructuur veroorzaken om fouten te breken of terug te keren, gebruik snel API [&#x200B; activeer &#x200B;](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) bevel om terug naar een vroegere versie terug te rollen VCL. U kunt de VCL-versie niet terugdraaien vanuit de beheerfunctie.

**om terug versie te rollen VCL**:

1. Om een lijst van de beschikbare versies VCL voor de dienst te krijgen, stel het volgende bevel in werking

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Accept: application/json" https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version
   ```

1. Voer de volgende opdracht uit om de actieve VCL-versie te wijzigen in een opgegeven versie.

   ```bash
   curl -H "Fastly-Key: <FASTLY_API_TOKEN>" -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -X PUT https://api.fastly.com/service/<FASTLY_SERVICE_ID>/version/<VERSION_ID>/activate
   ```

Voor details over het gebruiken van Fastly API om VCL te herzien en te beheren, zie [&#x200B; VCL beheren gebruikend API &#x200B;](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
