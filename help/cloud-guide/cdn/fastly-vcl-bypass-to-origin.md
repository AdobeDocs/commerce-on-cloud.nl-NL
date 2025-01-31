---
title: Aangepaste VCL om snel cache te omzeilen
description: Los verzoekverkeer aan de oorsprongsserver problemen op door een fragment van douaneVCL te creëren om het Fastly geheime voorgeheugen te mijden.
feature: Cloud, Configuration, Cache
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Aangepaste VCL om snel cache te omzeilen

U kunt een aangepast VCL-fragment maken om de cache Fastly te omzeilen, zodat u het aanvraagverkeer op de oorspronkelijke server kunt oplossen. U kunt bijvoorbeeld een fragment maken om te bepalen of siteproblemen worden veroorzaakt door caching, of om koppen problemen op te lossen.

U kunt het fragment vormen om snel caching voor verzoeken van een specifiek IP adres of URL te mijden.

>[!NOTE]
>
>Alvorens de configuratie van douaneVCL in een productiemilieu samen te voegen, zorg ervoor om de code in het het Opvoeren milieu te testen.

**Eerste vereisten:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**om het geheime voorgeheugen over te slaan dat op IP adres of URL** wordt gebaseerd:

{{admin-login-step}}

1. Klik **Opslag** > Montages > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Breid **Volledige het Geheime voorgeheugen van de Pagina** > **Snelle Configuratie** uit > **de Fragmenten van VCL van de Douane**.

1. Klik **creëren het Fragment van de Douane**.

1. Voeg de waarden van het VCL-fragment toe:

   - **Naam** — `bypass_fastly`

   - **Type** — `recv`

   - **Prioriteit** — `5`

   - **VCL** fragmentinhoud —

     In het volgende voorbeeld wordt Fastly overgeslagen voor een specifiek IP-adres:

     ```conf
     if (client.ip == "<Your IPv4 IP address>" || client.ip == "<Your IPv6 IP address>") {
       return(pass);
     }
     ```

     In het volgende voorbeeld wordt snel overgeslagen voor een specifiek URL-patroon:

     ```conf
     if (req.url ~ "/media/feeds/GoogleShoppingHiVisNew.xml") {  return (pass);}
     ```

     Voor een exacte URL-overeenkomst gebruikt u de operator `==` in plaats van de operator `~` . Zie de [ Snelle verwijzing VCL ] voor details.

1. Klik **creëren**.

   ![ creeer snel het fragment van de Bypass VCL ](/help/assets/cdn/fastly-create-bypass-snippet.png)

1. Na de pagina herlaadt, uploadt de klik **VCL aan Fastly** in de *Snelle sectie van de Configuratie*.

1. Nadat het uploaden is voltooid, vernieuwt u de cache volgens het bericht boven aan de pagina.

   Hiermee valideert u de bijgewerkte VCL-versie snel tijdens het uploadproces. Als de validatie mislukt, bewerkt u het aangepaste VCL-fragment om eventuele problemen op te lossen. Vervolgens uploadt u de VCL opnieuw.

Nadat u het VCL-fragment hebt toegevoegd, kunt u met cURL-opdrachten aanvragen naar de oorspronkelijke server verzenden via het opgegeven IP-adres of de URL, zoals in het volgende voorbeeld wordt getoond:

```bash
curl -svo /dev/null www.example.com/index.html
```

Dan, inspecteer de reactie om kwesties met de niet caching inhoud problemen op te lossen.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}

<!--External link definitions-->

[Fastly VCL reference]: https://docs.fastly.com/vcl/
