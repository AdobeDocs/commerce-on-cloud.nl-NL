---
title: Snelle optimalisatie van afbeeldingen
description: Leer hoe u de levering van images kunt optimaliseren en het imagebeheer voor de Adobe Commerce-site kunt vereenvoudigen door het snel optimaliseren van images in te schakelen en te configureren.
feature: Cloud, Configuration, Media
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---

# Snelle optimalisatie van afbeeldingen

Snelle optimalisatie van afbeeldingen (Fastly IO) biedt realtime beeldbewerking en optimalisatie om de levering van afbeeldingen te versnellen en het onderhoud van sets met afbeeldingsbronnen voor responsieve webtoepassingen te vereenvoudigen. Zodra gevormde Fastly IO de volgende eigenschappen van de beeldoptimalisering verstrekt:

- Omzetting met verlies forceren
- Diepe optimalisatie van afbeeldingen
- Aangepaste pixelverhoudingen
- Ondersteuning voor algemene afbeeldingsindelingen: PNG, JPEG, GIF en WebP

Alvorens u toelaat en de Fastly optie IO vormt, moet u opstelling uw Snelle dienst en vormt de Beveiliging van de Oorsprong.

Op basis van uw configuratie-instellingen voegt het fragment Fastly Image Optimization (Fastly IO) de VCL-code in om de beeldoptimalisatie uit te voeren, waardoor de levering van productafbeeldingen in de winkel sneller verloopt. Er zijn drie stappen om Fastly IO te vormen: toelaten, vormen, en verifieer.

## SNELLE IO inschakelen

Schakel Fastly Image Optimization (Fastly IO) in vanuit het deelvenster Beheer door het fragment Fastly IO VCL te uploaden. Het fragment bevat de instructies voor een snelle configuratie voor het verwerken van alle afbeeldingen met behulp van standaardconfiguraties.

**Eerste vereisten:**

- Installeren of upgraden naar Fastly-module versie 1.2.62 of hoger
- [Scherm met snelle oorsprong en backend configureren](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding)

**om snel IO** toe te laten:

1. Login aan uw lokaal [&#x200B; Admin &#x200B;](../../get-started/onboarding.md#access-your-admin-panel) paneel als beheerder.

1. Selecteer **>** Montages **>** Configuratie **>** Geavanceerd **>** Systeem **.**

1. In de juiste ruit, breid **Volledig Geheime voorgeheugen van de Pagina** uit.

1. Selecteer **Snelle Configuratie** > **Optimalisering van het Beeld** om de configuratiemontages te specificeren.

1. Op het _snelst IO fragment_ gebied, uitgezocht **toelaten/onbruikbaar maken**.

1. Upload het fragment Fastly IO:

   - Selecteer **StandaardIO configuratieopties** om de standaard configuratieoptiepagina van het Beeld te openen optimalisering.
   - Selecteer **uploaden** om het fragment VCL aan uw server te uploaden.

## SNELLE IO configureren

Controleer en werk zo nodig de standaard IO-configuratie-instellingen voor optimalisatie van afbeeldingen bij. Bijvoorbeeld, zou u WebP en de kwaliteitsniveaus van de JPEG voor lossy formaten kunnen willen veranderen, of het formaat veranderen om de beelden van JPEG te dienen aan _Progressieve_ of _Basislijn_. Bovendien kunt u de snelste IO gebruiken voor meer functies voor het optimaliseren van afbeeldingen, zoals:

- Omzetting met verlies forceren
- Diepe optimalisatie van afbeeldingen
- Aangepaste pixelverhoudingen

**om snel IO** bij te werken:

1. Op de _Snelle pagina van de Configuratie_ op het _StandaardIO configuratieopties_ gebied, uitgezocht **vorm**.

   ![&#x200B; Mening de Snelle IO configuratiemontages &#x200B;](../../assets/cdn/fastly-io-default-config.png)

1. Herzie en werk de Fastly IO configuratiemontages op de _standaard configuratieopties van het Beeld_ pagina bij:

   ![&#128279;](../../assets/cdn/fastly-io-config-options.png) van de het overzicht snel IO configuratie 

   - **AutoWebP?** - verlaat standaard het plaatsen (`Yes`) om beelden in formaat om te zetten WebP in browsers die het steunen. Als u het plaatsen in **Nr** verandert, gebruikt het snelst het type van beelddossier in plaats van het omzetten van het beeld in formaat WebP.

   - **Standaard WebP (verlies) kwaliteit** - verlaat het gebrek dat (`85`) plaatst of het compressieniveau voor verlies dossier-geformatteerde beelden typt. U kunt een geheel getal tussen 1 en 100 opgeven.

   - **Standaard JPEG formaatcontroles** - verlaat het gebrek plaatsend (`Auto`), of selecteer het type van JPEG te gebruiken wanneer het dienen van een beeld. Als de waarde aan _Auto_ wordt geplaatst, levert de Fastly beelden met het outputtype dat het inputtype aanpast. Selecteer _Basislijn_ aan vertoningsbeelden lijn door lijn die van bovenkant links en naar het bodemrecht beginnen. Selecteer _Progressief_ om een vaag beeld te tonen dat duidelijk wordt aangezien het laadt.

   - **Standaard JPEG kwaliteit** - verlaat het gebrek dat (`85`) plaatst of het compressieniveau voor kwaliteit van lossy dossierformaten typt. Geef een geheel getal op tussen 1 en 100.

   - **Upscaling toestaan?** - laat standaard het plaatsen (`No`), of selecteer `Yes` om beelden terug te keren groter dan het originele brondossier zodat kunnen zij de gevraagde afmetingen passen.

   - **Resize filter** - verlaat het gebrek plaatsend (`Lancsoz3`), of selecteer een alternatief. Met deze instelling geeft u aan welk filter wordt gebruikt voor het leveren van een afbeelding waarvan de grootte is gewijzigd. Afhankelijk van het geselecteerde filter kan het gewijzigde formaat van de afbeelding een hoger of lager aantal pixels hebben.

      - `Lanczos3` (standaard) - Levert de afbeelding van de beste kwaliteit. Het vergroot de mogelijkheid om randen en lineaire functies in een afbeelding te detecteren en het gebruik van _[!DNL sinc]_&#x200B;resampling voor de beste reconstructie.
      - `Lanczos2` - Hiermee wordt hetzelfde filter gebruikt als `Lancsoz3` , maar met een minder nauwkeurige benadering van de functie Nieuwe pixels berekenen in _[!DNL sinc]_.
      - `Bicubic` - Dit filter heeft een natuurlijk verscherpingseffect wanneer u een afbeelding kleiner maakt.
      - `Bilinear` - Dit filter heeft een natuurlijk vloeiend effect wanneer u een afbeelding groter maakt.
      - `Nearest` - Heeft een natuurlijk pixeleffect wanneer het resizing van pixelkunst.

1. Nadat u de IO configuratiemontages voor de Snelle dienst specificeert, annuleert de uitgezochte **&#x200B;**&#x200B;om aan de Fastly configuratiemontages terug te keren.

1. In de configuratie van de Optimalisering van het Beeld _laat diep beeld optimalisering_ gebied toe, selecteer **ja** om diepe beeldoptimalisering aan te zetten.

   ![&#x200B; laat Snelle IO diepe beeldoptimalisering &#x200B;](../../assets/cdn/fastly-io-deep-image-config.png) toe

   Diepe optimalisatie van afbeeldingen is standaard uitgeschakeld. Als deze functie is ingeschakeld, wordt de ingebouwde functie voor het aanpassen van de grootte in Adobe Commerce uitgeschakeld en wordt het vergroten of verkleinen van de grootte overgelaten aan de Fastly IO-service. Optimalisatie van afbeeldingen geldt alleen voor productafbeeldingen. CMS-afbeeldingen worden niet vergroot of verkleind. Zie de [&#x200B; Snelle documentatie &#x200B;](#deep-image-optimization).

1. Nadat u diepe beeldoptimalisering toelaat, laat de [&#x200B; adaptieve pixelverhouding &#x200B;](#adaptive-pixel-ratios) eigenschap toe om beelden te produceren die voor gebruik in ontvankelijke websites worden geoptimaliseerd.

   ![&#x200B; laat snel IO aanpassende pixelverhoudingen &#x200B;](../../assets/cdn/fastly-io-config-adaptive-pixel.png) toe

   - Op _laat adaptieve de pixelverhoudingen van het apparatenapparaat_ gebied toe, uitgezochte **ja**.
   - Op het _pixelverhoudingen van het Apparaat_ gebied, keur het gebrek het plaatsen goed, of selecteer het **de controlevakje van de Invoer van het Systeem** om het plaatsen te verwijderen. Selecteer vervolgens de gewenste verhouding. Een hogere instelling voor pixelverhoudingen voor apparaten levert grotere afbeeldingen op.

1. Selecteer **sparen Configuratie**.

### Omzetting met verlies forceren

Standaard dwingt de Fastly IO-service de conversie van verliesvrije indelingen zoals PNG, BMP of WEBP naar de indeling JPEG/WEBP.

Het voordeel van een gedwongen omzetting met verlies is dat kleinere afbeeldingen worden gebruikt.
Als u bijvoorbeeld de indeling JPEG of WEBp gebruikt in plaats van PNG, kan de grootte met 60 tot 70 procent worden verkleind, afhankelijk van het kwaliteitsniveau dat is opgegeven in de Fastly IO-configuratie.

Afhankelijk van het kwaliteitsniveau dat is geselecteerd voor optimalisatie van de afbeelding, kunnen er visuele verschillen in afbeeldingen optreden. Alpha kanaal/transparanties worden bijvoorbeeld verwijderd en vervangen door een witte achtergrond, tenzij u de optie Diepe afbeelding optimaliseren gebruikt en de achtergrondkleur van uw thema gebruikt.

Als u het omzetten met verlies (`WebP Auto? = No`) uitschakelt, wijzigt Fastly IO slechts JPEG beelden in formaat WEBP voor compatibele browsers. Er worden geen andere afbeeldingstypen gewijzigd. Als de oorspronkelijke afbeelding bijvoorbeeld PNG is, is de uitvoer van de service Fastly IO PNG.

### Diepe optimalisatie van afbeeldingen

Diepe optimalisatie van afbeeldingen is standaard uitgeschakeld. Als u deze optie inschakelt, wordt het formaat van de ingebouwde Adobe Commerce uitgeschakeld en wordt het volledig geoffload naar de Fastly IO-service.
Deze eigenschap resizes _slechts productafbeeldingen 0&rbrace;._ CMS-afbeeldingen worden niet vergroot of verkleind.

Als u uitgebreide optimalisatie van afbeeldingen inschakelt, voegt u een achtergrondkleurdefinitie toe aan elke afbeelding zoals die in uw thema is gedefinieerd. Het resultaat is dat WebP-afbeeldingen worden overgeschakeld van WebP-verlies naar WebP-verlies. Een van de belangrijkste verschillen tussen verliesloos en verlies is dat bij verlies het alfakanaal van PNG-afbeeldingen wordt verwijderd, wat veel kleinere afbeeldingen oplevert. Afbeeldingen met transparanties kunnen er echter vreemd uitzien op product- en campagnepagina&#39;s die een andere achtergrond gebruiken.

De volgende code vertegenwoordigt bijvoorbeeld de oorspronkelijke bron voor een afbeelding van het thema Luma:

```html
<img class="product-image-photo"
     src="https://mymagentosite/pub/media/catalog/product/cache/f073062f50e48eb0f0998593e568d857/m/b/mb02-gray-0.jpg"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

Wanneer de functie Fastly IO Deep image optimization is ingeschakeld, wordt de oorspronkelijke broncode voor de afbeelding herschreven, zoals in het volgende voorbeeld wordt getoond:

```html
<img class="product-image-photo"
     src="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

### Aangepaste pixelverhoudingen

De functie Adaptieve pixelverhoudingen is handig voor het optimaliseren van afbeeldingen voor progressieve webtoepassingen. Hiermee kunt u meerdere afbeeldingsgrootten en resoluties van één afbeeldingsbronbestand leveren door een `srcset` toe te voegen voor elke productafbeelding.

Wanneer de functie Aangepaste pixelverhoudingen is ingeschakeld, levert de Fastly IO-service een afbeelding met een vaste breedte die zich kan aanpassen aan variaties `device-pixel-ratios` .
De service wijzigt bijvoorbeeld de definitie van de productafbeelding, zoals in het volgende voorbeeld wordt getoond:

```html
<img class="product-image-photo"
     srcset="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds&dpr=2 2x,
  https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds&dpr=3 3x"
     src="https://mymagentosite/pub/media/catalog/product/m/b/mb02-gray-0.jpg?width=240&height=300&quality=80&bg-color=255,255,255&fit=bounds"
     width="240"
     height="300"
     alt="Fusion Backpack"/>
```

Zie `srcset` [&#x200B; browser steun &#x200B;](https://caniuse.com/#feat=srcset) en [&#x200B; specificatie &#x200B;](https://html.spec.whatwg.org/multipage/embedded-content.html#attr-img-srcset).

## SNEL IO valideren

Nadat u I.O. toelaat en snel vormt, bevestig uw configuratie door de tests van de Webpaginasnelheid met en zonder Fastly toe te laten IO uit te voeren. Lees ook de afbeeldingen in uw winkel om de afbeeldingsgrootte en de weergave op problemen te controleren.
