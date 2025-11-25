---
title: PHP-instellingen
description: Meer informatie over de optimale PHP-instellingen voor de configuratie van Commerce-toepassingen in de cloudinfrastructuur.
feature: Cloud, Configuration, Extensions
exl-id: 83094c16-7407-41fa-ba1c-46b206aa160d
source-git-commit: de50fda78c28a57d76e5c0a4d5dac0f8d4d844a0
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# PHP-instellingen

U kunt kiezen welke [ versie van PHP ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) in uw `.magento.app.yaml` dossier in werking te stellen:

```yaml
name: mymagento
type: php:<version>
```

>[!TIP]
>
>Als u een upgrade uitvoert naar PHP 8.1 en hoger, verwijdert u JSON uit de [`runtime: extensions:` eigenschap ](properties.md#runtime) in het `.magento.app.yaml` -bestand en daarna opnieuw. De JSON-extensie wordt sinds PHP 8.0 geïnstalleerd in de Cloud-omgeving.

## PHP configureren

U kunt de PHP-instellingen aanpassen voor uw omgeving met behulp van een `php.ini` -bestand dat wordt toegevoegd aan de configuratie die wordt onderhouden door Adobe Commerce.

Voeg het `php.ini` -bestand toe aan de hoofdmap van de toepassing (de opslagplaats) in de opslagplaats.

>[!TIP]
>
>Als PHP-instellingen onjuist worden geconfigureerd, kunnen er problemen optreden. Daarom moeten alleen gevorderde beheerders deze opties instellen.

### Limiet voor PHP-geheugen verhogen

Als u de limiet van het PHP-geheugen wilt verhogen, voegt u de volgende instelling toe aan het `php.ini` -bestand:

```ini
memory_limit = 1G
```

Voor het zuiveren, verhoog de waarde tot 2G.

### Configuratie realpath_cache optimaliseren

Stel de volgende `realpath_cache` -instellingen in om de prestaties van de toepassing te verbeteren.

```conf
;
; Increase realpath cache size
;
realpath_cache_size = 10M

;
; Increase realpath cache ttl
;
realpath_cache_ttl = 7200
```

Met deze instellingen kunnen PHP-processen paden naar bestanden in cache plaatsen in plaats van ze voor elke pagina te bekijken die wordt geladen. Zie [ Prestaties die ](https://www.php.net/manual/en/ini.core.php) in de PHP documentatie stempelen.

>[!NOTE]
>
>Voor een lijst van geadviseerde PHP configuratiemontages, zie [ Vereiste PHP montages ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html) in de _gids van de Installatie_.

### Aangepaste PHP-instellingen controleren

Nadat u de `php.ini` wijzigingen in uw Cloud-omgeving hebt aangebracht, kunt u controleren of de aangepaste PHP-configuratie aan uw omgeving is toegevoegd. Gebruik bijvoorbeeld SSH om u aan te melden bij de externe omgeving, geef PHP-configuratiegegevens weer en filter voor de instructie `register_argc_argv` :

```bash
php -i | grep register_argc_ar
```

Voorbeelduitvoer:

```text
register_argc_argv => On => On
```

>[!WARNING]
>
>Als u het Dok van de Wolk voor Commerce voor lokale ontwikkeling gebruikt, zie {de dienstcontainers van 0} Docker [ voor informatie over het gebruiken van een douane ](https://developer.adobe.com/commerce/cloud-tools/docker/containers/service#fpm-container) dossier in een milieu van het Dok.`php.ini`

## Extensies inschakelen

U kunt PHP-extensies in- of uitschakelen in de sectie `runtime:extension` . Bovendien worden de opgegeven extensies beschikbaar in de Docker PHP containers.

>[!IMPORTANT]
>
>Voordat extensies kunnen worden ingeschakeld, is het belangrijk te begrijpen dat de PHP-versie compatibel moet zijn met het besturingssysteem dat het project host. Voor uw projectomgeving is mogelijk een upgrade van het besturingssysteem door het infrastructuurteam vereist voordat u kunt doorgaan.

Voorbeeld in `.magento.app.yaml` bestand:

```yaml
runtime:
    extensions:
        - sockets
        - sodium
        - ssh2
    disabled_extensions:
        - bcmath
        - bz2
        - calendar
        - exif
```

Gebruik SSH om u aan te melden bij een omgeving en geef een overzicht van de PHP-extensies.

```bash
php -m
```

Voor details over een specifieke PHP uitbreiding, zie de [ PHP Lijst van de Uitbreiding ](https://www.php.net/manual/en/extensions.alphabetical.php).

In de volgende tabel worden de ondersteunde PHP-extensies weergegeven wanneer Adobe Commerce wordt geïmplementeerd op het Cloud-platform.

{{$include /help/_includes/templated/php-extensions-cloud.md}}

PHP module requirements is linked to the Adobe Commerce version. Zie [ PHP vereisten ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/php-settings.html).

### Ondersteuning voor extensies

Voor Pro-projecten is aanvullende ondersteuning vereist voor de volgende extensies:

- `ioncube`
- `sourceguardian`

Als u PHP bijvoorbeeld zo wilt instellen dat alleen door SourceGuardian beveiligde scripts in alle omgevingen worden uitgevoerd, moet de volgende optie in het `php.ini` -bestand worden ingesteld:

```ini
[SourceGuardian]
sourceguardian.restrict_unencoded = "1"
```

Zie [ sectie 3.5 van de documentatie SourceGuardian ](https://sourceguardian.com/demofiles/files/SourceGuardian%20for%20Linux%20User%20Manual.pdf). _dit is een verbinding aan een PDF_.

[ leg een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) voor hulp met het installeren van deze PHP uitbreidingen in alle milieu&#39;s van de Productie en Pro het Staging milieu&#39;s voor. Neem het bijgewerkte `.magento/services.yaml` -bestand, `.magento.app.yaml` -bestand op met de bijgewerkte PHP-versie en eventuele extra PHP-extensies. Voor wijzigingen in een live productieomgeving moet u een minimale opzegtermijn van 48 uur opgeven. Het kan tot 48 uur duren voordat het infrastructuurteam van de cloud uw project kan bijwerken.

>[!WARNING]
>
>PHP die is gecompileerd met foutopsporing, wordt niet ondersteund en de sonde kan conflicteren met [!DNL XDebug] of [!DNL XHProf] . Schakel die extensies uit wanneer u de sonde inschakelt. De sonde veroorzaakt een conflict met sommige PHP-extensies zoals [!DNL Pinba] of IonCube.

<!-- Last updated from includes: 2025-04-14 09:39:27 -->
