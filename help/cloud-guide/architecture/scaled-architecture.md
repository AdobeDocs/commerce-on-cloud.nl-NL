---
title: Schaalbare architectuur
description: Lees meer over de gesplitste architectuur en hoe deze geschaald kan worden uitgebreid om aan de vraag te voldoen.
feature: Cloud, Auto Scaling, Iaas, Logs
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# Schaalbare architectuur

De Cloud-infrastructuur wordt geschaald op basis van uw vereisten voor bronnen voor een hogere efficiëntie. De Adobe Commerce op cloudinfrastructuur bewaakt uw toepassingen en kan de capaciteit aanpassen om stabiele, voorspelbare prestaties te behouden. Het omzetten in deze architectuur helpt om problemen, zoals latentie of grote pieken in verkeer te verlichten.

>[!NOTE]
>
>De geschaalde architectuur is beschikbaar voor Adobe Commerce op cloudinfrastructuuraccounts met de Pro 48-cluster of hoger.

## Architectuur op gesplitste niveaus

De Pro-architectuur bestond uit drie knooppunten, die elk een volledige technologiestapel bevatten. Nu, is er een scalable infrastructuur die een gelaagde architectuur met een minimum van zes knopen verstrekt: drie knopen voor het kerngegevensbestand en de diensten en drie knopen voor de Webserver. Deze gesplitste architectuur biedt de mogelijkheid om lagen onafhankelijk te schalen om een optimale balans van prestaties te bereiken.

### Serviceniveau

Er zijn drie de dienstknopen voor gegevensopslag, geheime voorgeheugen, en de diensten: **OpenSearch** of **Elasticsearch**, **MariaDB**, **Redis**, en meer. Wanneer de serviceniveau de capaciteit nadert, kunt u alleen schalen door de servergrootte te vergroten, bijvoorbeeld door de CPU-voeding en -geheugen op te voeren. De capaciteit is beperkt tot de grootte van de knoop die beschikbaar is. Omdat de gegevensbestandcluster voor hoge beschikbaarheid wordt ontworpen, kunt u niet horizontaal met de gebruikte technologieën schrapen.

![ het rij schrapen van de Dienst ](../../assets/scaling-service.png)

Overweeg een voorbeeld dat het de instantietype van de de dienstknoop _m5.2xlarge_ met 32-Gb RAM is. Een service, zoals de database, gebruikt een aanzienlijke hoeveelheid geheugen (30 Gb). Het schrapen aan de volgende beschikbare instantiegrootte _m5.4xlarge_ verstrekt 64-Gb RAM, die het geheugen verdubbelt en de groeiende behoeften van het gegevensbestand aanpast.

U kunt de prestaties van de de dienstrij verder optimaliseren door verkeer te verpletteren dat op het knooptype wordt gebaseerd. Door gebrek, wordt de gegevensbestandknoop geïsoleerd van het Webverkeer. Als voorbeeld kunt u ervoor kiezen om het webverkeer op het databaseknooppunt te bedienen.

### Weblaag

Er zijn drie Webknopen voor verwerkingsverzoeken en Webverkeer: **php-fpm** en **NGINX**. Naast verticale schaling door meer stroom en geheugen te gebruiken, kan de weblaag ook horizontaal worden geschaald door webservers toe te voegen aan een bestaande cluster wanneer deze beperkt zijn op PHP-niveau. Zie [ Auto het schrapen ](autoscaling.md) leren hoe de Webknopen automatisch schrapen.

![ het rij schrapen van het Web ](../../assets/scaling-web.png)

Dit vult de verticale schaling aan die door de de dienstrij wordt verstrekt. Aangezien de de dienstrij in grootte en macht schrapt om een groeiend gegevensbestand en de dienstgebruik aan te passen, de Webrijschaal in grootte, macht, en instanties om een toename van procesverzoeken en hogere verkeersvereisten aan te passen.

Overweeg een voorbeeld dat het de instantietype van de Webknoop _C5.2xlarge met acht cpu en 16-Gb RAM_ is. Het aantal verzoeken aan de plaats nam sterk toe. U kunt een C5.2xlarge knoop toevoegen om de toename in php-fpm processen te behandelen of u kunt elk instantietype in _C5.4xlarge met 16 CPU en 32-Gb RAM_ veranderen. Als u een knooppunt toevoegt, neemt het risico van onvoldoende piekcapaciteit af.

## Projectstructuur

Minimaal, hebben de Pro projecten met de Schaalde architectuur zes beschikbare knopen.

- 3 webknooppunten c5.2xlarge (8 CPU, 16 Gb RAM)

- 3 serviceknooppunten m5.2xlarge (8 CPU, 32 Gb RAM)

Elk project is echter uniek en vereist prestatiebewaking om het beheer van bronnen correct te analyseren. Elke rekening omvat de [ dienst van New Relic ](../monitor/new-relic-service.md), die automatisch met de toepassingsgegevens en prestatiesanalyses verbindt om dynamische servercontrole te verstrekken. Specifiek, kunt u de dienst van New Relic gebruiken om CPU en het gebruik van RAM te controleren om te bepalen welke knopen extra middelen vereisen. Wanneer een bron capaciteit bereikt of wanneer de prestaties achteruitgaan op basis van de analyse, kunt u een verzoek maken om uw infrastructuur te schalen om aan de vraag te voldoen.

### SSH-toegang

Bepaalde bestanden en logbestanden, zoals de map `/app/<project-id>/var/log` , worden niet gedeeld tussen knooppunten. Elk knooppunt heeft een unieke SSH-toegang. U kunt de CLI van `magento-cloud` niet gebruiken om zich aan te melden bij de dienst of de Webknopen, maar u kunt de knoopadressen in de lijst van de Toegang van SSH in uw [!DNL Cloud Console] vinden.

```bash
ssh <node>.<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
```

- `node` 1 door 3 - Adressen om tot de de dienstknopen toegang te hebben

- `node` 4 door _n_ - Adressen om tot de Webknopen toegang te hebben

>[!TIP]
>
>Na u login, kunt u serveridentiteitskaart en de rol bevestigen: de dienstknopen gebruiken de _verenigde_ rol, en de Webknopen gebruiken de _Web_ rol.

De reactie van het voorbeeld aangezien u login aan a **de dienstknoop** omvat _verenigde_ rol:

```
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:unified.

project-id@server-id:~$
```

De reactie van het voorbeeld aangezien u login aan a **Webknoop** omvat de _Web_ rol:

```
 __  __                   _          ___ _             _
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/

 Welcome to Magento Cloud.

 This is server unique-server-id, role project-id:web.

project-id@server-id:~$
```

### Loglocaties

De logboekplaatsen variëren lichtjes afhankelijk van de knoop. Bijvoorbeeld, is een gegevensbestandlogboek, zoals het **MySQL foutenlogboek**, beschikbaar op een de dienstknoop (`/var/log/mysql/mysql-error.log`), maar het is niet beschikbaar op een Webknoop.

Elke Pro rekening omvat de [ dienst van Logboeken van New Relic ](../monitor/new-relic-service.md), die automatisch met logboekgegevens van de toepassing verbindt om dynamisch logboekbeheer te verstrekken. Samengevoegde loggegevens van alle knooppunten worden weergegeven in de toepassing New Relic Logs, zodat u problemen met de prestaties van specifieke knooppunten op één dashboard kunt oplossen.
