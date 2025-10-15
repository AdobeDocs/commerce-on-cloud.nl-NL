---
title: Web Application Firewall (WAF)
description: Leer hoe de Fastly WAF dienst ontdekt, registreert, en kwaadwillig verzoekverkeer blokkeert alvorens het het netwerk of de plaatsen van Adobe Commerce kan beschadigen.
feature: Cloud, Configuration, Security
exl-id: f00e35f2-9800-4e24-a4d0-d36fde59a003
source-git-commit: 7e61673b343fb954b53bf7cbae88efaf7bbfab4c
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Web Application Firewall (WAF)

Dankzij de snelle verbinding met de WAF-service (webtoepassingsfirewall) voor Adobe Commerce op cloudinfrastructuur wordt kwaadaardig aanvraagverkeer gedetecteerd, geregistreerd en geblokkeerd voordat uw sites of netwerk beschadigd kunnen raken. De WAF-service is alleen beschikbaar in productieomgevingen.

De WAF-service biedt de volgende voordelen:

- **naleving PCI** - WAF enablement zorgt ervoor dat Adobe Commerce storefronts in de milieu&#39;s van de Productie aan PCI DSS 6.6 veiligheidsvereisten voldoen.
- **StandaardWAF beleid** - het standaardWAF beleid, dat door Fastly wordt gevormd en wordt gehandhaafd, verstrekt een inzameling van veiligheidsregels die worden gemaakt om uw het Webtoepassingen van Adobe Commerce tegen een brede waaier van aanvallen, met inbegrip van injectieaanvallen, kwaadwillige input, dwars-plaats scripting, gegevenscontrole, het protocolschendingen van HTTP, en andere [&#x200B; Top tien van OWASP &#x200B;](https://owasp.org/www-project-top-ten/) veiligheidsbedreigingen te beschermen.
- **WAF on boarding en enablement** - Adobe stelt en laat het standaard beleid van WAF in uw milieu van de Productie binnen 2 tot 3 weken toe nadat de levering definitief is.
- **Verrichtingen en onderhoudssteun**—
   - Adobe en snel uw logboeken, regels en waarschuwingen voor de WAF-service instellen en beheren.
   - Adobe maakt gebruik van tickets voor klantenondersteuning die gerelateerd zijn aan WAF-servicekwesties die legitiem verkeer blokkeren als Prioriteit 1-problemen.
   - Geautomatiseerde upgrades naar de WAF-serviceversie zorgen voor directe dekking voor nieuwe of zich ontwikkelende explosies. Zie [&#x200B; onderhoud en verbeteringen van WAF &#x200B;](#waf-maintenance-and-updates).

>[!TIP]
>
>Voor extra informatie over het handhaven van naleving PCI voor uw Adobe Commerce op de opslag van de wolkeninfrastructuur, zie [&#x200B; naleving PCI &#x200B;](https://business.adobe.com/nl/products/magento/pci-compliance.html).

## WAF inschakelen

Adobe biedt de WAF-service op nieuwe accounts binnen 2 tot 3 weken nadat de provisioning is voltooid. De WAF wordt geïmplementeerd via de Fastly CDN-service. U hoeft geen hardware of software te installeren of te onderhouden.

>[!NOTE]
>
>Voordat u de WAF-service kunt gebruiken, moet u alle externe verkeer naar uw Adobe Commerce via het infrastructuurproject voor de cloud doorlopen via de Fastly-service. Zie [&#x200B; Opstelling snel &#x200B;](fastly-configuration.md).

## Hoe werkt het

De dienst van WAF integreert met Fastly en gebruikt de geheim voorgeheugenlogica binnen de Fastly dienst CDN om verkeer bij de Fastly globale knopen te filtreren. Wij laten de dienst van WAF in uw milieu van de Productie met een standaardWAF beleid toe dat op [&#x200B; wordt gebaseerd ModSecurity Regels van Trustwave SpiderLabs &#x200B;](https://github.com/owasp-modsecurity/ModSecurity) en de Top Tien van OWASP veiligheidsbedreigingen.

De dienst van WAF inspecteert HTTP en HTTPS verkeer (GET en POST- verzoeken) tegen de regels van WAF en blokkeert verkeer dat kwaadwillig is of niet aan specifieke regels voldoet. De dienst inspecteert slechts oorsprong-gebonden verkeer dat probeert om het geheime voorgeheugen te verfrissen. Dientengevolge, houden wij het meeste aanvalsverkeer bij het Fastly geheime voorgeheugen tegen, beschermend uw oorsprongsverkeer tegen kwaadwillige aanvallen. Door slechts oorsprongverkeer te verwerken, behoudt de dienst van WAF geheim voorgeheugenprestaties, introducerend slechts een geschatte 1.5 milliseconden aan 20 milliseconden van latentie aan elk niet caching verzoek.

## Problemen met geblokkeerde aanvragen oplossen

Wanneer de dienst van WAF wordt toegelaten, inspecteert het al Web en admin verkeer tegen de regels van WAF en blokkeert om het even welke Webverzoek die een regel teweegbrengt. Wanneer een aanvraag wordt geblokkeerd, ziet de aanvrager een standaard `403 Forbidden` foutpagina die een referentie-id bevat voor de blokkeringsgebeurtenis.

![&#x200B; de foutenpagina van WAF &#x200B;](../../assets/cdn/fastly-waf-403-error.png)

U kunt deze pagina met foutreacties aanpassen via de beheerfunctie. Zie [&#x200B; de de reactiepagina van WAF &#x200B;](fastly-custom-response.md#customize-the-waf-error-page) aanpassen.

Als uw Adobe Commerce admin pagina of storefront een `403 Forbidden` foutenpagina in antwoord op een wettig verzoek URL terugkeert, leg een [&#x200B; kaartje van de Steun van Adobe Commerce &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-case) voor. Kopieer de referentie-id van de pagina met foutreacties en plak deze in de beschrijving van het ticket.

Als u de WAF-reactie voor een bepaalde aanvraag wilt identificeren met New Relic, gaat u naar het volgende:

- `Agent_response` - Geeft de WAF-antwoordcode aan ( `200` betekent goed en `406` betekent geblokkeerd)
- `sigsci` -tags—Hiermee wordt de aanvraag gecodeerd als een bepaald signaalwetenschapslabel op basis van de aard van de aanvraag

## WAF-onderhoud en -updates

Snellere updates en implementeert patches voor nieuwe CVE&#39;s/sjabloonregels op basis van regelupdates van commerciële derden, snel onderzoek en open bronnen. De gepubliceerde regels worden zo nodig snel bijgewerkt in een beleid of wanneer wijzigingen in de regels beschikbaar zijn uit de respectieve bronnen. Bovendien kunt u met Snelheid regels toevoegen die overeenkomen met de gepubliceerde klassen regels in de WAF-instantie van elke service nadat de WAF-service is ingeschakeld. Deze updates zorgen voor onmiddellijke dekking voor nieuwe of zich ontwikkelende exploitaties.

Adobe en Fastly beheren het updateproces om ervoor te zorgen dat nieuwe of gewijzigde WAF-regels effectief werken in uw productieomgeving voordat de updates worden geïmplementeerd in de blokkeermodus.

## Problemen

Als u merkt dat de WAF legitieme verzoeken blokkeert, zijn deze vaak valse positieven en moeten ze worden omzeild of een oplossing hebben die bij de WAF-service wordt geïmplementeerd. Verzend een ondersteuningsticket en neem de betreffende URL op, evenals de exacte stappen waarmee de fout wordt gereproduceerd en de naslaggids in tekst (in tegenstelling tot een schermafbeelding) om schrijffouten te voorkomen.

## Beperkingen

De standaard WAF-service met de functie Fastly biedt geen ondersteuning voor de volgende functies:

- De bescherming tegen malware of beide beperking-overweegt het gebruiken van [&#x200B; toegangsbeheerlijsten &#x200B;](./fastly-vcl-allowlist.md) of de derdienst.
- Het tarief beperkt-zie [&#x200B; Tarief dat &#x200B;](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/RATE-LIMITING.md) in de Snelle documentatie beperkt, of zie [&#x200B; het Tarief dat &#x200B;](https://developer.adobe.com/commerce/webapi/get-started/rate-limiting/) beperkt in _het Web API van Commerce_ veiligheidssectie beperkt.
- Het vormen van een registrereneindpunt voor klant-zie [&#x200B; dienst PrivateLink &#x200B;](../development/privatelink-service.md) als alternatief.

De dienst van WAF staat u toe om verkeer te blokkeren of toe te staan dat op IP adressen wordt gebaseerd. U kunt toegangsbeheerlijsten (ACL) en de fragmenten van douaneVCL aan uw Snelle dienst toevoegen om de IP adressen en logica VCL voor het blokkeren of het toestaan van verkeer te specificeren. Zie {de fragmenten van 0} Snelle VCL van de Douane &lbrace;[&#128279;](fastly-vcl-custom-snippets.md).

Filteren voor TCP-, UDP- of ICMP-aanvragen wordt niet ondersteund door de WAF-service. Nochtans, wordt deze functionaliteit verstrekt door de ingebouwde bescherming DDoS inbegrepen met de Fastly dienst CDN. Zie [&#x200B; bescherming DDoS &#x200B;](fastly.md#ddos-protection).
