---
title: Overzicht van integratie
description: Meer informatie over integratieopties van derden voor uw Adobe Commerce-project voor cloudinfrastructuur.
role: Developer
feature: Cloud, Integration
last-substantial-update: 2024-02-06T00:00:00Z
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Overzicht van integratie

De integraties zijn nuttig voor het gebruiken van externe dienst-zulke als het ontvangen van het Git of Slack bots-en het handhaven van uw huidige ontwikkelingsprocessen, zoals het gebruiken van de functie van het trekkingsverzoek van de codeherbeoordeling in GitHub. U kunt de volgende integraties toevoegen aan uw Adobe Commerce op het project van de wolkeninfrastructuur:

![ Integraties ](/help/assets/integrations.png)

>[!BEGINTABS]

>[!TAB  CLI ]

**om een integratie toe te voegen gebruikend Cloud CLI**:

De volgende opdracht begint interactieve herinneringen om het type en de opties voor de nieuwe integratie te selecteren.

```bash
magento-cloud integration:add
```

**om van de integratie een lijst te maken die voor uw project** wordt gevormd:

```bash
magento-cloud integration:list
```

Monsterrespons:

```
+----------+--------------+---------------------------------------------------------------------------+
| ID       | Type         | Summary                                                                   |
+----------+--------------+---------------------------------------------------------------------------+
| <int-id> | bitbucket    | Repository: user/magento-int                                              |
|          |              | Hook URL:                                                                 |
|          |              | https://magento-url.cloud/api/projects/projectID/integrations/int-ID/hook |
| <int-id> | health.email | From: you@example.com                                                     |
|          |              | To: them@example.com                                                      |
+----------+--------------+---------------------------------------------------------------------------+
```

>[!TAB  Console ]

**om een integratie toe te voegen gebruikend[!DNL Cloud Console]**:

1. In _Montages van het Project_, klik **[!UICONTROL Integrations]**.

1. Klik op een integratietype of klik op **[!UICONTROL Add integration]** .

1. Stap door de van het integratietype selectie en configuratie stappen.

1. Nadat u de integratie hebt toegevoegd, wordt deze weergegeven in de lijst in de weergave Integraties.

>[!ENDTABS]

## Commerce-webhaken

U kunt de websites van Commerce in uw project van de Wolk met [ vormen ENABLE_WEBHOOKS globale variabele ](../environment/variables-global.md#enable_webhooks). Commerce-websites verzenden aanvragen naar een externe server als reactie op door Commerce gegenereerde gebeurtenissen. De [_Gids van Webhooks_ ](https://developer.adobe.com/commerce/extensibility/webhooks) beschrijft deze eigenschap in detail.

## Algemene webhaken

U kunt de infrastructuur van de Wolk en bewaarplaats gebeurtenissen vangen en melden gebruikend een integratie van de douanewebsite aan `POST` JSON berichten aan a _webhaak_ URL.

**om een webhaak URL toe te voegen, gebruik de volgende syntaxis**:

```bash
magento-cloud integration:add --type=webhook --url=https://hook-url.example.com
```

- `type` - Geef het `webhook` integratietype op.
- `url` - Geef de URL van de webhaak op die JSON-berichten kan ontvangen.

De steekproefreactie toont een reeks herinneringen die een kans bieden om de integratie aan te passen. Het gebruiken van de standaard (lege) reactie verzendt berichten over alle gebeurtenissen op alle milieu&#39;s in een project.

U kunt de integratie aanpassen om specifieke [ gebeurtenissen ](#events-to-report) te melden, zoals het duwen van code aan een tak. U kunt bijvoorbeeld de `environment.push` -gebeurtenis opgeven die een bericht verzendt wanneer een gebruiker code naar een vertakking duwt:

```
Events to report (--events)
A list of events to report, e.g. environment.push
Default: *
Enter comma-separated values (or leave this blank)
>
```

U kunt gebeurtenissen in een `pending`-, `in_progress` - of `complete` status rapporteren:

```
States to report (--states)
A list of states to report, e.g. pending, in_progress, complete
Default: complete
Enter comma-separated values (or leave this blank)
>
```

En u kunt _omvatten_ of __ berichten voor specifieke milieu&#39;s uitsluiten:

```
Included environments (--environments)
The environment IDs to include
Default: *
Enter comma-separated values (or leave this blank)
>

Excluded environments (--excluded-environments)
The environment IDs to exclude
Enter comma-separated values (or leave this blank)
>
```

Wanneer de integratie is voltooid, ontvangt u een overzicht van de waarden:

```
Created integration integration-ID (type: webhook)
+-----------------------+------------------------------+
| Property              | Value                        |
+-----------------------+------------------------------+
| id                    | integration-ID               |
| type                  | webhook                      |
| events                | - '*'                        |
| environments          | - '*'                        |
| excluded_environments | {  }                         |
| states                | - complete                   |
| url                   | https://hook-url.example.com |
+-----------------------+------------------------------+
```

### Bestaande integratie bijwerken

U kunt een bestaande integratie bijwerken. Wijzig bijvoorbeeld de staten van `complete` in `pending` met behulp van het volgende:

```bash
magento-cloud integration:update --states=pending <int-id>
```

Monsterrespons:

```
Integration integration-ID (webhook) updated
+-----------------------+------------------------------+
| Property              | Value                        |
+-----------------------+------------------------------+
| id                    | integration-ID               |
| type                  | webhook                      |
| events                | - '*'                        |
| environments          | - '*'                        |
| excluded_environments | {  }                         |
| states                | - pending                    |
| url                   | https://hook-url.example.com |
+-----------------------+------------------------------+
```

### Te rapporteren gebeurtenissen

| Gebeurtenis | Beschrijving |
| ----- | :-----------|
| `environment.access.add` | Een gebruiker heeft toegang tot het milieu |
| `environment.access.remove` | Een gebruiker is verwijderd uit de omgeving |
| `environment.activate` | Een vertakking is &quot;geactiveerd&quot; met een omgeving |
| `environment.backup` | Een gebruiker heeft een opname geactiveerd |
| `environment.branch` | Een tak is gecreeerd gebruikend de beheersconsole |
| `environment.deactivate` | Een vertakking is &quot;gedeactiveerd&quot;. De code is er nog steeds, maar het milieu is vernietigd |
| `environment.delete` | Een vertakking is verwijderd |
| `environment.initialize` | De `master` -vertakking van het project dat is geïnitialiseerd met een eerste bewerking |
| `environment.merge` | Een actieve vertakking is samengevoegd met de beheerconsole of API |
| `environment.push` | Een gebruiker heeft code naar een vertakking geduwd |
| `environment.restore` | Een gebruiker heeft een opname hersteld |
| `environment.route.create` | Een route is gecreeerd gebruikend de beheersconsole |
| `environment.route.delete` | Een route is geschrapt gebruikend de beheersconsole |
| `environment.route.update` | Een route is gewijzigd gebruikend de beheersconsole |
| `environment.subscription.update` | De omgeving van `master` is aangepast omdat het abonnement is gewijzigd, maar er zijn geen wijzigingen in de inhoud |
| `environment.synchronize` | In een omgeving zijn gegevens of code uit de bovenliggende omgeving opgehaald |
| `environment.update.http_access` | De toegangsregels van HTTP voor een milieu zijn gewijzigd |
| `environment.update.restrict_robots` | De functie voor alle robots voor blokken is in- of uitgeschakeld |
| `environment.update.smtp` | Het verzenden van e-mailberichten is in- of uitgeschakeld in een omgeving |
| `environment.variable.create` | Er is een variabele gemaakt |
| `environment.variable.delete` | Een variabele is verwijderd |
| `environment.variable.update` | Een variabele is gewijzigd |
| `project.domain.create` | Een domein is gecreeerd en aan het project toegevoegd |
| `project.domain.delete` | Een domein verbonden aan het project is verwijderd |
| `project.domain.update` | Een domein verbonden aan het project is bijgewerkt |
