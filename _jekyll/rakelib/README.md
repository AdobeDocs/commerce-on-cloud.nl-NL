---
source-git-commit: f75dbbc9726ff21a648b1bb3d8f06cb45a5d6b08
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---
# Bibliotheekbestanden ophalen

Deze map bevat definities van lijntaken die op functionaliteit zijn geordend. Met Omtrekken worden automatisch alle `.rake` -bestanden in deze map geladen.

## Bestandsorganisatie

### `adobe-docs-tasks.rake`

Bevat veelvoorkomende taken op het gebied van vereisten, gedeelde functionaliteit en taken zonder naamgeving voor Adobe Commerce in de Experience League-documentatieopslagplaats:

- `whatsnew` - Gegevens genereren voor nieuwsoverzicht (standaard: sinds laatste update)
- `render` - Geslaagde bestanden renderen en include-bestanden onderhouden

### `includes.rake`

Bevat beheertaken die zijn geordend in de naamruimte `:includes` :

- `includes:maintain_relationships` - Inclusief relaties in markeringsbestanden detecteren en onderhouden
- `includes:maintain_timestamps` - Tijdstempels toevoegen/bijwerken op basis van bestandswijzigingen opnemen
- `includes:maintain_all` - Beide bewerkingen op volgorde uitvoeren
- `includes:unused` - Ongebruikte include-bestanden zoeken

### `images.rake`

Bevat taken voor afbeeldingsbeheer die zijn ingedeeld in de naamruimte `:images` :

- `images:optimize` - Afbeeldingen optimaliseren in gewijzigde, niet-toegewezen bestanden
- `images:unused` - Ongebruikte afbeeldingen zoeken in het project

## Hoe werkt het

Met Omtrekken worden alle `.rake` -bestanden in de map `rakelib/` automatisch gedetecteerd en geladen. Op die manier kunnen wij:

1. **organiseer taken door functionaliteit** - Groepeer verwante taken samen
2. **houd het belangrijkste Rakefile schoon** - concentreer zich op kernprojecttaken
3. **voegt gemakkelijk nieuwe taakgroepen** toe - creeer enkel nieuwe `.rake` dossiers
4. **handhaaf scheiding van zorgen** - Elk dossier behandelt een specifiek domein

## Nieuwe taakgroepen toevoegen

Een nieuwe groep verwante taken toevoegen:

1. Een nieuw `.rake` -bestand maken in deze map
2. Een beschrijvende naamruimte gebruiken (bijvoorbeeld `namespace :images` voor taken met betrekking tot afbeeldingen)
3. Uw taken binnen de naamruimte definiëren
4. Rake laadt deze automatisch

## Voorbeeldstructuur

```ruby
namespace :your_namespace do
  desc 'Description of what this task does'
  task :task_name do
    # Task implementation
  end
end
```

## Gebruik

Taken zijn direct na het maken beschikbaar:

```bash
rake your_namespace:task_name
```

## Voordelen

- **Modulariteit**: Elk dossier concentreert zich op een specifiek gebied
- **Handhaving**: Gemakkelijker om specifieke taakgroepen te vinden en te wijzigen
- **Schaalbaarheid**: Kan vele taakgroepen toevoegen zonder het belangrijkste Rakefile te verwarren
- **Ontwikkeling van het Team**: De verschillende ontwikkelaars kunnen aan verschillende taakgroepen werken
