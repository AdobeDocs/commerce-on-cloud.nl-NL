---
title: Aanmelden bij  [!DNL Cloud Console]
description: Leer over  [!DNL Cloud Console]  voor Adobe Commerce op de infrastructuur van de Wolk.
recommendations: noDisplay, catalog
last-substantial-update: 2024-02-06T00:00:00Z
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Aanmelden bij [!DNL Cloud Console]

[!DNL Cloud Console] biedt interactieve methoden voor het samenstellen, beheren en implementeren van Commerce-code. [!DNL Cloud Console] is een modernere, gebruiksvriendelijke ervaring en legt de basis voor toekomstige interfaceverbeteringen.

[&#x200B; Login aan  [!DNL Cloud Console] &#x200B;](https://console.adobecommerce.com) om uw projectlijst te bekijken.

![&#x200B; lijst van het Project &#x200B;](../assets/ui-allprojects-list.png)

## Functies

De nieuwe of verbeterde functies zijn onder meer:

- Duidelijk overzicht van project en milieu kenmerken
- Activiteitsstroom met sorteerbare geschiedenis
- Handmatig back-upbeheer en geschiedenis voor Starter-projecten
- Verbeterde logweergaven
- Sorteerbare lijsten
- Eenvoudige formulieren en richtlijnen voor het toevoegen van integratie
- WCAG-compatibiliteit (Web Content Accessibility Guidelines)

![[!DNL Cloud Console]](../assets/CloudConsole.svg)

De nieuwe of verbeterde functies zijn als volgt:

| Functie | Verbeteringen |
| -------------- | ----------------------------------- |
| [&#x200B; stroom van de Activiteit &#x200B;](../cloud-guide/project/activity-stream.md) | Communiceer met een sorteerbare lijst met actieve, hangende of historische handelingen. Selecteer een activiteit en bekijk logboeken of annuleer een lopende bouwstijl. |
| [&#x200B; project en Omgeving overzichten &#x200B;](../cloud-guide/project/overview.md#project-overview) | Open uw project en zie het overzicht van projectdetails en milieulijst. Het overzicht van het milieu verstrekt meer details over de milieustatus, toepassingstoegang, en recente activiteiten. |
| [&#x200B; de vormen van de Integratie &#x200B;](../cloud-guide/integrations/overview.md) | Gebruik eenvoudige formulieren en richtlijnen om integraties toe te voegen, zoals meldingen over bitmaps of Slacks. |
| [&#x200B; lijst van het Project &#x200B;](../cloud-guide/project/overview.md#cloud-console) | De _Alle projecten_ mening maakt een lijst van alle projecten die u toestemming hebt om toegang te hebben. U kunt op **[!UICONTROL Show filters]** klikken en uw projectlijst filteren op type, gebied of plan. |
| [&#x200B; Veranderlijke zichtbaarheidsopties &#x200B;](../cloud-guide/environment/variable-levels.md) | Beperk de zichtbaarheid van een variabele op projectniveau of op milieuniveau tijdens het maken of uitvoeren. |

<!-- The following are features yet to be activated:
| **Apps and services topology** | The Apps & Services topology is visible on Project and Environment views. This interactive diagram allows you to select a service and view the relationship details, such as name, type, version, port, and more. Click **[!UICONTROL View details]** to access the overview and configuration panel for each service. | -->

## Console-vragen

**_waar kan ik de eigenschap van Momentopnamen_** vinden?

Voor [!DNL Starter] projecten, wordt de eigenschap van Momentopnamen nu genoemd _Steunen_. U kunt een handmatige back-up van uw [!DNL Starter] -omgeving maken vanuit [!DNL Cloud Console] of een momentopname maken vanuit de Cloud CLI. U moet een beheerdersrol voor het milieu hebben.

Selecteer een omgeving in de projectnavigatiebalk. De omgeving moet actief zijn. Selecteer de tab **[!UICONTROL Backups]** . Deze optie is momenteel niet beschikbaar voor Pro-omgevingen.

**_waar is de lijst van gevormde routes voor het milieu_**?

U kunt de lijst van gevormde routes op het _lusje van de Diensten_ voor een milieu vinden.

Selecteer een omgeving in de projectnavigatiebalk. Selecteer de tab **[!UICONTROL Services]** . Het **overzicht van de Router** toont de gevormde routes. U kunt momenteel geen route toevoegen vanuit de nieuwe [!DNL Cloud Console] .

## Het menu Account

In de rechterbovenhoek bevindt zich het accountmenu. Klik op de pijl-omlaag voor het menu en selecteer **[!UICONTROL My Profile]** . In de _Mijn mening van het Profiel_, kunt u uw gebruikersdetails en vertoningsmontages controleren, [&#x200B; veiligheidsauthentificatie &#x200B;](../cloud-guide/project/user-access.md#user-authentication-requirements), [&#x200B; API tokens &#x200B;](../cloud-guide/project/user-access.md#create-an-api-token), en [&#x200B; sleutels van SSH &#x200B;](../cloud-guide/development/secure-connections.md) beheren.
