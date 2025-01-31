---
title: Testinstructies
description: Lees meer over testtypen en best practices voor het starten van Adobe Commerce op cloudinfrastructuur.
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Testinstructies

Nadat u uw Adobe Commerce hebt geconfigureerd en aangepast voor het infrastructuurproject voor de cloud, kunt u het beste uw toepassing grondig testen voordat u de website van de winkel start. Testen helpt de verwachtingen ten aanzien van de clustergrootte op de juiste wijze te beheren en schaalt naar behoren voor toekomstige bedrijfsbehoeften.

## Functionele tests

Tijdens de ontwikkeling is het belangrijk om end-to-end functionele tests uit te voeren op uw Adobe Commerce voor het infrastructuurproject van de cloud. Zie de volgende richtlijnen voor het uitvoeren van functionele tests in de Docker-omgeving:

- **het testen van de Toepassing** - gebruik het [ Magento Functional Testing Kader (MFTF) ](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) voor toepassing het testen in het milieu van het Dok van de Wolk.

- **het testen van de Code** - gebruik het [ Codeception testende kader voor PHP ](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/) voor het bevestigen van code die voor bijdrage aan de het pakketbewaarplaatsen van de Wolk bedoeld is.

## Tips en trucs voor het starten

U kunt de volgende testtypen het beste gebruiken voordat u de site start:

- **test van de Lading** - voer een ladingstest uit om het gedrag van het systeem onder een verwachte lading te begrijpen. Test bijvoorbeeld een gelijktijdig aantal actieve gebruikers in de toepassing, waarbij elke gebruiker een specifiek aantal transacties binnen de ingestelde duur uitvoert. Deze test onthult de reactietijd van belangrijke zaken-kritieke transacties, zoals het gegevensbestand of het gedrag van de toepassingsserver. Een belastingstest kan helpen knelpunten op te sporen.

- **test van de Stress** - Uitdaging de hogere grenzen van capaciteit binnen het systeem om te bepalen als het systeem voldoende presteert wanneer de huidige lading veel boven het verwachte maximum gaat.

- **het Scannen van de Veiligheid** - Adobe verstrekt een vrij [ Hulpmiddel van het Scannen van de Veiligheid ](../launch/overview.md#set-up-the-security-scan-tool) voor uw plaatsen.

- **test van de Penetratie** - is een geoorloofde gesimuleerde cyberaanval op een computersysteem dat wordt ontworpen om de veiligheid van het systeem te evalueren. De penetratietest helpt zwakke plekken of kwetsbaarheden te identificeren, waaronder de mogelijkheid voor onbevoegde partijen om toegang te krijgen tot systeemfuncties en gegevens.

>[!WARNING]
>
>Klanten mogen geen beveiligingsbeoordelingen uitvoeren van de AWS-infrastructuur of de AWS-services zelf. Als u een veiligheidskwestie binnen om het even welke diensten van AWS ontdekt die in uw veiligheidsbeoordeling worden waargenomen, [ contacteer de Veiligheid van AWS ](mailto:aws-security@amazon.com) onmiddellijk. Zie [ het beleid van de Klant van AWS voor het testen van de Overboeking ](https://aws.amazon.com/security/penetration-testing/).
