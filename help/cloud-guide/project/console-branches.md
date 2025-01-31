---
title: Vertakkingen beheren met de  [!DNL Cloud Console]
description: Leer hoe te om de milieutakken voor Adobe Commerce op wolkeninfrastructuur te beheren gebruikend  [!DNL Cloud Console].
role: Developer
feature: Cloud, Install
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 0%

---

# Vertakkingen beheren met de [!DNL Cloud Console]

U kunt uw omgevingen beheren met de [!DNL Cloud Console] of de `magento-cloud` CLI. Uw projectbestanden worden opgeslagen in een Git-opslagplaats. U kunt Git-opdrachten gebruiken om uw code te beheren, maar de CLI van `magento-cloud` is ontworpen voor interactie met platformfuncties, terwijl de opdrachten van Git dat niet doen. Zie [ bevelen van de Git ](../dev-tools/cloud-cli-overview.md#git-commands) in het onderwerp van wolk CLI.

In dit onderwerp wordt besproken hoe u de [!DNL Cloud Console] kunt gebruiken om:

- Een omgeving toevoegen of verwijderen
- Synchroniseren (`git pull`) vanuit de bovenliggende omgeving
- Samenvoegen (`git push`) tot de bovenliggende omgeving

>[!TIP]
>
>U kunt geen vertakkingen maken vanuit Pro Staging- en Productieomgevingen. U kunt vertakken vanuit de `master` vertakking.

## Een omgeving maken

De vertakkingsstrategie gebruikt een algemene Git-workflow waar u code ontwikkelt en extensies toevoegt in een ontwikkelingsvertakking. Zie [ Aanzet ](../architecture/starter-architecture.md) en [ Pro ](../architecture/starter-develop-deploy-workflow.md) architectuuroverzichten.

- Maak bij Starter een `staging` -vertakking vanuit de `master` -vertakking en vertakking vanuit `staging` voor ontwikkeling.
- Voor Pro maakt u een ontwikkelingsvertakking vanuit de `Integration` -omgeving.

Uw rekening steunt een beperkt aantal ![ actieve tak ](../../assets/icon-active.png){width="32"} (active) and an unlimited number of ![inactive branch](../../assets/icon-inactive.png){width="32"} (inactieve) ontwikkelingstakken. Actieve en inactieve vertakkingen beheren door een vertakking toe te voegen of te verwijderen met alleen de vertakking [!DNL Cloud Console] of de Cloud CLI. Alvorens u een tak kunt schrappen, deactiveert u de tak, die in de _1} lijst van Milieu&#39;s {als_ inactief _blijft._ U kunt de tak later opnieuw activeren of u kunt [ de tak ](../dev-tools/cloud-cli-overview.md#) in milieumontages schrappen of Cloud CLI gebruiken.

Als u extra actieve milieu&#39;s voor ontwikkeling nodig hebt, leg a [ kaartje van de Steun ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor.

**om een tak** toe te voegen:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Selecteer een omgeving.

   >[!TIP]
   >
   >Uw nieuwe vertakking is gekloond uit deze omgeving. Kies een bovenliggende omgeving die vergelijkbaar is met de omgeving die u gaat maken.

1. Klik op **[!UICONTROL Branch]**.

   ![ creeer een tak ](../../assets/button-branch.png){width="150"}

1. In het _Vertakking van.._ vorm, ga een taknaam in.

   De milieu _naam_ is verschillend van milieu _identiteitskaart_ slechts als u ruimten of hoofdbrieven in de milieunaam gebruikt. Een milieu-id bestaat uit alle kleine letters, getallen en toegestane symbolen. Hoofdletters in een omgevingsnaam worden omgezet in kleine letters in de id. Spaties in een omgevingsnaam worden omgezet in streepjes.

   Een milieu naam **kan** geen karakters omvatten die voor uw shell van Linux of voor regelmatige uitdrukkingen worden gereserveerd. De verboden karakters omvatten krullende steunen (`{ }`), haakjes, asterisk (`*`), punthaakjes (`>`), en ampersand (`&`), percenten (<code>%</code>) en andere tekens.

1. Selecteer een **[!UICONTROL Environment type]** .

1. Klik op **[!UICONTROL Create Branch]**.

1. Wacht terwijl het milieu opstelt.

   Tijdens plaatsing, is de milieustatus **in proces**. Na een succesvolle plaatsing, verandert de status in een groen vinkje voor **succes**.

## Inactieve vertakking maken

U kunt geen inactieve tak van de console van Adobe Commerce Cloud of CLI tot stand brengen. Als u een inactieve vertakking wilt maken, maakt u deze in de Git-opslagplaats en drukt u met de optie `environment.Parent` op de opdracht.

```bash
git push -o "environment.Parent=<parent branch>" <origin> <branch>
```

## Een omgeving verwijderen

Voordat u een omgeving kunt verwijderen, moet u deze deactiveren. Als een omgeving inactief is, kunt u deze verwijderen.

**om een milieu** te deactiveren:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Selecteer het milieu van de navigatiebar _lijst van het Milieu_.

1. Klik op het configuratiepictogram aan de rechterkant van de bovenste navigatiebalk om de omgevingsinstellingen te openen.

1. Ga naar het tabblad _[!UICONTROL General]_, blader omlaag naar de_[!UICONTROL Deactivate environment]_ -sectie en klik **[!UICONTROL Deactivate environment and delete data]** en volg de instructies.

## Een omgeving synchroniseren

Een omgeving (of vertakking) synchroniseren is hetzelfde als `git pull origin <parent>` . U kunt bijgewerkte code synchroniseren vanuit een bovenliggende omgeving. U kunt deze functie gebruiken via [!DNL Cloud Console] voor alle Starter- en Pro-omgevingen.

Voor een Pro-abonnement kunt u synchroniseren van Staging en Productie naar uw `master` -vertakking. Deze synchronisatie trekt en duwt slechts code, niet gegevens. Om gegevens te synchroniseren, stort de gegevensbestandgegevens en duw het aan het gegevensbestand van een andere milieu. Zie [ migreren en statische dossiers en gegevens ](/help/cloud-guide/deploy/staging-production.md#migrate-static-files) opstellen.

**om een milieu** te synchroniseren:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Klik in de lijst met omgevingen op de naam van de vertakking die u wilt synchroniseren.

1. Klik (synchroniseren).

   ![ Synchroniseer een milieu ](../../assets/button-sync.png){width="150"}

1. Selecteer de te synchroniseren items.

   - Vervang de gegevens—(gegevens en bestanden) synchroniseert wijzigingen in de database en inhoudsbestanden van de bovenliggende vertakking.
   - Met Samenvoegen—(code) wordt de bijgewerkte code van de bovenliggende vertakking gesynchroniseerd.

   Dit bouwt ook een bevel CLI voor u om te kopiëren en te gebruiken.

1. Klik **Synchronisatie**.

## Samenvoegen met bovenliggende omgeving

Het samenvoegen van een omgeving (of vertakking) is hetzelfde als `git push origin` . U voegt samen om bijgewerkte code van een milieu aan zijn oudermilieu te duwen. U kunt deze code samenvoegen tot `master` . Met de opdracht `merge` kunt u de implementatie naar Staging en Productie uitvoeren.

**om met het oudermilieu** samen te voegen:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Klik in de lijst met omgevingen op de naam van de vertakking die u wilt samenvoegen.

1. Klik op Samenvoegen.

   ![ voeg een milieu ](../../assets/button-merge.png){width="150"} samen

1. Klik **Fusie** en bevestig de actie.

## Logboeken weergeven

Via de [!DNL Cloud Console] kunt u verschillende logbestanden voor omgevingen bekijken, zoals de build, implementatie en implementatiegeschiedenis.

Voor **Starter**, kunt u bouwt en opstelt logboeken en de plaatsingsgeschiedenis. Deze omgevingen omvatten de `master` (Production) -vertakking en alle vertakkingen die daaruit zijn gemaakt.

Voor **Pro**, kunt u de volgende logboeken in elk milieu herzien:

- Integratie-bouwt en opstelt en plaatsingsgeschiedenis
- Staging—Bouw logbestanden en implementatiegeschiedenis samen. Gebruik SSH om u aan te melden bij de server om logboeken voor implementatie weer te geven.
- Productie-bouw logboeken en plaatsingsgeschiedenis. Gebruik SSH om u aan te melden bij de server om logboeken voor implementatie weer te geven.

**om logboeken in[!DNL Cloud Console]** te bekijken:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Selecteer een omgeving.

   De omgevingsmening verstrekt een [ lijst van de Activiteit ](activity-stream.md) die _recente_ gebeurtenissen, één ingang per geprobeerd actie met inbegrip van syncs, fusies, takken, steunen, en meer toont. Klik **allen** voor de volledige plaatsingsgeschiedenis.

1. Om het bouwstijllogboek te bekijken, selecteer het Succes of de Verbinding van de Mislukking per plaatsingsverslag op de rekening.

>[!TIP]
>
>Klik de **Filter door** pictogram voor een drop-down lijst en selecteer het type van berichten aan mening.

## Code ophalen uit een persoonlijke Git-opslagplaats

Uw Adobe Commerce on cloud-infrastructuurproject kan code van een privéopslagplaats voor Git bevatten. U hebt bijvoorbeeld code voor een aangepaste module of een aangepast thema in een privérepo. Hiervoor moet u de openbare SSH-sleutel van uw project toevoegen aan uw persoonlijke Git-opslagplaats en het `composer.json` -projectbestand bijwerken.

Om een plaatsingssleutel aan uw privé bewaarplaats toe te voegen GitHub, moet u de beheerder van die bewaarplaats zijn. GitHub staat u toe om sleutel voor één bewaarplaats slechts te gebruiken opstellen.

Als u liever hebt dat uw project toegang krijgt tot meerdere opslagruimten, kunt u een SSH-sleutel aan een geautomatiseerde gebruikersaccount koppelen. Omdat deze rekening niet door een mens wordt gebruikt, wordt het bedoeld als a [ machinegebruiker ](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys). Voeg de computeraccount toe als medewerker of voeg de gebruiker van de computer toe aan een team dat toegang heeft tot de opslagruimten.

>[!INFO]
>
>Adobe raadt u aan deze code toe te voegen en samen te voegen aan uw Git-opslagruimten voor projecten. Als u de verbinding niet vormt, kunt u bouwstijlkwesties ervaren.

**om uw openbare sleutel van SSH te vinden**:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Klik op het configuratiepictogram rechts van de bovenste navigatiebalk.

1. In _Montages van het Project_, klik **[!UICONTROL Deploy Key]**.

1. Kopieer de implementatiesleutel naar het klembord voor gebruik in een van de volgende op Git gebaseerde methoden:

>[!BEGINTABS]

>[!TAB  GitHub ]

### Ga uw sleutel van GitHub opstellen in

Op GitHub, stel sleutels in read-only door gebrek op.

**om uw project openbare sleutel in te gaan aangezien GitHub sleutel** opstelt:

1. Meld u als beheerder aan bij uw GitHub-opslagplaats.
1. Klik op de tab Opslagruimte **[!UICONTROL Settings]** .

   >[!NOTE]
   >
   >Als deze optie niet wordt weergegeven, wordt u niet aangemeld als beheerder van de gegevensopslagruimte en kunt u deze taak niet uitvoeren. Vraag uw beheerder van de bewaarplaats GitHub om dit te doen.

1. Op het _lusje van Montages_ in de linkernavigatie, klik **[!UICONTROL Deploy Keys]**.
1. Klik op **[!UICONTROL Add deploy key]**.
1. Volg de aanwijzingen.

Gebruik in `composer.json` de `<user>@<host>:<.git</code>` -indeling of `ssh://<user>@<host>:<port>/<path>.git` als u een niet-standaardpoort gebruikt.

>[!TAB  Bitbucket ]

### Voer de implementatietoets voor bitmaps in

**om uw project openbare sleutel in te gaan aangezien Bitbucket sleutel** opstelt:

1. Meld u als beheerder aan bij de opslagplaats voor bitmaps.
1. Klik in de linkernavigatie op **[!UICONTROL Settings]** .
1. Klik op Algemeen > **[!UICONTROL Deployment Keys]** .
1. Klik op **[!UICONTROL Add Key]**.
1. Volg de aanwijzingen.

>[!TAB  GitLab ]

### Voer uw GitLab-implementatietoets in

**om de openbare sleutel van SSH voor uw project toe te voegen aangezien GitLab sleutel** opstelt:

1. Meld u als eigenaar aan bij de GitLab-opslagplaats.
1. Verifieer dat de _optie van Pijpleidingen_ voor uw project wordt toegelaten:

   1. Vouw de sectie **[!UICONTROL Visibility, project, features, permissions]** in de projectinstellingen uit.
   1. Klik indien nodig op **[!UICONTROL Pipelines]** om de optie in te schakelen.

1. Voeg uw openbare sleutel van SSH aan de montages CI/CD toe.

   1. Klik in de linkernavigatie op Instellingen > **[!UICONTROL CI / CD]** .
   1. Klik op Deploy Keys **breid** uit om de sleutel te vormen.
   1. In _stel Zeer belangrijke_ vorm op, voeg een opstellen zeer belangrijke naam aan het **[!UICONTROL Title]** gebied toe en kleef uw openbare sleutel van SSH op het **[!UICONTROL Key]** gebied.
   1. Klik op **[!UICONTROL Add Key]** om de configuratie op te slaan.

>[!ENDTABS]

## Beveiligde omgevingen en vertakkingen

U hebt vanuit elke locatie toegang tot uw project en omgevingen via een webbrowser met de [!DNL Cloud Console] . U kunt veiligheid hebben die voor uw milieu, opslag, en plaatsen van de Productie wordt geplaatst. Deze sectie helpt u uw milieu&#39;s van de Integratie en van het Staging voor strikt uw ontwikkelaars, DBAs, en meer beveiligen.

>[!WARNING]
>
>**GEBRUIK NIET** de volgende methodes om de milieu&#39;s van het ProStaging en van de Productie te beveiligen. Dit verbreekt snel caching. Gebruik de [ Blokkerende ](../cdn/fastly-vcl-blocking.md) eigenschap beschikbaar in Fastly CDN voor Adobe Commerce.

**aan veilige milieu&#39;s**:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Selecteer een omgeving en klik op het configuratiepictogram op de navigatiebalk.

1. Op het milieu montages _Algemene_ lusje, klik **** voor **[!UICONTROL HTTP access control enabled]** om veilige toegang toe te laten. U kunt tussen geloofsbrieven of IP adressen kiezen om voor toegang te filtreren.

1. Als u op referenties wilt filteren, klikt u op **[!UICONTROL Add Login]** , voert u een gebruikersnaam en wachtwoord in en klikt u op **[!UICONTROL Add Login]** om toe te voegen.

1. Als u op IP-adres wilt filteren, voert u de IP-adressen in een lijst in met `deny` of `allow` . Bijvoorbeeld:

   ```text
   123.456.789.111/29 allow
   123.456.789.112/29 allow
   234.123.567.111/29 allow
   0.0.0.0/0 deny
   ```

1. Klik op **[!UICONTROL Save]**. Hierdoor wordt de omgeving opnieuw geïmplementeerd om de beveiliging en instellingen bij te werken. Adobe raadt aan de omgeving te testen nadat de beveiligingsinstellingen zijn voltooid.
