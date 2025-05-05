---
title: Werknemers
description: Leer hoe te om het arbeidersbezit in het  [!DNL Commerce]  dossier van de toepassingsconfiguratie te vormen.
feature: Cloud, Configuration
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Workers, eigenschap

U kunt een worker definiëren die onafhankelijk van de webinstantie moet worden uitgevoerd zonder een actieve Nginx-instantie. De worker gebruikt echter wel dezelfde netwerkopslag die door de [!DNL Commerce] -toepassing wordt gebruikt. U te hoeven niet aan opstelling een Webserver op de arbeidersinstantie (het gebruiken Node.js of Go) omdat de router openbare verzoeken aan de worker niet kan richten. Dit maakt de arbeidersinstantie ideaal voor achtergrondtaken of voortdurend lopende taken die een plaatsing dreigen te blokkeren.

## Een worker configureren

Workers zijn alleen beschikbaar voor gebruik met Pro Staging- en Productomgevingen. De pro integratie en de milieu&#39;s van de Aanzet kunnen verkiezen om [ CRON_CONSUMERS_RUNNER ](../environment/variables-deploy.md#cron_consumers_runner) variabele te gebruiken.

Om een arbeider in Pro het Opvoeren of Productie te vormen, [ leg een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voor en omvat de volgende informatie:

- Project-id
- Milieu-id
- Naam van worker
- Opdrachten starten

U kunt één proces per worker configureren. Een basisconfiguratie van een algemene worker in het `.magento.app.yaml` -bestand kan er als volgt uitzien:

```yaml
workers:
    queue:
        commands:
            start: |
                php ./bin/magento queue:consumers:start commerce.eventing.event.publish
```

In dit voorbeeld wordt één worker met de naam `queue` gedefinieerd, met een klein (grootte-S) niveau van brontoewijzing, en wordt de opdracht `php ./bin/magento` bij het opstarten uitgevoerd. De worker `queue` wordt vervolgens op elk knooppunt als een arbeidersproces uitgevoerd. Als de opdracht wordt afgesloten, wordt deze automatisch opnieuw gestart.

## Opdrachten en overschrijvingen

De `commands.start` -toets is vereist om opdrachten met de arbeiderstoepassing te starten. U kunt elke geldige shell-opdracht gebruiken, hoewel deze ideaal is voor het gebruik van de taal van uw toepassing. Als de opdracht die is opgegeven met de `start` -toets wordt beëindigd, wordt deze automatisch opnieuw gestart.

>[!IMPORTANT]
>
>De opdrachten `deploy` en `post_deploy` hooks en `crons` worden alleen uitgevoerd in de webcontainer, niet in instanties van workers.

### Overerving

Definities voor de eigenschappen `size` , `relationships` , `access` , `disk` en `mount` en `variables` worden overgeërfd door een worker, tenzij ze expliciet worden genegeerd.

De volgende eigenschappen zijn het meest meestal gebruikt om [ top-level montages ](properties.md) met voeten te treden:

- `size` - minder bronnen toewijzen aan één achtergrondproces
- `variables` - de toepassing de opdracht geven anders te werken

### Timing en wachtstand

Hoewel elke worker achter een andere worker in de rij staat, produceert de volgende configuratie een consistente scheiding van twee seconden in tijdstempels in het `var/time.txt` -bestand, ongeacht de 8 seconden durende slaap binnen de PHP-code:

```yaml
workers:
    time1:
        commands:
            start: 'php -r "sleep(8); echo time() . PHP_EOL;" >> var/time.txt& sleep 2'
```
