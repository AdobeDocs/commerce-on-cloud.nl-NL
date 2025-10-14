---
title: Gezondheidsmeldingen
description: Leer hoe u Slack-, e-mail- en PagerDuty-meldingen voor gebruik van schijfruimte op uw Adobe Commerce configureert voor een cloud-infrastructuurproject.
feature: Cloud, Observability, Integration
exl-id: 5a7f37e9-e8f9-4b6b-b628-60dcaa60cc64
source-git-commit: c3c708656e3d79c0893d1c02e60dcdf2ad8d7c7c
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Gezondheidsmeldingen

Adobe Commerce on cloud Infrastructure bewaakt het gebruik van schijfruimte voor alle toepassingen en services in uw Starter-omgeving of uw Pro-integratieomgeving. Een databaseschijf die onvoldoende ruimte heeft, kan gegevensbeschadiging veroorzaken. De statuscontrole vindt elke 5 minuten plaats en kan u via e-mail of een andere externe service op de hoogte stellen. Er zijn drie waarschuwingen op een lage schijf voor gezondheidsmeldingen:

- **Waarschuwing** - de beschikbare daling van de schijfruimte onder 20%
- **Kritieke** - beschikbare daling van de schijfruimte onder 10%
- **allen-duidelijk** - de beschikbare schijfruimtewinst boven 20%, na een laag-schijfgebeurtenis

>[!NOTE]
>
>In een Pro Production-omgeving kunt u de Beheerde waarschuwingen voor het Adobe Commerce-waarschuwingsbeleid voor New Relic gebruiken om schijfruimte te controleren. Zie [&#x200B; prestaties van de Monitor met Beheerde Alarm &#x200B;](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

## E-mailmeldingen

Voor de integratie van e-mailberichten over de gezondheid is een adres van oorsprong en ten minste één adres van de ontvanger vereist. U kunt hetzelfde e-mailadres gebruiken voor het adres `from-address` en `recipients` . In het volgende voorbeeld wordt een integratie van een e-mail met de status geregistreerd met twee ontvangers:

```bash
magento-cloud integration:add --type health.email --from-address you@example.com --recipients them@example.com --recipients others@example.com
```

## Slack-kanaalmeldingen

Slack is een externe service die interactieve apps, bots genaamd, gebruikt om berichten in een chatroom te posten. Alvorens u gezondheidsberichten in Slack kunt ontvangen, moet u een douane [&#x200B; allebei gebruiker &#x200B;](https://api.slack.com/bot-users) voor uw groep van Slack tot stand brengen. Nadat u de beide gebruiker voor uw kanaal, of kanalen vormt, sparen het [&#x200B; bot teken &#x200B;](https://api.slack.com/docs/token-types#bot) dat door Slack wordt verstrekt om uw integratie te registreren. In het volgende voorbeeld worden gezondheidsmeldingen geregistreerd in een Slack-kanaal:

```bash
magento-cloud integration:add --type health.slack --token SLACK_BOT_TOKEN --channel '#slack-channel-name'
```

## PagerDuty-meldingen

PagerDuty is een externe dienst die teamleden op vraag van belangrijke kwesties kan op de hoogte brengen. Alvorens u gezondheidsberichten in PagerDuty kunt ontvangen, moet u de integratie van a [&#x200B; PagerDuty &#x200B;](https://developer.pagerduty.com/v2/docs/integrating) tot stand brengen die de versie 2 van de Gebeurtenissen API gebruikt. Gebruik de integratiesleutel, of _die sleutel_ verplettert, om uw integratie te registreren. Het volgende voorbeeld registreert berichten voor PagerDuty gebruikend een verpletterende sleutel:

```bash
magento-cloud integration:add --type health.pagerduty --routing-key PAGERDUTY_ROUTING_KEY
```

## Logbeheer

Als u meer beschikbare schijfruimte wilt, kunt u logbestanden afkappen of verwijderen uit uw omgeving. Als logrotate wordt toegelaten, download eerst een reserveexemplaar van het logboeken, dan verwijder hen:

```bash
rm -rf some-log-file.log.gz
```

U kunt ook afzonderlijke logbestanden afkappen om de bestandsgrootte te verkleinen. Voor een gedetailleerd voorbeeld van logboekdossierbeknotting, zie de videoleerprogramma&#39;s van de Boomstam van het Logboek van de Boomstam {target="_blank"}.
