---
title: De takken met CLI beheren
description: Leer hoe u de vertakkingen voor Adobe Commerce op cloudinfrastructuur beheert met de Cloud CLI.
role: Developer
feature: Cloud, Install
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# De takken met CLI beheren

Om `magento-cloud` CLI te installeren, zie de [&#x200B; CLI verwijzing van de Wolk &#x200B;](../dev-tools/cloud-cli-overview.md). Nadat u de CLI van `magento-cloud` hebt geïnstalleerd en SSH-toetsen hebt ingesteld voor externe toegang tot uw cloudinfrastructuur, kunt u met `magento-cloud` CLI-opdrachten de omgevingen voor uw projecten beheren. Voor informatie over de omgevingsarchitectuur, zie [&#x200B; architectuur van de Aanzet &#x200B;](../architecture/starter-architecture.md) of [&#x200B; Pro architectuur &#x200B;](../architecture/pro-architecture.md).

Om de takken en de milieu&#39;s met [!DNL Cloud Console] te beheren, zie [&#x200B; takken met  [!DNL Cloud Console]](../project/console-branches.md) beheren.

## CLI-opdrachten gebruiken

De CLI-opdrachten van `magento-cloud` lijken op die van Git. U kunt ze gebruiken om verbinding te maken met uw project en uw omgevingen te beheren. Hoewel u de bevelen van om het even welke folder kunt in werking stellen, adviseert men dat u hen van een projectfolder in werking stelt. Wanneer u vanuit een projectmap uitvoert, kunt u de parameter `-p <project-ID>` weglaten. Zie de [&#x200B; CLI verwijzing van de Wolk &#x200B;](../dev-tools/cloud-cli-overview.md).

## Het project klonen

De volgende instructies gebruiken een combinatie van `magento-cloud` bevelen CLI en de bevelen van het Git om uw project aan uw lokaal werkstation te klonen. Als u een volledige lijst met `magento-cloud` CLI-opdrachten wilt weergeven, gebruikt u de opdracht `magento-cloud list` .

>[!IMPORTANT]
>
>Met sommige opdrachten van Git kunt u geen actie in uw Adobe Commerce uitvoeren voor een infrastructuurproject in de cloud. U kunt bijvoorbeeld een vertakking maken met de opdracht Git, maar u kunt geen nieuwe omgeving maken en activeren. U moet een milieu tot stand brengen gebruikend het `magento-cloud environment:branch <branch-name>` bevel voor het milieu om _actief_ te worden. U kunt [!DNL Cloud Console] ook gebruiken om actieve omgevingen te maken. Zie [&#x200B; CLI van de Wolk verwijzing &#x200B;](../dev-tools/cloud-cli-overview.md#git-commands).

**om een project `master` milieu** te klonen:

1. Login aan uw lokaal werkstation met de eigenaar van het a [&#x200B; dossiersysteem &#x200B;](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/file-system/configure-permissions.html?lang=nl-NL) rekening.

1. Verandering in de Webserver of virtuele gastheer _docroot_ folder.

1. Meld u aan met de CLI van `magento-cloud` .

   ```bash
   magento-cloud login
   ```

1. Maak een lijst van uw projecten.

   ```bash
   magento-cloud project:list
   ```

1. Een project klonen.

   ```bash
   magento-cloud project:get <project-ID>
   ```

   Geef een mapnaam op wanneer hierom wordt gevraagd.

1. Ga naar de map `magento2` .

1. Maak een lijst van beschikbare milieu&#39;s voor het project.

   ```bash
   magento-cloud environment:list
   ```

   >[!IMPORTANT]
   >
   >De opdracht `magento-cloud environment:list` geeft omgevingshiërarchieën weer, maar de opdracht `git branch` niet.

1. De externe vertakkingen ophalen.

   ```bash
   git fetch origin
   ```

1. Pas de bijgewerkte code aan.

   ```bash
   git pull origin <environment-ID>
   ```

>[!TIP]
>
>Zie [&#x200B; Integraties &#x200B;](../integrations/overview.md) voor informatie over het gebruiken van op git-Gebaseerde het ontvangen van de diensten met Adobe Commerce op wolkeninfrastructuur.

## Een vertakking maken voor ontwikkeling

Nadat u uw project hebt gekloond en de configuratie van de Adobe Commerce-beheerdersaccount hebt bijgewerkt, kunt u zich vertakken voor ontwikkeling. Zoals vroeger verklaard, moet u een milieu creëren gebruikend het `magento-cloud environment:branch <branch-name>` bevel of [!DNL Cloud Console] voor het milieu om _actief_ te worden.

- Voor [&#x200B; Aanzet &#x200B;](../architecture/starter-develop-deploy-workflow.md#clone-and-branch), denk na creërend een tak voor `staging`, dan creeer een ontwikkelingstak die op de `staging` tak wordt gebaseerd.
- Voor [&#x200B; Pro &#x200B;](../architecture/pro-develop-deploy-workflow.md#development-workflow), creeer ontwikkelingstakken die op de `Integration` tak worden gebaseerd.

**om een ontwikkelingstak** tot stand te brengen:

1. Wijzig op uw lokale werkstation de projectmap.

1. Maak een omgeving op basis van de vertakking die wordt aanbevolen voor de projectworkflow.

   ```bash
   magento-cloud branch <new-environment-name> integration
   ```

1. Afhankelijkheden bijwerken.

   ```bash
   composer --no-ansi --no-interaction install --no-progress --prefer-dist --optimize-autoloader
   ```

1. [_facultatieve_] creeer a [&#x200B; steun &#x200B;](../storage/snapshots.md) van het milieu.

### Een vertakking samenvoegen

Voeg deze vertakking na het voltooien van de ontwikkeling samen met het bovenliggende element:

1. Wijzigingen in de code vastleggen en doorvoeren:

   ```bash
   git add -A && git commit -m "Add message here"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Samenvoegen met de bovenliggende omgeving:

   ```bash
   magento-cloud environment:merge <environment-ID>
   ```

### Een omgeving verwijderen

Verwijder een omgeving alleen als u zeker weet dat u deze niet meer nodig hebt. U kunt een omgeving niet herstellen nadat u deze hebt verwijderd.

>[!WARNING]
>
>U kunt de `master` -vertakking van geen enkel project verwijderen.

U moet een projectbeheerder, een milieubeheerder, of de Eigenaar van de Rekening zijn om deze taak uit te voeren. Zie [&#x200B; gebruikerstoegang tot de projecten van de Wolk beheren &#x200B;](../project/user-access.md).

Wanneer u een milieu schrapt, wordt het milieu geplaatst aan _inactief_. De code is nog beschikbaar in de tak van het Git, maar bevat niet meer de diensten of het gegevensbestand. Als u de omgeving volledig wilt verwijderen, moet u ook de bijbehorende externe Git-vertakking verwijderen.

**om een milieu** te schrappen:

1. Wijzig op uw lokale werkstation de projectmap.

1. Updates ophalen van de externe server.

   ```bash
   git fetch
   ```

1. Verwijder de omgevingsvertakking.

   ```bash
   magento-cloud environment:delete <environment-ID>
   ```

   U kunt desgewenst meer dan één omgeving tegelijk verwijderen door meerdere milieu-id&#39;s toe te voegen aan de opdracht Verwijderen.

   ```bash
   magento-cloud environment:delete <environment-1-ID> <environment-2-ID>
   ```

1. Reageer op de vragen om de lokale omgeving en de bijbehorende externe omgeving te verwijderen.

   ```
   The environment <environment-ID> is currently active: deleting it will delete all associated data.
   Are you sure you want to delete the environment <environment-ID>? [Y/n]
   ```

   Het schrappen van het milieu plaatst het in een _inactieve_ staat.

   ```
   Delete the remote Git branch too? [Y/n]
   ```

   Als u de externe Git-vertakking verwijdert, wordt de omgeving van het project verwijderd.

1. Wacht tot de omgeving is verwijderd.

   ```
   Deleting environment <environment-ID>
   Waiting for the activity...
     Deleting environment <project-id>-<environment-ID>-xxxxxx
   
     [============================]  1 min (complete)
   Activity ID succeeded
   Deleted remote Git branch <environment-ID>
   Run git fetch --prune to remove deleted branches from your local cache.
   ```

>[!TIP]
>
>Gebruik de opdracht `magento-cloud environment:activate` om een niet-actieve omgeving te activeren.

## Interactie met externe omgevingen

Nadat u [&#x200B; opstellingsSSH sleutels &#x200B;](../development/secure-connections.md), kunt u [&#x200B; van uw lokale werkruimte met een ver milieu &#x200B;](../development/secure-connections.md#connect-to-a-remote-environment) verbinden en met uw projectdiensten in wisselwerking staan en montages wijzigen.
