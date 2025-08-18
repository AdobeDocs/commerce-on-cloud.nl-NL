---
title: Workflow voor Pro-projecten
description: Leer hoe u de workflows voor ontwikkeling en implementatie van Pro gebruikt.
feature: Cloud, Iaas, Paas
exl-id: efe41991-8940-4d5c-a720-80369274bee3
source-git-commit: 8aacac9ae721bc98cbe29e67ddf23d784e478e55
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 0%

---

# Workflow voor Pro-projecten

Het Pro-project bevat één Git-opslagplaats met een globale `master` vertakking en drie grote omgevingen:

1. **het milieu van de Productie** voor lancering en het handhaven van de levende plaats
1. **het Opvoeren** milieu voor het testen met alle diensten
1. **het milieu van de Integratie** voor ontwikkeling en het testen

![ Pro milieulijst ](../../assets/pro-environments.png)

Dit zijn `read-only` omgevingen die geïmplementeerde codewijzigingen accepteren die alleen vanuit uw lokale werkruimte worden doorgegeven.

In de volgende afbeelding ziet u hoe de workflow voor het ontwikkelen en implementeren van Pro is gebaseerd op een eenvoudige, vertakkende aanpak. U [ ontwikkelt ](#development-workflow) code gebruikend een actieve tak die op het `integration` milieu wordt gebaseerd, _duwend_ en _trekken_ codeveranderingen aan en van uw verre, Actieve tak. U stelt geverifieerde code door _samen te voegen_ de verre tak aan de basistak op, die een geautomatiseerd [ bouwt en ](#deployment-workflow) proces voor dat milieu opstelt.

![ mening op hoog niveau van het Pro werkschema van de architectuurontwikkeling ](../../assets/pro-dev-workflow.png)

Omdat de omgeving alleen-lezen is, kunt u geen wijzigingen in de code rechtstreeks in de Cloud-omgeving doorvoeren. Als u `composer install` probeert uit te voeren om modules te installeren, wordt een fout gegenereerd, bijvoorbeeld:

```bash
file_put_contents(...): Failed to open stream: Read-only file system  
The disk hosting /app/<cluster_ID> is full
```

Voor meer informatie, zie [ Pro architectuur ](pro-architecture.md) voor een overzicht van Pro milieu&#39;s, en zie [[!DNL Cloud Console]](../project/overview.md#cloud-console) voor een overzicht van de Pro milieu&#39;s lijst in de projectweergave.

## Ontwikkelingsworkflow

De integratieomgeving biedt één basisvertakking `integration` met uw Adobe Commerce op code voor de cloud-infrastructuur. U kunt één extra actieve omgevingsvertakking maken. Dit staat voor maximaal twee actieve takken toe die aan Platform als de dienstcontainers (PaaS) worden opgesteld. Er is geen limiet voor het aantal niet-actieve omgevingen, maar hoe meer inactieve omgevingen er zijn, hoe langer het duurt voordat de Cloud Console wordt geladen.

{{enhanced-integration-envs}}

De projectmilieu&#39;s steunen een flexibel, ononderbroken integratieproces. Eerst kloont u de `integration` -vertakking naar uw lokale projectmap. Creeer een tak, of veelvoudige takken, ontwikkel nieuwe eigenschappen, vorm veranderingen, voeg uitbreidingen toe, en stel updates op:

- **Vetch** veranderingen van `integration`

- **Tak** van `integration`

- **ontwikkelt** code op een lokaal werkstation, met inbegrip van [!DNL Composer] updates

- **duw** codeveranderingen in ver en bevestigt

- **Fusie** aan `integration` en test

Met een ontwikkelde codevertakking en de overeenkomstige configuratiedossiers, zijn uw codeveranderingen klaar om aan de `integration` tak voor uitvoeriger het testen samen te voegen. De `integration` -omgeving is ook het meest geschikt voor:

- **Integrerend derdediensten** - niet zijn alle diensten beschikbaar in het milieu PaaS.

- **Genererend configuratiebeheersdossiers** - sommige configuratiemontages zijn _slechts Lees_ in een opgesteld milieu.

- **Vormend uw opslag** - u zou alle opslagmontages volledig moeten vormen gebruikend het integratiemilieu. U kunt **Admin URL van de Opslag** op de _integratie_ milieumening in _[!DNL Cloud Console]_&#x200B;vinden.

## Implementatieworkflow

Telkens als u code van uw lokale werkstation aan het verre milieu duwt of code aan een milieutak samenvoegt, bouwt en stelt manuscripten op produceren nieuwe code en levering de gevormde diensten aan het verre milieu op.

Scripthandelingen maken:

- De plaats in het doelmilieu blijft tijdens een bouwstijl lopen

- Adobe Commerce controleren en uitvoeren op patches en hotfixes voor cloudinfrastructuur

- Compileer code met een bouwstijl en stel logboek op

- Controleren op configuratiebeheer, implementatie van statische inhoud vindt plaats tijdens deze fase

- Een witruimte maken of gebruiken in ongewijzigde code om het proces te versnellen

- Alle back-endservices en -toepassingen aanbieden

Scripthandelingen implementeren:

- Plaats de plaats in het doelmilieu op a _wijze van het Onderhoud_

- Statische inhoud implementeren als deze niet is voltooid tijdens de build

- Adobe Commerce installeren of bijwerken op cloudinfrastructuur

- Vorm het verpletteren voor verkeer

Na het proces voor het maken en implementeren van code komt uw winkel online terug met de nieuwste codewijzigingen en -configuraties. Zie [ proces van de Plaatsing ](../deploy/process.md).

### Samenvoegen tot integratie

Combineer alle geverifieerde codewijzigingen door uw actieve ontwikkelingsvertakking samen te voegen tot de basissvertakking `integration` . U kunt al uw wijzigingen in de `integration` -vertakking testen voordat u wijzigingen in de Staging-omgeving bevordert.

### Samenvoegen tot fasering

Staging is een omgeving vóór de productie die alle services en instellingen zo dicht mogelijk bij de productieomgeving biedt. Duw altijd uw codeveranderingen van het `integration` milieu aan het `staging` milieu zodat u grondig het testen met alle diensten kunt uitvoeren. De eerste keer u het opvoeren milieu gebruikt, moet u de diensten, zoals [ snel CDN ](../cdn/fastly.md) en [ New Relic ](../monitor/new-relic-service.md) vormen. Configureer betaalgateways, verzendingen, meldingen en andere essentiële services met sandbox- of testgegevens.

Het is best om elke dienst grondig te testen, uw prestaties testende hulpmiddelen te verifiëren, en het testen van UAT als beheerder en als klant uit te voeren, tot u vindt dat uw opslag klaar voor het productiemilieu is. Zie [ uw opslag ](../deploy/staging-production.md) opstellen.

{{second-staging}}

### Samenvoegen tot productie

Na grondig het testen in het opvoeren milieu, fusie aan het productiemilieu en grondig test gebruikend levende geloofsbrieven. Wanneer u uw productiesite start, moeten klanten hun aankopen kunnen voltooien en moeten beheerders de live winkel kunnen beheren. Zie de volgende onderwerpen voor een gedetailleerde, duidelijke looppas-door voor het opstellen van uw opslag en het gaan live:

- [Je winkel implementeren](../deploy/staging-production.md)
- [Site starten](../launch/overview.md)

### Samenvoegen tot algemene stramien

Duw altijd een exemplaar van de productiecode aan Globaal `master` voor het geval er een opkomende behoefte is om het productiemilieu te zuiveren zonder de diensten te onderbreken.

Maak **&#x200B;**&#x200B;geen tak van Globaal `master`. Gebruik de `integration` -vertakking om nieuwe, actieve vertakkingen te maken voor ontwikkeling en oplossingen.
