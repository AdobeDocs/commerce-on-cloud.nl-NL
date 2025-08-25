---
title: Aangepaste VCL voor het toestaan van aanvragen
description: De inkomende verzoeken van de filter en verleent toegang door IP adres voor de plaatsen van Adobe Commerce door met een Fastly Edge ACL lijst en een douaneVCL fragment.
feature: Cloud, Configuration, Security
exl-id: 836779b5-5029-4a21-ad77-0c82ebbbcdd5
source-git-commit: d08ef7d46e3b94ae54ee99aa63de1b267f4e94a0
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Aangepaste VCL voor het toestaan van aanvragen

U kunt een Snelle Edge ACL lijst met een codefragment van douaneVCL gebruiken om inkomende verzoeken te filtreren en toegang door IP adres toe te staan. De ACL lijst specificeert de IP adressen toe te staan.

Creeer een lijst van gewenste personen om toegang tot uw het Opvoeren milieu te beperken zodat slechts de verzoeken van gespecificeerde IP adressen voor interne ontwikkelaars en de goedgekeurde externe diensten worden toegelaten. U kunt ook een lijst van gewenste personen maken om de toegang tot de beheeromgeving te beveiligen in de omgeving voor staging en productie.

Het volgende voorbeeld toont hoe te om een fragment van douaneVCL met a [ Snelle Lijst van het Toegangsbeheer (ACL) te gebruiken ](https://docs.fastly.com/guides/access-control-lists/about-acls) om toegang tot Admin voor een Adobe Commerce op het milieu van het het infrastructuurproject van de wolk te beveiligen. Wanneer u het douaneVCL fragment aan het milieu van de Wolk toevoegt, staat snel slechts verzoeken van IP adressen inbegrepen in ACL toe.

>[!TIP]
>
>Voor het Staging en de integratiemilieu&#39;s die niet openbaar toegankelijk zouden moeten zijn, gebruik de optie van de toegangscontrole van HTTP beschikbaar in [[!DNL Cloud Console]](../project/overview.md#access-the-project-web-interface) om toegang tot de volledige plaats door IP adres te beheren.

**Eerste vereisten:**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Lijst van cliëntIP adressen om op de lijst van gewenste personen te omvatten

## Edge ACL maken voor het toestaan van IP-adressen van clients

Edge ACLs creeert IP adreslijsten voor het beheren van toegang tot uw plaats. In dit voorbeeld, creeert u Edge ACL en voegt de lijst van cliëntIP adressen toe die worden toegestaan om tot Admin voor uw projectmilieu toegang te hebben.

{{admin-login-step}}

1. Klik **Opslag** > Montages > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Breid **Volledig Geheime voorgeheugen van de Pagina** > **Snelle Configuratie** uit > **ACL van Edge**.

1. Creeer de ACL container:

   - Klik **toevoegen ACL**.

   - Op de *ACL pagina van de Container*, ga een **ACL naam** in - `allowlist`.

   - Selecteer **activeren na de verandering** om uw veranderingen in de versie van de Snelle de dienstconfiguratie op te stellen die u uitgeeft.

   - Klik **uploaden** om ACL aan uw Snelle de dienstconfiguratie vast te maken.

1. Voeg de lijst met IP-adressen toe die toegang geven tot de beheerder:

   - Klik het pictogram van Montages voor `allowlist` ACL.

   - Voeg en bewaar de *IP Waarde* voor elk cliëntIP adres toe.

   - Klik **annuleren** om aan de pagina van de systeemconfiguratie terug te keren.

1. Klik **sparen Config**.

1. Vernieuw de cache volgens het bericht boven aan de pagina.

## Het aangepaste VCL-fragment maken om beheertoegang te beveiligen

De volgende aangepaste VCL-fragmentcode (JSON-indeling) toont de logica voor het filteren van aanvragen naar de beheerder en het verlenen van toegang als het client-IP-adres overeenkomt met een adres in de `allowlist` ACL.

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

Alvorens [ creërend een douanefragment ](https://experienceleague.adobe.com/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist.html?lang=nl-NL#add-the-custom-vcl-snippet) van dit voorbeeld, herzie de waarden om te bepalen of u om het even welke veranderingen moet aanbrengen. Voer vervolgens elke waarde in de desbetreffende velden, zoals `type` in het veld Type `content` in het veld Inhoud.

- `name` — Naam voor het VCL-fragment. Voor dit voorbeeld, `allowlist`.

- `priority` — Hiermee bepaalt u wanneer het VCL-fragment wordt uitgevoerd. De prioriteit is `5` om onmiddellijk in werking te stellen en te controleren of een Admin- verzoeken uit een toegestaan IP adres komen. Het fragment loopt vóór om het even welke standaardMagento VCL fragmenten (`magentomodule_*`) toegewezen een prioriteit van 50. Stel de prioriteit voor elk aangepast fragment in op een waarde hoger of lager dan 50, afhankelijk van het tijdstip waarop het fragment moet worden uitgevoerd. Fragmenten met een lagere prioriteit worden eerst uitgevoerd.

- `type` — Geeft een locatie op waar het fragment moet worden ingevoegd in de versioned VCL-code. Dit VCL is een `recv` fragmenttype dat de fragmentcode toevoegt aan de `vcl_recv` -subroutine onder de standaard VCL-code (Fastly VCL) en boven objecten.

- `content` — Het fragment van VCL-code dat moet worden uitgevoerd. In dit voorbeeld, verzoeken de codefilters aan Admin en staan toegang toe als het cliëntIP adres een adres in `allowlist` ACL aanpast. Als het adres niet overeenkomt, wordt de aanvraag geblokkeerd door een `403 Forbidden` -fout.

  Als de URL voor uw beheerder is gewijzigd, vervangt u de samplewaarde `/admin` door de URL voor uw omgeving. Bijvoorbeeld `/company-admin` .

In de codesteekproef, is de voorwaarde `!req.http.Fastly-FF` belangrijk wanneer het gebruiken van [ Afscherming van de Oorsprong ](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding). Verwijder of bewerk deze code niet.

Na het herzien van en het bijwerken van de code voor uw milieu, gebruik één van beiden van de volgende methodes om het fragment van douaneVCL aan uw Fastly de dienstconfiguratie toe te voegen:

- [ voeg het fragment van douaneVCL van Admin ](#add-the-custom-vcl-snippet) toe. Deze methode wordt aanbevolen als u toegang kunt krijgen tot de beheerder. (Vereist [ Snelle CDN module voor Magento 2 versie 1.2.58 ](fastly-configuration.md#upgrade) of later.)

- Sparen het JSON codevoorbeeld aan een dossier (bijvoorbeeld, `allowlist.json`) en [ uploadt het gebruikend Fastly API ](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Gebruik deze methode als u geen toegang hebt tot de beheerder.

## Het aangepaste VCL-fragment toevoegen

{{admin-login-step}}

1. Klik **Opslag** > Montages > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Breid **Volledige het Geheime voorgeheugen van de Pagina** > **Snelle Configuratie** uit > **de Fragmenten van VCL van de Douane**.

1. Klik **creëren het Fragment van de Douane**.

1. Voeg de waarden van het VCL-fragment toe:

   - **Naam** — `allowlist`

   - **Type** — `recv`

   - **Prioriteit** — `5`

   - Voeg de **VCL** fragmentinhoud toe:

     ```conf
     if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
     ```

1. Klik **creëren** om het VCL fragmentdossier met het naampatroon `type_priority_name.vcl` te produceren, bijvoorbeeld `recv_5_allowlist.vcl`

1. Na de pagina herlaadt, uploadt de klik **VCL aan Fastly** in de *Snelle sectie van de Configuratie* om het dossier aan de Snelle de dienstconfiguratie toe te voegen.

1. Nadat het uploaden is voltooid, vernieuwt u de cache volgens het bericht boven aan de pagina.

Hiermee wordt de bijgewerkte versie van de VCL-code snel gevalideerd tijdens het uploadproces. Als de validatie mislukt, bewerkt u het aangepaste VCL-fragment om het probleem op te lossen. Vervolgens uploadt u de VCL opnieuw.

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}

<!-- Last updated from includes: 2025-01-27 17:16:28 -->
