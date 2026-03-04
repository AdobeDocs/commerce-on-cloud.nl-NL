---
title: ADMIN-variabelen
description: Zie een lijst met omgevingsvariabelen die worden gebruikt bij de installatie van Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
exl-id: d2746185-bc59-4d30-a088-73df1bd2c0b2
source-git-commit: 4e751f02b92f954cd41d5523237da295a068661a
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 0%

---

# Beheerdersvariabelen

De gebruikers die administratieve toegang tot Adobe Commerce op het project van de wolkeninfrastructuur hebben kunnen de volgende variabelen van het projectmilieu gebruiken om de configuratiemontages voor de administratieve gebruikersrekening met voeten te treden om tot Admin UI toegang te hebben.

## Beheerdersreferenties

U kunt de aanmeldingsgegevens van Admin-gebruikers tijdens de Commerce-installatie overschrijven met de ADMIN-variabelen in de volgende tabel.

Als u de waarden na installatie wilt veranderen, verbind met uw milieu gebruikend SSH en gebruik het [`admin:user` bevel ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) van Adobe Commerce CLI om de Admin gebruikersgeloofsbrieven tot stand te brengen of uit te geven.

| Variabele | Standaard | Beschrijving |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | E-mailadres eigenaar licentie | Een gebruikersnaam voor de administratieve gebruiker met de capaciteit om andere gebruikers, met inbegrip van administratieve gebruikers tot stand te brengen. |
| `ADMIN_EMAIL` |                             | E-mailadres voor de beheerder. Dit adres wordt gebruikt om meldingen voor het opnieuw instellen van wachtwoorden te verzenden. |
| `ADMIN_PASSWORD` |                             | Wachtwoord voor de administratieve gebruiker. Wanneer het project wordt gecreeerd, wordt een willekeurig wachtwoord geproduceerd en een e-mail verzonden naar de Eigenaar van de Vergunning. Tijdens het maken van een project had de eigenaar van de licentie het wachtwoord al moeten wijzigen. Neem contact op met de eigenaar van de licentie voor het bijgewerkte wachtwoord. |
| `ADMIN_LOCALE` | `en_US` | De standaardlandinstelling die door de beheerder wordt gebruikt. |

## URL van beheerder

Gebruik de volgende omgevingsvariabele om de toegang tot uw beheerinterface te beveiligen. Indien opgegeven, overschrijft deze waarde de standaard-URL tijdens de installatie. In [!DNL Adobe Commerce] op cloudinfrastructuur moet u de URL voor het beheer instellen of wijzigen met de variabele `ADMIN_URL` in de map ([!DNL Cloud Console] of [!DNL Cloud CLI]). Het wijzigen van de instelling in [!DNL Admin] is alleen van toepassing op installaties op locatie.

`ADMIN_URL` - De relatieve URL voor toegang tot de beheerinterface. De standaard-URL is `/admin` .

### De URL van de beheerder wijzigen

Door gebrek, wordt [ Commerce Admin ](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/admin.html) URL geplaatst aan *&lt;domain_name>/admin*. Om veiligheidsredenen raadt Adobe aan om de URL te wijzigen in een unieke, aangepaste Admin-URL die niet gemakkelijk te raden is.

**in [!DNL Adobe Commerce] op wolkeninfrastructuur**, moet u Admin URL veranderen gebruikend de `ADMIN_URL` omgevingsvariabele in ([!DNL Cloud Console] of [!DNL Cloud CLI]). Het wijzigen van de instelling in [!DNL Admin] is alleen van toepassing op installaties op locatie. Voor installaties op-gebouw, volg [ gebruik een douane admin URL ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html#use-a-custom-admin-url).

Adobe raadt u aan de variabele op milieuniveau voor Admin URL na installatie te wijzigen. Configureer deze instelling om beveiligingsredenen voordat u vertakt vanuit de gekloonde `master` -omgeving. Alle vertakkingen die zijn gemaakt in de `master` -vertakking overerven de variabelen op milieuniveau en de bijbehorende waarden, tenzij u de overerving instelt op false.

Gebruik [!DNL Cloud Console] of [!DNL Cloud CLI] om `ADMIN_URL` in te stellen of bij te werken.

#### Optie A: Wijzig de URL van de beheerder met de [!DNL Cloud Console]

##### Integratieomgeving

Van de [ Console van de Wolk ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html), voeg een nieuwe variabele met toe:

- **Naam:** `ADMIN_URL`
- **Waarde:** Uw nieuwe Admin URL (bijvoorbeeld, `magento_A8v10`)

- Voor gedetailleerde stappen, zie [ milieuvariabelen ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/project/overview.html#configure-environment) of [ milieuvariabelen ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-admin.html) in onze ontwikkelaarsdocumentatie toevoegen.

##### Stel de URL van de beheerder in in de [!DNL Cloud Console]

1. Login aan de [ Console van de Wolk ](https://console.adobecommerce.com/).
2. Selecteer een project in de lijst **[!UICONTROL All projects]** .
3. In het projectoverzicht, selecteer het milieu en klik het configuratiepictogram.
4. Selecteer de tab **[!UICONTROL Variables]** .
5. Klik op **[!UICONTROL Create Variable]** (of bewerk de bestaande `ADMIN_URL` -variabele, indien aanwezig).
6. Voer het volgende in:
   - **Naam van Variabele:** `ADMIN_URL`
   - **Waarde:** Uw nieuwe weg Admin (bijvoorbeeld, `magento_A8v10`).

   Standaard zijn **[!UICONTROL Available during runtime]** en **[!UICONTROL Make inheritable]** geselecteerd. Wis **[!UICONTROL Make inheritable]** voor deze variabele om te voorkomen dat onderliggende omgevingen deze waarde overnemen.
7. Klik op **[!UICONTROL Create variable]** (of **[!UICONTROL Save]** ) en wacht tot de implementatie is voltooid. De knop is alleen zichtbaar wanneer de vereiste velden waarden bevatten.

##### Als Staging en productie niet beschikbaar zijn in de [!DNL Cloud Console]

[ voorlegt een steunkaartje ](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#submit-ticket) verzoekend om de `ADMIN_URL` variabele voor uw het Opvoeren of milieu van de Productie toe te voegen. Als het Opvoeren en de Productie van [!DNL Cloud Console] toegankelijk zijn, voeg de variabele toe zoals die in [ het milieu van de Integratie ](#integration-environment) wordt beschreven.

#### Optie B: Wijzig de URL van de beheerder met de [!DNL Cloud CLI]

Gebruik de opdracht `magento-cloud variable:update` om de variabele bij te werken. (De opdracht `variable:set` is vervangen en is niet beschikbaar.)

In het volgende voorbeeld wordt de `master` omgeving `ADMIN_URL` bijgewerkt naar `newAdmin_A8v10` en wordt voorkomen dat onderliggende omgevingen de waarde overnemen:

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master --inheritable false
```

- **Herplaatsing:** Veranderend de `ADMIN_URL` variabele in [!DNL Cloud CLI] brengt een herplaatsing van het milieu teweeg.
- **Overerving:** de Variabelen zijn overerverteerbaar door gebrek. Als u wilt voorkomen dat de waarde wordt overgeërfd door onderliggende omgevingen, gebruikt u de optie `--inheritable false` zoals weergegeven. Voor meer detail, zie [ veranderlijk niveauzicht ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/variable-levels.html#visibility).

>[!NOTE]
>
>De `ADMIN_URL` -waarde accepteert letters (a-z, A-Z), getallen (0-9) en het onderstrepingsteken (_). Spaties of andere tekens worden niet geaccepteerd.
