---
source-git-commit: 0d9d3d64cd0ad4792824992af354653f61e4388d
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---
# Cloud-fragmenten

## Waarschuwing Elasticsearch {#elasticsearch-support}

>[!WARNING]
>
>Elasticsearch 7.11 en hoger wordt niet ondersteund voor Adobe Commerce op cloudinfrastructuur. Adobe Commerce-versies 2.3.7-p3, 2.4.3-p2 en 2.4.4 en hoger ondersteunen de OpenSearch-service. De installaties ter plaatse blijven Elasticsearch steunen.

## Verbeterde integratie {#enhanced-integration-envs}

>[!NOTE]
>
>De projecten die vóór 5 juni 2020 werden verstrekt hadden veelvoudige, kleinere milieu&#39;s van de Integratie. Als u een grotere milieu van de Integratie voor het testen en de ontwikkeling nodig hebt, verzoek om een verbetering aan Verbeterde milieu&#39;s van de Integratie. Zie het [ verzoek van het Milieu van de Integratie ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/announcements/commerce-announcements/integration-environment-enhancement-request-pro-and-starter.html) artikel in het _Centrum van de Hulp van Adobe Commerce_ voor details.

## Samenvoegopties {#merge-options}

Standaard overschrijft het implementatieproces alle instellingen in het `env.php` -bestand. U kunt er echter voor kiezen een of meer waarden voor een serviceconfiguratie samen te voegen zonder alle waarden te overschrijven.

Stel de optie `_merge` in op een van de volgende opties:

- `true` - **voeg** de gevormde de de dienstwaarden met de milieu veranderlijke waarden samen.
- `false` - **overschrijft** de gevormde de de dienstwaarden met de milieu veranderlijke waarden.

## Persoonlijke opslagplaats {#private-repository}

>[!NOTE]
>
>Adobe raadt u ten zeerste aan een privéopslagplaats voor uw Adobe Commerce te gebruiken voor een cloudinfrastructuurproject om eigendomsgebonden informatie of ontwikkelingswerk, zoals extensies en kwetsbare configuraties, te beschermen.

## Pro-waarschuwing voor zelfbediening {#pro-self-service-warning}

>[!WARNING]
>
>Sommige **Pro projecten** vereisen een steunkaartje om de routeconfiguratie in het `routes.yaml` dossier en de kroonconfiguratie in het `.magento.app.yaml` dossier bij te werken. De Adobe adviseert het bijwerken van en het testen van de configuratiedossiers van YAML in een milieu van de Integratie, dan het opstellen van veranderingen in het het Opvoeren milieu. Als uw veranderingen niet op het Opvoeren plaatsen na u worden toegepast en er geen verwante foutenmeldingen in het logboek zijn, dan MOET u **[ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voorleggen dat de geprobeerd configuratieveranderingen beschrijft.** Neem de bijgewerkte YAML-configuratiebestanden op in het ticket.

## Pro-services-ondersteuning {#pro-update-service}

>[!TIP]
>
>Voor Pro projecten, moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voorleggen om [ diensten ](https://experienceleague.adobe.com/docs/commerce-on-cloud/user-guide/configure/service/services-yaml.html) in `Staging` en `Production` slechts milieu&#39;s te installeren of bij te werken.
>
>Geef aan welke servicewijzigingen nodig zijn, neem de bijgewerkte `.magento.app.yaml` - en `services.yaml` -bestanden op en geef de PHP-versie op in het ticket. Voor zelfbedienings veranderingen in PHP versie, uitbreidingen, of milieu montages, zie [ PHP montages ](https://experienceleague.adobe.com/docs/commerce-on-cloud/user-guide/configure/app/php-settings.html) in _configuratie van de Toepassing_.
>
>Voor veranderingen in een levende milieu van de Productie (**slechts Pro**), wordt een minimum van 48 uurverklaring vereist. Hierdoor kan het infrastructuurteam van de cloud voldoende tijd krijgen om bronnen te bundelen en een veilige upgrade uit te voeren. De opzegtermijn begint wanneer het infrastructuurteam de aanvraag erkent en de upgrade plant, met uitzondering van weekends. Bijvoorbeeld, om de dienstverbeteringen te hebben op een maandag worden voltooid, moet een erkenning van de geplande verbetering tegen Woensdag worden ontvangen. Tijdens piekvraagperiodes, zou het meer tijd kunnen vergen om uw verzoek te verwerken.

## Pro-back-ups {#pro-backups}

>[!TIP]
>
>Op Pro het Opvoeren en de milieu&#39;s van de Productie, moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voorleggen om een specifieke steun terug te winnen noterend de datum, de tijd, en de tijdzone in het kaartje.
>
>De Adobe herstelt **&#x200B;**&#x200B;geen milieu&#39;s van een automatische steun. Zie [ herstellen een momentopname van DB van het Opvoeren of Productie ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production.html) voor hulp die een methode kiezen om een het Opname van het Opvoeren of van de Productie te herstellen.

## Waarschuwing bij opnieuw implementeren {#redeploy-warning}

>[!WARNING]
>
>Het implementatieproces begint wanneer u een samenvoeging, push of synchronisatie van uw omgeving uitvoert of wanneer u een handmatige herimplementatie activeert, waarbij de toepassing van [!DNL Commerce] zich in de onderhoudsmodus bevindt. Voor een productieomgeving raadt de Adobe aan deze werkzaamheden tijdens de werkuren buiten de piekuren af te ronden om onderbreking van de service te voorkomen.

## Plaatsaanduiding voor route {#route-placeholder}

>[!NOTE]
>
>De volgende voorbeelden van de routeconfiguratie gebruiken routesjablonen met placeholders. De tijdelijke aanduiding `{default}` vertegenwoordigt het standaarddomein dat voor uw site is geconfigureerd. Als uw project veelvoudige domeinen heeft, gebruik placeholder `{all}` om het verpletteren voor het standaarddomein en alle aliassen te vormen. Zie [ routes ](/help/cloud-guide/routes/routes-yaml.md) vormen.

## SCD-timing {#scd-timing-warning}

>[!WARNING]
>
>Als er problemen optreden met statische inhoudsbestanden in uw toepassing na de implementatie, zoals ontbrekende aangepaste themabestanden, verhoogt u de maximale verwachte uitvoeringstijd tot 900 seconden of langer.

## Implementatie op basis van scenario's {#scenarios}

>[!NOTE]
>
>Met [!DNL ECE-Tools] 2002.1.0 en hoger kunt u de op scenario&#39;s gebaseerde implementatiefunctie gebruiken om de build-, implementatie- en postimplementatieprocessen voor uw Adobe Commerce aan te passen in het infrastructuurproject in de cloud. Zie [ op scenario-Gebaseerde plaatsing ](/help/cloud-guide/deploy/scenario-based.md).

## Tweede fasering {#second-staging}

>[!NOTE]
>
>Sommige projecten vereisen een meer geavanceerd ontwikkelingswerkschema. Om deze behoefte te steunen, biedt de Adobe een [ extra het opvoeren milieu ](/help/cloud-guide/test/second-staging.md) als toe:voegen-op optie aan uw wolkeninfrastructuur aan.

## Serviceinstructie {#service-instruction}

Gebruik de volgende instructies voor de dienstopstelling op de milieu&#39;s van de Integratie Pro en van de Starter milieu&#39;s, met inbegrip van de `master` tak.

>[!NOTE]
>
>[ leg een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor om de de dienstconfiguratie op ProProductie en het Opvoeren milieu&#39;s te veranderen.

## Servicewijziging {#service-change-tip}

>[!TIP]
>
>Nadat u de service hebt ingesteld, kunt u de softwareversie van een geïnstalleerde service wijzigen door de configuratiebestanden van `services.yaml` en `.magento.app.yaml` bij te werken. Zie [ de dienstversie van de Verandering ](/help/cloud-guide/services/services-yaml.md#change-service-version) voor begeleiding bij de bevordering of het degraderen van de dienst.

## Tip voor implementatie stoppen {#stuck-deployment-tip}

>[!TIP]
>
>Voor hulp met gestadige plaatsingen, gebruik [ de plaatsingslos van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/deployment/magento-deployment-troubleshooter.html) in het _Centrum van de Hulp van Commerce_.

## Bijwerken naar ECE-gereedschappen {#ece-tools-package}

>[!NOTE]
>
>Als u een versie van Adobe Commerce op wolkeninfrastructuur gebruikt die niet het `ece-tools` pakket bevat, dan moet u a [ éénmalige verbetering ](/help/cloud-guide/dev-tools/install-package.md) aan uw wolkenproject uitvoeren om verouderde pakketten te verwijderen. Als u momenteel het `ece-tools` pakket gebruikt en u het moet bijwerken, zie [ Update het ECE-Hulppakket ](/help/cloud-guide/dev-tools/update-package.md).

## Upgradetip {#upgrade-tip}

>[!TIP]
>
>Voordat u met een upgrade of een patchproces begint, maakt u een actieve vertakking vanuit de integratieomgeving en checkt u de nieuwe vertakking uit naar uw lokale werkstation. Als u een vertakking aan de upgrade of het patchproces toewijst, voorkomt u dat uw werk wordt gehinderd.

<!-- Fastly-related snippets begin -->

## Aanmelden bij beheerder {#admin-login-step}

1. [ Login ](/help/get-started/onboarding.md#access-your-admin-panel) aan Admin.

## Aangepaste implementatie van VCL-fragmenten automatiseren {#automate-vcl-snippet-deployment}

>[!NOTE]
>
>In plaats van handmatig aangepaste VCL-fragmenten te uploaden, kunt u fragmenten toevoegen aan de map `$MAGENTO_CLOUD_APP_DIR/var/vcl_snippets_custom` in uw omgeving. De fragmenten in deze folder uploaden automatisch wanneer u _klikt uploadt VCL aan Fastly_ in Commerce Admin. Zie [ Geautomatiseerde plaatsing van de fragmenten VCL van douaneVCL ](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md#automated-custom-vcl-snippets-deployment) in de Fastly CDN module voor Magento 2 documentatie.

<!-- Fastly-related snippets end -->
