---
user-guide-title: Handleiding voor Commerce in de cloud
user-guide-description: Leer hoe u de Adobe Commerce-toepassing beheert op cloudinfrastructuur.
product: magento
feature: Cloud
source-git-commit: 3347ad0a5fe202cbd80d08b7289c20a1c98ed1e3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 4%

---


# Commerce on Cloud Infrastructure {#user-guide}

+ [Commerce](overview.md)
+ Architectuur {#architecture}
   + [Cloud-infrastructuur](architecture/cloud-architecture.md)
   + [Beveiliging](architecture/security.md)
   + [Technologiestapel](architecture/tech-stack.md)
   + [Starter-architectuur](architecture/starter-architecture.md)
   + [Starter-workflow](architecture/starter-develop-deploy-workflow.md)
   + [Pro-architectuur](architecture/pro-architecture.md)
   + [Pro-workflow](architecture/pro-develop-deploy-workflow.md)
   + [Schaalbare architectuur](architecture/scaled-architecture.md)
   + [Automatisch schalen](architecture/autoscaling.md)
+ [&#x200B; begonnen worden &#x200B;](https://experienceleague.adobe.com/docs/commerce-on-cloud/start/overview.html?lang=nl-NL)
+ Opmerkingen bij de release {#release-notes}
   + [Cloud Tools-suite](release-notes/cloud-tools-suite.md)
   + [ECE-gereedschapspakket](release-notes/ece-tools-package.md)
   + [Cloudpatches](release-notes/cloud-patches.md)
   + [Cloud Docker-pakket](release-notes/cloud-docker.md)
   + [Cloud-componenten](release-notes/cloud-components.md)
   + [Cloud Packages](release-notes/cloud-packages.md)
   + [Achteruit incompatibele wijzigingen](release-notes/backward-incompatible-changes.md)
   + [Archief met opmerkingen vrijgeven](release-notes/cloud-release-archive.md)
+ Cloud-project {#project}
   + [Overzicht van project](project/overview.md)
   + [Projectstructuur](project/file-structure.md)
   + [Toegang van gebruikers](project/user-access.md)
   + [Meervoudige verificatie](project/multi-factor-authentication.md)
   + [Activiteitenstroom](project/activity-stream.md)
   + [Uitgaande e-mails](project/outgoing-emails.md)
   + [E-mailservice SendGrid](project/sendgrid.md)
   + [Branchebeheer van console](project/console-branches.md)
   + [Regionale IP-adressen](project/regional-ip-addresses.md)
+ Gereedschappen voor ontwikkelaars {#dev-tools}
   + [Overzicht](dev-tools/overview.md)
   + Cloud CLI {#cloud-cli}
      + [CLI-overzicht](dev-tools/cloud-cli-overview.md)
      + [CLI-verwijzing](dev-tools/cloud-cli-reference.md)
   + [Cloud Docker](dev-tools/cloud-docker.md)
   + ECE-gereedschappen {#ece-tools}
      + [Overzicht van pakket](dev-tools/package-overview.md)
      + [Eenmalige upgrade voor gebruik van ECE-tools](dev-tools/install-package.md)
      + [Het pakket ECE-gereedschappen bijwerken](dev-tools/update-package.md)
      + [CLI-verwijzing](dev-tools/ece-tools-cli-reference.md)
      + [Verwijzing fout](dev-tools/error-reference.md)
   + Integraties {#integrations}
      + [Overzicht](integrations/overview.md)
      + [Bitmap](integrations/bitbucket.md)
      + [GitHub](integrations/github.md)
      + [GitLab](integrations/gitlab.md)
      + [Gezondheidsmeldingen](integrations/health-notifications.md)
+ Ontwikkeling {#develop}
   + [Overzicht](development/overview.md)
   + [Verificatietoetsen](development/authentication-keys.md)
   + [CLI-branchebeheer](development/cli-branches.md)
   + [Beveiligde verbindingen](development/secure-connections.md)
   + Implementeren {#deploy}
      + [Implementatieproces](deploy/process.md)
      + [Optimalisatie](deploy/optimization.md)
      + [Aanbevolen procedures](deploy/best-practices.md)
      + [Implementatie op basis van scenario&#39;s](deploy/scenario-based.md)
      + [Implementatie zonder downtime](deploy/reduce-downtime.md)
      + [Statische implementatie van inhoud](deploy/static-content.md)
      + [Slimme wizards](deploy/smart-wizards.md)
      + [Distribueren naar Staging en Productie](deploy/staging-production.md)
      + [Herstellen van componentfout](deploy/recover-failed-deployment.md)
   + Testen {#test}
      + [Testinstructies](test/guidance.md)
      + [Logboeken](test/log-locations.md)
      + [Xdebug](test/debug.md)
      + [Voorbeeldgegevens](test/sample-data.md)
      + [Staging en productie](test/staging-and-production.md)
      + [Tweede testomgeving](test/second-staging.md)
   + [PrivateLink-service](development/privatelink-service.md)
   + [Beschermend blok](development/protective-block.md)
   + [Omgeving herstellen](development/restore-environment.md)
   + Opslag {#storage}
      + [Schijfruimte beheren](storage/manage-disk-space.md)
      + [Databasequery&#39;s profiel](storage/profile-database-queries.md)
      + [Back-up maken van de database](storage/database-dump.md)
      + [Back-upbeheer](storage/snapshots.md)
   + Upgrades en patches {#upgrade}
      + [Aanbevolen procedures](development/best-practices.md)
      + [Commerce-versie upgraden](development/commerce-version.md)
      + [Patches toepassen](development/apply-patches.md)
+ Configuratie {#configure}
   + [Overzicht](environment/overview.md)
   + Toepassing {#app}
      + [Implementatie van toepassingen configureren](application/configure-app-yaml.md)
      + [PHP-instellingen](application/php-settings.md)
      + Eigenschappen {#properties}
         + [Toepassingseigenschappen](application/properties.md)
         + [Crons](application/crons-property.md)
         + [Firewall (alleen Starter)](application/firewall-property.md)
         + [Hooks](application/hooks-property.md)
         + [Variabelen](application/variables-property.md)
         + [Web](application/web-property.md)
         + [Werknemers](application/workers-property.md)
      + [Cache instellen voor statische bestanden](application/set-cache.md)
   + Omgeving {#env}
      + [Implementatie van omgeving configureren](environment/configure-env-yaml.md)
      + [Niveaus en opties van variabele](environment/variable-levels.md)
      + Variabelen overschrijven {#stage}
         + [Omgevingsvariabelen](environment/variables-intro.md)
         + [ADMIN](environment/variables-admin.md)
         + [Cloud-variabelen](environment/variables-cloud.md)
         + [Algemeen](environment/variables-global.md)
         + [Opbouwen](environment/variables-build.md)
         + [Implementeren](environment/variables-deploy.md)
         + [Na implementatie](environment/variables-post-deploy.md)
      + Meldingen configureren {#log}
         + [Meldingen](environment/set-up-notifications.md)
         + [Logboekhandlers](environment/log-handlers.md)
   + Routes {#routes}
      + [Verbindingen vormen](routes/routes-yaml.md)
      + [Caching](routes/caching.md)
      + [Omleiding](routes/redirects.md)
      + [Include-bestanden op de server](routes/server-side-includes.md)
   + Services {#service}
      + [Services configureren](services/services-yaml.md)
      + [Elasticsearch](services/elasticsearch.md)
      + [MySQL](services/mysql.md)
      + [OpenSearch](services/opensearch.md)
      + [KonijnMQ](services/rabbitmq.md)
      + [Redis](services/redis.md)
      + [Valkey](services/valkey.md)
+ Sneldiensten {#cdn}
   + [Overzicht](cdn/fastly.md)
   + Snelle installatie {#setup-fastly}
      + [Services voor snel configureren](cdn/fastly-configuration.md)
      + [Cacheconfiguratie aanpassen](cdn/fastly-custom-cache-configuration.md)
      + [Fout- en onderhoudspagina&#39;s aanpassen](cdn/fastly-custom-response.md)
   + [Web Application Firewall](cdn/fastly-waf-service.md)
   + [Afbeelding optimaliseren](cdn/fastly-image-optimization.md)
   + Aanpassen met VCL {#custom-vcl-snippets}
      + [Aan de slag](cdn/fastly-vcl-custom-snippets.md)
      + [Aanvragen voor een CMS-backend routeren](cdn/fastly-vcl-wordpress.md)
      + [Blokverwijzingsspam](cdn/fastly-vcl-badreferer.md)
      + [IP LIJST VAN GEWENSTE PERSONEN](cdn/fastly-vcl-allowlist.md)
      + [IP LIJST VAN GEWEZEN PERSONEN](cdn/fastly-vcl-blocking.md)
      + [Snelcache omzeilen](cdn/fastly-vcl-bypass-to-origin.md)
   + [Snelle probleemoplossing](cdn/fastly-troubleshooting.md)
+ Opslaginstellingen {#configure-store}
   + [Overzicht](store/overview.md)
   + [Aanbevolen procedures](store/best-practices.md)
   + [Aangepast thema](store/custom-theme.md)
   + [Extensies](store/extensions.md)
   + [B2B-module](store/b2b-module.md)
   + [Meerdere sites](store/multiple-sites.md)
   + [Robots voor site-overzicht en zoekprogramma&#39;s](store/robots-sitemap.md)
   + [PayPal-betalingsmethoden](store/paypal.md)
   + [Configuratiebeheer](store/store-settings.md)
+ Site starten {#launch}
   + [Overzicht](launch/overview.md)
   + [Checklist starten](launch/checklist.md)
   + [Stappen starten](launch/steps.md)
+ Monitorsite {#monitor}
   + [Prestaties](monitor/performance.md)
   + [Operationele telemetrie](monitor/operational-telemetry.md)
   + New Relic-service {#new-relic}
      + [New Relic-overzicht](monitor/new-relic-service.md)
      + [Account- en gebruikersbeheer](monitor/account-management.md)
      + Prestaties onderzoeken {#investigate}
         + [Beleid, waarschuwingen en workflows](monitor/investigate-performance.md)
         + [Gegevensinvoer](monitor/ingest-data.md)
         + [Implementaties bijhouden](monitor/track-deployments.md)
      + [Logbeheer](monitor/log-management.md)
