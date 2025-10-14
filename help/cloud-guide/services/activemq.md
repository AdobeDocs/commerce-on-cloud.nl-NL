---
title: ActiveMQ-service instellen
description: Leer hoe u de ActiveMQ Artemis-service kunt inschakelen voor het beheren van berichtenrijen voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Services
source-git-commit: ef22de6873b49f0fb9adfa9fc343a8d738a543e9
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# [!DNL ActiveMQ] -service instellen

Het [&#x200B; Kader van de Rij van het Bericht (MQF) &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html) is een systeem binnen Adobe Commerce dat a [&#x200B; module &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#module) toestaat om berichten aan rijen te publiceren. Het bepaalt ook de consumenten die de berichten asynchroon ontvangen.

MQF kan [&#x200B; Artemis ActiveMQ &#x200B;](https://activemq.apache.org/components/artemis/) als overseinenmakelaar gebruiken, die een scalable platform voor het verzenden van en het ontvangen van berichten verstrekt. Het omvat ook een mechanisme voor het opslaan van niet-geleverde berichten. [!DNL ActiveMQ Artemis] ondersteunt het STOMP-protocol (Streaming Text Oriented Messaging Protocol) voor berichten.

[!DNL ActiveMQ Artemis] is beschikbaar als alternatief voor RabbitMQ voor het beheren van berichtrijen. Het is met name handig wanneer u functies nodig hebt die specifiek zijn voor ActiveMQ of wanneer u het STOMP-protocol wilt gebruiken.

>[!IMPORTANT]
>
>Als u liever een bestaande berichtenmakelservice gebruikt, zoals [!DNL ActiveMQ] , in plaats van Adobe Commerce op een cloudinfrastructuur te vertrouwen om deze voor u te maken, gebruikt u de [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) -omgevingsvariabele om deze aan te sluiten op uw site.

{{service-instruction}}

**om Artemis toe te laten ActiveMQ**:

1. Voeg de vereiste naam, het type en de schijfwaarde (in MB) toe aan het `.magento/services.yaml` -bestand en aan de geïnstalleerde ActiveMQ-versie.

   ```yaml
   activemq-artemis:
       type: activemq-artemis:<version>
       disk: 1024
   ```

1. Configureer de relaties in het `.magento.app.yaml` -bestand.

   ```yaml
   relationships:
       activemq-artemis: "activemq-artemis:activemq-artemis"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable ActiveMQ Artemis service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [&#x200B; verifieer de de dienstverhoudingen &#x200B;](services-yaml.md#service-relationships).

{{service-change-tip}}

## Verbinding maken met ActiveMQ voor foutopsporing

Voor het zuiveren doeleinden, kunt u met een de dienstinstantie op één van de volgende manieren direct verbinden:

- Verbinding maken met uw lokale ontwikkelomgeving
- Verbinding maken vanuit de toepassing
- Verbinding maken met uw PHP-toepassing

### Verbinding maken met uw lokale ontwikkelomgeving

1. Meld u aan bij de `magento-cloud` CLI en het project:

   ```bash
   magento-cloud login
   ```

1. Ontdek de omgeving met ActiveMQ Artemis geïnstalleerd en geconfigureerd.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. SSH gebruiken om verbinding te maken met de cloud-omgeving:

   ```bash
   magento-cloud ssh
   ```

1. Haal de verbindingsdetails ActiveMQ en login geloofsbrieven van [$MAGENTO_CLOUD_RELATIONSHIPS &#x200B;](../application/properties.md#relationships) variabele terug:

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   In de reactie, vind de informatie ActiveMQ. De relatienaam hangt van af hoe u het in uw `.magento.app.yaml` dossier vormde. Als u bijvoorbeeld `activemq-artemis` als relatienaam hebt gebruikt:

   ```json
   {
      "activemq-artemis" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "stomp",
            "port" : 61616,
            "host" : "activemq-artemis.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Laat lokale haven toe door:sturen aan ActiveMQ (als uw project op een verschillend gebied zoals V.S.-3, EU-5, of AP-3 gebied wordt gevestigd, substitueer ``us-3``/``eu-5``/ ``ap-3`` voor ``us``)

   ```bash
   ssh -L <port-number>:activemq-artemis.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Een voorbeeld voor toegang tot de ActiveMQ Artemis-webconsole op `http://localhost:8161` is:

   ```bash
   ssh -L 8161:activemq-artemis.internal:8161 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   >[!NOTE]
   >
   >ActiveMQ Artemis gebruikt poort 61616 voor STOMP-berichten en poort 8161 voor de webconsole.

1. Terwijl de sessie is geopend, kunt u de ActiveMQ Artemis-webconsole op `http://localhost:8161` openen met de gebruikersnaam en het wachtwoord van de MAGENTO_CLOUD_RELATIONSHIPS-variabele.

### Verbinding maken vanuit de toepassing

Als u verbinding wilt maken met ActiveMQ die wordt uitgevoerd in een toepassing, installeert u een STOMP-clientbibliotheek in uw PHP-toepassing.

### Verbinding maken met uw PHP-toepassing

Als u verbinding wilt maken met ActiveMQ met uw PHP-toepassing, voegt u een PHP STOMP-bibliotheek toe aan de bronstructuur. Adobe Commerce gebruikt het STOMP-protocol voor ActiveMQ-communicatie en de configuratie wordt automatisch ingesteld tijdens de implementatie wanneer ActiveMQ-artemis wordt gedetecteerd als een geconfigureerde service.

## Protocol-ondersteuning

ActiveMQ-artemis in Adobe Commerce op cloudinfrastructuur gebruikt het STOMP-protocol (Streaming Text Oriented Messaging Protocol):

- **STOMP**: Het overseinenprotocol dat voor rijverrichtingen (haven 61616) wordt gebruikt
- **Console van het Web**: De interface van het beheer toegankelijk via HTTP (haven 8161)

## Verschillen met KonijnMQ

Hoewel zowel [!DNL ActiveMQ Artemis] als [!DNL RabbitMQ] fungeren als berichtenmakelaars voor Adobe Commerce, zijn er enkele verschillen:

- **Protocol**: De Artemis van ActiveMQ gebruikt STOMP protocol, terwijl RabbitMQ AMQP gebruikt
- **Configuratie**: Wanneer de Artemis ActiveMQ wordt gevormd, gebruikt Adobe Commerce automatisch het protocol van STOMP
- **Prioriteit**: Als zowel ActiveMQ als RabbitMQ worden gevormd, neemt ActiveMQ belangrijkheid voor op STOMP-Gebaseerde verrichtingen, terwijl de verrichtingen van AMQP RabbitMQ gebruiken
- **Console van het Web**: ActiveMQ verstrekt een web-based beheersconsole voor controlerijen en berichten

## Wachtrijconfiguratie

Wanneer de Artemis ActiveMQ als dienst wordt gevormd, vormt Adobe Commerce automatisch het rijsysteem om het protocol van STOMP te gebruiken. De configuratie wordt tijdens de implementatie naar het `app/etc/env.php` -bestand geschreven:

```php
'queue' => [
    'stomp' => [
        'host' => 'activemq-artemis.internal',
        'port' => '61616',
        'user' => 'guest',
        'password' => 'guest'
    ],
    'default_connection' => 'stomp'
]
```

U kunt deze configuratie indien nodig negeren met de omgevingsvariabele [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) .

