---
title: Logboekhandlers
description: Leer hoe u loghandlers voor Adobe Commerce kunt configureren op cloudinfrastructuur.
feature: Cloud, Logs, Configuration
role: Developer
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Logboekhandlers

U kunt logboekmanagers vormen om berichten naar een verre registrerenserver te verzenden. Een logboekmanager duwt bouw en stelt logboeken aan andere systemen op, gelijkaardig aan de manier u logboeken aan Slack en e-mail duwt. U kunt a _syslog_ manager toelaten, die voor registrerenberichten met betrekking tot hardware, of een Graylog Uitgebreide manager van het Logboek van het Formaat (GELF) ideaal is, die voor registrerenberichten van softwaretoepassingen ideaal is.

In het volgende voorbeeld worden beide handlers geconfigureerd door de configuratie aan het `.magento.env.yaml` -bestand toe te voegen. Voor het minimale registrerenniveau (`min_level`) waarden, zie [&#x200B; niveaus van het Logboek &#x200B;](#log-levels).

```yaml
log:
  syslog:
    ident: "<syslog-ident>"
    facility: 8 # https://php.net/manual/en/network.constants.php
    min_level: "info"
    logopts: <syslog-logopts>

  syslog_udp:
    host: "<syslog-host>"
    port: <syslog-port>
    facility: 8  # https://php.net/manual/en/network.constants.php
    ident: "<syslog-ident>"
    min_level: "info"

  gelf:
    min_level: "info"
    use_default_formatter: true
    additional: # Some additional information for each log message
      project: "<some-project-id>"
      app_id: "<some-app-id>"
    transport:
      http:
        host: "<http-host>"
        port: <http-port>
        path: "<http-path>"
        connection_timeout: 60
      tcp:
        host: "<tcp-host>"
        port: <tcp-port>
        connection_timeout: 60
      udp:
        host: "<udp-host>"
        port: <udp-port>
        chunk_size: 1024
```

## Logboekniveaus

De niveaus van het logboek bepalen het niveau van detail in berichtberichten. De volgende categorieën van het logboekniveau omvatten elk logboekniveau onder het. Een niveau `debug` omvat bijvoorbeeld logbestanden op elk niveau, terwijl een niveau `alert` alleen waarschuwingen en noodsituaties weergeeft.

- **zuivert** - gedetailleerd zuivert informatie
- **info** - interessante gebeurtenissen, zoals een gebruikerslogin of SQL logboek
- **bericht** - normaal, maar significante gebeurtenissen
- **waarschuwing** - uitzonderlijke voorkomen die geen fouten, zoals het gebruik van afgekeurde API of slecht gebruik van API zijn
- **fout** - runtime fouten die geen directe actie vereisen
- **kritieke** - kritieke voorwaarden, zoals een niet beschikbare toepassingscomponent of een onverwachte uitzondering
- **waakzaam** - directe vereiste actie-zulke als een website is neer of het gegevensbestand niet beschikbaar-dat een alarm van SMS teweegbrengt
- **nood** - het systeem is onbruikbaar
