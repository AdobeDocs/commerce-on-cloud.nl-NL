---
source-git-commit: 0df07e865c3c4fc4ac14483972643eafa8814726
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---
# Bestand opnemen om aangepaste VCL snel te wijzigen

## Het aangepaste VCL-fragment wijzigen

1. [ Login ](/help/get-started/onboarding.md#access-your-admin-panel) aan Admin.

1. Klik **Slaat** op > **Montages** > **Configuratie** > **Geavanceerd** > **Systeem**.

1. Breid **Volledige het Geheime voorgeheugen van de Pagina** > **Snelle Configuratie** uit > **de Fragmenten van VCL van de Douane**.

   ![ beheer de fragmenten van douaneVCL ](/help/assets/cdn/fastly-manage-snippets.png)

1. In de _kolom van de Actie_, klik het montagespictogram naast het uit te geven fragment.

1. Na de pagina herlaadt, uploadt de klik **VCL aan Fastly** in de _Snelle sectie van de Configuratie_.

1. Nadat het uploaden is voltooid, vernieuwt u de cache volgens het bericht boven aan de pagina.

>[!WARNING]
>
>De _optie UI van de fragmenten van de Douane VCL van 0&rbrace; toont slechts de fragmenten die door Adobe Commerce worden toegevoegd Admin._ Als u fragmenten toevoegt die Snelle API gebruiken, gebruik API om hen [ te beheren ](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
