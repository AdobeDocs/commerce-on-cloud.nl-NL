---
title: Cacheconfiguratie aanpassen
description: Leer hoe u de instellingen van de cacheconfiguratie kunt controleren en aanpassen nadat de service Fastly is ingesteld.
feature: Cloud, Configuration, Iaas, Cache
exl-id: f6901931-7b3f-40a8-9514-168c6243cc43
source-git-commit: dcf585e25a4b06ff903642e42e72a71820bad008
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 0%

---

# Cacheconfiguratie aanpassen

Nadat u opstelling en de Snelle dienst in uw het Staging en milieu&#39;s van de Productie test, herzie en pas montages van de geheim voorgeheugenconfiguratie aan. U kunt bijvoorbeeld instellingen bijwerken om ervoor te zorgen dat TLS HTTP-aanvragen snel kan doorsturen, instellingen voor leegmaken kan bijwerken en standaardverificatie kan inschakelen om uw site tijdens de ontwikkeling met een wachtwoord te beveiligen.

In de volgende secties vindt u een overzicht en instructies voor het configureren van bepaalde cacheinstellingen. Vind extra informatie over de beschikbare configuratieopties in de [ Snelle Module CDN voor Magento 2 ](https://github.com/fastly/fastly-magento2/tree/master/Documentation) documentatie.

## TLS forceren

Verstrekt snel de _Kracht TLS_ optie voor het opnieuw richten van ongecodeerde verzoeken (HTTP) aan Fastly. Nadat uw het Opvoeren of milieu van de Productie van het Staging is voorzien met a [ geldig SSL/TLS certificaat ](fastly-configuration.md#provision-ssltls-certificates), kunt u de Snelle configuratie voor uw opslag bijwerken om de optie van TLS van de Kracht toe te laten. Zie de Fastly [ gids van TLS van de Kracht ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md) in de _Fastly CDN Module voor Magento 2_ documentatie.

>[!NOTE]
>
>Het inschakelen van de optie TLS forceren is een aanbevolen werkwijze voor Adobe Commerce in de opslag van cloudinfrastructuur.

## Snelle time-out verlengen

In de Fastly-serviceconfiguratie wordt een standaardtime-outperiode van 180 seconden opgegeven voor HTTPS-aanvragen bij de beheerder. Om het even welke verzoekverwerking die de onderbrekingsperiode overschrijdt keert een fout 503 terug. Dientengevolge, kunt u 503 fouten in antwoord op verzoeken ontvangen die lange verwerking vereisen, of wanneer het proberen om bulkverrichtingen uit te voeren.

Om bulkacties te voltooien die langer dan 3 minuten duren verander de _onderbrekingen van de weg Admin_ value_ om 503 fouten te verhinderen.

>[!NOTE]
>
>Als u een eindpunt van de Weg van douaneAdmin in het **gebied van de Weg van Admin van de Douane in** Opslag **>** Configuratie **>** Geavanceerd **>** Admin **>** Admin Basis URL **hebt gespecificeerd, zult u ook de [ variabele ADMIN_URL ](../environment/variables-admin.md#change-the-admin-url) in dat milieu moeten plaatsen op dezelfde waarde.** Als de instellingen verschillen, werkt de time-out niet.
>
>Om snel onderbrekingsparameters voor buiten Admin in Snelle UI uit te breiden, zie [ Onderbreking van de Verhoging voor Lange Banen ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-INCREASE-TIMEOUTS-LONG-JOBS.md).

**om de Snelle onderbreking voor Admin** uit te breiden:

{{admin-login-step}}

1. Klik **Slaat** op > Montages > **Configuratie** > **Geavanceerd** > **Systeem** en breid **het Volledige Geheime voorgeheugen van de Pagina** uit.

1. In de _Snelle sectie van de Configuratie_, breid **Geavanceerde Configuratie** uit.

1. Plaats de **waarde van de de wegonderbreking van 0&rbrace; Admin &lbrace;in seconden.** Deze waarde mag niet langer zijn dan 10 minuten (600 seconden).

1. Klik **sparen Config** bij de bovenkant van de pagina.

1. Na de pagina herlaadt, uitgezochte **uploadt VCL aan Vast** in de _Snelle sectie van de Configuratie_.

Hiermee wordt het beheerpad voor het genereren van het VCL-bestand snel opgehaald uit het configuratiebestand van `app/etc/env.php` .

## Opties voor leegmaken configureren

Kies deze optie om snel meerdere typen verwijderingsopties op de Magento Cache Management-pagina weer te geven, waaronder opties voor het leegmaken van de productcategorie, de productelementen en de inhoud. Wanneer deze optie is ingeschakeld, zoekt Fastly naar gebeurtenissen om deze cache automatisch leeg te maken. Als u een optie voor leegmaken uitschakelt, kunt u de cache met snelheden handmatig leegmaken nadat de updates via de pagina Cachebeheer zijn voltooid.

De volgende opties voor leegmaken zijn beschikbaar:

- **zuivert categorie** - zuivert de inhoud van de productcategorie (niet productinhoud) wanneer u toevoegt en één enkel product bijwerkt. U kunt dit uitgeschakeld houden en leegmaken inschakelen, waardoor producten en productcategorieën worden gezuiverd.
- **zuiveren product** - zuivert al product en productcategorie inhoud wanneer het opslaan van één enkele wijziging aan een product. Het inschakelen van een zuiveringsproduct kan handig zijn om direct updates aan klanten te krijgen wanneer u een prijs wijzigt, een productoptie toevoegt en wanneer de productvoorraad uit voorraad is.
- **zuiveren CMS pagina** - schept paginacontent wanneer het bijwerken van en het toevoegen van pagina&#39;s aan Adobe Commerce CMS. U kunt bijvoorbeeld leegmaken bij het bijwerken van de voorwaarden of het retourbeleid. Als u deze wijzigingen zelden aanbrengt, kunt u automatisch leegmaken uitschakelen.
- **Zachte zuivering** - de Reeksen veranderden inhoud in schaal en zuivert volgens de schaaltiming. Naast de schaaltijdinstellingen worden klanten ook verouderde inhoud aangeboden, terwijl de inhoud op de achtergrond snel wordt bijgewerkt.

![ vormen zuiveringsopties ](../../assets/cdn/fastly-purge-options.png)

**om de Snelle zuiveringsopties** te vormen:

1. In de _Snelle sectie van de Configuratie_, breid **Geavanceerde Configuratie** uit om de zuiveringsopties te tonen.

1. Voor elke zuiveringsoptie, uitgezochte **ja** om automatisch het zuiveren toe te laten, of **Nr** om automatisch het zuiveren onbruikbaar te maken.

   Wanneer u een zuiveringsoptie onbruikbaar maakt, moet u het geheime voorgeheugen voor die categorie van de _pagina van het Beheer van het Geheime voorgeheugen_ manueel zuiveren.

1. Klik **sparen Config** bij de bovenkant van de pagina.

1. Na de pagina herlaadt, uitgezochte **uploadt VCL aan Vast** in de _Snelle sectie van de Configuratie_.

Voor meer informatie, zie [ de snelste configuratieopties ](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#further-configuration-options).

## GeoIP-afhandeling configureren

De module Snelheid bevat GeoIP-afhandeling om bezoekers automatisch om te leiden of om een lijst met winkels op te geven die overeenkomen met hun landcode. Als u al een extensie gebruikt voor GeoIP-afhandeling, moet u de functies mogelijk controleren met de opties Snelst.

**aan opstelling GeoIp behandeling**:

{{admin-login-step}}

1. Klik **Slaat** op > Montages > **Configuratie** > **Geavanceerd** > **Systeem** en breid **het Volledige Geheime voorgeheugen van de Pagina** uit.

1. In de _Snelle sectie van de Configuratie_, breid **Geavanceerde Configuratie** uit.

1. De rol neer en selecteert **ja** aan **laat GeoIP** toe. Er worden extra configuratieopties weergegeven.

1. Voor Actie GeoIP, selecteer als de bezoeker automatisch met **opnieuw richt** wordt omgeleid of een lijst van opslag verstrekt om van met **Dialoog** te selecteren.

1. Voor **Afbeelding van het Land**, **&#x200B;**&#x200B;toevoegen om een twee-brief landcode in te gaan om met een specifieke opslag van Adobe Commerce van een lijst in kaart te brengen.

   ![ voeg GeoIP landkaarten ](/help/assets/cdn/fastly-geo-code.png) toe

1. Klik **sparen Config** bij de bovenkant van de pagina.

1. Na pagina herlaadt, uitgezochte **uploadt VCL aan Fastly** in de _Snelle sectie van de Configuratie_.

>[!NOTE]
>
>De huidige implementatie van de Adobe Commerce Fastly GeoIP-module ondersteunt geen omleidingen tussen meerdere websites.

Verstrekt snel ook een reeks [ geolocation-related eigenschappen VCL ](https://developer.fastly.com/reference/vcl/variables/geolocation/) voor aangepaste geolocatiecodes.

## SNELLE Edge-modules inschakelen

De snel Edge Modules is een flexibel kader dat definitie van UI componenten en bijbehorende code VCL door een malplaatje toestaat. Deze modules maken het gemakkelijk om de Snelle de dienstconfiguratie door het gebruikersinterface aan te passen en uit te breiden in plaats van het gebruiken van de fragmenten van douaneVCL.

Met Edge-modules kunt u specifieke functionaliteit inschakelen, zoals CORS-headers, Cloud Sitemap herschrijft en integratie configureren tussen uw Adobe Commerce-winkel en andere CMS-systemen of backends.

Om tot het menu van Modules van Edge toegang te hebben om, de beschikbare modules te bekijken te vormen en te beheren, _aanzet snel Edge modules_ optie toe. Zie {de Modules van Edge van 0} de Snelheid [&#128279;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULES.md) in de Fastly CDN moduledocumentatie.

## Teruguiteinden en afscherming van oorsprong configureren

Back-end-instellingen zorgen voor fijnafstemming voor snelle prestaties met Oorsprong bescherming en time-outs. A _achtereind_ is een specifieke plaats (IP of domein) met gevormd schild van de Oorsprong en onderbrekingsmontages voor het controleren van en het verstrekken van caching inhoud.

_Oorsprong die_ werpt alle verzoeken om uw opslag aan een specifiek Punt van Aanwezigheid (POP). Wanneer een verzoek wordt ontvangen, controleert POP caching inhoud en verstrekt het. Als de inhoud niet in de cache wordt opgeslagen, gaat deze verder naar de POP Shield en vervolgens naar de server Origin die de inhoud in de cache plaatst. De schilden verminderen direct verkeer aan de oorsprong.

De standaard VCL-code met snelheden geeft standaardwaarden op voor Oorspronkelijke beveiliging en time-outs voor uw Adobe Commerce op cloudinframesites. In sommige gevallen moet u mogelijk de standaardwaarden wijzigen. Bijvoorbeeld, als u Tijd aan Eerste fouten van de Byte (TTFB) krijgt, zou u de _eerste waarde van de byteonderbreking_ kunnen moeten aanpassen.

>[!NOTE]
>
>Als uw plaats functioneel geleverd door een achterstandsintegratie zoals [ Wordpress ](fastly-vcl-wordpress.md) vereist, pas uw Fastly de dienstconfiguratie aan om het achtereind toe te voegen en redirects van uw opslag van Adobe Commerce aan Wordpress te beheren. Voor details, zie {de Modules van 0} Snelle Edge - Andere integratie CMS/Backend [&#128279;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) in de de moduledocumentatie van de Fastly.

**om de configuratie van achterste montages** te herzien:

{{admin-login-step}}

1. Klik **Slaat** op > Montages > **Configuratie** > **Geavanceerd** > **Systeem** en breid **het Volledige Geheime voorgeheugen van de Pagina** uit.

1. Vouw de **Snelle sectie van de Configuratie** uit.

1. Breid **montages van de Achtergrond** uit en selecteer het vistuig om het gebrek achtereind te controleren. Er wordt een modaal dialoogvenster geopend waarin de huidige instellingen worden weergegeven met opties om deze te wijzigen.

   ![ wijzig het achtereind ](../../assets/cdn/fastly-backend.png)

1. Selecteer de **plaats van het Schild** (of gegevenscentrum).

   Met de standaardsnelconfiguratie voor uw project stelt u de locatie in die het dichtst bij uw cloudservicegebied ligt. Als u deze wilt wijzigen, selecteert u een locatie dicht bij de standaardlocatie.

1. Wijzig de time-outwaarden (in microseconden) voor de verbinding met het scherm, de tijd tussen bytes en de tijd voor de eerste byte. We raden u aan de standaardtime-outinstellingen te behouden.

1. Naar keuze, uitgezocht om **te activeren achterste en Schild na het uitgeven of sparen**.

1. Klik **uploaden** om uw veranderingen te bewaren en hen te uploaden aan de Snelle servers.

1. In Admin, uitgezochte **sparen Config**.

Voor meer informatie, zie de [ gids van de Montages van de Achtergrond ](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/Guides/BACKEND-SETTINGS.md) in de de moduledocumentatie van de Snelheid.

## Basisverificatie

Standaardverificatie is een functie om elke pagina en elk element op uw site te beveiligen
met een gebruikersnaam en wachtwoord. Wij **adviseren niet** activerend basis
verificatie in uw productieomgeving. U kunt het bij het Plaatsen vormen
om uw site tijdens het ontwikkelingsproces te beschermen. Zie de [ Basis Gids van de Authentificatie ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BASIC-AUTH.md) in de Fastly CDN moduledocumentatie.

Als u gebruikerstoegang toevoegt en basisauthentificatie bij het Opvoeren toelaat, kunt u nog
toegang tot de beheerder zonder extra referenties te vereisen.

## Aangepaste VCL-fragmenten maken

Steunt snel een aangepaste versie van de Taal van de Configuratie van de Varnish (VCL) om de Snelle de dienstconfiguratie aan te passen. U kunt bijvoorbeeld toegang voor bepaalde gebruikers of IP-adressen toestaan, blokkeren of omleiden met VCL-codeblokken met de woordenboeken Rand en Toegangsbeheer (ACL).

Voor instructies om de fragmenten van douaneVCL, randwoordenboeken, en ACLs tot stand te brengen, zie &lbrace;de fragmenten van VCL van de Douane VCL [&#128279;](fastly-vcl-custom-snippets.md).

>[!NOTE]
>
>Alvorens douanecode VCL, randwoordenboeken, en ACLs aan uw Fastly moduleconfiguratie toe te voegen, verifieer dat de Fastly caching dienst met de standaardconfiguratie werkt. Zie [ Opstelling snel ](fastly-configuration.md).

## Domeinen beheren

Voor zowel Starter- als Pro-projecten kunt u de optie [!UICONTROL Domains] gebruiken om de snelste domeinconfiguratie voor uw winkel toe te voegen en te beheren.

- Voor Starter-projecten gaat u naar Project URL onder het tabblad [!UICONTROL Domains] in [!DNL Cloud Console] om de URL van het project toe te voegen.

- Voor Pro projecten, leg een [ kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor om het domein aan uw configuratie van het wolkenproject toe te voegen. Het ondersteuningsteam werkt ook de Adobe Commerce Fastly-accountconfiguratie bij om het domein toe te voegen.

**om Snelle domeinconfiguratie van Admin** te beheren:

{{admin-login-step}}

1. Selecteer **Slaat** > Montages > **Configuratie** > **Geavanceerd** > **Systeem** op en breid **het Volledige Geheime voorgeheugen van de Pagina** uit.

1. In de Admin _Snelle sectie van de Configuratie_, uitgezochte **Domeinen**.

1. Klik **leiden Domeinen** om de pagina van Domeinen te openen.

1. Voeg de namen van het hoogste niveau en subdomein toe voor de winkels in de Cloud-omgeving.

   U kunt alleen domeinen opgeven die al zijn toegevoegd aan de configuratie van de Cloud-infrastructuur.

   ![ voeg Fastly domeinconfiguratie voor Vuurwerk toe ](../../assets/cdn/fastly-starter-activate-domain.png)

1. Klik **activeren** om de Snelle domeinconfiguratie bij te werken.

>[!NOTE]
>
>Als hetzelfde domein is geconfigureerd op een andere snelaccount, moet u een Adobe Commerce-ondersteuningsticket indienen om Domeindelegatie aan te vragen voordat u het domein kunt toevoegen aan Adobe Commerce. Zie [ Veelvoudige Snelle rekeningen en toegewezen domeinen ](fastly.md#multiple-fastly-accounts-and-assigned-domains).

## Onderhoudsmodus inschakelen

Gebruik de _optie van de Wijze van het Onderhoud_ om administratieve toegang tot uw plaats van gespecificeerde IP adressen toe te staan terwijl het terugkeren van een foutenpagina voor alle andere verzoeken.

**om de wijze van het Onderhoud met Administratieve toegang** toe te laten:

1. Open de _Snelle configuratie_ sectie in Admin.

1. In de _ACL van Edge_ sectie, werk de `maint_allow` toegangsbeheerlijst (ACL) met de administratieve IP adressen bij die tot uw opslag kunnen toegang hebben terwijl het op de wijze van het Onderhoud is.

   ![ lijst van gewenste personen van de IP van het Onderhoudswijze van de Update ](../../assets/cdn/fastly-maint-allowlist.png)

1. Op de _sectie van de Wijze van het Onderhoud_, uitgezochte **laat de Wijze van het Onderhoud** toe.

   Nadat u onderhoudswijze toelaat, wordt al verkeer geblokkeerd behalve verzoeken van de IP adressen in `maint_allowlist` ACL. U kunt `maint_allowlist` bijwerken om de IP adressen in ACL te veranderen.

   Voor gedetailleerde configuratieinstructies, zie de [ gids van de Wijze van het Onderhoud ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/MAINTENANCE-MODE.md) in Fastly CDN voor Magento 2 moduledocumentatie.
