---
title: Voorbereiden op ontwikkeling
description: Verzamel referenties en leer over de tools die beschikbaar zijn om een ontwikkelwerkruimte in te stellen voor gebruik met uw Commerce op een cloud-infrastructuurproject.
recommendations: noDisplay, catalog
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Voorbereiden op ontwikkeling

Of u nu nieuw bent in Commerce of een bestaande Commerce-eigenaar die overgaat naar de cloudinfrastructuur, gebruik deze stappen voor het voorbereiden van een ontwikkelwerkruimte voor uw Cloud-project. Als u al een aantal van deze stappen hebt uitgevoerd of een bestaande Adobe Commerce-ontwikkelaarsomgeving hebt, kunt u het volgende controleren op verwachte resultaten en doorgaan met de volgende stap. Sommige configuraties en workflows verschillen van een standaardinstallatie op locatie.

## Credentials

Verzamel de volgende sleutels en accounttoegang voordat u een werkruimte instelt:

- **de sleutels van de Authentificatie (de sleutels van Composer)**

  De sleutels van de authentificatie zijn 32 karakterauthentificatie tokens die veilige toegang tot de bewaarplaats van de Samensteller van Adobe Commerce (`repo.magento.com`) en om het even welke andere diensten van het Git die voor toepassingsontwikkeling zoals GitHub worden vereist verlenen. Uw account kan meerdere verificatietoetsen hebben. Voor de opstelling van de werkruimte, begin met één specifieke sleutel voor uw codebewaarplaats. Als u geen sleutels hebt, contacteer de projecteigenaar, of creeer de [&#x200B; authentificatiesleutels &#x200B;](../cloud-guide/development/authentication-keys.md) zelf.

- **de rekening van het Project van de Wolk**

  De eigenaar van het project moet u uitnodigen voor het Adobe Commerce-project voor cloudinfrastructuur. Wanneer u de e-mailuitnodiging ontvangt, klikt u op de koppeling en volgt u de aanwijzingen om uw account te maken. Zie [&#x200B; on boarding &#x200B;](onboarding.md).

- **Sleutel van de Encryptie van Adobe Commerce**

  Wanneer u alleen een bestaand systeem importeert, legt u de coderingssleutel vast die wordt gebruikt om uw toegang en gegevens voor de database te beveiligen. Voor details op deze sleutel, zie [&#x200B; kwesties met encryptiesleutel oplossen &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolve-issues-with-encryption-key.html?lang=nl-NL)

## Gereedschappen voor ontwikkelaars

- **installeer de Cloud CLI**

  Installeer de CLI van `magento-cloud` zodat u cloudomgevingen kunt beheren en automatiseringstaken kunt uitvoeren. Zie [&#x200B; Cloud CLI &#x200B;](../cloud-guide/dev-tools/cloud-cli-overview.md) voor installatieinstructies.

- **installeer Docker voor lokale ontwikkeling en het testen**

  U kunt ook de Docker-omgeving gebruiken om de Commerce-omgeving op de cloud-infrastructuur `integration` te emuleren voor lokale ontwikkeling. Er zijn drie essentiële componenten: een Adobe Commerce v2-sjabloon, een docker-compositie en een `ece-tools` -pakket.

   - [Docker-architectuur en algemene opdrachten](../cloud-guide/dev-tools/cloud-docker.md)
   - [&#x200B; de ontwikkelomgeving van Docker van de Lancering &#x200B;](https://developer.adobe.com/commerce/cloud-tools/docker/setup/)
   - [ECE-gereedschapspakket](../cloud-guide/dev-tools/package-overview.md)

- **integreer op git-Gebaseerde diensten**

  U kunt desgewenst een op Git gebaseerde hostingservice, zoals GitHub of GitLab, integreren met Adobe Commerce op cloudinfrastructuur. Zie [&#x200B; Integraties &#x200B;](../cloud-guide/integrations/overview.md).

## Projectcode

Een veilige verbinding is essentieel voor interactie met de externe omgeving. Voor een nieuw project, [&#x200B; login aan  [!DNL Cloud Console] &#x200B;](https://console.adobecommerce.com) en klik **[!UICONTROL No SSH key]**. Dit pictogram is rechts van het bevelgebied en is zichtbaar wanneer het project geen sleutel van SSH bevat. Zie [&#x200B; Veilige verbindingen &#x200B;](../cloud-guide/development/secure-connections.md#add-an-ssh-public-key-to-your-account).

**om uw codebase aan uw lokaal werkstation** te klonen:

1. Klik in [[!DNL Cloud Console] &#x200B;](https://console.adobecommerce.com) op **[!UICONTROL code]** en selecteer de tab **[!UICONTROL Git]** .

   ![&#x200B; Kloon uw code &#x200B;](../assets/ui-git-code.png){width="450"}

1. Kopieer de opgegeven opdracht `git clone ...` .

1. In een terminal, creeer en verander in uw het werk folder.

1. Plak de opdracht `git clone ...` en voer deze uit.

>[!TIP]
>
>De Adobe voorziet uw aanvankelijke projectmilieu gebruikend een malplaatjebewaarplaats die pakketinstructies voor een specifieke versie van Adobe Commerce omvat. Herzie het [&#128279;](../cloud-guide/project/file-structure.md) onderwerp van het 0&rbrace; projectdossier structuur en leer meer over belangrijke projectdossiers en wolkenmalplaatjes.
