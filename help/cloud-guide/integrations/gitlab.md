---
title: GitLab-integratie
description: Leer hoe u uw Adobe Commerce in een cloud-infrastructuurproject kunt integreren met GitLab.
feature: Cloud, Integration
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# GitLab-integratie

U kunt een gegevensopslagplaats vormen GitLab om automatisch een milieu te bouwen en op te stellen wanneer u codeveranderingen duwt. Deze integratie synchroniseert uw GitLab-opslagplaats met uw Adobe Commerce op cloudinfratuuropportaccount.

{{private-repository}}

Dankzij deze integratie kunt u:

- Een omgeving maken wanneer u een vertakking maakt
- Implementeer de omgeving opnieuw wanneer u een pull-verzoek samenvoegt
- De omgeving verwijderen wanneer u de vertakking verwijdert

U moet een GitLab-token en een webhaak verkrijgen om het proces voort te zetten.

## Vereisten

- Beheerderstoegang tot de Adobe Commerce in het infrastructuurproject voor de cloud
- [`magento-cloud` CLI &#x200B;](../dev-tools/cloud-cli-overview.md) in uw lokale omgeving
- Een GitLab-account
- Een GitLab persoonlijke toegangstoken met schrijftoegang tot de GitLab-opslagplaats, moet het geselecteerde bereik ten minste zijn: `api` en `read_repository` .

## De opslagplaats voorbereiden

Clone your Adobe Commerce on cloud Infrastructure project from an existing environment and migrate the project branches to a new, empty GitLab repository, preserve the same tak names. Het is kritiek **om een identieke boom van het Git te behouden, zodat u geen bestaande milieu&#39;s of takken in uw Adobe Commerce op het project van de wolkeninfrastructuur verliest.**

1. Meld u vanaf de terminal aan bij uw Adobe Commerce voor een infrastructuurproject voor de cloud.

   ```bash
   magento-cloud login
   ```

1. Maak een lijst van uw projecten en kopieer projectidentiteitskaart

   ```bash
   magento-cloud project:list
   ```

1. Kloont het project naar uw lokale omgeving.

   ```bash
   magento-cloud project:get <project-id>
   ```

1. Voeg uw GitLab-opslagplaats toe als een externe opslagplaats (ervan uitgaande dat GitLab wordt gebruikt in de SaaS-versie).

   ```bash
   git remote add origin git@gitlab.com:<user-name>/<repo-name>.git
   ```

   De standaardnaam voor de externe verbinding kan `origin` of `magento` zijn. Als `origin` bestaat, kunt u een verschillende naam kiezen of u kunt de bestaande verwijzing een andere naam geven of verwijderen. Zie [&#x200B; git-verre documentatie &#x200B;](https://git-scm.com/docs/git-remote).

1. Controleer of u de GitLab-afstandsbediening correct hebt toegevoegd.

   ```bash
   git remote -v
   ```

   Verwacht antwoord:

   ```
   origin git@gitlab.com:<user-name>/<repo-name>.git (fetch)
   origin git@gitlab.com:<user-name>/<repo-name>.git (push)
   ```

1. Verplaats de projectbestanden naar de nieuwe GitLab-opslagplaats. Vergeet niet alle vertakkingsnamen gelijk te houden.

   ```bash
   git push -u origin master
   ```

   Als u begint met een nieuwe GitLab-opslagplaats, moet u mogelijk de optie `-f` gebruiken, omdat de externe opslagplaats niet overeenkomt met uw lokale kopie.

1. Controleer of uw GitLab-opslagplaats al uw projectbestanden bevat.

## De integratie met GitLab inschakelen

Gebruik de opdracht `magento-cloud integration` om de integratie met GitLab in te schakelen en de Payload-URL voor de GitLab-webhaak te gebruiken om updates van GitLab naar uw Adobe Commerce te verzenden via het infrastructuurproject in de cloud.

```bash
magento-cloud integration:add --type=gitlab --project=<project-ID> --token=<your-GitLab-token> [--base-url=<GitLab-url> --server-project=<GitLab-project> --build-merge-requests={true|false} --merge-requests-clone-parent-data={true|false} --fetch-branches={true|false} --prune-branches={true|false}]
```

| Optie | Beschrijving |
| ------ | ----------- |
| `<project-ID>` | Projectid Adobe Commerce on cloud Infrastructure |
| `<your-GitLab-token>` | Het persoonlijke toegangstoken dat u voor GitLab produceerde |
| `--base-url` | URL van GitLab (`https://gitlab.com/` als GitLab in zijn versie SaaS wordt gebruikt) |
| `--server-project` | Projectnaam in GitLab (onderdeel na de basis-URL) |
| `--build-merge-requests` | Een _facultatieve_ parameter die Adobe Commerce op wolkeninfrastructuur opdraagt om een nieuw milieu voor elk fusieverzoek (`true` door gebrek te bouwen) |
| `--merge-requests-clone-parent-data` | Een _facultatieve_ parameter die Adobe Commerce op wolkeninfrastructuur opdraagt om de gegevens van het oudermilieu voor fusieverzoeken (`true` door gebrek te klonen) |
| `--fetch-branches` | Een _facultatieve_ parameter die Adobe Commerce op wolkeninfrastructuur veroorzaakt om alle takken van ver (als inactieve milieu&#39;s) te halen (`true` door gebrek) |
| `--prune-branches` | Een _facultatieve_ parameter die Adobe Commerce op wolkeninfrastructuur opdraagt om takken te schrappen die niet op ver (`true` door gebrek bestaan) |

>[!WARNING]
>
>Het `magento-cloud integration` bevel beschrijft _alle_ code in uw Adobe Commerce op het project van de wolkeninfrastructuur met de code van uw bewaarplaats GitLab. Dit geldt voor alle vertakkingen, inclusief de `production` -vertakking. Deze handeling gebeurt onmiddellijk en kan niet ongedaan worden gemaakt. Als beste praktijken, is het belangrijk om al uw takken van uw Adobe Commerce op het project van de wolkeninfrastructuur te klonen en hen te duwen aan uw bewaarplaats GitLab alvorens de integratie GitLab toe te voegen.

**om de integratie GitLab** toe te laten:

1. Voeg vanaf de terminal de GitLab-integratie toe aan uw Adobe Commerce-project voor cloudinfrastructuur:

   ```bash
   magento-cloud integration:add --type gitlab --project=3txxjf32gtryos --token=qVUfeEn4ouze7A7JH --base-url=https://gitlab.com/ --server-project=my-agency/project-name --build-merge-requests=false --merge-requests-clone-parent-data=false --fetch-branches=true --prune-branches=true
   ```

1. Voer `y` in wanneer u daarom wordt gevraagd om de integratie toe te voegen.

   ```
   Warning: adding a 'gitlab' integration will automatically synchronize code from the external Git repository.
   This means it can overwrite all the code in your project.
   Are you sure you want to continue? [y/N] y
   ```

1. Kopieer **Hook URL** die door de terugkeeroutput wordt getoond.

   ```
   Hook URL: https://eu-3.magento.cloud/api/projects/3txxjf32gtryos/integrations/eolmpfizzg9lu/hook
   Created integration eolmpfizzg9lu (type: gitlab)
   +----------------------------------+---------------------------------------------------------------------------------------+
   | Property                         | Value                                                                                 |
   +----------------------------------+---------------------------------------------------------------------------------------+
   | id                               | <integration-id>                                                                      |
   | type                             | gitlab                                                                                |
   | token                            | ******                                                                                |
   | base_url                         | https://gitlab.com/                                                                   |
   | project                          | my-agency/project-name                                                                |
   | fetch_branches                   | true                                                                                  |
   | prune_branches                   | true                                                                                  |
   | build_merge_requests             | false                                                                                 |
   | merge_requests_clone_parent_data | false                                                                                 |
   | hook_url                         | https://eu-3.magento.cloud/api/projects/<project-id>/integrations/<integration-id>/hook |
   +----------------------------------+---------------------------------------------------------------------------------------+
   ```

### Webhaak toevoegen in GitLab

Om gebeurtenissen —zoals een duw of fusieverzoeken— met uw server van de Git van de Wolk mee te delen, moet u een webhaak [&#128279;](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html#overview) voor uw bewaarplaats van GitLab  tot stand brengen

1. In uw bewaarplaats GitLab, klik de **Montages** tabel.

1. In de linkernavigatiebar, klik **Webhooks**.

1. In de _vorm Webhooks_, geef de volgende gebieden uit:

   - **URL**: Ga `Hook URL` teruggekeerd in wanneer u de integratie GitLab toeliet.
   - **Geheime token**: Ga indien nodig een verificatiegeheim in.
   - **Trekker**: Controle `Merge request events` en/of `Push events` afhankelijk van uw behoeften.
   - **laat SSL controle** toe: U moet deze optie selecteren.

1. Klik **toevoegen webhaak**.

### Integratie testen

Na het vormen van de integratie GitLab, kunt u verifiëren dat de integratie operationeel is gebruikend `magento-cloud` CLI:

```bash
magento-cloud integration:validate
```

Of u kunt het testen door een eenvoudige verandering in uw bewaarplaats GitLab te duwen.

1. Maak een testbestand.

   ```bash
   touch test.md
   ```

1. Leg de wijziging vast en duw deze naar uw GitLab-opslagplaats.

   ```bash
   git add . && git commit -m "Testing GitLab integration" && git push
   ```

1. Meld u aan bij de [[!DNL Cloud Console]](../project/overview.md) en controleer of uw commit-bericht wordt weergegeven en of uw project wordt geïmplementeerd.

## Een Cloud-vertakking maken

Gebruik de opdracht `magento-cloud` CLI `environment:push` om een nieuwe omgeving te maken en te activeren. Zie [&#x200B; een tak van de Wolk &#x200B;](bitbucket.md#create-a-cloud-branch) creëren.

## Integratie verwijderen

Gebruik de opdracht `magento-cloud` CLI `integration:delete` om de integratie te verwijderen. Zie [&#x200B; de integratie &#x200B;](bitbucket.md#remove-the-integration) verwijderen.
