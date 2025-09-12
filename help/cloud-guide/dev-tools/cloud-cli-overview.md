---
title: Cloud CLI
description: Leer meer over de magento-cloud CLI en hoe u hiermee lokale ontwikkelomgevingen voor uw Adobe Commerce kunt beheren op het infrastructuurproject voor de cloud.
exl-id: 71a705f2-8672-4125-b539-b7b1621f2f64
source-git-commit: 82d89f442792baec995dd0be40f2a49cba168f76
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Cloud CLI

`magento-cloud` CLI is een bevel-lijn hulpmiddel dat ontwikkelaars en systeembeheerders toelaat om Adobe Commerce op de projecten en milieu&#39;s van de wolkeninfrastructuur van hun lokaal werkstation te beheren.

Dit hulpmiddel breidt de functionaliteit van [[!DNL Cloud Console]](../../get-started/cloud-console.md) uit door extra automatiseringsmogelijkheden en directe toegang tot de eigenschappen van het projectbeheer te verstrekken. Nadat u het programma lokaal hebt geïnstalleerd, kunt u het gebruiken voor het beheren van de integratie-omgevingen van zowel Starter als Pro.

>[!NOTE]
>
>Dit is een lokaal hulpmiddel en wordt alleen ondersteund op Unix-gebaseerde besturingssystemen. Windows wordt niet ondersteund. Deze kan niet worden geïnstalleerd in de cloud-omgeving (alleen-lezen) met de methode die op deze pagina wordt beschreven. U kunt modules op het milieu van de Wolk door één van de volgende **plaatsingswerkschema&#39;s** slechts installeren.
>
>- [ Pro plaatsingswerkschema ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/pro-develop-deploy-workflow#deployment-workflow)
>- [ de plaatsingswerkschema van de Aanzet ](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/starter-develop-deploy-workflow)

**om `magento-cloud` CLI** te installeren:

1. Op uw _lokale werkstation_, verandering in de folder waar u van plan bent het project van de Wolk te klonen en waar de [ eigenaar van het dossiersysteem ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html) _heeft schrijven_ toegang.

1. Installeer de `magento-cloud` CLI.

   ```bash
   curl -sS https://accounts.magento.cloud/cli/installer | php
   ```

1. Voeg `magento-cloud` CLI aan het basisprofiel toe.

   ```bash
   export PATH=$PATH:$HOME/.magento-cloud/bin
   ```

1. Laad het bijgewerkte basisprofiel opnieuw.

   ```bash
   . ~/.bash_profile
   ```

1. Als u de CLI wilt starten, roept u `magento-cloud` aan en voert u de referenties van uw Cloud-account in wanneer u hierom wordt gevraagd.

   ```bash
   magento-cloud
   ```

   ```
   Welcome to Magento Cloud!
   Please log in using your Magento Cloud account.
   Your email address or username:
   ```

1. Controleer of de opdracht `magento-cloud` zich in het pad bevindt. In het volgende voorbeeld worden de beschikbare opdrachten weergegeven.

   ```bash
   magento-cloud list
   ```

## Algemene opdrachten

Adobe heeft deze opdrachten ontworpen om omgevingen voor cloudintegratie te beheren en raadt u aan de CLI van `magento-cloud` uit te voeren vanuit een projectmap zodat u de parameter `-p <project-ID>` kunt weglaten.

De volgende lijst met veelgebruikte `magento-cloud` CLI-opdrachten bevat alleen de vereiste opties. U kunt de optie `--help` met elke opdracht gebruiken om meer informatie weer te geven.

| Opdracht | Beschrijving |
| ------------------------------------ | -------------------------------------------------- |
| `magento-cloud login` | Meld u aan bij het project. |
| `magento-cloud list` | Maak een lijst van de beschikbare bevelen voor CLI hulpmiddel. |
| `magento-cloud environment:list` | Maak een lijst van de milieu&#39;s in het huidige project. |
| `magento-cloud environment:checkout` | Ontdek een bestaande omgeving. |
| `magento-cloud environment:merge -e` | Wijzigingen in deze omgeving samenvoegen met het bovenliggende element. |
| `magento-cloud variables` | Variabelen weergeven in deze omgeving. |
| `magento-cloud ssh` | Gebruik SSH om verbinding te maken met de externe omgeving. |
| `magento-cloud url` | Open de Adobe Commerce storefront in een browser. |
| `magento-cloud web` | Open de lus [!DNL Cloud Console] . |

## Omgeving, opdrachten

De milieu _naam_ is verschillend van milieu _identiteitskaart_ slechts als u ruimten of hoofdbrieven in de milieunaam gebruikt. Een milieu-id bestaat uit alle kleine letters, getallen en toegestane symbolen. Hoofdletters in een omgevingsnaam worden omgezet in kleine letters in de id. Spaties in een omgevingsnaam worden omgezet in streepjes.

Een milieu naam _kan_ geen karakters omvatten die voor uw shell van Linux of voor regelmatige uitdrukkingen worden gereserveerd. De verboden karakters omvatten krullende steunen (`{ }`), haakjes, asterisk (`*`), punthaakjes (`< >`), en het en (`&`), percenten (`%`), en andere karakters.

De opdracht `magento-cloud environment:list` geeft omgevingshiërarchieën weer, maar `git branch` niet. Als u een geneste omgeving hebt, gebruikt u het volgende:

```bash
magento-cloud environment:list
```

### Omgeving opnieuw implementeren

Trigger een herplaatsing zonder een duw te gebruiken. Controleer en bevestig de omgeving die opnieuw moet worden geïmplementeerd. Gebruik geen hergroepering als er een bouwstijl in een hangende staat is.

```bash
magento-cloud environment:redeploy
```

Monsterrespons:

```
Are you sure you want to redeploy the environment <environment-name>? [Y/n]
```

{{redeploy-warning}}

## Opdrachten Git

Het kan zijn dat sommige van deze opdrachten lijken op de opdrachten bij Git. De opdrachten van `magento-cloud` maken rechtstreeks verbinding met het op Git gebaseerde Cloud-project met extra functies. Als u een vertakking maakt zonder de CLI van `magento-cloud` te gebruiken, wordt deze niet geactiveerd en wordt deze niet automatisch gegenereerd wanneer u wijzigingen in de externe omgeving aanbrengt. De opdracht `magento-cloud` CLI bevat activering.

Als u een vertakking wilt maken, gebruikt u de opdracht `magento-cloud` , zodat de vertakking wordt geactiveerd.

```bash
magento-cloud environment:branch <new-name> <parent-branch>
```

Voor de status van een vertakking:

- Gebruik de opdracht `magento-cloud env` om een lijst weer te geven met de vertakkingen van de omgeving en hun status: actief of inactief.
- Gebruik de opdracht `magento-cloud environment:activate` om een omgevingsvertakking te activeren.

Druk op een lege Git om een implementatie te activeren. Bijvoorbeeld:

```bash
git commit --allow-empty -m "redeploy" && git push <branch-name>
```

Sommige acties, zoals het toevoegen van een gebruiker, resulteren niet in plaatsing.

### Een omgevingsvertakking maken

De volgende stappen tonen het gebruiken van CLI en van het Git bevelen onderling verwisselbaar aan om uw lokale milieu te beheren:

1. Wijzig op uw lokale werkstation de projectmap.

1. Schakelaar aan de [ eigenaar van het dossiersysteem ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html).

1. Meld u aan bij uw project.

   ```bash
   magento-cloud login
   ```

1. Maak een lijst van uw projecten.

   ```bash
   magento-cloud project:list
   ```

1. Maak een lijst van milieu&#39;s in het project. Elke omgeving bevat een actieve Git-vertakking die uw code, database, omgevingsvariabelen, configuraties en services bevat.

   ```bash
   magento-cloud environment:list
   ```

   >[!NOTE]
   >
   >Het is belangrijk dat u de opdracht `magento-cloud environment:list` gebruikt, omdat deze omgevingshiërarchieën weergeeft, maar de opdracht `git branch` niet.

1. Zoek de laatste code naar de vertakkingen van de oorsprong.

   ```bash
   git fetch origin
   ```

1. Uitchecken of overschakelen naar een specifieke vertakking en omgeving.

   ```bash
   magento-cloud environment:checkout <environment-ID>
   ```

   Met Git-opdrachten kunt u alleen de Git-vertakking uitchecken. De opdracht `magento-cloud checkout` checkt de vertakking uit en schakelt over naar de actieve omgeving.

   >[!TIP]
   >
   >U kunt een omgevingsvertakking maken met de opdrachtsyntaxis `magento-cloud environment:branch <environment-name> <parent-environment-ID>` . Het kan enige extra tijd duren om een omgevingsvertakking te maken en te activeren.

1. Gebruik de milieu-id om bijgewerkte code aan uw lokale computer te trekken. Dit is niet nodig als de omgevingsvertakking nieuw is.

   ```bash
   git pull origin <environment-ID>
   ```

1. (_Facultatieve_) creeer a [ momentopname ](../storage/snapshots.md) van het milieu als steun.

   ```bash
   magento-cloud snapshot:create -e <environment-ID>
   ```

## CLI bijwerken

De CLI van `magento-cloud` controleert op beschikbare updates wanneer u login, maar u kunt op updates controleren gebruikend het `self:update` bevel. Als er een update beschikbaar is, volg de instructies om CLI bij te werken.

Als uw `magento-cloud` CLI bijgewerkt is, ziet u de volgende reactie:

```bash
magento-cloud update
```

```
Checking for Magento Cloud CLI updates (current version: X.XX.X)
No updates found
```
