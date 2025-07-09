---
title: New Relic-accountbeheer
description: Leer hoe u toegang krijgt tot uw New Relic-account en toegang, integratie en het gebruik van tools voor uw Adobe Commerce kunt beheren voor een cloud-infrastructuurproject.
feature: Cloud, Observability
role: Admin
exl-id: 7aeedd12-7a81-47eb-a82f-3079e16ecb06
source-git-commit: 5b633108f4113b26f6487073c1ccedebb632b111
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# New Relic-accountbeheer

Wanneer Adobe uw cloud-infrastructuurproject verzorgt, ontvangt de Eigenaar van de licentie een e-mail van New Relic met referenties en instructies voor toegang tot de New Relic-account. Als u het e-mailbericht niet hebt ontvangen, gebruikt u het e-mailadres van de eigenaar van de licentie om het New Relic-wachtwoord opnieuw in te stellen.

Als de Eigenaar van de Vergunning werd veranderd en de nieuwe Eigenaar van de Vergunning heeft momenteel geen toegang tot New Relic, [ voorlegt een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

## Gebruikerstoegang beheren (beheerdersrol)

>[!NOTE]
>
>Biedt alleen volledige toegang tot gebruikers die strikt toegang tot de volledige functieset vereisen.

**om tot Gebruikersbeheer in New Relic** toegang te hebben:

1. Login aan uw [ rekening van New Relic ](https://login.newrelic.com/login).

1. Selecteer uw gebruikersnaam in de navigatie linksonder.

1. Klik op **[!UICONTROL Administration]** en selecteer een van de volgende opties in de lijst:

   - **[!UICONTROL User management]** om een gebruiker toe te voegen en actieve gebruikers en uitnodigingen in behandeling te beheren.

   - **[!UICONTROL Access management]** om gebruikersgroepen, rollen en accounts te beheren.

Zie [ Gebruikersbeheer ](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) in de _New Relic_ documentatie.

## New Relic for Starter-omgeving configureren

>[!NOTE]
>
>**Pro milieu&#39;s** worden preconfigured om de diensten van New Relic te gebruiken en kunnen overslaan laat en verbindt instructies toe. Als New Relic APM niet geïnstalleerd op de het Opvoeren en van de Productie milieu&#39;s of de Infrastructuur van New Relic niet beschikbaar in het milieu van de Productie is, [ voorlegt een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) om installatie te verzoeken.

Voor Starter-omgevingen moet u het `.magento.app.yaml` -bestand controleren om te controleren of de sectie `runtime` de New Relic-extensie bevat. Als de extensie niet is geconfigureerd, voegt u het volgende toe:

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Licentiecode toepassen

Als u een Cloud-omgeving wilt verbinden met New Relic, voegt u de New Relic-licentiecode toe aan de omgeving.

- Voor **Pro projecten**, voegt Adobe de vergunningssleutel aan uw Productie en het Staging milieu&#39;s tijdens het inrichtingsproces toe. U kunt login aan uw [ rekening van New Relic ](https://login.newrelic.com/login) om connectiviteit tussen uw Adobe Commerce op de plaats van de wolkeninfrastructuur en New Relic te verifiëren.

- Voor **de projecten van de Aanzet**, hebt u een de vergunningssleutel van New Relic die tot _drie_ milieu&#39;s steunt. U moet de sleutel aan uw omgevingsconfiguraties manueel toevoegen. Starteromgevingen zijn niet vooraf ingericht voor gebruik van de New Relic-service.

Voor Starter-omgevingen schakelt u de New Relic-integratie in door de New Relic-licentiecode toe te voegen aan de omgevingsconfiguratie. Voeg de sleutel toe aan de het Staging en milieu&#39;s van de Productie en één andere milieu van uw keus. Alleen de New Relic-licentiecode is vereist voor de configuratie. U kunt informatie over extra configuratieopties in [ New Relic vinden die ](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) onderwerp in de _Gids van de Gebruiker van Adobe Commerce_ melden.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Aanmeldingsgegevens voor de Adobe Commerce-accountpagina of voor de New Relic-licentie voor uw project
>- [ Admin-vlakke toegang ](../project/user-access.md) aan de milieu&#39;s van de Aanzet om te vormen
>- De geloofsbrieven om tot [ Admin ](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) voor het milieu toegang te hebben

**om New Relic voor Startermilieu&#39;s** te vormen:

1. Zoek uw New Relic-licentiecode via de CLI van [!DNL Cloud Console] of de Cloud.

   **[!DNL Cloud Console]methode** :

   - Open uw pagina van de wolkenproject [ rekening ](https://accounts.magento.cloud/user).

   - Op het _lusje van Projecten_, vind uw project.

   - Klik **Details van de Mening** voor de informatie van de projectinfrastructuur.

   - Breid de **sectie van de Dienst van New Relic** uit om de vergunningssleutel te bekijken.

   - Kopieer de licentiecode.

   **Cloud CLI methode**:

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Voeg de New Relic-licentiecode toe aan een omgeving met behulp van de `magento-cloud` CLI.

   - Verandering in het milieu dat de vergunningssleutel vereist.
   - Werk de waarde van de variabele bij met behulp van de volgende `magento-cloud` CLI-opdracht:

     ```bash
     magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
     ```

   Naar keuze, kunt u het van [ Commerce Admin ](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store) toevoegen.

1. Login aan uw [ rekening van New Relic ](https://login.newrelic.com/login) om te verifiëren dat u gegevens van het milieu van Adobe Commerce kunt bekijken. Zie [ prestaties ](investigate-performance.md) onderzoeken.

### Licentiecode verwijderen

U kunt uw New Relic-licentiecode alleen in drie actieve omgevingen gebruiken. Als de sleutel in gebruik in drie milieu&#39;s is, moet u de sleutel uit één van de milieu&#39;s verwijderen alvorens u het aan een verschillende milieu kunt toevoegen.

**om een vergunningssleutel uit een milieu** te verwijderen:

1. Omgevingsvariabelen weergeven.

   ```bash
   magento-cloud variable:list
   ```

   Monsterrespons:

   ```
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >Als u de vergunningssleutel als a _project_ variabele toevoegde, moet u die project-vlakke variabele verwijderen. Een projectvariabele voegt de vergunning aan _toe elke_ gecreeerde milieutak, die de vergunningsgrens kan verbruiken of overschrijden. Projectvariabelen weergeven: `magento-cloud variable:list --level project`

1. Verwijder de licentievariabele.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
