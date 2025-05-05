---
title: Beveiligde verbindingen
description: Leer hoe u SSH-toetsen op uw Adobe Commerce kunt toepassen op een cloudinfrastructuurproject en u kunt aanmelden bij externe omgevingen.
role: Developer
feature: Cloud, Security
topic: Security
exl-id: 73af13d8-7085-4ac8-9cfe-9772bc6bc112
source-git-commit: c25e5b74ae8105995107860246ecb9ba45910bb1
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# Beveiligde verbindingen met externe omgevingen

Veilig Shell (SSH) is een gemeenschappelijk protocol dat wordt gebruikt om veilig in verre servers en systemen te registreren. U kunt SSH gebruiken om toegang te krijgen tot uw externe omgevingen voor het beheer van de Adobe Commerce-toepassing en het openen van logbestanden voor externe omgevingen. Adobe ondersteunt alleen Secure FTP-verbindingen (sFTP) met behulp van de openbare SSH-sleutel. FTP-verbindingen worden niet ondersteund.

## Een SSH-sleutelpaar genereren

Creeer een SSH zeer belangrijk paar op elke machine en werkruimte die toegang tot uw code en milieu&#39;s van de projectbron vereist. De sleutel van SSH staat u toe om met GitHub te verbinden om broncode te beheren en met wolkenservers te verbinden zonder het moeten uw gebruikersbenaming en wachtwoord constant leveren. Zie [ Verbindend met GitHub met SSH ](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) voor verdere instructies bij het creëren van een SSH zeer belangrijk paar.

- De _openbare sleutel_ is veilig om voor de toegang tot van een plaats, SSH, en sFTP te verstrekken.
- De _privé sleutel_ blijft privé op het werkstation.

>[!CAUTION]
>
>**deelt nooit uw privé sleutel.** Voeg het niet toe aan een ticket, kopieer het naar een chat of koppel het aan e-mailberichten.

## Een SSH-openbare sleutel toevoegen aan uw account

Nadat u toevoegt of uw openbare sleutel van SSH aan uw Adobe Commerce op de rekening van de wolkeninfrastructuur bijwerkt, [ herstelt alle actieve milieu&#39;s ](https://experienceleague.adobe.com/nl/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-reference#environmentredeploy) op uw rekening om de sleutel te installeren.

U kunt SSH-sleutels aan uw account toevoegen met een van de volgende methoden: Cloud CLI of [!DNL Cloud Console] .

>[!BEGINTABS]

>[!TAB  CLI ]

### De SSH-toets toevoegen met de Cloud CLI

1. Wijzig op uw lokale werkstation de projectmap.

1. Meld u aan bij uw project:

   ```bash
   magento-cloud login
   ```

1. Voeg de openbare sleutel toe.

   ```bash
   magento-cloud ssh-key:add ~/.ssh/id_rsa.pub
   ```

>[!TIP]
>
>U kunt SSH-toetsen weergeven en verwijderen met de Cloud CLI-opdrachten `ssh-key:list` en `ssh-key:delete` .

>[!TAB  Console ]

### De SSH-toets toevoegen met de [!DNL Cloud Console]

**om een sleutel van SSH aan een nieuw project** toe te voegen:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Klik op **[!UICONTROL No SSH key]**. Dit pictogram is rechts van het bevelgebied en is zichtbaar wanneer het project geen sleutel van SSH bevat.

1. Kopieer en kleef de inhoud van uw openbare sleutel van SSH op het **Openbare zeer belangrijke** gebied.

1. Volg de overige aanwijzingen.

**om een sleutel van SSH aan uw profiel van de Wolk toe te voegen**:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. In het hoger-juiste rekeningsmenu, klik **Mijn Profiel**.

1. In de _sleutels van SSH_ mening, klik **openbare sleutel** toevoegen.

1. In _voeg een sleutel van SSH_ vorm toe, geef uw sleutel a **Titel**, en kleef de openbare sleutel van SSH op het **Zeer belangrijke** gebied.

1. Klik **sparen**.

>[!ENDTABS]

## Verbinding maken met een externe omgeving

U kunt verbinding maken met een externe omgeving met de opdracht `magento-cloud` CLI of SSH. De `magento-cloud` CLI bevelen kunnen slechts in de integratiemilieu&#39;s van de Aanzet en van de Pro worden gebruikt.

### Cloud CLI gebruiken

**aan login aan een verre integratiemilieu**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak een lijst van de milieu&#39;s in dat project.

   ```bash
   magento-cloud environment:list -p <project-ID>
   ```

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh -p <project-ID> -e <environment-ID>
   ```

### Een SSH-opdracht gebruiken

[!DNL Cloud Console] omvat een lijst van Web en de toegangsbevelen van SSH voor elk milieu.

**om het bevel van SSH te kopiëren**:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .

1. Selecteer een project van de _Alle projecten_ lijst.

1. Selecteer een omgeving.

1. Klik op **[!UICONTROL SSH]**.

1. In het _SSH_ lusje, klik de exemplaarknoop om het volledige bevel van SSH aan het klembord te kopiëren.

1. Open een terminal en plak de opdracht SSH om een verbinding te maken.

   ```bash
   ssh abcdefg123abc-branch-a12b34c--mymagento@ssh.us-2.magento.cloud
   ```

>[!TIP]
>
>Voor Pro het Staging en van de Productie milieu&#39;s, kan het bevel van SSH als kijken:
>
>```bash
>ssh <node>.ent-<project-ID>-<environment>-<user-ID>@ssh.<region>.magento.com
>```

## sFTP

Adobe Commerce on cloud Infrastructure ondersteunt toegang tot uw omgevingen met sFTP (Secure FTP) met SSH-verificatie. Gebruik een cliënt die de zeer belangrijke authentificatie van SSH voor sFTP steunt en uw openbare sleutel van SSH gebruiken. Uw openbare sleutel van SSH moet aan het doelmilieu worden toegevoegd. Voor de milieu&#39;s van de Aanzet en Pro integratiemilieu&#39;s, kunt u het [ toevoegen door  [!DNL Cloud Console]](#add-your-ssh-key-using-the-project-web-interface).

De read-only verbindingen sFTP worden _niet_ gesteund; sFTP de toegang wordt voorzien van _schrijft_ toestemming door gebrek.

Wanneer het vormen sFTP, gebruik de informatie van uw bevel van het de toegangsmilieu van SSH: `<project-id>-<environment-id>--<app-name>@ssh<cloud-host>`

- **Gebruikersnaam**: Alle inhoud vóór `@` in uw de toegangsbestemming van SSH.
- **Wachtwoord**: U hebt geen wachtwoord voor sFTP nodig. sFTP-toegang gebruikt de SSH-sleutelverificatie.
- **Gastheer**: Alle inhoud na `@` in uw toegang van SSH.
- **Haven**: 22, die de haven standaardSSH is.
- **SSH** Privé Sleutel: Indien noodzakelijk, verstrek de plaats van uw privé sleutel aan de cliënt sFTP. Persoonlijke sleutels worden standaard opgeslagen in de map `~/.ssh` .

Afhankelijk van de client zijn mogelijk aanvullende opties vereist om SSH-verificatie voor sFTP te voltooien. Controleer de documentatie voor de geselecteerde client.

Voor **de milieu&#39;s van de Aanzet en Pro integratiemilieu&#39;s**, kunt u [ ook overwegen toevoegend a `mount`](../application/properties.md#mounts) voor toegang tot een specifieke folder. U voegt de hoeveelheid toe aan uw `.magento.app.yaml` -bestand. Voor een lijst van beschrijfbare folders, zie [ de structuur van het Project ](../project/file-structure.md). Dit koppelingspunt werkt alleen in die omgevingen.

Voor **Pro het Opvoeren en de milieu&#39;s van de Productie**, als u geen toegang SSH tot het milieu hebt, moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voorleggen om sFTP- toegang en een onderstelpunt voor toegang tot de specifieke omslag, b.v., `pub/media` te verzoeken.

>[!NOTE]
>Voor Pro het Opvoeren en Productie, als de sFTP verbinding voor a _generische_ gebruiker is die **&#x200B;**&#x200B;niet [ moet worden toegevoegd aan het project van de Wolk ](../project/user-access.md), moet u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) met hun **openbare** sleutel in bijlage voorleggen. **verstrekt nooit uw privé sleutel van SSH.**

## SSH-tunneling

U kunt SSH het een tunnel graven gebruiken om met de dienst van uw lokale ontwikkelomgeving te verbinden alsof de dienst lokaal was. Alvorens het een tunnel graven, vorm uw [ SSH ](#add-an-ssh-public-key-to-your-account).

Gebruik een eindtoepassing aan login en geef bevelen uit.

```bash
magento-cloud login
```

Controleer of er tunnels geopend zijn.

```bash
magento-cloud tunnel:list
```

Om een tunnel te bouwen, moet u de [ toepassingsnaam ](../application/properties.md#name) kennen. U kunt de toepassingsnaam controleren gebruikend CLI:

```bash
magento-cloud apps
```

### De SSH-tunnel instellen

```bash
magento-cloud tunnel:open -e <environment-ID> --app <app-name>
```

Als u bijvoorbeeld een tunnel wilt openen naar de `sprint5` -vertakking in een project met een app met de naam `mymagento` , voert u

```bash
magento-cloud tunnel:open -e sprint5 --app mymagento
```

Monsterrespons:

```
SSH tunnel opened on port 30004 to relationship: redis
SSH tunnel opened on port 30005 to relationship: database
Logs are written to: /home/magento_user/.magento/tunnels.log

List tunnels with: magento-cloud tunnels
View tunnel details with: magento-cloud tunnel:info
Close tunnels with: magento-cloud tunnel:close
```

**om informatie over uw tunnel** te tonen:

```bash
magento-cloud tunnel:info -e <environment-ID>
```

### Verbinding maken met services

Na het vestigen van een tunnel van SSH, kunt u met de diensten verbinden alsof het lopen plaatselijk. Als u bijvoorbeeld verbinding wilt maken met de database, gebruikt u de volgende opdracht:

```bash
mysql --host=127.0.0.1 --user='<database-username>' --pass='<user-password>' --database='<name>' --port='<port>'
```
