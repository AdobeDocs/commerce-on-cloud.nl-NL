---
title: RabbitMQ-service instellen
description: Leer hoe u de RabbitMQ-service in staat stelt om berichtwachtrijen voor Adobe Commerce te beheren op cloudinfrastructuur.
feature: Cloud, Services
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# [!DNL RabbitMQ] -service instellen

Het [&#x200B; Kader van de Rij van het Bericht (MQF) &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html?lang=nl-NL) is een systeem binnen Adobe Commerce dat a [&#x200B; module &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-operations/implementation-playbook/glossary#module) toestaat om berichten aan rijen te publiceren. Het bepaalt ook de consumenten die de berichten asynchroon ontvangen.

MQF gebruikt [&#x200B; RabbitMQ &#x200B;](https://www.rabbitmq.com/) als overseinenmakelaar, die een scalable platform voor het verzenden van en het ontvangen van berichten verstrekt. Het omvat ook een mechanisme voor het opslaan van niet-geleverde berichten. [!DNL RabbitMQ] is gebaseerd op de Geavanceerde specificatie 0.9.1 van het een rij vormen van het Bericht van het Protocol (AMQP).

>[!WARNING]
>
>Als u liever een bestaande AMQP-gebaseerde service gebruikt, zoals [!DNL RabbitMQ] , in plaats van Adobe Commerce op cloudinfrastructuur te vertrouwen om deze voor u te maken, gebruikt u de [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) -omgevingsvariabele om deze aan uw site te koppelen.

{{service-instruction}}

**om RabbitMQ** toe te laten:

1. Voeg de vereiste naam, het type en de schijfwaarde (in MB) toe aan het `.magento/services.yaml` -bestand en aan de geïnstalleerde RabbitMQ-versie.

   ```yaml
   rabbitmq:
       type: rabbitmq:<version>
       disk: 1024
   ```

1. Configureer de relaties in het `.magento.app.yaml` -bestand.

   ```yaml
   relationships:
       rabbitmq: "rabbitmq:rabbitmq"
   ```

1. U kunt wijzigingen in de code toevoegen, doorvoeren en doorvoeren.

   ```bash
   git add .magento/services.yaml .magento.app.yaml
   ```

   ```bash
   git commit -m "Enable RabbitMQ service"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. [&#x200B; verifieer de de dienstverhoudingen &#x200B;](services-yaml.md#service-relationships).

{{service-change-tip}}

## Verbinding maken met RabbitMQ voor foutopsporing

Voor het zuiveren doeleinden, is het nuttig om met een de dienstinstantie op één van de volgende manieren direct te verbinden:

- Verbinding maken met uw lokale ontwikkelomgeving
- Verbinding maken vanuit de toepassing
- Verbinding maken met uw PHP-toepassing

### Verbinding maken met uw lokale ontwikkelomgeving

1. Meld u aan bij de `magento-cloud` CLI en het project:

   ```bash
   magento-cloud login
   ```

1. Ontdek de omgeving met RabbitMQ geïnstalleerd en geconfigureerd.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. SSH gebruiken om verbinding te maken met de cloud-omgeving:

   ```bash
   magento-cloud ssh
   ```

1. Haal de de verbindingsdetails van RabbitMQ en login geloofsbrieven van [$MAGENTO_CLOUD_RELATIONSHIPS &#x200B;](../application/properties.md#relationships) variabele terug:

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   of

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   In het antwoord vindt u bijvoorbeeld de RabbitMQ-informatie:

   ```json
   {
      "rabbitmq" : [
         {
            "password" : "guest",
            "ip" : "246.0.129.2",
            "scheme" : "amqp",
            "port" : 5672,
            "host" : "rabbitmq.internal",
            "username" : "guest"
         }
      ]
   }
   ```

1. Enable local port forward to RabbitMQ (als uw project zich op een verschillend gebied zoals V.S.-3, EU-5, of AP-3 gebied bevindt, substitueer ``us-3``/``eu-5``/``ap-3`` for ``us``)

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Een voorbeeld voor toegang tot de RabbitMQ Management Web Interface op `http://localhost:15672` is:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. Terwijl de zitting open is, kunt u een cliënt van RabbitMQ van uw keus van uw lokaal werkstation beginnen, die wordt gevormd om met `localhost:<portnumber>` te verbinden gebruikend het havenaantal, gebruikersbenaming, en wachtwoordinformatie van de variabele MAGENTO_CLOUD_RELATIONSHIPS.

### Verbinding maken vanuit de toepassing

Om met RabbitMQ te verbinden die in een toepassing loopt, installeer een cliënt, zoals [&#x200B; amqp-utils &#x200B;](https://github.com/dougbarth/amqp-utils), als projectgebiedsdeel in uw `.magento.app.yaml` dossier.

Bijvoorbeeld:

```yaml
dependencies:
    ruby:
        amqp-utils: "0.5.1"
```

Wanneer u zich aanmeldt bij uw PHP-container, voert u een `amqp-` -opdracht in die beschikbaar is voor het beheren van uw wachtrijen.

### Verbinding maken met uw PHP-toepassing

Als u verbinding wilt maken met RabbitMQ met uw PHP-toepassing, voegt u een PHP-bibliotheek toe aan de bronstructuur.
