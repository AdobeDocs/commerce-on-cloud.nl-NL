---
title: Meerdere websites of winkels instellen
description: Leer hoe u meerdere websites of winkels voor Adobe Commerce configureert op cloudinfrastructuur.
feature: Cloud, Configuration, Routes, Site Navigation
exl-id: 773d8d64-d235-4c2b-87e9-aadbf8471b2c
source-git-commit: 0d84d29c470a098c7238b6ca7cc9538463dda695
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Meerdere websites of winkels instellen

U kunt Adobe Commerce zo configureren dat er meerdere websites of winkels zijn, zoals een Engelse winkel, een Franse winkel en een Duitse winkel. Zie [&#x200B; Begrijpend websites, opslag, en opslagmeningen &#x200B;](best-practices.md#store-views).

>[!WARNING]
>
>De gegevens van de catalogus worden uitgebreid aangezien u het aantal websites en opslag verhoogt. Afhankelijk van uw projectarchitectuur, kunnen de extra opslag tot een langer indexerend proces en langzamere reactietijden voor niet caching cataloguspagina&#39;s leiden. Adobe raadt u aan de prestaties van de site nauwlettend te volgen.

Het proces voor het instellen van meerdere winkels hangt af van het feit of u ervoor kiest unieke of gedeelde domeinen te gebruiken.

Meerdere opslagruimten met unieke domeinen:

```
https://first.store.com/
https://second.store.com/
```

Meerdere opslagruimten met hetzelfde domein:

```
https://store.com/first/
https://store.com/second/
```

>[!TIP]
>
>Als u een opslagweergave wilt toevoegen aan de basis-URL van de site, hoeft u geen meerdere mappen te maken. Zie [&#x200B; de opslagcode aan basisURL &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html?lang=nl-NL) in de _Gids van de Configuratie_ toevoegen.

## Domeinen toevoegen

Aangepaste domeinen kunnen worden toegevoegd aan Pro Staging en elke productieomgeving. Ze kunnen niet worden toegevoegd aan integratieomgevingen.

Het proces om een domein toe te voegen hangt af van het type Cloud-account:

- Voor Pro Staging en Productie

  Voeg het nieuwe domein aan Fastly toe, zie [&#x200B; domeinen &#x200B;](../cdn/fastly-custom-cache-configuration.md#manage-domains) beheren, of open een steunkaartje om hulp te verzoeken. Bovendien moet u [&#x200B; een kaartje van de Steun van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voorleggen om nieuwe domeinen te verzoeken om aan een cluster worden toegevoegd.

- Alleen voor startproductie

  Voeg het nieuwe domein aan Fastly toe, zie [&#x200B; domeinen &#x200B;](../cdn/fastly-custom-cache-configuration.md#manage-domains) beheren, of [&#x200B; leg een kaartje van de Steun van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voor om hulp te verzoeken. Bovendien moet u het nieuwe domein aan het **lusje van Domeinen** in [!DNL Cloud Console] toevoegen: `https://<zone>.magento.cloud/projects/<project-ID>/edit`

## Lokale installatie configureren

Om uw lokale installatie te vormen om veelvoudige opslag te gebruiken, zie [ Veelvoudige websites of opslag ][config-multiweb] in de _Gids van de Configuratie_.

Nadat u de lokale installatie hebt gemaakt en getest om meerdere winkels te kunnen gebruiken, moet u de integratieomgeving voorbereiden:

1. **vorm routes of plaatsen** - specificeer hoe inkomende URLs door Adobe Commerce wordt behandeld

   - [Routes voor afzonderlijke domeinen](#configure-routes-for-separate-domains)
   - [Locaties voor gedeelde domeinen](#configure-locations-for-shared-domains)

1. **Opstelling websites, opslag, en opslagmeningen** - vorm gebruikend Adobe Commerce Admin UI
1. **wijzigt variabelen** - specificeer de waarden van `MAGE_RUN_TYPE` en `MAGE_RUN_CODE` variabelen in het `magento-vars.php` dossier
1. **stelt en test milieu&#39;s** op - stel en test de `integration` tak op

>[!TIP]
>
>U kunt een lokale omgeving gebruiken om meerdere websites of winkels in te stellen. Zie de instructies van het Dok van de Wolk aan [&#x200B; Opstelling veelvoudige websites of opslag &#x200B;](https://developer.adobe.com/commerce/cloud-tools/docker/configure/multiple-sites).

### Configuratie-updates voor Pro-omgevingen

{{pro-self-service-warning}}

### Vorm routes voor afzonderlijke domeinen

Routes bepalen hoe binnenkomende URLs wordt verwerkt. Voor meerdere opslagruimten met unieke domeinen moet u elk domein in het `routes.yaml` -bestand definiëren. De manier u routes vormt hangt van af hoe u uw plaats wilt werken.

**om routes in een integratiemilieu** te vormen:

1. Open het bestand `.magento/routes.yaml` in een teksteditor op uw lokale werkstation.

1. Definieer het domein en de subdomeinen. De waarde `mymagento` upstream is dezelfde waarde als de eigenschap name in het `.magento.app.yaml` -bestand.

   ```yaml
   "http://{default}/":
       type: upstream
       upstream: "mymagento:http"
   
   "http://<second-site>.{default}/":
       type: upstream
       upstream: "mymagento:http"
   ```

1. Sla de wijzigingen op in het `routes.yaml` -bestand.

1. Ga aan [&#x200B; Vastgestelde websites, opslag, en opslagmeningen &#x200B;](#set-up-websites-stores-and-store-views) voort.

### Locaties voor gedeelde domeinen configureren

Waar de routeneconfiguratie bepaalt hoe URLs wordt verwerkt, bepaalt het `web` bezit in het `.magento.app.yaml` dossier hoe uw toepassing aan het Web wordt blootgesteld. Het Web _plaatsen_ staat meer granulariteit voor inkomende verzoeken toe. Als uw domein bijvoorbeeld `store.com` is, kunt u `/first` (standaardsite) en `/second` gebruiken voor aanvragen bij twee verschillende winkels die een domein delen.

**om een nieuwe Webplaats** te vormen:

1. Creeer een alias voor de wortel (`/`). In dit voorbeeld is de alias `&app` op regel 3.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
   ```

1. Maak een pass-through voor de website (`/website`) en verwijs naar de hoofdmap met de alias van de vorige stap.

   Met de alias krijgt `website` toegang tot waarden vanaf de hoofdlocatie. In dit voorbeeld bevindt de website `passthru` zich op regel 21.

   ```yaml
   web:
       locations:
           "/": &app
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static":
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>": *app
             ...
   ```

**om een plaats met een verschillende folder** te vormen:

1. Creeer een alias voor de wortel (`/`) en voor de statische (`/static`) plaatsen.

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/static": &static
               root: "pub/static"
   ```

1. Maak een submap voor de website onder de map `pub` : `pub/<website>`

1. Kopieer het `pub/index.php` -bestand naar de `pub/<website>` -map en werk het `bootstrap` -pad (`/../../app/bootstrap.php`) bij.

   ```
   try {
       require __DIR__ . '/../../app/bootstrap.php';
   } catch (\Exception $e) { 
   ```

1. Maak een doorvoerbewerking voor het `index.php` -bestand.

   ```yaml
   web:
       locations:
           "/": &root
               # The public directory of the app, relative to its root.
               root: "pub"
               passthru: "/index.php"
               index:
               - index.php
               ...
           "/media":
               root: "pub/media"
               ...
           "/static": &static
               root: "pub/static"
               allow: true
               scripts: false
               passthru: "/front-static.php"
               rules:
                   ^/static/version\d+/(?<resource>.*)$:
                       passthru: "/static/$resource"
           "/<website>":
               <<: *root
               passthru: "<website>/index.php"
           "/<website>/static": *static
             ...
   ```

1. Leg de gewijzigde bestanden vast en duw erop.

   - `pub/<website>/index.php` (Als dit bestand zich in `.gitignore` bevindt, heeft de drukknop mogelijk de optie force nodig.)
   - `.magento.app.yaml`

### Websites, winkels en winkels instellen

In _Admin UI_, opstelling uw Websites van Adobe Commerce **&#x200B;**, **Sporen**, en **Mening van de Opslag**. Zie [&#x200B; Opstelling veelvoudige websites, opslag, en opslagmeningen in Admin &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-admin.html?lang=nl-NL) in de _Gids van de Configuratie_.

Het is belangrijk om dezelfde naam en code van uw websites te gebruiken, en meningen van uw Admin op te slaan wanneer u opstelling uw lokale installatie. U hebt deze waarden nodig wanneer u het `magento-vars.php` -bestand bijwerkt.

### Variabelen wijzigen

In plaats van een virtuele NGINX-host te configureren, geeft u de variabelen `MAGE_RUN_CODE` en `MAGE_RUN_TYPE` door met behulp van het bestand `magento-vars.php` in de hoofdmap van het project.

**om variabelen over te gaan die het `magento-vars.php` dossier** gebruiken:

1. Open het `magento-vars.php` -bestand in een teksteditor.

   Het [&#x200B; standaard `magento-vars.php` dossier &#x200B;](https://github.com/magento/magento-cloud/blob/master/magento-vars.php) zou als het volgende moeten kijken:

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   //if (isHttpHost("example.com")) {
   //    $_SERVER["MAGE_RUN_CODE"] = "default";
   //    $_SERVER["MAGE_RUN_TYPE"] = "store";
   //}
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] === $host;
   }
   ```

1. Verplaats het gecommenteerde `if` blok zodat het _na_ het `function` blok is en niet meer gecommentarieerd.

   ```php
   <?php
   // enable, adjust and copy this code for each store you run
   // Store #0, default one
   
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
           return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("example.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "default";
       $_SERVER["MAGE_RUN_TYPE"] = "store";
   }
   ```

1. Vervang de volgende waarden in het blok `if (isHttpHost("example.com"))` :
   - `example.com` - met de basis URL van uw _website_
   - `default` - met unieke CODE voor uw _website_ of _opslagmening_
   - `store`—met een van de volgende waarden:
      - `website` - laad de _website_ in de storefront
      - `store` - laad a _opslagmening_ in de storefront

   Voor meerdere sites die unieke domeinen gebruiken:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("second.store.com")) {
       $_SERVER["MAGE_RUN_CODE"] = "<second-site>";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }elseif (isHttpHost("store.com")){
       $_SERVER["MAGE_RUN_CODE"] = "base";
       $_SERVER["MAGE_RUN_TYPE"] = "website";
   }
   ```

   Voor veelvoudige plaatsen met het zelfde domein, moet u de _gastheer_ en _URI_ controleren:

   ```php
   <?php
   function isHttpHost($host)
   {
       if (!isset($_SERVER['HTTP_HOST'])) {
       return false;
       }
       return $_SERVER['HTTP_HOST'] ===  $host;
   }
   
   if (isHttpHost("store.com")) {
      $code = "base";
      $type = "website";
   
      $uri = explode('/', $_SERVER['REQUEST_URI']);
      if (isset($uri[1]) && $uri[1] == 'second') {
        $code = '<second-site>';
        $type = 'website';
      }
      $_SERVER["MAGE_RUN_CODE"] = $code;
      $_SERVER["MAGE_RUN_TYPE"] = $type;
   }
   ```

1. Sla de wijzigingen op in het `magento-vars.php` -bestand.

### Implementeren en testen op de integratieserver

Breng uw wijzigingen aan in uw Adobe Commerce op de integratieomgeving van de cloudinfrastructuur en test uw site.

1. Wijzigingen in de externe vertakking toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add -A && git commit -m "Implement multiple sites" && git push origin <branch-name>
   ```

1. Wacht tot de implementatie is voltooid.

1. Na de implementatie opent u de URL van je winkel in een webbrowser.

   Gebruik voor een uniek domein de volgende indeling: `http://<magento-run-code>.<site-URL>`

   Bijvoorbeeld: `http://french.master-name-projectID.us.magentosite.cloud/`

   Gebruik voor een gedeeld domein de volgende indeling: `http://<site-URL>/<magento-run-code>`

   Bijvoorbeeld: `http://master-name-projectID.us.magentosite.cloud/french/`

1. Test uw site grondig en voeg de code samen naar de `integration` -vertakking voor verdere implementatie.

## Distribueren naar Staging en Productie

Volg het plaatsingsproces voor [&#x200B; het opstellen aan het Opvoeren en de Productie &#x200B;](../deploy/staging-production.md). Voor Starter- en Pro-omgevingen gebruikt u [!DNL Cloud Console] om code in verschillende omgevingen te plaatsen.

Adobe raadt aan volledig te testen in de testomgeving voordat naar de productieomgeving wordt overgeschakeld. Breng codeveranderingen in het integratiemilieu aan en begin het proces om over milieu&#39;s opnieuw op te stellen.

<!-- link definitions -->

[config-multiweb]: https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/multi-sites/ms-overview.html?lang=nl-NL
