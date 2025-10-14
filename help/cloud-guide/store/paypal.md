---
title: PayPal-betalingsmethoden instellen
description: PayPal-betalingsmethoden instellen voor Adobe Commerce op cloudinfrastructuur.
feature: Cloud, Checkout, Payments
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# PayPal-betalingsmethoden instellen

Adobe Commerce on cloud Infrastructure biedt een instaphulpmiddel om PayPal Express Checkout-accounts rechtstreeks via de beheerder te configureren. Dit gereedschap is beschikbaar voor ECE 2.1.8 en hoger. Om live te gaan en PayPal-betalingsmethoden te testen, kunt u uw PayPal Express Checkout-account inschakelen en configureren voor sandbox- of productierekeningen.

U kunt de sandbox- of productieaccount in elke omgeving configureren:

* Stel Sandbox-referenties in voor integratie- en staging-omgevingen.
* Stel voor uw productieomgeving Sandbox-referenties in voor de eerste test en vervang deze gegevens door de live productiegegevens voor een gestarte winkel.

## PayPal-rekening

Het is het beste om een PayPal Merchant-account te gebruiken dat is voorbereid en geconfigureerd, maar u kunt een account maken of een persoonlijke account upgraden via Beheer.

[!DNL PayPal onboarding] biedt ondersteuning voor het maken van verbinding met de volgende accounts:

* PayPal Business-account
* Persoonlijke PayPal-rekening, converteren naar een zakelijke account. Als u een bestaand persoonlijk PayPal-account hebt, kunt u zich aanmelden met deze gegevens en dit account upgraden naar een zakelijke account wanneer u de synchronisatie hebt voltooid.

Als u geen bestaande PayPal-rekening hebt, maakt u er een. Voer een e-mailadres in voor een nieuwe account. Als er geen overeenkomend PayPal-account wordt gevonden, volgt u de aanwijzingen om een PayPal Business-account te maken. Of u kunt een rekening direct door [&#x200B; PayPal &#x200B;](https://www.paypal.com/us/webapps/mpp/account-selection) tot stand brengen.

### Paypal-beperkingen

PayPal biedt ondersteuning voor het verbinden van PayPal Express Checkout voor landen over de hele wereld, behalve voor de volgende beperkingen:

* India en Japan (toekomstige PayPal-updates kunnen deze accounts ondersteunen)
* Israël

Voor Brazilië moet je een bestaande PayPal-zakelijke account hebben om verbinding te maken. Tijdens dit proces kunt u geen bestaande persoonlijke PayPal-rekening voor Brazilië converteren. Als u een rekening nodig hebt, [&#x200B; creeer een zakenPayPal rekening &#x200B;](https://www.paypal.com/us/webapps/mpp/account-selection).

## PayPal Express-afhandeling configureren

PayPal Express Checkout configureren:

1. Open de Admin voor het milieu.
1. In de linkerzijnavigatie, uitgezochte **Slaat** > **Configuratie**, dan selecteren **Verkoop** > **de Methoden van de Betaling**.
1. Voor PayPal, uitgezochte **vormt**. De gebieden van de configuratie tonen in uitbreidbare secties voor Uitdrukkelijke Afhandeling, Adverteer PayPal Krediet, en Basis en Geavanceerde montages.
1. Sluit uw Paypal-account aan. Totdat de account is verbonden, zijn de opties die moeten worden ingeschakeld uitgeschakeld. Voor details op beschikbare en gesteunde rekeningen om en beperkingen te verbinden, zie [&#x200B; PayPal rekening &#x200B;](#paypal-account).

   * Klik op Verbinding maken met PayPal en volg de aanwijzingen om verbinding te maken met uw PayPal-account. Aankopen door klanten met behulp van een live PayPal-rekening zijn voltooid en brengen klanten in een live winkel actief in rekening.
   * Als u uw sandboxaccount wilt koppelen voor testdoeleinden, klikt u op Sandboxreferenties en volgt u de aanwijzingen. Aankopen door klanten met behulp van een sandbox PayPal voltooid zonder klanten actief in rekening te brengen.

1. Configureer de instellingen voor Express Checkout om de PayPal-API te verifiëren en te gebruiken:

   * **E-mail Verbonden aan PayPal Merchant Rekening** (Facultatief) gaat het e-mailadres in verbonden aan uw handels PayPal rekening. Deze e-mail is hoofdlettergevoelig.
   * **Methoden van de Authentificatie van API** als API Handtekening of API Certificaat.
   * Gebruikersnaam, wachtwoord en handtekening van de API die zijn vastgelegd via uw Paypal-account.
   * **de Wijze van Sandbox** uitgezocht ja of Nr om erop te wijzen als de geloofsbrieven u inging voor zandbak zijn. Als u productiereferenties hebt ingevoerd, selecteert u Nee.
   * **API gebruikt Volmacht** uitgezocht ja of Neen om te plaatsen als het systeem een volmachtsserver gebruikt om een verbinding tussen Adobe Commerce en het PayPal betalingssysteem te vestigen. Als ja, ga de volmachtsgastheer en de haven in.

1. Voor gedetailleerde informatie en stappen voor het vormen van uw rekening, zie [&#x200B; Uitdrukkelijke Controle PayPal &#x200B;](https://experienceleague.adobe.com/nl/docs/commerce-admin/stores-sales/payments/paypal/paypal-express-checkout) die met Stap 2 begint voltooit de Vereiste Montages.

Als de account is geconfigureerd en geverifieerd, kunt u PayPal-betalingsopties in- en uitschakelen bij Vereiste PayPal-instellingen:

* **laat deze Oplossing** toe toont de betaalmethode PayPal aan klanten door de website.
* **laat Ervaring In-Context Checkout** toe
* **laat Krediet van PayPal** toe klanten aan PayPal kredietfinanciering zonder extra kosten. PayPal betaalt de bestelling vooraf en verwerkt alle aflossingen voor het krediet rechtstreeks bij de klant.

## PayPal-variabelen

Als u het PayPal-programma voor instapcontrole gebruikt met Adobe Commerce op een cloudinfrastructuur, voegt u de volgende variabele toe aan de sectie `variables:env` van het `magento.app.yaml` -bestand.

```yaml
# Environment variables
variables:
  env:
    CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
```

Als u aan 2.2 van 2.1.8 of later bevordert, moet u nog deze variabele toevoegen.
