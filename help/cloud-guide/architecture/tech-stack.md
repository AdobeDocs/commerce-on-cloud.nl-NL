---
title: Technologiestapel
description: Bekijk de technologiestapel die de Commerce op Cloud-infrastructuur vormt.
feature: Cloud, Iaas, Paas
exl-id: 3fac1ab7-6440-4bf9-8169-9fadf51d70dd
source-git-commit: 5fc2082ca2aae8a1466821075c01ce756ba382cc
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Technologiestapel

U kunt de Adobe Commerce op cloudinfrastructuur beschouwen als vijf functionele lagen, zoals hieronder wordt getoond:

![&#x200B; de stapel van de Wolk &#x200B;](../../assets/CloudStack.svg)

1. [**de Infrastructuur van de Wolk**](pro-architecture.md): Kies of Amazon Web Services (AWS) of Microsoft Azure als uw Infrastructuur als stichting van de Dienst (IaaS) voor uw Adobe Commerce op de projecten van de wolkeninfrastructuur Pro.

   Adobe analyseert routinematig uw gebruik van uw virtuele computerbron (vCPU) en wijst automatisch bronnen toe om uw langetermijngebruik te optimaliseren en het risico te beperken dat uw maximale jaarlijkse vCPU-daglimiet wordt overschreden. Als u verhoogd plaatsverkeer voor specifieke tijdsperioden verwacht, moet u een kaartje van de Steun blijven openen om [&#x200B; om tijdelijk te verzoeken upsize &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/how-to-request-temporary-magento-upsize.html?lang=nl-NL).

1. [**Platform als Dienst**](cloud-architecture.md): Elke Adobe Commerce op het project van de wolkeninfrastructuur verstrekt een Platform als milieu van de Integratie van de Dienst (PaaS) voor het ontwikkelen, het testen, en het integreren van de diensten.
1. [**Adobe Commerce**](../project/overview.md): Adobe Commerce op wolkeninfrastructuur verstrekt een pre-provisioned infrastructuur die PHP, MySQL (MariaDB), Redis, de diensten van de berichtrij ([!DNL RabbitMQ] of [!DNL ActiveMQ]) omvat, en de gesteunde technologieën van de onderzoeksmotor.
1. [**Hulpmiddelen van Prestaties**](../monitor/new-relic-service.md): De prestatieshulpmiddelen van New Relic laten u toe om, uw toepassingen en infrastructuur te zuiveren te controleren en te beheren door, gegevens van uw Adobe Commerce op de projecten van de wolkeninfrastructuur te verzamelen te analyseren en te tonen.
1. [**Netwerk van de Levering van de Inhoud (CDN), de Firewall van de Toepassing van het Web ([!DNL WAF]), en Optimalisering van het Beeld (IO)**](../cdn/fastly.md):

   * [&#x200B; snel CDN &#x200B;](../cdn/fastly.md#ddos-protection) - verleent de veilige diensten CDN met ingebouwde bescherming tegen Verdeelde Ontkenning van de aanvallen van de Dienst (DDoS) zoals [!DNL Ping of Death], [!DNL Smurf] aanvallen, en andere Internet Control Message Protocol (ICMP) gebaseerde overstromingsaanvallen.
   * {de 0} Firewall van de Toepassing van het Web (WAF) [&#x200B; - de diensten van WAF verzekeren naleving PCI voor Adobe Commerce storefronts in productiemilieu&#39;s en beleid van WAF die uw Adobe Commerce Webtoepassingen tegen injectieaanvallen, kwaadwillige input, dwars-plaats scripting, gegevensextractie, het protocolschendingen van HTTP, en andere &#x200B;](../cdn/fastly-waf-service.md) Hoogste Tien veiligheidsbedreigingen [[!DNL OWASP]  beschermen.](https://owasp.org/www-project-top-ten/)
   * [&#x200B; optimalisering van het Beeld (IO) &#x200B;](../cdn/fastly-image-optimization.md) - verstrekt beeldmanipulatie in real time en optimalisering om beeldlevering te versnellen en onderhoud van beeldbronreeksen voor ontvankelijke Webtoepassingen te vereenvoudigen. Met de snelste IO wordt het laden van images geoffload en de grootte van de images aangepast, zodat servers bestellingen en conversies efficiënt kunnen verwerken.

Monolithische toepassingen zijn hulpbronnenintensief en moeilijk te schalen en snel te gebruiken. Met de Cloud-infrastructuur krijgen Commerce-klanten ongeëvenaarde toegang tot SaaS-gebaseerde microservices die rijk, intelligent en krachtig zijn. Zie [&#x200B; Ondersteunde software en de diensten &#x200B;](cloud-architecture.md#supported-software-and-services).

Gebruik [&#x200B; Commerce krijgt Begonnen gids &#x200B;](../../get-started/overview.md) aan opstelling uw nieuw programma van de Wolk en begint uw [!DNL Commerce] toepassing in een wolk-inheemse milieu te beheren.
