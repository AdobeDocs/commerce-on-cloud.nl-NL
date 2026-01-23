---
title: RabbitMQ-service instellen
description: Leer hoe u de RabbitMQ-service kunt inschakelen voor het beheren van berichtenrijen voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Services
exl-id: 64af1dfa-e3f0-4404-a352-659ca47c1121
source-git-commit: 258fe6de7a8b80cb3403f1ce04d0bf2e299f68ae
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# [!DNL RabbitMQ] -service instellen

Het [&#x200B; Kader van de Rij van het Bericht (MQF) &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework.html?lang=nl-NL) is een systeem binnen Adobe Commerce dat a [&#x200B; module &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-operations/implementation-playbook/glossary#module) toestaat om berichten aan rijen te publiceren. Het bepaalt ook de consumenten die de berichten asynchroon ontvangen.

MQF gebruikt [&#x200B; RabbitMQ &#x200B;](https://www.rabbitmq.com/) als overseinenmakelaar, die een scalable platform voor het verzenden van en het ontvangen van berichten verstrekt. Het omvat ook een mechanisme voor het opslaan van niet-geleverde berichten. [!DNL RabbitMQ] is gebaseerd op de Geavanceerde specificatie 0.9.1 van het een rij vormen van het Bericht van het Protocol (AMQP).

>[!NOTE]
>
>Adobe Commerce op wolkeninfrastructuur steunt ook [&#x200B; Artemis ActiveMQ &#x200B;](activemq.md) als alternatieve dienst van de berichtrij gebruikend het protocol van STOMP.

>[!IMPORTANT]
>
>Als u liever een bestaande AMQP-gebaseerde service gebruikt, zoals [!DNL RabbitMQ] , in plaats van Adobe Commerce op cloudinfrastructuur te vertrouwen om deze voor u te maken, gebruikt u de [`QUEUE_CONFIGURATION`](../environment/variables-deploy.md#queue_configuration) -omgevingsvariabele om deze aan uw site te koppelen.

{{service-instruction}}

**om RabbitMQ** toe te laten:

1. Voeg de vereiste naam, het type en de schijfwaarde (in MB) toe aan het `.magento/services.yaml` -bestand, samen met de geïnstalleerde RabbitMQ-versie.

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

   In de reactie, vind de informatie RabbitMQ, bijvoorbeeld:

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

1. Laat lokale haven toe door:sturen aan RabbitMQ (als uw project op een verschillend gebied zoals V.S.-3, EU-5, of AP-3 gebied wordt gevestigd, substitueer ``us-3``/``eu-5``/ ``ap-3`` voor ``us``)

   ```bash
   ssh -L <port-number>:rabbitmq.internal:<port-number> <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

   Een voorbeeld voor het verkrijgen van toegang tot de RabbitMQ-beheerwebinterface in `http://localhost:15672` is:

   ```bash
   ssh -L 15672:rabbitmq.internal:15672 <project-ID>-<branch-ID>@ssh.us.magentosite.cloud
   ```

1. Terwijl de sessie geopend is, kunt u een willekeurige RabbitMQ-client starten vanuit uw lokale werkstation, geconfigureerd om verbinding te maken met de `localhost:<portnumber>` . Hiervoor gebruikt u het poortnummer, de gebruikersnaam en de wachtwoordgegevens van de variabele MAGENTO_CLOUD_RELATIONSHIPS.

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

## Problemen met de service [!DNL RabbitMQ] oplossen

Zie [&#x200B; Onbekwaam om met RabbitMQ in de Wolk van de Handel van Adobe te verbinden &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-cloud-kcs/kbarticles/ka-27688).

## De service [!DNL RabbitMQ] bijwerken

>
>
>Sla versies niet over wanneer u [!DNL RabbitMQ] bijwerkt in een integratieomgeving. Slechts [&#x200B; opeenvolgende verbeteringen &#x200B;](https://www.rabbitmq.com/docs/upgrade#rabbitmq-version-upgradability) worden gesteund (bijvoorbeeld, 3.8 → 3.9 → 3.10 → 3.11 → 3.12 → 3.13 → 4.0 → 4.1), en elke versiebump moet aan een daadwerkelijke, succesvolle plaatsing van uw milieu van de Wolk beantwoorden.
>
>Voor de algemene instructies van de de dienstverbetering, zie [&#x200B; de dienstversie van de Verandering &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-on-cloud/user-guide/configure/service/services-yaml#change-service-version).
