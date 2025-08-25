---
source-git-commit: d08ef7d46e3b94ae54ee99aa63de1b267f4e94a0
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---
# Bibliotheekbestanden ophalen

Deze map bevat definities van lijntaken die op functionaliteit zijn geordend. Met Omtrekken worden automatisch alle `.rake` -bestanden in deze map geladen.

## Bestandsorganisatie

### `includes.rake`

Bevat alle taken met betrekking tot een include-teken onder de naamruimte `:includes` :

- `includes:maintain_relationships` - Inclusief relaties detecteren en onderhouden
- `includes:maintain_timestamps` - Tijdstempels toevoegen/bijwerken op basis van bestandswijzigingen opnemen
- `includes:maintain_all` - Beide bewerkingen op volgorde uitvoeren

## Hoe het werkt

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
