---
title: Aanbevolen procedures voor winkelconfiguratie
description: Lees meer over de beste praktijken voor het configureren van uw winkel op Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Best Practices
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Aanbevolen procedures voor winkelconfiguratie

Voor gedetailleerde informatie voor het vormen van uw opslag, plaatsen, en websites, kunt u de [ Gids van de Gebruiker van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html) willen herzien. Deze pagina biedt tips en trucs, handige informatie en richtlijnen voor het configureren van uw winkels, sites en meer met extra inhoud die in de loop der tijd en in verschillende versies moet worden gepost.

## Marketingcampagnes en promoties

Deze informatie is handig voor Adobe Commerce op cloudinfrastructuur 2.1.X en 2.2.X.

Om campagnes en bevorderingen tot stand te brengen, creeer de opties en de montages in [ het Opvoeren van Inhoud ](https://experienceleague.adobe.com/docs/commerce-admin/content-design/staging/content-staging.html). Met deze functie kunt u uw campagnes maken en voorvertonen voordat u ze openbaar maakt voor verkoop aan klanten. De volgende informatie biedt nuttige informatie. Voor nauwkeurige instructies raadpleegt u de gekoppelde inhoud van de Adobe Commerce-gebruikershandleiding.

_Campagnes_ zijn marketing gebeurtenissen voor seizoensverkoop, nieuwe productlijnen, en meer. Elke campagne kan aangepaste thema&#39;s, blokken voor inhoud, widgets voor het beheren en weergeven van inhoud en bijbehorende promoties met prijsregels bevatten. Vanwege de uitgebreide aard van een campagne kunt u deze maken met een begin- en einddatum via Inhoud opslaan.

_Bevorderingen_ verstrekken kortingen, één keer aanbiedingen, coupons, eerste-tijd kopersstimulansen, en meer. U creeert deze bevorderingen als _Regels van de Prijs_ die de termijnen, kortingen, en opties plaatsen om klanten aan te moedigen om te kopen. U kunt prijsregels op het [ winkelwagentje ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart.html) of [ catalogus ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/catalog-rules/price-rules-catalog.html), met extra opties voor banners, bonuspunten, en meer tot stand brengen. U kunt campagnes voor uw promoties plannen en prijsregels toepassen voor grote evenementen zoals een nieuwe productlijn of seizoensgebonden verkoop.

Hier volgen tips voor het maken, bijwerken en beheren van promoties en campagnes:

* Een promotie kan deel uitmaken van een campagne. Een campagne kan geen deel uitmaken van een promotie. U kunt lijsten met promoties als prijsregels hebben om meerdere keren, met meerdere campagnes, te gebruiken.
* Wanneer u een promotie creeert, leidt het altijd tot een aanvankelijke campagne die inactief is. Het heeft een begindatum maar geen einddatum. U kunt deze eerste campagne negeren. U kunt een Nieuwe Update met het correcte campagnemateriaal plannen en het actief maken.
* Een campagne heeft een begin- en einddatum, geen promotie. De Planner die verschijnt wanneer u een bevordering creeert vormt niet de begin en einddata voor de bevordering. Hiermee kunt u een campagne voor deze speciale actie plannen terwijl u op de configuratiepagina van de speciale actie bent.
* U kunt niet rechtstreeks bewerken in Inhoud met werkgebied. Als u de instellingen en opties in de campagne moet bewerken, bewerkt u het origineel of een replica en drukt u op om deze te overschrijven in Gelaagde inhoud. Als u bijvoorbeeld geen einddatum voor een campagne hebt, moet u het origineel bewerken en op de toets drukken om de campagne bij te werken.

## Geavanceerde prijzen en gefaseerde inhoud

Deze informatie is handig voor Adobe Commerce op cloudinfrastructuur 2.1.X en 2.2.X.

Typisch, kunt u [ Geavanceerde Prijsbepaling ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) voor producten door de **Producten** plaatsen > **het gebied van Catalogi** van Admin. Met Getrapte Inhoud, voltooi een paar extra stappen om de prijs aan een bevordering en een campagne toe te voegen.

U bewerkt als volgt de geavanceerde prijsstelling en de inhoudstaging wordt bijgewerkt:

1. Meld u aan bij de beheerder.
1. Navigeer aan **Producten** > **Catalogus** en selecteer een product en geef uit.
1. In het Prijsende lusje, uitgezochte **Geavanceerde Prijsbepaling**. Bewerk de prijs en sla de wijzigingen op.
1. Bij de bovenkant van de pagina, klik **Nieuwe Update van het Programma**.
1. Een speciale actie voor het product maken.
1. Voltooi de promotiegegevens. Voor de Planner, ga een begin en einddatum en een tijd in.
1. Sla de aanbieding op. Er wordt een inactieve eerste campagne gemaakt.
1. U kunt Voorvertonen om de speciale prijs, de naam van de speciale actie, de normale prijs en het geplande datumbereik voor de campagne te bekijken.

Voor extra stappen, kunt u met instructies met [ Veranderingen van het Programma voor de Regels van de Prijs van de Catalogus ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/catalog-rules/price-rule-catalog-scheduled-changes.html) verdergaan. Klik **daarna** om door de stappen te lopen.

## Prijsregels

Prijsregels kunnen logica en voorwaarden bevatten die zo beperkt zijn als uw marketingverbeelding. Tot de populaire voorbeelden behoren Koop één gratis ophalen, Koop één voor 50% korting, een korting voor $25 voor bestellingen van meer dan $100 en meer.

Om een Regel van de Prijs tot stand te brengen, zie {de Gids van de Gebruiker van 0} Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/catalog-rules/price-rules-catalog-create.html).[

In het volgende voorbeeld ziet u hoe u een prijsregel maakt voor een korting van Alleen eerste bestelling. Voor deze korting wilt u:

* Creeer een prijsregel met a [ klantensegment ](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/segments/customer-segment-price-rule) met een voorwaarde: Totaal Aantal Orden minder dan 1
* Dit klantensegment toevoegen als een voorwaarde aan de kartelregel
* Facultatief - voeg voorwaarden en regels toe om de kortingen op specifieke SKU&#39;s of categorieën producten voor gerichte aankopen toe te passen

Dit zorgt ervoor dat nieuwe klanten of bestaande klanten die geen aankoop hebben gedaan, de korting alleen op hun eerste bestelling ontvangen. U kunt banners maken en e-mailpromoties verzenden voor de eerste aankoopkorting.

## Winkelweergaven

U kunt meerdere winkels instellen en uitvoeren met één Adobe Commerce-implementatie op een cloudinfrastructuur. Zie [ Opstelling veelvoudige websites of opslag ](multiple-sites.md).

Voor opslag die niet met elkaar in wisselwerking staan, kunt u veelvoudige _websites_ tot stand brengen. Elke website bevat specifieke artikelen, klantgegevens, kassa en winkelwagentje die niet met andere websites in Adobe Commerce worden gedeeld.

Elke website kan één of meerdere _opslag_ met verschillende categorieën en artikelen, gedeelde klantengegevens, controle, en het winkelwagentje omvatten. Voor deze winkels kan een klant zich eenmaal aanmelden en met één kassa winkelen in verschillende productcatalogi.

Ook, kunt u _opslagmeningen_ voor verschillende talen, lay-outs, en ontwerpen tot stand brengen. Elke weergave kan een apart domein, branding en taal hebben terwijl artikelen, klantgegevens, kassa en winkelwagentje worden gedeeld.

Hieronder volgen enkele voorbeelden die u beter kunt uitleggen:

* Eén website met één winkel en twee weergaven voor de landinstelling Engels en Spaans. Alle artikelgegevens, klanten, kassa en winkelwagentje worden gedeeld.

  ![ Voorbeeld van de opslag 1 ](../../assets/example-store1.png)

* Eén website met een winkel voor vrouwenkleding bevat twee opvattingen: een voor Engels en een voor Spaans. De winkel voor kinderkleding bevat één winkelweergave in het Engels. Alle artikelgegevens, klanten, kassa en winkelwagentje worden gedeeld. De winkels kunnen verschillende domeinen en thema&#39;s hebben.

  ![ Voorbeeld van de opslag 2 ](../../assets/example-store2.png)

* Twee websites voor kleding en een andere voor thuiskleuren met verschillende catalogi en afzonderlijke artikelen, klantgegevens en winkelwagentje. Elke website kan meerdere winkels en weergaven hebben die alleen op die website artikelen, klantgegevens, kassa en winkelwagentje delen.

  ![ Voorbeeld van de opslag 3 ](../../assets/example-store3.png)

>[!WARNING]
>
>De gegevens van de catalogus worden uitgebreid aangezien u het aantal websites en opslag verhoogt. Afhankelijk van uw projectarchitectuur, kunnen de extra opslag tot een langer indexerend proces en langzamere reactietijden voor niet caching cataloguspagina&#39;s leiden. Adobe raadt u aan de prestaties van de site nauwlettend te volgen.
