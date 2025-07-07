---
title: E-mailservice SendGrid
description: Leer over de SendGrid e-mailservice voor Adobe Commerce op cloudinfrastructuur en hoe u uw DNS-configuratie kunt testen.
exl-id: 06236068-df32-468f-99ec-c379984be136
source-git-commit: 771fc9d0aed0e3ab6b9d693e7274ce1a7ffcf7ad
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---

# E-mailservice SendGrid

De SendGrid Eenvoudige de volmachtsdienst van de Overdracht van de Post van het Protocol (SMTP) verleent de uitgaande e-mailauthentificatie en reputatie controlediensten, met inbegrip van steun voor:

* Alle uitgaande e-mails over een transactie
* Specifieke IP-adressen
* Domeinregistratie, DomainKeys Identified Mail (DKIM)-handtekeningen voor e-maildomeinvalidatie (alleen voor Pro Staging- en Production-omgevingen)
* Aangepaste domeinregistratie (alleen voor Pro)
* Geautomatiseerde integratie voor Starter- en Pro-integratieomgevingen. Pro-productie- en staging-omgevingen vereisen handmatige provisioning en configuratie tijdens het hardwareinrichtingsproces voor de infrastructuur als service (IaaS)

De SMTP-proxy van SendGrid is niet bedoeld voor gebruik als e-mailserver voor algemene doeleinden voor het ontvangen van binnenkomende e-mail of voor gebruik met e-mailmarketingcampagnes. Als u welkome e-mails wilt importeren en verzenden naar een groot aantal klanten (bijvoorbeeld 10.000 of meer), splitst u het importeren en verzenden van e-mailberichten over meerdere dagen. Deze praktijk helpt binnen dagelijkse verzendende grenzen te blijven en beschermt uw afzenderreputatie.

>[!TIP]
>
>Zorg ervoor dat u de juiste e-mailadressen van de winkel in Admin hebt geconfigureerd door naar Opslagruimten > Configuratie > Algemeen te gaan om problemen met de te leveren items en domeinverificatie te voorkomen. U moet **[!UICONTROL Use Default]** uitschakelen en de standaardwaarden vervangen door een domein dat u bezit. E-mailservices van openbare of gedeelde domeinen, zoals gmail.com en outlook.com, moeten niet worden geconfigureerd als het e-mailadres van de afzender wanneer e-mails via Sendgrid worden verzonden.

## E-mail in- of uitschakelen

U kunt uitgaande e-mailberichten voor elke omgeving in- of uitschakelen via de cloudconsole of de opdrachtregel.

Standaard zijn uitgaande e-mails ingeschakeld in Pro Production- en Staging-omgevingen. Nochtans, [!UICONTROL Outgoing emails] kan gehandicapt in de milieu montages verschijnen tot u het `enable_smtp` bezit door de [ bevellijn ](outgoing-emails.md#enable-emails-in-the-cli) of [ Console van de Wolk ](outgoing-emails.md#enable-emails-in-the-cloud-console) plaatst. U kunt uitgaande e-mails voor integratie- en staging-omgevingen inschakelen om tweefasenverificatie te verzenden of wachtwoorde-mails voor gebruikers van Cloud-projecten opnieuw in te stellen. Zie [ e-mails voor het testen ](outgoing-emails.md) vormen.

Als de uitgaande e-mails moeten worden onbruikbaar gemaakt of op ProProductie of het Opvoeren milieu&#39;s opnieuw worden toegelaten, kunt u een [ kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) voorleggen.

>[!TIP]
>
>Het bijwerken van de [!UICONTROL enable_smtp] bezitswaarde door [ bevellijn ](outgoing-emails.md#enable-emails-in-the-cli) verandert ook de [!UICONTROL Enable outgoing emails] plaatsende waarde voor dit milieu op de [ Console van de Wolk ](outgoing-emails.md#enable-emails-in-the-cloud-console).

## SendGrid-dashboard

Alle Cloud-projecten worden beheerd onder een centraal account, zodat alleen Support toegang heeft tot het SendGrid-dashboard. SendGrid biedt geen beperkingen voor subaccounts.

Om de logboeken van de Activiteit voor leveringsstatus of een lijst van teruggestuurde, verworpen of geblokkeerde e-mailadressen te herzien, [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) voorleggen. Het team van de Steun **kan** activiteitenlogboeken niet terugwinnen ouder dan 30 dagen.

Indien mogelijk, neem de volgende informatie met uw verzoek op:

* het desbetreffende e-mailadres of -adres
* het betrokken tijdschema (alleen binnen de afgelopen 30 dagen)
* het onderwerp van de e-mail

## DomainKeys Identified Mail (DKIM)

DKIM is een technologie van de e-mailauthentificatie die de Dienstverleners van Internet (ISPs) toelaat om zowel wettige als nep afzenderadressen, een techniek te identificeren die algemeen in phishing en e-mailzwendel wordt gebruikt. DKIM is afhankelijk van een domeineigenaar die de DNS-records beheert. Wanneer u DKIM gebruikt, gebruikt de server van de afzender een persoonlijke sleutel om de berichten te ondertekenen. Bovendien voegt de eigenaar van het domein een DKIM-record (een gewijzigde `TXT` -record) toe aan de DNS-records van het afzender-domein. Deze `TXT` -record bevat een openbare sleutel die door e-mailservers van ontvangers wordt gebruikt om de handtekening van een bericht te controleren. De openbare-zeer belangrijke cryptografieprocedure van DKIM laat ontvangers toe om de authenticiteit van een afzender te verifiëren. Zie [ Verklaarde de Verslagen van DKIM ](https://docs.sendgrid.com/ui/account-and-settings/dkim-records).

>[!WARNING]
>
>De handtekeningen van SendGrid DKIM en de steun van de domeinauthentificatie zijn slechts beschikbaar op de Productie en het Staging milieu&#39;s voor Pro projecten, maar niet voor alle milieu&#39;s van de Aanzet. Als gevolg hiervan worden uitgaande e-mailberichten over transacties waarschijnlijk gemarkeerd door spamfilters. Als u DKIM gebruikt, wordt de levering sneller uitgevoerd als geverifieerde e-mailafzender. Om de snelheid van de berichtlevering te verbeteren, kunt u van Starter aan Pro bevorderen of uw eigen server SMTP of dienstverlener van de e-maillevering gebruiken. Zie [ E-mailverbindingen ](https://experienceleague.adobe.com/nl/docs/commerce-admin/systems/communications/email-communications) in de _gids van Systemen Admin_ vormen.

### Afzender en domeinverificatie

Voor SendGrid om transactie-e-mails namens u van de milieu&#39;s van de Proproductie of van het Staging te verzenden, moet u uw DNS montages vormen om de drie subdomeinDNS ingangen te omvatten SendGrid. Aan elke SendGrid-account wordt een unieke `TXT` -record toegewezen waarmee uitgaande e-mailberichten worden geverifieerd.

>[!TIP]
>
>Zorg ervoor dat u de **[!UICONTROL Sopslag E-mailadressen]** met het juiste domein in **[!UICONTROL Stores > Configuration > General > Store Email Addresses]** vormt. De domeinauthentificatie wordt uitgevoerd op het e-mailadres van de afzender. Als de standaardinstelling (`example.com`) is geconfigureerd, worden de e-mails van `example.com` geblokkeerd door Sendgrid.

**om domeinauthentificatie** toe te laten:

1. Verzend a [ steunkaartje ](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) om het toelaten van DKIM voor een specifiek domein (**Pro het Opvoeren en de milieu&#39;s van de Productie slechts**) te verzoeken.
1. Werk uw DNS-configuratie bij met de `TXT` - en `CNAME` -records die in het ondersteuningsticket aan u worden geleverd.

**Voorbeeld `TXT` verslag met rekeningsidentiteitskaart**:

```text
v=spf1 include:u17504801.wl.sendgrid.net -all
```

**Voorbeeld `CNAME` verslagen**:

| Domein | Punten naar | Recordtype |
| ---------- | ---------- | ------------- |
| em.emaildomain.com | uxxxxxx.wl.sendgrid.net | CNAME |
| s1._domainkey.emaildomain.com | s1.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |
| s2._domainkey.emaildomain.com | s2.domainkey.uxxxxxx.wl.sendgrid.net | CNAME |

### DKIM-handtekeningen en geautomatiseerde beveiliging

U kunt kiezen tussen geautomatiseerde en handmatige beveiliging wanneer u een geverifieerd domein instelt. Als u automatische beveiliging kiest, worden uw DKIM- en SPF-records automatisch door SendGrid beheerd. Wanneer u een nieuw specifiek verzendend IP-adres toevoegt aan uw account, werkt SendGrid direct uw DNS-instellingen en DKIM-handtekening bij. Als u automatische beveiliging uitschakelt, bent u verantwoordelijk voor het bijwerken van uw DKIM-handtekening wanneer u uw verzendend domein wijzigt.

**Geautomatiseerde toegelaten veiligheid van het Voorbeeld**:

```text
subdomain.mydomain.com. | CNAME | uxxxxxx.wl.sendgrid.net
s1._domainkey.mydomain.com. | CNAME | s1.domainkey.uxxxxxx.wl.sendgrid.net
s2._domainkey.mydomain.com. | CNAME | s2.domainkey.uxxxxxx.wl.sendgrid.net
```

**Geautomatiseerde van het Voorbeeld gehandicapte veiligheid**:

```text
me12345.mydomain.com | MX | mx.sendgrid.net
me12345.mydomain.com | TXT | v=spf1 include:sendgrid.net ~all
m1._mydomain.com | TXT | k=rsa; t=s; p=<public-key>
```

Nadat de domeinauthentificatie opstelling is, behandelt SendGrid automatisch het Kader van het Beleid van de Veiligheid (SPF) en de verslagen van DKIM voor u. Nadat SendGrid de `CNAME` verslagen verstrekt om aan uw DNS verslagen toe te voegen, kunt u specifieke IP adressen toevoegen en andere rekeningsupdates maken zonder het moeten uw SPF verslagen manueel beheren. Zie [ Geautomatiseerde Veiligheid en Uw Handtekening van DKIM ](https://docs.sendgrid.com/ui/account-and-settings/dkim-records#automated-security-and-your-dkim-signature).

Om uw DNS configuratie te testen:

```
dig CNAME em.domain_name
dig CNAME s1._domainkey.domain_name
dig CNAME s2._domainkey.domain_name
```

## Drempel voor Transactionele e-mail

De drempel voor transactie-e-mail verwijst naar het aantal transactie-e-mailberichten dat u vanuit Pro-omgevingen binnen een specifieke periode kunt verzenden, zoals 12.000 e-mailberichten per maand vanuit niet-productieomgevingen. De drempel is ontworpen om te beschermen tegen het verzenden van spam en mogelijk uw e-mailreputatie te beschadigen.

Er zijn geen harde grenzen aan het aantal e-mails dat kan worden verzonden in de Productieomgeving, zolang de score voor de reproductie van de afzender meer dan 95% bedraagt. De reputatie wordt beïnvloed door het aantal gebrande of verworpen e-mails en of op DNS-Gebaseerde spamregisters uw domein als potentiële spambron hebben gemarkeerd. Zie [ E-mails niet verzonden wanneer de credits SendGrid op Adobe Commerce ](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/emails-not-being-sent-sendgrid-credits-exceeded) in de _Kennisbank van de Steun van Commerce_ werden overschreden.

**om te controleren als de maximumkredieten** worden overschreden:

1. Wijzig op uw lokale werkstation de projectmap.

1. Gebruik SSH om u aan te melden bij de externe omgeving.

   ```bash
   magento-cloud ssh
   ```

1. Controleer de `/var/log/mail.log` op `authentication failed : Maxium credits exceeded` -items.

   Als u om het even welke `authentication failed` logboekingangen ziet en **E-mail verzendende reputatie** is bij een minimum van 95, kunt u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) voorleggen om een verhoging van de krediettoewijzing te verzoeken.

### E-mailverzendingsreputatie

Een e-mailverzendende reputatie is een score die door een Internet Service Provider (ISP) wordt toegewezen aan een bedrijf dat e-mailberichten verzendt. Hoe hoger de score, des te waarschijnlijker is ISP berichten aan inbox van een ontvanger moet leveren. Als de score onder een bepaald niveau valt, kan ISP berichten aan de spamomslag van ontvangers leiden, of zelfs berichten volledig verwerpen. De reputatie score wordt bepaald door verscheidene factoren zoals een 30 daggemiddelde van uw IP adressen rangschikt tegen andere IP adressen en het tarief van de spamklacht. Zie [ 8 Manieren om Uw E-mail te controleren die Reputatie ](https://sendgrid.com/en-us/blog/5-ways-check-sending-reputation) verzendt.

### E-mailsuppressielijsten

Een lijst met e-mailsuppressies is een lijst met ontvangers waarnaar geen e-mailberichten mogen worden verzonden als dit nadelige gevolgen zou hebben voor uw verzendingsreputatie en leveringspercentages. Het wordt vereist door de CAN-SPAM Akte om ervoor te zorgen dat de e-mailafzenders een methode hebben om ontvangers uit te kiezen die e-mail als spam opsloot of duidelijk maakten. De suppressielijst verzamelt ook e-mails die stuiteren, worden geblokkeerd of ongeldig zijn.

Om e-mails te verhinderen worden verzonden naar de spamomslag in de eerste plaats, volg het beste praktijken artikel van Sendgrid, [ waarom Mijn e-mails naar Spam gaan?](https://sendgrid.com/en-us/blog/10-tips-to-keep-email-out-of-the-spam-folder).

Als sommige ontvangers uw e-mails niet ontvangen, kunt u [ een kaartje van de Steun van Adobe Commerce ](https://experienceleague.adobe.com/nl/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) voorleggen om een overzicht van de suppressielijsten te verzoeken en ontvanger(s) indien nodig te verwijderen.

Voor meer details, verwijs naar [ wat een Lijst van de Onderdrukking is?](https://sendgrid.com/en-us/blog/what-is-a-suppression-list)
