---
title: ADMIN-variabelen
description: Zie een lijst met omgevingsvariabelen die worden gebruikt bij de installatie van Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Beheerdersvariabelen

De gebruikers die administratieve toegang tot Adobe Commerce op het project van de wolkeninfrastructuur hebben kunnen de volgende variabelen van het projectmilieu gebruiken om de configuratiemontages voor de administratieve gebruikersrekening met voeten te treden om tot Admin UI toegang te hebben.

## Beheerdersreferenties

U kunt de aanmeldingsgegevens van Admin-gebruikers tijdens de Commerce-installatie overschrijven met de ADMIN-variabelen in de volgende tabel.

Als u de waarden na installatie wilt veranderen, verbind met uw milieu gebruikend SSH en gebruik het [`admin:user` bevel ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html?lang=nl-NL) van Adobe Commerce CLI om de Admin gebruikersgeloofsbrieven tot stand te brengen of uit te geven.

| Variabele | Standaard | Beschrijving |
| -------------- | --------------------------- | ----------- |
| `ADMIN_USERNAME` | E-mailadres eigenaar licentie | Een gebruikersnaam voor de administratieve gebruiker met de capaciteit om andere gebruikers, met inbegrip van administratieve gebruikers tot stand te brengen. |
| `ADMIN_EMAIL` |                             | E-mailadres voor de beheerder. Dit adres wordt gebruikt om meldingen voor het opnieuw instellen van wachtwoorden te verzenden. |
| `ADMIN_PASSWORD` |                             | Wachtwoord voor de administratieve gebruiker. Wanneer het project wordt gecreeerd, wordt een willekeurig wachtwoord geproduceerd en een e-mail verzonden naar de Eigenaar van de Vergunning. Tijdens het maken van een project had de eigenaar van de licentie het wachtwoord al moeten wijzigen. Neem contact op met de eigenaar van de licentie voor het bijgewerkte wachtwoord. |
| `ADMIN_LOCALE` | `en_US` | De standaardlandinstelling die door de beheerder wordt gebruikt. |

## URL van beheerder

Gebruik de volgende omgevingsvariabele om de toegang tot uw beheerinterface te beveiligen. Indien opgegeven, overschrijft deze waarde de standaard-URL tijdens de installatie.

`ADMIN_URL` - De relatieve URL voor toegang tot de beheerinterface. De standaard-URL is `/admin` . Om veiligheidsredenen raadt de Adobe u aan de standaardinstelling te wijzigen in een unieke, aangepaste Admin-URL die niet gemakkelijk te raden is.

### De URL van de beheerder wijzigen

Adobe raadt u aan de variabele op milieuniveau voor de URL van Admin na installatie te wijzigen. Configureer deze instelling om beveiligingsredenen voordat u vertakt vanuit de gekloonde `master` -omgeving. Alle vertakkingen die zijn gemaakt in de `master` -vertakking overerven de variabelen op milieuniveau en de bijbehorende waarden.

Gebruik de opdracht `magento-cloud variable:update` om de waarde van de variabele bij te werken. (De opdracht `variable:set` is vervangen en is niet beschikbaar.) In het volgende voorbeeld wordt ADMIN_URL bijgewerkt naar `newAdmin_A8v10` :

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master
```

>[!NOTE]
>
>De `ADMIN_URL` -waarde accepteert letters (a-z of A-Z), getallen (0-9) en het onderstrepingsteken (_) voor een aangepast beheerpad. De ruimten of andere karakters worden **niet** toegelaten.

**om URL te veranderen gebruikend[!DNL Cloud Console]**:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. In het projectoverzicht, selecteer het milieu en klik het configuratiepictogram.

   ![ de configuratie van het Project ](../../assets/icon-configure.png){width="36"}

1. Selecteer de **Variabelen** tabel.

1. Klik **creëren Variabele**.

1. Voer het volgende in:

   - **Veranderlijke naam** = `ADMIN_URL`
   - **waarde** = Nieuwe URL. Stel bijvoorbeeld de URL voor beheer in op `magento_A8v10` .

   Standaard zijn `Available during runtime` en `Make inheritable` geselecteerd.

1. Klik **creeer variabele** en wacht tot de plaatsing voltooit. Deze knop is alleen zichtbaar wanneer de vereiste velden waarden bevatten.
