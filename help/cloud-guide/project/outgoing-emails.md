---
title: Uitgaande e-mails configureren
description: Leer hoe u uitgaande e-mails voor Adobe Commerce kunt inschakelen voor cloudinfrastructuur.
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Uitgaande e-mails configureren

U kunt uitgaande e-mailberichten voor integratie (en het opvoeren voor Starter slechts) milieu&#39;s van [!DNL Cloud Console] of van de bevellijn toelaten en onbruikbaar maken. U kunt uitgaande e-mails verzenden om tweefelige verificatie te verzenden of wachtwoorde-mails opnieuw in te stellen voor gebruikers van een Cloud-project.

Standaard zijn uitgaande e-mails ingeschakeld in Productie- en Staging-omgevingen (alleen Pro). Nochtans, kan het **[!UICONTROL Enable outgoing emails]** plaatsen gehandicapt in de milieu montages ongeacht status lijken tot u het `enable_smtp` bezit door de [ bevellijn ](#enable-emails-in-the-cli) of [ Console van de Wolk ](outgoing-emails.md#enable-emails-in-the-cloud-console) plaatst.

Het bijwerken van de `enable_smtp` bezitswaarde door [ bevellijn ](#enable-emails-in-the-cli) verandert ook de [!UICONTROL Enable outgoing emails] plaatsende waarde voor dit milieu op de Console van de Wolk.

>[!NOTE]
>
>Als u de instelling **[!UICONTROL Enable outgoing emails]** inschakelt/uitschakelt, worden e-mails in de Pro Staging- of Production-omgeving niet in- of uitgeschakeld.

{{redeploy-warning}}

## E-mails inschakelen in de Cloud Console

Gebruik **[!UICONTROL Outgoing emails]** knevel in _vormt milieu_ mening om e-mailsteun toe te laten of onbruikbaar te maken.

Als de uitgaande e-mails moeten worden onbruikbaar gemaakt of op ProProductie of het Opvoeren milieu&#39;s opnieuw worden toegelaten, kunt u een [ kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) voorleggen.

>[!TIP]
>
>De status van uitgaande e-mail wordt mogelijk niet weerspiegeld voor Pro Staging- of Production-omgevingen in de Cloud Console.

**Om e-mailsteun van[!DNL Cloud Console]** te beheren:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .
1. Selecteer een project van de _Alle projecten_ lijst.
1. Voor het dashboard van het Project, klik het configuratiepictogram in het hogere recht.
1. Klik op **[!UICONTROL Environments]** en selecteer een specifieke omgeving in de lijst (behalve Staging en Productie voor Pro).
1. Om uitgaande e-mail toe te laten of onbruikbaar te maken, knevel _uitgaande e-mail_ **** of **weg** toe.

   ![ laat uitgaande e-mailconfiguratie ](../../assets/outgoing-emails.png) toe

Nadat u het plaatsen verandert, bouwt het milieu en stelt met de nieuwe configuratie op.

## E-mails inschakelen in de CLI

U kunt de e-mailconfiguratie voor een actieve omgeving wijzigen met de opdracht `magento-cloud` CLI `environment:info` om de eigenschap `enable_smtp` in te stellen. Wanneer u SMTP inschakelt, wordt de omgevingsvariabele `MAGENTO_CLOUD_SMTP_HOST` bijgewerkt met het IP-adres van de SMTP-host voor het verzenden van e-mail.

**om e-mailsteun van de bevellijn** te beheren:

1. Wijzig op uw lokale werkstation de projectmap.

1. Controleer de instelling voor de uitgaande e-mail voor de omgeving.

   ```bash
   magento-cloud environment:info -e <environment-id> | grep enable_smtp
   ```

1. Wijzig de configuratie van de e-mailondersteuning door de omgevingsvariabele `enable_smtp` in te stellen op `true` of `false` .

   ```bash
   magento-cloud environment:info --refresh -e <environment-id> enable_smtp true
   ```

   Wacht op het milieu om te bouwen en op te stellen.

1. Gebruik SSH aan login het verre milieu.

1. Controleer of het e-mailbericht werkt. Stuur een test-e-mail naar een adres dat u kunt controleren.

   ```bash
   php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
   ```

1. Controleer of het e-mailbericht is opgehaald door SendGrid.

   ```bash
   grep mail@example.com /var/log/mail.log
   ```
