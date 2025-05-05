---
title: PrivateLink-service
description: Leer hoe u de PrivateLink-service gebruikt om een veilige verbinding tot stand te brengen tussen een privécloud en een Adobe Commerce-cloudplatform in dezelfde regio.
feature: Cloud, Iaas, Security
source-git-commit: 1e789247c12009908eabb6039d951acbdfcc9263
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# PrivateLink-service

Adobe Commerce op de infrastructuur van de wolk steunt integratie met [ AWS PrivateLink ](https://aws.amazon.com/privatelink/) of [ Azure Private Link ](https://learn.microsoft.com/en-us/azure/private-link/) dienst. U kunt PrivateLink gebruiken om veilige, persoonlijke communicatie tot stand te brengen tussen Adobe Commerce in omgevingen met cloudinfrastructuren met services en toepassingen die worden gehost op externe systemen. Zowel de Adobe Commerce-toepassing als externe systemen moeten toegankelijk zijn via Virtual Private Cloud (VPC)-eindpunten die op hetzelfde cloudplatform (AWS of Azure) in dezelfde cloudregio zijn geconfigureerd.

>[!TIP]
>
>PrivateLink kan het best worden gebruikt voor het beveiligen van verbindingen voor niet-HTTP(S)-integratie, zoals database- of bestandsoverdrachten. Als u van plan bent om uw toepassing met Adobe Commerce APIs te integreren, zie hoe te om een [ Adobe API Net ](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/) in _API Net voor Adobe Developer App Builder_ tot stand te brengen.

## Functies en ondersteuning

De PrivateLink-service-integratie voor Adobe Commerce op cloud-infrastructuurprojecten omvat de volgende functies en ondersteuning:

- Een veilige verbinding tussen een klant Virtual Private Cloud (VPC) en de Adobe VPC op hetzelfde cloudplatform (AWS of Azure) in dezelfde Cloud-regio.
- Steun voor unidirectionele of bidirectionele communicatie tussen eindpuntdiensten beschikbaar bij Adobe en Klant VPCs.
- Inschakelen van service:

   - Open vereiste poorten in de Adobe Commerce in de cloud-infrastructuuromgeving
   - De eerste verbinding tussen de klant en Adobe-VPC&#39;s tot stand brengen
   - Verbindingsproblemen oplossen tijdens inschakelen

## Beperkingen

- Ondersteuning voor PrivateLink is alleen beschikbaar in Pro Production- en Staging-omgevingen. Het is niet beschikbaar op lokale of integratieomgevingen, of op Starter-projecten.
- U kunt geen verbindingen tot stand brengen SSH gebruikend PrivateLink. Zie [ SSH sleutels ](secure-connections.md) toelaten.
- Adobe Commerce-ondersteuning biedt geen ondersteuning voor het oplossen van problemen met AWS PrivateLink buiten initiële activering.
- Klanten zijn verantwoordelijk voor de kosten die gepaard gaan met het beheer van hun eigen VPC.
- U kunt niet het protocol HTTPS (haven 443) gebruiken om met Adobe Commerce op wolkeninfrastructuur over Azure Privé Verbinding te verbinden toe te schrijven aan [ Snelle oorsprong het camoufleren ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/faq/fastly-origin-cloaking-enablement-faq.html?lang=nl-NL). Deze beperking geldt niet voor AWS PrivateLink.
- PrivateDNS is niet beschikbaar.

## Verbindingstypen van PrivateLink

Er zijn twee PrivateLink verbindingstypes beschikbaar-getoond in het volgende netwerkdiagram-om veilige communicatie tussen uw opslag en externe systemen te vestigen die buiten het milieu van de Wolk worden ontvangen.

![ PrivateLink netwerkdiagram ](../../assets/privatelink-architecture-diagram.png)

Kies een van de verbindingstypen voor PrivateLink die het meest geschikt zijn voor uw Adobe Commerce in omgevingen met cloudinfrastructuren:

- **Unidirectional PrivateLink** - verkies deze configuratie om gegevens veilig van een Adobe Commerce op de opslag van de wolkeninfrastructuur terug te winnen.
- **bidirectional PrivateLink** - verkies deze configuratie om veilige verbindingen aan en van systemen buiten Adobe Commerce op het milieu van de wolkeninfrastructuur te vestigen. De bidirectionele optie vereist twee verbindingen:

   - Een verbinding tussen de klant VPC en de Adobe VPC
   - Een verbinding tussen de Adobe VPC en de klant VPC

>[!TIP]
>
>Werk met uw netwerkbeheerder of Cloud platform provider voor hulp bij het selecteren van het verbindingstype PrivateLink of hulp bij het instellen en beheren van VPC. Zie het platform PrivateLink van de Wolk documentatie: [ AWS PrivateLink ](https://aws.amazon.com/privatelink/) of [ Azure Private Link ](https://learn.microsoft.com/en-us/azure/private-link/).

## Enable PrivateLink aanvragen

>[!WARNING]
>
>Het toelaten van PrivateLink kan tot _vijf_ bedrijfsdagen nemen. Het verstrekken van onvolledige of onjuiste informatie kan het proces vertragen.

### Vereisten

![ controle ](../../assets/fix.svg) de rekening van de Wolk van A (AWS of Azure) in het zelfde gebied zoals Adobe Commerce op de instantie van de wolkeninfrastructuur.

![ controle ](../../assets/fix.svg) een VPC in het klantenmilieu dat gastheren de diensten om door PrivateLink te verbinden. Raadpleeg de documentatie bij AWS of Azure voor hulp bij de installatie van VPC of neem contact op met uw netwerkbeheerder.

![ controle ](../../assets/fix.svg) voor bidirectionele verbindingen PrivateLink, moet u de configuratie van de eindpuntdienst voor uw toepassing of dienst tot stand brengen, en een eindpunt in uw milieu van VPC creëren alvorens om PrivateLink te verzoeken enablement. Zie [ Opstelling voor bidirectionele verbindingen PrivateLink ](#set-up-for-bidirectional-privatelink-connections).

Verzamel de volgende gegevens die voor PrivateLink worden vereist toelaat:

- **de rekeningsaantal van de Klant Cloud** (AWS of Azure) - moet in het zelfde gebied zoals Adobe Commerce op de instantie van de wolkeninfrastructuur zijn
- **gebied van de Wolk** - verstrek het gebied van de Wolk waar de rekening voor verificatiedoeleinden wordt ontvangen
- **de Diensten en communicatie havens** - de Adobe moet havens openen om de dienstmededeling tussen VPCs, bijvoorbeeld SQL haven 3306, haven 2222 toe te laten SFTP
- **identiteitskaart van het Project** - verstrek Adobe Commerce op het projectidentiteitskaart van de wolkeninfrastructuur Pro. U kunt identiteitskaart van het Project en andere projectinformatie krijgen gebruikend het volgende [ CLI van de Wolk ](../dev-tools/cloud-cli-overview.md) bevel: `magento-cloud project:info`
- **het type van Verbinding** - specificeer unidirectioneel of bidirectioneel voor verbindingstype
- **de dienst van het Eindpunt** - voor bidirectionele verbindingen PrivateLink, verstrek DNS URL voor de het eindpuntdienst van VPC die de Adobe met moet verbinden, bijvoorbeeld: `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`
- **verleende de diensttoegang van het Eindpunt** - om met de externe dienst te verbinden, de toegang van de eindpuntdienst tot het volgende de rekeningshoofd van AWS toestaan: `arn:aws:iam::402592597372:root`

  >[!WARNING]
  >
  >Als de toegang tot de eindpuntdienst niet wordt verleend, dan wordt de bidirectionele verbinding PrivateLink aan de dienst in uw VPC **niet** toegevoegd, die de opstelling vertraagt.

#### Aanvullende voorwaarden specifiek voor Azure Private Link-activering

- Geef de cluster-id op; gebruik SSH, meld u aan bij de externe server en gebruik de opdracht: `cat /etc/platform_cluster`
- Een externe service kan alleen verbinding maken met uw Adobe Commerce Pro-cluster als u:

   - Een lijst van havens op uw Pro cluster om aan het nieuwe externe Privé Eindpunt bloot te stellen
   - Een lijst van Azure abonnement IDs voor de verbindingen van het Privé Eindpunt

- Als u uw Adobe Commerce Pro-cluster wilt verbinden met een externe service, hebt u het volgende nodig:

   - Een lijst van middel IDs voor de doeldiensten. De externe Privé dienst IDs van de Verbinding kijken gelijkaardig aan het volgende:

  ```text
  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/privateLinkServices/{svcNameID}
  ```

### Workflow Enablement

In de volgende workflow wordt beschreven hoe u PrivateLink-integratie met Adobe Commerce kunt inschakelen voor cloudinfrastructuur.

1. **Klant** legt een steunkaartje voor die om PrivateLink toelaat met de onderwerpregel `PrivateLink support for <company>` verzoekt. Omvat de [ gegevens die voor enablement ](#prerequisites) in het kaartje worden vereist. De Adobe gebruikt het kaartje van de Steun om mededeling tijdens het enablement proces te coördineren.

1. **Adobe** laat de toegang van de klantenrekening tot de eindpuntdienst in de Adobe VPC toe.

   - Werk de de dienstconfiguratie van het eindpunt van de Adobe bij om verzoeken goed te keuren die van de klantAWS of de Azure rekening in werking worden gesteld.
   - Werk het kaartje van de Steun bij om de de dienstnaam voor het eindpunt van AdobeVPC te verstrekken om te verbinden met, bijvoorbeeld `com.amazonaws.vpce.<cloud-region>.vpce-svc-<service-id>`.

1. **Klant** voegt de dienst van het eindpunt van de Adobe aan hun rekening van de Wolk (AWS of Azure) toe, die een verbindingsverzoek aan Adobe teweegbrengt. Raadpleeg de documentatie bij het Cloud-platform voor instructies:

   - Voor AWS, zie [ Accepterend en verwerpend de verbindingsverzoeken van het interfaceeindpunt ].
   - Voor Azure, zie [ verbindingsverzoeken ] leiden.

1. **Adobe** keurt het verbindingsverzoek goed.

1. Na de goedkeuring van het verbindingsverzoek, **verifieert de klant** [ de verbinding ](#test-vpc-endpoint-service-connection) tussen hun VPC en Adobe VPC.

1. Aanvullende stappen om tweerichtingsverbindingen in te schakelen:

   - **Adobe** levert het belangrijkste van de de rekeningsrekening van de Adobe (wortelgebruiker voor AWS of Azure rekening) en vraagt toegang tot de klantVPC eindpuntdienst.
   - **Klant** laat de toegang van de Adobe tot de eindpuntdienst in klantVPC toe. Dit veronderstelt dat het hoofd van de rekening van de Adobe toegang tot `arn:aws:iam::402592597372:root` heeft, zoals eerder beschreven in de **verleende de diensttoegang van het Eindpunt** voorwaarde.

      - Werk de de dienstconfiguratie van het klanteneindpunt bij om verzoeken goed te keuren die van de rekening van de Adobe in werking worden gesteld. Raadpleeg de documentatie bij het Cloud-platform voor instructies:

         - Voor AWS, zie [ Toevoegend en verwijderend toestemmingen voor uw eindpuntdienst ].
         - Voor Azure, zie [ een Privé verbinding van het Eindpunt beheren ]

      - Verstrek Adobe van de eindpuntdienstnaam voor de klant VPC.

   - **Adobe** voegt de dienst van het klanteneindpunt aan de rekening van het Adobe platform (AWS of Azure) toe, die een verbindingsverzoek aan klant VPC teweegbrengt.
   - **Klant** keurt het verbindingsverzoek van Adobe goed om de opstelling te voltooien.
   - **Klant** [ verifieert de verbinding ](#test-vpc-endpoint-service-connection) van de Adobe VPC.

## VPC-eindpuntserviceverbinding testen

U kunt de toepassing van Telnet gebruiken om de verbinding aan de de eindpuntdienst van VPC te testen.

**om de verbinding aan de het eindpuntdienst van VPC te testen**:

1. Van de folder van de projectwortel, **controle** het het Opvoeren of milieu van de Productie die wordt gevormd om tot de PrivateLink eindpuntdienst toegang te hebben.

   ```bash
   magento-cloud environment:checkout <environment-id>
   ```

1. Voer de volgende CURL-opdracht uit:

   ```bash
   curl -v telnet://<endpoint-service-dns-url>:<port>/
   ```

   Voorbeeld:

   ```
   $ curl -v telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80 -vvv
   ```

   Voorbeeld van succesvolle reactie:

   ```
   * Rebuilt URL to: telnet://vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce.amazonaws.com:80
   * Connected to vpce-0088d56482571241d-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.us-east-1.vpce. amazonaws.com (191.210.82.246) port 80 (#0)
   ```

   Monster is mislukt antwoord:

   ```
   Failed to connect to vpce-007ffnb9qkcnjgult-yfhmywqh.vpce-svc-083cqvm2ta3rxqat5v.ap-southeast-1.vpce.amazonaws.com port 80: Connection timed out
   * Closing connection 0
   ```

1. Controleer of de service luistert op de VM.

   ```bash
   netstat -na | grep <port>
   ```

1. Controleer de pakketstroom.

   ```bash
   tcpdump -i <ethernet-interface> -tt -nn port <destination-port> and host <source-host>
   ```

   Controleer de volgende interne instellingen om te controleren of de configuratie geldig is:

   - Instellingen voor eindpunten- en eindpuntservices
   - NLB-instellingen (Network Load Balancer)
   - De doelgroepen in NLB en controleren of zij gezond zijn
   - De URL voor het netwerkpunt/curl-eindpunt van elke VM (hierboven vermeld)

   Raadpleeg de volgende artikelen voor hulp bij het oplossen van problemen met verbindingen:

   - [ AWS: De verbindingen van de eindpuntdienst van het oplossen van problemen ]
   - [ Amazon: Het oplossen van problemen Azure Privé de connectiviteitsproblemen van de Verbinding ]

   Als u de fouten niet kunt oplossen, werkt u het Adobe Commerce Support-ticket bij om hulp te vragen bij het vaststellen van de verbinding.

## De configuratie van PrivateLink wijzigen

[ leg een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=nl-NL#submit-ticket) voor om een bestaande configuratie te veranderen PrivateLink. U kunt bijvoorbeeld de volgende wijzigingen aanvragen:

- Verwijder de PrivateLink-verbinding van de Adobe Commerce op de Pro-productie- of Staging-omgeving van de cloudinfrastructuur.
- Wijzig het accountnummer van het Cloud-platform van de klant voor toegang tot de eindpuntservice van de Adobe.
- Voeg of verwijder verbindingen PrivateLink van de Adobe VPC aan andere eindpuntdiensten toe beschikbaar in het milieu van klantVPC.

## Instellen voor bidirectionele Private Link-verbindingen

De klant VPC moet de volgende middelen beschikbaar hebben om bidirectionele verbindingen te steunen PrivateLink:

- Een netwerktaakverdeler (NLB)
- Een configuratie van de eindpuntdienst die toegang tot een toepassing of de dienst van klant VPC toelaat
- Een [ interfaceeindpunt ] (AWS) of [ privé eindpunt ] (Azure) dat Adobe toestaat om met eindpuntdiensten te verbinden die in uw VPC worden ontvangen

Als deze bronnen niet beschikbaar zijn in de VPC van de klant, moet u zich aanmelden bij uw Cloud-platformaccount om de configuratie toe te voegen.

- Amazon VPC-console- `https://console.aws.amazon.com/vpc/`
- Azure Portal- `https://portal.azure.com`

Raadpleeg de documentatie bij het Cloud-platform voor instructies voor het instellen van Private Link:

- **AWS PrivateLink documentatie**
   - [ creeer een Balancer van de Lading van het Netwerk ]
   - [ creeer een configuratie van de eindpuntdienst ]
   - [ creeer een interfaceeindpunt ]
   - [ de eindpuntlevenscyclus van de Interface ]

- **Azure PrivateLink documentatie**
   - [ creeer een Balancer van de Lading ]
   - [ Azure Private Link-workflow ]

<!--Link definitions-->

[Accepterend en verwerpend de verbindingsverzoeken van het interfaceeindpunt]: https://docs.aws.amazon.com/vpc/latest/userguide/accept-reject-endpoint-requests.html
[Het toevoegen van en het verwijderen van toestemmingen voor uw eindpuntdienst]: https://docs.aws.amazon.com/vpc/latest/userguide/add-endpoint-service-permissions.html
[Amazon: Problemen met de Azure Private Link-connectiviteit oplossen]: https://docs.microsoft.com/en-us/azure/private-link/troubleshoot-private-link-connectivity
[AWS: Problemen oplossen, eindpuntserviceverbindingen]: https://aws.amazon.com/premiumsupport/knowledge-center/connect-endpoint-service-vpc/
[Azure Private Link-workflow]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#workflow
[Een taakverdeling maken]: https://docs.microsoft.com/en-us/azure/load-balancer/quickstart-load-balancer-standard-public-portal
[Creeer een Balans van de Lading van het Netwerk]: https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-network-load-balancer.html
[Creeer een configuratie van de eindpuntdienst]: https://docs.aws.amazon.com/vpc/latest/userguide/create-endpoint-service.html
[Creeer een interfaceeindpunt]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint
[interface endpoint lifecycle]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-lifecycle
[interface-eindpunt]: https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html
[Een verbinding met een privé-eindpunt beheren]: https://docs.microsoft.com/en-us/azure/private-link/manage-private-endpoint
[Verbindingsverzoeken beheren]: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview#manage-your-connection-requests
[privé-eindpunt]: https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview
