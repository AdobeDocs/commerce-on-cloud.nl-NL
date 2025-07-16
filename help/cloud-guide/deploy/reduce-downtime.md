---
title: Implementatie zonder downtime
description: Leer hoe u de algemene downtime kunt verminderen bij de implementatie van Adobe Commerce op cloudinfrastructuuroplossingen.
feature: Cloud, Deploy, SCD, Themes
exl-id: c216c5e9-d787-4428-b67a-b6aee814ded5
source-git-commit: b831bc5bce0f76ec8972b3578c500508dd4d7d41
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Implementatie zonder downtime

Adobe Commerce op de looppas van de wolkeninfrastructuur de toepassing op [_onderhoud_ wijze ](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/setup/application-modes.html#production-mode) tijdens de opstellen fase, die uw plaats offline neemt tot de plaatsing volledig is. De tijdsduur uw plaats van de Productie is op onderhoudswijze hangt van de grootte van de plaats, het aantal veranderingen af die tijdens de plaatsing worden toegepast, en de configuratie voor statische inhoudsplaatsing. Het is mogelijk om uw project te vormen zodat het met a **nul** downtime effect opstelt.

Tijdens het plaatsingsproces, staan alle verbindingen voor maximaal 5 minuten het bewaren van om het even welke actieve zittingen en hangende acties, zoals het toevoegen aan karretje of controle in de rij. Na plaatsing, wordt de rij vrijgegeven en de verbindingen blijven zonder onderbreking. Om deze _verbinding te gebruiken greep_ aan uw voordeel en plaatsing te verminderen aan _nul_ onderbreking, moet u uw project vormen om de meest efficiënte op te stellen strategie te gebruiken.

>[!NOTE]
>
>Om te verifiëren of uw project van de Wolk optimaal wordt gevormd om plaatsing onderbreking te minimaliseren, gebruik de [ Slimme Tovenaar ](smart-wizards.md). De slimme Tovenaar controleert uw huidige opstelling en begeleidt u door geadviseerde configuratieaanpassingen om beste praktijken voor nul-onderbreking plaatsingen toe te laten.

Gebruik de volgende stappen om de hoeveelheid tijd te verminderen die uw winkel nodig heeft om een update naar Production te implementeren:

1. [ Verbetering aan het `ece-tools` pakket ](../dev-tools/install-package.md) of [ werk `ece-tools` versie ](../dev-tools/update-package.md) bij
Uw Adobe Commerce on cloud-infrastructuurproject moet beschikken over het nieuwste `ece-tools` -pakket, zodat u over de tools beschikt om een optimale implementatie te configureren. Als u over de laatste `ece-tools` beschikt, gaat u verder met de volgende stap.

   >[!NOTE]
   >
   >Alhoewel het een beste praktijk is om het recentste `ece-tools` pakket te gebruiken, de nul-onderbreking plaatsingsmethode werkt met `ece-tools` [ versie 2002.0.13 ](../release-notes/cloud-release-archive.md#v2002013) en later.

1. [ vorm statische inhoudsplaatsing ](static-content.md)
Als de statische plaatsing van inhoud in de plaatsingsfase ontbreekt, wordt uw plaats geplakt op onderhoudswijze. Wanneer een mislukking tijdens de bouwstijlfase voorkomt, vermijdt het proces onderbreking omdat het nooit begint opstellen fase. [ het produceren van statische inhoud tijdens de bouwstijlfase met geminiateerde HTML ](static-content.md#setting-the-scd-on-build), die ook als ideale staat wordt bekend, is de optimale configuratie voor nul-onderbreking plaatsingen en _verhindert_ onderbreking als een mislukking voorkomt.

1. [ vorm de post-opstellen haak ](../application/hooks-property.md)
U moet de naimplementatiehaak vormen om de cache op te schonen en op te warmen. Door gebrek, komt het geheime voorgeheugen schoon tijdens de opstellen fase voor wanneer de plaats neer is. Als u het cachegeheugen naar de fase na implementatie verplaatst, blijft de cache actief totdat de implementatiefase is voltooid en kunt u de cache veilig opschonen.

   Pas de lijst van pagina&#39;s aan die worden gebruikt om het geheime voorgeheugen met [ te laden WAM_UP_PAGES milieuvariabele ](../environment/variables-post-deploy.md#warmuppages).

1. [ Reduceer themadossiers ](../environment/variables-deploy.md#scdmatrix)
U kunt het aantal onnodige themabestanden verminderen door de SCD\_MATRIX-omgevingsvariabele te configureren.

1. [ Versnelt omhoog statische inhoudsplaatsing ](../environment/variables-deploy.md#scdthreads)
U kunt het plaatsingsproces versnellen door de SCD\_THREADS milieuvariabele bij te werken om het aantal draden voor statische inhoudsplaatsing te verhogen.

>[!NOTE]
>
>U kunt uw projectconfiguratie voor optimale plaatsing bevestigen door [ in werking te stellen de ideale staatstovenaar ](smart-wizards.md#verifying-an-ideal-configuration).
