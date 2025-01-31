---
title: Include-bestanden op de server
description: Leer hoe u include-bestanden op de server kunt gebruiken met Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Routes
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Include-bestanden op de server

[ server-kant omvat ](https://nginx.org/en/docs/http/ngx_http_ssi_module.html) (SSI) zijn richtlijnen in HTML pagina&#39;s die op de server worden geëvalueerd terwijl de pagina&#39;s teruggeven. Met SSI kunt u dynamisch gegenereerde inhoud toevoegen aan een bestaande HTML-pagina zonder de hele pagina te bedienen.

U kunt SSI per route in uw `.magento/routes.yaml` activeren of deactiveren; bijvoorbeeld:

```yaml
    "http://{default}/":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: false
            ssi:
                enabled: true
    "http://{default}/time.php":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: true
```

SSI laat u toe om in uw HTML reactierichtlijnen te omvatten die de server veroorzaken om delen van de HTML te vullen, die om het even welke bestaande [ in het voorgeheugen onderbrengende configuratie ](caching.md) respecteren.

In het volgende voorbeeld ziet u hoe u een dynamisch datumbesturingselement boven aan een pagina invoegt en een ander datumbesturingselement onder aan dat elke 600 seconden wordt bijgewerkt:

Voeg het volgende toe aan elke pagina, zoals `/index.php` :

```php?start_inline=1
echo date(DATE_RFC2822);
<!--#include virtual="time.php" -->
```

Voeg het volgende toe aan `time.php`:

```php?start_inline=1
header("Cache-Control: max-age=600");
echo date(DATE_RFC2822);
```

Blader naar de pagina waarop u het besturingselement hebt toegevoegd. Vernieuw de pagina een aantal keren. U ziet dat de tijd boven aan de pagina verandert, maar de tijd onder aan de pagina verandert slechts om de 600 seconden.
