---
title: Overzicht van configuratiebestanden
description: Meer informatie over het configureren van de cloudinfratuuromgeving ter ondersteuning van de implementatie en het beheer van uw aangepaste Adobe Commerce-winkel.
feature: Cloud, Configuration, Services, Iaas, Paas
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Overzicht van configuratiebestanden

De milieu&#39;s in Adobe Commerce op wolkeninfrastructuur omvatten containers met toepassingen, de diensten, en een gegevensbestand om een volledig systeem voor uw de toepassingscodebase van Adobe Commerce en dossiers te verstrekken.

U kunt toepassingsmontages, routes vormen, acties bouwen en opstellen, en berichten om uw projectmilieu&#39;s te steunen gebruikend de volgende configuratiedossiers:

| Configuratie | Bestandsnaam | Beschrijving |
| ------------- | -------- | ----------- |
| [ Toepassing ](../application/configure-app-yaml.md) | `.magento.app.yaml` | Definieert hoe u Adobe Commerce kunt bouwen en implementeren, inclusief services, haken en uitsnijdtaken. |
| [ Milieu ](configure-env-yaml.md) | `.magento.env.yaml` | Hiermee centraliseert u het beheer van acties voor het maken en implementeren van toepassingen in al uw omgevingen, inclusief Pro Staging en Production, met behulp van omgevingsvariabelen. |
| [ Routes ](../routes/routes-yaml.md) | `.magento/routes.yaml` | Configureer caching, omleidingen en include-bestanden op de server. |
| [ de Dienst ](../services/services-yaml.md) | `.magento/services.yaml` | Definieert de services die Adobe Commerce gebruikt op naam en versie. Dit bestand kan bijvoorbeeld versies van MariaDB, PHP-extensies, Redis, RabbitMQ en Elasticsearch of OpenSearch bevatten. U moet een steunkaartje openen om deze veranderingen in de milieu&#39;s van het Staging en van de Productie van het Pro plan te duwen. |
| [ PHP montages ](../application/php-settings.md#configure-php) | `php.ini` | Een optioneel bestand dat aan het project kan worden toegevoegd. De instellingen in dit bestand worden toegevoegd aan de instellingen die door de cloudinfrastructuur worden onderhouden. |

{style="table-layout:auto"}

## Configuratie-updates voor Pro-omgevingen

Voor Adobe Commerce op cloud Infrastructure Pro Staging and Production-omgevingen kunt u veel configuratieopties bijwerken in uw lokale ontwikkelomgeving en de wijzigingen doorvoeren om deze toe te passen op deze omgevingen. Nochtans, moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voorleggen om de volgende configuratieopties bij te werken:

- Installeer of werk de diensten in het `.magento/services.yaml` dossier bij.
- Wijzig de configuratie voor de eigenschappen `mounts` en `disk` in het `.magento.app.yaml` -bestand.

{{pro-self-service-warning}}
