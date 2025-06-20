---
title: Back-upbeheer
description: Leer hoe u handmatig een back-up voor uw Adobe Commerce-infrastructuurproject in de cloud kunt maken en herstellen.
feature: Cloud, Paas, Snapshots, Storage
exl-id: e73a57e7-e56c-42b4-aa7b-2960673a7b68
source-git-commit: 13cb5e3231c2173d5687aec3e4e64ecc154ee962
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Back-upbeheer

U kunt op elk gewenst moment een handmatige back-up van de actieve Starter-omgeving maken met de knop **[!UICONTROL Backup]** in de [!DNL Cloud Console] of met de opdracht `magento-cloud snapshot:create` .

Een steun of _momentopname_ is een volledige steun van omgevingsgegevens die alle blijvende gegevens van het runnen van de diensten (gegevensbestand MySQL) en om het even welke dossiers omvat die op de opgezette volumes (var, pub/media, app/etc) worden opgeslagen. De momentopname omvat __ geen code, aangezien de code reeds in de op git-Gebaseerde bewaarplaats wordt opgeslagen. U kunt geen kopie van een opname downloaden.

>[!WARNING]
>
>Zorg dat back-ups doorgaans de inhoud van gekoppelde mappen bevatten, inclusief openbare webmappen zoals `pub/media` , en verplaats back-upuitvoerbestanden niet naar openbare webmappen zoals `pub/media` of `pub/static` .

De reserve/momentopnamefunctie is **niet** op de Pro het Staging en milieu&#39;s van de Productie van toepassing, die regelmatige steunen voor de doeleinden van de rampenterugwinning door gebrek ontvangen. Verwijs naar [ Pro Steun &amp; de Terugwinning van de Ramp ](../architecture/pro-architecture.md#backup-and-disaster-recovery) voor meer informatie. In tegenstelling tot de automatische levende steunen op de Pro het Staging en milieu&#39;s van de Productie, zijn de steunen **niet** automatisch. Het is _uw_ verantwoordelijkheid om een steun manueel tot stand te brengen of opstelling een kroonbaan om een steun van uw Starter of Pro integratiemilieu&#39;s periodiek tot stand te brengen.

## Een handmatige back-up maken

U kunt een handmatige back-up maken van elke actieve Starter-omgeving en integratie Pro-omgeving vanuit de [!DNL Cloud Console] of een momentopname maken vanuit de Cloud CLI. U moet een [ rol Admin ](../project/user-access.md) voor het milieu hebben.

>[!NOTE]
>
>U kunt een steun van de code op ProProductie en het Opvoeren clusters tot stand brengen door het volgende bevel in de terminal in werking te stellen - die het voor om het even welke omslagen/wegen aanpast die u wilt omvatten/uitsluiten:
>
>```bash
>mkdir -p var/support
>/usr/bin/nice -n 15 /bin/tar -czhf var/support/code-$(date +"%Y%m%d%H%M%p").tar.gz app bin composer.* dev lib pub/*.php pub/errors setup vendor --exclude='pub/media'
>```

**om een gegevensbestandsteun van Pro milieu** tot stand te brengen:

Om een gegevensbestandstortplaats van om het even welk Pro milieu, met inbegrip van het Opvoeren en Productie tot stand te brengen, zie [ een artikel van de Kennisbank van de gegevensbestandstortplaats ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud) creëren.

**om een steun van om het even welke milieu te creëren van de Aanzet gebruikend[!DNL Cloud Console]**:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .
1. Selecteer een omgeving in de projectnavigatiebalk. De omgeving moet actief zijn.
1. In de _mening van Steunen_, klik **[!UICONTROL Backup]**. Deze optie is niet beschikbaar voor een Pro-omgeving.

   ![ Steun ](../../assets/button-backup.png){width="150"}

**om een steun van een integratiemilieu tot stand te brengen gebruikend[!DNL Cloud Console]**:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .
1. Selecteer een integratie-/ontwikkelomgeving in de projectnavigatiebalk. De omgeving moet actief zijn.
1. Selecteer de optie **[!UICONTROL Backup]** in het menu rechtsboven. Deze optie is beschikbaar voor zowel Starter- als Pro-omgevingen.
1. Klik op **[!UICONTROL Yes]** .

**om een momentopname tot stand te brengen gebruikend `magento-cloud` CLI**:

1. Wijzig op uw lokale werkstation de projectmap.
1. Bekijk de omgevingsvertakking voor opname.
1. Maak de opname.

   ```bash
   magento-cloud snapshot:create --live
   ```

   U kunt ook de opdracht `magento-cloud backup` short gebruiken. Met de optie `--live` blijft de omgeving actief om downtime te voorkomen. Voer `magento-cloud snapshot:create --help` in voor een volledige lijst met opties.

   Monsterrespons:

   ```
   Creating a snapshot of develop-branch
   Waiting for the activity ID (User created a backup of develop-branch):
   
   Creating backup of develop-branch
   Created backup my-snapshot
   [============================] 45 secs (complete)
   Activity ID succeeded
   Snapshot name: my-snapshot
   ```

1. Controleer de meest recente momentopnamen.

   ```bash
   magento-cloud snapshot:list
   ```

   De lijst retourneert informatie over de status van de momentopname:

   ```
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

## Een handmatige back-up herstellen

U moet [ toegang Admin ](../project/user-access.md) tot het milieu hebben. U hebt tot **zeven dagen** aan _herstel_ een handsteun. Bij het herstellen van een back-up wordt de code van de huidige git-vertakking niet gewijzigd. Het herstellen van een steun op deze manier is niet van toepassing op Pro het opvoeren en productiemilieu&#39;s; zie [ Pro Steun &amp; de Terugwinning van de Ramp ](../architecture/pro-architecture.md#backup-and-disaster-recovery).

De hersteltijden variëren afhankelijk van de grootte van de database:

- grote database (200+ GB) kan 5 uur in beslag nemen
- middelgrote database (150 GB) kan 2 1/2 uur in beslag nemen
- kleine database (60 GB) kan 1 uur duren

>[!TIP]
>
>Herstellen zonder back-up:
>
>- Om terug naar vorige code terug te rollen of toegevoegde uitbreidingen in een milieu te verwijderen, zie [ Terugschroeven van prijzen code ](#roll-back-code).
>- Om een instabiel milieu te herstellen dat __ geen steun heeft, zie [ een milieu ](../development/restore-environment.md) herstellen.

**om een steun te herstellen gebruikend[!DNL Cloud Console]**:

1. Meld u aan bij de map [[!DNL Cloud Console] ](https://console.adobecommerce.com) .
1. Selecteer een omgeving in de projectnavigatiebalk.
1. In de _mening van Steunen_, kies een steun van de _Opgeslagen_ lijst. De reserveeigenschap is **niet** van toepassing op de Pro milieu&#39;s.
1. In ![ Meer ](../../assets/icon-more.png){width="32"} (_meer_) menu, klik **herstellen**.
1. Herzie Herstellen van reserveinformatie en klik **ja, herstel**.

**om een momentopname te herstellen gebruikend Cloud CLI**:

1. Wijzig op uw lokale werkstation de projectmap.
1. Bekijk de omgevingsvertakking die u wilt herstellen.
1. Alle beschikbare momentopnamen weergeven.

   ```bash
   magento-cloud snapshot:list
   ```

   De lijst retourneert informatie over de beschikbare momentopnamen:

   ```
   Snapshots on the project (project-id), environment develop-branch (type: development):
   +---------------------------+----------------------+------------+
   | Created                   | Snapshot ID          | Restorable |
   +---------------------------+----------------------+------------+
   | 2023-03-08T17:07:01+00:00 | my-snapshot          | true       |
   +---------------------------+----------------------+------------+
   ```

1. Herstel een momentopname gebruikend momentopname identiteitskaart van de lijst.

   ```bash
   magento-cloud snapshot:restore <snapshot-id>
   ```

## Een momentopname voor noodherstel herstellen

Om de Momentopname van de Terugwinning van de Ramp in Pro het Opvoeren en milieu&#39;s van de Productie te herstellen, [ voer direct de gegevensbestandstortplaats van de server ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/restore-a-db-snapshot-from-staging-or-production#meth3) in.

## Code terugdraaien

De steunen en de momentopnamen omvatten __ geen exemplaar van uw code. Uw code is al opgeslagen in de op Git gebaseerde gegevensopslagruimte, zodat u Git-gebaseerde opdrachten kunt gebruiken om code terug te draaien (of terug te draaien). Bijvoorbeeld, gebruik `git log --oneline` om door vorige begaat te scrollen; dan gebruik [`git revert` ](https://git-scm.com/docs/git-revert) om code van te herstellen specifiek begaat.

Ook, kunt u verkiezen om code in een _inactieve_ tak op te slaan. Gebruik git-opdrachten om een vertakking te maken in plaats van `magento-cloud` -opdrachten. Zie over [ bevelen van de Git ](../dev-tools/cloud-cli-overview.md#git-commands) in het Cloud CLI onderwerp.

## Verwante informatie

- [Back-up maken van de database](database-dump.md)
- [ Steun en rampenterugwinning ](../architecture/pro-architecture.md#backup-and-disaster-recovery) voor ProProductie en het Opvoeren clusters
