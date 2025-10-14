---
title: Checklist starten
description: Controlelijst met items voor het starten van de site weergeven.
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---

# Checklist starten

Alvorens u aan het milieu van de Productie opstelt, download de [&#x200B; checklist van de Lancering &#x200B;](../../assets/adobe-commerce-cloud-prelaunch-checklist.pdf), en gebruik het met deze instructies om te bevestigen dat u alle vereiste configuratie en het testen hebt voltooid. Zie een overzicht van het volledige plaatsingsproces voor Starter en Pro bij [&#x200B; uw opslag &#x200B;](../deploy/staging-production.md) opstellen.

## Volledig testen in productie

Zie [&#x200B; plaatsing van de Test &#x200B;](../test/staging-and-production.md) voor het testen van alle aspecten van uw plaatsen, opslag, en milieu&#39;s. Deze tests omvatten het controleren van Fastly, de Tests van de Erkenning van de Gebruiker (UAT), en prestatietests.

## TLS en snel

Adobe biedt een Let&#39;s Encrypt SSL/TLS-certificaat voor elke omgeving. Dit certificaat is vereist om snel veilig verkeer via HTTPS te kunnen uitvoeren.

Om dit certificaat te gebruiken, moet u uw DNS configuratie bijwerken zodat de Adobe domeinbevestiging kan voltooien en het certificaat op uw milieu toepassen. Elke omgeving heeft een uniek certificaat dat de domeinen voor de Adobe Commerce bestrijkt op cloudinframinframites die in die omgeving worden geïmplementeerd. Wij adviseren de voltooiing en de configuratieupdates tijdens het [&#x200B; Snelle opstellingsproces &#x200B;](../cdn/fastly-configuration.md).

## DNS-configuratie bijwerken met productie-instellingen

Wanneer u bereid bent om uw plaats te lanceren, moet u de DNS configuratie bijwerken om verkeer van uw milieu van de Productie door de Snelle dienst te leiden.

**Eerste vereisten:**

- [Stel uw ontwikkelomgeving in en test deze snel](../cdn/fastly-configuration.md#)

- Configuratie van productieomgeving is bijgewerkt met alle vereiste domeinen

  Gewoonlijk werkt u met uw technische adviseur van de Klant om alle domeinen en subdomeinen op hoofdniveau toe te voegen die voor uw opslag worden vereist. Om de domeinen voor uw milieu van de Productie toe te voegen of te veranderen, [&#x200B; leg een kaartje van de Steun van Adobe Commerce &#x200B;](https://support.magento.com/hc/en-us/articles/360019088251) voor. Wacht op bevestiging dat uw projectconfiguratie is bijgewerkt.

  Voor de projecten van de Aanzet, moet u de domeinen aan uw project toevoegen. Zie [&#x200B; domeinen &#x200B;](../cdn/fastly-custom-cache-configuration.md#manage-domains) beheren.

- SSL/TLS-certificaat dat is ingericht voor uw productieomgeving.

  Als u de ACME uitdagingsverslagen voor uw domeinen van de Productie tijdens het Fastly opstellingsproces toevoegde, uploadt de Adobe het SSL/TLS certificaat aan uw milieu van de Productie automatisch wanneer u de DNS configuratie aan routeverkeer aan de Fastly dienst bijwerkt. Als u het certificaat niet vooraf hebt verstrekt, of als u uw domeinen bijwerkte, moet de Adobe domeinbevestiging voltooien en levering het certificaat, dat tot 12 uren kan vergen.

### DNS-configuratie bijwerken voor het starten van de site:

1. Werk de volgende DNS configuratie voor uw plaats van de Productie bij:

   - Alle benodigde omleidingen instellen, vooral als u van een bestaande site migreert

   - Plaats het verslag van het wortelmiddel van de streek om hostname te richten

   - Verlaag de waarde voor Tijd-aan-Levende (TTL) om DNS informatie te verfrissen om klanten aan de correcte opslag van de Productie te richten

     Wij adviseren een beduidend lagere waarde van TTL wanneer het schakelen van het DNS verslag. Deze waarde vertelt DNS hoe lang om het DNS verslag in het voorgeheugen onder te brengen. Wanneer verkort, verfrist het sneller DNS. U kunt bijvoorbeeld de TTL-waarde wijzigen van drie dagen in tien minuten wanneer u uw site bijwerkt. Houd er rekening mee dat het verkorten van de TTL-waarde het laden van de DNS-infrastructuur toevoegt. Herstel de vorige, hogere waarde na de lancering van de plaats.


1. Voeg CNAME-records toe om de subdomeinen voor uw productieomgeving te wijzen naar de Fastly-service `prod.magentocloud.map.fastly.net` , bijvoorbeeld:

   | Domein of Subdomein | CNAME |
   | ----------------------- | -------------------------------- |
   | `www.<domain-name>.com` | prod.magentocloud.map.fastly.net |
   | `mystore.<domain-name>.com` | prod.magentocloud.map.fastly.net |

1. Voeg zo nodig A-records toe om het apex-domein (`<domain-name>.com`) toe te wijzen aan de volgende snelste IP-adressen:

   | Apex-domein | ANAME |
   | --------------- | ----------------- |
   | `<domain-name>.com` | `151.101.1.124` |
   | `<domain-name>.com` | `151.101.65.124` |
   | `<domain-name>.com` | `151.101.129.124` |
   | `<domain-name>.com` | `151.101.193.124` |

>[!IMPORTANT]
>
>De DNS instructies in [&#x200B; RFC1034 &#x200B;](https://www.rfc-editor.org/rfc/rfc1912) (**sectie 2.4**) verklaren dat:
>_Een CNAME-record mag niet naast andere gegevens bestaan. Met andere woorden, als suzy.podunk.xx een alias voor use.podunk.xx is, kunt u geen MX- verslag voor suzy.podunk.edu, of een verslag van A, of zelfs geen verslag TXT._ hebben
>
>DNS-records moeten daarom van het type `CNAME` zijn voor subdomeinen en van het type `A` voor apex-domeinen (hoofddomeinen). Het verwerpen van deze regel kan in verstoringen aan uw postdienst of DNS propagatie resulteren omdat u de capaciteit verliest om andere verslagen, zoals MX of NS toe te voegen. Sommige DNS leveranciers kunnen dit door interne aanpassingen te gebruiken omzeilen, maar het volgen van de norm verzekert stabiliteit en flexibiliteit (zoals verandering van de DNS leverancier).

1. Werk de basis-URL bij.

   - Gebruik SSH om u aan te melden bij de productieomgeving.

     ```bash
     magento-cloud ssh -e production
     ```

   - Gebruik CLI om de basis URL voor uw opslag te veranderen.

     ```bash
     php bin/magento setup:store-config:set --base-url="https://www.<domain-name>.com/"
     ```

   **NOTA**: U kunt de Basis URL van Admin ook bijwerken. Zie [&#x200B; opslag URLs &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-urls.html?lang=nl-NL) in de _Opslag van Adobe Commerce en Gids van de Ervaring van de Aankoop_.

1. Wacht een paar minuten totdat de site is bijgewerkt.

1. Test uw site.

## Productieconfiguratie verifiëren

Maak een definitieve pas om de configuratie van de Productie voor één of meerdere opslag te bevestigen. U kunt de configuratie bijwerken in de productieomgeving. Als de montages read-only zijn, kunt u een verbinding van SSH moeten openen en CLI bevelen gebruiken om de configuratie te veranderen, of configuratieveranderingen in uw lokale milieu aan te brengen. Nadat u de updates hebt voltooid, kunt u de wijzigingen implementeren in de omgeving van Staging en Productie.

Hieronder vindt u aanbevolen wijzigingen en controles:

- [Uitgaande e-mailtests voltooid](../project/outgoing-emails.md)

- [&#x200B; Veilige configuratie voor geloofsbrieven Admin en Basis Admin URL &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-admin/systems/security/security-admin)

- [Alle afbeeldingen voor het web optimaliseren](../cdn/fastly-image-optimization.md)

- [Minimalisatie-instellingen controleren voor HTML, JavaScript en CSS](../deploy/static-content.md)

## Snelle caching controleren

- Test en verifieer dat het snel in cache plaatsen correct op de plaats van de Productie werkt. Voor gedetailleerde tests en controles, zie [&#x200B; Snelle het testen &#x200B;](../test/staging-and-production.md#check-fastly-caching).

- [Zorg ervoor dat de nieuwste versie van de Fastly CDN Module voor Commerce is geïnstalleerd in de productieomgeving](../cdn/fastly-configuration.md#upgrade-the-fastly-module)

- [Controleer of de meest actuele versie van de VCL-code snel is geüpload](../cdn/fastly-configuration.md#upload-vcl-to-fastly)

## Prestatietests

Wij adviseren dat u de [&#x200B; Toolkit van Prestaties &#x200B;](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) opties als deel van uw pre-lanceringsbereidheidsproces herziet.

U kunt ook testen met de volgende opties van derden:

- [&#x200B; Siege &#x200B;](https://www.joedog.org/siege-home/): Het verkeer vormend en testend software om uw opslag aan de grens te duwen. Plaats uw site met een configureerbaar aantal gesimuleerde clients. Siege ondersteunt basisverificatie, cookies, HTTP-, HTTPS- en FTP-protocollen.

- [&#x200B; Jmeter &#x200B;](https://jmeter.apache.org/): Uitstekende ladingstest om prestaties voor verrijkt verkeer, zoals voor flitsverkoop te meten. Aangepaste tests maken die op uw site worden uitgevoerd.

- [&#x200B; New Relic &#x200B;](https://support.newrelic.com/s/) (verstrekt): Helpt van processen en gebieden van de plaats de plaats bepalen veroorzakend langzame prestaties met bijgehouden tijd die per actie wordt doorgebracht zoals het overbrengen van gegevens, vragen, Redis, en meer.

- [&#x200B; WebPageTest &#x200B;](https://www.webpagetest.org/) en [&#x200B; VK &#x200B;](https://www.pingdom.com/): De analyse in real time van uw pagina&#39;s van de plaats laadt tijd met verschillende oorsprongsplaatsen. Het koninkrijk kan een vergoeding kosten. WebPageTest is een gratis hulpmiddel.

## Beveiligingsconfiguratie

- [Beveiligingsscan instellen](overview.md#set-up-the-security-scan-tool)

- [&#x200B; Veilige configuratie voor Admin gebruiker &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-admin/systems/security/security-admin)

- [&#x200B; Veilige configuratie voor Admin URL &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url)

- [Gebruikers die zich niet meer op de Adobe Commerce bevinden, verwijderen uit het infrastructuurproject voor de cloud](../project/user-access.md)

- [&#x200B; vorm twee-factor authentificatie &#x200B;](https://developer.adobe.com/commerce/testing/functional-testing-framework/two-factor-authentication/)

## Prestatiebewaking

U kunt New Relic-services gebruiken voor prestatiebewaking in Pro- en Starter-omgevingen. Op Pro-planaccounts bieden we de Beheerde waarschuwingen voor het Adobe Commerce-waarschuwingsbeleid om de prestaties van toepassingen en infrastructuren te controleren met behulp van New Relic APM en Infrastructure-agents. Voor details bij het gebruiken van deze diensten, zie [&#x200B; prestaties van de Monitor met Beheerde Alarm &#x200B;](../monitor/investigate-performance.md#monitor-performance-with-managed-alerts).

### Volgende stap

[Stappen starten](steps.md)
