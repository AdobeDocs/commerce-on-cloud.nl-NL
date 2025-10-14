---
title: Commerce op Cloud aanbieden
description: Leer hoe u een technische adviseur van de klant van de Adobe voorbereidt om uw Adobe Commerce op het project van de wolkeninfrastructuur te leveren.
recommendations: noDisplay, catalog
role: Admin
source-git-commit: 0d9d3d64cd0ad4792824992af354653f61e4388d
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Voorwaarden voor Commerce on Cloud-levering

We beginnen en initialiseren uw Commerce-project op cloudinfrastructuur!

Voordat u uw Commerce Adobe toewijst op omgevingen met cloudprojecten, is het raadzaam de volgende strategieën in overweging te nemen en antwoorden voor te bereiden voor uw eerste overleg met het accountteam van uw Adobe. Gebruik de volgende secties als checklist om u voor uw gesprek met een Technische Adviseur van de Klant voor te bereiden om een wolkenproject te verstrekken:

## Domeindefinitie

**Vraag 1**: _Welk domein of domeinen wilt u voor plaatshanctie gebruiken?_

Bereid u voor om de services Fastly en nginx te integreren door uw domeinen en subdomeinen op hoofdniveau te definiëren voor de omgevingen met Pro Staging en Production. Na de eerste installatie kunt u alleen domeinen toevoegen door een Adobe Commerce Support-ticket in te dienen. Het wordt daarom aangeraden dat u over de domeingegevens beschikt.

Voorbeelden voor de domeinen Productie en Staging:

- `www.your-store.com`
- `your-store.com`
- `mcprod.your-store.com`
- `mcstaging.your-store.com`

Zie [&#x200B; Opstelling veelvoudige websites of opslag &#x200B;](../cloud-guide/store/multiple-sites.md) in _Commerce op de gids van de Infrastructuur van de Wolk_ voor verdere begeleiding op veelvoudige of unieke domeinen.

Zie [&#x200B; Veelvoudige Snelle Rekeningen en toegewezen domeinen &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-on-cloud/user-guide/cdn/fastly#multiple-fastly-accounts-and-assigned-domains){target="_blank"}  als u een bestaande Fastly rekening hebt die de zelfde apex en subdomeinen verbindt die op uw plaats van Adobe Commerce worden gebruikt.

## Transactioneel e-maildomein

**Vraag 2**: _Welke domein of domeinen wilt u voor transactie e-mails gebruiken?_

Adobe Commerce on Cloud gebruikt de SendGrid Simple Mail Transfer Protocol (SMTP)-proxyservice, die services biedt voor uitgaande e-mailverificatie en controle van de reputatie. SendGrid verzendt namens u transactie-e-mails, zodat er domeininformatie voor nodig is.

Voorbeeld voor SendGrid-domein: `example@your-store.com`

Zie [&#x200B; de postdienst SendGrid &#x200B;](../cloud-guide/project/sendgrid.md) in _Commerce op de 3&rbrace; gids van de Infrastructuur van de Wolk voor verdere begeleiding over transactie e-mail en domeinmontages._

## Opslagtoewijzing

**Vraag 3**: _hoeveel van uw gecontracteerde opslag u van plan bent om voor dossier toe te wijzen uploadt en voor gegevensbestand?_

Adobe Commerce on cloud Infrastructure gebruikt opslag voor de bestandsstructuur, zoekindexering en de database. U kunt de opslagruimte naar behoefte verdelen vanaf 10 GB voor elke partitie.

De hoeveelheid opslagruimte die u hebt gecontracteerd voor uw cloudproject, vertegenwoordigt de totale opslagcapaciteit voor elke omgeving. Als u bijvoorbeeld 50 GB opslagruimte hebt gekocht, hebt u 50 GB opslagruimte voor elke omgeving. Er is 50 GB aan afzonderlijke opslag voor productie, het opvoeren, en elke integratiemilieu respectievelijk.

U kunt uw gecontracteerde opslag op elk ogenblik verhogen. Voor Pro Production- en Staging-omgevingen moet u een Adobe Commerce Support-ticket indienen om de toewijzing van schijfruimte te wijzigen. Een grootteverhoging van de milieu&#39;s van de Proproductie en van het Staging kan slechts met bepaalde intervallen voorkomen. Afhankelijk van uw huidige gebruik van schijfruimte, zou het steunteam kunnen adviseren om de toewijzing van schijfruimte met een minimum van 10 GB te verhogen. Zodra toegewezen, kan de opslagverhoging voor Pro het Opvoeren en Productie **niet** worden teruggedraaid.

Zie [&#x200B; schijfruimte beheren &#x200B;](../cloud-guide/storage/manage-disk-space.md) in _Commerce op de gids van de Infrastructuur van de Wolk_.

## Cloud-servicegebied

**Vraag 4**: _Welk de dienstgebied van de Wolk het geschiktst aan uw nabijheid is?_

Kies Amazon Web Services (AWS) of Microsoft Azure als uw IaaS-stichting (Infrastructure as a Service) voor uw Adobe Commerce op cloudinfrasinfrastructuurPro-projecten. Elke dienstverlener werkt in veelvoudige gebieden en verstrekt veelvoudige beschikbaarheidsstreken. Selecteer een gebied dat u op uw locatie handig vindt en verminder de mogelijkheden voor latentie en hogere kosten.

Zie [&#x200B; een kaart van de wolkengebieden van Adobe Commerce &#x200B;](../cloud-guide/overview.md).

## Verbindingsservice

**Vraag 5**: _hebt u de dienst PrivateLink nodig? Als zo, in welk gebied is de verbinding PrivateLink?_

Adobe Commerce on cloud Infrastructure ondersteunt integratie met de AWS Private Link of Azure Private Link-service. Hoewel deze service optioneel is, wordt PrivateLink gebruikt om een veilige, persoonlijke communicatie tot stand te brengen tussen cloudinframingevingen met services en toepassingen die op externe systemen worden gehost.

Het is belangrijk dat u rekening houdt met uw cloudservicestrategie (AWS of Azure), zodat het Adobe Commerce-exemplaar binnen dezelfde regio toegankelijk is. Zie &lbrace;de dienst PrivateLink [&#128279;](../cloud-guide/development/privatelink-service.md) in _Commerce op de gids van de Infrastructuur van de Wolk_ voor verdere verduidelijking over regionale toegankelijkheid.

## Doelsite starten

**Vraag 6**: _wat is uw geprojecteerde datum van de doellancering?_

Voor het starten van een site is iteratieve configuratie en tests vereist om te kunnen garanderen dat de site correct wordt gestart. Door een doeldatum in te stellen, kunnen u en uw accountteam van de Adobe voorbereidingen treffen voor de laatste, aan de lancering voorafgaande activiteiten, die een oproep omvatten om de laatste stappen te coördineren.

Zie het [&#x200B; overzicht van de plaats van de Lancering &#x200B;](../cloud-guide/launch/overview.md) in _Commerce op de gids van de Infrastructuur van de Wolk_ om het volledige proces te herzien en een exemplaar van checklist van de Lancering te downloaden.

>[!TIP]
>
> Bekijk de Cloud-portal en open uw nieuwe cloud-project.
>
>**Volgende stap**: [&#x200B; Onboarding aan Commerce &#x200B;](onboarding.md)
