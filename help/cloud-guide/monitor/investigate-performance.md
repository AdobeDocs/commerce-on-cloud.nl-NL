---
title: New Relic-bewaking
description: Leer hoe u toegang krijgt tot uw New Relic-dashboard en hoe u gegevens van uw Adobe Commerce analyseert over het infrastructuurproject in de cloud.
feature: Cloud, Observability
topic: Performance
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# New Relic-bewaking

New Relic maakt verbinding met en controleert uw infrastructuur en [!DNL Commerce] -toepassing met behulp van PHP-agents. Nadat een Cloud-omgeving verbinding heeft gemaakt met New Relic, kunt u zich aanmelden bij uw New Relic-account om de gegevens te bekijken die door de agent zijn verzameld.

Op de _APM &amp; de pagina van de Diensten_, selecteer **Samenvatting** om transactionele informatie over uw toepassing te bekijken. Met deze weergave kunt u mogelijke fouten opsporen en de algemene status van uw toepassing en services controleren.

![ het overzichtspagina van New Relic van het project van de Wolk ](../../assets/new-relic/dashboard.png)

Vanuit deze weergave kunt u transacties volgen die trage reacties of knelpunten, de doorvoer van toepassingen, webfouten en nog veel meer veroorzaken.

Bijgehouden gegevens controleren:

- **het meest tijdrovende** - bepaal tijdconsumptie door verzoeken parallel te volgen. U hebt bijvoorbeeld de hoogste transactietijd in product- en categorieweergaven doorgebracht. Als een pagina van de klantenrekening plotseling hoog in tijdconsumptie rangschikt, zou uw toepassing door een vraag of vraag-slepende prestaties kunnen worden beïnvloed.

- **Hoogste productie** - identificeer pagina&#39;s het meest gebaseerd op de grootte en de frequentie van overgebrachte bytes.

Alle verzamelde gegevensdetails de tijd die aan acties wordt doorgebracht die gegevens, vragen, of _doorgeven_ gegevens. Als query&#39;s problemen veroorzaken, geeft New Relic informatie om deze problemen te volgen en erop te reageren.

>[!TIP]
>
>Voor details bij het gebruiken van dit gegeven om de kwesties van toepassingsprestaties problemen op te lossen, zie [ prestaties problemen oplossen gebruikend New Relic ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-performance-using-new-relic-on-magento-commerce.html) in het _Centrum van de Hulp van Adobe Commerce_.

## Prestaties bewaken met beheerde waarschuwingen

De Adobe verstrekt _Beheerde Alarm voor Adobe Commerce_ waakzaam beleid om prestatiesmetriek te volgen. Het beleid omvat een inzameling van alarm dat drempels plaatst en waarschuwing en kritieke berichten teweegbrengt wanneer de infrastructuur of de toepassingskwesties plaatsprestaties beïnvloeden. Het beleid volgt de volgende metriek op de milieu&#39;s van de Productie:

| Metrisch | Gegevensverzameling | Beschikbaarheid |
|:-------------------|:----------------|:----------------|
| [!DNL Apdex] score | APM | Pro en Starter |
| CPU-gebruik | NRI | Pro |
| Schijfruimte | NRI | Pro |
| Foutfrequentie | APM | Pro en Starter |
| Geheugengebruik | NRI | Pro |
| MariaDB-query laden | NRI | Pro |
| Herdis-geheugen | NRI | Pro |

Wanneer de infrastructuur of de toepassingsvoorwaarden van de plaats een waakzame drempel teweegbrengen, verzendt New Relic waakzame berichten zodat u de kwestie kunt proactief behandelen. Zie [ Beheerde Alarm voor Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) in het _Centrum van de Hulp van Adobe Commerce_ voor details over waakzame drempels en het oplossen van problemenstappen om de kwesties op te lossen die de waakzaamheid teweegbrachten.

>[!TIP]
>
>Voor Pro het Staging en integratie milieu&#39;s en de milieu&#39;s van de Aanzet, gebruik [ de berichten van de Gezondheid ](../integrations/health-notifications.md) om schijfruimte te controleren.

>[!PREREQUISITES]
>
>- **de geloofsbrieven van New Relic** - geloofsbrieven aan login aan de rekening van New Relic voor uw project van de Wolk
>- **Actieve integratie van New Relic** - verifieer dat uw milieu van de Wolk met New Relic wordt verbonden
>- **het bericht van het Werkschema** - vorm minstens één [ werkschema ](#set-up-a-workflow-for-notifications) om de waakzame berichten te ontvangen

**om de Beheerde Alarm voor het beleid van Adobe Commerce te herzien**:

1. Login aan uw [ rekening van New Relic ](https://login.newrelic.com/login).

1. Bepaal de plaats van _Beheerde Alarm voor het beleid van Adobe Commerce_:

   - Klik in het navigatiemenu Verkenner op **[!UICONTROL Alerts & AI]** .

   - Onder _ontdekken_, klik **[!UICONTROL Alert Conditions & Policies]**.

   - Verifieer dat uw Rekening bij de bovenkant van de _Waakzame Voorwaarden &amp; van het Beleid_ mening wordt geselecteerd.

   - In de _lijst van het Beleid_, uitgezochte **Beheerde Alarm voor het beleid van Adobe Commerce**.

     ![ Gegenereerd waakzaam beleid ](../../assets/new-relic/managed-alerts-policy.png)

     >[!NOTE]
     >
     >Als het _Beheerde Alarm voor het beleid van Adobe Commerce_ niet beschikbaar is, zie [ Beheerde Alarm voor Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce.html) in het _Centrum van de Hulp van Adobe Commerce_.

1. Klik op het tabblad **[!UICONTROL Alert conditions]** om de waarschuwingsvoorwaarden te bekijken die in het beleid zijn gedefinieerd.

## Waarschuwingsbeleid maken

Wijzig geen waarschuwingen die zijn opgenomen in het beleid Beheerde waarschuwingen voor Adobe Commerce. De Adobe werkt en verbetert de waakzame voorwaarden in dit beleid in tijd bij, dat om het even welke aanpassingen beschrijft u aan het beleid toevoegt.

In plaats van een bestaande waarschuwing te wijzigen, kunt u een waarschuwingsbeleid maken. Kopieer vervolgens de waarschuwingsvoorwaarden naar het nieuwe beleid.

>[!TIP]
>
>Zie [ Inleiding aan alarm ](https://docs.newrelic.com/docs/alerts/overview/) in _New Relic_ documentatie voor meer gedetailleerde informatie over Alarm, waakzaam beleid, en werkschema&#39;s.

## Een workflow voor meldingen instellen

U kunt opstelling a _werkschema_, vroeger genoemd een berichtkanaal, nu oprichten om berichten over uw plaatsprestaties te ontvangen die op gefiltreerde gegevens, zoals een waakzaam beleid worden gebaseerd. Meldingen over prestatieproblemen gaan naar alle workflows die aan een waarschuwingsbeleid zijn gekoppeld wanneer de voorwaarden van de toepassing of infrastructuur een waarschuwing activeren. U ontvangt ook meldingen wanneer een probleem wordt bevestigd en gesloten.

New Relic biedt sjablonen voor het configureren van verschillende typen workflowmeldingen, zoals e-mail, Slack, PagerDuty, webhooks en meer.

**om een werkschema** te vormen:

1. Login aan uw [ rekening van New Relic ](https://login.newrelic.com/login).

1. Maak een workflow.

   - Klik in het navigatiemenu Verkenner op **[!UICONTROL Alerts & AI]** .

   - In de linkernavigatie onder _verrijkt &amp; meldt_, klik **[!UICONTROL Workflows]**.

   - Klik op **[!UICONTROL Add a workflow]** aan de rechterkant.

     ![ New Relic voegt een werkschema ](../../assets/new-relic/add-a-workflow.png) toe

   - Voor _vorm uw werkschema_ pagina, ga een naam voor het werkschema in.

   - In de _gegevens van de Filter_ sectie, selecteer **[!UICONTROL Managed Alerts for Adobe Commerce]** van de **[!UICONTROL Policy]** drop-down lijst.

   - In _maak_ sectie op, selecteer een kanaal en volg de instructies.

   - Klik op **[!UICONTROL Test workflow]** om uw configuratie te verifiëren.

1. Klik op **[!UICONTROL Activate workflow]**.

Zie de documentatie van New Relic over [ Werkschema&#39;s ](https://docs.newrelic.com/docs/alerts-applied-intelligence/applied-intelligence/incident-workflows/incident-workflows/).

>[!WARNING]
>
>De waarschuwingen in het beleid Beheerde waarschuwingen voor Adobe Commerce hebben standaardworkflows die zijn geconfigureerd om Adobe-teams die Adobe Commerce ondersteunen op klanten van cloudinfrastructuren op de hoogte te brengen. Wijzig niet de configuratie voor deze standaardkanalen, en verwijder geen waakzaam beleid dat aan hen wordt toegewezen.
