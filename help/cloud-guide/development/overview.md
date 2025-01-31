---
title: Overzicht van ontwikkeling
description: Voorbereiden op lokale ontwikkeling met een Adobe Commerce-project voor cloudinfrastructuur.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Overzicht van ontwikkeling

Adobe Commerce op de verre milieu&#39;s van de wolkeninfrastructuur is **slechts-lezen**, met inbegrip van alle milieu&#39;s van de Aanzet en alle Pro integratie, het Opvoeren, en milieu&#39;s van de Productie. In een lokale ontwikkelomgeving kunt u code schrijven en testen voordat u deze naar een integratieomgeving duwt voor verdere tests en implementatie naar Staging en Productie.

Alvorens uw lokale werkruimte voor te bereiden, zorg ervoor dat u uw [ geloofsbrieven ](../../get-started/prepare-workspace.md) hebt. De lokale ontwikkeling vereist PHP en de installatie van Composer tenzij u verkiest om [ Docker van de Wolk voor Commerce ](#docker-environment) te gebruiken.

## Vereiste pakketten

Adobe Commerce on cloud Infrastructure gebruikt Composer om de afhankelijkheden en upgrades voor projecten te beheren. Voor lokale ontwikkeling moet u de PHP en Composer versies installeren die compatibel zijn met uw Cloud project. Bijvoorbeeld, als u het [!DNL Commerce] 2.4.7 wolkenmalplaatje gebruikt, kunt u zien dat het [`.magento.app.yaml` ](https://github.com/magento/magento-cloud/blob/2.4.7/.magento.app.yaml) configuratiedossier **PHP 8.3** en **Composer 2.7.2** gebruikt.

Composer installeert de vereiste bibliotheken en afhankelijkheden voor uw project in de map `vendor` . De volgende vereiste Composer-bestanden bevinden zich in de hoofdmap van het project:

- `composer.json` - Gebruik het `composer.json` -bestand om productinstallaties en upgrades te beheren.
- `composer.lock` - Het `composer.lock` dossier slaat een reeks nauwkeurige versiegebiedsdelen op die aan de versiebeperkingen van elke vereiste voor elk pakket in de gebiedsdeelboom van het project voldoen.

**Gemeenschappelijke bevelen:**

| Opdracht | Beschrijving |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Updates voor de meest recente versies van de afhankelijkheden die in het `composer.json` -bestand worden weergegeven. Hiermee werkt u het `composer.lock` -bestand bij. |
| `composer install` | Leest het `composer.lock` -bestand om afhankelijkheden te downloaden. Het wordt aanbevolen om een actuele kopie van `composer.lock` bij te houden in uw projectopslagplaats. |

{style="table-layout:auto"}

Zodra u toevoegt, begaat, en duw de bijgewerkte code, stelt het plaatsingsproces automatisch het `composer install` bevel tijdens [ bouwt fase ](../deploy/process.md#build-phase-build-phase) in werking.

### Cloud-pakket

Adobe Commerce on cloud Infrastructure maakt gebruik van een metapakket waarvoor `magento/product-enterprise-edition` vereist is. Gebruik de volgende beperkingssyntaxis om de nieuwste updates voor de nieuwste versie van Commerce te verkrijgen:

```text
>=current_version <next_version
```

Als u bijvoorbeeld de nieuwste Adobe Commerce-versie 2.4.7 wilt gebruiken, stelt u `2.4.7` in als de &quot;huidige&quot; versie en `2.4.8` als de &quot;volgende&quot; versie in het `composer.json` -bestand:

```text
"magento/magento-cloud-metapackage": ">=2.4.7 <2.4.8"
```

De belangrijkste pakketten van deze metapakket zijn:

- **verkoper/magento/ece-tools** - het `ece-tools` pakket is compatibel met versie 2.1.4 van Adobe Commerce en later om een rijke reeks eigenschappen te verstrekken u kunt gebruiken om uw Adobe Commerce op het project van de wolkeninfrastructuur te beheren. Het bevat scripts en Adobe Commerce op instructies voor de cloud-infrastructuur die zijn ontworpen om u te helpen uw code te beheren en automatisch uw projecten te maken en te implementeren. Zie het [`ece-tools` pakketoverzicht ](../dev-tools/package-overview.md).
- **verkoper/magento/product-onderneming-uitgave** - Dit metapakket vereist toepassingscomponenten, met inbegrip van modules, kaders, thema&#39;s, en meer.
- **verkoper/faals2/magento2** - Deze module beheert snel CDN en de diensten voor de Pro het Staging en Productie en de milieu&#39;s van de Productie van de Starter. Zie [ de Snelle diensten ](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **verkoper/magento/module-parypal-op-inboarding** - Deze module verstrekt PayPal betalingspogcontrole door met uw handels PayPal rekening te verbinden. Zie [ PayPal on-Boarding hulpmiddel ](../store/paypal.md).

>[!TIP]
>
>Zie [ de pakketten van de Wolk voor Adobe Commerce ](/help/cloud-guide/release-notes/cloud-packages.md) in de _nota&#39;s van de Versie van Commerce_ voor een lijst van gebiedsdelen en derdevergunningen.

## Dockingomgeving

Met het hulpprogramma Cloud Docker for Commerce kunt u de Adobe Commerce emuleren voor de productie- en ontwikkelomgevingen van cloudinfrastructuur voor lokale ontwikkeling. Voor Cloud Docker voor Commerce hoeven PHP en Composer niet lokaal te worden geïnstalleerd.

- [ Lokale ontwikkeling met het Dok van de Wolk ](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) in de plaats van Adobe Developer
- [Docker-architectuur en algemene opdrachten](../dev-tools/cloud-docker.md)
- [Opmerkingen bij de release Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Voor informatie over het gebruiken van op git-Gebaseerde ontvangende diensten met Adobe Commerce op wolkeninfrastructuur, zie [ Integraties ](../integrations/overview.md).
