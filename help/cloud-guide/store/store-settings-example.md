---
title: Voorbeeld van het beheren van systeemspecifieke instellingen
description: Bekijk een voorbeeld van hoe u de configuratie-instellingen van de winkel in alle Adobe Commerce kunt beheren en synchroniseren in omgevingen met cloudinfrastructuren.
hidefromtoc: true
source-git-commit: 0df07e865c3c4fc4ac14483972643eafa8814726
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# Voorbeeld van het beheren van systeemspecifieke instellingen

In dit voorbeeld wordt getoond hoe u configuratiebeheer kunt gebruiken om de opslaginstellingen in alle omgevingen consistent te houden.

Het voorbeeld gebruikt de volgende procedure die in [&#x200B; wordt bepaald montages van de Opslag &#x200B;](store-settings.md):

1. Voer uw configuraties in in de winkel Admin van uw integratieomgeving in.
1. Maak een `config.php` -bestand en breng dit over naar uw lokale werkstation.
1. Duw `config.php` naar de externe integratieomgeving.
1. Controleer of uw instellingen niet kunnen worden bewerkt in Beheer.
1. Breng de gewenste wijzigingen aan:

   * Wijzig de configuratie-instellingen in de integratieomgeving.
   * Als u configuraties wilt toevoegen, voert u de opdracht uit om `config.php` opnieuw te maken. Nieuwe configuraties worden aan het bestand toegevoegd.
   * Als u bestaande configuraties wilt verwijderen of bewerken, bewerkt u het bestand handmatig.
   * Vastleggen en duwen.

U kunt bijvoorbeeld de volgende instellingen instellen:

* De optimalisatie-instellingen voor landinstellingen en statische bestanden uitschakelen in uw integratieomgeving
* Optimalisatie van statische bestanden inschakelen in testomgevingen en productieomgevingen
* Vorm snel in het Staging en Productie met specifieke geloofsbrieven voor elk

_Statische dossieroptimalisering_ betekent het samenvoegen en het miniaturen van JavaScript en Cascading Style Sheets, en het miniaturen van HTML malplaatjes. Zie [&#x200B; Statische strategieën van de inhoudsplaatsing &#x200B;](../deploy/static-content.md).

## Vereisten

Om deze taken van het configuratiebeheer te voltooien, hebt u het volgende nodig:

* De lezerrol van het project met [&#x200B; milieu &quot;admin&quot;](../project/user-access.md) voorrechten
* Admin URL en geloofsbrieven voor integratie, het Opvoeren, en de milieu&#39;s van de Productie

## Commerce Admin configureren

In de integratieomgeving kunt u zich aanmelden bij de beheerder om de systeemconfiguratie-instellingen voor winkels, websites, modules of extensies, de optimalisatie van statische bestanden en systeemwaarden te wijzigen voor de implementatie van statische inhoud. Zie [&#x200B; gegevens van de Configuratie &#x200B;](store-settings.md#scd-performance).

**om scène en statische montages van de dossieroptimalisering** te veranderen:

1. Meld u aan bij de beheerder van de integratieomgeving. U hebt toegang tot deze URL via [[!DNL Cloud Console]](../project/overview.md) .
1. Navigeer aan **Slaat** > Montages > **Configuratie** > Algemeen > **Algemeen**.
1. In de paginanavigatie, breid **Opties van de Landinstelling** uit.
1. Van de **Lijst van de Landinstelling**, verander de scène. U kunt deze later wijzigen.

   ![&#x200B; verander de scène &#x200B;](../../assets/locale-options.png)

1. Klik **sparen Config**.
1. Indien ertoe aangezet, [&#x200B; spoel het geheime voorgeheugen &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-admin/systems/tools/cache-management).
1. Afmelden bij de beheerder.

## Waarden exporteren en config.php overbrengen naar uw lokale systeem

Met deze stap wordt het `config.php` -configuratiebestand in de integratieomgeving gemaakt en overgebracht met behulp van een opdracht die u op uw lokale computer uitvoert.

Deze procedure beantwoordt aan stap 2 in de [&#x200B; geadviseerde procedure &#x200B;](store-settings.md). Nadat u `config.php` hebt gemaakt, brengt u deze over naar uw lokale systeem, zodat u deze aan Git kunt toevoegen.

**om te creëren en over te brengen`config.php`**:

1. Wijzig op uw lokale werkstation de projectmap.

1. Verandering in het milieu van de Integratie.

   ```bash
   magento-cloud environment:checkout integration
   ```

1. Creeer een lokale stortplaats van het verre gegevensbestand.

   ```bash
   magento-cloud db:dump
   ```

In het volgende fragment uit `config.php` ziet u een voorbeeld van het wijzigen van de standaardlandinstelling in `en_GB` en het wijzigen van de optimalisatie-instellingen voor statische bestanden:

```php?start_inline=1
'general' => [
     'locale' => [
         'code' => 'en_GB',
         'timezone' => 'UTC',
     ],

     ... more ...

 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],
     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],

     ... more ...
```

## config.php naar omgevingen duwen en implementeren

Nu u `config.php` hebt gemaakt en naar uw lokale systeem hebt overgebracht, koppelt u het aan Git en duwt u het naar uw omgevingen. Deze procedure beantwoordt aan stap 3 en 4 in de [&#x200B; geadviseerde procedure &#x200B;](store-settings.md).

Met de volgende opdracht voegt u de `master` -vertakking toe, verbindt u zich en drukt u deze door:

```bash
git add app/etc/config.php && git commit -m "Add system-specific configuration" && git push origin master
```

Volledige codeplaatsing aan het Staging en Productie. Bij Starter drukt u op `staging` en `master` vertakkingen. Voor details op plaatsingsbevelen, zie [&#x200B; uw opslag &#x200B;](../deploy/staging-production.md) opstellen.

Wacht tot de implementatie in alle omgevingen is voltooid.

## Wijzigingen in configuratie controleren

Nadat u `config.php` in uw omgeving hebt geplaatst, moeten alle gewijzigde waarden alleen-lezen zijn in de beheerfunctie. In dit voorbeeld zijn de gewijzigde standaardinstellingen voor landinstellingen en optimalisatie van statische bestanden niet bewerkbaar in Beheer. Deze configuratie-instellingen worden ingesteld in `config.php` .

Om uw configuratieveranderingen te verifiëren:

1. Log uit van de beheerder in een van de omgevingen.
1. Meld u weer aan bij de beheerder.
1. Klik **Slaat** op > Montages > **Configuratie** > Algemeen > **Algemeen**.
1. In de juiste ruit, breid **Opties van de Landinstelling** uit.

   U ziet dat verschillende velden niet kunnen worden bewerkt, zoals in het volgende voorbeeld wordt getoond. Deze configuratie-instellingen blijven behouden door `config.php` .

   ![&#x200B; Bepaalde waarden niet meer editable in Admin &#x200B;](../../assets/locale-options-disabled.png)

1. Afmelden bij de beheerder.

## Systeemspecifieke configuratie-instellingen wijzigen en bijwerken

Als u een van deze instellingen moet wijzigen, wijzigt u het bestand `config.php` handmatig met een teksteditor. Nadat u de bewerkingen of verwijderingen hebt voltooid, kunt u deze doorvoeren en naar de externe omgeving verplaatsen volgens de vorige stappen.

Om configuraties toe te voegen, wijzig uw integratiemilieu en stel het bevel opnieuw in werking om het dossier te produceren. Nieuwe configuraties worden toegevoegd aan de code in het bestand. Duw het aan Git na de vorige stappen.

In dit voorbeeld wijzigt u de optimalisatie-instellingen voor statische bestanden en voegt u een nieuwe instelling toe voor JavaScript.

### Configuraties toevoegen in integratie

Configuratiewaarden toevoegen in de integratieomgeving Admin. In dit voorbeeld worden JavaScript-bestanden samengevoegd.

1. Meld u af bij de integratie-beheerder.
1. Meld u weer aan bij de integratiebeheerder.
1. Klik **Slaat** op > Montages > **Configuratie** > **Geavanceerd** > **Ontwikkelaar**.
1. In de juiste ruit, breid **Montages van JavaScript** uit.
1. Van de **lijst van de Dossiers van JavaScript van de Fusie**, klik **ja**.
1. Klik **sparen Config**.
1. Indien ertoe aangezet, [&#x200B; spoel het geheime voorgeheugen &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-admin/systems/tools/cache-management).
1. Afmelden bij de beheerder.

Door het dumpbevel opnieuw in werking te stellen, wordt de nieuwe configuratie toegevoegd aan het dossier.

```bash
magento-cloud db:dump
```

### config.php bewerken met nieuwe instellingen

Bewerk het bijgewerkte `app/etc/config.php` -bestand via een teksteditor. Bewerk deze instellingen om miniaturen voor JavaScript-, HTML- en CSS-bestanden in te schakelen.

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '0',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '0',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '0',
     ],
```

Als u instellingen wilt wijzigen om minificatie toe te staan, bewerkt u `'0'` naar `'1'` for `'minify_html'` en elke `'minify_files'` optie:

```php?start_inline=1
 'dev' => [
     'template' => [
         'allow_symlink' => '0',
         'minify_html' => '1',
     ],

     ... more ...

     'js' => [
         'merge_files' => '0',
         'enable_js_bundling' => '0',
         'minify_files' => '1',
     ],
     'css' => [
         'merge_css_files' => '0',
         'minify_files' => '1',
     ],
```

Sla de wijzigingen in het bestand op.

### De wijzigingen in Git duwen

Voer het volgende in om uw wijzigingen door te voeren:

```bash
git add app/etc/config.php
```

```bash
git commit -m "Add system-specific configuration and edit settings"
```

```bash
git push origin master
```

Wacht tot de implementatie is voltooid.

Herhaal het implementatieproces om de code naar alle omgevingen te verplaatsen.
