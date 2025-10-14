---
title: GitHub-integratie
description: Leer hoe te om uw Adobe Commerce op het project van de wolkeninfrastructuur met GitHub te integreren.
feature: Cloud, Integration
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---

# GitHub-integratie

De integratie GitHub laat u toe om uw Adobe Commerce op de milieu&#39;s van de wolkeninfrastructuur direct van uw bewaarplaats te beheren GitHub. De integratie beheert inhoud reeds in GitHub en synchroniseert met uw Adobe Commerce op de bewaarplaats van de code van de wolkeninfrastructuur. In wezen, wordt de codebewaarplaats een spiegel van de bewaarplaats GitHub.

{{private-repository}}

Dankzij deze integratie kunt u:

- Een omgeving maken wanneer u een vertakking maakt
- Implementeer de omgeving opnieuw wanneer u een pull-verzoek samenvoegt
- De omgeving verwijderen wanneer u de vertakking verwijdert

U moet een teken GitHub en een webhaak verkrijgen om het proces voort te zetten.

## Vereisten

- Beheerderstoegang tot de Adobe Commerce in het infrastructuurproject voor de cloud
- GitHub-opslagplaats
- Het persoonlijke toegangstoken van GitHub

## Een GitHub-token genereren

Creeer een klassiek persoonlijk toegangstoken in de ontwikkelaarmontages van GitHub. U moet een lid van een groep met schrijven-toegang tot de bewaarplaats zijn GitHub, zodat u _duw_ aan de bewaarplaats kunt. Neem het volgende bereik op bij het maken van uw token:

- `admin:repo_hook`—Webhaken maken
- `repo`—Integreren met uw gegevensopslagruimte
- `read:org`—Integreer met de opslagplaats van uw organisatie

Zie [&#x200B; GitHub: creeer &#x200B;](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

## De opslagplaats voorbereiden

Clone uw Adobe Commerce op het project van de wolkeninfrastructuur van een bestaand milieu en migreer de projecttakken aan een nieuwe, lege bewaarplaats GitHub, die de zelfde taknamen bewaart. Het is kritiek **om een identieke boom van het Git te behouden, zodat u geen bestaande milieu&#39;s of takken in uw Adobe Commerce op het project van de wolkeninfrastructuur verliest.**

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
   magento-cloud project:get <project-ID>
   ```

1. Voeg uw bewaarplaats GitHub als ver toe.

   ```bash
   git remote add origin git@github.com:<user-name>/<repo-name>.git
   ```

   De standaardnaam voor de externe verbinding kan `origin` of `magento` zijn. Als `origin` bestaat, kunt u een verschillende naam kiezen of u kunt de bestaande verwijzing een andere naam geven of verwijderen. Zie [&#x200B; git-verre documentatie &#x200B;](https://git-scm.com/docs/git-remote).

1. Verifieer dat u ver GitHub correct toevoegde.

   ```bash
   git remote -v
   ```

   Verwacht antwoord:

   ```
   origin git@github.com:<user-name>/<repo-name>.git (fetch)
   origin git@github.com:<user-name>/<repo-name>.git (push)
   ```

1. Duw de projectdossiers aan uw nieuwe bewaarplaats GitHub. Vergeet niet alle vertakkingsnamen gelijk te houden.

   ```bash
   git push -u origin master
   ```

   Als u met een nieuwe bewaarplaats GitHub begint, kunt u de `-f` optie moeten gebruiken, omdat de verre bewaarplaats niet uw lokale exemplaar aanpast.

1. Verifieer dat uw bewaarplaats GitHub al uw projectdossiers bevat.

## De integratie met GitHub inschakelen

Alvorens u begint, moeten uw projectcode en milieu&#39;s in de bewaarplaats zijn GitHub. Na het toelaten van de integratie, wordt de bewaarplaats GitHub de codebron. Als u code verandert in de originele `magento` bewaarplaats, wordt het overschreven door de integratie wanneer u codeveranderingen in uw bewaarplaats GitHub duwt.

Het volgende laat de integratie GitHub toe en verstrekt een nuttige URL om te gebruiken wanneer het creëren van een webhaak.

>[!WARNING]
>
>Het volgende bevel beschrijft _alle_ code in uw Adobe Commerce op het project van de wolkeninfrastructuur met code van uw bewaarplaats GitHub, die alle takken, met inbegrip van de `production` tak omvat. Deze handeling gebeurt onmiddellijk en kan niet ongedaan worden gemaakt. Als beste praktijken, is het belangrijk om alle takken van uw Adobe Commerce op het project van de wolkeninfrastructuur te klonen en hen te duwen aan uw bewaarplaats GitHub **alvorens** de integratie GitHub toe te voegen.

U kunt verkiezen om door de CLI herinneringen te stappen gebruikend `magento-cloud integration:add` of u kunt het integratiebevel met de volgende opties bouwen:

| Optie | Vereist? | Beschrijving |
| ----------------------- | --------- | --------------------------------- |
| `--base-url` | Ja | De basis-URL van de serverinstallatie, die `https://github.com/` of een aangepast item kan zijn. Laat deze optie weg als uw gegevensopslagruimte wordt gehost met openbare Github of als uw gegevensopslagruimte niet wordt gehost op particuliere servers. Laat deze optie weg als uw gegevensopslagplaats URL aan `https://github.com/{account}/{repository-name}` gelijkaardig is. Dit kan tot fouten zoals `Unable to connect to GitHub: repository not found` leiden. |
| `--token` | Ja | Het persoonlijke toegangstoken dat u voor GitHub produceerde |
| `--repository` | Ja | De naam van de gegevensopslagruimte: `owner-or-organisation/repository` |
| `--build-pull-requests` | Optioneel | Instrueert Adobe Commerce op wolkeninfrastructuur om op te stellen nadat u een trekkrachtverzoek samenvoegt (`true` door gebrek) |
| `--fetch-branches` | Optioneel | Zorgt ervoor dat Adobe Commerce op cloudinfrastructuur vertakkingen bijhoudt en implementeert nadat u een vertakking hebt bijgewerkt (`true` standaard) |
| `--prune-branches` | Optioneel | Vertakkingen verwijderen die niet op de externe server bestaan (`true` standaard) |

Er zijn veel meer opties en u kunt deze weergeven met de optie Help:

```bash
magento-cloud integration:add --help
```

**om de integratie GitHub** toe te laten:

1. De integratie inschakelen.

   ```bash
   magento-cloud integration:add --type=github --project=<project-ID> --token=<your-GitHub-token> {--repository=USER/REPOSITORY | --repository=ORGANIZATION/REPOSITORY} [--build-pull-requests={true|false} --fetch-branches={true|false}
   ```

   **Voorbeeld 1**: Laat de integratie GitHub voor een persoonlijke, privé bewaarplaats toe:

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=myUserName/myrepo
   ```

   **Voorbeeld 2**: Laat de integratie GitHub voor een organisatiebewaarplaats toe:

   ```bash
   magento-cloud integration:add --type=github --project=ov58dlacU2e --base-url=https://github.com --token=<token> --repository=Magento/teamrepo
   ```

1. Voer de vereiste informatie in wanneer u hierom wordt gevraagd.

1. Kopieer **Payload URL** getoond door de terugkeeroutput.

   ```
   Created integration <integration-ID> (type: github)
   Repository: myUserName/myrepo
   Build PRs: yes
   Fetch branches: yes
   Payload URL: https://us.magento.cloud/api/projects/<project-id>/integrations/wO8a0eoamxwcg/hook
   ```

## Webhaak toevoegen in GitHub

Om gebeurtenissen-zulke zoals een duw-met uw server van de it van de Plaats van de Wolk mee te delen, moet u een webhaak voor uw bewaarplaats van GitHub tot stand brengen:

1. In uw bewaarplaats GitHub, klik de **Montages** tabel.

1. In de linkernavigatiebar, klik **Webhooks**.

1. In de _ruit Webhooks_, klik **webhaak** toevoegen.

1. In _Webhooks/voeg webhaak_ vorm toe, geef de volgende gebieden uit:

   - **Payload URL**: Ga URL in teruggekeerd toen u de integratie GitHub toeliet.
   - **Type van Inhoud**: Kies **toepassing/json** van de lijst.
   - **Geheim**: Ga een verificatiegeheim in.
   - **Welke gebeurtenissen wilt u deze webhaak teweegbrengen?**: Selecteer **verzend me alles**.
   - Selecteer **Actieve** checkbox.

1. Klik **toevoegen webhaak**.

## Integratie testen

Na het vormen van de integratie GitHub, kunt u verifiëren dat de integratie operationeel gebruikend `magento-cloud` CLI is:

```bash
magento-cloud integration:validate
```

Of u kunt het testen door een eenvoudige verandering in uw bewaarplaats te duwen GitHub.

1. Maak een testbestand.

   ```bash
   touch test.md
   ```

1. Verbind en duw de verandering in uw bewaarplaats GitHub.

   ```bash
   git add . && git commit -m "Testing GitHub integration" && git push
   ```

1. Meld u aan bij de [[!DNL Cloud Console]](../project/overview.md) en controleer of uw commit-bericht wordt weergegeven en of uw project wordt geïmplementeerd.

## Integratie verwijderen

U kunt de integratie van GitHub uit uw project veilig verwijderen zonder uw code te beïnvloeden.

**om de integratie te verwijderen GitHub**:

1. Meld u vanaf de terminal aan bij uw Adobe Commerce voor een infrastructuurproject voor de cloud.

1. Maak een lijst van uw integratie. U hebt de integratie-id van GitHub nodig om de volgende stap te voltooien.

   ```bash
   magento-cloud integration:list
   ```

1. De integratie verwijderen.

   ```bash
   magento-cloud integration:delete <int-ID>
   ```

Ook, kunt u de integratie verwijderen GitHub door aan uw rekening te registreren GitHub en de Webhaak in _Webhooks_ tabel van de bewaarplaats _Montages_ te verwijderen.
