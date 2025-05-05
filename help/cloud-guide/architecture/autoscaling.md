---
title: Automatisch schalen
description: Leer hoe Adobe Commerce op cloudinfrastructuur kan schalen om aan de behoeften aan bronnen te voldoen.
feature: Cloud, Auto Scaling
topic: Architecture
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Automatisch schalen

Automatisch schalen voegt automatisch bronnen toe aan of verwijdert bronnen uit de cloudinfrastructuur om optimale prestaties en redelijke kosten te behouden. Momenteel, is deze eigenschap slechts beschikbaar voor projecten die met a [ worden gevormd Schaalde architectuur ](scaled-architecture.md).

## Webserverknooppunten

De [ schaal van de Webrij ](scaled-architecture.md#web-tier) om een verhoging in procesverzoeken en hogere verkeersvereisten aan te passen. Momenteel wordt de functie voor automatisch schalen alleen horizontaal geschaald door knooppunten van de webserver toe te voegen of te verwijderen.

Er treedt een automatisch schaalbare gebeurtenis op wanneer het CPU-gebruik en het-verkeer een vooraf gedefinieerde drempel bereiken:

- **toegevoegde Knooppunten** - Cpu/cores over alle actieve Webknopen zijn bij 75% capaciteit voor 1 minuut en het verkeer stijgt met 20% voor 5 opeenvolgende notulen.
- **verwijderde Knooppunten** - cpu/kernen over alle actieve Webknopen worden geladen bij 60% voor 20 minuten. Knooppunten worden verwijderd in de volgorde waarin ze zijn toegevoegd.

De minimum- en maximumdrempels worden bepaald en vastgesteld op basis van de contractueel vastgelegde middellimieten van elke handelaar; dit vermindert het risico van oneindige schaling.

## Drempelwaarden bewaken met New Relic

U kunt de [ dienst van New Relic ](../monitor/new-relic-service.md) gebruiken om bepaalde drempels, zoals gastheertelling en het gebruik van CPU te controleren. De volgende New Relic-query&#39;s gebruiken een variabele notatie alleen voor `cluster-id` -doeleinden.

>[!TIP]
>
>Voor een verwijzing bij het bouwen van vragen, zie [ syntaxis NRQL, clausules, en functies ](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/) in de _New Relic_ documentatie.
>Gebruik uw vragen om dashboard van a [ New Relic ](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/introduction-dashboards/) te bouwen.

### Aantal gastheren

In het volgende voorbeeld van een New Relic-query wordt het aantal hosts in de omgeving getoond:

```sql
SELECT uniqueCount(SystemSample.entityId) AS 'Infrastructure hosts', uniqueCount(Transaction.host) AS 'APM hosts seen' FROM SystemSample, Transaction where (Transaction.appName = 'cluster-id_stg' AND Transaction.transactionType = 'Web') OR SystemSample.apmApplicationNames LIKE '%|cluster-id_stg|%' TIMESERIES SINCE 3 HOURS AGO
```

In het volgende schermafbeelding, **zien de gastheren van APM** &lbrace;naar het aantal gastheren met transacties verwijzen die tijdens de geselecteerde periode worden geregistreerd.

![ de gastheertelling van New Relic ](../../assets/new-relic/host-count.png)

### CPU-gebruik

Het volgende voorbeeld van een New Relic-query laat CPU-gebruik voor webknooppunten zien:

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname, apmApplicationNames WHERE instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![ het gebruik van CPU van de Webknopen van New Relic ](../../assets/new-relic/web-node-cpu-usage.png)

## Automatisch schalen inschakelen

Om auto het schrapen voor uw Adobe Commerce op het project van de wolkeninfrastructuur toe te laten of onbruikbaar te maken, [ leg een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voor. Kies de volgende redenen in het ticket:

- **reden van het Contact**: Verzoek van de Verandering van de infrastructuur
- **Reden van het Contact van de Infrastructuur van Adobe Commerce**: Andere Verzoek van de Verandering van de Infrastructuur

>[!IMPORTANT]
>
>Met de functie voor automatisch schalen worden onverwachte gebeurtenissen vastgelegd. Zelfs als u toegelaten auto het schrapen hebt, adviseert de Adobe dat u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) blijft voorleggen als u een aanstaande gebeurtenis verwacht.

### Laden testen

De Adobe laat auto het schrapen op uw project van de Wolk toe _het opvoeren_ cluster eerst. Nadat u het laden in uw omgeving hebt getest en voltooid, schakelt Adobe vervolgens automatische schaling in uw productiecluster in. Voor begeleiding bij lading het testen, zie [ het testen van Prestaties ](../launch/checklist.md#performance-testing).

### IP LIJST VAN GEWENSTE PERSONEN

Na het toelaten van auto het schrapen, komt het uitgaande verkeer van de Webknoop uit de IP adressen van de de dienstknopen voort. Als u een lijst van gewenste personen met een derdedienst gebruikt die niet met uw Adobe Commerce op het project van de wolkeninfrastructuur wordt gebundeld, dan verifieer de IP adressen in de lijst van gewenste personen van de derdendienst.

Bijvoorbeeld:

- Als de lijst van gewenste personen de IP adressen voor uw de dienstknopen (1, 2, en 3) bevat, dan is er geen vereiste actie.
- Als de lijst van gewenste personen de IP adressen voor uw de dienstknopen (1, 2, en 3) en Webknopen (4, 5, en 6)-in dit geval alle zes knopen-toen bevat is er geen vereiste actie.
- Als de lijst van gewenste personen de IP adressen _slechts_ voor uw Webknopen (4, 5, en 6) bevat, dan moet u de lijst van gewenste personen bijwerken om de IP adressen voor de de dienstknopen te omvatten.
