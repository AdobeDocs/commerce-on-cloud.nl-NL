---
title: Variables, eigenschap
description: Gebruik het variabelenbezit om de opties van de opslagconfiguratie voor de  [!DNL Commerce]  toepassing aan te passen.
feature: Cloud, Configuration
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Variables, eigenschap

U kunt op toepassing-gebaseerde omgevingsvariabelen gebruiken om opslagconfiguraties aan te passen. Deze variabelen gebruiken een specifieke syntaxis. Zie [&#x200B; configuratiemontages van de Overschrijving &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html?lang=nl-NL) in de _gids van de Configuratie_.

De volgende omgevingsvariabelen in het `.magento.app.yaml` -bestand zijn vereist voor specifieke versies van de [!DNL Commerce] -toepassing.

Vereist voor Adobe Commerce 2.2.x tot 2.3.x:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```

Stel voor Adobe Commerce 2.4.x de volgende variabelen in:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```
