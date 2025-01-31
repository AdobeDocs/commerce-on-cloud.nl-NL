---
title: Projectstructuur
description: Meer informatie over de bestandsstructuur en projectsjablonen voor Adobe Commerce op cloudinfrastructuur.
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Projectstructuur

Een Adobe Commerce on cloud-infrastructuurproject bevat essentiële bestanden voor referenties en toepassingsconfiguratie. Deze bestanden zijn beschikbaar in de vorm van een sjabloon volgens de Adobe Commerce-versie. Zie de wolkenmalplaatjes die op versie van Adobe Commerce in de [`magento/magento-cloud` bewaarplaats GitHub ](https://github.com/magento/magento-cloud) worden gebaseerd.

In de volgende tabel worden de bestanden beschreven die zijn opgenomen in een wolkenproject:

| Bestand | Beschrijving |
| ------------------------- | ------------ |
| `/.magento/routes.yaml` | Het dossier van de configuratie dat `www` aan het apex domein en `php` toepassing opnieuw richt om HTTP te dienen. Zie [ routes ](../routes/routes-yaml.md) vormen. |
| `/.magento/services.yaml` | Een configuratiedossier dat een instantie MySQL (MariaDB), Redis, en OpenSearch of Elasticsearch bepaalt. Zie [ de diensten ](../services/services-yaml.md) vormen. |
| `/app` | De map `code` wordt gebruikt voor aangepaste modules. De `design` omslag wordt gebruikt voor [ douanethema&#39;s ](../store/custom-theme.md). De map `etc` bevat configuratiebestanden voor de toepassing. |
| `/m2-hotfixes` | Wordt gebruikt voor aangepaste patches. |
| `/update` | Een de dienstomslag die door de steunmodule wordt gebruikt. |
| `.gitignore` | Geef op welke bestanden en mappen u wilt negeren. Zie [`.gitignore` reference ](#ignoring-files) . |
| `.magento.app.yaml` | Een configuratiebestand dat de eigenschappen definieert om de toepassing samen te stellen. Zie [ toepassing ](../application/configure-app-yaml.md) vormen. |
| `.magento.env.yaml` | Het dossier van de configuratie voor de bouw, opstellen, en post-opstellen fasen. Het pakket `ece-tools` bevat een voorbeeld van dit bestand. Zie [ milieu&#39;s ](../environment/configure-env-yaml.md) vormen. |
| `composer.json` | Zoekt Adobe Commerce en de configuratiescripts om uw toepassing voor te bereiden. Zie [ Vereiste pakketten ](../development/overview.md#required-packages). |
| `composer.lock` | Slaat versiegebiedsdelen voor elk pakket op. Zie [ Vereiste pakketten ](../development/overview.md#required-packages). |
| `magento-vars.php` | Gebruikt om [ veelvoudige opslag ](../store/multiple-sites.md) en plaatsen te bepalen die variabelen gebruiken. |

{style="table-layout:auto"}

>[!NOTE]
>
>Wanneer u uw lokale wijzigingen in de externe server doorvoert, gebruikt het implementatiescript de waarden die zijn gedefinieerd door configuratiebestanden in de map `.magento` . Vervolgens verwijdert het script de map en de inhoud ervan. Dit heeft geen invloed op uw lokale ontwikkelomgeving.

## Hoofdmap van toepassing

De locatie van de hoofdmap van de toepassing is afhankelijk van de omgeving.

- **Begin en ProIntegratie**: `/app`
- **Productie van de Aanzet**: `/<project-ID>`
- **Pro het Staging**: `/<project-ID>_stg`
- **Proproductie**: `/<project-ID>`

### Schrijfbare mappen

De externe integratie-, staging- en productieomgevingen zijn alleen-lezen. De volgende folders zijn *slechts* beschrijfbare folders voor veiligheidsredenen:

- `var`
- `pub/static`
- `pub/media`
- `app/etc`
- `/tmp`

>[!NOTE]
>
>In Productie- en staging-omgevingen heeft elk knooppunt in de cluster met drie knooppunten een `/tmp` -map die niet met de andere knooppunten wordt gedeeld.

## Bestanden negeren

Er is een base `.gitignore` -bestand met de Adobe Commerce op de projectopslagplaats van de cloud-infrastructuur. Zie het recentste dossier [.gitignore in magento-wolkenbewaarplaats ](https://github.com/magento/magento-cloud/blob/master/.gitignore). Als u een bestand wilt toevoegen dat in de lijst van `.gitignore` staat, kunt u de optie `-f` (geforceerd) gebruiken bij het stapelen van een commit:

```bash
git add <path/filename> -f
```

## Basissjabloon wijzigen

U kunt de volgende stappen gebruiken om de structuur van een bestaand project te veranderen om het recentste basissjabloon voor Adobe Commerce op wolkeninfrastructuur te weerspiegelen.

1. Kloont het project aan een lokaal werkstation.

1. Werk het `composer.json` -bestand bij met de volgende waarden voor de `extra` -sectie.

   ```json
   "extra": {
       "magento-force": true
       "magento-deploystrategy": "copy"
   }
   ```

1. Voeg het `.gitignore` -bestand toe dat is ontworpen voor de basissjabloon. Bijvoorbeeld, als u het `.gitignore` dossier voor versie 2.2.6 malplaatje nodig hebt, gebruik [ .gitignore voor 2.2.6 ](https://github.com/magento/magento-cloud/blob/2.2.6/.gitignore) dossier als verwijzing.

1. Wis de git-cache.

   ```bash
   git rm -r --cached .
   ```

1. Wijzigingen toevoegen en doorvoeren.

   ```bash
   git add -A && git commit -m "Update base template"
   ```

{{redeploy-warning}}
