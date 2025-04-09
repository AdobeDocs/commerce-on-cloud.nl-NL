---
title: Overzicht van ontwikkeling
description: Voorbereiden op lokale ontwikkeling met een Adobe Commerce-project voor cloudinfrastructuur.
role: Developer
feature: Cloud, Install
topic: Development
last-substantial-update: 2024-02-06T00:00:00Z
exl-id: 14fb0b41-1c3a-4abc-8726-cea16ab00ba8
source-git-commit: 1cea1cdebf3aba2a1b43f305a61ca6b55e3b9d08
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# Overzicht van ontwikkeling

Externe omgevingen van Adobe Commerce in de cloudinfrastructuur zijn **alleen-lezen**, inclusief alle Starter-omgevingen en alle Pro-integratie-, faserings- en productieomgevingen. In een lokale ontwikkelomgeving kunt u code schrijven en testen voordat u deze naar een integratieomgeving pusht voor verder testen en implementeren in testomgeving en productie.

Voordat u uw lokale werkruimte voorbereidt, moet u ervoor zorgen dat u over uw [inloggegevens beschikt.](../../get-started/prepare-workspace.md) Lokale ontwikkeling vereist de installatie van PHP en Composer, tenzij u ervoor kiest om Cloud Docker for Commerce](#docker-environment) te gebruiken[.

## Benodigde pakketten

Adobe Commerce op cloudinfrastructuur maakt gebruik van Composer om de afhankelijkheden en upgrades voor projecten te beheren. Voor lokale ontwikkeling moet u de PHP- en Composer-versies installeren die compatibel zijn met uw Cloud-project. Als u bijvoorbeeld de [!DNL Commerce] 2.4.8-cloudsjabloon gebruikt, kunt u zien dat het [`.magento.app.yaml`](https://github.com/magento/magento-cloud/blob/2.4.8/.magento.app.yaml) configuratiebestand PHP 8.4 **en** Composer 2.8.4 **gebruikt**.

Composer installeert de vereiste bibliotheken en afhankelijkheden voor uw project in de map `vendor` . De volgende vereiste Composer-bestanden bevinden zich in de hoofdmap van het project:

- `composer.json` - Gebruik het `composer.json` -bestand om productinstallaties en upgrades te beheren.
- `composer.lock` - Het `composer.lock` dossier slaat een reeks nauwkeurige versiegebiedsdelen op die aan de versiebeperkingen van elke vereiste voor elk pakket in de gebiedsdeelboom van het project voldoen.

**Gemeenschappelijke bevelen:**

| Bevelen | Beschrijving |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `composer update` | Updates van de nieuwste versies van de afhankelijkheden die in het `composer.json` bestand worden weergegeven. Hiermee wordt het `composer.lock` bestand bijgewerkt. |
| `composer install` | Leest het `composer.lock` bestand om afhankelijkheden te downloaden. Het is een best practice om een up-to-date kopie van `composer.lock` te bewaren in uw projectrepository. |

{style="table-layout:auto"}

Zodra u de bijgewerkte code hebt toegevoegd, vastgelegd en gepusht, wordt de `composer install` opdracht tijdens de buildfase automatisch uitgevoerd tijdens het [implementatieproces](../deploy/process.md#build-phase-build-phase).

### Cloud metapakket

Adobe Commerce on cloud Infrastructure maakt gebruik van een metapakket waarvoor `magento/product-enterprise-edition` vereist is. Gebruik de volgende beperkingssyntaxis om de nieuwste updates voor de nieuwste versie van Commerce te verkrijgen:

```text
>=current_version <next_version
```

Als u bijvoorbeeld de nieuwste Adobe Commerce-versie 2.4.9 wilt gebruiken, stelt u `2.4.8` in als de &quot;huidige&quot; versie en `2.4.9` als de &quot;volgende&quot; versie in het `composer.json` -bestand:

```text
"magento/magento-cloud-metapackage": ">=2.4.8 <2.4.9"
```

De belangrijkste pakketten van deze metapakket zijn:

- **verkoper/magento/ece-tools** - het `ece-tools` pakket is compatibel met versie 2.1.4 van Adobe Commerce en later om een rijke reeks eigenschappen te verstrekken u kunt gebruiken om uw Adobe Commerce op het project van de wolkeninfrastructuur te beheren. Het bevat scripts en Adobe Commerce on Cloud Infrastructure-opdrachten die zijn ontworpen om u te helpen bij het beheren van uw code en het automatisch bouwen en implementeren van uw projecten. Zie het [`ece-tools` pakketoverzicht](../dev-tools/package-overview.md).
- **vendor/magento/product-enterprise-edition**: voor dit metapakket zijn applicatieonderdelen vereist, waaronder modules, frameworks, thema&#39;s en meer.
- **vendor/fastly2/magento2**—Deze module beheert het Fastly CDN en de services voor de omgevingen Pro Staging en Production en Starter Production. Zie [Fastly-services](/help/cloud-guide/cdn/fastly.md#fastly-cdn-module-for-magento-2).
- **vendor/magento/module-PayPal-on-boarding—Deze module biedt PayPal-betalingsgateway-afrekenen door verbinding te maken met uw PayPal-verkopersaccount**. Zie [PayPal On-Boarding tool](../store/paypal.md).

>[!TIP]
>
>Zie [ de pakketten van de Wolk voor Adobe Commerce ](/help/cloud-guide/release-notes/cloud-packages.md) in de _nota&#39;s van de Versie van Commerce_ voor een lijst van gebiedsdelen en derdevergunningen.

## Dockingomgeving

Met het hulpprogramma Cloud Docker for Commerce kunt u de Adobe Commerce emuleren voor de productie- en ontwikkelomgevingen van cloudinfrastructuur voor lokale ontwikkeling. Voor Cloud Docker voor Commerce hoeven PHP en Composer niet lokaal te worden geïnstalleerd.

- [ Lokale ontwikkeling met het Dok van de Wolk ](https://developer.adobe.com/commerce/cloud-tools/docker/setup/) in de plaats van Adobe Developer
- [Docker-architectuur en algemene opdrachten](../dev-tools/cloud-docker.md)
- [Opmerkingen bij de release van Cloud Docker](../release-notes/cloud-docker.md)

>[!TIP]
>
>Zie [Integraties](../integrations/overview.md) voor meer informatie over het gebruik van Git-hostingservices met Adobe Commerce op cloudinfrastructuur.
