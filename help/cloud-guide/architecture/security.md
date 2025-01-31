---
title: Beveiliging van de cloudinfrastructuur
description: Leer hoe Adobe Adobe Commerce veilig houdt op de cloudinfrastructuur.
feature: Cloud, Security
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 0%

---

# Beveiliging

De het planarchitectuur van Adobe Commerce [ Pro ](pro-architecture.md) wordt ontworpen om een hoogst veilig milieu te verstrekken. Elke klant wordt opgesteld in hun eigen geïsoleerde servermilieu, gescheiden van andere klanten. De beveiligingsdetails van de productieomgeving worden hieronder beschreven.

## Webbrowsers

Het grootste deel van het verkeer dat in en uit de wolkenomgeving gaat, komt van de webbrowsers van de consument. Consumentenverkeer kan worden beveiligd met HTTPS voor alle pagina&#39;s op de website (met behulp van een gedeelde SSL-certificering of het eigen SSL-certificaat van de klant voor een extra vergoeding). Afhandelings- en accountpagina&#39;s worden altijd via HTTPS verzonden. De beste manier is om alle pagina&#39;s onder HTTPS te bedienen.

## Inhoudsleveringsnetwerk

Verstrekt snel een Netwerk van de Levering van de Inhoud (CDN) en verdeelde ontkenning van de dienstbescherming (DDoS). De snelste CDN helpt directe toegang tot de oorspronkelijke servers te isoleren. Openbare DNS richt slechts aan het Fastly Netwerk. De snelste oplossing DDoS beschermt tegen hoogst ontwrichtende Laag 3 en Laag 4 aanvallen, en complexere Laag 7 aanvallen. Laag 7 de aanvallen kan worden geblokkeerd gebruikend douaneregels die op de volledige HTTP/HTTPS- verzoeken worden gebaseerd en op cliënt en verzoekcriteria, met inbegrip van kopballen, koekjes, verzoekweg, en cliëntIP, of indicatoren zoals geolocatie worden gebaseerd.

Zie [ het Snelle overzicht van de diensten ](../cdn/fastly.md).

## Web Application Firewall

De snelste firewall van de Toepassing van het Web (WAF) wordt gebruikt om extra bescherming te verstrekken. De op cloud gebaseerde WAF van Fastly maakt gebruik van regels van derden van commerciële en open-source bronnen zoals de OWASP Core Ruleset. Bovendien zijn er specifieke Adobe Commerce-regels. De klanten worden beschermd tegen zeer belangrijke toepassing-laag aanvallen, met inbegrip van injectieaanvallen en kwaadwillige input, dwars-plaats scripting, gegevensexfiltratie, het protocolschendingen van HTTP, en andere OWASP top tien bedreigingen.

De WAF-regels worden door Adobe Commerce bijgewerkt als er nieuwe kwetsbaarheden worden gedetecteerd, zodat Managed Services beveiligingsproblemen voor softwarepatches zo goed mogelijk kan verhelpen. De Fastly WAF biedt geen snelheidsbeperkende of botdetectiediensten. Indien gewenst kunnen klanten een licentie voor een service voor botdetectie van derden verkrijgen die compatibel is met Fastly.

Zie {de Firewall van de Toepassing van 0} Web (WAF) ](../cdn/fastly-waf-service.md).[

## Virtuele privécloud

De productieomgeving van het Adobe Commerce Pro-plan is zo geconfigureerd als een Virtual Private Cloud (VPC) dat productieservers geïsoleerd zijn en slechts beperkte mogelijkheden hebben om verbinding te maken met en uit de cloudomgeving. Alleen veilige verbindingen met de cloudservers zijn toegestaan. Beveiligde protocollen zoals SFTP of rsync kunnen worden gebruikt voor bestandsoverdracht.

De klanten kunnen de tunnels van SSH gebruiken om mededelingen met de toepassing te beveiligen. Voor toegang tot AWS Private Link kan een extra bedrag worden betaald. Alle verbindingen met deze servers worden gecontroleerd met behulp van AWS-beveiligingsgroepen, een virtuele firewall die verbindingen met de omgeving beperkt. De technische middelen van klanten kunnen tot deze servers toegang hebben gebruikend SSH.

## Versleuteling

Amazon Elastic Block Store (EBS) wordt gebruikt voor opslag. Alle EBS-volumes worden gecodeerd met het algoritme AES-256, wat betekent dat de gegevens in rust worden gecodeerd. Het systeem codeert ook gegevens in doorvoer tussen CDN en de oorsprong, en tussen de oorspronkelijke servers. De wachtwoorden van de klant worden opgeslagen als knoeiboel. Gevoelige geloofsbrieven, met inbegrip van de geloofsbrieven van de betaalgateway, worden gecodeerd gebruikend het algoritme SHA-256.

De Adobe Commerce-toepassing biedt geen ondersteuning voor codering of codering op kolom- of rijniveau wanneer de gegevens niet in rust zijn of niet worden verzonden tussen servers. De klant kan coderingssleutels beheren vanuit de toepassing. Toetsen die door het systeem worden gebruikt, worden opgeslagen in het AWS Key Management System en moeten door Managed Services worden beheerd om onderdelen van de service te kunnen leveren.

## Detectie van eindpunten en respons

[!DNL CrowdStrike Falcon], wordt een lichte, volgende-generatie agent van het Eindpunt van de Opsporing en van de Reactie (EDR) geïnstalleerd op alle eindpunten (met inbegrip van servers) binnen Adobe. EDR-agenten beschermen de gegevens en systemen van de Adobe met permanente controle en verzameling in real time, die snelle identificatie en reactie van de dreiging mogelijk maken.

## Penetentietests

Managed Services voert regelmatig penetratietests uit van het Adobe Commerce-wolkensysteem met behulp van de out-of-the-box-toepassing. Klanten zijn verantwoordelijk voor eventuele penetratietests van hun aangepaste toepassing.

## Betalingsgateway

Adobe Commerce vereist integratie van betaalgateway, waarbij creditcardgegevens rechtstreeks van de browser van de consument naar de betaalgateway worden doorgegeven. De kaartgegevens zijn nooit beschikbaar in een van de Adobe Commerce Pro Plan Managed Services-omgevingen. De acties op de transacties door de toepassing van de Handel worden voltooid gebruikend een verwijzing naar de transactie van de gateway.

## Adobe Commerce-toepassing

De Adobe test regelmatig de kerntoepassingscode op veiligheidskwetsbaarheid. Patches voor defecten en beveiligingsproblemen worden aan klanten geleverd. Het Product Security Team valideert Adobe Commerce-producten volgens de beveiligingsrichtlijnen van de OWASP-toepassing. Verschillende hulpprogramma&#39;s voor beveiligingskwetsbaarheidsbeoordeling en externe leveranciers worden gebruikt om de naleving te testen en te controleren. Beveiligingsgereedschappen zijn onder meer:

- Statisch en dynamisch scannen van veracode
- Scannen naar RIPS-broncode
- Trustwave en Alert Logic&#39;s kwetsbaarheidsscanservices
- Burp Suite Pro
- OWASPZAP
- andSqlMap

De volledige codebasis wordt gescand met deze hulpmiddelen op een tweewekelijkse basis. De klanten worden op de hoogte gebracht van veiligheidspatches door directe e-mail, berichten in de toepassing, en in het [ Centrum van de Veiligheid ](https://helpx.adobe.com/security.html).

Klanten moeten ervoor zorgen dat deze patches binnen 30 dagen na de release op hun aangepaste toepassing worden toegepast, volgens de PCI-richtlijnen. De Adobe verstrekt ook het Hulpmiddel van het Scannen van de a [ Veiligheid ](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan) dat verkopers toelaat om hun plaatsen regelmatig te controleren en updates over bekende veiligheidsrisico&#39;s, malware, en onbevoegde toegang te ontvangen. Het hulpprogramma Beveiligingsscan is gratis en kan worden uitgevoerd op elke versie van Adobe Commerce.

Om veiligheidsonderzoekers aan te moedigen om kwetsbaarheid te identificeren en te melden, heeft Adobe Commerce a [ insect-hinderlijk programma ](https://hackerone.com/magento) naast interne het testen. Bovendien wordt de klant de volledige broncode van de toepassing verstrekt voor hun eigen overzicht indien gewenst.

## Alleen-lezen bestandssysteem

Alle uitvoerbare code wordt opgesteld in een read-only beeld van het dossiersysteem, dat dramatisch de oppervlakken vermindert die voor aanval beschikbaar zijn. Het implementatieproces maakt een Squash-FS-afbeelding om de mogelijkheden voor het injecteren van PHP- of JavaScript-code in het systeem te verkleinen of om Adobe Commerce-toepassingsbestanden te wijzigen.

## Externe implementatie

De enige manier om uitvoerbare code in de de productieomgeving van Managed Services te krijgen is het door een leveringsproces in werking te stellen. Voor provisioning moet de broncode van uw bronopslagplaats worden doorgestuurd naar een externe opslagplaats die een implementatieproces start. De toegang tot dat plaatsingsdoel wordt gecontroleerd, zodat hebt u volledige controle over wie tot het plaatsingsdoel kan toegang hebben. Alle plaatsingen van toepassingscode aan het niet productiemilieu worden gecontroleerd door de klant.

## Logboekregistratie

Alle AWS-activiteiten zijn aangemeld bij AWS CloudTrail. Besturingssysteem-, toepassingsserver- en databaselogboeken worden opgeslagen op de productieservers en opgeslagen in back-ups. Alle wijzigingen in de broncode worden vastgelegd in een Git-opslagplaats. De geschiedenis van de plaatsing is beschikbaar in de Interface van het Web van het Project van Adobe Commerce [ ](../project/overview.md). Alle ondersteuningstoegang wordt geregistreerd en de steunzittingen worden geregistreerd.

Zie [ Mening en beheer logboeken ](../test/log-locations.md).

## Gevoelige gegevens

Gevoelige gegevens kunnen betrekking hebben op persoonlijke informatie van consumenten of vertrouwelijke gegevens van Managed Services-klanten. De bescherming van gevoelige gegevens van klanten en consumenten is een essentiële verplichting voor Adobe Commerce Managed Services. Zowel Managed Services- als Adobe-klanten hebben wettelijke verplichtingen met betrekking tot persoonlijk identificeerbare informatie. Naast de veiligheidseigenschappen van de architectuur, zijn er andere controles om de distributie en de toegang tot gevoelige gegevens te beperken.

De klanten hebben hun gegevens en hebben controle over waar dat gegeven wordt gevestigd. De klant geeft de locatie op waar de productie- en ontwikkelingsinstanties zich bevinden. Zij geven ook aan welke locatie wordt gebruikt voor de Adobe Commerce Reporting-omgeving met Commerce en of die Adobe Commerce Reporting-toepassing toegang heeft tot persoonlijk identificeerbare informatie of niet. Productie-instanties kunnen zich in de meeste AWS-regio&#39;s bevinden, terwijl ontwikkelings- en Adobe Commerce-rapportageomgevingen zich momenteel in de Verenigde Staten of in de Europese Unie bevinden.

Gevoelige gegevens kunnen door het Fastly CDN servernetwerk overgaan maar worden niet opgeslagen in het Fastly netwerk. Alle partners die deel uitmaken van het Managed Services-aanbod hebben contractuele verplichtingen om de bescherming van gevoelige gegevens te waarborgen. Managed Services verplaatst geen gevoelige klant- of consumentengegevens van de door de klant opgegeven locaties.

Als onderdeel van het aanbieden van de diensten die deel uitmaken van het Managed Services-aanbod, hebben Managed Services-medewerkers toegang nodig tot productiesystemen die gevoelige gegevens bevatten. Deze werknemers worden opgeleid over hun verplichtingen om gevoelige klant en consumentengegevens te beschermen. De toegang tot deze systemen is beperkt tot werknemers die toegang vereisen. Deze werknemers hebben slechts toegang voor de tijd nodig om deze diensten te leveren.

## Algemene verordening inzake gegevensbescherming

Algemene verordening inzake gegevensbescherming (GDPR) is een juridisch kader dat richtsnoeren vaststelt voor het verzamelen en verwerken van persoonsgegevens voor personen in de Europese Unie (EU). Deze regels gelden ongeacht de vestigingsplaats van de site en EU-bezoekers hebben er toegang toe.

Bezoekers moeten in kennis worden gesteld van de gegevens die een site van hen verzamelt en moeten uitdrukkelijk instemmen met het verzamelen van informatie. De sites moeten bezoekers op de hoogte stellen als de persoonsgegevens van de site worden geschonden.

De handelaar of het bedrijf dat de locatie exploiteert, moet een speciale functionaris voor gegevensbescherming hebben die toezicht houdt op de gegevensbeveiliging van de site. De Data Privacy Officer (of het websitebeheerteam) moet beschikbaar zijn voor contact als een bezoeker om wissen van zijn gegevens verzoekt.

GDPR dringt erop aan dat alle persoonlijk identificeerbare informatie (zoals namen, ras en geboortedatum) die wordt verzameld, geanonimiseerd of pseudoniem wordt gemaakt.

>[!NOTE]
>
>Deze pagina biedt een algemeen overzicht van wat u in overweging kunt nemen voor GDPR. Zie de _[Gids van de Veiligheid en van de Naleving ](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/overview)_ voor details over hoe Adobe Commerce persoonlijke informatie opslaat. Om te bepalen hoe uw zaken om het even welke wettelijke verplichtingen zouden moeten naleven, raadpleeg uw wettelijke raadsman of verwijs naar de [ officiële tekst ](https://eur-lex.europa.eu/eli/reg/2016/679/oj).

## Back-ups

De steun wordt uitgevoerd elk uur voor de laatste 24 uren van verrichting. Na de periode van 24 uur worden back-ups volgens een schema bewaard met behulp van de AWS EBS Snapshot-service. Zie [ Beleid van het Behoud ](pro-architecture.md#retention-policy).

De service maakt een onafhankelijke back-up van redundante opslag. Omdat de EBS-volumes gecodeerd zijn, worden de back-ups ook gecodeerd. Bovendien voert Managed Services op verzoek back-ups uit.

Bij uw Managed Services-aanpak voor back-up en herstel wordt gebruikgemaakt van een architectuur met hoge beschikbaarheid in combinatie met back-ups op het volledige systeem. Elk project wordt herhaald—alle gegevens, code, en activa-over drie afzonderlijke de beschikbaarheidsstreken van AWS; elke streek met een afzonderlijk gegevenscentrum.

Zie [ Momentopnamen en reservebeheer ](../storage/snapshots.md).
