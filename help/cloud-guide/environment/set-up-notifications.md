---
title: Meldingen instellen
description: Leer hoe u meldingen voor Adobe Commerce configureert in omgevingen met cloudinfrastructuren.
feature: Cloud, Configuration, Logs
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Meldingen instellen

Standaard schrijft Adobe Commerce op de cloud-infrastructuur acties voor het maken en implementeren van acties naar het `app/var/log/cloud.log` -bestand in de Adobe Commerce-hoofdmap van de toepassing. U kunt logbestanden ook naar een berichtensysteem verzenden, zoals Slack en e-mail, voor het ontvangen van realtime berichten.

Bijvoorbeeld, kon u een bericht van de Slack verzenden om een groep mensen te waarschuwen wanneer een plaatsing ontbreekt, en een onderzoek naar te veroorzaken wat verkeerd ging.

## Abonnementen

Overweeg het volgende voordat u meldingen configureert:

- Welk soort berichten wilt u ontvangen (Slack berichten, e-mail, allebei)?
- Hoeveel detail wilt u in de logboeken zien?
- Waar wilt u meldingen instellen (Integratie, Staging, Productie)?

Bijvoorbeeld, tijdens aanvankelijke ontwikkeling kunt u e-mailberichten verkiezen die gedetailleerde logboeken over uw integratiemilieu tonen om u te helpen kwesties zuiveren alvorens aan het Staging milieu op te stellen. Wanneer u bereid bent om aan het het Opvoeren of milieu van de Productie op te stellen, kunt u een bericht van de Slack verkiezen dat minder gedetailleerde informatie bevat.

>[!NOTE]
>
>Het configuratiedossier dat aan opstellingsberichten wordt gebruikt is bij de wortel van uw projectfolder, zodat is het van toepassing wanneer u veranderingen in om het even welk milieu duwt. Als u meldingen per omgeving wilt aanpassen, moet u het configuratiebestand wijzigen voordat u het naar die omgeving duwt.

## Meldingen configureren

Meldingen configureren:

1. Wijzig op uw lokale werkstation de projectmap.
1. In het `.magento.env.yaml` dossier in uw projectwortel, voeg uw montages van het overseinensysteem, met inbegrip van aangewezen bericht [ niveaus van het Logboek ](log-handlers.md#log-levels) toe.

   Bijvoorbeeld, om zowel Slack _als_ e-mailconfiguraties te vormen, gebruik het volgende:

   ```yaml
   log:
     slack:
       token: "<your-slack-token>"
       channel: "<your-slack-channel>"
       username: "SlackHandler"
       min_level: "info"
     email:
       to: <your-email>
       from: <your-email>
       subject: "Log notification from Adobe Commerce"
       min_level: "notice"
   ```

   >[!NOTE]
   >
   >Adobe Commerce on cloud Infrastructure verzendt alleen e-mailberichten tijdens de implementatiefase.

1. Leg uw wijzigingen vast en duw deze op de externe server.

   ```bash
   git -A && git commit -m "Configure build/deploy notifications"
   ```

   ```bash
   git push origin <branch-name>
   ```

### Voorbeeldconfiguratie van Slack

Het volgende voorbeeld toont een Slack-enige configuratie:

```yaml
log:
  slack:
    token: "<your-slack-token>"
    channel: "<your-slack-channel>"
    username: "SlackHandler"
    min_level: "info"
```

- `token` - Uw Slack [ gebruikerstoken ](https://api.slack.com/docs/token-types#user). Met uw gebruikerstoken wordt Adobe Commerce op de cloudinfrastructuur gemachtigd om berichten te verzenden.
- `channel` - Naam van het kanaal Adobe Commerce van de Slack op wolkeninfrastructuur verzendt berichten.
- `username`—Gebruikersnaam Adobe Commerce op cloudinfrastructuur gebruikt om berichtberichten in Slack te verzenden.
- `min_level` - Min logniveau voor berichtberichten. We raden u aan `info` te gebruiken.

### Voorbeeld-e-mailconfiguratie

In het volgende voorbeeld ziet u een configuratie die alleen via e-mail kan worden gebruikt:

>[!NOTE]
>
>Adobe Commerce on cloud Infrastructure verzendt alleen e-mailberichten tijdens de implementatiefase.

```yaml
log:
  email:
    to: <your-email>
    from: <your-email>
    subject: "Log notification from Adobe Commerce"
    min_level: "notice"
```

- `to` - Het e-mailadres Adobe Commerce op de cloudinfrastructuur verzendt meldingen.
- `from` - E-mailadres voor het verzenden van berichtberichten aan ontvangers.
- `subject` - Beschrijving van het e-mailbericht.
- `min_level` - Min logniveau voor berichtberichten. We raden u aan `notice` of `warning` te gebruiken.
