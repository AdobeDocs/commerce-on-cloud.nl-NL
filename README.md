---
source-git-commit: b151aac666510594751937e80dc3d9db4ede41b7
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---
# Adobe Commerce on Cloud Infrastructure

Deze site bevat de meest recente ontwikkelaarsdocumentatie voor Commerce on Cloud Infrastructure.

- [&#x200B; Commerce op de Gids van de Infrastructuur van de Wolk &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-on-cloud/user-guide/overview)
- [&#x200B; krijgen Begonnen met Commerce &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-on-cloud/start/overview) op de infrastructuur van de Wolk

## Adobe Open Source-gedragscode

Dit project heeft de [&#x200B; Adobe Open Code van Source van Gedrag &#x200B;](code-of-conduct.md) goedgekeurd. Zie het artikel [Bijdragen](contributing.md) voor meer informatie.

## Over je bijdragen aan Adobe-inhoud

Zie de [&#x200B; Gids van de Medewerker van de Docent van Adobe &#x200B;](https://experienceleague.adobe.com/nl/docs/contributor/contributor-guide/introduction).

Hoe u een bijdrage levert, hangt af van wie u bent en van het soort wijzigingen dat u wilt bijdragen:

### Kleine wijzigingen

Als u minder belangrijke updates bijdraagt, bezoek het artikel en klik het terugkoppelen gebied dat bij de bodem van het artikel verschijnt, klik **Gedetailleerde terugkoppelt opties**, en klik dan **Voorstellen en** uitgeven om naar het prijsonderdrukkingsbrondossier op GitHub te gaan. Gebruik GitHub UI om uw updates te maken.

Kleine correcties of verduidelijkingen die u ter documentatie en codevoorbeelden in dit antwoord aanbrengt, worden behandeld in de gebruiksvoorwaarden van Adobe.

### Belangrijke wijzigingen of nieuwe artikelen van leden van de gemeenschap

Als u deel uitmaakt van de Adobe-community en u een nieuw artikel wilt maken of belangrijke wijzigingen wilt indienen, gebruikt u het tabblad Issues in de Git-opslagplaats om een uitgave in te dienen die een gesprek met het documentatieteam kan beginnen. Als u eenmaal akkoord bent gegaan met een abonnement, moet u samenwerken met een medewerker om die nieuwe inhoud mee te brengen via een combinatie van werk in de openbare en particuliere opslagruimten.

### Belangrijke wijzigingen van werknemers van Adobe

Als u een technisch schrijver, programmamanager, of ontwikkelaar van het productteam voor een oplossing van Adobe Experience Cloud bent en het uw baan is om tot technische artikelen bij te dragen of te schrijven, zou u de privé bewaarplaats bij `https://git.corp.adobe.com/AdobeDocs` moeten gebruiken.

## Gereedschappen en instellen

Communautaire contribuanten kunnen GitHub UI voor basishet uitgeven of vork gebruiken het repo om belangrijke bijdragen te leveren.

Zie de [&#x200B; Gids van de Medewerker van de Docent van Adobe &#x200B;](https://experienceleague.adobe.com/nl/docs/contributor/contributor-guide/introduction) voor details.

## Hoe te om prijsdaling te gebruiken om uw onderwerp te formatteren

Alle artikelen in deze repository gebruiken GitHub gearomatiseerde prijsopgave. Als u niet vertrouwd bent met markering, zie:

- [&#x200B; Grondbeginselen van de Prijsverlaging &#x200B;](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [&#x200B; Afdrukbare prijsdaling &#x200B;](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

## Sjablonen

Voor sommige onderwerpen, gebruiken wij gegevensdossiers en malplaatjes om gepubliceerde inhoud te produceren. De gevallen van het gebruik voor deze benadering omvatten:

- Grote sets met programmatisch gegenereerde inhoud publiceren
- Het verstrekken van één enkele bron van waarheid voor klanten over veelvoudige systemen die machine-leesbare dossierformaten, zoals YAML, voor integratie vereisen (b.v., de hulpmiddelen van de wolk CLI, de dienstconfiguraties)

Voorbeelden van sjablooninhoud zijn onder andere:

- [Cloud CLI-verwijzing](help/templated/cloud-cli-ref.md)
- [Cloud-pakketten](help/templated/cloud-packages.md)
- [Referentie ECE-gereedschappen](help/templated/ece-tools.md)
- [PHP-extensies voor cloud](help/templated/php-extensions-cloud.md)

### Sjablooninhoud genereren

In het algemeen, moeten de meeste schrijvers slechts een versieversie aan de de productbeschikbaarheid en lijsten van de systeemvereisten toevoegen. Het onderhoud voor alle andere sjablooninhoud wordt automatisch of beheerd door een toegewezen teamlid. Deze instructies zijn bedoeld voor de meeste schrijvers.

>**NOTA:**
>
>- Voor het genereren van gesjabloonde inhoud moet u op de opdrachtregel in een terminal werken.
>- Ruby moet zijn geïnstalleerd om het renderscript uit te voeren. Zie [_jekyll/.ruby-version ] (_jekyll/.ruby-version) voor de vereiste versie.

Zie het volgende voor een beschrijving van de bestandsstructuur voor sjablooninhoud:

- `_jekyll`—Bevat sjablonen voor onderwerpen en vereiste elementen
- `_jekyll/_data`—Bevat de machineleesbare bestandsindelingen die worden gebruikt om sjablonen te renderen
- `_jekyll/templated`—Bevat op HTML gebaseerde sjabloonbestanden die de taal voor vloeiende sjablonen gebruiken
- `help/_includes/templated`—Bevat de gegenereerde uitvoer voor sjablooninhoud in `.md` -bestandsindeling zodat deze kan worden gepubliceerd in Experience League-onderwerpen; het renderscript schrijft automatisch gegenereerde uitvoer naar deze map voor u

Sjablooninhoud bijwerken:

1. Open een gegevensbestand in de map `_jekyll/_data` in de teksteditor. Bijvoorbeeld:

   - [&#x200B; Cloud CLI verwijzing &#x200B;](help/templated/cloud-cli-ref.md): `_jekyll/_data/cloud-cli-ref.yaml`
   - [&#x200B; de pakketten van de Wolk &#x200B;](help/templated/cloud-packages.md): `_jekyll/_data/cloud-packages.yaml`
   - [&#x200B; ECE hulpmiddelverwijzing &#x200B;](help/templated/ece-tools.md): `_jekyll/_data/ece-tools.yaml`

2. Gebruik de bestaande YAML-structuur om items te maken.

3. Navigeer naar de map `_jekyll` .

   ```bash
   cd _jekyll
   ```

4. Genereer sjablooninhoud en schrijf de uitvoer naar de map `help/_includes/templated` .

   ```bash
   bundle exec rake render
   ```

   >**NOTA:** u moet het manuscript van de `_jekyll` folder in werking stellen. Als dit de eerste keer is om het script uit te voeren, moet u Ruby-afhankelijkheden eerst installeren met de opdracht `bundle install` . De lijntaken worden geleverd door de `adobe-comdox-exl-rake-tasks` gem voor betere onderhoudbaarheid in alle Adobe Commerce-documentatieruimten.

5. Navigeer terug naar de map `root` .

   ```bash
   cd ..
   ```

6. Controleer of de verwachte `help/_includes/templated` -bestanden zijn gewijzigd.

   ```bash
   git status
   ```

   U zou output gelijkend op het volgende moeten zien:

   ```bash
   modified:   _data/cloud-cli-ref.yaml
   modified:   help/_includes/templated/cloud-cli-ref.md
   ```

7. Druk op de wijzigingen.

   ```bash
   git add .
   git commit -m "descriptive message of the intended commit"
   git push
   ```

Zie de documentatie van Jekyll voor meer details over [&#x200B; Dossiers van Gegevens &#x200B;](https://jekyllrb.com/docs/datafiles), [&#x200B; Vloeiende filters &#x200B;](https://jekyllrb.com/docs/liquid/filters/), en andere eigenschappen.

## Beschikbare taken

Deze gegevensopslagruimte gebruikt taken die door de `adobe-comdox-exl-rake-tasks` gem worden geleverd. Voer de volgende handelingen uit om alle beschikbare taken weer te geven:

```bash
cd _jekyll
bundle exec rake --tasks
```

## Koppelingen vooraf toewijzen voor optimalisatie van afbeeldingen

Deze opslagplaats omvat geautomatiseerde haken die vooraf worden vastgelegd en die afbeeldingen optimaliseren voordat ze worden vastgelegd. **Alle contribuanten zouden deze haken** moeten toelaten om verenigbare beeldoptimalisering en verminderde bewaarplaatsgrootte te verzekeren.

### Snelle installatie

Nadat u de opslagplaats hebt gekloond, voert u het volgende uit:

```bash
.githooks/setup-hooks.sh
```

### Wat de haken doen

- Gelaagde afbeeldingsbestanden automatisch detecteren (PNG, JPG, JPEG, GIF, SVG)
- `image_optim` uitvoeren om afbeeldingen te comprimeren en te optimaliseren
- Geoptimaliseerde afbeeldingen automatisch opnieuw plaatsen
- Zorg ervoor dat alle toegewezen images correct zijn geoptimaliseerd

### Voordelen

- Beperkte grootte opslagplaats
- Snellere paginabelasting voor documentatie
- Consistente beeldkwaliteit voor alle contribuanten
- Geen handmatige optimalisatie vereist

Zie [`.githooks/README.md`](.githooks/README.md) voor gedetailleerde installatie-instructies, probleemoplossing en configuratie.
