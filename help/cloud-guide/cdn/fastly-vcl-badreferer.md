---
title: Blokverwijzingsspam
description: Blokkeer de verwijzingspamme van uw site met behulp van het Fastly Edge-woordenboek en een aangepast VCL-fragment.
feature: Cloud, Configuration, Security
exl-id: 4ed47a71-7fee-4f37-a7da-3e30052004df
source-git-commit: d08ef7d46e3b94ae54ee99aa63de1b267f4e94a0
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Blokverwijzingsspam

Het volgende voorbeeld toont hoe te om [&#x200B; Snelle Woordenboek van Edge &#x200B;](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) met een fragment van douaneVCL te vormen om verwijzingsspam van uw Adobe Commerce op de plaats van de wolkeninfrastructuur te blokkeren.

>[!NOTE]
>
>Wij adviseren toevoegend de configuraties van douaneVCL aan een het Opvoeren milieu waar u hen kunt testen alvorens hen tegen het milieu van de Productie in werking te stellen.

**Eerste vereisten:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

- Controleer uw sitelogboeken op nepverwijzing-URL&#39;s en maak een lijst met domeinen die u wilt blokkeren.

## Een lijst van gewezen personen met referentie maken

Edge-woordenboeken maken sleutelwaardeparen die toegankelijk zijn voor VCL-functies tijdens de verwerking van VCL-fragmenten. In dit voorbeeld maakt u een Edge-woordenboek met de lijst met referentiewebsites die u wilt blokkeren.

{{admin-login-step}}

1. Klik **Slaat** op > **Montages** > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Breid **Volledig Geheime voorgeheugen van de Pagina** > **Snelle Configuratie** uit > **Edge woordenboeken**.

1. De container voor woordenboeken maken:

   - Klik **toevoegen container**.

   - Op de *pagina van de Container*, ga a **naam van het Woordenboek** in - `referrer_blocklist`.

   - Selecteer **activeren na de verandering** om uw veranderingen in de versie van de Snelle de dienstconfiguratie op te stellen die u uitgeeft.

   - Klik **uploaden** om het woordenboek aan uw Snelle de dienstconfiguratie vast te maken.

1. Voeg de lijst met domeinnamen die u wilt blokkeren toe aan het woordenboek `referrer_blocklist` :

   - Klik op het pictogram Instellingen voor het woordenboek `referrer_blocklist` .

   - U kunt sleutelwaardeparen toevoegen en opslaan in het nieuwe woordenboek. Voor dit voorbeeld, is elke **Sleutel** de domeinnaam van een verwijzer URL om te blokkeren en **Waarde** is `true`.

     ![&#x200B; voeg slechte punten van het verwijzingenwoordenboek &#x200B;](../../assets/cdn/fastly-referrer-blocklist-dictionary.png) toe

   - Klik **annuleren** om aan de pagina van de systeemconfiguratie terug te keren.

1. Klik **sparen Config**.

1. Vernieuw de cache volgens het bericht boven aan de pagina.

Voor meer informatie over de Woordenboeken van Edge, zie [&#x200B; Creërend en gebruikend de Woordenboeken van Edge &#x200B;](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) en [&#x200B; de fragmenten van douaneVCL &#x200B;](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api#custom-vcl-examples) in de Fastly documentatie.

## Een aangepast VCL-fragment maken om verwijzingsspam te blokkeren

De volgende aangepaste VCL-fragmentcode (JSON-indeling) toont de logica voor het controleren en blokkeren van aanvragen. Het VCL-fragment legt de host van een verwijzingswebsite vast in een header en vergelijkt vervolgens de hostnaam met de lijst met URL&#39;s in het `referrer_blocklist` -woordenboek. Als de hostnaam overeenkomt, wordt de aanvraag geblokkeerd door een `403 Forbidden` -fout.

```json
{
  "name": "block_bad_referrer",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if (req.http.Referer ~ \"^(.*:)//([A-Za-z0-9\-\.]+)(:[0-9]+)?(.*)$\") {set req.http.Referer-Host = re.group.2;}if (table.lookup(referrer_blocklist, req.http.Referer-Host)) {error 403 \"Forbidden\";}"
}
```

Voordat u een op dit voorbeeld gebaseerd fragment maakt, controleert u de waarden om te bepalen of u wijzigingen wilt aanbrengen:

- `name` — Naam voor het VCL-fragment. In dit voorbeeld hebben we `block_bad_referrer` gebruikt.

- `dynamic` — Waarde 0 wijst op a [&#x200B; regelmatig fragment &#x200B;](https://docs.fastly.com/en/guides/using-regular-vcl-snippets) om aan versioned VCL voor de Snelle configuratie te uploaden.

- `priority` — Hiermee bepaalt u wanneer het VCL-fragment wordt uitgevoerd. De prioriteit is `5` om deze fragmentcode in werking te stellen alvorens om het even welke standaardMagento VCL fragmenten (`magentomodule_*`) toegewezen een prioriteit van 50. Stel de prioriteit voor elk aangepast fragment in op een waarde hoger of lager dan 50, afhankelijk van het tijdstip waarop het fragment moet worden uitgevoerd. Fragmenten met een lagere prioriteit worden eerst uitgevoerd.

- `type` — Geeft een locatie op waar het fragment moet worden ingevoegd in de VCL-versie. In dit voorbeeld is het VCL-fragment een `recv` -fragment. Wanneer het fragment in de VCL-versie wordt ingevoegd, wordt het toegevoegd aan de `vcl_recv` -subroutine, onder de standaard VCL-code snel en boven alle objecten.

- `content` — Het fragment van VCL-code dat op één regel wordt uitgevoerd, zonder regeleinden.

Na het herzien van en het bijwerken van de code voor uw milieu, gebruik één van beiden van de volgende methodes om het fragment van douaneVCL aan uw Fastly de dienstconfiguratie toe te voegen:

- [&#x200B; voeg het fragment van douaneVCL van Admin &#x200B;](#add-the-custom-vcl-snippet) toe. Deze methode wordt aanbevolen als u toegang kunt krijgen tot de beheerder. (Vereist [&#x200B; Snelle versie 1.2.58 &#x200B;](fastly-configuration.md#upgrade) of later.)

- Sparen het JSON codevoorbeeld aan een dossier (bijvoorbeeld, `allowlist.json`) en [&#x200B; uploadt het gebruikend Fastly API &#x200B;](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Gebruik deze methode als u geen toegang hebt tot de beheerder.

## Het aangepaste VCL-fragment toevoegen

{{admin-login-step}}

1. Klik **Opslag** > Montages > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Breid **Volledige het Geheime voorgeheugen van de Pagina** > **Snelle Configuratie** uit > **de Fragmenten van VCL van de Douane**.

1. Klik **creëren het Fragment van de Douane**.

1. Voeg de waarden van het VCL-fragment toe:

   - **Naam** — `block_bad_referrer`

   - **Type** — `recv`

   - **Prioriteit** — `5`

   - **VCL** fragmentinhoud —

     ```conf
     if (req.http.Referer ~ "^(.*:)//([A-Za-z0-9\-\.]+)(:[0-9]+)?(.*)$") {
       set req.http.Referer-Host = re.group.2;  
     }
     if (table.lookup(referrer_blocklist, req.http.Referer-Host)) {
       error 403 "Forbidden";
     }
     ```

1. Klik **creëren**.

   ![&#x200B; creeer het fragment van het blok van de douaneverwijzing VCL &#x200B;](/help/assets/cdn/fastly-create-referrer-block-snippet.png)

1. Na de pagina herlaadt, uploadt de klik **VCL aan Fastly** in de *Snelle sectie van de Configuratie*.

1. Nadat het uploaden is voltooid, vernieuwt u de cache volgens het bericht boven aan de pagina.

Hiermee valideert u de bijgewerkte VCL-versie snel tijdens het uploadproces. Als de validatie mislukt, bewerkt u het aangepaste VCL-fragment om eventuele problemen op te lossen. Vervolgens uploadt u de VCL opnieuw.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}

<!-- Last updated from includes: 2025-01-27 17:16:28 -->
