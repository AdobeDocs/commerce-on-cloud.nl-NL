---
title: Implementatie op basis van scenario's
description: Leer hoe u Adobe Commerce kunt aanpassen bij de implementatie van cloudinfrastructuren met behulp van aangepaste configuratiebestanden.
feature: Cloud, Configuration, Deploy, Build
source-git-commit: 0d9d3d64cd0ad4792824992af354653f61e4388d
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# Implementatie op basis van scenario&#39;s

Met `ece-tools` 2002.1.0 en hoger kunt u de op scenario&#39;s gebaseerde implementatiefunctie gebruiken om het standaardimplementatiegedrag aan te passen.
Deze eigenschap gebruikt **scenario&#39;s** en **stappen** in de configuratie:

- {de configuratie van het 0} Scenario **-Elke plaatsingshaak is a *scenario*, dat een de configuratiedossier is van XML dat de opeenvolging en configuratieparameters beschrijft om plaatsingstaken te voltooien.** U configureert de scenario&#39;s in de sectie `hooks` van het `.magento.app.yaml` -bestand.

- **- elk scenario van de 1&rbrace; Stap gebruikt een opeenvolging van *stappen* die programmatically de verrichtingen beschrijven die worden vereist om plaatsingstaken te voltooien.** U vormt de stappen in een op XML-Gebaseerd dossier van de scenarioconfiguratie.

Adobe Commerce op wolkeninfrastructuur verstrekt een reeks [&#x200B; standaardscenario&#39;s &#x200B;](https://github.com/magento/ece-tools/tree/2002.1/scenario) en [&#x200B; standaardstappen &#x200B;](https://github.com/magento/ece-tools/tree/2002.1/src/Step) in het `ece-tools` pakket. U kunt plaatsingsgedrag aanpassen door de configuratiedossiers van douaneXML te creëren om de standaardconfiguratie met voeten te treden of aan te passen. U kunt ook scenario&#39;s en stappen gebruiken om code uit aangepaste modules uit te voeren.

## Voeg scenario&#39;s toe gebruikend bouw en opstellings haken

U voegt de scenario&#39;s voor het bouwen en het opstellen van Adobe Commerce aan de `hooks` sectie van het `.magento.app.yaml` dossier toe. Elke haak specificeert de scenario&#39;s om tijdens elke fase te lopen. Het volgende voorbeeld toont de standaardscenario configuratie.

> `magento.app.yaml` haken

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

>[!NOTE]
>
>Met de versie van `ece-tools` 2002.1.x, is er een nieuw [&#x200B; hooks configuratie &#x200B;](https://experienceleague.adobe.com/docs/commerce-on-cloud/user-guide/configure/app/properties/hooks-property.html?lang=nl-NL) formaat. De oudere indeling uit `ece-tools` 2002.0.x-releases wordt nog steeds ondersteund. Nochtans, moet u aan het nieuwe formaat bijwerken om de op scenario-gebaseerde plaatsingseigenschap te gebruiken.

## Evaluatiescenario-stappen

In de hakconfiguratie, is elk scenario een dossier van XML dat stappen bevat om bouwt, op te stellen, of post-stelt taken in werking te stellen. Het bestand `scenario/transfer` bevat bijvoorbeeld drie stappen: `compress-static-content` , `clear-init-directory` en `backup-data`

> `scenario/transfer.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <step name="compress-static-content" type="Magento\MagentoCloud\Step\Build\CompressStaticContent" priority="100"/>
    <step name="clear-init-directory" type="Magento\MagentoCloud\Step\Build\ClearInitDirectory" priority="200"/>
    <step name="backup-data" type="Magento\MagentoCloud\Step\Build\BackupData" priority="300">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="steps" xsi:type="array">
                <item name="static-content" xsi:type="object" priority="100">Magento\MagentoCloud\Step\Build\BackupData\StaticContent</item>
                <item name="writable-dirs" xsi:type="object"  priority="200">Magento\MagentoCloud\Step\Build\BackupData\WritableDirectories</item>
            </argument>
        </arguments>
    </step>
</scenario>
```

## Een standaardscenario uitbreiden

Het volgende voorbeeld breidt het gebrek uit stelt scenario door extra op te nemen configuratiedossiers aan de hakenconfiguratie toe te voegen.

```yaml
hooks:
  deploy: |
    php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/<vendor-name>/<module-name>/deploy.xml vendor/<vendor-name>/<module-name>/deploy2.xml
```

Tijdens plaatsing, voegen de douanescenario&#39;s met standaard scenario-gebaseerd op de volgende regels samen:

- De scenario&#39;s worden voorrang gegeven aan gebaseerd op hun opeenvolging in de hakdefinitie met het laatste vermelde scenario dat de hoogste prioriteit heeft.

  In het voorbeeld hebben de scenario&#39;s de volgende prioriteit:

   1. `vendor/vendor-name/module-name/deploy2.xml`
   1. `vendor/vendor-name/module-name/deploy.xml`
   1. `scenario/deploy.xml` (standaard- of basislijnscenario)

- De stappen in het hoogste prioritaire scenario treden stappen met de zelfde naam in de andere scenario&#39;s met voeten. Nieuwe stappen worden toegevoegd aan de configuratie. Dezelfde regels gelden voor meer dan twee scenario&#39;s waarbij elk scenario van rechts naar links voorrang krijgt, bijvoorbeeld (C → B → A).

### Standaardstappen verwijderen

Met de parameter `skip` verwijdert u stappen uit standaardscenario&#39;s.

Als u bijvoorbeeld de stappen `enable-maintenance-mode` en `set-production-mode` in het standaard implementatiescenario wilt overslaan, maakt u een configuratiebestand dat de volgende configuratie bevat.

> `vendor/vendor-name/module-name/deploy-custom-mode-config.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <step name="enable-maintenance-mode" skip="true" />
    <step name="set-production-mode"  skip="true" />
</scenario>
```

Als u het aangepaste configuratiebestand wilt gebruiken, werkt u het standaard `.magento.app.yaml` -bestand bij.

> `.magento.app.yaml` met een aangepast implementatiescenario

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/vendor-name/module-name/deploy-custom-mode-config.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

### Standaardstappen vervangen

De scenario&#39;s van de douane kunnen standaardstappen vervangen om douaneimplementatie te verstrekken. Hiervoor gebruikt u de standaardnaam voor de stap als naam voor de aangepaste stap.

Bijvoorbeeld, in het [ gebrek stelt scenario ] in werking de `enable-maintenance-mode` stap stelt het standaard [ EnableMaintenanceMode PHP manuscript ] in werking.

```xml
<step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="300"/>
```

Als u deze stap wilt overschrijven, maakt u een aangepast scenario-configuratiebestand om een ander script uit te voeren wanneer de stap `enable-maintenance-mode` wordt uitgevoerd.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="VendorName\VendorModule\Step\CustomEnableMaintenanceMode" priority="300"/>
</scenario>
```

### De prioriteit van de stap wijzigen

De scenario&#39;s van de douane kunnen de prioriteit van standaardstappen veranderen. In de volgende stap wordt de prioriteit van de `enable-maintenance-mode` -stap gewijzigd van `300` in `10` , zodat de stap eerder wordt uitgevoerd in het implementatiescenario.

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
<scenario>
    <step name="enable-maintenance-mode" type="Magento\MagentoCloud\Step\EnableMaintenanceMode" priority="10"/>
</scenario>
```

In dit voorbeeld gaat de stap `enable-maintenance-mode` naar het begin van het scenario omdat deze een lagere prioriteit heeft dan alle andere stappen in het standaard implementatiescenario.

### Voorbeeld: het implementatiescenario uitbreiden

Het volgende voorbeeld past het [ gebrek toe stelt scenario ] met de volgende veranderingen op:

- Hiermee vervangt u de stap `remove-deploy-failed-flag` door een aangepaste stap
- Hiermee wordt de substap `clean-redis-cache` in de pre-implementatiestap overgeslagen
- Hiermee wordt de stap `unlock-cron-jobs` overgeslagen
- Hiermee slaat u de stap `validate-config` over om kritieke validators uit te schakelen
- Voegt een nieuwe pre-implementatiestap toe

> `vendor/vendor-name/module-name/deploy-extended.xml`

```xml
<?xml version="1.0"?>
<scenario xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:ece-tools:config/scenario.xsd">
    <!-- Replace "remove-deploy-failed-flag" step with custom step -->
    <step name="remove-deploy-failed-flag" type="Vendor\ModuleName\Step\Deploy\RemoveDeployFailedFlag" priority="100"/>

    <!-- Skip "clean-redis-cache" sub-step in pre-deploy step -->
    <step name="pre-deploy" type="Magento\MagentoCloud\Step\Deploy\PreDeploy" priority="200">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="steps" xsi:type="array">
                <item name="clean-redis-cache" xsi:type="object" skip="true"/>
            </argument>
        </arguments>
    </step>

    <!-- Skip step "unlock-cron-jobs" -->
    <step name="unlock-cron-jobs" skip="true"/>

    <!-- Skip critical validators -->
    <step name="validate-config" type="Magento\MagentoCloud\Step\ValidateConfiguration" priority="300">
        <arguments>
            <argument name="logger" xsi:type="object">Psr\Log\LoggerInterface</argument>
            <argument name="validators" xsi:type="array">
                <item name="critical" xsi:type="array">
                    <item name="database-configuration" xsi:type="object" skip="true"/>
                    <item name="search-configuration" xsi:type="object" skip="true"/>
                </item>
            </argument>
        </arguments>
    </step>

    <!-- Add new step into the beginning of the deploy scenario -->
    <step name="new-pre-deploy-step" type="Vendor\ModuleName\Step\Deploy\PreDeploy" priority="10"/>
</scenario>
```

Als u dit script in uw project wilt gebruiken, voegt u de volgende configuratie toe aan het `.magento.app.yaml` -bestand voor uw Adobe Commerce-project voor cloudinfrastructuur:

```yaml
hooks:
    build: |
        set -e
        php ./vendor/bin/ece-tools run scenario/build/generate.xml
        php ./vendor/bin/ece-tools run scenario/build/transfer.xml
    deploy: |
        php ./vendor/bin/ece-tools run scenario/deploy.xml vendor/vendor-name/module-name/deploy-extended.xml
    post_deploy: |
        php ./vendor/bin/ece-tools run scenario/post-deploy.xml
```

>[!TIP]
>
>U kunt de [&#x200B; standaardscenario&#39;s &#x200B;](https://github.com/magento/ece-tools/tree/2002.1/scenario) herzien en [&#x200B; standaardstep configuratie &#x200B;](https://github.com/magento/ece-tools/tree/2002.1/src/Step) in de `ece-tools` bewaarplaats GitHub om te bepalen welke scenario&#39;s en stappen voor uw project bouwen, opstellen, en post-opstelt taken.

## Een aangepaste module toevoegen om uit te breiden `ece-tools`

Het pakket `ece-tools` biedt standaard API-interfaces die voldoen aan de normen voor semantische versies. Alle API-interfaces zijn gemarkeerd met **@api** -annotatie. U kunt de standaard-API-implementatie vervangen door uw eigen implementatie door een aangepaste module te maken en de standaardcode desgewenst te wijzigen.

Als u de aangepaste module met Adobe Commerce wilt gebruiken in de cloud-infrastructuur, moet u de module registreren in de lijst met extensies voor het `ece-tools` -pakket. Het registratieproces is vergelijkbaar met het proces dat u gebruikt om modules te registreren in Adobe Commerce.

**om een module met het `ece-tools` pakket** te registreren:

1. Maak of breid het `registration.php` -bestand uit in de hoofdmap van uw module.

   ```php?start_inline=1
   \Magento\MagentoCloud\ExtensionRegistrar::register('module-name', __DIR__);
   ```

1. Werk de sectie `autoload` voor het configuratiebestand van de module bij om het `registration.php` -bestand op te nemen dat modulebestanden automatisch laadt in `composer.json` .

   ```json
   {
     "name": "vendor/ece-tools-extend",
     "description": "Extension for ece-tools",
     "type": "magento2-component",
     "version": "1.0.0",
     "license": "OSL-3.0",
     "autoload": {
       "files": [ "registration.php" ],
       "psr-4": {
         "Vendor\\EceToolExtend\\": "src/"
       }
     }
   }
   ```

1. Voeg het `config/services.xml` -bestand toe aan uw module. Deze configuratie wordt via `ece-tools` -pakket over `config/services.xml` samengevoegd.

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <container xmlns="http://symfony.com/schema/dic/services"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://symfony.com/schema/dic/services https://symfony.com/schema/dic/services/services-1.0.xsd">
       <services>
           <defaults autowire="true" autoconfigure="true" public="true"/>
   
           <prototype namespace="Vendor\EceToolExtend\" resource="../src/*" exclude="../src/{Test}"/>
   
           <!-- Use your own implementation of EnvironmentDataInterface -->
           <service id="Magento\MagentoCloud\Config\EnvironmentDataInterface" alias="Vendor\EceToolExtend\Config\CustomEnvironmentData" />
       </services>
   </container>
   ```

Meer over gebiedsdeelinjectie leren, zie [&#x200B; Injectie van de Afhankelijkheid van het Symfony &#x200B;](https://symfony.com/doc/current/components/dependency_injection.html).

<!-- link definitions -->

[standaard implementatiescenario]: https://github.com/magento/ece-tools/blob/develop/scenario/deploy.xml
[EnableMaintenanceMode PHP-script]: https://github.com/magento/ece-tools/blob/develop/src/Step/EnableMaintenanceMode.php
