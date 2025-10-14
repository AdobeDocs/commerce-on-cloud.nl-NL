---
title: New Relic-logbeheer
description: Meer informatie over het gebruik van het New Relic-logboek
feature: Cloud, Logs, Observability
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# New Relic-logbeheer

Alle projecten van de wolkeninfrastructuur omvatten [&#x200B; het logboekbeheer van New Relic &#x200B;](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/). De dienst wordt pre-gevormd om alle logboekgegevens van uw het Opvoeren en milieu&#39;s van de Productie samen te voegen en het in een gecentraliseerd logboekbeheersdashboard te tonen.

De geaggregeerde gegevens bevatten informatie uit de volgende logboeken:

- Alle `ece-tools` - en toepassingslogbestanden uit de `~/var/log` -map
- Logboeken voor cloudservices vanuit de map `var/log/platform/<project-ID>`
- Fastly CDN en WAF

Wanneer uw project is verbonden met New Relic, kunt u de service New Relic Logs gebruiken om taken als:

- New Relic-query&#39;s gebruiken om geaggregeerde loggegevens te zoeken
- Loggegevens visualiseren via de toepassing New Relic Logs
- Aangepaste grafieken, dashboards en waarschuwingen maken
- Problemen met prestaties oplossen via één dashboard

## Loggegevens weergeven en analyseren

Gebruik de New Relic Logs-toepassing om de geaggregeerde loggegevens te doorzoeken en toepassings-, infrastructuur-, CDN- en WAF-fouten op te lossen. U kunt grafieken, dashboards, en alarm tot stand brengen gebruikend logboekgegevens die bij de diensten van New Relic APM en van de Infrastructuur worden verzameld.

**om de toepassing van Logs van New Relic te gebruiken**:

1. Login aan uw [&#x200B; rekening van New Relic &#x200B;](https://login.newrelic.com/login).

1. Selecteer **Logboeken** van het de navigatiemenu van de Ontdekkingsreiziger.

1. Verifieer dat uw Rekening bij de bovenkant van _wordt geselecteerd Al logboeken_ mening.

1. Selecteer een tijdbereik voor de Logs-query.

1. Om de gegevens van het infrastructuurlogboek voor de wolkendiensten (logboeken van `~/var/log/`) te herzien, ga het vraagkoord `has: "filePath"` op het _Onderzoek naar Logs_ gebied in. Klik vervolgens op **[!UICONTROL Query logs]** .

   De namen van de logbestanden worden opgeslagen in de kolom `filePath` , met volledige paden naar het logbestand.

   ![&#x200B; de gegevens van het de dienstlogboek van het projectNew Relic van de Wolk &#x200B;](../../assets/new-relic/var-log-query.png)

1. Om gegevens van het logboek van de overzicht snel te herzien, ga het vraagkoord `has: "client_ip"` op het _Onderzoek naar Logs_ gebied in. Klik vervolgens op **[!UICONTROL Query logs]** .

1. Als u de resultaten van het snellog wilt filteren op landcode, klikt u op **[!UICONTROL Add column]** en selecteert u vervolgens **[!UICONTROL geo_country_code]** .

   ![&#x200B; het logboekattributenfilter van New Relic CDN van het project van de Wolk &#x200B;](../../assets/new-relic/fastly-countrycode-filter.png)

>[!TIP]
>
>U kunt de vraagmening van _Bewaarde meningen_ dropdown bewaren. Klik op **[!UICONTROL Create new]** , geef een naam op, selecteer opties en klik op **[!UICONTROL Save view]** .
>
>Zie [&#x200B; begonnen met logboekbeheer &#x200B;](https://docs.newrelic.com/docs/logs/get-started/get-started-log-management/) en [&#x200B; Inleiding aan de vraagtaal van New Relic &#x200B;](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/) op de _New Relic Docs_ plaats worden.
