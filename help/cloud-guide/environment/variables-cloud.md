---
title: Cloudspecifieke variabelen
description: Zie een lijst met omgevingsvariabelen die specifiek zijn voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Configuration
recommendations: noDisplay, catalog
role: Developer
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Cloudspecifieke variabelen

Omgevingsvariabelen die specifiek zijn voor Adobe Commerce op cloudinfrastructuur gebruiken het voorvoegsel `MAGENTO_CLOUD_*` :

| Variabele | Beschrijving |
| -------- | --------------- |
| `MAGENTO_CLOUD_APP_DIR` | Het absolute pad naar de toepassingsmap. |
| `MAGENTO_CLOUD_APPLICATION` | Een basis64-gecodeerd JSON-object dat de toepassing beschrijft. Het is toegewezen aan de bestandsinhoud `.magento.app.yaml` en heeft subsleutels. |
| `MAGENTO_CLOUD_APPLICATION_NAME` | De naam van de toepassing die in het `.magento.app.yaml` -bestand is geconfigureerd. |
| `MAGENTO_CLOUD_DOCUMENT_ROOT` | Het absolute pad naar de hoofdmap van het webdocument, indien van toepassing. |
| `MAGENTO_CLOUD_ENVIRONMENT` | De naam van de omgevingsvertakking. |
| `MAGENTO_CLOUD_PROJECT` | De project-id. |
| `MAGENTO_CLOUD_RELATIONSHIPS` | Een base64-gecodeerd JSON-object dat de definitie van het eindpunt van een key (relatienaam) en value (arrays of relationship pairs) vertegenwoordigt. Elke definitie van het relatieeindpunt is een ontlede vorm van een URL. Het heeft a `scheme`, a `host`, a `port`, en _optioneel_ a `username`, `password`, `path`, en sommige extra informatie in `query`. |
| `MAGENTO_CLOUD_ROUTES` | Beschrijf de routes die in het milieu `.magento/routes.yaml` dossier worden bepaald. |
| `MAGENTO_CLOUD_TREE_ID` | De boom-id voor de toepassing, die overeenkomt met de SHA van de boomstructuur in Git. |
| `MAGENTO_CLOUD_VARIABLES` | Een basis64-gecodeerd JSON-object met sleutel-waardeparen, zoals `"key":"value"` . |
| `MAGENTO_CLOUD_LOCKS_DIR` | Verstrekt de weg aan het onderstelpunt voor de slotleverancier op de infrastructuur van de Wolk. De vergrendelingsprovider voorkomt het starten van dubbele snijtaken en afdekgroepen. |

>[!WARNING]
>
>Om milieuvariabelen aan [ met voeten te treden configuratiemontages ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) gebruikend [[!DNL Cloud Console]](../project/overview.md), moet u de veranderlijke naam met `env:` zoals in het volgende voorbeeld prepend:
>
>![ veranderlijk voorbeeld van het Milieu ](../../assets/set-env-variable-ui.png)

Aangezien de waarden in de loop der tijd kunnen veranderen, is het best om de variabele bij runtime te inspecteren en het te gebruiken om uw toepassing te vormen. Gebruik bijvoorbeeld de variabele `MAGENTO_CLOUD_RELATIONSHIPS` als volgt om relaties met betrekking tot de omgeving op te halen:

```php
<?php
/**
  * Get relationships information from cloud environment variable.
  *
  * @return mixed
  */
    protected function getRelationships()
    {
        return json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"]), true);
    }
```

## Omgevingsvariabelen weergeven

U kunt het `env:config:show` bevel van [ gebruiken het `ece-tools` pakket ](../dev-tools/package-overview.md) om een lijst van variabelen voor het huidige milieu te tonen.

```bash
php ./vendor/bin/ece-tools env:config:show variables
```

Voorbeelduitvoer voor de optie `variables` :

```
Magento Cloud Environment Variables:
+-----------------------------------+----------------------------------+
| Variable name                     | Value                            |
+-----------------------------------+----------------------------------+
| ADMIN_EMAIL                       | commerceadmin@company.com        |
| ADMIN_PASSWORD                    | 123123q                          |
+-----------------------------------+----------------------------------+
```
