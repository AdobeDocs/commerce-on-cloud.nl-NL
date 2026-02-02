---
source-git-commit: ee2ed3a78939af36572f0baa6672b2e9f9a2557f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---
# Koppelingen vooraf toewijzen voor optimalisatie van afbeeldingen

Deze map bevat vooraf vastgelegde haken die afbeeldingen automatisch optimaliseren voordat ze worden toegewezen aan de opslagplaats.

## Wat de haken doen

- **ontdekt automatisch** gestagte beelddossiers (PNG, JPG, JPEG, GIF)
- **Uitvoeren`image_optim`** om afbeeldingen te comprimeren en te optimaliseren
- **re-stage geoptimaliseerde beelden** automatisch
- **verzeker alle toegewijde beelden** behoorlijk worden geoptimaliseerd

## Voordelen

- Beperkte grootte opslagplaats
- Snellere paginabelasting voor documentatie
- Consistente beeldkwaliteit voor alle contribuanten
- Geen handmatige optimalisatie vereist

## Vereisten

- Ruby 3.0 of hoger
- Bundler
- Git

## Instellen

### Automatische installatie (aanbevolen)

```bash
.githooks/setup-hooks.sh
```

### Handmatige installatie

```bash
git config core.hooksPath .githooks
chmod +x .githooks/*
```

### Volledige projectinstelling

1. De opslagplaats klonen:

   ```bash
   git clone <repository-url>
   cd commerce-admin.en
   ```

2. Enable pre-commit hooks:

   ```bash
   .githooks/setup-hooks.sh
   ```

3. Jekyll-afhankelijkheden installeren:

   ```bash
   cd _jekyll
   bundle install
   ```

## De haken testen

1. Een afbeeldingsbestand toevoegen aan uw opslagplaats
2. Werkgebied: `git add <image-file>`
3. Probeer vast te leggen: `git commit -m 'test'`
4. De haak moet de afbeelding automatisch optimaliseren

### Verwachte uitvoer

```bash
Found 1 staged image(s). Running optimization...
Optimizing: path/to/your/image.png
Re-staged optimized image: path/to/your/image.png
Image optimization complete!
```

## Richtlijnen voor afbeeldingen

- **PNG**: Gebruik voor screenshots en elementen UI (zal automatisch worden geoptimaliseerd)
- **JPEG**: Gebruik voor foto&#39;s (zal automatisch worden geoptimaliseerd)
- **GIF**: Gebruik voor animaties (zal automatisch worden geoptimaliseerd)
- **SVG**: Gebruik voor pictogrammen en eenvoudige grafiek (niet verwerkt door haken, begaat zoals-is)

De haken die vooraf worden vastgelegd, optimaliseren bij toewijzen automatisch PNG-, JPEG- en GIF-afbeeldingen.

## Handmatige optimalisatie

Voor handmatige optimalisatie van afbeeldingen:

```bash
cd _jekyll
bundle exec rake images:optimize path=../path/to/images
```

## Configuratie

De haken gebruiken het configuratiedossier `_jekyll/.image_optim.yml` om optimalisatie montages aan te passen:

- **PNG**: Gebruik `advpng`, `optipng`, en `pngquant`
- **JPEG**: Gebruik `jhead`, `jpegoptim`, en `jpegtran`
- **GIF**: Gebruik `gifsicle`
- **SVG**: Niet verwerkt (uitgesloten van opsporing om vectorgrafiek en animaties te bewaren)

## Problemen oplossen

### Hook niet actief

- Configuratie haak controleren: `git config core.hooksPath`
- Controleer of het haakbestand uitvoerbaar is: `chmod +x .githooks/pre-commit`
- Controleer of u zich in de juiste opslagplaats bevindt met de map `_jekyll`

### Optimalisatie mislukt

- Controleren of `bundle install` is uitgevoerd in de map `_jekyll`
- Controleer of de `adobe-comdox-exl-rake-tasks` gem is geïnstalleerd (biedt `image_optim` )
- Controleer het `.image_optim.yml` configuratiebestand

### Prestatieproblemen

- Aantal verbindingen aanpassen in `_jekyll/.image_optim.yml`
- Omgevingsvariabele `DEBUG=1` instellen voor gedetailleerde foutinformatie

## Hoe werkt het

1. **pre-begaat trekker**: Wanneer u `git commit` in werking stelt, voert de haak automatisch uit
2. **de opsporing van het Beeld**: Scant gefaseerde dossiers voor beelduitbreidingen
3. **Optimalisering**: Looppas `image_optim` op elk gestaagd beeld
4. **het Wederopvoeren**: Voegt automatisch geoptimaliseerde beelden terug naar het het opvoeren gebied toe
5. **begaat opbrengst**: Als optimalisering slaagt, begaat normaal

## Ondersteunde afbeeldingsindelingen

- **PNG** (`.png`) - Lossless en verliesvrije compressie
- **JPEG** (`.jpg`, `.jpeg`) - Lossy compressie met meta-gegevensschoonmaak
- **GIF** (`.gif`) - Animatie en statische optimalisering
- **SVG** (`.svg`) - niet verwerkt door haken (begaat as-is om kwaliteit te bewaren)

## Aanbevolen procedures

1. **Test de haak**: Probeer het begaan van een klein beeld eerst om het te verzekeren werkt
2. **veranderingen van het Overzicht**: Controleer git diff om optimalisatieresultaten te zien
3. **prestaties van de Monitor**: De grote beelden kunnen tijd vergen om te optimaliseren
4. **de controle van de Versie**: Hooks worden opgeslagen in deze `.githooks/` folder

## Ondersteuning

Voor problemen met de haken die voorafgaan:

1. Controleer de hakoutput voor foutenmeldingen
2. Controleren of de `image_optim` -instelling werkt
3. Test eerst met handmatige lijntaken
4. Herzie de hakenlogboeken en configuratie
5. Controleer de configuratie van de haken: `git config core.hooksPath`
