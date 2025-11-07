---
title: Gebruikerstoegang beheren
description: Leer hoe u de toegang van gebruikers tot Adobe Commerce kunt beheren voor projecten en omgevingen met cloudinfrastructuur.
role: Admin
feature: Cloud, Roles/Permissions
last-substantial-update: 2023-06-27T00:00:00Z
topic: Security
exl-id: 953593de-f675-49fd-988f-f11306f67fbd
source-git-commit: c972d9f2029499cf53edc334c1d9a40b155a991d
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---

# Gebruikerstoegang beheren

Adobe Commerce-projecten voor cloudinfrastructuur maken gebruik van rolgebaseerde toegang. Er zijn twee rollen beschikbaar op het projectniveau:

- **admin van het Project** - schrijf toegang tot alle projectmilieu&#39;s en kan gebruikers, duw code, en de montages van het updateproject beheren. (vroeger gekend als **Super admin**)
- **de kijker van het Project** - mening-slechts toegang tot alle projectmilieu&#39;s.

De kijkers van het project kunnen geen taken op om het even welk milieu uitvoeren; nochtans, kunt u projectkijkers toegang tot een specifiek milieutype verlenen schrijven.

Toegang op milieuniveau is gebaseerd op het type milieu: productie, staging en ontwikkeling. Het verlenen van een gebruiker _kijker_ toestemming aan _ontwikkelings_ milieu&#39;s betekent dat zij **alle** ontwikkelomgevingen in het project kunnen bekijken. In de volgende tabel worden de mogelijkheden voor elk machtigingsniveau verduidelijkt:

| Machtigingsniveau | Toegang | SSH-toegang |
| ------------------ | ----------- | :----------: |
| **Admin** | Voer beheerderstaken uit, zoals veranderingsmontages, dupcode, voer taken, en takbeheer uit, met inbegrip van het samenvoegen met het oudermilieu | Ja |
| **Medewerker** | Code duwen en de omgeving vertakken; kan instellingen niet wijzigen of acties uitvoeren | Ja |
| **Kijker** | Alleen-weergeven toegang tot het omgevingstype | Nee |
| **Geen toegang** | Geen toegang tot het omgevingstype | Nee |

{style="table-layout:auto"}

U kunt gebruikers toevoegen en rollen toewijzen met behulp van de `magento-cloud` CLI of de [!DNL Cloud Console] .

>[!BEGINSHADEBOX]

**Eerste vereisten:**

- Een geregistreerde gebruiker bij een Adobe ID. Een gebruiker moet [&#x200B; voor een rekening van Adobe &#x200B;](https://account.adobe.com) registreren, en dan hun [&#x200B; rekening van de Wolk initialiseren &#x200B;](https://console.adobecommerce.com) door [&#x200B; https://console.adobecommerce.com &#x200B;](https://console.adobecommerce.com) te bezoeken alvorens u hen aan een project van de Wolk kunt toevoegen.
- Een gebruiker toegewezen de **Admin** rol kan gebruikers met `magento-cloud` CLI niet leiden. Slechts kunnen de gebruikers die de **rol van de Eigenaar van de 0&rbrace; Rekening worden verleend gebruikers beheren.**

>[!ENDSHADEBOX]

## Gebruikers beheren met de CLI

Gebruik de CLI van `magento-cloud` om gebruikers te beheren en met geautomatiseerde systemen te integreren:

- `magento-cloud user:add` - voeg een gebruiker aan het project toe
- `magento-cloud user:delete` -delete een gebruiker
- `magento-cloud user:list [users]` -list project users
- `magento-cloud user:role` - bekijk of verander de gebruikersrol
- `magento-cloud user:update` -update gebruikersrol in een project

De volgende voorbeelden gebruiken `magento-cloud` CLI om een gebruiker toe te voegen, rollen te vormen, projecttaken te wijzigen, en gebruikersrollen toe te wijzen.

**om een gebruiker toe te voegen en rollen** toe te wijzen:

1. Voeg de gebruiker toe met de CLI van `magento-cloud` .

   ```bash
   magento-cloud user:add
   ```

   >[!IMPORTANT]
   >
   >De gebruiker moet een Adobe ID hebben; zie de [&#x200B; eerste vereisten &#x200B;](#add-users-and-manage-access).

1. Volg de herinneringen: specificeer het gebruikers e-mailadres, plaats het project en milieu-type rollen, en voeg de gebruiker toe.

   > Voorbeeldaanwijzingen

   ```
   Enter the user's email address: alice@example.com
   
   Email address: alice@example.com
   
   The user's project role can be admin (a) or viewer (v).
   
   Project role (default: viewer) [a/v]: viewer
   
   The user's environment type role(s) can be admin (a), viewer (v), contributor (c) or none (n).
   
   Role on type development (default: none) [a/v/c/n]: none
   Role on type production (default: none) [a/v/c/n]: admin
   Role on type staging (default: none) [a/v/c/n]: admin
   
   Adding the user alice@example.com to (project_id):
   Project role: viewer
     Role on type production: admin
     Role on type staging: admin
   
   Are you sure you want to add this user? [Y/n] y
   Adding the user to the project
   ```

   Nadat u de gebruiker hebt toegevoegd, stuurt Adobe een e-mail naar het opgegeven adres met instructies voor toegang tot de Adobe Commerce voor het infrastructuurproject in de cloud.

### De projectrol van een gebruiker weergeven

```bash
magento-cloud user:get alice@example.com
```

>Monsterrespons:

```
Current role(s) of User (alice@example.com) on Production (project_id):
  Project role: admin
```

### Een gebruiker toevoegen aan meerdere omgevingen

U kunt als volgt een gebruiker toevoegen als een `viewer` in een `Production` -omgeving en als een `contributor` in een `Integration` -omgeving:

```bash
magento-cloud user:add alice@example.com -r production:v -r integration:c
```

### Machtigingen voor de gebruikersomgeving bijwerken

U kunt als volgt gebruikersomgevingsmachtigingen bijwerken naar `admin` in de `Production` -omgeving:

```bash
magento-cloud user:update alice@example.com -r production:a
```

## Gebruikers beheren vanuit de [!DNL Cloud Console]

U kunt [[!DNL Cloud Console]](../../get-started/cloud-console.md) gebruiken om toestemmingen toe te voegen en _te gebruiken geef_ eigenschap uit om toestemmingen voor een bestaande gebruiker te wijzigen.

>[!IMPORTANT]
>
>De gebruiker moet een Adobe ID hebben; zie de [&#x200B; eerste vereisten &#x200B;](#add-users-and-manage-access).

### Een gebruiker toevoegen aan het project

1. Meld u aan bij de map [[!DNL Cloud Console] &#x200B;](https://console.adobecommerce.com/) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Voor het dashboard van het Project, klik het configuratiepictogram in het hogere recht.

1. Onder _Montages van het Project_, klik **[!UICONTROL Access]**.

1. In de _mening van de Toegang_, klik **[!UICONTROL Add]**.

1. Vul het _[!UICONTROL Add User]_-formulier in:

   - Voer het e-mailadres van de gebruiker in.

   - **[!UICONTROL Project admin]** - geef beheerdersrechten op voor alle instellingen en omgevingstypen.

   - **[!UICONTROL Environment types and permissions]** - geef toegang en specifieke toestemmingsniveaus aan bepaalde milieutypes. _Geen toegang_, _Admin_ (veranderingsmontages, voer actie uit, verenigt code), _Medewerker_ (duw code), of _Kijker_ (mening slechts).

   >[!TIP]
   >
   >Slechts kan a **admin van het Project** gebruikers in om het even welk milieu beheren. Om een gebruikerstoegang tot het **lusje van de Toegang** te verlenen, moet een ander **Project admin** of de **Eigenaar van de Rekening** die gebruiker toewijzen **admin** rol van het Project.

1. Klik op **[!UICONTROL Add User]**.

   >[!IMPORTANT]
   >
   >Het toevoegen van een gebruiker activeert niet automatisch een plaatsing.

1. Nadat u gebruikers hebt toegevoegd, implementeert u alle omgevingen opnieuw om de wijzigingen toe te passen. Het toevoegen van een gebruiker activeert niet automatisch een plaatsing. Herplaatsing is een belangrijke stap om ervoor te zorgen dat de gebruiker tot een milieu kan toegang hebben gebruikend SSH of beheerderstaken uitvoeren.

Nadat u de gebruiker hebt toegevoegd, stuurt Adobe een e-mail naar het opgegeven adres met instructies voor toegang tot de Adobe Commerce voor het infrastructuurproject in de cloud.

## Vereisten voor gebruikersverificatie

Voor extra veiligheid, verstrekt Adobe project-vlakke multi-factor authentificatie (MFA) handhaving om twee-factor authentificatie (TFA) voor de toegang van SSH tot Adobe Commerce op de broncode en milieu&#39;s van het wolkeninfrastructuurproject te vereisen. Zie [&#x200B; MFA voor SSH &#x200B;](multi-factor-authentication.md) toelaten.

Wanneer MFA-handhaving is ingeschakeld op een Adobe Commerce op een cloudinfrastructuurproject, moeten alle gebruikers met SSH-toegang tot een omgeving in dat project TFA inschakelen op hun Adobe Commerce op een cloudinframeconferentieaccount. Voor geautomatiseerde processen kunt u een gebruiker van de computer en een API-token maken voor verificatie via de opdrachtregel.

Nadat u een gebruiker aan een Cloud-project hebt toegevoegd, vraagt u de gebruiker om de beveiligingsinstellingen van zijn account te controleren en de volgende beveiligingsconfiguraties toe te voegen, indien nodig:

- **laat TFA** toe - ontmoet veiligheid en nalevingsnormen door twee-factor authentificatie te vormen. De projecten die met [&#x200B; worden gevormd MFA handhaving &#x200B;](multi-factor-authentication.md) vereisen TFA op rekeningen die SSH gebruiken om tot de projecten toegang te hebben.

- **laat de sleutels van SSH** toe - de Gebruikers die toegang tot Adobe Commerce op de gegevensopslagplaatsen van de bron van de wolkeninfrastructuur vereisen moeten de sleutels van SSH op hun rekening toelaten. Zie [&#x200B; Veilige verbindingen &#x200B;](../development/secure-connections.md).

- **creeer een API teken** - de gebruikers moeten een API teken produceren dat voor de toegang van SSH tot een milieu wordt gebruikt. U hebt het token nodig om verificatieworkflows voor geautomatiseerde processen in te schakelen.

  Bij projecten waarvoor MFA-handhaving is ingeschakeld, moet u het API-token gebruiken om SSH-toegangsverzoeken van geautomatiseerde accounts te verifiëren. Met het token kunnen geautomatiseerde processen verificatieworkflows omzeilen waarvoor TFA is vereist.

### TFA inschakelen voor Cloud-accounts

Adobe Commerce op cloud-infrastructuur ondersteunt TFA met een van de volgende toepassingen:

- [&#x200B; de Authenticator van Google (Android/iPhone) &#x200B;](https://support.google.com/accounts/answer/1066447?hl=en)
- [&#x200B; Authy (Android/iPhone) &#x200B;](https://authy.com/features/)
- [&#x200B; FreeOTP (Android) &#x200B;](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)
- [&#x200B; de Authenticator van de GAuth (OS Firefox, Desktop, anderen) &#x200B;](https://github.com/gbraad-apps/gauth)

De instructies voor het installeren van de authentificatortoepassing en het toelaten van TFA zijn beschikbaar op de _montages van de Rekening_ pagina in [!DNL Cloud Console].

**om TFA op uw gebruikersrekening** toe te laten:

1. Login aan [&#x200B; uw rekening &#x200B;](https://console.adobecommerce.com).

1. Klik op **[!UICONTROL My Profile]** in het accountmenu rechtsboven.

1. Voor het _lusje van de Veiligheid_, klik **[!UICONTROL Set up application]**.

1. Als u geen goedgekeurde verificatietoepassing op uw mobiele apparaat hebt, gebruikt u de gekoppelde instructies om een toepassing te installeren.

1. Voeg uw Adobe Commerce-account voor de cloud-infrastructuur toe aan de verificatietoepassing.

   - Open de verificatietoepassing op uw mobiele apparaat. Voeg vervolgens de instellingscode toe aan de toepassing.

   - Typ op de pagina [!UICONTROL **[!UICONTROL TFA set up - Application]**] de TFA-code van uw mobiele apparaat in het veld **[!UICONTROL Application verification code]** .

   - Klik op **[!UICONTROL Verify and save]**.

     Als de code geldig is, stuurt Adobe een bericht naar het e-mailadres van de account waarin wordt bevestigd dat de account nu TFA heeft.

1. Optioneel. Laat _Vertrouwde browser_ montages toe om de authentificatiecode in browser voor 30 dagen in cache te plaatsen.

   Deze configuratie vermindert het aantal authentificatieuitdagingen tijdens projectlogin.

1. Klik **sparen** of **Overslaan**.

1. Sla de herstelcodes op.

   - Voor de _opstelling van TFA - de codepagina van de Terugwinning_, kopieer en bewaar de terugwinningscodes zodat u in uw Adobe Commerce op het project van de wolkeninfrastructuur kunt registreren wanneer u niet tot uw mobiel apparaat of authentificatietoepassing kunt toegang hebben.

   - Kopieer de herstelcodes naar een andere locatie of noteer deze voor het geval dat u de toegang tot uw apparaat of verificatietoepassing verliest.

   - Klik **sparen** om de codes aan uw rekening te bewaren zodat kunt u hen van uw montages van de rekeningsveiligheid bekijken en beheren.

     >[!WARNING]
     >
     >Als u toegang tot een rekening met TFA verliest en niet de lijst van terugwinningscodes hebt, moet u uw projectbeheerder contacteren, of [&#x200B; een kaartje van de Steun van Adobe Commerce voorleggen &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) om de toepassing van TFA terug te stellen.

1. Na de voltooiing van de opstelling van TFA, klik **sparen** om uw rekening bij te werken.

1. Verifieer uw huidige zitting met TFA.

   - Afmelden bij uw account.
   - Meld u aan met uw gebruikersnaam en wachtwoord.
   - Voer desgevraagd de TFA-code voor het `accounts.magento.cloud` -item in vanuit de verificatietoepassing op uw mobiele apparaat.

### TFA-configuratie en herstelcodes beheren

U kunt de configuratie van TFA voor een Adobe Commerce op de rekening van de wolkeninfrastructuur van de _sectie van de Veiligheid_ op de _Mijn pagina van het Profiel_ beheren.

1. Login aan [&#x200B; uw rekening &#x200B;](https://console.adobecommerce.com).

1. Klik op **[!UICONTROL My Profile]** in het accountmenu rechtsboven.

1. Voor de _Mijn pagina van het Profiel_, klik het **[!UICONTROL Security]** lusje.

1. Gebruik de beschikbare koppelingen om de TFA-instellingen voor uw Adobe Commerce bij te werken op uw account voor cloudinfrastructuur:

   - TFA uitschakelen
   - De verificatietoepassing herstellen
   - Vertrouwde browsers toevoegen of verwijderen
   - TFA-herstelcodes weergeven of vernieuwen op uw account

### Een API-token maken

Een API teken kan voor een OAuth 2 toegangsteken worden geruild, dat dan kan worden gebruikt om verzoeken voor authentiek te verklaren.

Bij projecten waarvoor MFA-handhaving is ingeschakeld, moet u een API-token hebben om SSH-toegang voor systeemgebruikers en geautomatiseerde processen mogelijk te maken.

>[!IMPORTANT]
>
>Bescherm API-tokenwaarden voor uw account. Stel de waarde niet beschikbaar in codesteekproeven, het scherm vangt, of onveilige cliënt-server mededelingen. Stel ook niet de waarde in broncode bloot die in openbare bewaarplaatsen wordt opgeslagen.

**om een API teken** tot stand te brengen:

1. Login aan [&#x200B; uw rekening &#x200B;](https://console.adobecommerce.com).

1. Klik op **[!UICONTROL My Profile]** in het accountmenu rechtsboven.

1. Voor de _Mijn pagina van het Profiel_, klik het **[!UICONTROL API tokens]** lusje.

1. Klik op **[!UICONTROL Create API token]** en voer een naam in, bijvoorbeeld een naam die overeenkomt met de gebruiker van de computer of een geautomatiseerd proces dat het API-token gebruikt.

   ![&#x200B; API tokens &#x200B;](../../assets/api-token-name.png)

1. Klik op **[!UICONTROL Create API token]**.
